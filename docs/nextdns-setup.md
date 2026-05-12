# Hướng dẫn cài đặt NextDNS cá nhân trên iOS/macOS

## ⚠️ Lưu ý quan trọng

> Hướng dẫn này chỉ dùng cho cấu hình DNS cá nhân, lọc DNS, bảo vệ quyền riêng tư và kiểm tra lỗi mạng.
> Hướng dẫn này **không** dùng để mở khóa, bypass, giả lập hoặc giữ lại bất kỳ tính năng trả phí nào.
> Không sử dụng hướng dẫn này để vượt qua thanh toán, entitlement hoặc xác thực subscription của ứng dụng.

## Giới thiệu

NextDNS là dịch vụ DNS cá nhân cho phép bạn:

- Chặn quảng cáo và tracker ở cấp DNS
- Xem log các truy vấn DNS từ thiết bị
- Bảo vệ quyền riêng tư khi duyệt web
- Không cần cài VPN hay app bên thứ ba

Hướng dẫn này sử dụng file `.mobileconfig` để cấu hình DNS-over-HTTPS ở cấp hệ thống.

## Yêu cầu

- iPhone/iPad chạy iOS 14+ hoặc Mac chạy macOS 11+
- Tài khoản NextDNS (miễn phí)
- Text editor (để chỉnh sửa template)

## Bước 1: Tạo tài khoản NextDNS

1. Truy cập [https://nextdns.io](https://nextdns.io)
2. Đăng ký tài khoản miễn phí
3. Mở Dashboard
4. Tìm **Configuration ID** của bạn (dạng 6 ký tự, ví dụ: `abc123`)
5. Ghi lại ID này

## Bước 2: Tùy chỉnh file MobileConfig

Repository này chứa file template:

```
PersonalNextDNS.mobileconfig
```

Mở file và thay thế các placeholder:

| Placeholder | Thay bằng | Ví dụ |
|---|---|---|
| `{{NEXTDNS_ID}}` | Configuration ID của bạn | `abc123` |
| `{{DEVICE_NAME}}` | Tên thiết bị (hiển thị trên NextDNS) | `iPhone-15-Pro` |
| `{{PROFILE_DISPLAY_NAME}}` | Tên profile hiển thị trên iPhone | `My Personal DNS` |
| `{{PROFILE_OWNER}}` | Tên chủ sở hữu | `william` |
| `{{DNS_PAYLOAD_UUID}}` | UUID mới (chạy `uuidgen` trên terminal) | `A1B2C3D4-...` |
| `{{MAIN_PAYLOAD_UUID}}` | UUID mới khác | `E5F6G7H8-...` |

Tạo UUID bằng terminal:

```bash
uuidgen
uuidgen
```

Sau khi thay xong, URL DNS sẽ có dạng:

```
https://apple.dns.nextdns.io/abc123/iPhone-15-Pro
```

## Bước 3: Cài đặt trên iPhone

1. Gửi file `.mobileconfig` đã chỉnh sửa sang iPhone (AirDrop, iCloud, email)
2. Mở file trên iPhone
3. Vào **Cài đặt > Cài đặt chung > VPN & Quản lý thiết bị**
4. Chọn profile vừa tải
5. Nhấn **Cài đặt**
6. Nhập mật mã nếu được yêu cầu
7. Xác nhận cài đặt

> Lưu ý: Tên menu có thể khác nhau tùy phiên bản iOS và ngôn ngữ.

## Bước 4: Xác nhận hoạt động

1. Mở [NextDNS Dashboard](https://my.nextdns.io)
2. Vào **Logs** hoặc **Analytics**
3. Mở Safari trên iPhone, truy cập một trang web bất kỳ
4. Kiểm tra xem truy vấn DNS có xuất hiện trên Dashboard không
5. Xác nhận tên thiết bị hiển thị đúng

## Bước 5: Cấu hình Denylist

Denylist dùng để chặn các domain không mong muốn (quảng cáo, tracker, v.v.).

Vào NextDNS Dashboard > **Denylist** > thêm domain cần chặn.

| Domain | Lý do | Ghi chú |
|---|---|---|
| `example-tracker.com` | Tracking | Thay bằng domain của bạn |
| `example-ads.com` | Quảng cáo | Thay bằng domain của bạn |

**Không nên chặn:**

- Domain xác thực thanh toán (Apple, Google)
- Domain backend của ứng dụng
- Domain xác thực subscription
- Domain hệ thống Apple (captive.apple.com, v.v.)

## Xử lý sự cố

### Không thấy log DNS trên Dashboard

- Kiểm tra NextDNS ID đã thay đúng chưa
- Kiểm tra profile đã cài thành công chưa
- Tắt VPN/DNS app khác đang chạy
- Khởi động lại iPhone
- Tạo lại profile nếu cần

### Một số app không hoạt động

- Kiểm tra Logs trên NextDNS xem domain nào bị chặn
- Chuyển domain bị chặn nhầm sang **Allowlist**
- Giảm số lượng blocklist nếu quá nhiều

### Pin hao nhanh

File `.mobileconfig` DNS thường tiêu thụ pin rất ít. Nếu pin hao nhanh, có thể do app bị chặn domain liên tục retry request.

## Bảo mật & Quyền riêng tư

- NextDNS có thể xem các domain bạn truy vấn nếu bật Logs
- **Không** chia sẻ công khai NextDNS ID nếu bạn muốn log sạch
- **Không** chia sẻ file `.mobileconfig` chứa NextDNS ID cá nhân
- **Không** cài profile từ người lạ
- **Không** cài profile chứa root certificate, VPN, proxy, hoặc MDM payload trừ khi bạn hiểu rõ

## Nguồn / Credit

Nếu bạn chia sẻ, fork hoặc đăng lại tutorial này, vui lòng giữ lại phần ghi nguồn.

Nguồn gốc:
- Repository: [Long18/shadowrocket](https://github.com/Long18/shadowrocket)
- Maintainer: William / Long18

Bạn có thể chỉnh sửa hướng dẫn này cho mục đích cá nhân, nhưng vui lòng không xóa phần ghi nguồn khi chia sẻ công khai.
