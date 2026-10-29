# Bài tập tổng hợp: Nhóm SmartCampus chạy nước rút trước deadline

## Phần 1 – Thiết lập Hybrid Workflow

### 1. Laptop hỏng ổ cứng có làm mất Slide_BaoCao.pptx mới nhất không?

Nếu nhóm đã thiết lập đúng **Hybrid Workflow = Local + Auto Sync** và lần đồng bộ gần nhất đã hoàn tất, sự cố hỏng ổ cứng không làm mất bản mới nhất. File vẫn còn trên Cloud và có thể tải lại trên máy khác.

Tuy nhiên, Auto Sync không phải là sao lưu tức thời trong mọi trường hợp. Nếu bạn vừa sửa file khi đang mất mạng, ứng dụng đồng bộ bị tạm dừng hoặc biểu tượng đồng bộ chưa báo hoàn tất thì phần thay đổi mới nhất có thể chưa lên Cloud. Vì vậy trước khi tắt máy hoặc kết thúc buổi làm việc, phải kiểm tra trạng thái **Synced/Up to date**.

### 2. Ba bước thiết lập Auto Sync

1. Cài Google Drive for desktop, đăng nhập bằng tài khoản dự án và bật ứng dụng tự khởi động cùng máy.
2. Chọn thư mục dự án SmartCampus trên laptop, chọn **Sync with Google Drive** và bật đồng bộ tự động cho thư mục này.
3. Chờ biểu tượng báo **Synced/Up to date**, sau đó tạo một file kiểm tra nhỏ và mở Drive trên web để xác nhận file đã xuất hiện trên Cloud.

### 3. Khôi phục hai trang bị xóa nhầm

Không gõ lại từ đầu. Thực hiện như sau:

1. Mở BaoCao_CuoiKy_SmartCampus.docx trên Drive.
2. Nếu file đã được mở bằng Google Docs: chọn **File → Version history → See version history**.
3. Chọn phiên bản có thời gian trước lúc xóa hai trang, kiểm tra phần nội dung xem đã đúng chưa, rồi chọn **Restore this version**.
4. Nếu file vẫn giữ nguyên định dạng Word: nhấp phải file trên Drive, mở phần quản lý phiên bản (**Manage versions**), chọn bản tải lên trước đó và khôi phục/tải bản đó về.
5. Đặt lại tên hoặc ghi chú phiên bản sau khi khôi phục để cả nhóm biết đây là bản đã cứu dữ liệu.

### 4. Hai sai lầm khi đồng bộ cả thư mục dự án

- **Đồng bộ thư mục node_modules:** đây là thư mục sinh ra từ dependency, có hàng vạn file nhỏ, làm chậm Auto Sync, tốn dung lượng và dễ tạo nhiều thay đổi không cần thiết. Cách đúng là loại khỏi thư mục đồng bộ bằng danh sách loại trừ; mỗi máy tự chạy lại lệnh npm install hoặc npm ci.
- **Đồng bộ các file phim 4K xem giải trí:** đây là dữ liệu lớn, không phục vụ báo cáo, làm tốn băng thông và dung lượng Cloud. Cách đúng là chuyển ra ngoài thư mục dự án hoặc không đưa vào phạm vi Auto Sync.

Hai lỗi trên đều thuộc nhóm **đồng bộ dữ liệu không cần thiết**: đưa file sinh tự động, file tạm hoặc file giải trí vào Cloud Workspace làm tăng chi phí và nguy cơ xung đột mà không giúp nhóm hoàn thành báo cáo.

## Phần 2 – Phân quyền chia sẻ an toàn

### 1. Bảng quyền cho từng file

Quy ước: mỗi dòng chỉ chọn một mức quyền và một phạm vi chia sẻ.

| File | Mức quyền | Phạm vi chia sẻ | Giải thích |
|---|---|---|---|
| BaoCao_CuoiKy_SmartCampus.docx gửi giảng viên | **Viewer** | **Restricted**, chia sẻ trực tiếp đúng email giảng viên | Giảng viên chỉ cần mở và chấm; Viewer ngăn sửa đè nội dung báo cáo |
| Slide_BaoCao.pptx cho 5 thành viên nhóm | **Editor** | **Restricted**, chia sẻ trực tiếp cho 5 email thành viên | Cả nhóm cần cùng chỉnh sửa gấp; Restricted tránh người ngoài có link truy cập |
| GopY_BanNhap.docx gửi anh khóa trên | **Commenter** | **Restricted**, chia sẻ trực tiếp đúng email anh khóa trên | Anh ấy đọc và để lại nhận xét nhưng không sửa trực tiếp bản nháp |
| ThongTin_CaNhan_NhomVien.xlsx | **Editor** | **Restricted**, chỉ trưởng nhóm và người làm thủ tục được cấp quyền | File cần cập nhật hồ sơ nhưng chứa CCCD và SĐT; không chia sẻ cho cả nhóm nếu không cần |

### 2. Quy tắc Cờ Đỏ Bảo mật cho file thông tin cá nhân

Áp dụng quy tắc:

- Dữ liệu CCCD, SĐT là dữ liệu nhạy cảm nên luôn để **Restricted**.
- Chỉ cấp cho những người thật sự làm thủ tục; dùng email cá nhân cụ thể hoặc nhóm nội bộ được kiểm soát.
- Không dùng **Anyone with the link**, không đăng link vào Zalo hoặc channel công khai.
- Không đặt file trong thư mục cha mà cả nhóm đang có quyền Editor, vì quyền thư mục có thể được kế thừa xuống file.
- Khi hoàn tất thủ tục, thu hồi quyền của người hỗ trợ và lưu/xóa dữ liệu theo quy định của nhóm.

Không được kết hợp **Anyone with the link + Editor** vì bất kỳ ai có link đều có thể chỉnh sửa, xóa, tải hoặc tiếp tục chia sẻ dữ liệu CCCD và SĐT. Khi đó nhóm không xác định được ai đã truy cập, dữ liệu có thể bị thay đổi và việc thu hồi quyền gần như không còn kiểm soát theo từng người.

### 3. Hai thao tác trong Settings cho Slide_BaoCao.pptx

Vì cả 5 thành viên đều là Editor, trưởng nhóm nên:

1. **Tắt “Editors can change permissions and share”** để thành viên không tự mời người lạ hoặc đổi quyền cho tài khoản ngoài nhóm.
2. **Tắt “Viewers and commenters can download, print, and copy”** để nếu sau này có người được cấp Viewer/Commenter thì họ không thể tải hoặc sao chép tùy ý.

Thiết lập thứ hai không hạn chế được Editor; vì vậy file vẫn phải để Restricted và người quản lý phải rà soát danh sách 5 Editor. Nếu cần gửi bản trình chiếu ra ngoài, nên xuất một bản PDF riêng thay vì chia sẻ file nguồn.

## Phần 3 – Tổ chức giao tiếp nhóm chuẩn doanh nghiệp

### 1. Ba vấn đề trong đoạn chat Zalo

1. **No-Hello / thiếu ngữ cảnh:** “có ai rảnh không” và “giúp em cái này được không ạ” buộc người đọc phải hỏi lại việc gì, cần bao lâu và hạn khi nào.
2. **Tin nhắn không phân luồng:** ảnh mèo và câu chuyện vui nằm chung dòng với công việc, làm giảm khả năng tìm lại thông tin; nhóm chưa tách channel/topic công việc và tán gẫu.
3. **Spam @all giờ khuya:** thông báo lúc 23:47 gọi toàn nhóm nhưng không nêu rõ ai còn thiếu phần nào, cần làm gì và hạn cụ thể; đây là giao tiếp đồng bộ bị đẩy sang mọi người ngoài giờ thay vì dùng thông báo có lịch và tag đúng người.

### 2. Channel/Topic nên tạo

- **#thong-bao-deadline:** chỉ đăng deadline, thay đổi kế hoạch và quyết định ảnh hưởng cả nhóm.
- **#bao-cao-noi-dung:** trao đổi từng mục báo cáo, dẫn link file và dùng thread cho góp ý chi tiết.
- **#slide-thuyet-trinh:** chỉnh slide, hình ảnh, kịch bản nói và danh sách việc còn thiếu.
- **#task-handover:** tạo Task, ghi người phụ trách, trạng thái và deadline.
- **#random:** tán gẫu; không dùng làm nơi lưu quyết định hay file chính thức.

### 3. Viết lại tin nhắn đầu tiên của Lan theo tư duy Asynchronous

> **[Cần người kiểm tra mục 3.2 – hạn hôm nay]**  
> Mình đã hoàn thành phần nội dung mục 3.2 của báo cáo nhưng cần một bạn đọc lại số liệu và lỗi chính tả trong khoảng 20 phút. Bạn nào có thể nhận việc, vui lòng trả lời trực tiếp tên mình trước 14:30; nếu chưa thể làm hôm nay, hãy đề xuất một khung giờ khác. File: [link đến BaoCao_CuoiKy_SmartCampus.docx].

Tin nhắn này có đủ bối cảnh, việc cần làm, thời lượng, hạn phản hồi và link nên người đọc lúc 14:00 hoặc 22:00 đều có thể trả lời ngay.

### 4. Viết lại tin nhắn lúc 23:47 bằng Schedule Send

Đặt **Schedule Send lúc 08:00 sáng hôm sau**, không gửi ngay lúc 23:47:

> **[DEADLINE – cần hoàn thành trước 10:00]**  
> Theo bảng tiến độ, @Lan còn thiếu phần kết luận mục 4 và @Nam còn thiếu bảng kiểm thử API. Vui lòng cập nhật hai phần này vào Slide_BaoCao.pptx trước 10:00 sáng nay và đánh dấu Task là Done sau khi hoàn tất. @Hoa, bạn kiểm tra lại bản cuối trong thread trước 11:00. Nếu có vướng mắc, trả lời ngay dưới tin nhắn này kèm phần đang bị kẹt và thời điểm có thể hoàn thành.

Tin nhắn dùng tag đích danh, nêu rõ việc và deadline; không dùng @all.

## Phần 4 – Thông báo tổng hợp trên #thong-bao

> **[SmartCampus – cập nhật trước deadline]**  
> Mình đã bật **Auto Sync** cho thư mục dự án trên laptop và kiểm tra trạng thái đã đồng bộ lên Cloud.  
>   
> File **BaoCao_CuoiKy_SmartCampus.docx** đã được chia sẻ cho giảng viên với quyền **Viewer / Restricted**, nên giảng viên có thể xem và chấm nhưng không sửa đè nội dung.  
>   
> Theo bảng tiến độ, @Lan hoàn thiện kết luận mục 4 trước 10:00, @Nam bổ sung bảng kiểm thử API trước 10:00 và @Hoa kiểm tra bản cuối trước 11:00. Vui lòng cập nhật trực tiếp trên file/Task tương ứng và phản hồi trong thread khi xong. Các trao đổi ngoài phạm vi công việc đưa sang #random; không gửi lại dữ liệu cá nhân hoặc link công khai trong nhóm.

Thông báo này kết hợp ba kỹ năng: bảo đảm file có bản Cloud dự phòng, cấp đúng quyền cho giảng viên và giao việc bằng tag đích danh trong một kênh chính thức.
