# Unit test là gì 
unit test là phương pháp kiểm thử để đảm bảo cân nhắc tất cả các thành phần nhỏ nhất của phần mềm hoạt động đúng như mong đợi. Mục tiêu của unit test là xác định và sửa lỗi ở giai đoạn sớm nhất trong quá trình phát triển phần mềm, giúp giảm thiểu chi phí sửa lỗi và cải thiện chất lượng mã nguồn.

# Mục tiêu của unit test
Khi viết unit test, ta đang thực hiện đảm bảo rằng 1 hàm được expect phải hoạt động đúng và hoạt động trong tất cả các trường hợp.

Các unit test này đảm bảo rằng các code cũ đã được unit test vẫn hoạt động đúng khi có các thay đổi mới được thêm vào codebase.

# Phát triển theo hướng kiểm thử (TDD)
Phương pháp này có nghĩa là viết các unit test trước khi viết code thực tế. 

Điều này có nghĩa khi viết code thực tế, ta sẽ viết code để vượt qua các unit test đã viết trước đó.

Ngoài ra trong quá trình viết code, ta sẽ bắt gặp các trường hợp mà ta chưa nghĩ đến khi viết unit test, do đó ta sẽ viết thêm các unit test mới để bao phủ các trường hợp này.

Do đó, code sẽ solid hơn và đảm bảo rằng tất cả các trường hợp đều được kiểm tra. Điều này sẽ giảm thời gian thực hiện refactor code trong tương lai.

Trong đó, các từ khóa thường gặp khi áp dụng TDD là "Red", "Green", "Refactor".

Thực hiện theo chu trình:
1. Viết một unit test thất bại (Red) nhằm kiểm tra toàn bộ các trường hợp cần kiểm tra
2. Viết code để vượt qua unit test (Green) và đảm bảo tất cả các unit test đều thành công, trong quá trình này sẽ diễn ra việc viết thêm các unit test để bao phủ các trường hợp mới phát sinh
3. Refactor code để cải thiện chất lượng code mà không làm thay đổi hành vi (Refactor)

# Phát triển theo hướng kiểm thử ngược (BBD)
Phương pháp này tập trung vào việc viết các unit test dựa trên hành vi mong đợi của hệ thống. Thay vì chỉ kiểm tra các hàm riêng lẻ, BDD tập trung vào việc mô tả cách mà hệ thống nên hoạt động từ góc nhìn của người dùng cuối.

Trong đó các từ khóa thường gặp khi áp dụng BDD là "Given", "When", "Then". Chúng thường mang hơi hướng `semantics` hơn so với unit test truyền thống.

# Các lưu ý khi viết unit test
- Code duplication: Nên tránh việc lặp lại code trong các unit test. Ta có thể sử dụng các hàm helper để tái sử dụng code, điều này giúp giảm thiểu việc bảo trì code trong tương lai.
- Đối tượng thực hiện unit test: Nên để các developer viết unit test cho chính code của họ. Điều này giúp họ hiểu rõ hơn về code và đảm bảo rằng các unit test được viết đúng cách. Các hàm với các giá trị trả về phức tạp nên sử dụng các phương pháp khác ngoài unit test để kiểm thử.
- Independent: Mỗi unit test nên độc lập với nhau, không phụ thuộc vào trạng thái của các unit test khác. Điều này giúp đảm bảo rằng việc chạy một unit test không ảnh hưởng đến kết quả của các unit test khác.
- Coverage: Mục tiêu của unit test là bao phủ càng nhiều code càng tốt, tuy nhiên không nên quá chú trọng vào việc đạt được 100% coverage. Thay vào đó, nên tập trung vào việc kiểm tra các trường hợp quan trọng và các phần code có nguy cơ cao.
- Tên unit test: Nên đặt tên unit test một cách rõ ràng và mô tả chính xác mục đích của unit test. Tên unit test nên phản ánh hành vi mà nó đang kiểm tra.
- Tốc độ thực thi: Unit test nên được thiết kế để chạy nhanh chóng. Nếu một unit test mất quá nhiều thời gian để thực thi, nó có thể làm chậm quá trình phát triển và kiểm thử.
- Sử dụng mock và stub: Khi viết unit test, nên sử dụng các kỹ thuật như mock và stub để giả lập các phụ thuộc bên ngoài. Điều này giúp tập trung vào việc kiểm tra logic của hàm mà không bị ảnh hưởng bởi các yếu tố bên ngoài.