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
  
  **Gradient Boosting**
  
  **XGBoost**
  
  Mỗi mô hình được huấn luyện với 3 cách xử lý imbalance:
  
  **Original**
  
  **Class Weight/  Sample Weight**
  
  **SMOTE**
  
  Sau đó tiến hành so sánh performance trên tập validation/test.
  
  **3.5 Model Selection & Threshold Tuning**

   Trong các mô hình được thử nghiệm, XGBoost với scale_pos_weight cho kết quả tốt nhất khi đạt recall cao nhất (0.73) và F1-score cao nhất (0.54), cho thấy khả năng phát hiện khách hàng rời bỏ hiệu quả nhất. Mặc dù accuracy không cao nhất, nhưng trong bài toán churn, việc tối ưu recall quan trọng hơn. Gradient Boosting kết hợp với SMOTE cũng cho kết quả tốt với recall 0.71 và được chọn làm mô hình dự phòng.
   
   Ngưỡng phân loại được điều chỉnh từ 0.5 xuống 0.4 để tăng khả năng phát hiện churn.
   
**4. Kết quả**

Mô hình cho kết quả ổn định giữa validation và test, cho thấy khả năng tổng quát hóa tốt. Ngưỡng dự đoán được tối ưu trên tập validation, sau đó áp dụng lên tập test và đạt recall cao (~81%) cho nhóm churn, phù hợp mục tiêu phát hiện khách hàng rời bỏ, dù phải đánh đổi precision.

Các metric được sử dụng để đánh giá:

**Precision**

**Recall**

**F1-score**

**Confusion Matrix**

**ROC-AUC**

**5. Phân tích các đặc trưng quan trọng**

Sau khi trích xuất các đặc trưng ảnh hưởng thì kết quả cho thấy **NumOfProducts** và **Age** là hai yếu tố ảnh hưởng mạnh nhất đến khả năng churn. Khách hàng sử dụng ít sản phẩm ngân hàng và khách hàng lớn tuổi có xu hướng rời bỏ dịch vụ cao hơn. Ngoài ra, yếu tố khu vực cũng đóng vai trò đáng kể khi khách hàng tại **Germany** có xác suất churn cao hơn so với các khu vực khác.

**6. Business Recommentation**

Dựa trên kết quả mô hình, các nhóm khách hàng có nguy cơ churn cao bao gồm khách lớn tuổi, có số dư cao và đặc biệt là nhóm khách chỉ sử dụng 1 sản phẩm. Đây là nhóm chiếm tỷ trọng lớn và có tỷ lệ churn tương đối cao, do đó cần được ưu tiên trong chiến lược giữ chân.

Doanh nghiệp có thể áp dụng các chiến lược như cross-sell để khuyến khích khách hàng sử dụng thêm sản phẩm, kết hợp với các chương trình ưu đãi và cá nhân hóa trải nghiệm nhằm tăng mức độ gắn kết.

Ngoài ra, nhóm khách hàng sử dụng 3–4 sản phẩm có tỷ lệ churn rất cao nhưng số lượng nhỏ, nên cần được theo dõi như một nhóm rủi ro cao. Nếu xu hướng này được xác nhận, có thể do nhóm khách này có kỳ vọng cao và dễ rời bỏ khi không hài lòng.

**7. Deployment**

Mô hình có thể được triển khai để dự đoán xác suất churn hàng tháng. Những khách hàng có xác suất > 0.4 sẽ được đưa vào danh sách cảnh báo để đội marketing thực hiện các chiến dịch giữ chân.
