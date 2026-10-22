# CosmicWatch SiPM với mạch Analog Front End, bù nhiệt cho SiPM 

> **Mục đích của file này**: Giúp mọi thành viên mới trong nhóm biết được mục tiêu dự án, cách tổ chức vault Obsidian, thứ tự đọc tài liệu, và flow làm việc từ nghiên cứu → thiết kế → thực nghiệm → phân tích → viết bài.

---

## 1. Dự án

**Tên dự án (tạm thời):**  
“Thiết kế và đánh giá hệ thống đọc tín hiệu tương tự có khả năng bù nhiệt cho máy dò muon dùng SiPM”

**một detector muon chi phí thấp dựa trên plastic scintillator + SiPM, với analog front-end (AFE) và nguồn bias SiPM có bù nhiệt chủ động, sau đó đánh giá định lượng hiệu quả bù nhiệt và khả năng mở rộng thành kính viễn vọng.**

  **Cơ sở**
- CosmicWatch Desktop Muon Detector là detector muon giáo dục chi phí thấp của MIT, dùng scintillator + SiPM + electronics tùy chỉnh. [6][19]  
- SiPM có gain phụ thuộc mạnh vào nhiệt độ; môi trường nóng ẩm tại TP.HCM làm vấn đề này nổi bật.  
- Các hệ low-cost hiện tại thường tập trung vào tính di động/giáo dục, ít có đánh giá định lượng về ổn định nhiệt của readout.

**Vấn đề chính:**  
Khi nhiệt độ thay đổi, breakdown voltage của SiPM thay đổi, làm dịch gain, pulse amplitude và threshold hiệu dụng → count rate và kết quả đo không ổn định.

**Giải pháp đề xuất:**  
- Thiết kế AFE chi phí thấp cho SiPM.  
- Thiết kế nguồn bias có bù nhiệt chủ động theo mô hình \(V_\mathrm{bias}(T)\).  
- Đánh giá bằng thực nghiệm: so sánh fixed-bias, offline correction và active compensation.  
- Mở rộng thành module cho telescope 2 tầng và low-cost muon tomography.

---

## 2. Mục tiêu dự án

### 2.1. Mục tiêu nghiên cứu

- **RQ1 — Thermal drift:**  
  Nhiệt độ ảnh hưởng bao nhiêu đến amplitude, noise trigger rate và coincidence rate của detector scintillator–SiPM khi bias cố định?

- **RQ2 — Active compensation:**  
  Điều khiển bias theo nhiệt độ có làm giảm biến thiên của amplitude và coincidence-normalized rate so với fixed-bias không?

- **RQ3 — Cost-performance:**  
  Kiến trúc AFE + bù nhiệt đề xuất có đạt cải thiện đủ lớn so với chi phí, công suất và độ phức tạp tăng thêm không?

- **RQ4 — Scalability:**  
  Module có thể trở thành node nhiều kênh cho telescope hoặc low-cost muon tomography array không?

### 2.2. Mục tiêu đầu ra

- 1 detector muon hoàn chỉnh (≥1 tầng, khuyến nghị 2 tầng cho coincidence).  
- 1 PCB AFE + bias compensation tự thiết kế.  
- Dữ liệu thực nghiệm dài hạn về thermal drift và hiệu quả bù nhiệt.  
- 1 bài báo cấp trường hoặc nộp Euréka (lĩnh vực Kỹ thuật công nghệ hoặc Vật lý).  
- Repository mở (GitHub) chứa: schematic, BOM, firmware, script phân tích, tài liệu hướng dẫn.

---

## 3. Vai trò trong nhóm

> Điều chỉnh theo nhóm bạn.

| Vai trò         | Nhiệm vụ chính                                                 | Gợi ý thành viên |
| --------------- | -------------------------------------------------------------- | ---------------- |
| Hardware        | AFE, bias, PCB, bring-up, test bench                           | TBD              |
| Firmware        | MCU, ADC, timestamp, coincidence, logging, firmware versioning | TBD              |
| Data & analysis | Xử lý dữ liệu, thống kê, uncertainty, figures                  | TBD              |
| Documentation   | Obsidian vault, paper writing, slides, poster                  | TBD              |


---

## 4. Cấu trúc vault Obsidian


---

## 5. Hướng dẫn đọc

### Bước 1: Đọc overview




### Bước 2: Hiểu quá trình thiết kế CosmicWatch v3X

1. Đọc:  
   - `02_Literature/Project_Repositories/CosmicWatch_v3X.md`  
   - `03_Baseline_and_Requirements/CosmicWatch_v3X_Baseline.md`  

1. Vào GitHub gốc:  
   - https://github.com/spenceraxani/CosmicWatch-Desktop-Muon-Detector-v3X  
   - Đọc: README, Instruction Manual (phần đầu), BOM, schematic (nếu có).

1. Ghi chú lại:
   - SiPM model 
   - Bias circuit như thế nào, temperature compensation 
   - AFE kiến trúc (TIA, common-base, CSA)
   - Có coincidence không 
   - Firmware/logging

### Bước 3: Đọc tài liệu nền về SiPM và nhiệt độ

1. Vào `02_Literature/Papers/` và `02_Literature/Datasheets/`.  
2. Tìm các note có tag: `#topic/sipm`, `#topic/temperature-compensation`.  
3. Đọc ít nhất:
   - 1–2 paper về SiPM temperature compensation.  
   - Datasheet của 1–2 model SiPM (Hamamatsu/Ketek/Onsemi).  
4. Ghi chú vào note tương ứng:
   - Temperature coefficient của breakdown voltage.  
   - Ảnh hưởng của nhiệt độ lên gain, dark count.  
   - Các phương pháp bù nhiệt đã công bố.

### Bước 4: Nắm flow thực nghiệm

1. Mở `06_Experiments/00_Experiment_Index.md`.  
2. Xem danh sách experiment đã lên kế hoạch:
   - EXP-01: AFE noise & pulse test  
   - EXP-02: SiPM bias sweep  
   - EXP-03: Coincidence setup  
   - EXP-04: Temperature compensation  
3. Đọc 1–2 protocol mẫu trong `06_Experiments/Protocols/`.  
4. Hiểu cấu trúc:
   - Mục tiêu → Giả thuyết → Thiết bị → Cấu hình → Biến độc lập/phụ thuộc → Dữ liệu log → Tiêu chí dừng.

### Bước 5: Chọn việc để làm trong tuần này


## 6. Flow làm việc chuẩn (từ ý tưởng → paper)

### 6.1. Khi có một ý tưởng / câu hỏi mới

1. Tạo note trong `01_Problem_and_Questions/` hoặc `04_System_Design/`.  
2. Liên kết tới:
   - `Research_Questions.md` (RQ nào được trả lời?)  
   - `Research_Gap.md` (gap nào được lấp?)  
3. Nếu ý tưởng liên quan thiết kế: tạo/ cập nhật note trong `04_System_Design/`.  
4. Nếu cần thí nghiệm để kiểm chứng: tạo protocol trong `06_Experiments/Protocols/`.

### 6.2. Khi đọc một tài liệu mới (paper, datasheet, repo)

1. Lưu file gốc vào `99_Attachments/` (PDF, datasheet, link repo).  
2. Tạo note mới theo template:
   - `Template_Literature_Note.md` cho paper.  
   - Template tương tự cho datasheet/repo.  
3. Điền:
   - Citation/URL, tác giả, năm.  
   - Tóm tắt 5 dòng.  
   - Câu hỏi nghiên cứu mà tài liệu giúp trả lời.  
   - Thông số/bằng chứng có thể trích trong paper.  
   - Quyết định/rút ra cho dự án.  
4. Link note này tới:
   - `Research_Gap.md`  
   - `CosmicWatch_v3X_Baseline.md`  
   - Các note thiết kế/thí nghiệm liên quan.

### 6.3. Khi thiết kế một khối (AFE, bias, optical, DAQ)

1. Tạo/cập nhật note trong `04_System_Design/`, ví dụ `AFE_Design.md`.  
2. Nội dung tối thiểu:
   - Mục tiêu khối.  
   - Kiến trúc được chọn và lý do.  
   - Phương án thay thế đã xem xét.  
   - Thông số mục tiêu (gain, bandwidth, noise, power, cost).  
   - Link tới datasheet, paper, note baseline.  
3. Nếu quyết định quan trọng: tạo ADR trong `00_Dashboard/Decisions_Log.md` hoặc note ADR riêng.  
4. Link tới experiment sẽ validate thiết kế này.

### 6.4. Khi làm thí nghiệm

**Trước khi đo:**

1. Tạo protocol trong `06_Experiments/Protocols/EXP-XX_Ten_Thi_Nghiem.md`.  
2. Điền đầy đủ:
   - Mục tiêu, giả thuyết.  
   - Thiết bị, cấu hình.  
   - Biến độc lập/phụ thuộc.  
   - Dữ liệu cần log.  
   - Tiêu chí dừng.  

**Trong/sau khi đo:**

1. Tạo run log trong `06_Experiments/Run_Logs/YYYY-MM-DD_EXP-XX_Run-YY.md`.  
2. Ghi:
   - Cấu hình thật sự dùng (PCB rev, firmware commit, threshold, bias, geometry).  
   - Timeline, sự cố, sai lệch so với protocol.  
   - Link tới raw data (file name, checksum, thư mục Git/Drive).  
3. Cập nhật `Raw_Data_Manifest.md`.

### 6.5. Khi phân tích dữ liệu

1. Tạo/cập nhật note trong `07_Analysis/`:
   - `Data_Processing_Pipeline.md`  
   - `Figures_and_Tables.md`  
   - `Results_Summary.md`  
2. Mỗi figure/table quan trọng nên có note nhỏ:
   - Dữ liệu từ run nào?  
   - Script nào tạo ra? (commit hash)  
   - Ý nghĩa đối với RQ nào?  
3. Link kết quả về:
   - `Research_Questions.md`  
   - `Success_Metrics.md`  
   - Các section trong `08_Paper/`.

### 6.6. Khi viết bài báo

1. Mở `08_Paper/00_Paper_Outline.md`.  
2. Mỗi section (Introduction, Related Work, Methodology, Results, Discussion, Conclusion) là một file `.md` riêng.  
3. Viết nháp từng phần ngay khi có kết quả sơ bộ, không đợi “xong hết mới viết”.  
4. Dùng link nội bộ để kéo:
   - Kết quả từ `07_Analysis/Results_Summary.md`.  
   - Figure/table từ `Figures_and_Tables.md`.  
   - Phương pháp từ `04_System_Design/` và `06_Experiments/Protocols/`.  

## 7. Quy ước đặt tên và tag

### 7.1. Tag 



```text
#project/cosmicwatch
#detector/muon
#sensor/sipm
#topic/afe
#topic/temperature-compensation
#topic/coincidence
#topic/tomography
#source/paper
#source/datasheet
#source/repository
#status/unread
#status/reading
#status/extracted
#priority/P1
#priority/P2
```

---

## 8. Plugin 


- **Templater**: tạo nhanh literature note, protocol, run log, ADR.  
- **Tasks** hoặc **Dataview Tasks**: quản lý task theo tuần/dự án.  
- **Dataview**: tạo dashboard tự động (paper chưa đọc, experiment planned, decision open).  
- **Citations** + Zotero (Better BibTeX): quản lý trích dẫn, tạo `References.bib`.  
- **Obsidian Git**: backup và version history cho vault.  
- **Excalidraw** hoặc Mermaid: vẽ sơ đồ khối detector, AFE, flow experiment.

## 10. Link quan trọng

- Repo CosmicWatch v3X (baseline):  
  https://github.com/spenceraxani/CosmicWatch-Desktop-Muon-Detector-v3X  
- Trang chủ CosmicWatch:  
  http://www.cosmicwatch.lns.mit.edu  
- Bài báo CosmicWatch (arXiv):  
  https://arxiv.org/abs/1801.03029  
- Thể lệ Euréka:  
  https://eureka.khoahoctre.com.vn/
