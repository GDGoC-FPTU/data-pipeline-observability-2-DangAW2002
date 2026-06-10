# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** 2A202600602  
**Student Email:** 26ai.dangnn@vinuni.edu.vn  
**Name:** Nguyễn Nhựt Đăng  

---

## Mo ta

Bài lab này thực hiện xây dựng một quy trình ETL (Extract, Transform, Load) tự động bằng Python để làm sạch, chuẩn hóa và quan sát dữ liệu (observability) trước khi đưa vào Agent AI. Đồng thời thực hiện Stress Test để đánh giá ảnh hưởng của chất lượng dữ liệu (Data Quality) đối với độ chính xác phản hồi của Agent AI RAG.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Bước 1: Tạo tệp dữ liệu rác (garbage_data.csv)
python generate_garbage.py

# Bước 2: Chạy chương trình mô phỏng phản hồi của Agent AI
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline sau khi lam sach
├── generate_garbage.py      # Script tao du lieu rac cho stress test
├── agent_simulation.py      # Script mo phong Agent AI tra loi
├── experiment_report.md     # Bao cao thi nghiem va phan tich
└── README.md                # File nay
```

---

## Ket qua

Hệ thống ETL đã chạy thành công với kết quả như sau:
- **Tổng số bản ghi đầu vào:** 5 bản ghi.
- **Số bản ghi hợp lệ được xử lý:** 3 bản ghi (Laptop, Chair, Monitor).
- **Số bản ghi không hợp lệ bị loại (Dropped):** 2 bản ghi (Mystery Box có giá âm -10, và Phone có category bị trống).
- **Kết quả đầu ra:** Tệp `processed_data.csv` đã được lưu thành công với các cột giá trị tính toán đúng (`discounted_price` giảm 10%), nhóm danh mục chuẩn hóa chữ hoa đầu từ (Title Case), và ghi nhận mốc thời gian xử lý `processed_at`.
- **Kết quả Stress Test:** AI Agent trả lời đúng trên dữ liệu sạch (Laptop - $1200) nhưng bị sai lệch nghiêm trọng trên dữ liệu rác (chọn Nuclear Reactor - $999999 là sản phẩm điện tử tốt nhất do nhiễu ngoại lai).

