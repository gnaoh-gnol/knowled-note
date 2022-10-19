
## Khái niệm
- là một seach engine.
- được kế thừa từ Lucene Apache.
- hoạt động như một web server, có khả năng tìm kiếm nhanh chóng (realtime) thông qua giao thức RESTful.
- Có khả năng phân tích và thống kê dữ liệu.
- chạy trên server riêng và đồng thời giao tiếp thông qua RESTful do vậy nên không phụ thuộc vào client viết bằng gì hay hệ thông hiện tại được viết bằng ngôn ngữ gì giúp cho việc tích hợp vào hệ thống hiện tại khá dễ dàng, chỉ cần gửi http request lên và nhận về kết quả.
- là một hệ thống phân tán, thích hợp với tập data lớn, horizontal scalability. Chỉ cần add thêm node là ES sẽ auto scale cho bạn.
- là một open source phát triển bằng java.
- được sử dụng bởi nhiều hệ thống lớn: Wikimedia, Netflix, Adobe Systems, Facebook, Quora, Pixabay ...

## Ưu/ Nhược điểm của ES:
#### __Ưu điểm:
- Tìm kiếm dữ liệu rất nhanh chóng, mạnh mẽ dựa trên Apache Lucene (near-realtime searching).
- Có khả năng phân tích dữ liệu (Analysis data).
- Có khả năng mở rộng theo chiều ngang tốt (horizontal scalability).
- Hỗ trợ tìm kiếm mờ (fuzzy), tức là từ khoá tìm kiếm có thể bị viết sai lỗi chính tả hay không đúng cú pháp thì vẫn có khả năng search và trả về kết quả tốt.
- Hỗ trợ structured Query DSL (Domain-Specific Language), cung cấp việc đặc tả những câu truy vấn phức tạp bằng JSON.
- Hỗ trợ nhiều ES Client như: java, php, javascript, python, ruby, .net
#### __Nhược điểm:
- ES được thiết kế cho mục đích search, do vậy với những nhiệm vụ khác ngoài search như CRUD thì elastic kém thế hơn so với những DB khác như mongodb, mysql ... Do vậy ng ta ít dùng ES làm database chính, mà thường kết hợp nó với 1 DB khác.
- Trong ES không có khái niệm DB Transaction, tức là nó sẽ không đảm bảo được sự toàn vẹn giữ liệu trong các hoạt động Insert, Update, Delete. Tức là khi chúng ta thực hiện thay đổi nhiều bản ghi, nếu xảy ra lỗi thì sẽ làm cho logic bị sai hay dẫn tới mất mát dữ liệu. Đây cũng là 1 phần khiến ES không nên là DB chính.
- Không thích hợp với những hệ thống thường xuyên cập nhật dữ liệu. Vì sẽ rất tốt kém cho việc đánh index giữ liệu.