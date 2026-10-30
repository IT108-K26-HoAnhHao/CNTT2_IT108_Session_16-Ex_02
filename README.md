# BÀI 2

## I. BẢN THIẾT KẾ PHÂN QUYỀN TRUY CẬP (ACCESS CONTROL MATRIX)

Để áp dụng **Quy tắc Cờ Đỏ Bảo mật** nhằm bảo vệ thông tin nhạy cảm (SĐT, Mức lương kỳ vọng) và ngăn chặn rò rỉ dữ liệu, toàn bộ quyền truy cập tệp danh sách ứng viên được tái cấu trúc nghiêm ngặt theo bảng dưới đây:

| Đối tượng | Mức quyền hạn | Tính năng được phép | Lý do nghiệp vụ / Biện pháp bảo mật |
| :--- | :---: | :--- | :--- |
| **Trưởng phòng Nhân sự (Owner)** | **Owner / Editor** | Toàn quyền cấu hình, phê duyệt chỉnh sửa, quản lý chia sẻ. | Là người chịu trách nhiệm chính về dữ liệu tuyển dụng. |
| **Các Trưởng bộ phận (HODs)** | **Commenter** | Xem dữ liệu, nhận xét và đề xuất ý kiến qua **Suggesting Mode**. | Đảm bảo đóng góp ý kiến đánh giá ứng viên mà không làm thay đổi trực tiếp file gốc khi chưa duyệt. |
| **Nhân viên Nhân sự (HR Staff)** | **Viewer** | Chỉ xem thông tin điều phối, không được chỉnh sửa hay chia sẻ. | Hạn chế tối đa rủi ro "vô tình thao tác sai" gây rò rỉ hoặc sửa đổi cấu trúc tệp. |
| **Ứng viên / Đối tác bên ngoài** | **Restricted (No Access)** | Không có quyền truy cập tệp. | Thông tin nhân sự và quỹ lương là bảo mật tuyệt đối của Startup. |

### Cấu hình bảo mật nâng cao bắt buộc (Cờ Đỏ):
1. **Tắt tính năng chia sẻ của Editor:** Trưởng phòng Nhân sự phải chặn không cho phép các Editor khác thay đổi quyền truy cập hoặc chia sẻ file cho người mới.
2. **Chặn Viewer/Commenter tải xuống:** Khóa tính năng sao chép (Copy), in (Print), và tải xuống (Download) đối với tất cả tài khoản có quyền Viewer và Commenter.

---

## II. KỊCH BẢN XỬ LÝ SỰ CỐ: QUY TRÌNH 3 BƯỚC KHI RÒ RỈ DỮ LIỆU

Khi phát hiện một nhân viên vô tình chia sẻ link tệp với quyền **Editor** cho một ứng viên bên ngoài, quy trình ứng phó khẩn cấp 3 bước sau phải được kích hoạt lập tức:

### Bước 1: Cô lập và Thu hồi quyền truy cập tức thì (Revoke Access)
*   **Hành động:** Trưởng phòng Nhân sự (hoặc Quản trị viên hệ thống) truy cập ngay vào mục Chia sẻ (`Share`), tìm đến email của ứng viên bên ngoài hoặc cấu hình link công khai, chuyển trạng thái từ **Editor** sang **Remove Access** (Xóa quyền truy cập) và nhấn Lưu.
*   **Chặn truy cập diện rộng:** Nếu link được chia sẻ ở chế độ "Bất kỳ ai có link đều có quyền Editor", lập tức chuyển cấu hình link thành **Hạn chế (Restricted)** để vô hiệu hóa đường dẫn cũ ngay trong giây lát.

### Bước 2: Truy vết hành vi và Kiểm tra rò rỉ (Access Audit Log Investigation)
*   **Hành động:** Truy cập vào trình quản lý **Google Workspace Admin Console** (hoặc mục *Activity/Version History* của tệp).
*   **Kiểm tra lịch sử:** Rà soát nhật ký hoạt động của tệp trong khung thời gian từ lúc nhân viên gửi sai link đến lúc thu hồi:
    *   *Trường hợp 1 (An toàn):* Nhật ký hiển thị ứng viên **chưa mở file hoặc chỉ mới mở xem (View)** mà chưa có hành vi sao chép. Sự cố được kiểm soát thành công.
    *   *Trường hợp 2 (Rủi ro cao):* Nhật ký ghi nhận ứng viên đã thực hiện thao tác **Tạo bản sao (Make a copy)**, **Tải xuống (Download)** hoặc chỉnh sửa. Cần chụp lại màn hình lịch sử log để làm bằng chứng xử lý khủng hoảng.

### Bước 3: Đánh giá thiệt hại và Khắc phục lỗ hổng (Mitigation & Hardening)
*   **Xử lý hệ quả:** Nếu dữ liệu đã bị tải về (Trường hợp 2 ở Bước 2), bộ phận HR phối hợp cùng bộ phận Pháp lý liên hệ trực tiếp với ứng viên để yêu cầu cam kết bảo mật, yêu cầu xóa bỏ bản sao dựa trên các quy định pháp luật về bảo vệ dữ liệu cá nhân.
*   **Vá lỗi hệ thống:** 
    *   Tổ chức họp kiểm điểm, tái đào tạo nhân viên về "Quy tắc Cờ Đỏ Bảo mật".
    *   Chuyển toàn bộ danh sách ứng viên nhạy cảm vào **Bộ nhớ dùng chung (Shared Drive)** của doanh nghiệp để áp dụng chính sách chặn chia sẻ file ra bên ngoài tổ chức một cách tự động.
