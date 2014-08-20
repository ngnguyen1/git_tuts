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
# Gửi commit trong nhánh master lên github. (Chúng ta sẽ tìm hiểu sau hơn về nhánh trong tuts lần sau.)
```
Bây giờ chúng ta có thể view file README.md trên Github Repo.

#### Fork a repository ####

Tại một thời điểm, chúng ta muốn phân phối project của ai đó, hay chúng ta muốn sử dụng project của một ai đố để bắt đầu. Điều này được định nghĩa là `forking`. Trong phần này, chúng ta sẽ forking một repo tên là awesome.

- Để forking một project, click vào button fork trong github repo.

![forking](https://raw.githubusercontent.com/NgaNguyenDuy/git_tuts/master/images/gitfork.png "Forking repo")

Sau khi fork một repo, tức là repo đó đã tồn tại trên github repo của chúng ta, chúng ta có thể clone repo đó về local repo. Sử dụng lệnh sau:
```
$ git clone https://github.com/your_username/awesome.git
# Clone repo mà chúng ta đã fork về github repo của mình vào thự mục hiện tại.
# your_username/awesome.git là repo chúng ta fork về, còn NgaNguyenDuy/awesome là repo gốc.
```

Khi một repo đã được clone, nó sẽ có một remote `origin` trỏ đến repo mà chúng ta fork về github của mình, chứ không phải là repo gốc. Để theo dõi (keep track) repo gốc mà đã fork, chúng ta cần add một remote khác có tên là `upstream`:
```
$ cd awesome

$ git remote add upstream https://github.com/NgaNguyenDuy/awesome.git
# Gán repo gốc vào một remote tên là upstream

$ git fetch upstream
```
> push: push thay đổi từ repository local lên repository server

> fetch: cập nhật thay đổi từ repository server về repository local

> pull/rebase: sao chép source code từ server về local workspace (tương đương checkout của SVN)

Như vậy chúng ta đã fork thành công một repo về local repo.
Chúng ta có thể làm gì tiếp theo:
- Sao chép những thay đổi ở repo gốc: `git fetch upstream`
- Nhóm bất kì điều gì thay đổi vào local repo: `git merge upstream/master`
- Sao chép tất cả commit từ repo gốc về local repo.

#### Làm việc với nhánh(brand)

Các nhánh (branches) được dùng để phát triển tính năng tách riêng ra từ những nhánh khác. Nhánh master là nhánh "mặc định" khi bạn tạo một repository. Sử dụng các nhánh khác tri đang trong giai đoạn phát triển và merge trở lại nhánh master một khi đã hoàn tất.

- Để xem toàn bộ nhánh của repo hiện tại:
`git branch -a`

- Để tạo một nhánh mới:
`git branch <branch-name>`

- Để chuyển brand: 
`git checkout <ten-nhanh>`

- Để nhập(merge) nhánh con vào nhánh hiện tại: 
`git merge <ten nhanh>`

Cơ bản về git có lẽ như vậy là ổn. Trong tuts sau, chúng ta sẽ đi sau hơn vào cách tạo và sử dụng nhánh, cách gửi pull request. Còn một phần nhỏ nữa là cách sử dụng submodule.
> Submodule cho phép chúng ta nhúng một repo vào trong repo chính của mình.
