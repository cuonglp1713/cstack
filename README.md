# Coding-agent starter kit

Bộ kit này dùng để bắt đầu repo mới hoặc tiếp nhận repo đang phát triển. `repo-starter/` là seed cho repo mới; `repo-adopt/` là bộ file trung lập cho repo đã có code. Cả hai là mẫu để điều chỉnh theo repo đích, không phải mô tả trạng thái của chính `cstack`.

## Cấu trúc

```text
cstack/
├── global/AGENTS.md                 Mặc định áp dụng trên nhiều repo
├── skills/*/SKILL.md                Bốn workflow dùng lại
├── repo-starter/
│   ├── AGENTS.md                    Chỉ dẫn và cách quản lý tài liệu của repo
│   ├── PLAN.md                      Phase/slice hiện tại
│   ├── PROGRESS.md                  Trạng thái và chỉ mục báo cáo phase
│   ├── VERIFY.md                    Lệnh kiểm chứng và kết quả gần nhất
│   ├── FEATURE_MAP.md               Chỉ mục hành trình sản phẩm của repo
│   ├── backend/docs/{phases,features,adr}/
│   ├── docker/
│   └── frontend/docs/{phases,features,adr}/
├── repo-adopt/                      Chỉ có AGENTS, PLAN, PROGRESS, VERIFY,
│                                    FEATURE_MAP; không tạo thư mục ứng dụng
└── examples/mysql-project/AGENTS.md  Ví dụ ghi đè lựa chọn database
```

## Cài đặt

Có thể dùng skill cho mọi repo qua `~/.agents/skills/`, hoặc chỉ cho một repo qua `<repo>/.agents/skills/`. Chỉ đặt một bản của mỗi skill để tránh trùng tên. `global/AGENTS.md` là tùy chọn; sao chép vào `~/.codex/AGENTS.md` nếu muốn các mặc định đó áp dụng trong mọi repo. Nếu file đích đã có nội dung, so sánh và gộp thay vì ghi đè.

Các lệnh dưới đây dùng GNU `cp --update=none`, nên bỏ qua file đích đã tồn tại. Thay các đường dẫn mẫu bằng đường dẫn của bộ kit và repo đích. Khi cập nhật một bản đã cài, so sánh và đồng bộ file hiện có; lệnh sao chép này không cập nhật chúng.

**Tạo repo mới với tài liệu và skill trong repo:**

```bash
KIT=/path/to/cstack
TARGET_REPO=/path/to/new-repo
mkdir -p "$TARGET_REPO/.agents/skills"
cp -a --update=none "$KIT/repo-starter/." "$TARGET_REPO/"
cp -a --update=none "$KIT/skills/." "$TARGET_REPO/.agents/skills/"
```

**Tiếp nhận repo đã có code:**

```bash
KIT=/path/to/cstack
TARGET_REPO=/path/to/existing-repo
mkdir -p "$TARGET_REPO/.agents/skills"
cp -a --update=none "$KIT/repo-adopt/." "$TARGET_REPO/"
cp -a --update=none "$KIT/skills/." "$TARGET_REPO/.agents/skills/"
```

`repo-adopt/` chỉ chứa năm file Markdown, không có `backend/`, `frontend/` hay `docker/`. Trước khi dùng, đối chiếu với chỉ dẫn, tài liệu, lệnh chạy/test và cấu trúc đã có trong repo đích. Lệnh sao chép bỏ qua file trùng tên: nếu repo đã có `AGENTS.md`, PLAN, tài liệu kiểm chứng hoặc skill cùng tên, đọc và gộp phần phù hợp; không thay thế nội dung hiện có. Không cần kiểm kê mọi feature hay dựng lại lịch sử phase trước khi làm yêu cầu hiện tại.

**Cài mặc định và skill dùng chung:**

```bash
KIT=/path/to/cstack
mkdir -p "$HOME/.codex" "$HOME/.agents/skills"
cp --update=none "$KIT/global/AGENTS.md" "$HOME/.codex/AGENTS.md"
cp -a --update=none "$KIT/skills/." "$HOME/.agents/skills/"
```

Dù cài skill dùng chung, mỗi repo vẫn cần tài liệu trạng thái riêng: dùng `repo-starter/.` cho repo mới hoặc tiếp nhận chọn lọc từ `repo-adopt/.` cho repo có sẵn. Giữ các tài liệu đã dùng trong Git.

## Bắt đầu làm việc trong repo mới

Mở agent tại root repo. Codex tự đọc `AGENTS.md` và khám phá metadata skill; nó đọc PLAN, PROGRESS, VERIFY và FEATURE_MAP theo chỉ dẫn hoặc nhu cầu của tác vụ.

> Đây là repo mới. Ý tưởng là ... cho người dùng ... Hãy làm rõ các quyết định quan trọng, rồi cập nhật PLAN.md cho phase đầu. Chỉ hỏi những gì không suy ra được từ yêu cầu hoặc repo.

`P-00.1` trong starter là bước xác định vertical slice đầu tiên, chưa phải phần triển khai code. Khi `PLAN.md` đã có một slice triển khai đủ rõ và bạn muốn bắt đầu (ví dụ `P-01.1`):

> Hãy triển khai P-01.1 theo PLAN.md, kiểm chứng hành vi, cập nhật PROGRESS.md và VERIFY.md. Nếu luồng người dùng/API thay đổi, cập nhật FEATURE_MAP.md.

Các prompt mẫu không cần nhắc tên skill: Codex có thể chọn skill phù hợp từ mô tả và chỉ dẫn trong `AGENTS.md`. Nếu muốn chỉ định workflow cho một yêu cầu, thêm `$grill-feature`, `$run-phase`, `$verify-backend` hoặc `$handoff-phase` vào prompt. Đây là cách chọn hướng dẫn trong `SKILL.md`, không phải lệnh terminal hay MCP tool. Nếu vừa cài skill mà nó chưa hiện, mở session Codex mới.

## Tiếp tục làm việc trong repo đã có code

Mở agent tại root repo đích. Đưa yêu cầu hiện tại trực tiếp; agent đọc chỉ dẫn và phần code/test/tài liệu liên quan, rồi tiếp tục công việc theo cấu trúc có sẵn. Các file trong `repo-adopt/` không khẳng định repo chưa có ứng dụng hay feature nào.

> Repo này đã có code. Hãy tiếp tục feature X theo kiến trúc và quy ước hiện tại. Kiểm tra luồng liên quan và các thay đổi dở dang, xác định kết quả quan sát được, triển khai và kiểm chứng trong phạm vi feature X. Cập nhật tài liệu kit dựa trên điều thực sự quan sát; không kiểm kê toàn repo trước khi bắt đầu.

Nếu việc dùng kit bắt đầu giữa chừng một feature, PLAN ghi phần việc còn lại; PROGRESS nêu trạng thái hiện tại và bước tiếp theo. VERIFY chỉ ghi kết quả vừa được quan sát. FEATURE_MAP có thể chỉ bao phủ các luồng đã chạm tới; feature chưa khảo sát không cần được suy đoán hoặc liệt kê. Dùng ID mới cho công việc từ lúc tiếp nhận, hoặc theo quy ước ID của repo; không gán ID hồi tố cho lịch sử cũ.

## Ghi đè theo repo

Mặc định trong `global/AGENTS.md` chỉ áp dụng khi repo chưa chọn khác. Ghi quyết định riêng vào `AGENTS.md` của repo. Ví dụ:

```markdown
## Project decisions that override global defaults

- Database: MySQL 8 for this project. This replaces the global PostgreSQL preference.
- Use MySQL-compatible SQLAlchemy models, Alembic migrations, and MySQL integration tests.
- Do not introduce PostgreSQL-only SQL, extensions, or deployment configuration.
```

Xem [`examples/mysql-project/AGENTS.md`](examples/mysql-project/AGENTS.md) cho ví dụ đầy đủ của repo mới. Với repo có sẵn, quyết định, lệnh và layout đang dùng được ưu tiên; không tạo `backend/`, `frontend/` hoặc `docker/` chỉ để khớp starter. Nếu một skill có giả định không hợp với repo, chỉnh bản skill trong repo hoặc tạo skill khác tên. Bốn skill trong bộ này không khóa loại database.

`AGENTS.override.md` chỉ cần khi muốn thay toàn bộ `AGENTS.md` trong cùng một thư mục; quyết định như MySQL có thể ghi trực tiếp vào `AGENTS.md` của repo.

## Vòng đời tài liệu

Bảng dưới mô tả nội dung cần giữ khi repo dùng các file của kit. Với repo được tiếp nhận, giữ tên và vị trí tài liệu hiện hữu khi chúng đã phục vụ cùng mục đích; chỉ gộp phần cần thiết. Đường dẫn `backend/docs/` và `frontend/docs/` dưới đây là layout của starter cho repo mới, không phải yêu cầu tái cấu trúc repo có sẵn.

| File | Cập nhật khi |
|---|---|
| `global/AGENTS.md` | Mặc định dùng chung thay đổi. |
| Repo `AGENTS.md` | Stack, kiến trúc, layout hoặc ràng buộc của repo thay đổi. |
| `PLAN.md` | Chốt hoặc đổi slice hiện tại; giữ lại kết quả và bằng chứng cũ trong vị trí tài liệu phù hợp trước khi thay nội dung. |
| `PROGRESS.md` | Trạng thái, blocker, bước tiếp theo hoặc con trỏ báo cáo thay đổi; không dùng làm nhật ký toàn bộ lịch sử. |
| `VERIFY.md` | Lệnh dùng lại hoặc kết quả gần nhất thay đổi; lưu bằng chứng chi tiết ở báo cáo khi repo dùng loại báo cáo đó. |
| `FEATURE_MAP.md` | Hành trình sản phẩm, trạng thái, đường vào hoặc cách kiểm chứng thay đổi. |
| `backend/docs/phases/` hoặc `frontend/docs/phases/` | Một child slice xong hoặc parent phase đóng: lưu kết quả, code/commit, lệnh và môi trường kiểm chứng, kết quả quan sát, việc còn lại. |
| `backend/docs/features/` hoặc `frontend/docs/features/` | Chi tiết một hành trình dài hơn mức phù hợp cho chỉ mục `FEATURE_MAP.md`. |
| `backend/docs/adr/` hoặc `frontend/docs/adr/` | Có quyết định kiến trúc lâu dài hoặc quyết định cũ bị thay thế. |
| `SKILL.md` | Workflow lặp lại cần thay đổi. |

`FEATURE_MAP.md` riêng cho từng repo. Với repo mới, agent có thể phác luồng `planned` từ ý tưởng đã chốt; với repo có sẵn, chỉ ghi các luồng đã khảo sát và tách trạng thái triển khai khỏi bằng chứng kiểm chứng. Khi bản đồ dài, giữ nó làm mục lục và liên kết tới tài liệu chi tiết theo layout của repo. Với phase liên quan nhiều thành phần, chọn một báo cáo chính và liên kết tới đó. Trước khi rút ngắn file gốc, chuyển mọi thông tin duy nhất vào báo cáo hoặc ADR và để lại con trỏ. Không ghi `passed` nếu chưa chạy kiểm chứng.

## Nguồn cảm hứng

Bộ kit này học hỏi từ [grill-me của Matt Pocock](https://www.aihero.dev/skills-grill-me) ([mã nguồn](https://github.com/mattpocock/skills)) và [chia sẻ của Lauren Tan về coding agents](https://www.youtube.com/watch?v=EWSUvEyFwjc), cùng [pstack của Lauren Tan](https://github.com/cursor/plugins/tree/main/pstack). Các quy ước và skill trong repo đã được điều chỉnh cho workflow của bộ kit này.
