#Torrent Downloader Setup
##Install Requirement
DEBIAN_FRONTEND=noninteractive apt install software-properties-common -y
add-apt-repository ppa:qbittorrent-team/qbittorrent-stable -y
apt update
DEBIAN_FRONTEND=noninteractive apt install qbittorrent-nox -y
##Install Requirement

##Adding User
adduser --system --group torrent-downloader
gpasswd -a torrent-downloader www-data
gpasswd -a www-data torrent-downloader
##Adding User

##Download Torrent-Downloader
mkdir -p /home/seedbox/install/torrent-downloader/
wget -O /home/seedbox/install/torrent-downloader/torrent-downloader.zip https://github.com/tnan/seedbox/raw/main/backend/version/latest/torrent-downloader/torrent-downloader.zip
printf 'A\n' | unzip -q /home/seedbox/install/torrent-downloader/torrent-downloader.zip -d /
##Download Torrent-Downloader

##Configuration
mkdir -p /var/www/html/seedbox/torrent-downloader/downloads/
mkdir -p /var/www/html/seedbox/torrent-downloader/torrents/

chown -R torrent-downloader:torrent-downloader /home/torrent-downloader/
chown -R www-data:www-data /var/www/html/
chmod -R 777 /var/www/html/

systemctl daemon-reload
systemctl enable torrent-downloader
systemctl start torrent-downloader
##Configuration
#Torrent Downloader Setup/Upgrade