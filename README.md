# Phân tích dữ liệu các bài hát trên Spotify

## Tổng quan dự án

Dự án này thực hiện phân tích sâu về các đặc trưng âm thanh của 114,000 bài hát trên nền tảng Spotify nhằm khám phá những yếu tố tạo nên một bài hát "Hit" và hiểu rõ hơn về mối quan hệ giữa các đặc tính kỹ thuật âm nhạc với sự phổ biến của bài hát.

### Thông tin nhóm

**Tên nhóm:** Nhóm 10

**Thành viên:**

- Nguyễn Văn An - 23127317
- Vũ Hoàng Minh - 23127427
- Vương Khải Phong - 23127453

**Môn học:** Programming for Data Science

**Trường:** Trường Đại học Khoa học Tự nhiên - ĐHQG TP.HCM

---

## Nguồn dữ liệu

### Thông tin dataset

- **Nguồn:** Hugging Face
- **Tác giả:** Maharshi Pandya
- **URL:** [Spotify tracks - Hugging Face](https://huggingface.co/datasets/maharshipandya/spotify-tracks-dataset)
- **Giấy phép:** BSD License (cho phép sử dụng cho mục đích giáo dục và nghiên cứu)
- **Kích thước:** 114,000+ bài hát
- **Số cột:** 21 cột
- **Thể loại:** 125 thể loại nhạc khác nhau

### Mô tả dataset

Bộ dữ liệu chứa thông tin chi tiết về các bài hát trên nền tảng Spotify, được thu thập thông qua **Spotify Web API**. Dữ liệu bao gồm:

#### Đặc trưng âm thanh:

- `danceability`: Độ thích hợp để nhảy (0.0 - 1.0)
- `energy`: Mức năng lượng/cường độ của bài hát (0.0 - 1.0)
- `loudness`: Độ to trung bình (dB)
- `speechiness`: Mức độ chứa từ ngữ
- `acousticness`: Độ mộc của bài hát
- `instrumentalness`: Dự đoán bài hát không có lời
- `liveness`: Xác suất bài hát được thu âm trực tiếp
- `valence`: Cảm xúc tích cực của bài hát (0.0 - 1.0)
- `tempo`: Nhịp độ (BPM)
- `duration_ms`: Độ dài bài hát (mili-giây)

#### Đặc trưng nhạc lý:

- `key`: Tông nhạc (0-11)
- `mode`: Điệu thức (1 = Major/Trưởng, 0 = Minor/Thứ)
- `time_signature`: Nhịp/Chỉ số thời gian

#### Metadata:

- `track_id`: ID duy nhất của bài hát
- `track_name`: Tên bài hát
- `artists`: Tên nghệ sĩ biểu diễn
- `album_name`: Tên album
- `track_genre`: Thể loại nhạc
- `popularity`: Điểm phổ biến (0-100)
- `explicit`: Đánh dấu bài hát có nội dung nhạy cảm

---

## Câu hỏi nghiên cứu

### Câu hỏi 1: Công thức của một bài hát "Hit" là gì?

- Những đặc trưng âm thanh nào có mối tương quan mạnh nhất với độ phổ biến?
- Cấu trúc nhạc lý và thể loại nội dung có ảnh hưởng đến độ phổ biến không?
- Có sự khác biệt rõ rệt về đặc tính âm thanh giữa nhóm bài hát Hit và Non-Hit?

### Câu hỏi 2: Có thể dự đoán độ phổ biến của bài hát bằng Machine Learning không?

- Liệu chúng ta có thể xây dựng mô hình Machine Learning để dự đoán chính xác độ phổ biến của một bài hát?
- Các đặc trưng âm thanh, thể loại và nghệ sĩ đóng góp bao nhiêu phần trăm vào độ phổ biến?
- Mô hình nào cho kết quả tốt nhất: Linear Regression, Random Forest hay XGBoost?

### Câu hỏi 3: Giọng Trưởng (Major) vs Giọng Thứ (Minor)

- Giọng Trưởng có thực sự mang lại cảm giác tích cực hơn giọng Thứ?
- Giọng Trưởng có nhiều năng lượng hơn giọng Thứ như lý thuyết âm nhạc thường mặc định?

### Câu hỏi 4: Nhạc Explicit vs Non-Explicit

- Nhạc có nội dung nhạy cảm (explicit) có đặc điểm âm thanh khác biệt gì?
- Nhạc explicit có khả năng tương tác (danceability) khác so với non-explicit?
- Nhạc explicit có thực sự ồn ào và khó nhảy hơn như định kiến?

### Câu hỏi 5: Nghịch lý Danceability

- Tại sao bài hát ở Mode Thứ (Minor) lại có Danceability cao hơn Mode Trưởng (Major)?
- Liệu sự khác biệt này có liên quan đến Tempo hay Energy?

### Câu hỏi 6: Ngoại lệ trong mối quan hệ Energy-Loudness

- Mối quan hệ giữa Energy và Loudness (r ≈ 0.76) có ổn định không?
- Những bài hát nào nằm ngoài khoảng tin cậy 95%?
- Đặc điểm chung của nhóm bài hát có Energy cực cao nhưng Loudness cực thấp là gì?

---

## Các phát hiện chính

### 1. Công thức tạo bài Hit

- **Yếu tố tích cực:** Loudness, Danceability, và Energy có tương quan dương với độ phổ biến
- **Yếu tố tiêu cực:** Instrumentalness (nhạc thuần không lời) có tương quan âm mạnh nhất
- Các thể loại đại chúng (Pop, Chill, Sad) giúp tăng tỷ lệ trở thành hit

### 2. Khả năng dự đoán bằng Machine Learning

- **Mô hình tốt nhất:** XGBoost và Random Forest đạt R² ≈ 0.63
- **Ý nghĩa:** Chỉ giải thích được ~63% sự biến thiên về độ phổ biến
- **Giới hạn:** ~37% còn lại phụ thuộc vào yếu tố ngoại sinh (Marketing, viral trends, thời điểm phát hành)
- **Yếu tố quan trọng nhất:** Nghệ sĩ ảnh hưởng lớn nhất đến độ phổ biến của bài hát

### 3. Major vs Minor

- **Về Valence:** Giọng Trưởng (Major) mang cảm giác tích cực hơn giọng Thứ (Minor), nhưng chênh lệch rất nhỏ
- **Về Energy:** Ngược với lý thuyết truyền thống, nhạc giọng Thứ có năng lượng trung bình cao hơn giọng Trưởng
- Phản ánh sự trỗi dậy của các dòng nhạc điện tử (EDM, Techno) sử dụng giọng Thứ

### 4. Explicit vs Non-Explicit

- **Định hình phong cách:** Nhạc explicit có cấu trúc âm thanh đặc trưng: ồn ào hơn và nhiều lời hơn
- **Khả năng tương tác:** Nhạc explicit có danceability cao hơn đáng kể, rất phù hợp cho hoạt động vận động
- **Bác bỏ định kiến:** Nhạc explicit không hề "khó nhảy" như suy nghĩ ban đầu

### 5. Nghịch lý Danceability

- Mode Thứ (Minor) có Danceability cao hơn Mode Trưởng (Major)
- Nguyên nhân: Nhạc Minor có Energy trung bình cao hơn
- Xu hướng hiện đại: Sử dụng điệu Thứ để tạo "Dark Dance" music với năng lượng bùng nổ
- **Định hình phong cách:** Nhạc explicit có cấu trúc âm thanh đặc trưng: ồn ào hơn và nhiều lời hơn
- **Khả năng tương tác:** Nhạc explicit có danceability cao hơn đáng kể, rất phù hợp cho hoạt động vận động

### 6. Giới hạn của mô hình dự đoán

- Mô hình tốt nhất (XGBoost/Random Forest) chỉ giải thích được ~63% (R² ≈ 0.63) sự biến thiên về độ phổ biến
- ~40% còn lại phụ thuộc vào các yếu tố ngoại sinh: Marketing, xu hướng mạng xã hội, thời điểm phát hành

---

## Cấu trúc thư mục

```
Spotify_final_project/
│
├── data/
│   ├── spotify_dataset.csv             # Dữ liệu gốc từ Hugging Face
│
├── notebooks/
│   ├── 01_data_exploration.ipynb       # Khám phá và làm sạch dữ liệu
│   ├── 02_data_analysis.ipynb          # Phân tích câu hỏi 1 & 2
│   ├── 03_data_analysis.ipynb          # Phân tích câu hỏi 3 & 4
│   ├── 04_data_analysis.ipynb          # Phân tích câu hỏi 4 & 6
│   └── 05_project_summary.ipynb        # Tóm tắt dự án và cảm nhận
│
├── README.md
├── requirements.txt                    # Các thư viện Python cần thiết
└── GIT_WORKFLOW.md                     # Hướng dẫn quy trình Git
```

### Mô tả các notebook

#### 01_data_exploration.ipynb

**Nội dung:**

- Thu thập và giới thiệu dataset
- Kiểm tra cấu trúc dữ liệu (114,000 dòng, 21 cột)
- Phân tích dữ liệu thiếu và trùng lặp
- Khám phá phân phối các biến số (histogram, boxplot)
- Phân tích tương quan giữa các biến
- Làm sạch và chuẩn bị dữ liệu

**Kỹ thuật chính:** EDA (Exploratory Data Analysis), Visualization

---

#### 02_data_analysis.ipynb

**Nội dung:**

**Câu hỏi 1: Công thức của một bài hát "Hit" là gì?**

- Tính toán hệ số tương quan Pearson và Spearman
- Phân loại Hit (popularity > 75) vs Non-Hit (popularity < 25)
- Phân tích đặc trưng âm thanh, nhạc lý, và metadata
- Sử dụng Radar Chart để so sánh hồ sơ âm thanh

**Câu hỏi 2: Dự đoán độ phổ biến bằng Machine Learning**

- Xây dựng và so sánh 3 mô hình: Linear Regression, Random Forest, XGBoost
- Feature Engineering với đặc trưng âm thanh, thể loại và nghệ sĩ
- Đánh giá mô hình (R², MSE, Cross-validation)
- Phân tích Feature Importance

**Kỹ thuật chính:** Correlation Analysis, Machine Learning, Regression, Feature Engineering

---

#### 03_data_analysis.ipynb

**Nội dung:**

**Câu hỏi 3: Giọng Trưởng (Major) vs Giọng Thứ (Minor)**

- Phân nhóm dữ liệu theo Mode (Major/Minor)
- Kiểm định T-test cho Valence và Energy
- Trực quan hóa bằng Boxplot và KDE plot
- Phân tích ý nghĩa thống kê (P-value)

**Câu hỏi 4: Nhạc Explicit vs Non-Explicit**

- Phân tích đặc điểm âm thanh khác biệt (Loudness, Speechiness, Danceability)
- Kiểm định T-test cho các đặc trưng
- Trực quan hóa bằng Boxplot và KDE plot
- Phân tích ý nghĩa thống kê (P-value)

**Kỹ thuật chính:** Statistical Testing (T-test), Group Comparison, Hypothesis Testing

---

#### 04_data_analysis.ipynb

**Nội dung:**

**Câu hỏi 5: Giải thích nghịch lý Danceability**

- Phân tích tại sao Minor có Danceability cao hơn Major
- Khám phá vai trò của Energy và Tempo
- Correlation Heatmap và Faceted Scatter Plot
- So sánh phân phối theo Mode

**Câu hỏi 6: Phân tích ngoại lệ Energy-Loudness**

- Hồi quy OLS để xây dựng mô hình baseline
- Xác định Prediction Interval (95% confidence)
- Phát hiện và phân tích nhóm "Nghịch lý âm thanh"
- Truy vết đặc điểm của Functional Audio (Nature Sounds)

**Kỹ thuật chính:** Regression Analysis (OLS), Outlier Detection, Correlation Analysis

---

#### 05_project_summary.ipynb

**Nội dung:**

- Tổng hợp các phát hiện chính từ 4 notebook trước
- Liệt kê giới hạn của nghiên cứu
- Đề xuất hướng phát triển tương lai
- Cảm nhận cá nhân của từng thành viên về quá trình học tập

---

## Hướng dẫn chạy project

### Bước 1: Cài đặt môi trường

**Yêu cầu hệ thống:**

- Python 3.8 trở lên
- Jupyter Notebook hoặc JupyterLab

### Bước 2: Clone repository

```bash
git clone https://github.com/KhaiPhong25/Spotify_final_project.git
cd Spotify_final_project
```

### Bước 3: Cài đặt các thư viện

**Cài đặt bằng requirements.txt:**

```bash
pip install -r requirements.txt
```

**Hoặc cài đặt thủ công:**

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost scipy statsmodels
pip install jupyter notebook
```

### Bước 4: Tải dataset

- Tải từ [Hugging Face](https://huggingface.co/datasets/maharshipandya/spotify-tracks-dataset)
- Đặt file `spotify_dataset.csv` vào thư mục `data`

### Bước 5: Chạy các notebook

Khởi động Jupyter:

```bash
jupyter notebook
```

**Thứ tự chạy được khuyến nghị:**

1. `01_data_exploration.ipynb` - Tìm hiểu dữ liệu
2. `02_data_analysis.ipynb` - Phân tích câu hỏi 1 & 2
3. `03_data_analysis.ipynb` - Phân tích câu hỏi 3 & 4
4. `04_data_analysis.ipynb` - Phân tích câu hỏi 5 & 6
5. `05_project_summary.ipynb` - Tổng kết

**Lưu ý:** Mỗi notebook có thể chạy độc lập, không phụ thuộc vào notebook khác.

---

## Thư viện phụ thuộc

### Core Libraries

```
pandas>=1.5.0           # Xử lý và phân tích dữ liệu
numpy>=1.23.0           # Tính toán số học
```

### Visualization

```
matplotlib>=3.6.0       # Vẽ biểu đồ cơ bản
seaborn>=0.12.0         # Biểu đồ thống kê nâng cao
```

### Machine Learning

```
scikit-learn>=1.2.0     # Mô hình ML, preprocessing, metrics
xgboost>=1.7.0          # Gradient Boosting model
```

### Statistical Analysis

```
scipy>=1.10.0           # Kiểm định thống kê (T-test, etc.)
statsmodels>=0.14.0     # OLS Regression, statistical models
```

### Development Tools

```
jupyter>=1.0.0          # Jupyter Notebook
notebook>=6.5.0         # Notebook server
```

---
