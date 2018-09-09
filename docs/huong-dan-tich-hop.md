# Hướng dẫn tích hợp lấy CDR, ghi âm, máy nhánh online

Ngoài việc sử dụng thư viện [JSSIP](http://jssip.net/) để lập trình điều khiển cuộc gọi. Tài liệu này sẽ giúp bạn lấy được thông tin chi tiết cuộc gọi \(CDR\), file ghi âm cuộc gọi, máy nhánh online.

#### **API end point**

 Tất cả các request được submmit thông qua base URL.

#### **HTTP Methods**

 Tất cả các request được submit thông qua phương thức HTTP POST, "Content-Type" cho phương thức POST là "application/x-www-form-urlencoded" và "application/json"

#### **Authentication**

 Tất cả các request đều yêu cầu giá trị cho tham số "**api\_key**" và **"api\_secret**", các giá trị này sẽ được ePacific cung cấp. 

## **1. Truy xuất dữ liệu CDR theo khoảng thời gian**

 Endpoint: **https://api.ccall.vn/cdrs/json**

### **Cấu trúc submit request\_data \(JSON Encoded\):**

![](.gitbook/assets/api-submission.png)

#### **Mô tả fields**

 **api\_key, api\_secret** \(Bất buộc\) : ePacific sẽ cung cấp cặp key này cho khách hàng

 **param\(s\)** : date\_range, hangup\_cause, source, destination, cid\_name, direction, page, limit

 Ví dụ:

date\_range: **"date\_range" : { "from" : "", "to" : "" }** có format là "YYYY-MM-DD HH:mm"

cid\_name: **"Thanh Nguyen"**

source: **"1001"**

destination: **"1005"**

hangup\_cause: **"NORMAL\_CLEARING"** 

direction: có 3 giá trị tương ứng là “**inbound**”, “**outbound**” và “**local**” \(Nếu trong cấu trúc submit không có param này, hệ thống sẽ truy vấn dựa vào cả 3 giá trị\)

page: **1** \(số trang hiện tại\)

limit: **50** \(số dòng cho một trang\)

### **Cấu trúc response data \(JSON Encoded\):**

#### Không phân trang

![](.gitbook/assets/api-nonpage.png)

#### Có phân trang

![](.gitbook/assets/api-paging.png)



#### **Mô tả fields**

 "**direction**" : hướng cuộc gọi

 "**cid\_name**" : Caller name, tên người dùng tương ứng với extension

 "**source**" : Caller number \(Extension\)

 "**destination**" : Destination number \(Extension\)

 "**recording**" : Hyperlink dùng để tải file ghi âm

 "**start**" : Thời gian bắt đầu thực hiện cuộc gọi

 "**tta**" : Time to Answer, thời điểm destination trả lời tính từ thời gian bắt đầu cuộc gọi \(= giây\)

 "**duration**" : Khoảng thời gian thoại \(có format theo hh:mm:ss\)

 "**pdd**" : Post Dial Delay 

 "**mos**" : Mean Opinion Score 

 "**status**" : Hangup cause

**“paging”:** thông tin về phân trang

**"txtdesc":** một chuỗi mô tả ngắn gọn

**"page\_current":** số trang hiện tai đang chọn

**"limit":** số dòng giới hạn cho 1 trang

**"record\_count":** tổng số dòng

**"page\_count":**  tổng số trang

**"prev\_page":** trang trước \(true là có trang trước, ngược lại là false\) 

**"next\_page":** trang sau \(true là có trang sau, ngược lại là false\)

**Danh sách giá trị Hangup cause:**

| NORMAL\_CLEARING ORIGINATOR\_CANCEL BLIND\_TRANSFER LOSE\_RACE NO\_ANSWER NORMAL\_UNSPECIFIED NO\_USER\_RESPONSE NO\_ROUTE\_DESTINATION SUBSCRIBER\_ABSENT NORMAL\_TEMPORARY\_FAILURE ATTENDED\_TRANSFER PICKED\_OFF USER\_BUSY CALL\_REJECTEDINVALID\_NUMBER\_FORMAT | NETWORK\_OUT\_OF\_ORDER DESTINATION\_OUT\_OF\_ORDER RECOVERY\_ON\_TIMER\_EXPIRE MANAGER\_REQUEST MEDIA\_TIMEOUT UNALLOCATED\_NUMBER NONE EXCHANGE\_ROUTING\_ERROR ALLOTTED\_TIMEOUT CHAN\_NOT\_IMPLEMENTED INCOMPATIBLE\_DESTINATION USER\_NOT\_REGISTERED SYSTEM\_SHUTDOWN MANDATORY\_IE\_MISSING |
| :--- | :--- |


## **2. Truy xuất dữ liệu CDRs theo “Call ID”**

### **Cấu trúc submit request\_data \(JSON Encoded\):**

![](.gitbook/assets/api-callid.png)

### **Cấu trúc response data \(JSON Encoded\):**

![](.gitbook/assets/api-callid-re1.png)

## **3. Lấy danh sách Extension đang Registered \(Online\):** 

 Endpoint: **https://api.ccall.vn/ext\_reg/json**

### **Cấu trúc submit request\_data \(JSON Encoded\):**

![](.gitbook/assets/api-ext.png)

#### **Mô tả fields**

 **api\_key, api\_secret** \(Bất buộc\) : ePacific sẽ cung cấp cặp key này cho khách hàng

### **Cấu trúc response data \(JSON Encoded\):**

![](.gitbook/assets/api-ext-online.png)

**Mô tả**

 Ví dụ trong hệ thống có 6 Extension từ 100 đến 106. Sau khi gọi API kết qua trả về như trong hình trên là hiện tại có 2 Ext đang online là 100 và 101 





Hãy liên lạc với chúng tôi qua số điện thoại: **1900 1563** hoặc qua email: **support@epacific.com.vn** để được tư vấn chi tiết.

