# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600022
**Name:** Đặng Quang Minh
**Date:** 2026-04-15

---

## 1. Muc tieu thi nghiem

Muc tieu cua bai thi nghiem la kiem tra muc do anh huong cua chat luong du lieu dau vao den kha nang tra loi cua mot AI agent don gian. Trong repo nay, agent duoc mo phong bang script `agent_simulation.py`, trong do agent doc du lieu tu file CSV va tra loi cau hoi: "What is the best electronic product?"

De so sanh, toi su dung hai bo du lieu:

- `processed_data.csv`: du lieu da duoc ETL pipeline lam sach.
- `garbage_data.csv`: du lieu co chu y chen cac loi chat luong nhu duplicate ID, sai kieu du lieu, gia tri null va outlier.

---

## 2. Cach thuc thuc hien

Quy trinh duoc thuc hien nhu sau:

1. Chay `python solution.py` de doc `raw_data.json`, validate du lieu, transform du lieu va tao file `processed_data.csv`.
2. Chay `python generate_garbage.py` de tao file `garbage_data.csv`.
3. Chay `python agent_simulation.py` de kiem tra phan hoi cua agent tren hai bo du lieu.
4. Ghi lai ket qua va phan tich su khac biet giua clean data va garbage data.

---

## 3. Ket qua thi nghiem

| Scenario | Input File | Agent Response | Accuracy (1-10) | Notes |
|----------|------------|----------------|-----------------|-------|
| Clean Data | `processed_data.csv` | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Du lieu da duoc lam sach, chi giu lai cac record hop le, category da duoc chuan hoa nen agent dua ra cau tra loi hop ly. |
| Garbage Data | `garbage_data.csv` | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Agent bi anh huong boi outlier co gia qua lon trong category electronics, dan den lua chon sai va phi thuc te. |

---

## 4. So sanh Clean Data va Garbage Data

Su khac biet lon nhat giua hai truong hop nam o chat luong cua nguon du lieu. Voi clean data, cac record loi da bi loai bo truoc khi dua vao agent. Gia tri category duoc viet dong nhat, cac record co gia am hoac category rong khong con ton tai. Nhờ do, agent co the tim dung san pham lien quan va dua ra cau tra loi kha hop ly.

Nguoc lai, garbage data co nhieu van de chat luong du lieu. Co duplicate ID lam tang nguy co nham lan giua cac thuc the. Co record co `price` la chuoi `"ten dollars"` gay sai kieu du lieu. Co gia tri `None` va gia tri bang `0` lam du lieu khong day du va khong dang tin cay. Nghiem trong nhat la outlier `Nuclear Reactor` voi gia `999999`, khien agent uu tien san pham nay chi vi no co gia cao nhat trong nhom electronics.

---

## 5. Phan tich va nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trong bai lab nay hoat dong theo logic rat don gian: neu cau hoi co lien quan den electronics, agent se loc cac dong co `category = electronics`, sau do chon record co gia cao nhat. Cach lam nay co the hoat dong tot khi du lieu da duoc lam sach, nhung se rat de bi danh lua khi nguon du lieu chua record bat thuong.

Trong file `garbage_data.csv`, record `Nuclear Reactor` co gia `999999` la mot outlier rat lon. Ve mat ky thuat, record nay van nam trong category electronics, nen agent xem day la lua chon "tot nhat" du no khong phu hop voi ngu canh thuc te cua bai toan. Dieu nay cho thay agent khong that su "hieu" du lieu, ma dang dua vao cac quy tac don gian de suy ra cau tra loi. Khi du lieu dau vao bi ban, ket qua cua agent cung se bi lech theo.

Ben canh do, duplicate ID co the gay trung lap thuc the, sai kieu du lieu co the lam hong qua trinh tinh toan hoac loc, con null values lam giam do day du cua bo du lieu. Duy chi mot van de trong so do cung da co the lam agent tra loi kem tin cay; khi nhieu van de xuat hien cung luc, rui ro se tang len ro ret. Bai thi nghiem nay cho thay chat luong du lieu la nen tang cua AI system. Neu khong co buoc validation va observability trong data pipeline, chung ta rat kho phat hien vi sao agent tra loi sai va cung kho tin tuong ket qua do.

---

## 6. Ket luan

Toi dong y voi nhan dinh: **Quality Data > Quality Prompt**. Prompt tot chi giup agent dien dat ro rang hon hoac huong dan cach xu ly thong tin, nhung no khong the sua duoc mot nguon du lieu sai hoac bi nhiem rac. Trong bai nay, cung mot cau hoi va cung mot logic agent, nhung khi dung clean data thi agent dua ra cau tra loi hop ly, con khi dung garbage data thi agent dua ra mot lua chon sai lech ro rang.

Vi vay, truoc khi toi uu prompt, can uu tien xay dung ETL pipeline, validation, cleaning va data observability. Khi du lieu nguon dang tin cay, kha nang AI dua ra ket qua dung va on dinh se cao hon rat nhieu.

---

## 7. De xuat cai thien

De giam kha nang agent tra loi sai trong tuong lai, co the ap dung mot so huong cai thien sau:

1. Bo sung validation de loai bo outlier bat thuong hoac danh dau can review.
2. Kiem tra kieu du lieu truoc khi dua vao he thong tra loi.
3. Xu ly duplicate ID va cac gia tri null ngay trong ETL pipeline.
4. Them logging va metrics de theo doi so record bi loai, so loi kieu du lieu va cac gia tri bat thuong.
5. Cai tien logic cua agent de khong chi dua vao gia cao nhat, ma con xet den tinh hop ly cua san pham.
