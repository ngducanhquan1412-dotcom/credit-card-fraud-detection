# Phát hiện gian lận giao dịch thẻ tín dụng bằng học máy

Dự án bài tập lớn học phần Học máy, xây dựng quy trình phân loại giao dịch thẻ tín dụng thành hai lớp:

- `Class = 0`: giao dịch bình thường
- `Class = 1`: giao dịch gian lận

## Thành viên

- Lê Tùng Dương
- Nguyễn Văn Mạnh
- Nguyễn Đức Anh Quân

Giảng viên hướng dẫn: Phạm Tiến Lâm.

## Nội dung dự án

Mã nguồn thực hiện:

1. Đọc và kiểm tra dữ liệu CSV.
2. Chuyển đổi kiểu dữ liệu và xử lý giá trị thiếu bằng trung vị.
3. Chia dữ liệu phân tầng thành 60% train, 20% validation và 20% test.
4. Huấn luyện Logistic Regression và Random Forest.
5. Xử lý mất cân bằng bằng `class_weight`.
6. Chọn ngưỡng phân loại theo F1-score trên tập validation.
7. Chọn mô hình theo PR-AUC trên tập validation.
8. Đánh giá trên tập test bằng Accuracy, Precision, Recall, F1, ROC-AUC, PR-AUC và ma trận nhầm lẫn.
9. Lưu mô hình, kết quả dự đoán và biểu đồ.

## Dữ liệu

Tệp `data/creditcard.csv` là dữ liệu tổng hợp gồm:

- 5.000 giao dịch
- 4.900 giao dịch bình thường
- 100 giao dịch gian lận
- 30 đặc trưng đầu vào: `Time`, `V1` đến `V28`, `Amount`
- 1 nhãn đầu ra: `Class`

Các cột `V1` đến `V28` là đặc trưng tổng hợp và không phải kết quả PCA từ dữ liệu ngân hàng thật.

## Cài đặt

```bash
pip install -r requirements.txt
```

## Chạy trên Google Colab

Upload mã nguồn và dữ liệu, sau đó chạy:

```python
%run src/credit_card_fraud_detection.py --mode train --data data/creditcard.csv
```

Trong trường hợp chạy file riêng trên Colab và chưa có dữ liệu, chương trình có thể tự mở hộp upload.

## Chạy trên máy tính

```bash
python src/credit_card_fraud_detection.py   --mode train   --data data/creditcard.csv   --output results
```

## Dự đoán dữ liệu mới

```bash
python src/credit_card_fraud_detection.py   --mode predict   --model results/best_model.joblib   --predict-data new_transactions.csv   --prediction-output predictions.csv
```

## Kết quả thực nghiệm hiện tại

Trên tập test tổng hợp gồm 1.000 giao dịch:

- True Negative: 980
- False Positive: 0
- False Negative: 0
- True Positive: 20
- Accuracy: 1,0000
- Precision: 1,0000
- Recall: 1,0000
- F1-score: 1,0000
- ROC-AUC: 1,0000
- PR-AUC: 1,0000

Kết quả 100% chỉ phản ánh tập dữ liệu tổng hợp có tín hiệu phân lớp rõ ràng. Kết quả này không phải cam kết hiệu năng trên dữ liệu ngân hàng thực tế.

## Cấu trúc thư mục

```text
credit-card-fraud-detection/
├── src/
│   └── credit_card_fraud_detection.py
├── data/
│   └── creditcard.csv
├── report/
│   └── bao_cao_hoc_may.docx
├── results/
│   ├── metrics.json
│   ├── test_predictions.csv
│   ├── feature_importance.csv
│   ├── best_model.joblib
│   └── các biểu đồ PNG
├── requirements.txt
├── .gitignore
└── README.md
```

## Tái lập kết quả

Dự án sử dụng `random_state = 42` trong quá trình sinh dữ liệu, chia tập và huấn luyện. Để tái lập kết quả, cần giữ nguyên tệp dữ liệu, phiên bản thư viện tương thích và các siêu tham số trong mã nguồn.

## Việc cần bổ sung

- Stratified 5-Fold Cross-Validation.
- Slides thuyết trình.
- Kế hoạch và bảng phân công thành viên.
