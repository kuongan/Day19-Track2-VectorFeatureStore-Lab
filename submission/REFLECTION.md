# Reflection — Lab 19

**Tên:** Nguyễn Trần Khương An
**Cohort:** A20-K1
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Theo NB2, hybrid thắng trung bình trên toàn bộ golden set với Precision@10 = 78.6%, nhỉnh hơn BM25 (77.8%) và vector (73.2%). Tuy nhiên, nếu tách theo loại query thì kết quả khác nhau: `exact` là vùng BM25 và hybrid gần như ngang nhau ở 96.7%, nên lexical signal đã đủ mạnh; `paraphrase` lại do BM25 thắng nhẹ (33.3% so với 32.0% của hybrid và 24.0% của vector), cho thấy `BAAI/bge-small-en-v1.5` chưa đủ tốt cho paraphrase tiếng Việt; còn `mixed` là nơi hybrid thắng rõ nhất với 100.0%, cao hơn BM25 (97.0%) và vector (98.5%).

Tôi không dùng hybrid khi query gần như chắc chắn là exact keyword search và mục tiêu là đường đi đơn giản, ổn định nhất. Pure BM25 phù hợp khi user gõ đúng thuật ngữ trong corpus; pure vector chỉ đáng ưu tiên khi embedding model tốt hơn cho ngôn ngữ/corpus và truy vấn thiên về diễn đạt lại ý hơn là keyword.

---

## Điều ngạc nhiên nhất khi làm lab này

Điều ngạc nhiên nhất là các phần “boilerplate” AI viết rất nhanh, nhưng các quyết định nhỏ như chọn embedding model, công thức RRF, metric latency, hay TTL trong Feast lại là chỗ quyết định chất lượng. Chỉ cần sai một chi tiết như rank bắt đầu từ 0 hoặc đo nhầm wall-clock thay vì server-side latency là kết quả đã lệch hẳn.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [x] Pair work với: Phạm Minh Việt - 2A202600265
