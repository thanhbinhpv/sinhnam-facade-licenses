# Sinh Nam FACADE — License Registry

Kho này lưu license **đã mã hóa** cho add-in Excel Sinh Nam FACADE. Không lưu trực tiếp product key, tên máy, IP hay serial ổ đĩa.

## Cấu trúc

```text
licenses/<SHA256_PRODUCT_KEY>.lic
```

DLL đọc license tại:

```text
https://raw.githubusercontent.com/thanhbinhpv/sinhnam-facade-licenses/main/licenses
```

## Thời hạn mặc định

- License mới thường có hạn **1 năm** từ ngày cấp.
- Khi GitHub hoặc dịch vụ kiểm tra IP không truy cập được, máy đã xác thực online được dùng cache tối đa **6 tháng**, nhưng không vượt ngày hết hạn.
- License hiện tại có hạn đến **2027-09-25**.

## Gia hạn license

1. Giữ nguyên product key, tên PC, public IP và serial ổ đĩa.
2. Chạy script `New-GithubLicenseFile.ps1` với ngày `ExpiresOn` mới.
3. File tạo ra có cùng tên hash với file hiện tại.
4. Trên GitHub, mở file trong thư mục `licenses`, chọn **Edit**, thay toàn bộ 5 dòng bằng nội dung file mới rồi commit.
5. Add-in sẽ nhận hạn mới ở lần kiểm tra online tiếp theo (tối đa 24 giờ), hoặc kích hoạt lại để cập nhật ngay.

## Bảo mật

- AES-256-CBC
- PBKDF2: 120,000 vòng
- HMAC-SHA256 chống sửa nội dung
- Cache máy dùng Windows DPAPI
- License bị từ chối nếu key, PC, IP hoặc serial ổ đĩa không khớp
