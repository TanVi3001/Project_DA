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
* **Làm sạch & Xử lý dữ liệu:** Python (Pandas)
* **Trực quan hóa dữ liệu:** Python (Matplotlib, Seaborn)
* **Môi trường:** Google Colab / Jupyter Notebook

---

## 🔍 Quy trình Phân tích 6 bước (Google Data Analytics Framework)

### 1. ASK (Đặt câu hỏi)
Dự án được định hướng bởi 3 câu hỏi nghiên cứu cốt lõi:
1. Dòng gen (`RAL_full`) nào có mức độ vận động trung bình cao nhất và thấp nhất?
2. Hành vi vận động thay đổi như thế nào theo các thời điểm trong ngày (Nhịp sinh học)?
3. Mức độ hoạt động có bị suy giảm qua các ngày quan sát (`batch`) trong môi trường thí nghiệm không?

### 2. PREPARE (Chuẩn bị dữ liệu)
* Dữ liệu được thu thập và lưu trữ an toàn dưới định dạng CSV.
* Đánh giá cấu trúc: Dữ liệu bao gồm các kiểu `int64` (số nguyên) và `object` (chuỗi văn bản). 
* Giới hạn: Dữ liệu tập trung hoàn toàn vào mức độ hoạt động thể chất, không bao gồm các nhãn y sinh học cụ thể của từng dòng gen.

### 3. PROCESS (Xử lý và Làm sạch dữ liệu)
* **Ép kiểu dữ liệu:** Chuyển đổi cột `datetime` từ định dạng chuỗi sang định dạng `datetime` chuẩn, xử lý các lỗi chuỗi bằng `errors='coerce'` và loại bỏ các dòng `NaT`.
* **Trích xuất đặc trưng (Feature Engineering):** Tạo thêm các cột mới `Hour` (Giờ) và `Date` (Ngày) từ cột `datetime` để phục vụ cho phân tích chuỗi thời gian (Time-series).
* **Kiểm tra tính toàn vẹn:** Xác nhận cột `act_sum` không chứa giá trị âm vô lý (Min = 0).

### 4. ANALYZE (Phân tích dữ liệu)
* Sử dụng phép tính gộp nhóm (`groupby`) để tính trung bình mức độ hoạt động (`act_sum` mean) theo từng dòng gen (`RAL_full`).
* Tổng hợp dữ liệu theo cột `Hour` để phác thảo biểu đồ nhịp sinh học 24 giờ.
* Đánh giá phương sai và sự ổn định của dữ liệu qua các ngày (`batch`).

### 5. SHARE (Trực quan hóa)
Quá trình trực quan hóa được thực hiện với 3 biểu đồ chính:
1. **Line Chart:** Mô tả nhịp độ hoạt động theo từng khung giờ trong ngày (từ 0h - 23h).
2. **Bar Chart:** Xếp hạng Top 5 dòng gen năng động nhất so với Top 5 dòng gen thụ động nhất.
3. **Box Plot:** Thể hiện độ phân tán mức độ hoạt động giữa các chu kỳ quan sát (ẩn Outliers để thấy rõ xu hướng chung).

*(Lưu ý: Bạn có thể lưu hình ảnh biểu đồ từ Google Colab và upload vào GitHub, sau đó chèn link ảnh vào đây bằng cú pháp: `![Tên ảnh](Link_ảnh)`)*

### 6. ACT (Kết luận & Đề xuất)
**💡 Các Phát Hiện Chính (Key Insights):**
* **Nhịp sinh học rõ rệt:** Ruồi giấm (Drosophila) thể hiện nhịp sinh học hàng ngày rất đặc trưng. Mức độ hoạt động tạo thành các đỉnh (peaks) vào những khung giờ nhất định và giảm mạnh vào thời gian nghỉ ngơi.
* **Yếu tố di truyền quyết định mức độ vận động:** Có sự phân hóa cực kỳ mạnh mẽ về mức độ hoạt động trung bình giữa 105 dòng gen. Dòng gen năng động nhất có chỉ số `act_sum` cao gấp nhiều lần so với dòng gen lười nhất. 
* **Độ ổn định thí nghiệm:** Mức độ hoạt động trung bình qua các ngày (`day1`, `day2`...) duy trì ở mức ổn định, khẳng định môi trường thí nghiệm được kiểm soát tốt và không làm suy giảm thể lực của ruồi.

**🚀 Đề xuất & Hướng nghiên cứu tiếp theo (Next Steps):**
* **Đối chiếu dữ liệu y sinh:** Khuyến nghị các nhà nghiên cứu sinh học tập trung giải trình tự gen của **Top 5 dòng gen thụ động nhất**. Mục tiêu là kiểm tra xem chúng có mang các đột biến gen tương đồng với bệnh lý suy giảm vận động ở người (như mô hình bệnh Parkinson) hay không.
* **Tối ưu hóa thiết kế thí nghiệm:** Các thử nghiệm thuốc (drug testing) vận động trong tương lai nên được lên lịch diễn ra vào đúng các khung giờ hoạt động "đỉnh" để thu được kết quả đo lường nhạy bén nhất.

---

## 💻 Hướng dẫn chạy dự án (How to Use)
1. Clone repository này về máy của bạn:
   ```bash
   git clone [https://github.com/TanVi3001/Project_DA.git](https://github.com/TanVi3001/Project_DA.git)
