# Coding-agent starter kit

Bộ kit cá nhân này dùng để bắt đầu repo mới hoặc tiếp nhận repo đang phát triển. Template và skill được lưu trong Git của `cstack`; bản tài liệu làm việc ở repo đích nằm trong `.cstack/` và được Git bỏ qua tại máy của bạn. `repo-starter/` là seed cho repo mới; `repo-adopt/` là bộ file trung lập cho repo đã có code.

## Cấu trúc

```text
cstack/
├── global/AGENTS.md                 Mặc định áp dụng trên nhiều repo
├── skills/*/SKILL.md                Bốn workflow dùng lại
├── repo-starter/
│   ├── .cstack/{CONTEXT,PLAN,PROGRESS,VERIFY,FEATURE_MAP}.md
│   ├── .cstack/docs/{features,adr}/
│   └── backend/, docker/, frontend/  Khung ứng dụng chỉ cho repo mới
├── repo-adopt/.cstack/              Chỉ có năm file Markdown cá nhân;
│                                    không tạo thư mục ứng dụng
└── examples/mysql-project/.cstack/CONTEXT.md
```

Hai template **không có sẵn** thư mục `specs/`. Agent chỉ tạo `.cstack/specs/<id>-<slug>/` trong repo đích khi đã xác định một thay đổi cụ thể cần theo dõi. `<slug>` lấy từ tên công việc và quy ước của chính dự án; kit không ấn định một tên feature mẫu.

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

`repo-adopt/` chỉ thêm năm file Markdown dưới `.cstack/`, không tạo `backend/`, `frontend/` hay `docker/`. Trước khi dùng, đối chiếu với chỉ dẫn, tài liệu, lệnh chạy/test và cấu trúc đã có trong repo đích. Không kiểm kê mọi feature hay dựng lại lịch sử cũ trước khi làm yêu cầu hiện tại.

Sau khi sao chép, kiểm tra Git đang bỏ qua file cá nhân và các file dự án khác vẫn hiện bình thường:

```bash
git -C "$TARGET_REPO" check-ignore -v .cstack/PLAN.md
git -C "$TARGET_REPO" status --short
```

Các bản `.cstack/` bị bỏ qua sẽ không theo bạn sang bản clone hoặc máy khác; sao lưu riêng nếu muốn giữ chúng lâu dài. Các thay đổi code, test, contract và quyết định mà nhóm cần biết vẫn phải đi qua tài liệu hoặc quy trình chung của dự án.

## Quy trình spec

Một **spec** là hồ sơ cho một thay đổi có phạm vi và tiêu chí chấp nhận rõ ràng. Dùng spec cho công việc đáng theo dõi qua nhiều bước hoặc phiên làm việc; sửa lỗi nhỏ có thể làm trực tiếp. Chỉ có một spec đang hoạt động. Một yêu cầu triển khai đã rõ phạm vi cho phép bắt đầu ngay; không cần đợi một nghi thức tạo tài liệu.

Khi cần hồ sơ, agent tạo `.cstack/specs/<id>-<slug>/` theo hướng dẫn trong `global/AGENTS.md` và `.cstack/CONTEXT.md`. ID tăng dần như `001`, `002`, trừ khi dự án có quy ước ID sẵn. Tên `<slug>` được chọn từ đầu việc thật của repo đó và có thể theo convention đang dùng. Không tạo `specs/` lúc copy template, không đặt tên trước cho công việc chưa có, và không gán spec hồi tố cho toàn bộ feature đã tồn tại.

| File trong spec | Nội dung |
|---|---|
| `spec.md` | Kết quả người dùng cần, phạm vi, quyết định, tiêu chí chấp nhận. Với repo đã có code, ghi baseline liên quan và phần việc còn lại. |
| `plan.md` | Cách triển khai, rủi ro, cách kiểm chứng. |
| `tasks.md` | Các bước thực hiện và trạng thái; dùng ID cục bộ như `T01` khi hữu ích. |
| `result.md` | Hành vi đã triển khai, code/commit, lệnh và môi trường kiểm chứng, kết quả quan sát, giới hạn và việc còn lại. |

Tạo các file trên khi thông tin tương ứng đã có; không điền nội dung giả định chỉ để đủ bộ. Khi hoàn tất, giữ hồ sơ đó như lịch sử. Thay đổi sau này có spec mới và liên kết về spec cũ. `.cstack/PLAN.md` trỏ tới công việc đang làm; `PROGRESS.md` có chỉ mục spec đã hoàn tất; `VERIFY.md` liên kết bằng chứng mới nhất trong `result.md`. Chúng không chép lại toàn bộ hồ sơ.

## Bắt đầu làm việc trong repo mới

Mở agent tại root repo sau khi cài chỉ dẫn cá nhân. Global `AGENTS.md` chỉ agent tìm `.cstack/CONTEXT.md`; các living doc được đọc theo nhu cầu tác vụ.

> Đây là repo mới. Ý tưởng là ... cho người dùng ... Hãy làm rõ các quyết định quan trọng và xác định thay đổi đầu tiên với tiêu chí chấp nhận quan sát được. Khi phạm vi đã rõ, lập spec cho thay đổi đó và cập nhật `.cstack/PLAN.md`.

Khi spec đã đủ rõ để triển khai:

> Hãy triển khai spec đang hoạt động theo `.cstack/PLAN.md`, kiểm chứng hành vi, cập nhật `result.md` cùng `.cstack/PROGRESS.md` và `.cstack/VERIFY.md`. Nếu luồng người dùng/API thay đổi, cập nhật `.cstack/FEATURE_MAP.md`.

Các prompt mẫu không cần nhắc tên skill: Codex có thể chọn skill phù hợp từ mô tả và chỉ dẫn đã nạp. Nếu muốn chỉ định workflow, thêm `$grill-feature`, `$run-spec`, `$verify-backend` hoặc `$handoff-spec` vào prompt. Đây là cách chọn hướng dẫn trong `SKILL.md`, không phải lệnh terminal hay MCP tool. Nếu vừa cài skill mà nó chưa hiện, mở session Codex mới.

## Tiếp tục làm việc trong repo đã có code

Mở agent tại root repo đích. Đưa yêu cầu hiện tại trực tiếp; agent đọc chỉ dẫn dự án, `.cstack/CONTEXT.md`, code/test/tài liệu liên quan, rồi tiếp tục theo cấu trúc có sẵn. Các file trong `repo-adopt/.cstack/` không khẳng định repo chưa có ứng dụng hay feature nào.

> Repo này đã có code. Hãy tiếp tục feature X theo kiến trúc và quy ước hiện tại. Kiểm tra luồng liên quan và thay đổi dở dang, xác định kết quả quan sát được, triển khai và kiểm chứng trong phạm vi feature X. Nếu cần hồ sơ cho công việc này, hãy tạo spec với tên phù hợp dự án. Cập nhật tài liệu kit dựa trên điều thực sự quan sát; không kiểm kê toàn repo trước khi bắt đầu.

Nếu kit được dùng giữa chừng một feature, `.cstack/PLAN.md` ghi phần việc còn lại; `PROGRESS.md` nêu trạng thái hiện tại và bước tiếp theo. `VERIFY.md` chỉ ghi kết quả vừa được quan sát. `FEATURE_MAP.md` có thể chỉ bao phủ các luồng đã chạm tới; feature chưa khảo sát không cần được suy đoán hoặc liệt kê. Chọn ID cho công việc từ lúc tiếp nhận hoặc theo quy ước dự án; không gán ID hồi tố cho lịch sử cũ.

## Ghi đè theo repo

Mặc định trong `global/AGENTS.md` chỉ áp dụng khi repo chưa chọn khác. Ghi chú cá nhân về quyết định đã xác nhận nằm trong `.cstack/CONTEXT.md`; quyết định cần chia sẻ với nhóm thuộc tài liệu dự án. Ví dụ phần ghi chú cá nhân:

```markdown
## Project decisions that override global defaults

- Database: MySQL 8 for this project. This replaces the global PostgreSQL preference.
- Use MySQL-compatible SQLAlchemy models, Alembic migrations, and MySQL integration tests.
- Do not introduce PostgreSQL-only SQL, extensions, or deployment configuration.
```

Xem [ví dụ MySQL](examples/mysql-project/.cstack/CONTEXT.md) cho một repo mới. Với repo có sẵn, quyết định, lệnh và layout đang dùng được ưu tiên; không tạo `backend/`, `frontend/` hoặc `docker/` chỉ để khớp starter. Nếu một skill có giả định không hợp với repo, chỉnh bản skill cá nhân hoặc tạo skill khác tên. Bốn skill trong bộ này không khóa loại database.

`AGENTS.md` có sẵn ở repo đích tiếp tục là chỉ dẫn của dự án. Không thay nó bằng ghi chú cá nhân.

## Vòng đời tài liệu

Các file `.cstack/` ở repo đích là tài liệu làm việc cá nhân bị Git bỏ qua. Tài liệu chính thức của dự án giữ tên và vị trí hiện hữu.

| File | Cập nhật khi |
|---|---|
| `global/AGENTS.md` | Mặc định dùng chung thay đổi. |
| `.cstack/CONTEXT.md` | Bối cảnh và quyết định cá nhân đã xác nhận thay đổi. |
| `.cstack/PLAN.md` | Spec đang làm, phạm vi ngắn và bước tiếp theo thay đổi. |
| `.cstack/PROGRESS.md` | Trạng thái, blocker, bước tiếp theo hoặc chỉ mục spec đã xong thay đổi. |
| `.cstack/VERIFY.md` | Lệnh dùng lại hoặc kết quả gần nhất thay đổi; liên kết `result.md` cho bằng chứng chi tiết. |
| `.cstack/FEATURE_MAP.md` | Hành trình sản phẩm, trạng thái, đường vào hoặc cách kiểm chứng thay đổi. |
| `.cstack/specs/<id>-<slug>/` | Tạo theo nhu cầu cho thay đổi thật; cập nhật `spec.md`, `plan.md`, `tasks.md`, `result.md` trong quá trình làm. |
| `.cstack/docs/features/` | Chi tiết hành trình dài hơn mức phù hợp cho chỉ mục feature. |
| `.cstack/docs/adr/` | Ghi chú cá nhân về quyết định kiến trúc lâu dài hoặc quyết định cũ bị thay thế. |
| `SKILL.md` | Workflow lặp lại cần thay đổi. |

Với repo mới, agent có thể phác luồng `planned` từ ý tưởng đã chốt; với repo có sẵn, chỉ ghi luồng đã khảo sát và tách trạng thái triển khai khỏi bằng chứng kiểm chứng. Khi bản đồ dài, giữ nó làm mục lục và liên kết tới `.cstack/docs/features/`. Trước khi rút ngắn living doc, chuyển thông tin duy nhất vào spec hoặc ghi chú quyết định và để lại con trỏ. Không ghi `passed` nếu chưa chạy kiểm chứng.

## Nguồn cảm hứng

Bộ kit này học hỏi từ [grill-me của Matt Pocock](https://www.aihero.dev/skills-grill-me) ([mã nguồn](https://github.com/mattpocock/skills)) và [chia sẻ của Lauren Tan về coding agents](https://www.youtube.com/watch?v=EWSUvEyFwjc), cùng [pstack của Lauren Tan](https://github.com/cursor/plugins/tree/main/pstack). Các quy ước và skill trong repo đã được điều chỉnh cho workflow của bộ kit này.
