# Serving static files in Express :woozy_face:
Để cung cấp những file như images, css files, JS files ... sử dụng express.static (buil-in middleware function in Express) </br>
</br>
`express.static(root, [option])` </br>
</br>
root: chỉ định root directory mà ở đó cung cấp static asset </br>
[option]: static directory </br>
VD: </br>

           app.use(express.static('public'))
Bây giờ bạn có thể load file trong public directoty </br>
           http://localhost:3000/images/kitten.jpg </br>
           http://localhost:3000/css/style.css </br>
           ... </br>
__Chú ý:__ Tên của static directory không phải là 1 phần của url </br>

Để sử dụng nhiều static asset directories, thì gọi middleware express.static nhiều lần </br>

VD: Thay vì 'public' có thể gọi thêm 'files' chẳng hạn </br>

           app.use(express.static('files'))

__Chú ý:__ Path cung cấp cho express.static liên quan đến đường dẫn từ nơi mà bạn lauch ứng dụng node </br>
Nếu bạn chạy express app từ một đường dẫn khác, thì sẽ an toàn hơn nếu như sử dụng đường dẫn tyệt đối (absolute path) </br>

           const path = require('path')
           app.use(
                      '/static',
                      express.static(path.join(__dirname, 'public'))
           )

# CreateWriteStream (write file theo luồng)
Option:

  encoding: <string> (default: utf8)
  autoClose: <boolen> (default: true)
  emitClose: <boolen> (default: true)
  start: <interger>
  
return: fs.WriteStream

`option` cũng có thể bao gồm `start` option để cho phép ghi data tại 1 số vị trí vào phần đầu của file. Chỉnh sửa file thay vì thay thế có thể yêu cầu `flags` `open` option đặt là r+ thay vì r như mặc định.
`encoding` có thể được chấp nhận bởi <Buffer>

Nếu như `autoClose` được set true on `'error'` hay `'finish'` bộ nhận diện file (file descriptor) sẽ được đóng tự động. Nếu set false file descriptor sẽ không đóng dù có lỗi. Đó là phản hồi đóng của application để chắc rằng không có bộ nhận diện file nào bị rò rỉ

Như mặc định luồng sẽ phát ra `'close'` event sau khi nó bị phá huỷ . Set the `emitClose` option về false để thay đổi điều đó

# fs.writeFile()

Sử dụng bất đồng bộ để viết data vào file. Như mặc định file sẽ bị replace nếu như đã tồn tại 

           fs.writeFile( file, data, options, callback ) 

__file:__ string, Buffer, url hay số nguyên miêu tả tệp (file description) biểu thị đường dẫn của file được viết. Sử dụng file descriptor sẽ làm cho hành động viết file giống như fs.write()

__data:__ string, Buffer, TypedArray hay DataView sẽ được viết vào file 
options: sting, object được sử dụng để chỉ định tham số tuỳ chọn (optional parameter) 

__options:__ string hay object chỉ định tham số tuỳ chọn sẽ ảnh hưởng đến đầu ra

           encoding: <string> (default: 'utf8')
           mode: <integer> (default: 0o666)
           flag: <string> (default: 'w')
           
__callback:__ function sẽ được gọi khi phương thức thực thi 

           err: throw error nếu như thất bại
           

