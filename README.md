# BÀI LÀM: THIẾT KẾ BACKLOG CHO TÍNH NĂNG THEO DÕI CHUYẾN GHÉP (RIKKEIGO)

---

## PHẦN 1: THIẾT KẾ KIẾN TRÚC BACKLOG (EPIC → FEATURE → USER STORY)

### 1. Sơ đồ phân cấp dạng cây (Tree Structure)

* **[EPIC] Minh bạch tiến trình đón & Hỗ trợ sự cố chuyến ghép theo thời gian thực**
  * **[FEATURE 1] Trực quan hóa thứ tự đón/trả và thời gian xe đến (ETA)**
    * US-01: Xem thứ tự đón trả của các điểm trên lộ trình
    * US-02: Xem thời gian đếm ngược (ETA) đến lượt đón của mình
  * **[FEATURE 2] Kênh liên lạc và xử lý tình huống phát sinh trên tuyến**
    * US-03: Gọi hoặc nhắn tin trực tiếp với tài xế ngay trên màn hình đón
    * US-04: Báo sự cố trễ giờ và yêu cầu điều phối xe thay thế

---

### 2. Chi tiết 4 User Story (Chuẩn 3 vế: As a... / I want... / So that...)

* **US-01**: **Là** một hành khách đi xe ghép, **tôi muốn** nhìn thấy rõ xe đang ở điểm nào, đang đón ai và tôi là điểm đón thứ mấy, **để** tôi không bị hoang mang và biết chính xác thời điểm cần ra cửa chờ xe.
* **US-02**: **Là** một hành khách đi xe ghép, **tôi muốn** biết thời gian dự kiến đón (ETA) được cập nhật liên tục theo tình hình kẹt xe thực tế, **để** tôi chủ động sắp xếp công việc cá nhân, không phải đứng đợi ngoài đường vô ích.
* **US-03**: **Là** một hành khách đi xe ghép, **tôi muốn** có nút bấm để gọi điện hoặc nhắn tin nhanh cho tài xế ngay trong app, **để** tôi dặn tài xế điểm đón cụ thể hoặc hỏi lý do khi thấy xe dừng lại quá lâu.
* **US-04**: **Là** một hành khách đi xe ghép, **tôi muốn** có nút báo khẩn cấp khi tài xế trễ quá 15 phút, **để** hệ thống đổi ngay xe khác cho tôi hoặc cho tôi hủy chuyến miễn phí nếu lỡ việc gấp.

---

## PHẦN 2: THỨ TỰ ƯU TIÊN VÀ PHÂN TÍCH THEO D.E.E.P

### 1. Thứ tự ưu tiên trong Product Backlog (Sắp xếp từ trên xuống dưới)

| Hạng | Mã Story | Tên User Story | Mức ưu tiên | Lý do ưu tiên |
| :---: | :---: | :--- | :---: | :--- |
| **1** | **US-01** | Xem thứ tự đón trả của các điểm trên lộ trình | **Cao nhất (Top 1)** | Đánh trúng nỗi bức xúc lớn nhất của khách: "Không biết xe đang đón ai, bao giờ tới mình". Biết được vị trí của mình trên tuyến là giải tỏa tâm lý ngay. |
| **2** | **US-02** | Xem thời gian đếm ngược (ETA) theo giờ thực | **Cao (Top 2)** | Đi kèm với US-01. Có thứ tự rồi thì cần thêm con số phút cụ thể để khách căn giờ ra điểm hẹn chuẩn xác. |
| **3** | **US-03** | Kênh liên lạc trực tiếp với tài xế | **Trung bình (Top 3)** | Công cụ giúp hai bên tự xử lý nhanh các lệch pha nhỏ về vị trí mà chưa cần làm phiền đến tổng đài. |
| **4** | **US-04** | Báo sự cố trễ giờ & yêu cầu đổi xe | **Thấp nhất (Top 4)** | Xử lý kịch bản ngoại lệ (Edge case/Exception). Tần suất phát sinh ít hơn hành vi theo dõi xe hàng ngày. |

---

### 2. Phân tích User Story cần làm chi tiết nhất theo nguyên tắc D.E.E.P

* **Story cần làm chi tiết nhất:** **US-01 (Xem thứ tự đón trả của các điểm trên lộ trình)**.
* **Giải thích theo D.E.E.P:**
  * **Detailed Appropriately (Chi tiết phù hợp):** Trong Backlog, thứ gì nằm sát đỉnh danh sách (chuẩn bị đưa vào Sprint tới để làm) thì phải được mổ xẻ kỹ lưỡng nhất. US-01 phải có đầy đủ bản vẽ UI/UX (hiển thị danh sách điểm đón dạng timeline hay map marker), logic chuyển trạng thái điểm đón, và bộ Acceptance Criteria rõ ràng để dev bắt tay vào code được ngay, không phải ngồi đoán.
  * Ngược lại, các Story nằm phía dưới (như US-03, US-04) chỉ cần mô tả ở mức tổng quan (Coarse-grained). Không nên tốn công viết quá chi tiết từ đầu vì trong quá trình làm US-01 và US-02, phản hồi thực tế từ người dùng có thể làm thay đổi hoàn toàn cách thiết kế tính năng liên lạc hay cứu hộ (**Emergent**).

---

## PHẦN 3: XỬ LÝ RỦI RO & BẪY TIẾN ĐỘ THỰC TẾ

### 1. Tình huống 1: Burndown Chart đi ngang 3 ngày liền do đối tác chậm giao API bản đồ

* **Dấu hiệu nhận biết:**
  * **Trên biểu đồ Sprint Burndown:** Đường công việc thực tế còn lại (Remaining Work) không chúi xuống mà **nằm ngang một đường thẳng tắp suốt 3 ngày**, bay cao hơn hẳn so với đường lý tưởng (Ideal Guideline).
  * **Trong buổi họp Daily Scrum:** Dev phụ trách ngày nào cũng chỉ lặp lại đúng một câu: *"Em xong khung giao diện rồi nhưng vẫn đang đợi bên đối tác cấp key/tài liệu API bản đồ nên chưa map được dữ liệu"*, khiến Story bị kẹt cứng, không đẩy sang cột *Done* được.
* **Ai xử lý:** **Scrum Master (chủ trì)**, phối hợp cùng **Product Owner (Đức)** và **Developers**.
* **Cách xử lý cụ thể:**
  1. **Scrum Master:** Xác định đây là vật cản bên ngoài (Impediment). SM phải trực tiếp liên hệ, thúc ép đầu mối kỹ thuật của bên bản đồ hoặc nhờ quản lý cấp trên can thiệp để lấy API sớm nhất.
  2. **Developers:** Không ngồi chơi đợi đối tác. Nhóm tự tạo dữ liệu giả lập (**Mock API / Stub Data**) dựa trên cấu trúc đã bàn thảo để ghép giao diện và test logic luồng đi trước. Khi có API thật từ đối tác chỉ việc thay endpoint là xong.
  3. **Product Owner (Đức):** Nếu sự cố kéo dài sang ngày thứ 4 và đe dọa trực tiếp tới mục tiêu Sprint (Sprint Goal), Đức sẽ họp khẩn với team để cắt bớt các phần phụ thuộc sâu vào bản đồ sang Sprint sau, đồng thời kéo các Story độc lập khác từ Product Backlog vào làm bù để tận dụng năng lực của nhóm.

---

### 2. Tình huống 2: PO muốn "nhét" nguyên cả Epic vào Sprint Backlog để "làm một lần cho xong"

* **Ai xử lý:** **Scrum Master** và **Đội ngũ phát triển (Developers)** cùng ngồi lại với Đức.
* **Cách xử lý cụ thể:**
  1. **Scrum Master kéo Đức về nguyên tắc cốt lõi của Scrum:**
     * Nhắc Đức rằng Sprint Backlog chỉ nhận các User Story đã được làm mịn, có tiêu chí rõ ràng (**Definition of Ready**) và có kích thước vừa vặn (**Small** theo INVEST) để gói gọn trong một Sprint.
     * Cả một Epic là một khối lượng công việc quá lớn và ẩn chứa nhiều rủi ro. Nếu cố nhét hết vào, team sẽ làm dở dang mỗi thứ một tí, cuối Sprint không có bất kỳ tính năng nào đạt chuẩn hoàn chỉnh (**Definition of Done**) để chạy thử hoặc demo cho ban lãnh đạo.
  2. **Developers và PO cùng chốt lại phạm vi khả thi:**
     * Đội ngũ đưa ra con số năng lực thực tế (Sprint Velocity) của mình.
     * Thuyết phục Đức chỉ chọn **1 hoặc 2 Story có giá trị cao nhất** (chẳng hạn **US-01** và **US-02** dùng dữ liệu Mock) đưa vào Sprint này. 
     * Cách làm này giúp team chắc chắn giao được một phiên bản chạy mượt mà ngay cuối Sprint để khách hàng dùng thử, còn các tính năng liên lạc hay cứu trợ (**US-03**, **US-04**) sẽ đưa vào các Sprint tiếp theo dựa trên dữ liệu sử dụng thực tế.