# Zabbix+Grafana+FreeBSD-13:

# ports update:
portsnap fetch extract update

# pkg update:
make -DBATCH -C /usr/ports/ports-mgmt/pkg reinstall clean

# compilers:
pkg install -y llvm cmake llvm10 go

# database:
make -DBATCH -C /usr/ports/databases/mariadb105-server install clean

# http:
make -DBATCH -C /usr/ports/www/apache24 install clean

# Configure some ports:
make -C /usr/ports/lang/php74-extensions config
# SELECT: CURL IMAP GD JSON LIBXML2 MBSTRING MYSQLI OPENSSL PDF PDO PDO_MYSQL SOAP ZLIB
make -C /usr/ports/net-mgmt/zabbix5-server config
# SELECT: LIBXML2

# zabbix:
make -DBATCH -C /usr/ports/net-mgmt/zabbix5-server install clean

# zabbix-frontend
make -DBATCH -C /usr/ports/net-mgmt/zabbix5-frontend install clean

# Grafana:

# node14:
make -DBATCH -C /usr/ports/www/node14 install clean

# yarn:
make -DBATCH -C /usr/ports/www/yarn-node14 install clean

# PROJECT:
cd
git clone https://github.com/alexanderzobnin/grafana-zabbix.git
cd grafana-zabbix
go mod vendor
env GOOS=freebsd GOARCH=amd64 go build -ldflags="-s -w" -mod=vendor -o ./dist/zabbix-plugin_freebsd_amd64 ./pkg
# install:
sudo install -c -g 904 -o 0 -m 0755 dist/zabbix-plugin_freebsd_amd64 \
  /var/db/grafana/plugins/alexanderzobnin-zabbix-app
