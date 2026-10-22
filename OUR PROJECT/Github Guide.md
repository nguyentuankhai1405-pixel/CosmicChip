

| Mục đích            | Câu lệnh Git (Terminal / Git Bash)                        | Thao tác tương đương trên Web GitHub       |
| :------------------ | :-------------------------------------------------------- | :----------------------------------------- |
| **Khai báo tên**    | `git config --global user.name "Tên Của Bạn"`             | Có sẵn trong phần *Settings $\to$ Profile* |
| **Khai báo email**  | `git config --global user.email "email_github@gmail.com"` | Có sẵn trong *Settings $\to$ Emails*       |
| **Tải repo về máy** | `git clone https://github.com/.../CosmicChip.git`         | Nút xanh **Code** $\to$ *Download ZIP*     |

---

### PHẦN 2: VÒNG LẶP LÀM VIỆC HÀNG NGÀY (DAILY WORKFLOW)
*(Thực hiện liên tục mỗi khi ngồi vào bàn làm việc)*

```
[BƯỚC 1: Kéo mới nhất] ──► [BƯỚC 2: Sửa file] ──► [BƯỚC 3: Đóng gói & Ghi chú] ──► [BƯỚC 4: Đẩy lên mây]
     git pull origin main                               git add . & commit             git push origin main
```

1. **Bước 1 (Bắt buộc trước khi làm): Kéo dữ liệu mới của đồng đội về máy:**
   ```bash
   git pull origin main
   ```
2. **Bước 2: Kiểm tra trạng thái các file vừa sửa:**
   ```bash
   git status
   ```
3. **Bước 3: Đóng gói và ghi chú công việc (Commit):**
   ```bash
   git add .
   git commit -m "tiền_tố: nội dung ngắn gọn công việc đã làm"
   ```
   * *Quy ước tiền tố commit:*
     * `hw: ...` $\to$ Phần cứng, KiCad, schematic, PCB (Vĩ)
     * `fw: ...` $\to$ Code RP2040, thuật toán bù nhiệt (Khải)
     * `mech: ...` $\to$ Thiết kế 3D, scintillator, quang học (Đào)
     * `sim: ...` $\to$ Code mô phỏng MATLAB, Python (Đào / Khải)
     * `docs: ...` $\to$ Viết bài báo, thuyết minh Euréka (Cả nhóm)
4. **Bước 4: Đẩy lên GitHub cho cả nhóm xem:**
   ```bash
   git push origin main
   ```

---

### PHẦN 3: KỸ THUẬT QUẢN LÝ PHIÊN BẢN (XÓA BỎ THÓI QUEN `FinalData_1`, `FinalData_2`)
*(Không bao giờ nhân bản tên file/folder, chỉ giữ duy nhất 1 file và dùng lịch sử Git)*

* **Xem lại lịch sử các lần lưu (Checkpoints):**
  ```bash
  git log --oneline -n 10
  ```
  *(Hiện danh sách 10 commit gần nhất kèm mã băm 7 ký tự, ví dụ: `a1b2c3d`)*.
* **Quay ngược thời gian khôi phục 1 file về quá khứ:**
  ```bash
  git checkout a1b2c3d -- ten_file.txt
  ```
* **Hủy toàn bộ chỉnh sửa chưa commit (quay về trạng thái sạch gần nhất):**
  ```bash
  git restore .
  ```
* **Đóng mộc cột mốc quan trọng (Tagging thay cho chữ "Final"):**
  ```bash
  # Tạo mốc
  git tag -a v1.0-nop-eureka -m "Bản chốt nộp hồ sơ Euréka"
  # Đẩy mốc lên GitHub
  git push origin v1.0-nop-eureka
  # Quay lại xem đúng phiên bản mốc đó bất cứ lúc nào
  git checkout v1.0-nop-eureka
  ```

---

### PHẦN 4: KỸ THUẬT PHÂN NHÁNH THỬ NGHIỆM (BRANCHING)
*(Thử nghiệm thoải mái ở "thế giới song song", không sợ hỏng bản chính)*

#### Quy trình thử nghiệm:
1. **Tạo và nhảy sang nhánh thử nghiệm mới:**
   ```bash
   git switch -c test-mach-peak-detector
   # (Hoặc lệnh cũ: git checkout -b test-mach-peak-detector)
   ```
2. **Sửa file, thử nghiệm và commit bình thường trên nhánh này:**
   ```bash
   git add .
   git commit -m "hw: thử nghiệm đổi giá trị tụ lưu đỉnh sang 100pF"
   ```

#### Khi có kết quả:
* **KỊCH BẢN A: Thử nghiệm THẤT BẠI $\to$ Xóa bỏ sạch sẽ trong 1 nốt nhạc:**
  ```bash
  # Bước 1: Nhảy về nhánh chính
  git switch main
  # Bước 2: Xóa sổ nhánh thử nghiệm (tham số -D là xóa cưỡng bức)
  git branch -D test-mach-peak-detector
  ```
  *(Toàn bộ file thử nghiệm lỗi biến mất, nhánh chính giữ nguyên $100\%$ sạch sẽ)*.

* **KỊCH BẢN B: Thử nghiệm THÀNH CÔNG $\to$ Gộp vào bản chính thức (Merge):**
  ```bash
  # Bước 1: Nhảy về nhánh chính
  git switch main
  # Bước 2: Gộp kết quả vào main
  git merge test-mach-peak-detector
  # Bước 3: Xóa nhánh phụ đã gộp cho gọn
  git branch -d test-mach-peak-detector
  # Bước 4: Đẩy lên GitHub
  git push origin main
  ```

---

### PHẦN 5: KỸ THUẬT NÂNG CAO – MỞ 2 FOLDER SONG SONG (`git worktree`)
*(Dành cho khi muốn mở 2 cửa sổ chạy 2 thí nghiệm cùng lúc trên 2 thư mục vật lý riêng mà không cần clone lại repo)*

* **Tạo một thư mục vật lý mới song song liên kết với nhánh thử nghiệm:**
  ```bash
  git worktree add ../CosmicChip-Test test-mach-moi
  ```
* **Xong việc, xóa bỏ thư mục thí nghiệm:**
  ```bash
  git worktree remove ../CosmicChip-Test
  ```

---

### PHẦN 6: KỸ THUẬT XỬ LÝ XUNG ĐỘT (MERGE CONFLICTS)
*(Xảy ra khi 2 người cùng sửa chung 1 dòng trong cùng 1 file và cùng đẩy lên)*

1. Khi gõ `git pull origin main` bị báo lỗi đỏ: `CONFLICT (content)...`
2. Mở file bị lỗi bằng **VS Code**, bạn sẽ thấy đoạn so sánh:
   ```text
   <<<<<<< HEAD (Phần của bạn)
   V_threshold = 4.0; // mV
   =======
   V_threshold = 5.0; // Đồng đội vừa đổi
   >>>>>>> a1b2c3d...
   ```
3. Bấm vào chữ **Accept Current Change** (giữ phần của bạn) hoặc **Accept Incoming Change** (lấy phần của bạn bè) hoặc sửa lại thành giá trị đúng nhất.
4. Lưu file lại và chạy tiếp:
   ```bash
   git add .
   git commit -m "fix: giải quyết xung đột ngưỡng trigger"
   git push origin main
   ```

---

### PHẦN 7: BẢNG ĐỐI CHIẾU THAO TÁC (DÙNG LỆNH vs. DÙNG CHUỘT TRÊN WEB)

Nếu bạn không muốn mở Git Bash mà muốn làm hoàn toàn trên trình duyệt:

| Thao tác | Cách gõ lệnh Git | Cách làm trên Web GitHub |
| :--- | :--- | :--- |
| **Mở bộ soạn thảo nhanh** | Mở VS Code trên máy tính | **Bấm phím dấu chấm `.`** ngay trên trang web repo |
| **Tạo thư mục con** | `mkdir Hardware` | Bấm *Add file $\to$ Create new file*, gõ: `Hardware/README.md` |
| **Upload file / Đẩy code**| `git add .` + `git commit` + `push` | Bấm *Add file $\to$ Upload files* $\to$ Kéo thả file $\to$ *Commit changes* |
| **Tạo nhánh mới** | `git switch -c <tên-nhánh>` | Bấm nút **`main`** góc trái $\to$ Gõ tên nhánh mới $\to$ *Create branch* |
| **Xóa nhánh thử nghiệm**| `git branch -D <tên-nhánh>` | Vào tab **Branches** $\to$ Bấm icon **Thùng rác** |
| **Gộp nhánh (Merge)** | `git merge <tên-nhánh>` | Vào tab **Pull requests** $\to$ *New pull request* $\to$ *Merge* |
| **Đóng mốc phiên bản** | `git tag -a v1.0` | Cột phải bấm **Releases** $\to$ *Draft a new release* $\to$ *Publish* |

---

### PHẦN 8: KỸ THUẬT XỬ LÝ VÀ XEM DỮ LIỆU NẶNG (LARGE DATASETS)

GitHub giới hạn file $< 25 - 100\,\text{MB}$, không thể để file đo muon hàng triệu dòng vào thư mục Git thông thường:

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ MÔ HÌNH PHÂN PHỐI LƯU TRỮ DỮ LIỆU CHUẨN KHOA HỌC:                                      │
│                                                                                        │
│ 1. Trực tiếp trên Git: Chỉ lưu file mẫu "sample_data_1000_lines.txt" (<1 MB).          │
│    (Mục đích: Người xem/giám khảo bấm vào là xem được cấu trúc bảng cột ngay trong 0.1s)│
│                                                                                        │
│ 2. Mục GitHub Releases: Nén file dữ liệu 7 ngày (.zip) nặng 100 MB - 2 GB.             │
│    (Mục đích: Lưu trữ phiên bản sản phẩm và dữ liệu lớn kèm mã nguồn)                  │
│                                                                                        │
│ 3. Cổng Zenodo.org (CERN): Tải lên toàn bộ dataset thô (cho phép tới 50 GB miễn phí). │
│    (Mục đích: Lấy mã DOI vĩnh viễn đưa vào bài báo HardwareX và thuyết minh Euréka)     │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

### PHẦN 9: FILE BỘ LỌC RÁC BẮT BUỘC (`.gitignore`)
Tạo một file đặt tên là `.gitignore` ở thư mục gốc của repo để Git tự động bỏ qua các file tạm thời, tránh làm rác và phình to dung lượng repo:

```text
# Bỏ qua file rác của KiCad
*.kicad_prl
*.bak
*-backups/
_autosave-*

# Bỏ qua file tạm của MATLAB
*.asv
*.m~
slprj/

# Bỏ qua file rác hệ điều hành
Thumbs.db
.DS_Store

# Bỏ qua file tạm khi biên dịch LaTeX
*.aux
*.log
*.out
*.toc
*.synctex.gz
```