# ETCD

## Backup

`ETCDCTL_API=3 etcdctl --endpoints=<endpoint_etcd> --cacert=<trusted-ca-file> --cert=<cert-file> --key=<key-file> snapshot save <backup-file-location>` - tworzy backup w podanej lokalizacji 

`ETCDCTL_API=3 etcdctl --endpoints=<endpoint_etcd> --cacert=<trusted-ca-file> --cert=<cert-file> --key=<key-file> snapshot restore <backup-file-location>` - odtwarza backup z podanego pliku   
  `--data-dir=<katalog>` - katalog gdzie może zostać odtworzony snapshot \(możemy zmienić kdatalog skąd ETCD przetrzymuje baze danych, nstaępnie trzeba zamienić katalog w definicji poda ETCD na podany by ETCD pobierało pliki bazy danych z nowego miejsca\)





