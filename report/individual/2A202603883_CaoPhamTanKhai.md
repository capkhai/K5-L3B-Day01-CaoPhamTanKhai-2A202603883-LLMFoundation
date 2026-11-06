# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV: 2A202603883**
- **Họ và tên: Cao Phạm Tân Khải**
- **SEED: 6524** (in ở ô đầu notebook):

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | x |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | x |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | x |

## 2. Kết quả chính

*Chép bảng so sánh cuối Phần 5 (F1 test, F1 SUB 40, p95 ms/tin, USD/1k tin) của chính bạn.*
                                 precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            1.000   0.812      0.896        0.824   
2. BoW + MLP (deep learning)         0.976   0.953      0.964        0.947   
3a. Encoder (MiniLM) + kNN           0.865   0.976      0.917        0.927   
3b. Encoder (MiniLM) + LogReg        0.923   0.988      0.955        0.974   
3c. Encoder (MiniLM) + MLP head      0.966   0.988      0.977        0.974   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            6.866      29259.245       0.048   
2. BoW + MLP (deep learning)         5.683      46696.162       0.170   
3a. Encoder (MiniLM) + kNN          85.408         23.822      55.697   
3b. Encoder (MiniLM) + LogReg       86.056         41.774      26.343   
3c. Encoder (MiniLM) + MLP head     86.435         43.992      27.950   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.103           0.0  
2. BoW + MLP (deep learning)          0.220           0.0  
3a. Encoder (MiniLM) + kNN           74.281           0.0  
3b. Encoder (MiniLM) + LogReg        41.215           0.0  
3c. Encoder (MiniLM) + MLP head      38.914           0.0  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*
predict("hard_eval", "1,2 thì trên 80%, 3a, 3b, 3c thì trên 90%, khó nhất với bow là nói về spam, khó nhất với llm là thao túng lừa đảo ") 
Không ngờ với các case khó số liệu lại lệch quá nhiều, toàn 5x-6x%

predict("tradeoff", "Bow + logreg, bow + MLP ")
bow + MLP nằm bên trái vạch SLA 50ms trong khi dự đoán nằm bên phải

predict("emb_tricky", "3b")
dự đoán mô hình 3b tốt hơn BOw nhưng thực sự với bộ dữ liệu nhỏ 2 model lại bằng nhau
## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*
Bow + logreg tụt nhiều nhất ở nhóm case thao túng lừa đảo và né từ khóa.
Cơ chế né từ khóa khiến Bow không nhận biết được các từ spam, nên lệch về ham
Thao túng lừa đảo sẽ dùng các từ ngữ ít trùng với bộ của Bow, vì đó model sẽ lệch về ham

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*
Không kịp làm vì 12h rồi

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*
Không kịp làm vì 12h rồi
## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
Không kịp làm vì 12h rồi
Nay có workshop trên discord nên 10h mới xong em không kịp làm T.T
