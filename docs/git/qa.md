---
sidebar_position: 3
---

# Q & A

**1. Lúc commit rồi mà phát hiện ra commit đó sai quá sai thì phải undo hay xóa cái commit đó ra sao?**

**2. Muốn quay lại commit thứ N thì làm sao?**

=> 3 cách thường dùng: Reset, Revert, -amend

**Reset**

```
git reset --hard HEAD^
```

- Ở đây có vài điểm cần lưu ý
  - `HEAD^` có ý nghĩa giống với `HEAD~` hay `@^`, nghĩa là quay về trước **1 commit**
  - Muốn quay về trước **n commit**, VD 5 commit thì có thể thay bằng `HEAD~5`.
  - `--hard` có nghĩa là bỏ commit đi và **bỏ cả những thay đổi chưa được commit trong working space**. Khi này môi trường sẽ hoàn toàn “sạch sẽ” như thời điểm trước khi commit.
  - `--soft` có nghĩa là bỏ commit đi nhưng **giữ nguyên những thay đổi chưa được commit trong working space**. `--soft` hữu dụng khi bạn muốn giữ lại những thay đổi chưa commit cho lần commit tiếp theo

**Revert**

```
git revert (commit_hash)
```

**-amend**

```
git commit --amend

# Đây là commit sai / thiếu
git add home.php
git commit -m 'Add home'

# Nhận ra là add thiếu 1 file home.css và muốn thêm vào commit bên trên
git add home.css
git commit --amend --no-edit
```

**3. Tôi đang chưa hiểu rõ sự khác biệt giữa `git merge` và `git rebase` là gì?**

**4. Tại sao tôi lại dùng git rebase mà không phải merge trong dự án này?**

**5. git rebase nó hay bị nhiều conflict hơn git merge?**

**6. git merge dễ tra log hơn git rebase đúng không vì rebase sửa log lại hết rồi  ?**

=> Lý do áp dụng rebase trong dự án là cho mọi thứ đều dễ dàng xem, điều tra log khi xem qua transport plan trong git. Chính vì thế việc áp dụng rebase cho từng brach riêng biệt là cách để cac developer có tư duy logic tốt log một cách có hệ thống những commit thực sự quan trọng và cần thiết để tra cứu sau này hạn chế commit spam ngoài ý muốn.

Việc conflict trong git là điều không thể tránh khỏi khi merge hay rebase branch khác mà làm chung trên 1 file, *mình chưa thấy dẫn chứng nào là rebase conflict nhiều hơn merge*

**7. Trước khi commit mới thì mình phải pull code mới về, mà nếu gặp conflict thì phải xử lý, nếu xử lý ko khéo thì mất code của mình làm, vậy phải làm sao đây?**
**8. Nếu chỉ backup 1 lần cho 1 commit thì cực quá vì pull nhiều branch thì sao?**
**9. Mình đang làm branch hiện tại chưa muốn commit, mà phải qua branch khác fix bug dùm member vậy thì phải làm sao?**

=> Nhìn chung mọi câu hỏi đều xoay quanh việc bạn muốn backup code mà chưa thể commit được! Có 1 câu thần chú mà mình hay dùng đó là **git stash** nó cho phép bạn backup mọi lúc, không giới hạn số lần backtup và bạn dễ dàng tra cứu lại những gì bạn backup nữa.

[Commands page](https://thanhlamkma.github.io/web-knowledge/docs/git/about)

[Q&A page](https://thanhlamkma.github.io/web-knowledge/docs/git/commands)
