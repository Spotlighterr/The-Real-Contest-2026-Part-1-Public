# Hướng Dẫn Chi Tiết Quản Lý & Nhập Đề Câu Hỏi

Tài liệu này cung cấp hướng dẫn chi tiết cách quản lý, chỉnh sửa và đưa bộ đề câu hỏi mới vào hệ thống thi đấu **The Real Contest 2026: Chặng 1** (`index.html`) một cách an toàn và chuyên nghiệp nhất.

---

## 1. Cấu Trúc Ngân Hàng Câu Hỏi Trong Code

Tất cả câu hỏi của trò chơi được lưu trữ dưới dạng một mảng các đối tượng Javascript (mảng `allQuestions`) đặt tại phần `<script>` cuối tệp `index.html` (từ dòng 976 đến 1477).

Mỗi câu hỏi là một đối tượng JSON có định dạng như sau:
```javascript
{
    "text": "Nội dung câu hỏi của bạn...\nA. Lựa chọn A\nB. Lựa chọn B\nC. Lựa chọn C\nD. Lựa chọn D",
    "answer": "Đáp án hiển thị (VD: C. Lựa chọn C hoặc cụm từ đáp án điền khuyết)",
    "points": 10 // Số điểm của câu hỏi (Thường là 10, 20 hoặc 30)
}
```

### Chi tiết các thuộc tính:
*   `text` (Kiểu chuỗi): Chứa nội dung câu hỏi. Đối với câu hỏi trắc nghiệm có các phương án lựa chọn A, B, C, D, hãy sử dụng ký tự xuống dòng `\n` để phân tách rõ ràng từng dòng (Ví dụ: `A. Lựa chọn A\nB. Lựa chọn B...`).
*   `answer` (Kiểu chuỗi): Chứa đáp án chính xác sẽ được hiển thị khi MC nhấn nút **ĐÚNG**, **SAI**, hoặc **BỎ QUA**.
*   `points` (Kiểu số): Số điểm cộng/trừ của câu hỏi. Giá trị này quyết định số điểm đội thi nhận được khi trả lời đúng, hoặc bị trừ một nửa số điểm khi trả lời sai.

---

## 2. Quy Tắc Phân Chia Câu Hỏi Theo Đội Thi

Hệ thống thi đấu quản lý 4 đội thi: **VISTANIAN**, **M2D**, **SOLAIRE**, và **ATLAS CITY**.
Để đảm bảo tính công bằng và dễ quản lý, ngân hàng gồm đúng **100 câu hỏi** được phân bổ cố định cho mỗi đội thi **25 câu liên tiếp** dựa trên dải chỉ số (Index) trong mảng `allQuestions`:

| Đội thi | Số lượng câu | Dải chỉ số trong mảng (0-indexed) | Vị trí thực tế trong file code |
| :--- | :---: | :---: | :--- |
| **VISTANIAN** | 25 câu | **`0` đến `24`** | 25 câu đầu tiên của mảng `allQuestions` |
| **M2D** | 25 câu | **`25` đến `49`** | 25 câu tiếp theo |
| **SOLAIRE** | 25 câu | **`50` đến `74`** | 25 câu tiếp theo |
| **ATLAS CITY** | 25 câu | **`75` đến `99`** | 25 câu cuối cùng của mảng |

Sự phân bổ này được cấu hình thông qua biến `teamQuestionPools` trong code:
```javascript
const teamQuestionPools = {
  "VISTANIAN": Array.from({length: 25}, (_, i) => i),      // Lấy câu hỏi từ 0 đến 24
  "M2D": Array.from({length: 25}, (_, i) => i + 25),       // Lấy câu hỏi từ 25 đến 49
  "SOLAIRE": Array.from({length: 25}, (_, i) => i + 50),   // Lấy câu hỏi từ 50 đến 74
  "ATLAS CITY": Array.from({length: 25}, (_, i) => i + 75) // Lấy câu hỏi từ 75 đến 99
}
```

> [!IMPORTANT]
> Bạn **phải luôn duy trì đủ 100 câu hỏi** trong mảng `allQuestions` để tránh lỗi tràn bộ nhớ hoặc tải sai câu hỏi giữa các đội thi. Nếu bạn thay đổi số lượng câu hỏi của một đội, bạn cần điều chỉnh lại công thức trong `teamQuestionPools` tương ứng.

---

## 3. Cách Cập Nhật Câu Hỏi Tự Động (Khuyến khích)

Chúng tôi đã xây dựng sẵn một công cụ giao diện Web chuyên dụng là **`tool_nhap_de.html`** đặt ngay trong thư mục `Part_1/`. Bạn không cần biết lập trình vẫn có thể nhập đề cực nhanh:

1.  **Bước 1**: Nhấp đúp chuột để mở tệp `tool_nhap_de.html` bằng trình duyệt **Google Chrome** hoặc **Microsoft Edge**.
2.  **Bước 2**: Nhấn nút **"Chọn tệp index.html"** trên giao diện chính, trỏ đến đúng file `index.html` của trò chơi.
3.  **Bước 3**: Giao diện quản lý trực quan sẽ hiện ra. Bạn có thể:
    *   Bấm chọn các tab đội thi (VISTANIAN, M2D, SOLAIRE, ATLAS CITY) để xem danh sách 25 câu hỏi của từng đội.
    *   Nhấp vào bất kỳ câu hỏi nào để chỉnh sửa Nội dung, Đáp án, hoặc Điểm số ngay lập tức.
    *   Nhập câu hỏi mới thay thế hoặc hoán đổi vị trí câu hỏi dễ dàng.
4.  **Bước 4**: Sau khi chỉnh sửa xong, nhấn nút **"Lưu thay đổi vào index.html"** (Lưu trực tiếp). Trình duyệt sẽ yêu cầu cấp quyền ghi file, bạn hãy nhấn **Chấp nhận / Save**.
5.  Mở chạy file `index.html` để tận hưởng thành quả!

---

## 4. Cách Cập Nhật Câu Hỏi Thủ Công (Nếu cần chỉnh sửa trực tiếp)

Nếu bạn muốn chỉnh sửa thủ công bằng các công cụ đọc mã nguồn (như VS Code, Notepad++):

1.  **Bước 1**: Nhấp chuột phải vào file `index.html` chọn **Open With** -> **Visual Studio Code** (hoặc trình soạn thảo văn bản bất kỳ).
2.  **Bước 2**: Sử dụng tổ hợp phím `Ctrl + F` (hoặc `Cmd + F` trên Mac) tìm kiếm từ khóa: `const allQuestions = [`.
3.  **Bước 3**: Tìm đến câu hỏi bạn muốn sửa dựa theo chỉ số hoặc nội dung.
4.  **Bước 4**: Tiến hành chỉnh sửa nội dung trong các dấu ngoặc kép `""`.
    *   *Lưu ý về dấu nháy kép*: Nếu nội dung câu hỏi chứa dấu nháy kép `""`, hãy viết thêm dấu gạch chéo ngược `\` phía trước (Ví dụ: `\"Đô thị đặc biệt\"`) để tránh lỗi cú pháp JS.
    *   *Lưu ý về xuống dòng*: Sử dụng `\n` thay vì ấn phím Enter để xuống dòng trong chuỗi câu hỏi.
5.  **Bước 5**: Nhấn `Ctrl + S` để lưu lại tệp.

---

## 5. Lưu Ý Quan Trọng Khi Nhập Đề Để Đưa Lên GitHub

Khi đưa mã nguồn lên GitHub, hãy đảm bảo:
*   **Không đẩy các file rác**: File backup tự động (`.bak`, `.bak2`), file nháp Excel tạm thời (`~$Update.xlsx`) đã được khai báo bỏ qua trong tệp `.gitignore` ở thư mục gốc của repository.
*   **Định dạng chuẩn**: Tệp `index.html` phải luôn lưu dưới dạng mã hóa **UTF-8** để hiển thị tiếng Việt có dấu chính xác trên trình duyệt và không bị lỗi hiển thị font chữ trên GitHub.
*   **Kiểm tra tính hợp lệ**: Sau khi chỉnh sửa, hãy mở `index.html` trên máy tính chạy thử một lượt trước khi thực hiện lệnh `git commit` và `git push`.
