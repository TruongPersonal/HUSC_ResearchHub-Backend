## Giải thích từng nhánh theo mô hình Git Flow

*Tất cả đều được thực hiện trên Git Bash, not CMD*

### Nhánh dev:

- `dev` là nhánh phát triển chính – nơi tất cả tính năng mới được code và test trước khi được merge lên `main`.
- `dev` chứa code đang phát triển, chưa ổn định và `main` chứa code ổn định, triển khai được.

#### Quy trình:

1. Tạo nhánh từ `dev` để thêm tính năng mới:

```bash
git checkout dev # chuyển qua nhánh dev
git fetch origin
git reset --hard origin/dev
git checkout -b feature/dang-nhap
```

2. Làm xong thì commit và đẩy lên nhánh `feature/dang-nhap`

```bash
git add .
git commit -m "lam xong tinh nang dang nhap"
git push -u origin feature/dang-nhap
```

3. Merge vào `dev` để đồng bộ code:

```bash
git checkout dev
git fetch origin # 
git reset --hard origin/dev # di chuyển tới commit mới nhất của nhánh
git merge feature/dang-nhap # gộp nhánh vào dev
```

- *Lưu ý*: Trường hợp error thì do nhánh `dev` đã được bảo vệ, cần chuyển sang bước [Create pull request](https://share.note.sx/ucb59y53#zI5tnQNLP4D8IeP2DShaGKA1PxWqKJK4ok9VUGY13JE)

### Nhánh hotfix:

#### Mục đích:

- Được tạo ra để sửa lỗi khẩn cấp xảy ra trên môi trường production (đã release).

#### Quy trình:

1. Bắt đầu từ nhánh `main/master`:

```bash
git checkout main # di chuyển tới nhánh chính
git fetch origin # 
git reset --hard origin/main # di chuyển tới commit mới nhất của nhánh
git checkout -b hotfix/fix-loi-login # tạo nhánh hotfix và di chuyển tới nhánh đó
```

2.  Sau khi fix, commit và đẩy lên:

```bash
git add .
git commit -m "fix loi login"
git push -u origin hotfix/fix-loi-login
```

3. Sau khi đẩy lên `hotfix/fix-loi-login`, merge vào nhánh `main`:

```bash
git checkout main # chuyển tới main
git merge hotfix/fix-loi-login # gộp nhánh vào main
git push
```

- *Lưu ý*: Trường hợp error thì do nhánh `main` đã được bảo vệ, cần chuyển sang bước [Create pull request](https://share.note.sx/ucb59y53#zI5tnQNLP4D8IeP2DShaGKA1PxWqKJK4ok9VUGY13JE)

4. Merge vào `dev` để đồng bộ code:

```bash
git checkout dev
git fetch origin # 
git reset --hard origin/dev # di chuyển tới commit mới nhất của nhánh
git merge hotfix/fix-loi-login # gộp nhánh vào dev
```

- *Lưu ý*: Trường hợp error thì do nhánh `dev` đã được bảo vệ, cần chuyển sang bước [Create pull request](https://share.note.sx/ucb59y53#zI5tnQNLP4D8IeP2DShaGKA1PxWqKJK4ok9VUGY13JE)

5. Xóa nhánh hotfix nếu không cần nữa:

```bash
git branch -d hotfix/fix-loi-login
git push origin --delete hotfix/fix-loi-login
```

- Lưu ý: Đảm bảo nhánh đang đứng không phải là nhánh cần xóa