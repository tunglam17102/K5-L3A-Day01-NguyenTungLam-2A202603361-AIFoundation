# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:2A202603361**
- **Họ và tên:Nguyễn Tùng Lâm**
- **SEED: 238** (in ở ô đầu notebook):

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

*Chép bảng so sánh cuối Phần 5 (F1 test, F1 SUB 40, p95 ms/tin, USD/1k tin) của chính bạn.*
                                 precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            1.000   0.759      0.863        0.824   
2. BoW + MLP (deep learning)         0.987   0.949      0.968        0.923   
3a. Encoder (MiniLM) + kNN           0.865   0.975      0.917        0.976   
3b. Encoder (MiniLM) + LogReg        0.950   0.962      0.956        1.000   
3c. Encoder (MiniLM) + MLP head      0.926   0.949      0.938        0.950   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            6.558       9356.618       0.056   
2. BoW + MLP (deep learning)        13.742      19898.127       0.330   
3a. Encoder (MiniLM) + kNN          80.059         44.279      40.501   
3b. Encoder (MiniLM) + LogReg       80.505         42.915      96.925   
3c. Encoder (MiniLM) + MLP head     81.911         23.038      21.567   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.091           0.0  
2. BoW + MLP (deep learning)          0.448           0.0  
3a. Encoder (MiniLM) + kNN           56.053           0.0  
3b. Encoder (MiniLM) + LogReg       175.776           0.0  
3c. Encoder (MiniLM) + MLP head      31.650           0.0  

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*
dl_relu	Bỏ ReLU thì giống logistic regression, F1 giảm hoặc không đổi	F1 = 0.954, cao hơn hẳn logistic regression Phần 1 (0.863)	Về toán vẫn là mô hình tuyến tính, nhưng cách train khác (Adam, mini-batch, 30 epoch so với gradient descent toàn bộ, 300 epoch)
ml_lr	lr = 50 làm loss dao động zigzag	Loss hội tụ rất nhanh, không dao động	Nghĩ xem vì sao bước nhảy lớn vẫn không phân kỳ (gợi ý: đầu vào chỉ 0/1 và rất thưa)
dl_curve	Val loss giảm rồi chững lại	Val loss thấp nhất ở epoch 6, sau đó tăng (overfit)	Train loss vẫn giảm nhưng mô hình khớp quá mức dữ liệu train nên mất khả năng tổng quát

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*
Model tụt nhiều nhất là BoW + MLP ở nhóm case spam giọng tự nhiên và né từ khóa,
## 5. Thử thách cá nhân

Chưa làm kịp

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*
Encoder (MiniLM) + LogReg vì có tỷ lệ lỗi thấp nhất (gần 0%) và p95 vẫn dưới 50 ms chấp nhận đánh đổi là chi phí vận hành khá cao vào khoảng 3000$

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
dùng AI để code cũng như đọc hiểu code, đọc hiểu câu hỏi cũng như gợi ý dự đoán, AI giúp mình hiểu ra những phần code mà mình đọc không hiểu hay những cú pháp mà mình chưa biết
