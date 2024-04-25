---
sidebar_position: 1
---

# About

## Bản chất của Git

#### Điểm khác nhau cơ bản giữa `Git` và các `VCS` khác là cách Git _nghĩ_ về dữ liệu.

- Phần lớn hệ thống khác lưu thông tin dưới dạng
  - Các tập tin được thay đổi
  - Coi thông tin được lưu trữ như là một tập hợp các tập tin
  - Các thay đổi được thực hiện trên mỗi tập tin theo thời gian
- Còn Git sẽ xem dữ liệu của mình giống như:
  - Một tập hợp **các "ảnh" (snapshot)** của một hệ thống tập tin
  - Mỗi lần bạn **lưu lại trạng thái hiện tại** của dự án, về cơ bản Git như đang "chụp một bức ảnh" ghi lại nội dung của tất cả các tập tin tại thời điểm đó và tạo ra một **tham chiếu tới "ảnh"** đó.
  - Để hiệu quả hơn, nếu như tập tin không có sự thay đổi nào, Git **không lưu trữ tập tin** đó lại một lần nữa mà **chỉ tạo ra một liên kết** tới tập tin gốc đã tồn tại trước đó

#### Cách `Git` làm việc với dữ liệu - `Git` chỉ **thêm mới dữ liệu**

- Dữ liệu của repository sẽ được lưu trong thư mục `.git`
- Khi bạn thực hiện các thao tác trong Git, phần lớn các hành động đó đều được thêm vào cơ sở dữ liệu của Git
- Rất khó để yêu cầu hệ thống thực hiện một hành động nào đó mà không thể khôi phục lại được hoặc xóa dữ liệu dưới mọi hình thức
- Giống như trong các VCS khác, bạn có thể mất hoặc làm rối tung dữ liệu mà bạn chưa commit, nhưng khi bạn đã commit thì rất khó để mất các dữ liệu đó, đặc biệt là bạn thường xuyên đẩy (push) cơ sở dữ liệu sang 1 kho chứa khác

#### Branching and Merging

- Thế nào là `repository`?

  - `repository` (hay gọi tắt là repo) là một kho chứa toàn bộ project bao gồm source code và lịch sử thay đổi cũng như nội dung thay đổi của từng file và từng cá nhân đóng góp cho project đó, gồm 2 loại là:

  - Remote repository: Kho này dùng để chia sẻ cho nhiều người và được đặt trên server chuyên dụng
  - Local repository: Kho này được đặt trên máy của bạn và chỉ dành cho 1 người

- `branch` là nhánh của repository:
  - Các nhánh sẽ độc lập với nhau và phát triển 1 tính năng hoặc làm nhiệm vụ nào đó, không gây ảnh hưởng đến các nhánh khác.
  - Khi các nhánh hợp nhất lại với nhau thì gọi là _merge_, thông thường nhánh mặc định là `master`
  - Branch ở trên local repo thì gọi là local branch (tương tự có remote branch)
  - Một branch trên local có thể liên kết 1 hoặc nhiều branch trên remote hoặc không branch nào cả
  - Git cho phép và khuyến khích bạn tạo nhiều branch tại máy tính cá nhân của bạn, việc tạo, sát nhập và xóa bỏ những branch này diễn ra rất nhanh chóng
  - Sau khi viết code để thực hiện chức năng mới ở branch nhỏ xong, bạn hợp nhất (_merge_) code vào branch dev, tiến hành kiểm thử, nếu ok thì tiếp tục _merge_ code từ dev vào master

**Backup**: Một trong những tính năng hấp dẫn nhất, mọi người có thể tạo 1 bản sao lưu đầy đủ trên máy cá nhân (clone) hoặc có thể đẩy lên để thay thế nhánh chính trong trường hợp rủi ro

## Các nguyên tắc cơ bản và flow

**2 workflow** làm việc với git thông dụng nhất

- `Subversion-Style:`
  - Tạm dịch là kiểu lật đổ, minh họa như hình bên dưới
  - Developer `clone` shared repository về máy của mình, cập nhật code
  - Sau đó `add`, `commit` rồi `push` lên shared repository.
  - Mỗi một commit sẽ đính kèm theo một message mô tả sự thay đổi của code, tức là chú thích bạn vừa thay đổi gì.
  - Như vậy mỗi khi bạn commit thì Git sẽ nhận **code thay đổi** và **message mô tả ngắn gọn** sự thay đổi đó.
  - Mỗi một lần `commit` là một lần lưu lại trạng thái của code dưới local.
  - Còn để người khác có thể nhìn thấy được sự thay đổi đó thì cần `push` lên server.
  - Lưu ý là Git sẽ không cho phép bạn `push` lên máy chủ nếu ai đó đã push trong khoảng thời gian từ lần cuối cùng bạn `pull` về trở đi.
  - Khi đó bạn cần phải `pull` về, kiểm tra lại, `add`, `commit` rồi mới `push` lên.
- `Integration Manager`
  - "Sao chép" repository về kho của mình, gọi là `fock repo`
  - `Clone` fock repo từ kho về máy tính cá nhân.
  - Sau khi chỉnh sửa, `push` trạng thái mới lên fock repo.
  - Tạo bản so sánh giữa 2 branch của 2 repo, gọi là `pull request`, gửi cho người quản lý có quyền merge code mới vào, sẽ có demo sau.

[Commands page](https://thanhlamkma.github.io/web-knowledge/docs/git/commands)

[Q&A page](https://thanhlamkma.github.io/web-knowledge/docs/git/qa)
