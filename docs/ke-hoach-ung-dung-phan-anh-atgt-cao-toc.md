# Kế hoạch xây dựng ứng dụng tiếp nhận phản ánh trật tự, an toàn giao thông trên cao tốc

> Bản nháp v0.2 — 23/10/2026. Tên tạm: **"Cao tốc An toàn"**.
> Đơn vị chủ quản: **Đội CSGT đường bộ cao tốc số 4**.

## 0. Thông tin đã chốt

| Nội dung | Quyết định |
|---|---|
| Đơn vị chủ quản, vận hành | Đội CSGT đường bộ cao tốc số 4 |
| Phạm vi tuyến | Cao tốc Bắc – Nam phía Đông, từ **Nghi Sơn đến Cam Lộ** (6 dự án thành phần, xem mục 1) |
| Mục đích sử dụng phản ánh | **Cả hai**: điều phối, xử lý hiện trường **và** làm căn cứ xử lý vi phạm |
| Định danh người gửi | Số điện thoại + OTP là bắt buộc. **VNeID**: nên có (xem mục 7.2) |

## 1. Phạm vi tuyến

| # | Đoạn | Địa bàn | Ghi chú |
|---|---|---|---|
| 1 | Nghi Sơn – Diễn Châu | Thanh Hóa, Nghệ An | |
| 2 | Diễn Châu – Bãi Vọt | Nghệ An, Hà Tĩnh | |
| 3 | Bãi Vọt – Vũng Áng (gồm Bãi Vọt – Hàm Nghi, Hàm Nghi – Vũng Áng) | Hà Tĩnh | |
| 4 | Vũng Áng – Bùng | Hà Tĩnh, Quảng Trị (Quảng Bình cũ) | |
| 5 | Bùng – Vạn Ninh | Quảng Trị (Quảng Bình cũ) | |
| 6 | Vạn Ninh – Cam Lộ | Quảng Trị | |

Tổng chiều dài khoảng 350 km, qua 4 tỉnh: Thanh Hóa, Nghệ An, Hà Tĩnh, Quảng Trị. **Cần Đội 4 cung cấp hoặc xác nhận**:

- Lý trình đầu/cuối chính xác của từng đoạn, vị trí các nút giao, đường dẫn và điểm dừng khẩn cấp.
- Mặt cắt ngang từng đoạn: có làn dừng khẩn cấp liên tục hay chỉ có điểm dừng; đoạn nào phân kỳ, quy mô làn hạn chế. Điều này ảnh hưởng đến danh mục vi phạm (VD: "dừng đỗ sai quy định" khác nhau giữa các đoạn).
- **Phân công địa bàn** của các tổ/trạm thuộc Đội 4 theo lý trình, để hệ thống tự chuyển phản ánh tới đúng tổ.
- Đơn vị quản lý, khai thác và bảo trì từng đoạn, cùng đầu mối liên hệ (để chuyển các phản ánh về hạ tầng).
- Đường dây nóng của Đội 4 và của từng đơn vị quản lý tuyến.

## 2. Mục tiêu

- Người dân gửi phản ánh **trong khoảng 30 giây**, vị trí được ghi theo **lý trình Km và chiều đi**, kèm ảnh hoặc video.
- Đội 4 **tiếp nhận, phân loại, điều phối và phản hồi** trên một hệ thống, có thời hạn xử lý (SLA) và lịch sử đầy đủ.
- Phản ánh về vi phạm đủ điều kiện được **chuyển thành hồ sơ xử lý vi phạm**, đúng quy trình pháp lý.
- Tích lũy dữ liệu để xác định **điểm đen, khung giờ nguy hiểm** trên tuyến, phục vụ bố trí tuần tra.

Ứng dụng **không thay thế** các số khẩn cấp 113/114/115. Với tai nạn có thương vong hoặc cháy xe, ứng dụng hướng người dùng gọi ngay, sau đó mới gửi phản ánh.

## 3. Đối tượng sử dụng

| Vai trò | Nhu cầu chính |
|---|---|
| Người dân, tài xế, hành khách | Gửi phản ánh, theo dõi kết quả, nhận cảnh báo trên tuyến |
| Cán bộ trực ban Đội 4 | Bản đồ thời gian thực, xác minh, gộp phản ánh trùng, chuyển cho tổ tuần tra |
| Tổ tuần tra, kiểm soát | Nhận việc trên điện thoại, cập nhật tiến độ, đính kèm ảnh kết quả |
| Cán bộ xử lý vi phạm | Thẩm định bằng chứng, lập hồ sơ, theo dõi kết quả xử lý |
| Đơn vị quản lý tuyến, cứu hộ | Nhận phản ánh về hạ tầng, sự cố được Đội 4 chuyển sang |
| Lãnh đạo Đội 4 | Thống kê, báo cáo, cấu hình danh mục, phân quyền |

## 4. Danh mục phản ánh

1. **Vi phạm** (có thể dùng làm căn cứ xử lý): đi ngược chiều, lùi xe, quay đầu xe; dừng/đỗ sai quy định; chạy sai làn, vượt sai quy định, lạng lách; chạy quá tốc độ hoặc quá chậm; xe quá tải, chở hàng rơi vãi; xe máy, người đi bộ đi vào cao tốc.
2. **Sự cố**: tai nạn; xe hỏng, xe cháy; vật cản, hàng rơi trên đường; động vật.
3. **Hạ tầng**: ổ gà, lún nứt; biển báo, vạch sơn hỏng hoặc mờ; hộ lan, rào chắn hư; đèn chiếu sáng; camera, biển báo điện tử hỏng.
4. **Điều kiện lưu thông**: ùn tắc, sương mù, mưa lớn, ngập nước, khói đốt đồng.
5. **Khác**.

Mỗi loại có **mức ưu tiên mặc định** (Khẩn cấp / Cao / Thường), từ đó quyết định SLA và kênh thông báo.

## 5. Tính năng

### 5.1. Ứng dụng người dân (MVP)

- **Gửi phản ánh trong 3 bước**: chọn loại → chụp ảnh hoặc quay video (tối đa 30 giây) **trực tiếp trong ứng dụng** → gửi. Mô tả và biển số xe là tùy chọn.
- **Định vị tự động**: tọa độ GPS được đổi sang *đoạn tuyến, lý trình Km+m, chiều đi*. VD: "Diễn Châu – Bãi Vọt, Km 15+300, hướng Hà Tĩnh". Người dùng có thể kéo ghim để chỉnh.
- **An toàn khi đang di chuyển**: khi tốc độ trên 10 km/h, ứng dụng nhắc "Chỉ dùng khi là hành khách hoặc đã dừng xe an toàn"; có thể gửi bằng giọng nói, nút gửi nhanh cỡ lớn.
- **Nút gọi khẩn cấp**: 113, 114, 115 và đường dây nóng Đội 4.
- **Theo dõi trạng thái** phản ánh, nhận thông báo đẩy khi có kết quả, đánh giá mức độ hài lòng.
- **Gửi khi mất sóng**: lưu hàng đợi trên máy, tự gửi lại khi có mạng, giữ nguyên thời gian và vị trí lúc chụp.
- **Video sự việc đã xảy ra** (VD: trích từ camera hành trình): cho phép tải lên, nhưng đánh dấu "nguồn ngoài" và yêu cầu thẩm định kỹ hơn (xem mục 7.1).

### 5.2. Cổng điều hành của Đội 4 (web)

- **Bản đồ thời gian thực** toàn tuyến Nghi Sơn – Cam Lộ, lọc theo đoạn, loại, mức ưu tiên, trạng thái.
- **Gộp phản ánh trùng**: cùng loại, cùng chiều, cách nhau không quá 500 m và 15 phút thì gợi ý gộp thành một sự vụ. Số người cùng báo là tín hiệu cho độ tin cậy.
- **Phân công và SLA**: tự chuyển cho tổ phụ trách theo lý trình, đếm ngược thời hạn, nhắc và báo lên cấp trên khi quá hạn.
- **Chuyển tiếp ra ngoài**: phản ánh về hạ tầng gửi cho đơn vị quản lý đoạn tuyến tương ứng; sự cố cần cứu hộ gửi tới đơn vị cứu hộ.
- **Luồng xử lý vi phạm**: xem mục 6.2.
- **Phản hồi người dân** bằng mẫu soạn sẵn; nhật ký ghi lại mọi thao tác (audit log).
- **Báo cáo**: số phản ánh theo đoạn, loại, thời gian; thời gian xử lý trung bình; bản đồ nhiệt điểm đen; xuất Excel/PDF theo mẫu báo cáo của Đội.

### 5.3. Ứng dụng cho tổ tuần tra (giai đoạn 2)

Nhận việc, dẫn đường tới lý trình, cập nhật "đã đến hiện trường / đã xử lý" kèm ảnh.

### 5.4. Mở rộng (giai đoạn 3)

- AI hỗ trợ: phân loại ảnh, nhận dạng biển số, **tự làm mờ khuôn mặt và biển số** trước khi hiển thị cho người không có thẩm quyền.
- Cảnh báo ngược tới người dân đang đi trên tuyến (VD: sự cố phía trước X km).
- Kết nối camera giám sát, biển báo điện tử trên tuyến và hệ thống nghiệp vụ của ngành.

## 6. Quy trình xử lý

### 6.1. Luồng chung

```
Mới ──► Đã tiếp nhận ──► Đã chuyển tổ/đơn vị ──► Đang xử lý ──► Đã xử lý ──► Đóng
  │            │                                                     ▲
  └─► Trùng (gộp vào sự vụ khác)   └─► Không xác minh được / Từ chối (nêu lý do)
```

SLA đề xuất (Đội 4 quyết định): Khẩn cấp — tiếp nhận trong 2 phút; Cao — trong 15 phút; Thường — trong 24 giờ.

### 6.2. Luồng phản ánh vi phạm làm căn cứ xử lý

```
Phản ánh vi phạm ──► Thẩm định bằng chứng ──► Đủ điều kiện? ──Không──► Chỉ lưu thống kê, phản hồi người gửi
                                                 │
                                                Có
                                                 ▼
                         Xác minh phương tiện, chủ xe ──► Lập hồ sơ theo quy trình ──► Thông báo, xử lý
                                                 ──► Cập nhật kết quả cho người gửi
```

**Tiêu chí thẩm định** (đề xuất, cần cán bộ pháp chế xác nhận):

- Nhìn rõ hành vi, biển số, có mốc nhận biết vị trí.
- Còn nguyên thời gian và tọa độ gốc; mã băm (hash) của file khớp với lúc tải lên.
- Người gửi đã định danh (xem 7.2) và đồng ý cung cấp thông tin khi cơ quan chức năng cần làm rõ.
- Gửi trong thời hạn quy định kể từ khi sự việc xảy ra.

## 7. Pháp lý, bảo mật, chống lạm dụng

### 7.1. Giá trị pháp lý của bằng chứng

- Vì phản ánh được dùng làm căn cứ xử lý, **cán bộ pháp chế cần rà soát** quy trình tiếp nhận và sử dụng hình ảnh do cá nhân cung cấp theo Luật Trật tự, an toàn giao thông đường bộ và các thông tư của Bộ Công an về tuần tra, kiểm soát, xử lý vi phạm.
- **Chuỗi lưu giữ bằng chứng**: file gốc được lưu nguyên, không nén lại; có mã băm SHA-256, thời gian máy chủ nhận, tọa độ và thông tin thiết bị; mọi lượt xem hoặc tải xuống đều ghi nhật ký.
- Ưu tiên ảnh và video **chụp trực tiếp trong ứng dụng**. File tải từ ngoài vào (camera hành trình) chỉ được dùng khi thẩm định đạt yêu cầu.

### 7.2. Định danh người gửi

- **MVP**: số điện thoại + OTP là bắt buộc.
- **VNeID ("nên có")**: tích hợp ngay khi được cấp phép kết nối. Đề xuất **bắt buộc VNeID cho phản ánh dùng làm căn cứ xử lý**. Phản ánh thông thường (sự cố, hạ tầng) chỉ cần số điện thoại để không cản trở người dân báo tin.
- Thông tin người gửi **không bao giờ** công khai cho người bị phản ánh.

### 7.3. Trùng lặp với nền tảng hiện có

Cục CSGT đã có ứng dụng **VNeTraffic**, trong đó có chức năng phản ánh vi phạm. Trước khi xây dựng, Đội 4 nên **xin ý kiến cấp trên** để chọn một trong ba hướng:

| Hướng | Ưu điểm | Nhược điểm |
|---|---|---|
| (a) Ứng dụng riêng cho tuyến | Chủ động, làm sâu theo lý trình, có SLA | Trùng chức năng, người dân phải cài thêm ứng dụng |
| (b) **Cổng điều hành riêng, nhận dữ liệu từ VNeTraffic** và ứng dụng riêng chỉ làm kênh phụ | Tận dụng nền tảng sẵn có | Phụ thuộc khả năng kết nối dữ liệu |
| (c) Đề xuất bổ sung tính năng vào VNeTraffic | Không phát sinh hệ thống mới | Đội không chủ động tiến độ |

**Khuyến nghị**: hướng (b). Phần có giá trị nhất cho Đội 4 là **cổng điều hành theo lý trình và SLA**, phần này cần làm dù nguồn phản ánh đến từ đâu.

### 7.4. Bảo mật và chống lạm dụng

- Hạ tầng đặt tại Việt Nam, ưu tiên hạ tầng của ngành Công an nếu được bố trí; phân quyền theo vai trò; mã hóa dữ liệu khi truyền và khi lưu; kiểm thử bảo mật trước khi vận hành.
- Thu thập dữ liệu cá nhân ở mức tối thiểu, xin đồng ý rõ ràng, có chính sách quyền riêng tư.
- Chống lạm dụng: giới hạn số lần gửi, chấm điểm uy tín người gửi, phát hiện ảnh trùng hoặc ảnh cũ, khóa tài khoản báo sai nhiều lần.

## 8. Kiến trúc kỹ thuật đề xuất

| Thành phần | Lựa chọn | Lý do |
|---|---|---|
| Ứng dụng người dân | **PWA** cho MVP (dùng camera, GPS, chạy khi mất mạng, cài được lên màn hình chính); sau đó làm app native bằng Flutter hoặc React Native | Ra mắt nhanh, không phải chờ duyệt trên kho ứng dụng |
| Cổng điều hành | React/Next.js + bản đồ MapLibre | Tự host được, không phụ thuộc dịch vụ bản đồ nước ngoài |
| Backend API | NestJS (Node) hoặc FastAPI (Python) | Phổ biến, dễ tuyển người |
| Cơ sở dữ liệu | **PostgreSQL + PostGIS** | Đổi tọa độ GPS sang lý trình bằng `ST_LineLocatePoint` trên dữ liệu tim tuyến |
| Lưu ảnh, video | Object storage tương thích S3, khóa chống sửa (WORM) cho bằng chứng vi phạm | Bảo toàn bằng chứng |
| Thời gian thực | Redis + WebSocket | Sự vụ mới hiện lên bản đồ ngay |
| Thông báo | FCM/APNs, SMS dự phòng | |

### Mô hình dữ liệu chính (rút gọn)

- `nguoi_dung` (id, sdt, vneid_xac_thuc, vai_tro, to_cong_tac_id, diem_uy_tin)
- `doan_tuyen` (id, ten, km_dau, km_cuoi, hinh_hoc_chieu_bac_nam, hinh_hoc_chieu_nam_bac, don_vi_quan_ly)
- `dia_ban_to` (to_cong_tac_id, doan_tuyen_id, km_tu, km_den)
- `phan_anh` (id, nguoi_gui_id, loai, muc_uu_tien, vi_tri, doan_tuyen_id, ly_trinh_m, chieu, mo_ta, bien_so, thoi_diem_chup, nguon_media, trang_thai, su_vu_id)
- `su_vu` (id, loai, doan_tuyen_id, ly_trinh_m, chieu, trang_thai, to_xu_ly_id, han_xu_ly)
- `ho_so_vi_pham` (id, su_vu_id, ket_qua_tham_dinh, can_bo_tham_dinh_id, bien_so, trang_thai, ket_qua_xu_ly)
- `tep_dinh_kem` (id, phan_anh_id, url, loai, sha256, exif, khoa_worm)
- `nhat_ky` (id, doi_tuong, hanh_dong, nguoi_thuc_hien, thoi_diem, du_lieu)

## 9. Lộ trình

| Giai đoạn | Thời gian | Kết quả |
|---|---|---|
| 0. Khảo sát và thống nhất | 3–4 tuần | Chốt hướng (a/b/c) ở mục 7.3; thu thập tim tuyến, lý trình, địa bàn các tổ; pháp chế duyệt luồng 6.2 |
| 1. MVP | 8–10 tuần | PWA người dân + cổng điều hành + backend. **Thí điểm 1–2 đoạn** (gợi ý: Nghi Sơn – Diễn Châu và Diễn Châu – Bãi Vọt, đã khai thác lâu nhất, nhiều dữ liệu đối chiếu) |
| 2. Mở rộng toàn tuyến | 2–3 tháng | Đủ 6 đoạn đến Cam Lộ; ứng dụng tổ tuần tra; luồng xử lý vi phạm chạy thật; tích hợp VNeID |
| 3. Nâng cao | sau 6 tháng | App native, AI, kết nối camera và biển báo điện tử, cảnh báo ngược tới người dân |

**Nhân sự MVP gợi ý**: 1 PM/BA, 1 UI/UX, 2 backend, 1–2 frontend, 1 QA, 0,5 DevOps/GIS. Phía Đội 4: 1 đầu mối nghiệp vụ, 1 cán bộ pháp chế.

## 10. Chỉ số đánh giá (KPI)

- Thời gian gửi phản ánh (trung vị) không quá 30 giây.
- Ít nhất 95% phản ánh xác định đúng đoạn tuyến và chiều đi; sai số lý trình không quá 200 m.
- Ít nhất 90% sự vụ được tiếp nhận đúng SLA theo từng mức ưu tiên.
- Ít nhất 95% phản ánh có phản hồi kết quả cho người gửi.
- Tỷ lệ phản ánh vi phạm đạt thẩm định, được lập hồ sơ (theo dõi; chưa đặt chỉ tiêu ở giai đoạn đầu).
- Mức hài lòng từ 4/5 trở lên; tỷ lệ phản ánh sai hoặc spam không quá 10%.

## 11. Rủi ro chính

| Rủi ro | Giảm thiểu |
|---|---|
| Tài xế thao tác điện thoại khi đang lái | Nhắc theo tốc độ, gửi bằng giọng nói, truyền thông "hành khách báo, tài xế lái" |
| GPS lệch giữa hai chiều đường | Dùng hướng di chuyển + cho phép chỉnh tay |
| Bằng chứng bị khiếu nại, không đủ giá trị pháp lý | Chuỗi lưu giữ bằng chứng (7.1), pháp chế duyệt trước khi chạy |
| Lợi dụng để tố cáo sai, trả thù cá nhân | Định danh, điểm uy tín, thẩm định trước khi lập hồ sơ |
| Trùng lặp với VNeTraffic | Chốt hướng ở giai đoạn 0 |
| Ít người dùng | Mã QR tại trạm dừng nghỉ, nút giao, biển báo điện tử; truyền thông qua báo địa phương và mạng xã hội của Đội |
| Lộ dữ liệu cá nhân, hình ảnh | Phân quyền, làm mờ, audit log, kiểm thử bảo mật |

## 12. Việc cần làm tiếp theo

1. Đội 4 xin ý kiến cấp trên về hướng (a/b/c) ở mục 7.3.
2. Gửi danh sách dữ liệu cần cung cấp ở mục 1 (lý trình, địa bàn các tổ, đơn vị quản lý tuyến, đường dây nóng).
3. Pháp chế rà soát luồng 6.2 và tiêu chí thẩm định bằng chứng.
4. Làm thủ tục xin kết nối VNeID.
5. Xác định nơi đặt hạ tầng (hạ tầng ngành Công an hay đám mây trong nước).
