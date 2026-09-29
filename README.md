# Personal coding-agent starter kit

Bộ này dùng để bắt đầu **repo cá nhân mới**, chưa có code. Nó không chứa trạng thái hay contract của dự án bất kỳ. Các file trong `repo-starter/` là seed có chủ đích: agent phải thay nội dung “chưa quyết định” bằng dữ kiện của dự án, không được coi đó là tính năng đã triển khai.

## Cấu trúc

```text
cstack/
├── global/AGENTS.md                Mặc định cá nhân cho Codex
├── skills/*/SKILL.md               Bốn workflow dùng lại
├── repo-starter/
│   ├── AGENTS.md                   Chỉ dẫn riêng của repo
│   ├── PLAN.md                     Phase và acceptance criteria hiện tại
│   ├── PROGRESS.md                 Trạng thái ngắn để handoff
│   ├── VERIFY.md                   Cách chứng minh và bằng chứng thực tế
│   └── FEATURE_MAP.md              Bản đồ luồng người dùng/API
└── examples/mysql-project/AGENTS.md Ví dụ repo ghi đè PostgreSQL
```

## Cài đặt khuyến nghị cho các dự án cá nhân

1. Đọc `global/AGENTS.md`, rồi **tự sao chép** nó vào `~/.codex/AGENTS.md` nếu muốn mặc định cá nhân có hiệu lực trong mọi repo Codex. Nếu file đích đã tồn tại, gộp có chọn lọc; đừng ghi đè mù.
2. Sao chép từng thư mục trong `skills/` vào `~/.agents/skills/` nếu muốn bốn skill dùng ở mọi repo. Hoặc đặt chúng trong `<repo>/.agents/skills/` nếu chỉ muốn dùng trong repo đó. Chọn một vị trí cho cùng tên skill để tránh mục trùng trong danh sách.
3. Với repo mới, sao chép **nội dung** `repo-starter/` vào root repo; sau đó mở Codex tại root repo. Giữ các file này trong Git để session sau có cùng context.
4. Tin nhắn mở đầu mẫu:

   > Đây là repo mới. Ý tưởng của tôi là ... cho người dùng ... Hãy đọc AGENTS.md, dùng personal-grill-feature để làm rõ các quyết định quan trọng, rồi cập nhật PLAN.md cho phase đầu. Chỉ hỏi những gì không suy ra được từ lời tôi hoặc repo.

5. Khi đã có scope cụ thể:

   > Hãy triển khai P-00.1 theo PLAN.md, kiểm chứng hành vi, cập nhật PROGRESS.md và VERIFY.md. Nếu đã có luồng người dùng/API, cập nhật FEATURE_MAP.md.

Codex tự nạp `AGENTS.md` ở đầu session và quét metadata skill trong `.agents/skills`; các file PLAN/PROGRESS/VERIFY/FEATURE_MAP được đọc nhờ chỉ dẫn trong `AGENTS.md` hoặc khi công việc cần. Có thể gọi trực tiếp `$personal-grill-feature`, `$personal-run-phase`, `$personal-verify-backend`, `$personal-handoff-phase` để chọn workflow rõ ràng. Nếu vừa cài skill mà nó chưa hiện, mở session Codex mới.

## Lệnh sao chép tham khảo

Thay đường dẫn `NEW_REPO` bằng repo mới của bạn. Các lệnh `cp --update=none` (GNU coreutils) không ghi đè file đã có; nếu đích đã tồn tại, hãy so sánh và gộp thủ công.

**Giữ mọi thứ trong từng repo cá nhân** (không ảnh hưởng repo công ty):

```bash
KIT=/home/cuong/workspace/fsoft/my-skills
NEW_REPO=/absolute/path/to/new-repo
mkdir -p "$NEW_REPO/.agents/skills"
cp -a --update=none "$KIT/repo-starter/." "$NEW_REPO/"
cp -a --update=none "$KIT/skills/." "$NEW_REPO/.agents/skills/"
```

**Dùng mặc định cá nhân cho mọi repo Codex** (bao gồm repo công ty, trừ khi repo ghi đè):

```bash
KIT=/home/cuong/workspace/fsoft/my-skills
mkdir -p "$HOME/.codex" "$HOME/.agents/skills"
cp --update=none "$KIT/global/AGENTS.md" "$HOME/.codex/AGENTS.md"
cp -a --update=none "$KIT/skills/." "$HOME/.agents/skills/"
```

Với cách global, vẫn sao chép `repo-starter/.` vào từng repo mới để có các tài liệu trạng thái riêng. Không đặt cùng một skill ở cả global và repo nếu không có mục đích rõ ràng.

## Ghi đè mặc định trong một repo

`global/AGENTS.md` dùng chữ **ưu tiên**, không khóa stack. Repo `AGENTS.md` được nạp sau file cá nhân nên có thể ghi một quyết định cụ thể thay thế mặc định. Ví dụ, ở repo A thêm:

```markdown
## Project decisions that override personal defaults

- Database: MySQL 8 for this project. This replaces the personal PostgreSQL preference.
- Use MySQL-compatible SQLAlchemy models, Alembic migrations, and MySQL integration tests.
- Do not introduce PostgreSQL-only SQL, extensions, or deployment configuration.
```

Xem file hoàn chỉnh tại `examples/mysql-project/AGENTS.md`. Nếu một skill cũng có giả định PostgreSQL, sửa **bản skill ở repo** hoặc thêm skill riêng ở repo với tên khác; đừng để hai skill cùng tên và nội dung trái nhau. Bốn skill trong bộ này không khóa loại database.

`AGENTS.override.md` không cần cho ví dụ trên. Trong cùng một thư mục, Codex chọn `AGENTS.override.md` **thay cho** `AGENTS.md`; dùng nó khi thật sự muốn thay toàn bộ chỉ dẫn của thư mục đó. Repo `AGENTS.md` thông thường đã đủ để ghi đè `~/.codex/AGENTS.md`.

Lưu ý: file cá nhân trong `~/.codex/AGENTS.md` cũng xuất hiện khi bạn mở repo công ty. Nếu không muốn điều đó, đừng cài global; đặt các skill tại `.agents/skills/` và mang những mặc định cần thiết vào `AGENTS.md` của từng repo cá nhân. Có thể dùng một `CODEX_HOME` riêng cho profile cá nhân, nhưng đường dẫn skill người dùng `~/.agents/skills` vẫn cần quản lý riêng.

## Khi nào sửa file nào

| File | Sửa khi |
|---|---|
| Global `AGENTS.md` | Một sở thích của bạn thay đổi trên nhiều dự án. |
| Repo `AGENTS.md` | Dự án có stack, kiến trúc, lệnh chạy/test hoặc ràng buộc riêng. |
| `PLAN.md` | Chốt, đổi scope hoặc đóng một phase. |
| `PROGRESS.md` | Có kết quả, quyết định, blocker hoặc handoff mới. |
| `VERIFY.md` | Có cách kiểm chứng mới hoặc bằng chứng đã chạy. |
| `FEATURE_MAP.md` | Luồng người dùng, endpoint, đường điều hướng hoặc proof path thay đổi. |
| `SKILL.md` | Workflow lặp lại bộc lộ lỗi, hoặc cách làm tốt hơn đã được kiểm chứng. |

Đừng ghi `passed` khi chưa chạy. Với repo trống, `FEATURE_MAP.md` chỉ ghi “chưa có bề mặt sản phẩm”; không cần bịa route hay UI.
