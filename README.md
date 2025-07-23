## Giải thích từng nhánh theo mô hình Git Flow

*Tất cả đều được thực hiện trên Git Bash, not CMD*

### Nhánh hotfix 

#### Mục đích

- được tạo ra để sửa lỗi khẩn cấp xảy ra trên môi trường production (đã release).
#### Quy trình

1. Bắt đầu từ nhánh `main/master`:

```bash
git checkout main # di chuyển tới nhánh chính
git fetch origin # 
git reset --hard origin/main # di chuyển tới commit mới nhất của nhánh
git checkout -b hotfix/fix-loi-login # tạo nhánh hotfix và di chuyển tới nhánh đó
```

2.  Sau khi fix commit và đẩy lên:

```bash
git add .
git commit -m "fix loi login"
git push -u origin hotfix/fix-loi-login
```

3. Sau khi đẩy lên `hotfix/fix-loi-login`, merge vào nhánh `main`:

```bash
git checkout main
git merge hotfix/fix-loi-login
git push
```

- *Lưu ý*: Trường hợp error thì do nhánh `main` đã được bảo vệ, cần chuyển sang bước [[Create pull request]]

4. Merge vào `dev` để đồng bộ code:

```bash
git checkout dev
git fetch origin # 
git reset --hard origin/dev # di chuyển tới commit mới nhất của nhánh
git merge hotfix/fix-loi-login
```

- *Lưu ý*: Trường hợp error thì do nhánh `dev` đã được bảo vệ, cần chuyển sang bước [[Create pull request]]

5. Xóa nhánh hotfix nếu không cần nữa:

```bash
git branch -d hotfix/fix-loi-login
git push origin --delete hotfix/fix-loi-login
```

- Lưu ý: Đảm bảo nhánh đang đứng không phải là nhánh cần xóa