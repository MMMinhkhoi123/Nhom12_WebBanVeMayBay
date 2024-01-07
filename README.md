# Hướng dẫn cài đặt  web đặt vé máy bay
- CÀI MÔI TRƯỜNG CHẠY
  + Docker : (tại đây) https://docs.docker.com/desktop/install/windows-install/
- CÀI FILE DỮ LIỆU
  + (tại đây) https://drive.google.com/file/d/1bBFXp5RmF6TODnYjYyosqIuCZCT7mwqM/view?usp=sharing
- KIỂM TRA
  + sau khi tải xong tiến hành install docker vào máy.
    
    * kiểm tra bằng cú pháp :
    
          docker --version
    
   ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/7e554b92-a5aa-4a75-9d0a-4c6f8900b6af)
~~ lưu ý:  nhớ mở docker desktop để thực hiện các bước sau.
- KHỞI TẠO ỨNG DỤNG
  + Bước 1 : tạo một file ở một địa chỉ bất kỳ , sau đó bỏ  file (file dữ liệu ) vừa tải vào đó.
    * Vd : Tạo Thư mục WebFlight như sau.
    
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/2f0700bb-b26f-4d5b-ac6a-53d40be52b19)
      
  + Bước 2 : Mở  Command Prompt trỏ thẳng vào thử mục đã tạo trước đó
    * Vd : Làm như sau.
    
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/4daf8b43-1579-4f6b-a947-a5b44ffe152c)
      
  + bước 3: Gõ lệnh khởi tạo để chạy ứng dụng.
    
    * Cú pháp :

          docker-compose -f docker-compose.dev.yml up --build
      
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/c8158ac9-9e9d-4a8c-a461-c0f661cbedda)
    
    * Sau khi chạy hoàn tất.
      
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/432d066f-5023-46e6-86c3-00fb16e0f837)
      
    * Kiểm tra trong Docker desktop (Mục Container)
      
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/96600469-d173-4c21-9a17-7d29ef4694ae)
      
      ~~Lưu ý : springboot-container hiện đang off do bất đồng bộ trong sql khi khởi tạo lần đầu tiên, Chúng ta sẻ tiến hành mở springboot-container lên.
      
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/4134c5a3-456d-400d-af62-5b0e3caef452)
      ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/0c9721c7-39de-495d-a00f-11df232f4d25)
  
  + Bước 4: Cung cấp các dữ liệu cần có cho ứng dụng
  
     * Kiểm tra container bằng  Cú pháp sau:

           docker container ls
    
       ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/c3af683e-13be-46ad-933f-5f9f1a4efdd1)
       ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/76d8ad67-96b8-4b56-be39-4f0339c29228)
       
     * Mở liên kết mysql docker bằng  Cú pháp sau:

           docker exec -it [id-container-mysql] mysql -u root -p
       
       ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/a5d588cd-c09b-460b-ab77-012755091824)
       
       ~~Lưu ý : mã ***[id-container-mysql]*** là mã id-container-mysql của máy , tùy vào từng máy và thời gian chạy id khác nhau nên các bạn lưu ý thay đổi id-container-mysql theo máy của mình.
        
       ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/d3937411-d937-466e-b24d-20a0ebc621a0) <br>
       
       ~Các bạn lấy mã theo vị trí này: <br>
       
       ~Vd: mã là ***759c777f04fe*** thì  Cú pháp của bạn là :

           docker exec -it 759c777f04fe mysql -u root -p
    
    * Nhập mật khẩu để vào. Mật khẩu là : 123
    ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/62870696-0eed-4652-a45b-172088f2a755)
    ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/140db519-4ca6-499e-9638-2e8f7f39b1ae)
    * Sữ dụng databse flight bằng cú pháp sau :
      
          use flight
    
    ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/5dd78557-1677-4b29-9c34-d817fa893b89)
    * Thêm trường role vào bằng cú pháp sau :
    
          insert into role(name) values ("user"),("creater"),("checker");
    
    ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/7f74e753-7fd8-4e16-b796-592566d0caf2)
    * Thêm tài khoản quản lý bẳng cú pháp sau:
      
            INSERT INTO user (email,fullname,PASSWORD,phone,verify) 
            VALUES ("creater@gmail.com","Creater","Creater@123","0329999999",1),
                   ("checker@gmail.com","Checker","Checker@123","0329999999",1);
      
    ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/ebfbcaf5-b40d-43f2-85f0-35e8c969a605)
    * Cấp quyền cho tài khoản bằng cú pháp sau:
    
          INSERT INTO users_roles (user_id, role_id)  VALUES (1, 2),(2,3);
    
    ![image](https://github.com/MMMinhkhoi123/Nhom12_WebBanVeMayBay/assets/118420965/82c03031-fa03-4c4e-b6e6-e4642bcaf6fe)


# khác
- Link Tài khoản thanh toán : https://sandbox.vnpayment.vn/apis/vnpay-demo/
- Quản lý dữ liệu tốt hơn bằng hedisql (không bắt buộc): https://www.heidisql.com/download.php

***Lưu ý : Ứng dụng được đưa vào docker chưa test toàn bộ nên sẻ được cập nhập để hoàn thiện vào thời gian sau đó  .
# Chúc Các bạn Thành Công  .




