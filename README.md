# Báo Cáo Phân Tích & Trực Quan Hóa Dữ Liệu Titanic (EDA Report)

Báo cáo này tóm tắt quá trình xử lý, phân tích khám phá dữ liệu (EDA) và trực quan hóa dữ liệu hành khách chuyến tàu Titanic dựa trên đoạn mã nguồn Python (Jupyter Notebook / Google Colab).

---

## 📑 Mục Lục
1. [Giới Thiệu](#1-giới-thiệu)
2. [Cấu Trúc Notebook](#2-cấu-trúc-notebook)
3. [Quy Trình Xử Lý & Phân Tích](#3-quy-trình-xử-lý--phân-tích)
4. [Kết Quả & Thống Kê Chính](#4-kết-quả--thống-kê-chính)
5. [Trực Quan Hóa Dữ Liệu](#5-trực-quan-hóa-dữ-liệu)
6. [Hướng Dẫn Chạy Mã](#6-hướng-dẫn-chạy-mã)

---

## 1. Giới Thiệu
* **Mục tiêu:** Phân tích các yếu tố ảnh hưởng đến tỷ lệ sống sót của hành khách trên chuyến tàu Titanic (Độ tuổi, Giới tính, Hạng vé, Giá vé,...).
* **Thư viện sử dụng:**
  * `kagglehub`: Tải xuống tập dữ liệu từ Kaggle.
  * `pandas`, `numpy`: Đọc, làm sạch, biến đổi và tính toán thống kê dữ liệu.
  * `matplotlib`, `seaborn`: Trực quan hóa dữ liệu dưới dạng đồ thị.

---

## 2. Cấu Trúc Notebook
Notebook bao gồm 2 ô mã nguồn chính (Code Cells):
1. **Cell 1:** Sử dụng `kagglehub` để tải các tập dữ liệu từ Kaggle (bao gồm Titanic, Insurance, Netflix, World Happiness, US Wildfires). Tập dữ liệu Titanic được sử dụng cho phần phân tích.
2. **Cell 2:** Thực hiện toàn bộ quy trình EDA: Đọc tập dữ liệu `train.csv` của Titanic, kiểm tra giá trị thiếu, xử lý dữ liệu khuyết, tính toán thống kê và vẽ 4 biểu đồ phân tích.

---

## 3. Quy Trình Xử Lý & Phân Tích

### 3.1. Kiểm Tra Ban Đầu
* **Kích thước dữ liệu:** 891 dòng (hành khách) và 12 cột (thuộc tính).
* **Giá trị khuyết (Missing Values) ban đầu:**
  * `Age`: 177 giá trị thiếu.
  * `Cabin`: 687 giá trị thiếu.
  * `Embarked`: 2 giá trị thiếu.

### 3.2. Làm Sạch Dữ Liệu (Data Cleaning)
* **Xử lý `Age`:** Điền các giá trị còn thiếu bằng giá trị trung vị (**Median** = 28.0).
* **Xử lý `Embarked`:** Điền các giá trị còn thiếu bằng giá trị xuất hiện nhiều nhất (**Mode** = 'S').
* **Xử lý `Cabin`:** Loại bỏ cột (`drop`) do số lượng giá trị khuyết quá lớn (>77%).

---

## 4. Kết Quả & Thống Kê Chính

### 4.1. Tỷ Lệ Sống Sót (`Survived`)
* **Tỷ lệ sống sót trung bình theo Giới tính (`Sex`):**
  * **Nữ (Female):** **74%**
  * **Nam (Male):** **19%**
* **Tỷ lệ sống sót trung bình theo Hạng vé (`Pclass`):**
  * **Hạng 1 (`Pclass 1`):** **63%**
  * **Hạng 2 (`Pclass 2`):** **47%**
  * **Hạng 3 (`Pclass 3`):** **24%**
* **Tỷ lệ sống sót kết hợp theo Hạng vé & Giới tính:**
  * Hạng 1 - Nữ: **97%** | Nam: **37%**
  * Hạng 2 - Nữ: **92%** | Nam: **16%**
  * Hạng 3 - Nữ: **50%** | Nam: **14%**

### 4.2. Thống Kê Chỉ Số Định Lượng (Sử dụng NumPy)
* **Độ tuổi (`Age`) sau khi xử lý:**
  * Trung bình (Mean): **29.36**
  * Trung vị (Median): **28.00**
  * Độ lệch chuẩn (Std): **13.01**
* **Giá vé (`Fare`):**
  * Trung bình (Mean): **32.20**
  * Trung vị (Median): **14.45**
  * Độ lệch chuẩn (Std): **49.67** (Cho thấy sự chênh lệch giá vé rất lớn giữa các hạng phòng)

---

## 5. Trực Quan Hóa Dữ Liệu
Notebook khởi tạo ma trận đồ thị $2 \times 2$ (4 biểu đồ):

1. **Top-Left (Barplot):** *Tỷ lệ sống sót theo Hạng vé & Giới tính*
   * Trực quan hóa tỷ lệ sống sót vượt trội của nữ giới ở tất cả các hạng vé, đặc biệt là Hạng 1 và Hạng 2.
2. **Top-Right (Histplot & KDE):** *Phân bố Độ tuổi*
   * Biểu diễn phân bố độ tuổi của hành khách với 30 khoảng (bins), cho thấy phần lớn hành khách nằm trong độ tuổi từ 20 - 35.
3. **Bottom-Left (Boxplot - Thang Logarithm):** *Phân bố Giá vé theo Hạng vé*
   * Sử dụng `yscale('log')` để xử lý các giá trị ngoại lệ (outliers) cực lớn. Hạng 1 có khoảng giá vé rộng nhất và cao nhất.
4. **Bottom-Right (Boxplot):** *Độ tuổi theo Trạng thái Sống sót*
   * So sánh phân bố tuổi giữa nhóm Không sống sót (0) và Sống sót (1).

---

## 6. Hướng Dẫn Chạy Mã
1. Cài đặt các thư viện phụ thuộc:
   ```bash
   pip install pandas numpy matplotlib seaborn kagglehub
   ```
2. Mở file Notebook trên Google Colab hoặc Jupyter Notebook/VS Code.
3. Thay đổi đường dẫn `path` trong cell 2 phù hợp với thư mục lưu trữ tập dữ liệu `train.csv` của bạn.
4. Chạy toàn bộ các cells để xem kết quả thống kê và hiển thị đồ thị.