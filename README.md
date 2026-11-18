# Lập kế hoạch tài chính cá nhân bằng Chain-of-Thought

## Phần A: Prompt

### Mục tiêu của bài toán

1. Luyện tư duy suy luận logic phức tạp bằng kỹ thuật Chain-of-Thought: chia bài toán thành các bước nhỏ, mỗi bước có đầu vào, công thức, kết quả rõ ràng.
2. Kiểm soát các bước lập luận trung gian để hạn chế sai sót số học của mô hình ngôn ngữ.
3. Trình bày kết quả trực quan gồm hai phần: phân tích logic và bảng tổng hợp số liệu.

### Vai trò

Bạn là chuyên gia lập kế hoạch tài chính cá nhân, làm việc cẩn thận, không làm tròn tùy tiện. Người dùng có thu nhập biến động hàng tháng và đang trả nợ.

### Dữ liệu đầu vào

1. Thu nhập: thu nhập gộp 3 tháng gần nhất [tháng 1, tháng 2, tháng 3] VND. Lập kế hoạch theo mức thấp nhất trong 3 tháng. Thuế và khấu trừ: [số tiền hoặc %].
2. Chi phí cố định bắt buộc: [khoản 1: số tiền], [khoản 2: số tiền], ...
3. Các khoản nợ: [tên, dư nợ, lãi suất %/năm, trả tối thiểu/tháng, hạn trả ngày]
4. Mục tiêu tiết kiệm: tối thiểu 20% thu nhập sau thuế; quỹ dự phòng mục tiêu [số tiền], hiện có [số tiền]; mục tiêu khác [nếu có].

### Chỉ thị tư duy

Hãy suy nghĩ từng bước một và tính toán chi tiết trước khi đưa ra quyết định.

### Quy tắc kiểm soát sai số (áp dụng cho mọi bước)

- a. Mỗi phép tính viết trên một dòng riêng theo dạng: tên đại lượng = công thức = kết quả (ví dụ: Tổng chi cố định = 3.000.000 + 500.000 + 200.000 = 3.700.000).
- b. Chỉ thực hiện một phép toán mỗi dòng. Phép nhiều số thì cộng dồn từng cặp.
- c. Dùng đơn vị VND thống nhất, không làm tròn ở bước trung gian. Chỉ làm tròn ở bảng cuối và ghi rõ chỗ đã làm tròn.
- d. Sau mỗi bước, ghi một dòng "Điểm kiểm tra" nêu lại kết quả chính và tính lại bằng cách khác (ví dụ: dùng phép trừ ngược) để đối chiếu. Nếu hai kết quả lệch nhau, tính lại trước khi đi tiếp.
- e. Mỗi bước phải ghi rõ dùng kết quả của bước nào trước đó, không tự bịa số mới.
- f. Nếu dữ liệu đầu vào thiếu hoặc mâu thuẫn, hỏi lại hoặc nêu giả định rõ ràng, không tự điền số.

### Quy trình lập luận bắt buộc

Bước 1: Thu nhập khả dụng.
- Thu nhập sau thuế = thu nhập gộp − thuế và khấu trừ.
- Tổng chi phí cố định = cộng từng khoản.
- Thu nhập khả dụng = thu nhập sau thuế − tổng chi phí cố định.

Bước 2: Trả nợ tối thiểu.
- Tổng nợ tối thiểu = cộng từng khoản.
- Số dư sau nợ tối thiểu = thu nhập khả dụng − tổng nợ tối thiểu.
- Nếu số dư âm: dừng lại, báo thâm hụt, đề xuất hướng xử lý (cắt giảm chi, tái cơ cấu nợ, tăng thu nhập) rồi mới làm tiếp.

Bước 3: Trích lập tiết kiệm.
- Tiết kiệm tối thiểu = 20% × thu nhập sau thuế.
- Chia giữa quỹ dự phòng và mục tiêu khác, ưu tiên quỹ dự phòng nếu chưa đủ.
- Kiểm tra số dư còn lại có đủ không. Nếu không đủ, nêu mâu thuẫn và cách cân đối, không âm thầm hạ tiết kiệm dưới 20%.

Bước 4: Chia phần còn lại theo quy tắc 50/30/20 cải tiến (tính trên thu nhập sau thuế).
- Nhóm Thiết yếu = chi cố định + nợ tối thiểu, tính tỷ lệ thực tế so với mục tiêu 50%.
- Nhóm Tiết kiệm đã chốt ở Bước 3.
- Nhóm Linh hoạt = thu nhập sau thuế − thiết yếu − tiết kiệm, chia thành chi tiêu hàng ngày, giải trí, trả nợ vượt mức (ưu tiên khoản lãi suất cao nhất).
- Nếu thiết yếu vượt 50% thì nhóm linh hoạt co lại, tiết kiệm không bao giờ dưới 20%.

### Định dạng đầu ra

- Phần 1: Nhật ký suy luận logic (Reasoning Steps). Trình bày Bước 1 đến Bước 4, mỗi bước gồm các dòng phép tính, kết quả trung gian và Điểm kiểm tra.
- Phần 2: Bảng phân bổ ngân sách cuối cùng bằng Markdown Table, đúng 4 cột: Hạng mục | Số tiền | Tỷ lệ % | Ghi chú, có dòng Tổng cộng.

### Ràng buộc cuối (tự kiểm tra trước khi trả lời)

- Tổng số tiền các hạng mục bằng chính xác thu nhập sau thuế.
- Tổng tỷ lệ % bằng chính xác 100%. Nếu làm tròn gây lệch, điều chỉnh ở hạng mục linh hoạt lớn nhất và ghi chú.
- Tiết kiệm ≥ 20%, mọi khoản nợ trả đủ mức tối thiểu, đúng hạn.
- Cuối Phần 2 thêm dòng "Kiểm tra" ghi lại phép cộng tổng tiền và tổng % để chứng minh khớp.
- Không dùng code Python hay thư viện, chỉ tính bằng lập luận từng bước.

---

## Phần B: Dữ liệu chạy thử

- Thu nhập gộp 20.000.000 (giả định cả 3 tháng như nhau nên lấy 20.000.000), khấu trừ 10%.
- Chi cố định: thuê nhà 4.500.000, điện nước internet 800.000, đi lại 1.200.000, ăn uống thiết yếu 3.000.000.
- Nợ 1: thẻ tín dụng, dư nợ 20.000.000, lãi 30%/năm, trả tối thiểu 1.000.000, hạn ngày 15.
- Nợ 2: vay tiêu dùng, dư nợ 30.000.000, lãi 18%/năm, trả tối thiểu 1.500.000, hạn ngày 5.
- Quỹ dự phòng mục tiêu 27.000.000, hiện có 5.000.000.
- Giả định: nhóm linh hoạt chia 50% trả nợ lãi cao nhất, 33,33% chi tiêu hàng ngày, 16,67% giải trí.

---

## Phần C: Kết quả chạy thử

### Phần 1: Nhật ký suy luận logic

Bước 1: Thu nhập khả dụng
- Khấu trừ = 20.000.000 × 10% = 2.000.000
- Thu nhập sau thuế = 20.000.000 − 2.000.000 = 18.000.000
- Chi cố định: 4.500.000 + 800.000 = 5.300.000
- 5.300.000 + 1.200.000 = 6.500.000
- 6.500.000 + 3.000.000 = 9.500.000
- Thu nhập khả dụng = 18.000.000 − 9.500.000 = 8.500.000
- Điểm kiểm tra: 8.500.000 + 9.500.000 = 18.000.000, khớp.

Bước 2: Trả nợ tối thiểu
- Tổng nợ tối thiểu = 1.000.000 + 1.500.000 = 2.500.000
- Số dư sau nợ = 8.500.000 − 2.500.000 = 6.000.000
- Số dư dương nên đi tiếp.
- Điểm kiểm tra: 6.000.000 + 2.500.000 = 8.500.000, khớp.

Bước 3: Tiết kiệm
- Tiết kiệm tối thiểu = 18.000.000 × 20% = 3.600.000
- Quỹ dự phòng còn thiếu = 27.000.000 − 5.000.000 = 22.000.000, nên dồn hết 3.600.000 vào quỹ dự phòng.
- Số dư còn lại = 6.000.000 − 3.600.000 = 2.400.000
- Điểm kiểm tra: 2.400.000 + 3.600.000 = 6.000.000, khớp.

Bước 4: Quy tắc 50/30/20 cải tiến
- Thiết yếu = 9.500.000 + 2.500.000 = 12.000.000
- Tỷ lệ thiết yếu = 12.000.000 ÷ 18.000.000 = 66,67%, vượt mục tiêu 50%, nên nhóm linh hoạt bị co lại.
- Linh hoạt = 18.000.000 − 12.000.000 − 3.600.000 = 2.400.000, tức 13,33%
- Ưu tiên nợ lãi cao nhất là thẻ tín dụng 30%/năm:
- Trả nợ thẻ vượt mức = 2.400.000 × 50% = 1.200.000
- Chi tiêu hàng ngày = 800.000
- Giải trí = 2.400.000 − 1.200.000 − 800.000 = 400.000
- Điểm kiểm tra: 1.200.000 + 800.000 + 400.000 = 2.400.000, khớp.

### Phần 2: Bảng phân bổ ngân sách

| Hạng mục | Số tiền (VND) | Tỷ lệ % | Ghi chú |
|---|---|---|---|
| Chi phí cố định | 9.500.000 | 52,78 | Nhà, điện nước, đi lại, ăn uống |
| Nợ tối thiểu | 2.500.000 | 13,89 | Vay tiêu dùng ngày 5, thẻ tín dụng ngày 15 |
| Quỹ dự phòng | 3.600.000 | 20,00 | Đúng mức tối thiểu 20% |
| Trả nợ thẻ vượt mức | 1.200.000 | 6,67 | Lãi cao nhất, 30%/năm |
| Chi tiêu hàng ngày | 800.000 | 4,44 | Phát sinh linh hoạt |
| Giải trí | 400.000 | 2,22 | Phần co lại nhiều nhất |
| Tổng cộng | 18.000.000 | 100,00 | |

Kiểm tra
- Tiền: 9.500.000 + 2.500.000 = 12.000.000; + 3.600.000 = 15.600.000; + 1.200.000 = 16.800.000; + 800.000 = 17.600.000; + 400.000 = 18.000.000, khớp thu nhập sau thuế.
- Phần trăm: 52,78 + 13,89 = 66,67; + 20,00 = 86,67; + 6,67 = 93,34; + 4,44 = 97,78; + 2,22 = 100,00, khớp.

### Lịch trả nợ trong tháng

- Ngày 5: trả 1.500.000 (vay tiêu dùng).
- Ngày 15: trả 1.000.000 + 1.200.000 = 2.200.000 (thẻ tín dụng, gồm mức tối thiểu và phần vượt mức).

### Nhận xét

Thiết yếu chiếm 66,67% là điểm nghẽn chính. Muốn có thêm tiền trả nợ, nên xem lại chi cố định trước, nhất là tiền nhà và ăn uống.
