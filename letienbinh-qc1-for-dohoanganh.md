# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): dohoanganh        Người kiểm (học viên): letienbinh  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `dohoanganh-front.zip` (sha256 `91a31187…d41d310`), `dohoanganh-fisheye.zip` (sha256 `f35270a4…b9b4b9`); chưa nhận manifest nên không có `revision`  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 76 (52 shape + 24 tag)

Ảnh đã kiểm: A03, A04, A05, A08, B02, B05. Chọn để phủ đủ các nhóm: làn bị che và đèn (A03), vàng đôi và direct/alternative (A04), vùng lái và mép lề (A05), nhiều cụm đèn và biển (A08), đèn sát mép fisheye (B02), camera hai bên và crosswalk (B05).

Cột "Nhãn" ghi `label#n`: `n` là thứ tự shape trong ảnh của file export, giống số `#n` mà `road_check lint` in ra. Tọa độ (x, y) tính theo pixel ảnh gốc.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 8 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 8 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 8 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 8 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 17 | 4 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 17 | 3 | nặng |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 27 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 10 | 2 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 8 | 2 | chính |
| QC1-12 file | lỗi file | 2 | 10 | nhẹ |

Cách đếm số mục kiểm:
- QC1-01: tag camera của 6 ảnh.
- QC1-02: hai vị trí L1, R1 trên mỗi ảnh.
- QC1-03 đến QC1-06: 8 polyline `lane`.
- QC1-07: 9 `drivable`, 3 `crosswalk`, 5 `road_curb`.
- QC1-08: 17 đèn.
- QC1-09: 17 đèn cộng 10 biển.
- QC1-10: 10 biển.
- QC1-11: 8 shape trên B02 và B05.
- QC1-12: 2 file.

QC1-02 ở A05: `lint` báo thiếu L1, R1, nhưng ảnh không có vạch sơn (đường phố hai bên đỗ xe), nên không tính là lỗi. Cần coach xác nhận để miễn.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-08 | A03 | traffic_light#4 (707,314) | nặng | Đèn quay về xe (`facing = front`) đang sáng **xanh**, gán `color = yellow` |
| 2 | QC1-08 | A04 | traffic_light#3 (550,267) | nặng | Đèn `facing = front` đang sáng **xanh**, gán `color = yellow` |
| 3 | QC1-08 | B02 | traffic_light#3 (1074,77) | nặng | Đèn `facing = front` có bóng xanh đang sáng (hơi mờ), gán `color = unknown`; xem mục Ca mơ hồ |
| 4 | QC1-07 | A04 | drivable#0 | chính | Polygon làn đang đi (giữa L1 vàng đôi và R1) gán `area_type = alternative`; ảnh không có polygon `direct` nào |
| 5 | QC1-07 | A05 | drivable#0 | chính | Polygon duy nhất là làn đang đi nhưng gán `alternative`; ảnh không có `direct` |
| 6 | QC1-07 | A05 | drivable#0 | chính | Polygon tràn vào dải đỗ xe hai bên: cạnh trái xuống tới (0,425) dưới hàng xe đỗ, cạnh phải sang tới vỉa (1280,425) |
| 7 | QC1-07 | A03 | drivable#7 | chính | Polygon `alternative` bên phải kéo tới hàng xe đỗ, gồm cả dải đỗ xe bên ngoài vạch trắng đứt sát lề |
| 8 | QC1-05 | A04 | lane#9, lane#10 | chính | Vạch vàng đôi L1 vẽ thành 2 polyline; theo guideline là 1 polyline ở giữa hai nét, `kind = double` |
| 9 | QC1-10 | A03 | (thiếu) traffic_sign tại ≈(1005–1040, 285–325) | chính | Thiếu biển vàng-xanh trường học / người đi bộ (cao khoảng 40 px), `group = warning` |
| 10 | QC1-10 | A08 | (thiếu) traffic_sign tại ≈(778–856, 38–60) | chính | Thiếu tấm biển trắng "PASSENGER CARS ONLY" phía trên biển xanh `traffic_sign#1`; cần hộp riêng |
| 11 | QC1-11 | B02 | traffic_light#2 (105,88) | chính | Tâm hộp nằm ngoài 80 % bán kính vòng ảnh nhưng `edge_zone` chưa bật |
| 12 | QC1-11 | B02 | traffic_light#3 (1074,77) | chính | Tâm hộp nằm ngoài 80 % bán kính vòng ảnh nhưng `edge_zone` chưa bật |
| 13 | QC1-12 | A03 | drivable#7 | nhẹ | 1 điểm lặp liền nhau (click hai lần) |
| 14 | QC1-12 | A04 | drivable#0 | nhẹ | 1 điểm lặp liền nhau |
| 15 | QC1-12 | A04 | road_curb#1 | nhẹ | 1 điểm lặp liền nhau |
| 16 | QC1-12 | A04 | drivable#11 | nhẹ | 1 điểm lặp liền nhau |
| 17 | QC1-12 | A05 | drivable#0 | nhẹ | 2 điểm lặp liền nhau |
| 18 | QC1-12 | A08 | lane#17 | nhẹ | 3 điểm lặp liền nhau |
| 19 | QC1-12 | B02 | crosswalk#0 | nhẹ | 1 điểm lặp liền nhau |
| 20 | QC1-12 | B02 | drivable#1 | nhẹ | 1 điểm lặp liền nhau |
| 21 | QC1-12 | B05 | road_curb#0 | nhẹ | 3 điểm lặp liền nhau |
| 22 | QC1-12 | B05 | drivable#2 | nhẹ | 1 điểm lặp liền nhau |

Ảnh kiểm **không thấy lỗi**: không có. Ảnh ít vấn đề nhất là B05: tag `fisheye_left` đúng, `crosswalk` bao đủ vạch, `road_curb` theo cung. B05 chỉ có lỗi nhẹ do điểm lặp, cộng một câu hỏi về `area_type` ở mục Ca mơ hồ.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| B02 | Đèn `traffic_light#3` có bóng xanh nhưng mờ do ngược sáng: gán `unknown` có chấp nhận được không, hay phải là `green`? Phiếu tạm xếp mức nặng (theo thang: phân vân thì chọn mức cao hơn) | |
| A03 | Trời đã chiều, ánh sáng vàng: `timeofday = dusk` hay `day`? Không tính lỗi | |
| B05 | Với camera hai bên, phần mặt đường sát thân xe là làn đang đi (`direct`) hay làn bên cạnh (`alternative`)? Guideline chưa nói; không tính lỗi | |
| A05 | Ảnh không có vạch sơn nào; xin coach xác nhận để miễn QC1-02 (thiếu L1/R1) | |

## Quyết định
Lỗi nặng: 3   Lỗi chính: 9 / 76 nhãn = 11,8 %   Lỗi nhẹ: 10   Ca chờ lead: 4  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Còn 3 lỗi nặng (QC1-08, sai màu đèn quay về xe ở A03, A04, B02), và chỉ một lỗi nặng đã đủ để Rework. Ngoài ra tỉ lệ lỗi chính là 11,8 %, vượt ngưỡng 5 %. Kể cả khi lead trả lời B02 không phải lỗi, A03 và A04 vẫn còn lỗi nặng nên quyết định không đổi; vì vậy chọn Rework chứ không Hold.

## Ghi chú thêm cho người gán (ngoài 6 ảnh mẫu, không tính vào tỉ lệ)
Các điểm dưới đây thấy qua `road_check lint` và đọc file, để bạn sửa luôn khi Rework:
- A09 (L2) và A11 (L1): vạch đôi cũng đang vẽ thành 2 polyline (QC1-05).
- A07: mặt đường ướt và kính có giọt nước nhưng `weather = overcast`; nên là `rain`.
- A14 (ảnh thêm): chưa có nhãn và chưa có tag nào. A13, A15, A16 không có trong file. Ảnh thêm không bắt buộc, nhưng nên xoá A14 khỏi file nếu không làm.
- B08 `lane#4`: chỉ có 3 điểm trên fisheye, nên thêm điểm theo cung (QC1-11).

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
