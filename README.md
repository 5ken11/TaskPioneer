# 📊 BÁO CÁO PHÂN TÍCH KHÁM PHÁ DỮ LIỆU (EDA REPORT)

**Tập dữ liệu:** Titanic Survival & Medical Cost Personal (Insurance)  
**Công cụ thực hiện:** Python 3 (`pandas`, `numpy`, `matplotlib`, `seaborn`)  
**Mục tiêu:** Thực hiện phân tích, làm sạch dữ liệu, tính toán thống kê mô tả, trực quan hóa và tổng kết kết quả cho toàn bộ 5 bài toán/yêu cầu.

---

## 📋 MỤC LỤC

1. [Bài 1: Làm sạch và Tiền xử lý Dữ liệu Titanic](#bài-1-làm-sạch-và-tiền-xử-lý-dữ-liệu-titanic)
2. [Bài 2: Phân tích Tỷ lệ Sống sót trên tàu Titanic](#bài-2-phân-tích-tỷ-lệ-sống-sót-trên-tàu-titanic)
3. [Bài 3: Thống kê Mô tả & Trực quan hóa Dữ liệu Titanic](#bài-3-thống-kê-mô-tả--trực-quan-hóa-dữ-liệu-titanic)
4. [Bài 4: Phân tích và Khám phá Dữ liệu Bảo hiểm Y tế (Insurance)](#bài-4-phân-tích-và-khám-phá-dữ-liệu-bảo-hiểm-y-tế-insurance)
5. [Bài 5: Phân tích Nâng cao & Phát hiện Ngoại lệ (Insurance)](#bài-5-phân-tích-nâng-cao--phát-hiện-ngoại-lệ-insurance)
6. [Tổng kết Chi tiết 5 Bài toán](#tổng-kết-chi-tiết-5-bài-toán)

---

## 🛳️ BÀI 1: LÀM SẠCH VÀ TIỀN XỬ LÝ DỮ LIỆU TITANIC

### 1.1 Kiểm tra Dữ liệu Ban đầu
* **Tổng số hàng:** `891` | **Tổng số cột:** `12`
* **Kiểm tra giá trị thiếu (Missing values):**
  * `Age`: Khuyết **177** giá trị (~19.87%).
  * `Cabin`: Khuyết **687** giá trị (~77.10%).
  * `Embarked`: Khuyết **2** giá trị (~0.22%).

### 1.2 Phương pháp Xử lý
* **Điền khuyết cho `Age`:** Điền bằng **Median (Trung vị)** = `28.0` tuổi (nhằm tránh ảnh hưởng bởi độ lệch dữ liệu).
* **Điền khuyết cho `Embarked`:** Điền bằng **Mode (Yếu vị)** = `'S'` (cảng Southampton có số lượng hành khách đông nhất).
* **Xử lý cột `Cabin`:** Loại bỏ hoàn toàn (Drop) do tỷ lệ khuyết quá lớn (> 70%), không đủ căn cứ khôi phục.

---

## ⚓ BÀI 2: PHÂN TÍCH TỶ LỆ SỐNG SÓT TRÊN TÀU TITANIC

### 2.1 Tỷ lệ Sống sót Chung
* Tỷ lệ hành khách sống sót toàn bộ: **38.38%** (342 / 891 người).

### 2.2 Tỷ lệ Sống sót theo Giới tính (`Sex`)
* **Nữ (`female`):** **74.20%**
* **Nam (`male`):** **18.89%**
* *Nhận xét:* Tỷ lệ sống sót của nữ giới cao gấp gần 4 lần nam giới.

### 2.3 Tỷ lệ Sống sót theo Hạng vé (`Pclass`)
* **Hạng 1 (`Pclass 1`):** **62.96%**
* **Hạng 2 (`Pclass 2`):** **47.28%**
* **Hạng 3 (`Pclass 3`):** **24.24%**

### 2.4 Phân tích Tương tác Giới tính $\times$ Hạng vé

| Hạng vé | Tỷ lệ Sống sót (Nữ) | Tỷ lệ Sống sót (Nam) |
| :--- | :--- | :--- |
| **Hạng 1** | **96.81%** | 36.89% |
| **Hạng 2** | **92.11%** | 15.74% |
| **Hạng 3** | 50.00% | **13.54%** |

---

## 📈 BÀI 3: THỐNG KÊ MÔ TẢ & TRỰC QUAN HÓA DỮ LIỆU TITANIC

### 3.1 Chỉ số Thống kê Biến Định lượng
* **Độ tuổi (`Age` - Sau khi làm sạch):**
  * Trung bình ($\mu$): **29.36** tuổi
  * Trung vị ($M_e$): **28.00** tuổi
  * Độ lệch chuẩn ($\sigma$): **13.01** tuổi
* **Giá vé (`Fare`):**
  * Trung bình ($\mu$): **32.20** USD | Trung vị ($M_e$): **14.45** USD
  * Độ lệch chuẩn ($\sigma$): **49.67** USD
  * Giá trị biên: **0.00** USD đến **512.33** USD

### 3.2 Biểu đồ Trực quan
1. **Barplot:** Minh họa sự chênh lệch lớn về tỷ lệ sống sót theo `Pclass` và `Sex`.
2. **Histplot & KDE (`Age`):** Dữ liệu phân bố tập trung mạnh từ 20 đến 35 tuổi.
3. **Boxplot (Scale Log - `Fare`):** Giá vé Hạng 1 xuất hiện nhiều điểm ngoại lệ rất cao (> 500 USD).

---

## 🏥 BÀI 4: PHÂN TÍCH VÀ KHÁM PHÁ DỮ LIỆU BẢO HIỂM Y TẾ (INSURANCE)

### 4.1 Kiểm tra Dữ liệu
* **Số lượng bản ghi:** `1,338` hàng, `7` thuộc tính (`age`, `sex`, `bmi`, `children`, `smoker`, `region`, `charges`).
* **Giá trị thiếu:** `0` (Dữ liệu hoàn toàn đầy đủ).
* **Bản ghi trùng lặp (Duplicates):** Phát hiện **1 dòng trùng lặp** tại hàng 195 và 581 (`age=19, sex=male, bmi=30.59, children=0, smoker=no, region=northwest, charges=1639.5631`).

### 4.2 Thống kê Chi phí Bảo hiểm (`charges`)
* **Các mức Tứ phân vị (Quantiles):**
  * **Q1 (25%):** **4,740.29** USD
  * **Q2 (50% - Median):** **9,382.03** USD
  * **Q3 (75%):** **16,639.91** USD
  * **Mean:** **13,270.42** USD (Lệch phải do chi phí cao ở một nhóm nhỏ).

### 4.3 Chi phí theo Giới tính & Khu vực
* **Theo Giới tính:** Nam (**13,956.75** USD) > Nữ (**12,569.58** USD).
* **Theo Khu vực (`region`):**
  * `southeast`: **14,735.41** USD (Cao nhất)
  * `northeast`: **13,406.38** USD
  * `northwest`: **12,417.58** USD
  * `southwest`: **12,346.94** USD (Thấp nhất)

---

## 🔍 BÀI 5: PHÂN TÍCH NÂNG CAO & PHÁT HIỆN NGOẠI LỆ (INSURANCE)

### 5.1 Tác động của Tình trạng Hút thuốc (`smoker`)
* Tỷ lệ hút thuốc chung: **20.48%** (Nam **23.52%** | Nữ **17.37%**).
* Khu vực `southeast` có tỷ lệ hút thuốc cao nhất (**25.00%**), giải thích cho việc chi phí bảo hiểm trung bình khu vực này cao nhất.

### 5.2 Phát hiện Ngoại lệ (Outliers Detection)
* **Phương pháp:** $Threshold = Q3 + 1.5 \times IQR$
* Các mức chi phí ngoại lệ: Từ **34,806.47 USD** đến **63,770.43 USD**.
* **Đặc điểm nhóm ngoại lệ:** 100% người thuộc nhóm chi phí cao bất thường là người **có hút thuốc (`smoker = yes`)** và phần lớn có chỉ số **BMI** $\ge$ **30**.

### 5.3 Ma trận Tương quan (Correlation Matrix)
* Yếu tố tác động mạnh nhất tới `charges`: **`smoker`** (Tương quan thuận rất cao).
* Yếu tố tác động trung bình: **`age`** và **`bmi`**.
* Yếu tố ít ảnh hưởng: **`children`**.

---

## 📌 TỔNG KẾT CHI TIẾT 5 BÀI TOÁN

| Bài toán | Nhiệm vụ chính | Kết quả / Chỉ số quan trọng nhất | Kết luận tổng quát |
| :--- | :--- | :--- | :--- |
| **Bài 1** | Làm sạch dữ liệu Titanic | Xử lý `Age` (177 missing - Median 28), drop `Cabin` (687 missing). | Dữ liệu hoàn toàn sạch, loại bỏ thông tin thiếu quá lớn. |
| **Bài 2** | Phân tích survival Titanic | Tỷ lệ sống: Nữ (74.2%) vs Nam (18.9%); Hạng 1 (63.0%) vs Hạng 3 (24.2%). | Giới tính và Hạng vé là 2 yếu tố phân loại chính quyết định cơ hội sống. |
| **Bài 3** | Thống kê & Trực quan Titanic | Độ tuổi TB: 29.36 tuổi; Giá vé TB: 32.20 USD (Max: 512.33 USD). | Biến Giá vé bị lệch phải mạnh và có độ biến động rất cao. |
| **Bài 4** | Khám phá dữ liệu Insurance | Xử lý 1 dòng lặp; Median Chi phí = 9,382.03 USD (Q1-Q3: 4.7k - 16.6k USD). | Chi phí bảo hiểm có sự phân hóa lớn, trung bình khu vực Southeast cao nhất. |
| **Bài 5** | Nâng cao & Ngoại lệ Insurance | Smoker làm tăng chi phí vượt trội; Ngoại lệ nằm ở mức 34.8k - 63.8k USD. | Hút thuốc kết hợp BMI cao là nguyên nhân cốt lõi tạo ra các mức phí kỷ lục. |