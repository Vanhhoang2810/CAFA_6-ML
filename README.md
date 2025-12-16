# CAFA 6: Protein Function Prediction 🧬

Dự án tham gia thử thách CAFA 6 trên Kaggle, giải quyết bài toán dự đoán chức năng protein (Gene Ontology) sử dụng phương pháp tìm kiếm tương đồng (Similarity-based) kết hợp với tri thức sinh học.

## 👤 Thành viên thực hiện

| Họ và Tên | MSSV |
| :--- | :--- |
| Hoàng Việt Anh | 23020583 |

## 🛠️ Thành phần đóng góp (Key Contributions)

Dự án này tập trung vào việc cải thiện hiệu suất dự đoán so với mô hình Baseline (Logistic Regression) thông qua các kỹ thuật sau:

### 1. Xử lý dữ liệu & Đặc trưng (Feature Engineering)
- **TF-IDF Vectorization:** Sử dụng TF-IDF với N-gram cấp ký tự (3, 4) để biểu diễn chuỗi protein, thay thế cho phương pháp Hashing (dễ gây nhiễu).
- **Sublinear Scaling:** Áp dụng logarit lên tần suất từ để giảm thiểu tác động của các đoạn lặp lại (repeats).
- **Sparse Matrix Optimization:** Tối ưu hóa bộ nhớ để xử lý **100% dữ liệu huấn luyện** (thay vì 20% như baseline).

### 2. Thuật toán & Mô hình (Algorithm)
- **K-Nearest Neighbors (KNN):** Triển khai thuật toán tìm kiếm láng giềng gần nhất dựa trên độ đo **Cosine Similarity**.
- **Lazy Learning:** Không cần huấn luyện (training-free), mô hình so sánh trực tiếp protein truy vấn với cơ sở dữ liệu.

### 3. Heuristic Sinh học (Bio-Heuristics)
- **Taxonomy Bonus:** Tăng trọng số điểm tương đồng (**x1.3**) nếu protein truy vấn và protein mẫu thuộc cùng một loài.
- **Length Penalty:** Áp dụng phạt điểm dựa trên sự chênh lệch độ dài chuỗi để loại bỏ các kết quả khớp nối ngẫu nhiên (false positives).

## 📊 Đánh giá & Kết quả (Rating/Performance)

So sánh hiệu năng giữa phương pháp Baseline và phương pháp Đề xuất:

| Tiêu chí | Baseline (SGD) | **My Solution (KNN + Bio)** |
| :--- | :--- | :--- |
| **Phương pháp** | Linear Classification | **Homology Transfer** |
| **Dữ liệu Train** | 20% (Downsampled) | **100% (Full Data)** |
| **Rating nhận được** | 0.127 | **0.212** 🚀 |
| **Tốc độ** | Nhanh | Trung bình (tốn thời gian Inference) |
