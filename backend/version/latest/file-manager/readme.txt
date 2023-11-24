#File-Manager Setup
##Install Requirement
apt update
DEBIAN_FRONTEND=noninteractive apt install curl -y
curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash
##Install Requirement

##Adding User
adduser --system --group file-manager
gpasswd -a file-manager www-data
gpasswd -a www-data file-manager
##Adding User

##Download File-Manager
mkdir -p /home/seedbox/install/file-manager/
wget -O /home/seedbox/install/file-manager/file-manager.zip https://github.com/tnan/seedbox/raw/main/backend/version/latest/file-manager/file-manager.zip
printf 'A\n' | unzip -q /home/seedbox/install/file-manager/file-manager.zip -d /
##Download File-Manager

##Configuration
mkdir -p /var/www/html/seedbox/files/downloads/
mkdir -p /var/www/html/seedbox/files/torrents/

chown -R torrent-downloader:torrent-downloader /home/torrent-downloader/
chown -R www-data:www-data /var/www/html/
chmod -R 777 /var/www/html/

systemctl daemon-reload
systemctl enable file-manager
systemctl start file-manager
##Configuration
#File-Manager Setup