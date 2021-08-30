# Zabbix+Grafana+FreeBSD-13:

# ports update:
portsnap fetch extract update

# pkg update:
make -DBATCH -C /usr/ports/ports-mgmt/pkg reinstall clean

# compilers:
pkg install -y llvm cmake llvm10

# database:
make -DBATCH -C /usr/ports/databases/mariadb105-server install clean

# http:
make -DBATCH -C /usr/ports/www/apache24 install clean

# Configure some ports:
make -C /usr/ports/lang/php74-extensions config

SELECT: CURL IMAP GD JSON LIBXML2 MBSTRING MYSQLI OPENSSL PDF PDO PDO_MYSQL SOAP ZLIB

make -C /usr/ports/net-mgmt/zabbix5-server config
SELECT: LIBXML2

# zabbix:
make -DBATCH -C /usr/ports/net-mgmt/zabbix5-server install clean

# zabbix-frontend
make -DBATCH -C /usr/ports/net-mgmt/zabbix5-frontend install clean

# Grafana:
