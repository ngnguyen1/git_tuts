## Hướng dẫn sử dụng git trên Linux & Window ##

### Nội dung: ###

* Setup git
* Create a repository
* Fork a repository

### Để cài đặt git: ###
  * Linux: Cài đặt qua command line (tùy vào từng distro): `sudo apt-get install git`
  * Windows: Download và cài đặt github for window: [Github for window](https://github-windows.s3.amazonaws.com/GitHubSetup.exe "Github for Window")


#### Setup Git ####

Sau khi đã cài đặt thành công, bây giờ là lúc để chúng ta cấu hình git. Để làm điều này, chúng ta cần mở terminal ( trên linux) hay GitBash (trên windows).

- Username
```
$ git config --global user.name "Your name here"
```

- Email: Git lưu địa chỉ email vào những commit mà chúng ta tạo. Chúng ta sử dụng địa chỉ email để liên kết các commit của bản thân với tài khoản github.
```
$ git config --global user.email "your_email@example.com"
```
Email của chúng ta phải giống với email đăng kí tài khoản github. Nếu không, có thể tham khảo ở [đây](https://help.github.com/articles/how-do-i-change-my-primary-email-address).

Nếu như muốn ghi đè cấu hình cho từng repo, chúng ta có thể cd vào repo muốn cấu hình rồi sử dụng lệnh git config mà không có option --global.

Ngoài ra còn một số thiết lập khác tùy vào từng mục đích sử dụng nhưng editor, hay merge tool.

Sau khi cấu hình, chúng ta có thể sử dụng lệnh `git config --list` để kiểm tra cấu hình đã thiết lập ở trên. Hoặc cũng có thể sử dụng editor để View file ~/.gitconfig (trên Linux) hay .gitconfig trong thư mục $HOME/%USERPROFILE% trên môi trường windows.

#### Create a repository ####
Để tạo môt repo trên github:
* Đầu tiên chúng ta phải tạo một repo trên server của github. Click vào Create new repo ở gác trên bên phải của github, điền đầu đủ thông tin và click Create new repo.
* Sau khi đã tạo một repo trên github, chúng ta phải tạo một thư mục có tên giống hệt với tên repo trên Server git. Hãy xem ví dụ sau:
```
$ mkdir ~/Hello-World
# Với Hello-World chính là tên repo mà chúng ta đã tạo trên github.

cd ~/Hello-World

git init
# Thiết lập những file cần thiết cho git
# Khởi tạo một Git repo rỗng bên trong thư mục .git

touch README.md
# Tạo một file README.md trong thự mục Hello-World
```
Sử dụng lệnh `git add README.md` để theo dõi tệp tin.
Sau đó commit file: `git commit -m "first commit"`.
Chúng ta có thể suy nghĩ commit giống như là trạng thái của toàn bộ project - code, file, mọi thứ tại một thời điểm cụ thể.
Good, mọi thứ đã hoàn thành trên local repo của chúng ta. Để kết nối từ local repo đến github account, chúng ta phải thiết lập một remote cho repo và push các commit lên đó.
> Một remote là một repo được lưu trữ trên một máy tính khác, trong trường hợp này là Github's Server. Git support multiple remote, điều này thường được sử dụng khi forking một repository.

Tham khảo đoạn mã sau:
```
$ git remote add origin https://github.com/username/Hello-World.git
# Tạo một remote tên là 'origin' đến Github repo của chúng ta.

$ git push orgin master.
# Gửi commit trong nhánh master lên github.
```
#### Fork a repository ####
