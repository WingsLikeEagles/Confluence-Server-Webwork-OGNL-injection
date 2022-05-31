# Confluence-Server-Webwork-OGNL-injection
  Object-Graph Navigation Language (OGNL) là một ngôn ngữ biểu thức nguồn mở dành cho Java. Thông thường, các biểu thức được các nhà phát triển sử dụng để tạo các trường động trong một ứng dụng. Ví dụ: tiêu đề của trang web có thể muốn được tạo động dựa trên người dùng hiện tại: OGNL mạnh mẽ và các biểu thức không bị giới hạn trong các ví dụ cơ bản như thế này. OGNL cũng cho phép thực thi bất kỳ loại Java nào trong biểu thức để cho phép các nhà phát triển xử lý nhiều hơn nữa. Khía cạnh nguy hiểm của OGNL là khi người dùng có thể kiểm soát biến được sử dụng trong biểu thức. Nếu kẻ tấn công có thể kiểm soát biến, chúng có thể đưa vào một biểu thức độc hại để máy chủ đánh giá. Trong trường hợp của Confluence, chúng có một số thông số ẩn mà người dùng cuối có thể kiểm soát khi POST các điểm cuối khác nhau.
  
  


  
 OGNL injection là lỗ hổng khá phổ biến mà các nhà phát triển nhận thức được và thường để giảm thiểu nó, trước tiên các nhà phát triển sẽ chuyển tất cả nội dung được đánh giá thông qua một danh sách đen (blacklist). Danh sách đen được sử dụng bởi Confluence đã kiểm tra xem có các lớp hoặc thuộc tính Java phổ biến mà kẻ tấn công sử dụng để thực thi mã hay không nhưng lại bỏ sót một số phương pháp nâng cao.
 Trình truy cập mảng có thể vượt qua danh sách đen của Confluence:
 
         queryString=aaa'+#{""["class"]}+'bbb
 Với việc bỏ qua danh sách đen, giờ đây họ có thể đưa vào bất kỳ mã Java nào mà máy chủ sẽ đánh giá. Ví dụ cuối cùng về payload có thể được đưa vào là:
 
       queryString=aaa
       #{
        ""["class"].forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec("/bin/bash -c ")
         }
         
      
   
   
