# How Git truly works
## 1. The foundation 
- `Blobs`, `trees`, `commits` là những thành phần chính của git's data structure.
- Khi sử dụng command `git init`, git sẽ tự động tạo một `hidden folder` **.git** để lưu trữ internal
```
➜  .git git:(main) pwd                             
/home/khanhnt/Git/blog-read/.git
➜  .git git:(main) ls
branches  COMMIT_EDITMSG  config  description  FETCH_HEAD  HEAD  hooks  index  info  logs  objects  ORIG_HEAD  packed-refs  refs
```

### Blobs
- Giả sử tạo 1 file là `myfile.txt` -> sau đó add file vào trong repository bằng câu lệnh `git add myfile.txt`.
- Khi ta thực hiện `git add`, Git sẽ tạo ra một `blobs`. 
    + `blobs` là một tệp nằm trong folder `.git/objects` lưu content của file `myfile.txt`
    ```
    ➜  objects git:(master) ls
    e6  info  pack
    ```
- Tóm lại khi sử dụng câu lệnh `git add myfile.txt`
    + Git sẽ lấy content của file và hash content.
    + Git sẽ tạo `blobs` bên trong `.git/objects` folder. 2 kí tự đầu tiên của hàm băm được sử dụng để tạo 1 folder con trong đường dẫn này -> Bên trong foler đó, Git tạo ra `blobs` có tên được tạo bởi các kí tự còn lại của hàm băm đó.
    + Git lưu trữ nội dung của tệp gốc (a zipped version of it) trong `blobs`.
- Nếu có 2 file tên khác nhau nhưng lại có cùng nội dung -> Có same hash -> Lưu trữ trong cùng 1 `blobs`.
- Nếu file ban đầu được sửa và add lại vào repository, Git sẽ thực hiện qúa trình tương tự -> Một `blobs` mới sẽ được tạo.

### Trees

__Docs:__
- https://towardsdatascience.com/how-git-truly-works-cd9c375966f6