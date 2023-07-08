# Serving static files in Express
Để cung cấp những file như images, css files, JS files ... sử dụng express.static (buil-in middleware function in Express) </br>
`express.static(root, [option])` </br>
root: chỉ định root directory mà ở đó cung cấp static asset </br>
[option]: static directory
VD:

           app.use(express.static('public'))
Bây giờ bạn có thể load file trong public directoty
           http://localhost:3000/images/kitten.jpg
           http://localhost:3000/css/style.css
           ...
Chú ý: Tên của static directory không phải là 1 phần của url

Để sử dụng nhiều static asset directories, thì gọi middleware express.static nhiều lần 

VD: Thay vì 'public' có thể gọi thêm 'files' chẳng hạn

           app.use(express.static('files'))

Chú ý: Path cung cấp cho express.static liên quan đến đường dẫn từ nơi mà bạn lauch ứng dụng node
Nếu bạn chạy express app từ một đường dẫn khác, thì sẽ an toàn hơn nếu như sử dụng đường dẫn tyệt đối (absolute path)
           const path = require('path')
           app.use(
                      '/static',
                      express.static(path.join(__dirname, 'public'))
           )
                      
