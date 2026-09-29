# Coding-agent starter kit

Bộ mẫu này dùng để bắt đầu một repo mới. `repo-starter/` chưa mô tả sản phẩm đã triển khai: agent phải thay các trạng thái “chưa quyết định” bằng dữ kiện của repo.

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

**Cài mặc định và skill dùng chung:**

```bash
KIT=/path/to/cstack
mkdir -p "$HOME/.codex" "$HOME/.agents/skills"
cp --update=none "$KIT/global/AGENTS.md" "$HOME/.codex/AGENTS.md"
cp -a --update=none "$KIT/skills/." "$HOME/.agents/skills/"
```

Dù cài skill dùng chung, vẫn sao chép `repo-starter/.` vào từng repo mới để có tài liệu trạng thái riêng. Giữ các tài liệu đó trong Git.

## Bắt đầu làm việc

Mở agent tại root repo. Codex tự đọc `AGENTS.md` và khám phá metadata skill; nó đọc PLAN, PROGRESS, VERIFY và FEATURE_MAP theo chỉ dẫn hoặc nhu cầu của tác vụ.

> Đây là repo mới. Ý tưởng là ... cho người dùng ... Hãy đọc AGENTS.md, dùng grill-feature để làm rõ các quyết định quan trọng, rồi cập nhật PLAN.md cho phase đầu. Chỉ hỏi những gì không suy ra được từ yêu cầu hoặc repo.

Khi slice đã rõ:

> Hãy triển khai P-00.1 theo PLAN.md, kiểm chứng hành vi, cập nhật PROGRESS.md và VERIFY.md. Nếu đã có luồng người dùng/API, cập nhật FEATURE_MAP.md.

Có thể gọi trực tiếp `$grill-feature`, `$run-phase`, `$verify-backend`, `$handoff-phase`. Nếu vừa cài skill mà nó chưa hiện, mở session Codex mới.

## Ghi đè theo repo

Mặc định trong `global/AGENTS.md` chỉ áp dụng khi repo chưa chọn khác. Ghi quyết định riêng vào `AGENTS.md` của repo. Ví dụ:

```markdown
## Project decisions that override global defaults

- Database: MySQL 8 for this project. This replaces the global PostgreSQL preference.
- Use MySQL-compatible SQLAlchemy models, Alembic migrations, and MySQL integration tests.
- Do not introduce PostgreSQL-only SQL, extensions, or deployment configuration.
```

Xem [`examples/mysql-project/AGENTS.md`](examples/mysql-project/AGENTS.md) cho ví dụ đầy đủ. Nếu một skill có giả định không hợp với repo, chỉnh bản skill trong repo hoặc tạo skill khác tên. Bốn skill trong bộ này không khóa loại database.

`AGENTS.override.md` chỉ cần khi muốn thay toàn bộ `AGENTS.md` trong cùng một thư mục; quyết định như MySQL có thể ghi trực tiếp vào `AGENTS.md` của repo.

## Vòng đời tài liệu

| File | Cập nhật khi |
|---|---|
| `global/AGENTS.md` | Mặc định dùng chung thay đổi. |
| Repo `AGENTS.md` | Stack, kiến trúc, layout hoặc ràng buộc của repo thay đổi. |
| `PLAN.md` | Chốt hoặc đổi slice hiện tại; lưu kết quả cũ vào báo cáo phase trước khi thay nội dung. |
| `PROGRESS.md` | Trạng thái, blocker, bước tiếp theo hoặc con trỏ phase thay đổi; giữ một dòng cho mỗi parent phase. |
| `VERIFY.md` | Lệnh dùng lại hoặc kết quả gần nhất thay đổi; bằng chứng cũ ở báo cáo phase. |
| `FEATURE_MAP.md` | Hành trình sản phẩm, trạng thái, đường vào hoặc cách kiểm chứng thay đổi. |
| `backend/docs/phases/` hoặc `frontend/docs/phases/` | Một child slice xong hoặc parent phase đóng: lưu kết quả, code/commit, lệnh và môi trường kiểm chứng, kết quả quan sát, việc còn lại. |
| `backend/docs/features/` hoặc `frontend/docs/features/` | Chi tiết một hành trình dài hơn mức phù hợp cho chỉ mục `FEATURE_MAP.md`. |
| `backend/docs/adr/` hoặc `frontend/docs/adr/` | Có quyết định kiến trúc lâu dài hoặc quyết định cũ bị thay thế. |
| `SKILL.md` | Workflow lặp lại cần thay đổi. |

`FEATURE_MAP.md` riêng cho từng repo. Agent có thể phác luồng `planned` từ ý tưởng đã chốt, tìm đường đi trong code/UI/routes/tests, rồi kiểm chứng trước khi ghi `verified`. Khi bản đồ dài, giữ nó làm mục lục và liên kết tới file chi tiết trong component sở hữu. Với phase liên quan cả backend lẫn frontend, chọn một báo cáo chính và liên kết tới đó. Trước khi rút ngắn file gốc, chuyển mọi thông tin duy nhất vào báo cáo hoặc ADR và để lại con trỏ. Không ghi `passed` nếu chưa chạy kiểm chứng.

## Nguồn cảm hứng

Bộ kit này học hỏi từ [grill-me của Matt Pocock](https://www.aihero.dev/skills-grill-me) ([mã nguồn](https://github.com/mattpocock/skills)) và [chia sẻ của Lauren Tan về coding agents](https://www.youtube.com/watch?v=EWSUvEyFwjc), cùng [pstack của Lauren Tan](https://github.com/cursor/plugins/tree/main/pstack). Các quy ước và skill trong repo đã được điều chỉnh cho workflow của bộ kit này.
