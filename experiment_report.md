# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600602
**Student Email:** 26ai.dangnn@vinuni.edu.vn
**Name:** Nguyễn Nhựt Đăng
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Trả về kết quả chính xác cho sản phẩm Laptop thuộc nhóm Electronics phù hợp nhất. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Trả về sản phẩm cực đoan không thực tế do bị ảnh hưởng bởi dữ liệu ngoại lai quá lớn. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent hoạt động dựa trên dữ liệu đầu vào theo nguyên tắc "rác vào thì rác ra" (Garbage In, Garbage Out). Khi sử dụng dữ liệu rác (`garbage_data.csv`), Agent đã trả về kết quả sai lệch nghiêm trọng là `Nuclear Reactor` với giá trị ngoại lai khổng lồ là $999999. Điều này xảy ra do các lỗi chất lượng dữ liệu cơ bản sau:
1. **Dữ liệu ngoại lai (Outliers):** Sản phẩm cực đoan như `Nuclear Reactor` với giá quá cao làm lệch hoàn toàn hàm tìm kiếm giá trị lớn nhất (`idxmax`).
2. **Trùng lặp ID (Duplicate IDs):** ID số 1 bị trùng lặp giữa Laptop và Banana, làm ảnh hưởng đến tính toàn vẹn và nhất quán của định danh dữ liệu.
3. **Sai kiểu dữ liệu (Wrong Data Types):** Giá của `Broken Chair` là chuỗi ký tự `'ten dollars'` thay vì số thực, điều này sẽ khiến các phép toán so sánh số học bị lỗi hoặc sập hệ thống khi xử lý.
4. **Giá trị Null (Null Values):** Bản ghi `Ghost Item` có các giá trị ID và Category trống (null), gây khó khăn cho việc lọc dữ liệu theo nhóm ngành.

Nếu không có pipeline ETL làm sạch dữ liệu trước, Agent AI sẽ dễ dàng bị đánh lừa bởi những thông tin nhiễu này.

---

## 3. Ket luan

**Quality Data > Quality Prompt?**
Tôi hoàn toàn đồng ý với nhận định này. Cho dù bạn viết câu lệnh prompt tối ưu và hoàn hảo thế nào, nếu cơ sở dữ liệu nền tảng bị nhiễm bẩn, chứa các thông tin rác hoặc sai lệch loại dữ liệu, kết quả trả về của Agent AI vẫn sẽ không chính xác và thiếu độ tin cậy. Dữ liệu chất lượng cao là nền tảng cốt lõi quyết định tính chính xác của bất kỳ hệ thống AI hay Agent RAG nào. Do đó, việc xây dựng và vận hành một pipeline ETL chuẩn hóa là vô cùng quan trọng trước khi tích hợp dữ liệu vào AI.
