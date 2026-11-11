# Spinx SecureCode AI — bản cài desktop

Spinx SecureCode AI rà soát bảo mật mã nguồn ngay trên máy bạn: chạy scanner trong container không
mạng, để agent AI phân tích và đề xuất bản sửa, và chờ bạn phê duyệt mọi hành động có rủi ro. Mã nguồn
không rời máy, trừ phần gửi cho LLM provider bạn cấu hình.

Repo này chỉ chứa **bản cài đã biên dịch**. Mỗi phiên bản là một
[release](https://github.com/lvphuong/spinxsca-releases/releases).

**[⬇ Tải bản mới nhất](https://github.com/lvphuong/spinxsca-releases/releases/latest)**

## Chọn file

| Hệ điều hành | File |
|---|---|
| macOS 12+ · Apple Silicon (M1 trở lên) | `Spinx-SecureCode-AI_<version>_aarch64.dmg` |
| macOS 12+ · Intel | `Spinx-SecureCode-AI_<version>_x64.dmg` |
| Windows 10/11 x64 | `Spinx-SecureCode-AI_<version>_x64-setup.exe` (hoặc `.msi`) |
| Linux x64 | `Spinx-SecureCode-AI_<version>_amd64.AppImage` (hoặc `.deb`) |

Không phải release nào cũng có đủ mọi nền tảng; xem danh sách file trong từng release.

## Yêu cầu

- Docker Desktop hoặc Docker Engine đang chạy. Scanner và sandbox chạy trong container.
- Anthropic API key nếu dùng AI. Nhập key trong màn **Onboarding** hoặc **Settings**; key được lưu
  trong keychain của hệ điều hành, không nằm trong file nào.
- Linux cần WebKitGTK 4.1.

Bản cài đã kèm Node.js runtime, máy không cần cài Node hay pnpm.

## Cài đặt

Các bản hiện tại **chưa ký** (chưa có chứng chỉ Apple Developer ID và Authenticode), nên hệ điều hành
sẽ cảnh báo ở lần mở đầu tiên.

**macOS:** mở file `.dmg`, kéo app vào **Applications**. Nếu macOS báo không mở được app, chạy

```sh
xattr -dr com.apple.quarantine "/Applications/Spinx SecureCode AI.app"
```

rồi mở lại, hoặc vào **System Settings → Privacy & Security** và bấm **Open Anyway**.

**Windows:** chạy file `-setup.exe`. Bản này cài cho người dùng hiện tại, không cần quyền admin. Nếu
SmartScreen cảnh báo, bấm **More info → Run anyway**.

**Linux:**

```sh
chmod +x Spinx-SecureCode-AI_*_amd64.AppImage && ./Spinx-SecureCode-AI_*_amd64.AppImage
# hoặc
sudo apt install ./Spinx-SecureCode-AI_*_amd64.deb
```

## Kiểm tra file tải về

Mỗi release có file `SHA256SUMS`. Tải nó cùng thư mục với bản cài rồi chạy:

```sh
grep <tên-file> SHA256SUMS | shasum -a 256 -c -     # Linux: sha256sum -c -
```

## Dữ liệu và gỡ cài đặt

Dữ liệu của app (cấu hình `spinxsca.yaml`, dự án, review, log) nằm trong thư mục dữ liệu của app:

- macOS: `~/Library/Application Support/com.spinxsca.desktop/`
- Windows: `%APPDATA%\com.spinxsca.desktop\`
- Linux: `~/.local/share/com.spinxsca.desktop/`

Gỡ app không xoá thư mục này. Xoá nó nếu muốn làm sạch hoàn toàn.

## Báo lỗi

Mở [issue](https://github.com/lvphuong/spinxsca-releases/issues) trong repo này, ghi rõ phiên bản, hệ điều hành
và đính kèm `sidecar.log` trong thư mục dữ liệu nếu dịch vụ cục bộ không khởi động được.
