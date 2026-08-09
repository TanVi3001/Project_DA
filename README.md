# 🔬 Phân tích Hành vi Vận động của Ruồi giấm (Drosophila Behavioral Analysis)

## 📖 Giới thiệu Dự án (Introduction)
Đây là Dự án cuối khóa (Capstone Project) thuộc chứng chỉ **Google Data Analytics Professional Certificate**. 
Dự án tập trung phân tích dữ liệu hành vi vận động của các dòng ruồi giấm (Drosophila) khác nhau trong môi trường phòng thí nghiệm. Mục tiêu của dự án là khám phá nhịp sinh học tự nhiên và xác định sự khác biệt về mức độ hoạt động giữa các kiểu gen (genotypes), từ đó tạo tiền đề cho các nghiên cứu y sinh học sâu hơn (như mô hình bệnh Parkinson).

## 🗂️ Nguồn dữ liệu (Data Source)
* **Tên file:** `datadryad-upload.csv`
* **Kích thước:** 344,000 dòng x 9 cột.
* **Tình trạng:** Dữ liệu hoàn chỉnh, không có giá trị khuyết thiếu (Null/NaN values = 0).
* **Các biến chính:** 
  * `RAL_full`: Tên phân loại dòng gen (105 loại).
  * `datetime`: Thời gian ghi nhận dữ liệu cảm biến.
  * `batch`: Chu kỳ ngày đo lường (day1, day2...).
  * `act_sum`: Tổng mức độ hoạt động ghi nhận được.

## 🛠️ Công cụ sử dụng (Tools)
* **Làm sạch & Xử lý dữ liệu:** Python (Pandas) / SQL
* **Trực quan hóa dữ liệu:** Python (Matplotlib, Seaborn) / Tableau / Power BI
* **Môi trường:** Jupyter Notebook / Kaggle

---

## 🔍 Quy trình Phân tích 6 bước (Google Data Analytics Framework)

### 1. ASK (Đặt câu hỏi)
Dự án được định hướng bởi 3 câu hỏi kinh doanh/nghiên cứu cốt lõi:
1. Dòng gen (`RAL_full`) nào có mức độ vận động trung bình cao nhất và thấp nhất?
2. Hành vi vận động thay đổi như thế nào theo các thời điểm trong ngày (Nhịp sinh học)?
3. Mức độ hoạt động có bị suy giảm qua các ngày quan sát (`batch`) trong môi trường thí nghiệm không?

### 2. PREPARE (Chuẩn bị dữ liệu)
* Dữ liệu được thu thập và lưu trữ an toàn dưới định dạng CSV.
* Đánh giá cấu trúc: Dữ liệu bao gồm các kiểu `int64` (số nguyên) và `object` (chuỗi văn bản). 
* Giới hạn: Dữ liệu tập trung hoàn toàn vào mức độ hoạt động thể chất, không bao gồm các nhãn y sinh học cụ thể của từng dòng gen.

### 3. PROCESS (Xử lý và Làm sạch dữ liệu)
* **Ép kiểu dữ liệu:** Chuyển đổi cột `datetime` từ định dạng chuỗi (string) sang định dạng `datetime` chuẩn (`YYYY-MM-DD HH:MM:SS`).
* **Trích xuất đặc trưng (Feature Engineering):** Tạo thêm các cột mới `Hour` (Giờ) và `Date` (Ngày) từ cột `datetime` để phục vụ cho phân tích chuỗi thời gian (Time-series).
* **Kiểm tra tính toàn vẹn:** Xác nhận cột `act_sum` không chứa giá trị âm vô lý (Min = 0).

### 4. ANALYZE (Phân tích dữ liệu)
* Sử dụng phép tính gộp nhóm (`GROUP BY`) để tính trung bình mức độ hoạt động (`act_sum` mean) theo từng dòng gen (`RAL_full`).
* Tổng hợp dữ liệu theo cột `Hour` để phác thảo biểu đồ nhịp sinh học 24 giờ.
* Đánh giá phương sai và sự ổn định của dữ liệu qua các ngày (`batch`).

### 5. SHARE (Trực quan hóa)
*(Thêm link hoặc chèn hình ảnh biểu đồ của bạn vào đây)*
* **Bar Chart:** Xếp hạng Top 10 dòng gen năng động nhất vs. 10 dòng gen thụ động nhất.
* **Line Chart:** Mô tả nhịp độ hoạt động theo từng khung giờ trong ngày.
* **Box Plot:** Thể hiện độ phân tán mức độ hoạt động giữa các chu kỳ quan sát (day1, day2).

### 6. ACT (Kết luận & Đề xuất)
* **Kết luận chính:** 
  * [Điền phát hiện số 1 của bạn - VD: Có sự chênh lệch rõ rệt về mức độ hoạt động giữa các dòng gen...]
  * [Điền phát hiện số 2 của bạn - VD: Khung giờ hoạt động đỉnh điểm của ruồi giấm thường rơi vào...]
* **Đề xuất nghiên cứu tiếp theo (Next Steps):** Khuyến nghị các nhà nghiên cứu y sinh đối chiếu danh sách các dòng gen hoạt động yếu nhất với dữ liệu giải trình tự gen để xác định các đột biến suy giảm vận động (ví dụ: các gen liên quan đến Parkinson).

---

## 🚀 Hướng dẫn chạy dự án (How to Use)
1. Clone repository này về máy của bạn:
   ```bash
