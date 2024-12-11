# [HawkeyeLab](https://cyberdefenders.org/blueteam-ctf-challenges/hawkeye/)
## ```Q1.How many packets does the capture have?```  
![image](https://github.com/user-attachments/assets/848f0b0b-b889-4b29-8dbc-16469cc19564)  
Sau khi mở file bằng Wireshark, ta có thể thấy số packet ở bên dưới góc phải màn hình.   
```Answer: 4003```  
## ```Q2.At what time was the first packet captured?```  
![image](https://github.com/user-attachments/assets/98ca4c36-ecae-43ff-9302-592fb3be52aa)
Sau khi sắp xếp cột TImes, ta có thể thấy thời gian gói tin đầu tiên được thu.  
```Answer: 2019-04-10 20:37:07 UTC```  
## ```Q3.What is the duration of the capture?```   
Tại ***Statistics/Capture file properties/Times***, ta có thể thấy được khoảng thời gian cách nhau giữa lúc thu được gói tin đầu tiên và gói tin cuối cùng.   
![image](https://github.com/user-attachments/assets/2c7445b5-f337-4e2e-8a1f-e1b6413e1bba)  
```Answer: 01:03:41```  
## ```Q4.What is the most active computer at the link level?```  
Tại ***Statistics/Endpoint***, ta có thể sắp xếp lại cột packet để tìm ra máy tính nào hoạt động nhiều nhất.  
![image](https://github.com/user-attachments/assets/f5893fb4-94ae-4f97-8a52-e401a22452f7)  
```Answer: 00:08:02:1c:47:ae```  
## ```Q5.Manufacturer of the NIC of the most active system at the link level?```  
Để tìm được nhà sản xuất, bạn có thể dùng mac address để tìm trên [Mac address lookup](https://macvendors.com/).  
![image](https://github.com/user-attachments/assets/58e14b8b-5d70-4b77-a3f2-ae94be40839d)  
```Answer: Hewlett-Packard```  
## ```Q6.Where is the headquarter of the company that manufactured the NIC of the most active computer at the link level?```  
Bạn cần tìm kiếm trụ sở chính của công ty bằng cách tìm kiếm nó trên **Google**.  
![image](https://github.com/user-attachments/assets/8b953667-8145-4432-b911-fc6c964b0c30)  
```Answer: Palo Alto```  
## ```Q7.The organization works with private addressing and netmask /24. How many computers in the organization are involved in the capture?```    
Tại ***Statistics/Endpoint/IPv4***, để tìm số máy tính của tổ chức làm việc với ```private addressing and netmask /24``` ta có thể dựa vào địa chỉ ip của nó có dạng: **```10.0.0.1 - 10.0.0.254```**  
![image](https://github.com/user-attachments/assets/2c26ac85-b247-4ae1-8b92-c8e2acce04a4)  
```Answer: 3```  
## ```Q8.What is the name of the most active computer at the network level?```   
Ta đã biết địa chỉ Mac của máy hoạt động năng suất nhất là ```00:08:02:1c:47:ae```, do đó ta sẽ sử dụng bộ lọc của Wireshark để lọc ra địa chỉ và tên của máy.  
```wireshark
eth.addr == 00:08:02:1c:47:ae && dhcp
```  
Ta có thể tìm được tên của máy trong phần **host name**.  
![image](https://github.com/user-attachments/assets/6f52d1d9-1622-467d-972a-54808158cc56)  
```Answer: Beijing-5cd1-PC```  
## ```Q9.What is the IP of the organization's DNS server?```  
Để tìm ip của DNS sever ta có thể dùng bộ lọc của Wireshark. bằng lệnh:  
```Wireshark
dns and dns.flags.response == 0
```
để lọc ra cái gói tin DNS và chỉ hiện thị các gói **```DNS Query```**.  
![image](https://github.com/user-attachments/assets/297ed6ee-2823-495f-b902-26c88a8d1313)  
Ta có thể thấy địa chỉ source: ```10.4.10.132``` là địa chỉ của thiết bị gửi yêu cầu DNS còn địa chỉ destination: ```10.4.10.4``` là địa chỉ ip của DNS sever được trả về để phân giải tên miền.  
```Answer: 10.4.10.4```  
## ```Q10.What domain is the victim asking about in packet 204?```  
Để tìm ra tên miền ở gói tin 204 ta cần lọc ra gói tin 204 trước tiên.   
```Wireshark
frame.number == 204
```
Sau khi lọc, ta có thể thấy trong phần **Domain name system (query)/Queries/proforma-invoices.com: type A, class IN** có chứa tên miền của gói tin là ```Name: proforma-invoices.com```    
![image](https://github.com/user-attachments/assets/87cd9fe5-02e7-4229-aa5c-5d2e714fcbf8)  
```Answer: proforma-invoices.com```    
##  ```Q11.What is the IP of the domain in the previous question?```  
Để tìm ip của tên miền trước đó, ta có thể dựa theo mô hình OSI và tìm trong các gói tin sau đó, địa chỉ của tên miền được tìm thấy ở gói tin **206**.  
![image](https://github.com/user-attachments/assets/3d733965-2779-4c9c-b9a0-f5d2d7c8bb74)  
Hoặc chúng ta có thể tìm kiếm luông UDP của gói tin **204** có chỉ số là 4  
![image](https://github.com/user-attachments/assets/8a266518-04ea-4b3b-8f86-84f84386f385)  
bằng lệnh:  
```Wireshark
udp.stream == 4
```
![image](https://github.com/user-attachments/assets/57058a3b-e26c-4fe2-af5a-e06199fdfb73)  
Trong đó ta cũng có thể thấy địa chỉ IP của tên miền trong phần ```Info``` của gói tin ***206***.  
```Answer: 217.182.138.150```  
## ```Q12.Indicate the country to which the IP in the previous section belongs.```  
Để tìm kiếm quốc gia của địa chỉ IP, ta có thể sử dụng [Geolocation service](https://www.geolocation.com/en_us?ip=217.182.138.150#ipresult).  
![image](https://github.com/user-attachments/assets/aff88c28-8b7b-43ef-9b0d-9f5b7072e8ac)  
```Answer: France``` ![image](https://github.com/user-attachments/assets/aef0a945-4905-4c05-9a75-f881ec118540)


















