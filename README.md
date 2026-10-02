# VNTrader – App điện thoại

## Dùng nhanh với tài khoản DNSE (không cần máy tính)

Sau khi cài app Android (Cách 1 bên dưới): mở app → bấm nút trạng thái trên cùng →
**Đăng nhập DNSE trực tiếp** → nhập tài khoản DNSE → nhập OTP → giao dịch.
Lần sau mở app, màn hình đăng nhập DNSE hiện ra ngay.

Điều kiện: tài khoản DNSE đã **đăng ký LightSpeed API**, và đã bật **Smart OTP** (ứng dụng DNSE) hoặc **OTP qua email**.
Giá thật, biểu đồ, tiền, danh mục và lệnh đều lấy thẳng từ DNSE.

Một mã nguồn, hai cách cài:

| | Android | iPhone |
|---|---|---|
| Cách cài | File **APK** (cài trực tiếp) | **PWA** – "Thêm vào Màn hình chính" từ Safari |
| Demo (giá mô phỏng) | Có, chạy cả khi mất mạng | Có |
| Giá thật qua bridge trên máy tính (cùng Wi-Fi) | Có | Không (Safari chặn kết nối ws:// từ trang https) |

## Máy tính Windows – file .exe

Tab **Actions** → workflow **Build Windows App** (chạy tự động sau khi tải mã lên, khoảng 5–10 phút)
→ tải **VNTrader-Windows** trong mục Artifacts. Bên trong có 2 file:

- `VNTrader-…-nsis.exe`: bộ cài đặt (tạo biểu tượng ngoài màn hình).
- `VNTrader-portable.exe`: chạy luôn, không cần cài.

Windows có thể hiện cảnh báo SmartScreen vì app chưa ký số: bấm **More info → Run anyway**.
Mở app → nút trạng thái → **Đăng nhập DNSE trực tiếp**.

Chạy thử không cần build (máy đã cài Node.js 20): `npm install` rồi `npm run desktop`.

## Cách 1 – Build APK bằng GitHub (không cần cài gì lên máy)

1. Tạo tài khoản GitHub, bấm **New repository**, đặt tên `vntrader-app`, chọn **Public**, bấm Create.
2. Bấm **uploading an existing file**, kéo **toàn bộ nội dung** thư mục này vào (gồm cả thư mục `.github`), bấm Commit.
   - Nếu trình duyệt không kéo được thư mục `.github`: bấm **Add file → Create new file**, gõ tên
     `.github/workflows/android.yml` rồi dán nội dung file tương ứng.
3. Mở tab **Actions** → workflow **Build Android APK** chạy tự động (khoảng 5–8 phút).
   Nếu chưa chạy: chọn workflow → **Run workflow**.
4. Khi xong (dấu ✓ xanh), bấm vào lần chạy → mục **Artifacts** → tải **VNTrader-APK** (file zip chứa `VNTrader.apk`).
5. Chép `VNTrader.apk` sang điện thoại Android (Zalo, Google Drive, cáp USB…), mở file và cho phép
   "Cài ứng dụng không rõ nguồn gốc" khi được hỏi.

APK này là bản debug, dùng cá nhân. Muốn đưa lên Google Play cần ký bằng khóa riêng và tài khoản nhà phát triển Google.

## Cách 2 – PWA cho iPhone (và Android)

1. Trong repo trên GitHub: **Settings → Pages → Source: GitHub Actions**.
2. Tab **Actions** → **Deploy PWA** → Run workflow. Xong sẽ có địa chỉ dạng `https://<tên>.github.io/vntrader-app/`.
3. iPhone: mở địa chỉ bằng **Safari** → nút Chia sẻ → **Thêm vào MH chính**.
   Android: mở bằng Chrome → menu ⋮ → **Cài đặt ứng dụng**.

## Cách 3 – Tự build trên máy (cho lập trình viên)

Cần Node.js 20, Android Studio, JDK 17.
```
npm install
npx cap add android
npm run android      # mở Android Studio → Build → Build APK(s)
```
iOS: cần máy Mac + Xcode: `npm i @capacitor/ios && npx cap add ios && npx cap open ios`.

## Kết nối giá thật từ app

Chạy bridge trên máy tính với `HOST=0.0.0.0` và `BRIDGE_TOKEN` (xem README của vntrader-bridge),
rồi trong app: nút Demo → chọn chế độ → `ws://<IP máy tính>:8788/?token=<mật khẩu>`.
