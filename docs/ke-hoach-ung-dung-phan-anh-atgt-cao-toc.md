# Kế hoạch xây dựng ứng dụng tiếp nhận phản ánh trật tự, an toàn giao thông trên cao tốc

> Bản nháp v0.1 — 23/10/2026. Tên tạm: **"Cao tốc An toàn"**.

## 1. Mục tiêu

- Cho người dân gửi phản ánh về vi phạm, sự cố, hư hỏng hạ tầng trên tuyến cao tốc **nhanh (≤ 30 giây), chính xác vị trí (lý trình Km + chiều đi), có bằng chứng (ảnh/video)**.
- Giúp trung tâm điều hành / lực lượng chức năng **tiếp nhận – phân loại – điều phối – phản hồi** trên một hệ thống, có hạn xử lý (SLA) và lịch sử đầy đủ.
- Tích lũy dữ liệu để xác định **điểm đen, khung giờ nguy hiểm**, phục vụ tuần tra và đầu tư hạ tầng.

**Không** thay thế số khẩn cấp 113/114/115: với tai nạn có thương vong hoặc cháy, ứng dụng phải hướng người dùng gọi ngay, rồi mới gửi phản ánh.

## 2. Đối tượng sử dụng

| Vai trò | Nhu cầu chính |
|---|---|
| Người dân, tài xế, hành khách | Gửi phản ánh, theo dõi kết quả, nhận cảnh báo trên tuyến |
| Điều phối viên (trung tâm điều hành cao tốc) | Xem bản đồ thời gian thực, xác minh, gộp trùng, chuyển xử lý |
| Đơn vị xử lý (CSGT tuần tra, cứu hộ, đơn vị quản lý khai thác/bảo trì) | Nhận việc trên điện thoại, cập nhật tiến độ, đính kèm ảnh kết quả |
| Lãnh đạo / quản trị | Thống kê, báo cáo, cấu hình danh mục, phân quyền |

## 3. Danh mục phản ánh

1. **Vi phạm**: đi ngược chiều, lùi xe, quay đầu; dừng/đỗ trên làn khẩn cấp không lý do; chạy sai làn, lạng lách; quá tốc độ / quá chậm; xe quá tải, chở hàng rơi vãi; người đi bộ, xe máy đi vào cao tốc.
2. **Sự cố**: tai nạn; xe hỏng, xe cháy; vật cản, hàng rơi trên đường; động vật.
3. **Hạ tầng**: ổ gà, lún nứt; biển báo/vạch sơn mờ, hỏng; hộ lan, rào chắn hư; đèn chiếu sáng; camera, biển báo điện tử (VMS) hỏng.
4. **Điều kiện lưu thông**: ùn tắc, sương mù, ngập nước, khói đốt đồng.
5. **Khác**: thái độ phục vụ trạm dừng nghỉ, thu phí…

Mỗi loại có **mức ưu tiên mặc định** (Khẩn cấp / Cao / Thường) quyết định SLA và kênh thông báo.

## 4. Tính năng

### 4.1. Ứng dụng người dân (MVP)

- **Gửi phản ánh 3 bước**: chọn loại → chụp ảnh/quay video (≤ 30 s) → gửi. Mô tả, biển số xe vi phạm là tùy chọn.
- **Định vị tự động**: GPS → quy đổi sang *tuyến, lý trình Km+m, chiều đi* (VD: "CT Hà Nội – Hải Phòng, Km 42+300, hướng Hải Phòng"). Cho phép kéo ghim chỉnh tay.
- **Chế độ an toàn khi đang di chuyển**: phát hiện tốc độ > 10 km/h thì hiển thị nhắc "Chỉ dùng khi là hành khách hoặc đã dừng an toàn"; hỗ trợ **gửi bằng giọng nói** và nút gửi nhanh cỡ lớn.
- **Nút gọi khẩn cấp**: 113, 114, 115 và đường dây nóng của tuyến đang đi (tự chọn theo vị trí).
- **Theo dõi trạng thái** phản ánh, nhận thông báo đẩy khi có kết quả; đánh giá mức độ hài lòng.
- **Gửi khi mất sóng**: lưu hàng đợi trên máy, tự gửi lại khi có mạng (giữ thời gian/vị trí lúc chụp).
- **Định danh**: đăng nhập bằng số điện thoại + OTP (giai đoạn sau: VNeID). Có tùy chọn **ẩn danh với cơ quan công khai** nhưng hệ thống vẫn lưu định danh để chống lạm dụng.

### 4.2. Cổng điều hành (web)

- **Bản đồ thời gian thực** các phản ánh theo tuyến, lọc theo loại / mức ưu tiên / trạng thái.
- **Gộp phản ánh trùng**: cùng loại, cùng chiều, cách nhau ≤ 500 m và ≤ 15 phút → gợi ý gộp thành 1 sự vụ (số người báo là tín hiệu độ tin cậy).
- **Phân công & SLA**: chuyển cho đơn vị phụ trách đoạn tuyến (cấu hình theo lý trình), đếm ngược hạn xử lý, tự động nhắc/leo thang khi quá hạn.
- **Phản hồi người dân** bằng mẫu soạn sẵn; ghi nhật ký mọi thao tác (audit log).
- **Báo cáo**: số phản ánh theo tuyến/loại/thời gian, thời gian xử lý trung bình, bản đồ nhiệt điểm đen; xuất Excel/PDF.

### 4.3. Ứng dụng lực lượng xử lý (giai đoạn 2)

Nhận việc, dẫn đường tới lý trình, cập nhật "đã đến hiện trường / đã xử lý" kèm ảnh.

### 4.4. Mở rộng (giai đoạn 3)

- AI hỗ trợ: phân loại ảnh, nhận dạng biển số, **tự làm mờ khuôn mặt/biển số** trước khi hiển thị công khai.
- Cảnh báo ngược tới người dân trên tuyến (sự cố phía trước X km).
- Kết nối hệ thống camera giám sát, VMS và các nền tảng của cơ quan chức năng.

## 5. Quy trình xử lý

```
Mới ──► Đã tiếp nhận ──► Đã chuyển xử lý ──► Đang xử lý ──► Đã xử lý ──► Đóng
  │            │                                                  ▲
  └─► Trùng (gộp vào sự vụ khác)   └─► Không xác minh được / Từ chối (nêu lý do)
```

SLA đề xuất (cần thống nhất với đơn vị vận hành): Khẩn cấp — tiếp nhận ≤ 2 phút; Cao — ≤ 15 phút; Thường — ≤ 24 giờ.

## 6. Kiến trúc kỹ thuật đề xuất

| Thành phần | Lựa chọn | Lý do |
|---|---|---|
| App người dân | **PWA** cho MVP (camera, GPS, offline, cài lên màn hình chính), sau đó Flutter/React Native nếu cần nền ghi âm, push iOS ổn định | Ra mắt nhanh, không chờ duyệt store |
| Cổng điều hành | React/Next.js + thư viện bản đồ MapLibre | Bản đồ vector, tự host được |
| Backend API | NestJS (Node) hoặc FastAPI (Python) | Phổ biến, dễ tuyển người |
| CSDL | **PostgreSQL + PostGIS** | Quy đổi GPS → lý trình bằng `ST_LineLocatePoint` trên dữ liệu tim tuyến |
| Lưu ảnh/video | Object storage tương thích S3, URL ký có thời hạn | Tách media khỏi CSDL |
| Hàng đợi / realtime | Redis + WebSocket | Đẩy sự vụ mới lên bản đồ điều hành ngay |
| Thông báo | FCM/APNs, SMS dự phòng | |
| Hạ tầng | Đám mây/trung tâm dữ liệu **đặt tại Việt Nam** | Yêu cầu lưu trữ dữ liệu trong nước, bảo vệ dữ liệu cá nhân |

**Dữ liệu nền cần có**: tim tuyến (polyline) từng cao tốc theo hai chiều, mốc lý trình, nút giao, trạm thu phí, trạm dừng nghỉ, phân đoạn phụ trách của từng đơn vị.

### Mô hình dữ liệu chính (rút gọn)

- `nguoi_dung` (id, sdt, vai_tro, don_vi_id, trang_thai)
- `tuyen` (id, ten, hinh_hoc_chieu_di, hinh_hoc_chieu_ve)
- `doan_phu_trach` (tuyen_id, km_tu, km_den, don_vi_id)
- `phan_anh` (id, nguoi_gui_id, loai, muc_uu_tien, vi_tri, tuyen_id, ly_trinh_m, chieu, mo_ta, bien_so, thoi_diem_chup, trang_thai, su_vu_id)
- `su_vu` (id, loai, tuyen_id, ly_trinh_m, chieu, trang_thai, don_vi_xu_ly_id, han_xu_ly)
- `tep_dinh_kem` (id, phan_anh_id, url, loai, hash_sha256, exif)
- `nhat_ky` (id, doi_tuong, hanh_dong, nguoi_thuc_hien, thoi_diem, du_lieu)

## 7. Pháp lý, bảo mật, chống lạm dụng

- **Bảo vệ dữ liệu cá nhân**: thu thập tối thiểu, xin đồng ý rõ ràng, chính sách quyền riêng tư, phân quyền truy cập theo vai trò, mã hóa khi truyền và khi lưu; rà soát theo quy định hiện hành về bảo vệ dữ liệu cá nhân và an ninh mạng.
- **Giá trị pháp lý của bằng chứng**: nếu muốn hình ảnh người dân làm căn cứ xử lý vi phạm, cần **phối hợp với cơ quan CSGT** để quy trình tiếp nhận, xác minh đúng quy định. Ứng dụng nên chỉ cho chụp/quay trực tiếp trong app, lưu hash + thời gian + tọa độ để chống chỉnh sửa.
- **Tránh trùng lặp với nền tảng sẵn có**: rà soát các ứng dụng/cổng phản ánh của cơ quan chức năng hiện có (VD: VNeTraffic của Cục CSGT, tổng đài của đơn vị quản lý tuyến) — cân nhắc **tích hợp/chuyển tiếp** thay vì làm song song.
- **Chống lạm dụng**: OTP, giới hạn tần suất gửi, chấm điểm uy tín người gửi, phát hiện ảnh trùng/ảnh cũ, khóa tài khoản báo sai nhiều lần.
- **Không công khai** thông tin người phản ánh cho bên bị phản ánh.

## 8. Lộ trình

| Giai đoạn | Thời gian | Kết quả |
|---|---|---|
| 0. Khảo sát & thống nhất | 2–3 tuần | Chốt đơn vị chủ quản, tuyến thí điểm, danh mục, SLA, quy trình liên thông; thu thập dữ liệu tim tuyến |
| 1. MVP | 8–10 tuần | PWA người dân + cổng điều hành + backend; thí điểm **1 tuyến** |
| 2. Thí điểm & hoàn thiện | 2–3 tháng | App lực lượng xử lý, báo cáo, gộp trùng, cải thiện theo phản hồi |
| 3. Mở rộng | sau 6 tháng | Nhiều tuyến, app native, AI, tích hợp camera/VMS và hệ thống bên ngoài |

**Nhân sự MVP gợi ý**: 1 PM/BA, 1 UI/UX, 2 backend, 1–2 frontend, 1 QA, 0,5 DevOps/GIS.

## 9. Chỉ số đánh giá (KPI)

- Thời gian gửi phản ánh trung vị ≤ 30 giây.
- ≥ 95% phản ánh quy đổi đúng tuyến và chiều đi; sai số lý trình ≤ 200 m.
- Thời gian tiếp nhận trung bình theo từng mức ưu tiên đạt SLA ≥ 90%.
- Tỷ lệ phản ánh có kết quả phản hồi cho người dân ≥ 95%.
- Mức hài lòng ≥ 4/5; tỷ lệ phản ánh sai/spam ≤ 10%.

## 10. Rủi ro chính

| Rủi ro | Giảm thiểu |
|---|---|
| Người dùng thao tác khi đang lái xe | Cảnh báo theo tốc độ, gửi bằng giọng nói, truyền thông "hành khách báo, tài xế lái" |
| GPS lệch giữa hai chiều đường | Dùng hướng di chuyển (heading) + cho chỉnh tay |
| Không có đơn vị xử lý cam kết → phản ánh "rơi vào im lặng" | Ký quy chế phối hợp, SLA trước khi ra mắt |
| Ít người dùng | Mã QR tại trạm thu phí/trạm dừng nghỉ, biển VMS, liên kết với ứng dụng thu phí / bản đồ |
| Lộ dữ liệu cá nhân, hình ảnh | Phân quyền, làm mờ, audit log, kiểm thử bảo mật trước khi ra mắt |

## 11. Câu hỏi cần chốt trước khi làm

1. Đơn vị chủ quản và vận hành là ai (doanh nghiệp quản lý tuyến, Sở GTVT, hay cơ quan CSGT)?
2. Tuyến cao tốc nào thí điểm?
3. Phản ánh có dùng làm căn cứ xử phạt hay chỉ để điều phối, cảnh báo?
4. Có bắt buộc định danh (VNeID) hay cho phép chỉ dùng số điện thoại?
5. Hạ tầng triển khai: đám mây thương mại trong nước hay trung tâm dữ liệu của cơ quan?
