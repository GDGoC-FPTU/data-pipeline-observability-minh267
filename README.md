[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572469&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** 2A202600022
**Student Email:** dqminh267@gmail.com
**Name:** Đặng Quang Minh

---

## Mo ta

Trong bai lab nay, toi xay dung mot ETL pipeline don gian de doc du lieu tu file JSON, kiem tra chat luong du lieu, bien doi du lieu theo business rule va luu ket qua ra file CSV. Pipeline loai bo cac record co `price <= 0` hoac `category` rong, tinh them cot `discounted_price`, chuan hoa `category` sang Title Case va them timestamp `processed_at`.

Ngoai ETL, toi cung thuc hien stress test voi agent mo phong de so sanh ket qua khi su dung clean data va garbage data. Ket qua cho thay chat luong du lieu co anh huong truc tiep den kha nang tra loi dung cua agent.

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

Lenh tren se doc `raw_data.json`, validate du lieu, transform du lieu va tao file `processed_data.csv`.

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

Lenh dau tien tao file `garbage_data.csv`. Lenh thu hai so sanh phan hoi cua agent khi dung clean data (`processed_data.csv`) va garbage data (`garbage_data.csv`).

### Chay test local
```bash
pytest
```

---

## Cau truc thu muc

```text
├── solution.py
├── raw_data.json
├── processed_data.csv
├── generate_garbage.py
├── garbage_data.csv
├── agent_simulation.py
├── experiment_report.md
├── tests/
└── README.md
```

---

## Ket qua

- Tong so record dau vao: 5
- So record hop le sau validation: 3
- So record bi loai: 2
- File `processed_data.csv` da duoc tao thanh cong
- Ket qua stress test:
  - Clean Data: Agent tra loi `Laptop` la lua chon tot nhat voi gia `$1200`
  - Garbage Data: Agent tra loi sai va chon `Nuclear Reactor` voi gia `$999999`

## Ghi chu

Ma sinh vien hien dang de tam la `AI20K-0000` de dung dinh dang autograder. Ban nen thay lai bang ma so sinh vien thuc te truoc khi nop bai.
