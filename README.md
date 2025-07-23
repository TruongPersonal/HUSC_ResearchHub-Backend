## Giải thích từng nhánh theo mô hình Git Flow

### Nhánh hotfix 

#### Mục đích

- được tạo ra để sửa lỗi khẩn cấp xảy ra trên môi trường production (đã release).

#### Quy trình

1. Bắt đầu từ nhánh `main/master`.

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

3. Sau khi đẩy lên `hotfix/fix-loi-login`, merge vào nhánh `main`.

```bash
git checkout main
git merge hotfix/fix-loi-login
git push
```

- *Lưu ý*^[Trường hợp error thì do nhánh đã được bảo vệ, cần chuyển sang [[Create pull request]]]