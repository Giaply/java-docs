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
==> đúng: có thể sét theo cấu hình thời gian (7 ngày)

 - 1 consumer phải tự xóa message sau khi consume đi để tránh lặp message
=>  đúng
===> sai, consumer nó k tự xóa
 - 1 consumer phải chuyển message vào topic khác để xóa nó đi
 => sai 
 
##### NOTE:  Kafka  còn là một hệ thống có đặc tính "duribility" dữ liệu có thể được lưu trữ an toàn cho đến khi có consumer sẵn sàng nhận nó. 
Đáp án đúng là B. 1 message được lưu trữ đến khi hết thời gian lưu trữ theo cấu hình 
Message được lưu trữ đến khi hết thời gian trong cấu hình, consumer chỉ biết đến offset và phải tự handler trường hợp xử lý lặp lại message.
 
#### 5. Zookeepers có tác dụng lưu trữ gì với Kafka:
-  Record headers

-  Consumer logic

 - Access Control Lists

 - Broker SSL certificate: đúng

 - Cluster metadata: 
 
#### 6. Kafka convert object sang định dạng gì để truyền dữ liệu / quá trình convert này gọi là:
 - String / Encryption: đúng

 - Byte / Serialization

 - String / Externalization

 - Byte / Canonicalization
 
Đáp án đúng là Byte / Serialization, ở trong code Spring consumer lấy message ra là String là đã qua parser. Quá trình ngược lại từ byte convert ra object là deserialization

####  7. Message kafka được chia vào các topic dựa trên: key
####  8. Giả sử có 3 partition P1, P2, P3 và 1 consumer group gồm từ 1-4 consumer C1, C2, C3, C4. Cách xử lý nào sau đây có thể xảy ra:


- C1 đọc P1, C2 đọc P2, P3: đúng

 - C1 đọc P1, C2 đọc P2, C3 đọc P3: đúng

 - C1 đọc P1, C2 đọc P2, C3 C4 đọc P3: sai khi 2 consumer trong 1 group không đọc cùng 1 partition, đúng khi 1 trong 2 consumer (VD: C3 bị shutdown hoặc crash thì C4 sẽ thay thế)

 - C1 đọc P1, C2 đọc P2, C3 đọc P3, C4 không đọc gì: đúng
 #### 9. Cho 2 consumer C1, C2 và message M1. C1 vừa đọc M1, C2 có thể đọc M1 tiếp không, với điều kiện như thế nào?
 - có thể: 
 + consumer nằm trong 2 group khác nhau
 + 1 consumer bị shutdown hoặc crash

 #### 10. 1 message được ghi vào Kafka có thể sửa được không và sửa bởi ai như thế nào
 Không thể sửa 
 ( Có thể coi việc xóa topic, hay cấu hình thời gian lưu trữ để loại bỏ message chứ k sửa đc)
