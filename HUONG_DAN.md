# PNCNC Process Hub – Hướng dẫn cài đặt miễn phí (Supabase + GitHub Pages/Netlify)

Thời gian: khoảng 20 phút. Không tốn phí (gói Free của Supabase, GitHub Pages / Netlify).

## Bước 1 – Tạo cơ sở dữ liệu Supabase
1. Vào https://supabase.com → **Start your project** → đăng nhập bằng GitHub hoặc email.
2. **New project**: đặt tên `pncnc-hub`, đặt mật khẩu database (lưu lại), Region chọn **Southeast Asia (Singapore)**.
3. Mở **SQL Editor** → **New query** → dán toàn bộ nội dung file `supabase.sql` → **Run**.
   (Tạo 2 bảng `processes`, `comments`, bật bảo mật chỉ cho người đăng nhập, bật realtime, nạp 7 quy trình mẫu.)
4. Vào **Project Settings → API**, copy **Project URL** và **anon public key**.
5. Mở file `config.js`, dán 2 giá trị vào `SUPABASE_URL` và `SUPABASE_ANON_KEY`.

## Bước 2 – Cấu hình đăng nhập bằng email
1. **Authentication → Sign In / Providers → Email**: bật Email (mặc định đã bật).
2. Để chặn người ngoài tự đăng ký: tắt **Allow new users to sign up**, rồi vào **Authentication → Users → Invite user** để mời từng email đồng nghiệp.
3. Sau khi có link web (Bước 3), vào **Authentication → URL Configuration**, điền link đó vào **Site URL** và **Redirect URLs**.

## Bước 3 – Đưa web lên mạng (chọn 1 cách)
**Cách A – Netlify (dễ nhất, kéo thả):**
1. Vào https://app.netlify.com/drop
2. Kéo cả thư mục `pncnc-hub` (gồm `index.html`, `config.js`) vào → có ngay link dạng `https://ten-ngau-nhien.netlify.app`.
3. Có thể đổi tên link trong **Site configuration → Change site name**.

**Cách B – GitHub Pages:**
1. Tạo repository mới trên GitHub (ví dụ `pncnc-hub`), upload `index.html` và `config.js`.
2. **Settings → Pages → Branch: main / root → Save**. Link: `https://<tên-github>.github.io/pncnc-hub/`.

## Bước 4 – Sử dụng
- Mở link, nhập email → bấm link trong email để đăng nhập.
- Mọi người dùng chung dữ liệu, góp ý hiện ngay cho người khác (realtime).
- Tên người góp ý lấy theo phần trước @ của email. Muốn hiện họ tên: Supabase → Authentication → Users → chọn user → sửa metadata `full_name`.

## Lưu ý
- Gói Free của Supabase tạm dừng project nếu **không có ai dùng trong 7 ngày**; vào dashboard bấm Restore là chạy lại, dữ liệu vẫn còn.
- `anon key` được phép để công khai trong web; dữ liệu vẫn được bảo vệ vì chỉ người đã đăng nhập mới đọc/ghi được.
- Sao lưu: Supabase → Table Editor → chọn bảng → Export CSV.
- Kết nối Base Workflow sau này: tạo Supabase Edge Function nhận webhook từ Base và ghi vào bảng số liệu vận hành.
