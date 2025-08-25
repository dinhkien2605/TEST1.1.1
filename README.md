
# Tauri Native OCR (Offline) – Windows .exe installer

**Tiền xử lý ảnh native (Rust)** + **OCR offline** (Tesseract.js với model nội bộ). Đóng gói bộ cài **.exe (NSIS)** bằng Tauri.

## 1) Chuẩn bị môi trường BUILD
- **Windows 10/11**
- **Node.js 18+**
- **Rust**: cài từ https://rustup.rs
- **Tauri CLI**: `cargo install tauri-cli`
- **NSIS** (để tạo .exe): tải & cài từ https://nsis.sourceforge.io/ (thêm vào PATH)

> Người dùng cuối chỉ chạy file cài `.exe` bạn build ra, **không cần Python, không cần Internet khi chạy**.

## 2) Cài deps & tải model offline
```bash
npm install
npm run fetch-models   # tải eng/vie + core/worker vào src-tauri/resources
```

## 3) Build bộ cài .exe
```bash
npm run dist
```
Bộ cài nằm ở:
```
src-tauri/target/release/bundle/nsis/tauri-native-ocr_1.0.0_x64-setup.exe
```

## 4) Dùng ứng dụng
- Mở app → Chọn ảnh → **Áp dụng tiền xử lý (Rust)** → **Bắt đầu OCR**.
- Ngôn ngữ: `eng`, `vie`, `eng+vie`.
- PSM: 3,4,6,7.
- Kết quả hiển thị, có **Copy** / **Lưu .txt**.

## 5) Lưu ý
- Tiền xử lý gồm: Gaussian, Median, Otsu, **auto-deskew** (tối giản), xoay thủ công.
- Mọi tài nguyên OCR (`traineddata`, `wasm`, `worker`) đã nằm trong `resources` → chạy **offline 100%**.
- Nếu muốn OCR native thay vì JS (libtesseract), hãy yêu cầu "build OCR native" — mình sẽ cập nhật dự án với `leptess`.

## 6) Troubleshooting
- Nếu `tauri` báo thiếu NSIS: cài NSIS và mở terminal mới để PATH cập nhật.
- Build lần đầu sẽ tải Rust crates; các lần sau nhanh hơn.
- Ảnh quá lớn → tiền xử lý có thể chậm; cân nhắc giảm kích thước trước khi OCR.
