**DỰ ĐOÁN KHÁCH HÀNG RỜI BỎ**

**1. Giới thiệu**
   Trong lĩnh vực ngân hàng, việc khách hàng rời bỏ dịch vụ (customer churn) gây ảnh hưởng trực tiếp đến doanh thu và chi phí thu hút khách hàng mới. Vì vậy, khả năng dự đoán sớm khách hàng có nguy cơ churn giúp doanh nghiệp triển khai các chiến lược giữ chân hiệu quả.

  **Mục tiêu của project:**
  
  - Xây dựng mô hình dự đoán khả năng khách hàng rời bỏ dịch vụ.
  
  - Phân tích các yếu tố ảnh hưởng đến churn.
  
  - Đề xuất các insight giúp doanh nghiệp giảm tỷ lệ churn.

**2. Dataset**

Dataset gồm **10,000** khách hàng ngân hàng được công bố trên **Kaggle** với các thông tin nhân khẩu học và hành vi sử dụng dịch vụ.

Biến mục tiêu

**Exited:**

0 → Khách hàng tiếp tục sử dụng dịch vụ

1 → Khách hàng rời bỏ dịch vụ

**Một số biến quan trọng:**

**CreditScore** – Điểm tín dụng

**Geography** – Khu vực khách hàng

**Gender** – Giới tính

**Age** – Tuổi

**Tenure** – Thời gian gắn bó với ngân hàng

**Balance** – Số dư tài khoản

**NumOfProducts** – Số lượng sản phẩm ngân hàng sử dụng

**HasCrCard** – Có thẻ tín dụng hay không

**IsActiveMember** – Mức độ hoạt động của khách hàng

**EstimatedSalary** – Thu nhập ước tính

**3. Quy trình thực hiện
   3.1 Exploratory Data Analysis (EDA)**
   Phân tích dữ liệu ban đầu cho thấy:

  **IsActiveMember** có ảnh hưởng mạnh đến churn
  → khách hàng không active có tỷ lệ rời bỏ cao hơn rõ rệt.
  
  **Geography**
  → khách hàng tại Germany có tỷ lệ churn cao hơn các khu vực khác.
  
  **NumOfProducts**
  → nhóm khách có 3–4 sản phẩm có tỷ lệ churn rất cao, tuy nhiên số lượng mẫu nhỏ nên cần cẩn trọng khi kết luận.
  
  **Age**
  → khách hàng lớn tuổi có xu hướng churn cao hơn.
  
  Ngoài ra:

  Các biến **Gender, HasCrCard** có ảnh hưởng đến churn nhưng mức độ yếu hơn so với các biến trên.
  
  Các biến như **CreditScore, Tenure, Balance, EstimatedSalary** không cho thấy sự phân tách rõ ràng khi xét riêng lẻ, nhưng vẫn có thể đóng vai trò quan trọng khi kết hợp trong mô hình.

 **3.2 Phân tích Outlier**

  Biến Age có xuất hiện một số giá trị được xem là outlier theo thống kê. Tuy nhiên, các giá trị này vẫn hợp lý trong bối cảnh khách hàng ngân hàng, do đó không thực hiện xử lý outlier.

  **3.3 Xử lý mất cân bằng dữ liệu**

  Dữ liệu bị mất cân bằng, với số lượng khách hàng không churn lớn hơn nhiều so với churn.
  
  **Để xử lý vấn đề này, project thử nghiệm 3 cách:**
  
  - Original dataset (không xử lý imbalance)
  
  - Class Weight / Sample Weight
  
  - SMOTE (Synthetic Minority Oversampling Technique)

  **3.4 Xây dựng mô hình**

  Các mô hình được thử nghiệm:
  
  **Logistic Regression**
  
  **Random Forest**
  
  Gradient Boosting
  
  XGBoost
  
  Mỗi mô hình được huấn luyện với 3 cách xử lý imbalance:
  
  Original
  
  Class Weight
  
  SMOTE
  
  Sau đó tiến hành so sánh performance trên tập validation/test.
