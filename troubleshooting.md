# Troubleshooting

## 

`kubectl cluster-info --kubeconfig=<ścieżka_do_kubeconfig>` - waliduje podany kubeconfig, sprawdza połączenie do klastra za pomocą podanego kubeconfig

`kubectl logs <nazwa_poda>` - pokazuje logi dla podanego poda  
  `-f` - pokazuje logi w trybie ciągłym tzn. jeżeli aplikacja wygeneruje kolejny log zostanie on wyświetlony  
  `--previous` - pokazuje log dla poda który został uśmiercony

`journalctl -u <nazwa_serwisu>` - pokazuje logi podanego serwisu

`openssl  x509 -in <certyfikat> -text` - pokazuje właściwości certyfikatu

