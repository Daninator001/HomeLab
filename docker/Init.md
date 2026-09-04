groupadd openhab
useradd -g openhab -r -s /sbin/nologin openhab
usermod -a -G openhab <platform_user>