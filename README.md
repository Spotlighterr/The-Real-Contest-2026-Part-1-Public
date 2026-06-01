# The Real Contest 2026 - Chặng 1

Chào mừng bạn đến với kho chứa mã nguồn chính thức của **The Real Contest 2026: Chặng 1**! Đây là ứng dụng web tương tác trực tiếp phục vụ cho vòng chung kết cuộc thi, sở hữu giao diện Glassmorphism hiện đại, chuyên nghiệp cùng hiệu ứng âm thanh sống động.

---

## 📂 Cấu trúc thư mục (Repository Structure)

```text
├── TRC/
│   ├── Part_1/
│   │   ├── index.html              # 🎮 Giao diện thi đấu và logic chính của trò chơi
│   │   ├── tool_nhap_de.html       # 🛠️ [MỚI] Công cụ giao diện Web giúp tự động nhập & sửa đề câu hỏi
│   │   ├── HUONG_DAN_NHAP_DE.md    # 📖 Hướng dẫn chi tiết cách quản lý câu hỏi
│   │   ├── *.mp3 / *.wav           # 🎵 Hệ thống âm thanh (Nhạc nền, âm báo Đúng/Sai/Skip/Click)
│   │   ├── *.xlsx                  # 📊 Tệp đề bài dự phòng dạng Excel
│   │   └── questions.txt           # 📝 Tệp văn bản thô chứa câu hỏi ban đầu
│   └── Lib/                        # 📚 Các thư viện hỗ trợ (nếu có)
├── netlify.toml                    # ⚡ Cấu hình triển khai nhanh lên Netlify
├── .gitignore                      # 🚫 Cấu hình các tệp tin được Git bỏ qua (node_modules, tệp tạm...)
├── LICENSE                         # ⚖️ Giấy phép MIT của dự án
└── README.md                       # 📝 Tệp giới thiệu tổng quan này
```

---

## ⚡ Tính năng nổi bật (Key Features)

1. **Giao diện đẳng cấp (Premium UI)**: Thiết kế Dark-mode huyền bí kết hợp với hiệu ứng kính mờ (Glassmorphism), chuyển động mượt mà (Micro-animations).
2. **Âm thanh tương tác song song**: Hỗ trợ nhạc nền lặp (Looping background music) có thể điều chỉnh âm lượng/bật/tắt trực quan và các âm thanh phản hồi (Đúng, Sai, Bỏ qua, Click) sống động.
3. **Phân chia Đội thi chuyên nghiệp**: Bảng điều khiển MC độc lập hỗ trợ phím tắt (`1`: Đúng, `2`: Sai, `3`: Bỏ qua, `M`: Tắt/Bật tiếng, `P`: Bật/Tắt nhạc nền).
4. **Hệ thống Quản lý Câu hỏi Tự động**: Tích hợp công cụ **`tool_nhap_de.html`** sử dụng công nghệ trình duyệt tiên tiến *File System Access API* cho phép đọc/ghi câu hỏi trực tiếp vào tệp `index.html` mà không cần cài đặt thêm phần mềm hay máy chủ.

---

## 🛠️ Hướng dẫn nhanh cách sử dụng và cập nhật câu hỏi

Để chạy trò chơi hoặc cập nhật bộ câu hỏi 100 câu mới, bạn hãy làm theo các bước đơn giản sau:

### 1. Trải nghiệm game thi đấu
*   Truy cập thư mục `TRC/Part_1/`.
*   Click đúp tệp **`index.html`** để chạy trực tiếp trên bất kỳ trình duyệt nào (Chrome, Edge, Firefox, Safari...).

### 2. Cập nhật câu hỏi tự động (Dễ nhất)
*   Mở tệp **`tool_nhap_de.html`** bằng trình duyệt Chrome hoặc Edge.
*   Bấm **"Chọn tệp index.html"** và trỏ đến đúng file `index.html` của bạn.
*   Chỉnh sửa hoặc thêm mới câu hỏi cực kỳ dễ dàng trên giao diện Web.
*   Nhấn **"Lưu thay đổi vào index.html"** để tự động đồng bộ hóa và cập nhật trực tiếp vào trò chơi!

> [!NOTE]
> Để xem chi tiết cấu trúc mảng câu hỏi và cách phân chia dải chỉ số (Index) câu hỏi cho từng đội thi đấu (VISTANIAN, M2D, SOLAIRE, ATLAS CITY), vui lòng đọc hướng dẫn tại:
> 👉 [**HUONG_DAN_NHAP_DE.md**](file:///TRC/Part_1/HUONG_DAN_NHAP_DE.md)

---

## ⚖️ Giấy phép (License)

Dự án này được phát hành dưới Giấy phép **MIT License**. Xem chi tiết tại tệp [LICENSE](./LICENSE).

---
*Chúc bạn có những trải nghiệm tuyệt vời cùng The Real Contest 2026!*
