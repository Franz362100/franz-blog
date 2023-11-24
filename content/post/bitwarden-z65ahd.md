---
title: Bitwarden部署与备份
slug: bitwarden-z65ahd
url: /post/bitwarden-z65ahd.html
date: '2023-11-20 10:22:37'
lastmod: '2023-11-24 09:57:03'
toc: true
tags:
  - Docker
categories:
  - 技术分享
keywords: Docker
isCJKLanguage: true
---



1. 生成一个 admin 用户管理页面的 token

    ```Bash
    openssl rand -base64 48
    ```
2. 使用docker部署

    ```Bash
    docker run -d --name vaultwarden \
     -e SIGNUPS_ALLOWED=false \
     -e INVITATIONS_ALLOWED=false \
     -e ADMIN_TOKEN=上面生成得Base64 \
     -e LOG_FILE=/data/log.log \
     -e LOG_LEVEL=info \
     -p 8081:80 \
     -v /root/vaultwarden/:/data/ \
     vaultwarden/server:latest
    ```

3. 对bitwarden进行定时备份

    * 按照官方说明，现执行 docker 镜像，获取 token。这里的镜像一大部分都是 Rclone。

      ```Bash
      docker run –rm -it \
      –mount type=volume,source=vaultwarden-rclone-data,target=/config/ \
      ttionya/vaultwarden-backup:latest rclone config
      ```
    * 配置Rclone
    * 执行备份定时备份的docker容器

      ```Bash
      # 七牛云 docker 备份配置,这里仅参考，正式备份内容见下方备份到多个位置
      docker run -d \
        --restart=always \
        --name vaultwarden_backup_qiniu \
        --volumes-from=vaultwarden \
        --mount type=volume,source=vaultwarden-rclone-data,target=/config/ \
        -e DATA_DIR="/data" \
        -e RCLONE_REMOTE_NAME=BitwardenBackup_qiniu \
         -e RCLONE_REMOTE_DIR="bitwarden-1024" \
         -e ZIP_TYPE="7z" \
         -e CRON="0 */8 * * *" \
         -e ZIP_PASSWORD="压缩密码" \
         -e BACKUP_KEEP_DAYS="30" \
        ttionya/vaultwarden-backup:latest
      ```

4. 从备份中还原

    * 停止bitwarden容器
    * 还原命令

      ```Bash
       docker run --rm -it \
             --mount type=bind,source="/root/vaultwarden",target=/data/ \
             --mount type=bind,source=$(pwd),target=/bitwarden/restore/ \
             -e DATA_DIR="/data" \
             ttionya/vaultwarden-backup:latest restore \
             --zip-file 文件名称 \
      	   -p 压缩密码
      ```
    * 启动bitwarden容器
