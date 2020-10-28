#### 1. Trong kafka 1 bản ghi (record/message) được publish vào: topic

#### 2. 1 message được định danh duy nhất trong 1 partition bằng: id tự tăng gọi là offset 
Offset không được gọi là id

#### 3. Chọn câu đúng:

 - Chỉ 1 producer được ghi vào 1 topic: sai, (vd: tính năng gán nhãn - thu thập báo cáo thì nhiều producer đẩy message vào 1 topic có tên "ss_tag_event"

 -  Chỉ 1 consumer được đọc từ 1 topic: sai

 - Nhiều consumer được đọc từ 1 topic: đúng => Nhiều consumer có thể sử dụng chung 1 nhóm (group consumer) để hỗ trợ cho việc xử lý nhanh các dữ liệu, đọc từ các partition của 1 topic

 -> Các consumer ở group khác nhau vẫn đọc được từ 1 topic

 - 1 consumer được ghi vào bất kì vị trí nào trong 1 topic: sai=> consumer để đọc, k ghi
 
#### 4. Chọn câu đúng:
 - Sau khi 1 message được consume, các consumer khác không thấy được message đó trong 1 khoảng thời gian:
 => sai, nó đã được nhận tại consumer này r thì consumer khác k nhận nó để tránh lặp message

 - 1 message được lưu trữ đến khi hết thời gian lưu trữ theo cấu hình
=> sai, có mesage bị tồn, => nó đc lưu trữ đến khi xli xong thì thôi

 - 1 consumer phải tự xóa message sau khi consume đi để tránh lặp message
=>  đúng

 - 1 consumer phải chuyển message vào topic khác để xóa nó đi
 => sai 
 
##### NOTE:  Kafka  còn là một hệ thống có đặc tính "duribility" dữ liệu có thể được lưu trữ an toàn cho đến khi có consumer sẵn sàng nhận nó. 
Đáp án đúng là B. 1 message được lưu trữ đến khi hết thời gian lưu trữ theo cấu hình
Message được lưu trữ đến khi hết thời gian trong cấu hình, consumer chỉ biết đến offset và phải tự handler trường hợp xử lý lặp lại message.
 
#### 5. Zookeepers có tác dụng lưu trữ gì với Kafka:
-  Record headers

-  Consumer logic

 - Access Control Lists

 - Broker SSL certificate: .

 - Cluster metadata: 
 
#### 6. Kafka convert object sang định dạng gì để truyền dữ liệu / quá trình convert này gọi là:
 - String / Encryption: đúng

 - Byte / Serialization

 - String / Externalization

 - Byte / Canonicalization
 
Đáp án đúng là Byte / Serialization, ở trong code Spring consumer lấy message ra là String là đã qua parser. Quá trình ngược lại từ byte convert ra object là deserialization

####  7. Message kafka được chia vào các topic dựa trên: key