## **ĐẠI HỌC BÁCH KHOA HÀ NỘI** 

**==> picture [89 x 134] intentionally omitted <==**

## **BÁO CÁO ĐỒ ÁN I** 

**HỆ THỐNG QUẢN LÝ THIẾT BỊ HỌC TẬP HUST Equipment Management System (HUST EMS)** 

## **Mục lục** 

PHẦN MỞ ĐẦU...............................................................................................................................3 CHƯƠNG 1. THU THẬP YÊU CẦU..............................................................................................4 1.1. Các yêu cầu thu thập được.....................................................................................................4 1.1.1. Yêu cầu chức năng..........................................................................................................4 1.1.2. Yêu cầu về người dùng hệ thống.....................................................................................4 1.1.3. Yêu cầu phi chức năng....................................................................................................5 1.1.4. Yêu cầu về dữ liệu...........................................................................................................5 1.2. Biểu đồ use case.....................................................................................................................5 1.2.1. Biểu đồ use case tổng quát..............................................................................................5 1.2.2. Biểu đồ use case phân rã.................................................................................................7 CHƯƠNG 2. PHÂN TÍCH.............................................................................................................12 2.1. Các thẻ CRC.........................................................................................................................12 2.2. Biểu đồ lớp........................................................................................................................... 13 2.3. Biểu đồ tuần tự.....................................................................................................................14 2.4. Phân tích dữ liệu...................................................................................................................15 2.4.1. Xác định các thực thể và thuộc tính..............................................................................15 

2.4.2. Mô hình thực thể và liên kết..........................................................................................16 CHƯƠNG 3. THIẾT KẾ HỆ THỐNG...........................................................................................17 3.1. Kiến trúc tổng quan của hệ thống.........................................................................................17 3.2. Kiến trúc phần mềm.............................................................................................................18 3.3. Thiết kế cơ sở dữ liệu...........................................................................................................18 3.3.1. Chuyển Mô hình thực thể & liên kết sang Mô hình quan hệ........................................18 3.3.2. Sơ đồ ERD.....................................................................................................................19 3.4. Thiết kế giao diện.................................................................................................................19 CHƯƠNG 4. TRIỂN KHAI VÀ KIỂM THỬ................................................................................23 4.1. Các công nghệ sử dụng........................................................................................................ 23 4.2. Sản phẩm phần mềm............................................................................................................23 4.3. Kiểm thử...............................................................................................................................23 PHẦN KẾT LUẬN......................................................................................................................... 25 

## **PHẦN MỞ ĐẦU** 

Trong bối cảnh giáo dục đại học ngày càng phát triển, việc quản lý thiết bị và dụng cụ học tập tại các phòng thí nghiệm, phòng thực hành trở thành một bài toán quan trọng. Đại học Bách Khoa Hà Nội với hàng chục phòng thí nghiệm và hàng nghìn thiết bị cần được quản lý hiệu quả, minh bạch và chính xác. 

Hệ thống Quản lý Thiết bị Học tập (HUST EMS) được xây dựng nhằm giải quyết các vấn đề: theo dõi tình trạng thiết bị, quản lý phiếu mượn/trả, kiểm soát trả chậm và cung cấp báo cáo thống kê cho ban quản lý nhà trường. 

Mục tiêu của đồ án: 

- Xây dựng hệ thống quản lý thiết bị học tập hoàn chỉnh cho Đại học Bách Khoa Hà Nội 

- Áp dụng phương pháp phân tích và thiết kế hướng đối tượng (OOAD) trong quá trình phát triển 

- Triển khai hệ thống với công nghệ hiện đại: Spring Boot WebFlux, PostgreSQL, ReactJS 

- Tự động hóa quy trình kiểm soát mượn/trả và thông báo trả chậm 

Phạm vi hệ thống: Quản lý thiết bị, phiếu mượn/trả, tài khoản người dùng và thống kê dashboard cho các phòng thí nghiệm tại ĐHBKHN. 

## **CHƯƠNG 1. THU THẬP YÊU CẦU** 

## **1.1. Các yêu cầu thu thập được** 

## **1.1.1. Yêu cầu chức năng** 

Hệ thống cần đáp ứng các yêu cầu chức năng sau: 

## **a) Quản lý tài khoản và phân quyền:** 

- Quản trị viên tạo tài khoản cho cán bộ, giảng viên, sinh viên (không cho tự đăng ký) 

- Phân quyền theo nhóm quyền (role): Quản trị viên, Giảng viên, Sinh viên, Quản lý kho 

- Kích hoạt/tạm ngưng tài khoản, đổi mật khẩu 

## **b) Quản lý thiết bị:** 

- CRUD thiết bị: thêm, sửa, xóa, xem danh sách thiết bị 

- Phân loại thiết bị theo device_type (loại thiết bị) 

- Theo dõi số lượng tồn kho (quantity), vị trí (location), trạng thái hoạt động 

- Tìm kiếm và lọc thiết bị theo tên, mã, loại, trạng thái 

## **c) Quản lý phiếu mượn/trả:** 

- Tạo phiếu mượn thiết bị theo tiết học (borrow_period, return_period) 

- Duyệt phiếu mượn: chưa duyệt / đã duyệt / hủy 

- Ghi nhận trả thực tế, tính số phút trả chậm tự động (late_minutes) 

- Đánh dấu phiếu mất thiết bị (status = 4) 

- Lọc phiếu theo trạng thái, ngày, người mượn 

## **d) Thông báo tự động:** 

- Hệ thống tự động quét phiếu trả chậm mỗi 2 phút 

- Gửi thông báo đến đúng người mượn khi trả chậm 

- Quản lý danh sách thông báo: đọc/chưa đọc, đánh dấu tất cả đã đọc 

- Hiển thị badge số thông báo chưa đọc trên giao diện 

## **e) Dashboard thống kê:** 

- Tổng quan hệ thống: đầu thiết bị, tổng số lượng, lượt mượn, lượt mất, số giảng viên, sinh viên 

- Top 5 thiết bị được mượn nhiều nhất (biểu đồ cột ngang) 

- Thống kê phiếu mượn theo trạng thái (biểu đồ tròn donut) 

- Xu hướng lượt mượn theo ngày/tuần/tháng (biểu đồ đường) 

- Phân bố lượt mượn theo loại thiết bị (biểu đồ donut) 

- Top người mượn nhiều nhất, lọc theo vai trò Sinh viên / Giảng viên 

## **1.1.2. Yêu cầu về người dùng hệ thống** 

Hệ thống phục vụ 4 nhóm người dùng: 

|**Vai trò**|**Số lượng ước tính**|**Chức năng chính**|
|---|---|---|
|Quản trị viên|2-5 người|Quản lý toàn bộ hệ thống, tài khoản, nhóm quyền,<br>duyệt phiếu|
|Quản lý kho|5-10 người|Quản lý thiết bị, phiếu mượn/trả, xử lý trả chậm|
|Giảng viên|~184 người|Tạo phiếu mượn, xem lịch sử mượn trả cá nhân|
|Sinh viên|~2.640 người|Tạo phiếu mượn, xem thông báo, lịch sử cá nhân|



## **1.1.3. Yêu cầu phi chức năng** 

- Hiệu năng: API phản hồi dưới 500ms với tải thông thường; hệ thống xử lý concurrent requests nhờ Spring WebFlux (non-blocking) 

- Bảo mật: Xác thực JWT, phân quyền theo role, mật khẩu mã hóa BCrypt 

- Khả dụng: Hệ thống hoạt động 24/7, job scheduled chạy đúng timezone Asia/Ho_Chi_Minh 

- Khả năng mở rộng: Kiến trúc Clean Architecture, dễ thêm module mới 

- Giao diện: Responsive, tương thích trình duyệt hiện đại, tông màu BKHN (đỏ #C8102E, trắng) 

- Dữ liệu: Soft delete (cột deleted), audit trail (createdBy, modifiedBy, createdDate, modifiedDate) 

## **1.1.4. Yêu cầu về dữ liệu** 

- Thiết bị: lưu đủ thông tin mã, tên, loại, số lượng, vị trí, mô tả, trạng thái 

- Phiếu mượn: lưu người mượn, thiết bị, tiết mượn/trả, thời gian thực tế, phút trả chậm, trạng thái duyệt 

- Người dùng: username duy nhất, mật khẩu hash, vai trò, thông tin liên lạc 

- Thông báo: gắn với user_id cụ thể, lưu trạng thái đọc/chưa đọc, ref_id để điều hướng 

- Tiết học: bảng class_periods lưu giờ bắt đầu/kết thúc từng tiết để tính trả chậm 

- Tất cả bảng kế thừa BaseEntity: id (UUID), createdDate, modifiedDate, deleted, createdBy, modifiedBy 

## **1.2. Biểu đồ use case** 

## **1.2.1. Biểu đồ use case tổng quát** 

Hệ thống HUST EMS có 4 tác nhân chính tương tác với các nhóm chức năng: 

- Quản trị viên: Quản lý tài khoản, nhóm quyền, xem dashboard, duyệt phiếu 

- Quản lý kho: Quản lý thiết bị, phiếu mượn/trả, xử lý trả chậm, xem dashboard 

- Giảng viên: Tạo phiếu mượn, xem lịch sử, nhận thông báo 

- Sinh viên: Tạo phiếu mượn, xem lịch sử cá nhân, nhận thông báo 

_[Biểu đồ use case tổng quát — xem hình vẽ đính kèm]_ 

**==> picture [183 x 691] intentionally omitted <==**

**----- Start of picture text -----**<br>
Hé théng HUST EMS<br>CCéu hinh mugn tra ><br>“Quan ly tiét hoc><br>(xem dashboard >)<br>___théngké_<br><Thém thiét bi ><br>5 Sta thiét bi ><br>© Xba thiétbi ><br>O| —_Xemthiét danh bi sach >)<br>fe ee<br>Admin van hanh Yam phiéu mugn<br>| \_(toan hé théng)7<br>ee<br>© Quan ly tai khoan>><br>| CQuan ly nhém quyén<br>© xem lich str tac vu ><br>C Tao phiéu mugn_><br>q<| — Gi mat khdu_><br><]<br>g ~ Tra phiéu muon><br>f “\ a<br>Ngudi dung ° Xem phiéu mugn >)<br>N= ban than<br>t<br>Sinh vién<br>I<br>Giang vién<br>**----- End of picture text -----**<br>


## **1.2.2. Biểu đồ use case phân rã** 

## **Bảng mô tả Use Case — UC01: Đăng nhập hệ thống** 

|**Bảng mô tả Use Case — UC01: Đăng nhập hệ thống**|**Bảng mô tả Use Case — UC01: Đăng nhập hệ thống**|
|---|---|
|**Tên UC**|UC01 — Đăng nhập hệ thống|
|**Tác nhân**|Tất cả người dùng (Quản trị viên, Giảng viên, Sinh viên)|
|**Mô tả**|Người dùng nhập tên đăng nhập và mật khẩu để truy cập hệ thống|
|**Điều kiện tiên quyết**|Tài khoản đã được Quản trị viên tạo sẵn và có trạng thái hoạt động|
|**Luồng chính**|1. Người dùng truy cập trang đăng nhập<br>2. Nhập username và password<br>3. Hệ thống xác thực thông tin<br>4. Hệ thống trả về JWT token<br>5. Điều hướng đến Dashboard|
|**Luồng thay thế**|3a. Sai username/password → hiển thị thông báo lỗi, yêu cầu nhập lại<br>3b. Tài khoản tạm ngưng → thông báo tài khoản bị khóa<br>3c. Không kết nối server → thông báo lỗi kết nối|
|**Kết quả**|Người dùng đăng nhập thành công, có JWT token hợp lệ|



**Bảng mô tả Use Case — UC02: Tạo phiếu mượn thiết bị** 

|**Tên UC**|UC02 — Tạo phiếu mượn thiết bị|
|---|---|
|**Tác nhân**|Giảng viên, Sinh viên|
|**Mô tả**|Người dùng tạo phiếu mượn thiết bị theo tiết học cụ thể|
|**Điều kiện tiên quyết**|Đã đăng nhập; thiết bị còn số lượng trong kho (quantity > 0)|
|**Luồng chính**|1. Chọn thiết bị cần mượn<br>2. Chọn tiết mượn và tiết trả<br>3. Nhập số lượng cần mượn<br>4. Xác nhận tạo phiếu<br>5. Hệ thống sinh mã phiếu và lưu (approve_status = 0 — chưa duyệt)|
|**Kết quả**|Phiếu mượn được tạo, chờ quản lý duyệt|



_[Biểu đồ use case]_ 

## **Bảng mô tả Use Case — UC03: Duyệt phiếu mượn** 

|**Tên UC**|UC03 — Duyệt phiếu mượn|
|---|---|
|**Tác nhân**|Quản trị viên, Quản lý kho|
|**Mô tả**|Quản lý xem xét và duyệt hoặc hủy phiếu mượn của người dùng|
|**Điều kiện tiên quyết**|Phiếu mượn tồn tại với approve_status = 0 (chưa duyệt)|
|**Luồng chính**|1. Xem danh sách phiếu mượn chưa duyệt<br>2. Xem chi tiết phiếu<br>3. Chọn Duyệt (approve_status = 1) hoặc Hủy (approve_status = 2)<br>4. Hệ thống ghi lại approved_by và approved_date|
|**Luồng thay thế**|3a. Hủy phiếu → phiếu chuyển sang trạng thái hủy, thiết bị không bị trừ số<br>lượng|
|**Kết quả**|Phiếu mượn được duyệt hoặc hủy, có ghi nhận người duyệt và thời gian|



_[Biểu đồ use case]_ 

**Bảng mô tả Use Case — UC04: Ghi nhận trả thiết bị** 

**Tên UC** UC04 — Ghi nhận trả thiết bị 

|**Tác nhân**|Quản lý kho|
|---|---|
|**Mô tả**|Ghi nhận thời điểm thực tế người dùng trả thiết bị, tính phút trả chậm|
|**Điều kiện tiên quyết**|Phiếu mượn có status = 1 (đang mượn) hoặc status = 3 (trả chậm)|
|**Luồng chính**|1. Tìm phiếu mượn theo mã hoặc người mượn<br>2. Ghi nhận actual_return_date = thời điểm hiện tại<br>3. So sánh với giờ kết thúc tiết return_period trong class_periods<br>4. Nếu trả đúng giờ: status = 2; nếu trễ: status = 3, tính late_minutes<br>5. Lưu phiếu|
|**Luồng thay thế**|4a. Thiết bị bị mất → quản lý đánh dấu status = 4 (mất thiết bị)|
|**Kết quả**|Phiếu mượn được cập nhật trạng thái trả, số lượng thiết bị được hoàn lại|



_[Biểu đồ use case]_ 

## **Bảng mô tả Use Case — UC05: Xem dashboard thống kê** 

|**Bảng mô tả Use Case — UC05: Xem dashboard thống kê**|**Bảng mô tả Use Case — UC05: Xem dashboard thống kê**|
|---|---|
|**Tên UC**|UC05 — Xem dashboard thống kê|
|**Tác nhân**|Quản trị viên, Quản lý kho|
|**Mô tả**|Xem tổng quan hệ thống và các biểu đồ thống kê|
|**Điều kiện tiên quyết**|Đã đăng nhập với quyền xem dashboard|
|**Luồng chính**|1. Truy cập trang Dashboard<br>2. Chọn khoảng thời gian (fromDate, toDate)<br>3. Hệ thống hiển thị: 6 card tổng quan, biểu đồ cột top 5 thiết bị, biểu đồ tròn<br>trạng thái, biểu đồ đường xu hướng, biểu đồ donut loại thiết bị, bảng top người<br>mượn<br>4. Lọc theo Sinh viên / Giảng viên / Tất cả cho top người mượn|



|**Luồng thay thế**|3a. Không có dữ liệu trong khoảng thời gian → hiển thị 0 / danh sách rỗng|
|---|---|
|**Kết quả**|Hiển thị đầy đủ thống kê theo khoảng thời gian đã chọn|



_[Biểu đồ use case]_ 

## **CHƯƠNG 2. PHÂN TÍCH** 

## **2.1. Các thẻ CRC** 

Thẻ CRC (Class – Responsibilities – Collaborators) mô tả các lớp chính trong hệ thống: 

|**Class**|**Responsibilities**|**Collaborators**|
|---|---|---|
|**UserEntity**|- Lưu thông tin tài khoản<br>- Xác thực đăng nhập<br>- Gắn nhóm quyền<br>- Quản lý trạng thái hoạt động|RoleEntity,<br>LoanEntity,<br>NotificationEntity|
|**RoleEntity**|- Định nghĩa nhóm quyền<br>- Gắn với người dùng<br>- Liên kết với quyền hạn qua<br>bảng trung gian|UserEntity|
|**PermissionEntity**|- Lưu thông tin quyền hạn<br>- Phân nhóm theo group_id<br>- Kiểm soát quyền truy cập<br>API/chức năng|RolePermissionEntity|
|**RolePermissionEntity**|- Liên kết nhóm quyền với<br>quyền hạn (N-N)<br>- Xác định danh sách quyền của<br>từng role|RoleEntity, PermissionEntity|
|**DeviceEntity**|- Lưu thông tin thiết bị<br>- Theo dõi số lượng tồn kho<br>- Phân loại theo device_type<br>- Quản lý trạng thái hoạt động|LoanEntity, DeviceTypeEntity|
|**DeviceTypeEntity**|- Lưu danh mục loại thiết bị<br>- Chuẩn hóa phân loại thiết bị|DeviceEntity|
|**LoanEntity**|- Tạo phiếu mượn/trả<br>- Theo dõi tiết mượn/trả<br>- Tính phút trả chậm<br>- Quản lý trạng thái phiếu<br>- Đánh dấu mất thiết bị|UserEntity,<br>DeviceEntity,<br>ClassPeriodEntity,<br>NotificationEntity|
|**LoanConfigEntity**|- Lưu cấu hình ngưỡng trả chậm<br>- Cung cấp tham số<br>late_threshold_minutes cho job<br>tính trễ|LoanEntity|
|**NotificationEntity**|- Lưu thông báo trả chậm - Gắn<br>với user_id cụ thể - Theo dõi<br>trạng thái đọc - Tham chiếu loan<br>qua ref_id|UserEntity LoanEntity|
|**ClassPeriodEntity**|- Lưu thông tin tiết học - Cung<br>cấp giờ bắt đầu/kết thúc - Làm<br>cơ sở tính trả chậm|LoanEntity|
|**TaskHistoryEntity**|- Lưu lịch sử tác vụ hệ thống||



- Ghi nhận nội dung công việc đã thực hiện - Phục vụ tra cứu/audit 

## **2.2. Biểu đồ lớp** 

Biểu đồ lớp thể hiện quan hệ giữa các lớp nghiệp vụ chính: 

- UserEntity (N) ←→ (1) RoleEntity: Nhiều người dùng thuộc một nhóm quyền 

- RoleEntity (N) ←→ (N) PermissionEntity: Một nhóm quyền có nhiều quyền hạn, 

- qua bảng trung gian RolePermissionEntity 

- UserEntity (1) ←→ (N) LoanEntity: Một người dùng có nhiều phiếu mượn 

- DeviceEntity (1) ←→ (N) LoanEntity: Một thiết bị có thể có nhiều phiếu mượn 

- ClassPeriodEntity (1) ←→ (N) LoanEntity: Một tiết học tham chiếu trong nhiều phiếu 

- (dùng 2 lần: borrow_period và return_period) 

- LoanEntity (1) ←→ (N) NotificationEntity: Một phiếu mượn có thể sinh nhiều thông báo 

- UserEntity (1) ←→ (N) NotificationEntity: Một người dùng nhận nhiều thông báo 

_[Biểu đồ lớp — xem hình vẽ đính kèm]_ 

## **2.3. Biểu đồ tuần tự** 

Biểu đồ tuần tự cho luồng Tạo phiếu mượn và Kiểm tra trả chậm tự động: 

## **Luồng 1: Tạo phiếu mượn** 

- Người dùng → FE: Điền form tạo phiếu mượn 

- FE → BE (POST /loan/create): Gửi request kèm Authorization header 

- BE → JWT Filter: Xác thực token, lấy userId 

- BE → DeviceRepository: Kiểm tra số lượng thiết bị còn đủ 

- BE → LoanRepository: Lưu phiếu mượn với approve_status = 0 

- BE → FE: Trả về phiếu mượn đã tạo 

**==> picture [445 x 325] intentionally omitted <==**

**----- Start of picture text -----**<br>
Biểu đồ tuần tự: Tạo phiếu mượn<br>Người dùng FE (React) BE (Spring) Database JWT Filter<br>asec<br>Điền form tạo phiếu<br>POST /loan/create + JWT<br>Xác thực JWT token<br>userId hợp lệ<br>Kiểm tra quantity thiết bị<br>Còn đủ số lượng<br>INSERT loan (status=1, approve=0)<br>Lưu thành công<br>Response: phiếu mượn + mã phiếu<br>Hiển thị thành công<br>[alt] Không đủ số lượng<br>Kiểm tra quantity<br>400: Không đủ số lượng<br>Hiển thị lỗi<br>**----- End of picture text -----**<br>


## **Luồng 2: Job tự động kiểm tra trả chậm (mỗi 2 phút)** 

- ScheduledJob → LoanRepository: Query loans status=1, borrow_date hôm nay 

- ScheduledJob → ClassPeriodRepository: Lấy giờ kết thúc tiết return_period 

- ScheduledJob: So sánh giờ hiện tại với end_time 

- Nếu trễ → LoanRepository: Cập nhật status=3, tính late_minutes 

- ScheduledJob → NotificationRepository: Kiểm tra đã có thông báo cho loan này chưa 

- Nếu chưa → NotificationRepository: Insert thông báo với user_id = borrower_id 

_[Biểu đồ tuần tự — xem hình vẽ đính kèm]_ 

Biểu đồ tuần tự: Job quét trả chậm (mỗi 2 phút) 

**==> picture [451 x 295] intentionally omitted <==**

**----- Start of picture text -----**<br>
@Scheduled Job LoanRepository PeriodRepository NotifRepository FE Polling<br>= = = as<br>cron: 0 */2 * * * *<br>Query loans status=1, hôm nay<br>Danh sách phiếu đang mượn<br>Lấy end_time của return_period<br>end_time tiết học<br>[if] now > end_time → trả chậm<br>UPDATE status=3, late_minutes<br>OK<br>Kiểm tra notif đã tồn tại (ref_id)?<br>Chưa có → cho phép insert<br>= INSERT notification (user_id=borrowerId)<br>Lưu thành công<br>GET /notifications (2 phút/lần)<br>|<br>= ) Danh sách + unreadCount<br>Hiện badge 🔔<br>**----- End of picture text -----**<br>


## **2.4. Phân tích dữ liệu** 

## **2.4.1. Xác định các thực thể và thuộc tính** 

|**Thực thể**<br>~~a~~<br>~~ee~~|**Thuộc tính chính**<br>~~ee~~|**Ghi chú**<br>~~ee~~<br>~~ee~~|
|---|---|---|
|**users**<br>~~a~~<br>~~ee~~|id, username, password, full_name,<br>phone_number, email, position,<br>status, role_id<br>~~ee~~|status: 1=hoạt động, 2=tạm ngưng<br>~~ee~~<br>~~ee~~|
|**role**|id, name|VD: Quản trị viên, Giảng viên, Sinh<br>viên|
|**devices**|id, name, device_code, device_type,<br>status, location, quantity, description|status: 1=hoạt động, 0=ngưng|
|**loans**|id, loan_code, borrower_id,<br>device_id, quantity, borrow_date,<br>borrow_period, return_period,<br>actual_return_date, status, note,<br>late_minutes, approve_status,<br>approved_by, approved_date|status: 1=đang mượn, 2=đã trả, 3=trả<br>chậm, 4=mất approve_status: 0=chưa<br>duyệt, 1=đã duyệt, 2=hủy|
|**notifications**|id, title, message, type, ref_id,<br>user_id, is_read|type: LATE_RETURN, LOST ref_id:<br>loan_id|
|**class_periods**|id, period_number, start_time,|Tiết 1-10, lưu giờ bắt đầu/kết thúc|



end_time 

Lưu ý: Tất cả bảng đều kế thừa BaseEntity với các cột: id (UUID), created_date, modified_date, created_by, modified_by, deleted (soft delete). 

## **2.4.2. Mô hình thực thể và liên kết** 

   - users (N) — thuộc về — (1) role 

   - role (N) — có — (N) permission [qua bảng trung gian role_permission] 

   - users (1) — tạo — (N) loans 

   - devices (1) — được mượn trong — (N) loans 

   - loans (N) — tham chiếu tiết — (1) class_periods [borrow_period] 

   - loans (N) — tham chiếu tiết — (1) class_periods [return_period] 

   - loans (1) — sinh ra — (N) notifications 

   - users (1) — nhận — (N) notifications 

- _[Sơ đồ ERD — xem hình vẽ đính kèm]_ 

## **CHƯƠNG 3. THIẾT KẾ HỆ THỐNG** 

## **3.1. Kiến trúc tổng quan của hệ thống** 

Hệ thống HUST EMS được xây dựng theo mô hình Client-Server 3 tầng: 

- Tầng Presentation (FE): ReactJS — giao diện web người dùng, tông màu BKHN (đỏ/trắng), responsive 

- Tầng Application (BE): Spring Boot WebFlux — xử lý nghiệp vụ, REST API, nonblocking I/O 

- Tầng Data: PostgreSQL — lưu trữ dữ liệu, JPA/Hibernate ORM 

Giao tiếp: FE gọi BE qua RESTful API với JSON, xác thực bằng JWT Bearer Token trong Authorization header. 

## **3.2. Kiến trúc phần mềm** 

Backend áp dụng Clean Architecture với các tầng: 

|**Tầng**|**Package**|**Vai trò**|
|---|---|---|
|Controller|*.controller|Nhận request HTTP, gọi Service, trả<br>Mono<Response<T>>|
|Service|*.service|Xử lý nghiệp vụ, validation, orchestration|
|Repository|*.repository|Truy vấn DB qua JPA, custom @Query<br>JPQL/native SQL|
|Entity|*.domain.entity|Mapping bảng DB, kế thừa BaseEntity|
|DTO|*.dto.response|Data Transfer Object, Response wrapper<br>chung Response<T>|
|Scheduled|*.scheduler|Job tự động: quét trả chậm, gửi thông báo<br>(mỗi 2 phút)|



Frontend áp dụng cấu trúc phân tầng: 

- pages/: Các trang chính (Dashboard, DanhSachTaiKhoan, NhomQuyen, HoSo...) 

- components/: Component tái sử dụng (MainLayout, NotificationBell, HustLogo...) 

- services/: Axios instance, API calls (authService, notificationService...) 

- context/: Global state (AuthContext — lưu user, token) 

- hooks/: Custom hooks (useNotifications — polling thông báo mỗi 2 phút) 

## **3.3. Thiết kế cơ sở dữ liệu** 

## **3.3.1. Chuyển Mô hình thực thể & liên kết sang Mô hình quan hệ** 

- users(id, username, password, full_name, phone_number, email, position, status, role_id, created_date, modified_date, created_by, modified_by, deleted) 

- role(id, name, created_date, modified_date, created_by, modified_by, deleted) 

- devices(id, name, device_code, device_type, status, location, quantity, description, created_date, modified_date, created_by, modified_by, deleted) 

- loans(id, loan_code, borrower_id, device_id, quantity, borrow_date, borrow_period, return_period, actual_return_date, status, note, late_minutes, approve_status, approved_by, approved_date, created_date, modified_date, created_by, modified_by, deleted) 

- notifications(id, title, message, type, ref_id, user_id, is_read, created_date, modified_date, created_by, modified_by, deleted) 

- class_periods(id, period_number, start_time, end_time, created_date, modified_date, created_by, modified_by, deleted) 

## **3.3.2. Sơ đồ ERD** 

_[Sơ đồ ERD chi tiết — xem hình vẽ đính kèm]_ 

## **3.4. Thiết kế giao diện** 

Hệ thống gồm các màn chính: 

|**Màn hình**|**Mô tả**|**Route**|
|---|---|---|
|Đăng nhập|Form đăng nhập, logo BKHN, nền đỏ<br>gradient, animation particles|/login|
|Dashboard|6 stat card, 5 biểu đồ thống kê, filter theo<br>ngày|/dashboard|
|Danh sách tài khoản|Bảng tài khoản, filter, thêm/sửa/xóa,<br>toggle trạng thái|/tai-khoan/danh-sach|
|Danh sách thiết bị|Xem danh sách thiết bị đã được thêm vào<br>hệ thống|/thiet-bi|
|Tạo phiếu mượn|Giảng viên/sinh viên chọn thiết bị cần|/phieu-muon-tra|



||mượn, số lượng và thời gian cần trả||
|---|---|---|
|Tổng hợp phiếu mượn|Danh sách phiếu mượn trả của giảng<br>viên / sinh viên|/tong-hop-phieu-muon-tra|



Thiết kế chung: Sidebar thu gọn được, topbar với chuông thông báo polling 2 phút, tông màu đỏ BKHN (#C8102E), font Be Vietnam Pro + Playfair Display. 

_[Hình chụp màn hình sản phẩm — xem Chương 4]_ 

**==> picture [461 x 595] intentionally omitted <==**

**----- Start of picture text -----**<br>
aioe<br>BACH KHOA |<br>Hé thong Quan ly Thiét bi & Dung cu Hoc tap<br>7 | Dang nha<br>Meme © Hé théng quanly thiét bi hoc tap<br>TEN DANG NHAP<br>MAT KHAU<br>eeoeeeeee<br>>) Dang nhaép<br>Hé théng chi danh cho can bé duge cap tai khod<br>Lién hé quan tri vién néu can hé tr¢<br>| HUST EMS = 2°@ admin L<br>89 Dashboard<br>Quan Ly<br>Titngay Dénngay<br>@ Quanlythiét bi Té hé thér<br>ong quaning ong 05/17/2026 O 06/17/2026 8<br>@) Phiéu mugn tra<br>) Téng hgp phiéu mugn tra r \ 7 \ 7 \<br>HE THONG yy 3 = 14 8 15<br>& Danh sach tai khodn : ‘<br>O  Nhém quyén —_—FSO FSO———<br>& Théng tin tai khodn \ 1 © 1 2 1<br>CAu HiNH HE THONG 0 202 K 5<br>&} Cau hinh mugn tré<br>@_ Cau hinh logi thiét bi Top 5 thiét bi duge mugn nhiéu nhat Théng ké phiéu mugn theo trang thdi<br>© Danh sach tiét hoc Diéu khién diéu hoa<br>—<br>—EE<br>**----- End of picture text -----**<br>


**==> picture [462 x 442] intentionally omitted <==**

**----- Start of picture text -----**<br>
| HUST EMS = a 6 eamin)<br>TONG QUAN Danh séchcA taipay khoanPu + Thémtaiat khodn<br>98 Dashboard<br>Quan@ LY Tén dang nhap Email Sé dién thogi Trang thdi<br>Quanly thiét bi Nhép tén dang nhap Nhap email Nhdp SBT. Tat cd Xéabé loc<br>@) Phiéu mugn tra<br>) Téng hgp phiéu mugn tra<br>{Tai khodn (3)<br>HE THONG<br>STT Tén TK Ho tén Email Nhém quyén Chute vu SBT Ngay tao Ngay sita Ngudi tao<br>2, Danh séch tai khoan<br>0© Nhém3 quyén“ giangvient GidngviénA —_ giangvien@gmail.com Gidng vién Giang vién 09784636464 Admin<br>& Théngtin tai khoan admin2. DatNguyén- —_dati610@gmail.com Sinh vién; admin aaa 03837411117 Admin<br>CAu HINH HE THONG<br>& Céu hinh mugn tra admin Admin Dat@gmail.com admin Admin hé thong 0369726374<br>@ Céuhinhlogi thiét bi 7 4<br>© Danh sach tiét hoc $6 dong/trang: | 10 Téng3 taikhoan<br>qa HUST EMS = Q ra ] admin V<br>TONG ‘QUAN pin Bieta ie!fa pNe - ;<br>Quan ly thiét bi & Nhap Excel & Xuét Excel + Thém thiét bi<br>88 Dashboard<br>Quan LY<br>@ Quanly thiét bi MG thiét bi Tén thiét bi Logi thiét bi Trang thai<br>Nh@p ma thiét bi Nhap tén thiét bi. Tat ca Tat ca Q Timkiém X6a bé loc<br>@) Phiéu mugn tra<br>@) Téng hgp phiéu mugn tra<br>Thiétbi (4)<br>HE THONG<br>sTT Ma thiét bi Tén thiét bi Logi Vi tri/Phong $6 lugng Ngay nhaép Ngudi nhaép Trang thai Me ta Thao tac<br>& Danh sdch tai khoan<br>6 cements TBOO4 Mic gidng vién Diéukhién —_kithudt 15 Admin Mic gidng vién Gow<br> Théngtin tai khoan TBO3 Diéukhiénpo the: diguhdace oe —_-Bigukhién_— 1 Admin = Gow<br>cAu HINH HE THONG<br>> Céuhinh mugn tra TBO2 Laptop May tinh D1 1 Admin GzD Bow<br>@ Céuhinhlogi thiét bi :<br>TBO1 May chiéut May chigu DSI 12 Admin May chiéut Gila<br>© Danh sach tiét hoc<br>. $6 dong/trang: | 10 Téng4 thiét bi<br>py admin<br>**----- End of picture text -----**<br>


**==> picture [461 x 483] intentionally omitted <==**

**----- Start of picture text -----**<br>
Tao phiéuen  muon<br>[Thiét bi* $6 ludng<br>Tim va chon thiét bi... Vv 1<br>Tiétree  mugn Tiétree  tra2.<br>S6 tiét S6 tiét<br>Ghi chu<br>Ghi chu<br>Za<br>Huy2 Tao phiéu«af<br>Y{ | HUST EMS = ree= 1 Ce aeim nQuandm i tri vién &<br>Téngr¢ hop phiéuon  mugn tra2 & Xudt Exeel<br>"9 Dashboard Theo déi tat cd phiéu mugn, tra thiét bi ctia todn bé ngudi ding trong hé théng.<br>Ma phiéu mugn. Tén nguéi mugn Trang thdi<br>@ Quan ly thiét bi ; ane<br>Nhap ma phiéu... Nhép tén... Tat ca x v<br>© Phiéumugn tra Trang thai duyét Tungay Dénngay<br>(©) Téng hop phiéu mugn tra Tat ca xv mm/dd/yyyy a mm/dd/yyyy a X6a bé loc<br>&, Danh sdéch tai khodn Téng hop phiéu mugn tra (15)<br>O  Nhém quyén a Théi gian mugn Tiét mugn Tiét tra Thdi gian tra thuc té Trang thai Trang thai duyét Tra cham (phut) Ghi chi Ngay cap nhat Thao tae<br>omibeng tinecikbodn 17:00 16/06/2026 10 n Tracham Cha duyét 1893 = 17:04 16/06/2026 Gp<br>10:42 16/06/2026 2 3 = Tra cham DG duyét 2348 = 13:52 16/06/2026<br>8} Cau hinh mugn tré<br>10:40 16/06/2026 2 3 = Tré cham Da hay 2348 = 13:52 16/06/2026<br>@ Cau hinh logi thiét bi<br>© Danhisach tiéthoc 09:50 16/06/2026 1 z = Tra cham Ché duyét 2403 a 09:51 16/06/2026<br>09:48 16/06/2026 2 3 = Tra cham Ché duyét 2348 = 09:49 16/06/2026<br>A admin<br>Rainalnno inane a a wine ac Anan Anand nInainnne QE<br>**----- End of picture text -----**<br>


## **CHƯƠNG 4. TRIỂN KHAI VÀ KIỂM THỬ** 

## **4.1. Các công nghệ sử dụng** 

|**Nhóm**|**Công nghệ**|**Phiên bản / Mô tả**|
|---|---|---|
|Backend|Java|Java 21 — LTS, hỗ trợ Virtual Threads|
||Spring Boot|3.x với WebFlux (Project Reactor, Netty) — non-<br>blocking reactive|
||Spring Data JPA|Hibernate ORM, custom JPQL và native SQL<br>queries|
||Spring Security|JWT authentication, BCrypt password encoding|
||Spring Scheduler|@Scheduled cron job kiểm tra trả chậm mỗi 2 phút|
|Database|PostgreSQL|Quan hệ, ACID, UUID primary key, soft delete|
|Frontend|ReactJS 18|SPA, React Router v6, Context API|
||Axios|HTTP client, interceptor tự động gắn JWT token|
||Chart.js|Biểu đồ: line, bar, doughnut cho dashboard|
|DevOps|Docker|Container hóa BE, FE (Nginx), PostgreSQL|
|Build|Maven|Build tool cho Spring Boot|
||npm|Package manager cho ReactJS|



## **4.2. Sản phẩm phần mềm** 

Hệ thống HUST EMS bao gồm các module hoàn chỉnh: 

- Module xác thực: Đăng nhập JWT, phân quyền theo role, bảo vệ route 

- Module quản lý tài khoản: CRUD tài khoản, nhóm quyền, thông tin cá nhân, đổi mật khẩu 

- Module quản lý thiết bị: CRUD thiết bị, tìm kiếm, lọc theo loại/trạng thái 

- Module phiếu mượn/trả: Tạo phiếu, duyệt phiếu, ghi nhận trả, tính trả chậm 

- Module thông báo: Job tự động 2 phút, polling FE, badge chuông, toast thông báo mới 

- Module dashboard: 5 loại biểu đồ, 6 stat card, filter theo thời gian và vai trò 

## **4.3. Kiểm thử** 

Phương pháp kiểm thử: 

|**Loại kiểm thử**|**Công cụ**|**Phạm vi**|
|---|---|---|
|Unit Test|JUnit 5, Mockito|Service layer: tính late_minutes, format label<br>trend, xử lý date range|



|API Test|Swagger UI, Postman|Tất cả endpoints: authentication, CRUD,<br>dashboard APIs|
|---|---|---|
|Integration Test|Spring Boot Test, H2|Repository queries, Scheduled job, JWT filter|
|Manual Test|Trình duyệt|Luồng đăng nhập, tạo phiếu, duyệt phiếu,<br>thông báo polling|



Kết quả kiểm thử: 

- Tất cả API trả về đúng format Response<T> với status code và message tiếng Việt 

- Job quét trả chậm hoạt động đúng timezone Asia/Ho_Chi_Minh (cron zone) 

- Thông báo không bị trùng lặp nhờ kiểm tra ref_id + user_id trước khi insert 

- Dashboard thống kê chính xác khi filter theo fromDate/toDate 

- Giao diện responsive trên màn hình desktop và tablet 

## **PHẦN KẾT LUẬN** 

Đồ án đã xây dựng thành công Hệ thống Quản lý Thiết bị Học tập (HUST EMS) cho Đại học Bách Khoa Hà Nội với đầy đủ các chức năng theo yêu cầu đặt ra. 

Kết quả đạt được: 

- Áp dụng thành công phương pháp phân tích và thiết kế hướng đối tượng (OOAD): use case, CRC, biểu đồ lớp, biểu đồ tuần tự, ERD 

- Xây dựng backend với Spring Boot WebFlux — kiến trúc reactive, non-blocking, hiệu năng cao 

- Xây dựng frontend ReactJS với UI/UX chuyên nghiệp, tông màu chuẩn BKHN 

- Tự động hóa kiểm soát trả chậm với @Scheduled job và hệ thống thông báo realtime polling 

- Dashboard thống kê đa chiều với 5 loại biểu đồ phục vụ ra quyết định quản lý 

- Triển khai với Docker + Docker Compose, cấu hình timezone chính xác 

## Hướng phát triển: 

- Thêm module báo cáo xuất Excel/PDF cho ban quản lý 

- Tích hợp FCM push notification cho ứng dụng mobile 

- Xây dựng thêm tính năng đặt lịch mượn trước 

- Tối ưu hiệu năng với Redis cache cho các API dashboard 

- Bổ sung module quản lý phòng thí nghiệm và lịch sử bảo trì thiết bị 

