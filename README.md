# Coding-agent starter kit

Bộ kit cá nhân này dùng để bắt đầu repo mới hoặc tiếp nhận repo đang phát triển. Template và skill được lưu trong Git của `cstack`; bản tài liệu làm việc ở repo đích nằm trong `.cstack/` và được Git bỏ qua tại máy của bạn. `repo-starter/` là seed cho repo mới; `repo-adopt/` là bộ file trung lập cho repo đã có code.

## Cấu trúc

```text
cstack/
├── global/AGENTS.md                 Mặc định áp dụng trên nhiều repo
├── skills/*/SKILL.md                Bốn workflow dùng lại
├── repo-starter/
│   ├── .cstack/{CONTEXT,PLAN,PROGRESS,VERIFY,FEATURE_MAP}.md
│   ├── .cstack/docs/{phases,features,adr}/
│   └── backend/, docker/, frontend/  Khung ứng dụng chỉ cho repo mới
├── repo-adopt/.cstack/              Chỉ có năm file Markdown cá nhân;
│                                    không tạo thư mục ứng dụng
└── examples/mysql-project/.cstack/CONTEXT.md
```

## Cài đặt chỉ dẫn và skill cá nhân

Đặt `global/AGENTS.md` trong Codex home và các skill trong thư mục skill cá nhân. Chỉ đặt một bản của mỗi skill để tránh trùng tên. Nếu file đích đã có nội dung, so sánh và gộp thay vì ghi đè.

```bash
KIT=/path/to/cstack
mkdir -p "$HOME/.codex" "$HOME/.agents/skills"
cp --update=none "$KIT/global/AGENTS.md" "$HOME/.codex/AGENTS.md"
cp -a --update=none "$KIT/skills/." "$HOME/.agents/skills/"
```

Codex tự nạp `~/.codex/AGENTS.md` và `AGENTS.md` trên đường từ repo root tới thư mục làm việc. Khi mở agent ở repo root, nó **không** tự nạp `.cstack/CONTEXT.md` nằm bên dưới; global `AGENTS.md` của kit chỉ agent đọc file đó khi có. Giữ `AGENTS.md` đã được repo theo dõi bằng Git; nó vẫn là chỉ dẫn của dự án. Xem [OpenAI Docs về AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md).

## Cài tài liệu cá nhân vào repo đích

Các lệnh sau dùng GNU `cp --update=none`, nên bỏ qua file đích đã tồn tại. Thay đường dẫn mẫu bằng đường dẫn thật.

Trước tiên, dùng một repo đã `git init` hoặc clone và thêm quy tắc bỏ qua **chỉ cho bản clone này**:

```bash
TARGET_REPO=/path/to/project
(
  cd "$TARGET_REPO" || exit 1
  EXCLUDE_PATH=$(git rev-parse --git-path info/exclude) || exit 1
  touch "$EXCLUDE_PATH"
  grep -Fxq '/.cstack/' "$EXCLUDE_PATH" || printf '/.cstack/\n' >> "$EXCLUDE_PATH"
)
```

`/.cstack/` chỉ khớp thư mục `.cstack` ở root. `.git/info/exclude` thuộc bản clone, không được commit và không áp quy tắc này cho đồng đội. `.gitignore` trong repo thường được chia sẻ; `core.excludesFile` là lựa chọn cá nhân ở mức mọi repo trên máy. Git ignore chỉ tác động file chưa được theo dõi: nếu `git ls-files .cstack` có kết quả, cần xử lý các file đã tracked một cách riêng, không dựa vào exclude. Xem [tài liệu Git về ignore](https://git-scm.com/docs/gitignore).

**Tạo repo mới:**

```bash
KIT=/path/to/cstack
TARGET_REPO=/path/to/new-repo
cp -a --update=none "$KIT/repo-starter/." "$TARGET_REPO/"
```

`repo-starter/` cung cấp tài liệu cá nhân trong `.cstack/` và khung `backend/`, `docker/`, `frontend/` khi bạn có quyền chọn cấu trúc ứng dụng. Không commit `.cstack/`; các thư mục ứng dụng là phần của repo dự án nếu bạn quyết định dùng chúng.

**Tiếp nhận repo đã có code:**

```bash
KIT=/path/to/cstack
TARGET_REPO=/path/to/existing-repo
cp -a --update=none "$KIT/repo-adopt/." "$TARGET_REPO/"
```

`repo-adopt/` chỉ thêm năm file Markdown dưới `.cstack/`, không tạo `backend/`, `frontend/` hay `docker/`. Trước khi dùng, đối chiếu với chỉ dẫn, tài liệu, lệnh chạy/test và cấu trúc đã có trong repo đích. Không kiểm kê mọi feature hay dựng lại lịch sử phase trước khi làm yêu cầu hiện tại.

Sau khi sao chép, kiểm tra Git đang bỏ qua file cá nhân và các file dự án khác vẫn hiện bình thường:

```bash
git -C "$TARGET_REPO" check-ignore -v .cstack/PLAN.md
git -C "$TARGET_REPO" status --short
```

Các bản `.cstack/` bị bỏ qua sẽ không theo bạn sang bản clone hoặc máy khác; sao lưu riêng nếu muốn giữ chúng lâu dài. Các thay đổi code, test, contract và quyết định mà nhóm cần biết vẫn phải đi qua tài liệu hoặc quy trình chung của dự án.

## Bắt đầu làm việc trong repo mới

Mở agent tại root repo sau khi cài chỉ dẫn cá nhân. Global `AGENTS.md` chỉ agent tìm `.cstack/CONTEXT.md`; các living docs được đọc theo nhu cầu của tác vụ.

> Đây là repo mới. Ý tưởng là ... cho người dùng ... Hãy làm rõ các quyết định quan trọng, rồi cập nhật `.cstack/PLAN.md` cho phase đầu. Chỉ hỏi những gì không suy ra được từ yêu cầu hoặc repo.

`P-00.1` trong starter là bước xác định vertical slice đầu tiên, chưa phải phần triển khai code. Khi `.cstack/PLAN.md` đã có một slice triển khai đủ rõ và bạn muốn bắt đầu (ví dụ `P-01.1`):

> Hãy triển khai P-01.1 theo `.cstack/PLAN.md`, kiểm chứng hành vi, cập nhật `.cstack/PROGRESS.md` và `.cstack/VERIFY.md`. Nếu luồng người dùng/API thay đổi, cập nhật `.cstack/FEATURE_MAP.md`.

Các prompt mẫu không cần nhắc tên skill: Codex có thể chọn skill phù hợp từ mô tả và chỉ dẫn đã nạp. Nếu muốn chỉ định workflow cho một yêu cầu, thêm `$grill-feature`, `$run-phase`, `$verify-backend` hoặc `$handoff-phase` vào prompt. Đây là cách chọn hướng dẫn trong `SKILL.md`, không phải lệnh terminal hay MCP tool. Nếu vừa cài skill mà nó chưa hiện, mở session Codex mới.

## Tiếp tục làm việc trong repo đã có code

Mở agent tại root repo đích. Đưa yêu cầu hiện tại trực tiếp; agent đọc chỉ dẫn của dự án, `.cstack/CONTEXT.md`, code/test/tài liệu liên quan, rồi tiếp tục công việc theo cấu trúc có sẵn. Các file trong `repo-adopt/.cstack/` không khẳng định repo chưa có ứng dụng hay feature nào.

> Repo này đã có code. Hãy tiếp tục feature X theo kiến trúc và quy ước hiện tại. Kiểm tra luồng liên quan và các thay đổi dở dang, xác định kết quả quan sát được, triển khai và kiểm chứng trong phạm vi feature X. Cập nhật tài liệu kit dựa trên điều thực sự quan sát; không kiểm kê toàn repo trước khi bắt đầu.

Nếu việc dùng kit bắt đầu giữa chừng một feature, `.cstack/PLAN.md` ghi phần việc còn lại; PROGRESS nêu trạng thái hiện tại và bước tiếp theo. VERIFY chỉ ghi kết quả vừa được quan sát. FEATURE_MAP có thể chỉ bao phủ các luồng đã chạm tới; feature chưa khảo sát không cần được suy đoán hoặc liệt kê. Dùng ID mới cho công việc từ lúc tiếp nhận, hoặc theo quy ước ID của repo; không gán ID hồi tố cho lịch sử cũ.

## Ghi đè theo repo

Mặc định trong `global/AGENTS.md` chỉ áp dụng khi repo chưa chọn khác. Ghi chú cá nhân về quyết định đã xác nhận nằm trong `.cstack/CONTEXT.md`; quyết định cần chia sẻ với nhóm thuộc tài liệu dự án. Ví dụ phần ghi chú cá nhân:

```markdown
## Project decisions that override global defaults

- Database: MySQL 8 for this project. This replaces the global PostgreSQL preference.
- Use MySQL-compatible SQLAlchemy models, Alembic migrations, and MySQL integration tests.
- Do not introduce PostgreSQL-only SQL, extensions, or deployment configuration.
```

Xem [`examples/mysql-project/.cstack/CONTEXT.md`](examples/mysql-project/.cstack/CONTEXT.md) cho ví dụ đầy đủ của repo mới. Với repo có sẵn, quyết định, lệnh và layout đang dùng được ưu tiên; không tạo `backend/`, `frontend/` hoặc `docker/` chỉ để khớp starter. Nếu một skill có giả định không hợp với repo, chỉnh bản skill cá nhân hoặc tạo skill khác tên. Bốn skill trong bộ này không khóa loại database.

`AGENTS.md` có sẵn ở repo đích tiếp tục là chỉ dẫn của dự án. Không thay nó bằng ghi chú cá nhân.

## Vòng đời tài liệu

Bảng dưới mô tả các file cá nhân trong `.cstack/` của repo đích. Chúng là tài liệu làm việc bị Git bỏ qua. Tài liệu chính thức của dự án giữ tên và vị trí hiện hữu.

| File | Cập nhật khi |
|---|---|
| `global/AGENTS.md` | Mặc định dùng chung thay đổi. |
| `.cstack/CONTEXT.md` | Ghi nhận bối cảnh và quyết định cá nhân đã được xác nhận. |
| `.cstack/PLAN.md` | Chốt hoặc đổi slice hiện tại; giữ lại kết quả và bằng chứng cũ trước khi thay nội dung. |
| `.cstack/PROGRESS.md` | Trạng thái, blocker, bước tiếp theo hoặc con trỏ báo cáo thay đổi; không dùng làm nhật ký toàn bộ lịch sử. |
| `.cstack/VERIFY.md` | Lệnh dùng lại hoặc kết quả gần nhất thay đổi; bằng chứng chi tiết nằm trong báo cáo khi cần. |
| `.cstack/FEATURE_MAP.md` | Hành trình sản phẩm, trạng thái, đường vào hoặc cách kiểm chứng thay đổi. |
| `.cstack/docs/phases/` | Một child slice xong hoặc parent phase đóng: lưu kết quả, code/commit, lệnh và môi trường kiểm chứng, kết quả quan sát, việc còn lại. |
| `.cstack/docs/features/` | Chi tiết một hành trình dài hơn mức phù hợp cho chỉ mục `FEATURE_MAP.md`. |
| `.cstack/docs/adr/` | Ghi chú cá nhân về quyết định kiến trúc lâu dài hoặc quyết định cũ bị thay thế. |
| `SKILL.md` | Workflow lặp lại cần thay đổi. |

`.cstack/FEATURE_MAP.md` riêng cho từng repo. Với repo mới, agent có thể phác luồng `planned` từ ý tưởng đã chốt; với repo có sẵn, chỉ ghi các luồng đã khảo sát và tách trạng thái triển khai khỏi bằng chứng kiểm chứng. Khi bản đồ dài, giữ nó làm mục lục và liên kết tới `.cstack/docs/features/`. Với phase liên quan nhiều thành phần, chọn một báo cáo chính. Trước khi rút ngắn living doc, chuyển mọi thông tin duy nhất vào báo cáo hoặc ghi chú quyết định và để lại con trỏ. Không ghi `passed` nếu chưa chạy kiểm chứng.

## Nguồn cảm hứng

Bộ kit này học hỏi từ [grill-me của Matt Pocock](https://www.aihero.dev/skills-grill-me) ([mã nguồn](https://github.com/mattpocock/skills)) và [chia sẻ của Lauren Tan về coding agents](https://www.youtube.com/watch?v=EWSUvEyFwjc), cùng [pstack của Lauren Tan](https://github.com/cursor/plugins/tree/main/pstack). Các quy ước và skill trong repo đã được điều chỉnh cho workflow của bộ kit này.
