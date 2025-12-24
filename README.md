BACKUP_DIR="/var/www/1office-$(date +%Y%m%d)"

echo "=== Bắt đầu Backup 1office -> $BACKUP_DIR ==="
```

```bash 
# 2. Chạy Rsync Backup

sudo -u www-data rsync -rltDv \
  --exclude='/Configs.php' \
  --exclude='index.php' \
  --exclude='files/' \
  --exclude='cache/' \
  1office/ "$BACKUP_DIR/"
```

```bash
# 3. Kiểm tra kết quả backup

ls -la
```

> [!check] Checkpoint
> 
> Đã thực hiện backup trước khi can thiệp vào code.

### Giai đoạn 2: Cập nhật Code (Deploy Logic)

```Bash
# 1. Chạy Rsync cập nhật code

sudo -u www-data rsync -rltDv \
  --exclude='/Configs.php' \
  --exclude='index.php' \
  --exclude='files/' \
  --exclude='cache/' \
  cloud-onpremise-boc/ 1office/
