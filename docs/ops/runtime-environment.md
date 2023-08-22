# Futtatási környezet

Az alkalmazás egyes komponensei [Docker](https://www.docker.com/) container-ekben futnak. A Docker-ről további információ: [https://www.docker.com/what-docker](https://www.docker.com/what-docker)

A rendszer a következő container-ekből áll:

* Alkalmazás:
    * `coursecatalog_app_1`: Az alkalmazás container-e. Ez egy NodeJS alkalmazást futtat.
    * `coursecatalog_db_1`: Az adatbázisszerver container-e. MariaDB adatbázisszerver.
* Infrastruktúra:
    * `nginx`: NGINX web proxy, a https-t biztosítja, illetve proxy-zza a kérésket az alkalmazás container-e felé. ([https://github.com/nginxinc/docker-nginx](https://github.com/nginxinc/docker-nginx))
    * `nginx-gen`: Segéd container, ő generálja az nginx konfigurációs állományokat automatikusan. ([https://github.com/jwilder/docker-gen](https://github.com/jwilder/docker-gen))
    * `letsencrypt-nginx-proxy-companion`: A rendszerhez szükséges Let's Encrypt tanúsítványokat kezeli. Amikor lejárnak, automatikusan megújítja őket, illetve az `nginx-gen` segítségével frissíti az NGINX config-okat. ([https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion))
    * `coursecatalog_root-redirect_1`: A [https://kmooc.uni-obuda.hu](https://kmooc.uni-obuda.hu) oldalra érkező kéréseket irányítja át a [https://www.kmooc.uni-obuda.hu](https://www.kmooc.uni-obuda.hu) oldalra (külön SSL certificate-je van).
    * `coursecatalog_backup_1`: Az adatbázisról 5 percenként biztonsági mentést készítő container.

```


                                 .-,(  ),-.    
                              .-(          )-. 
                             (    internet    )
                              '-(          ).-'
                                  '-.( ).-'    
                                      |
                                      |
                                      v
                                  .-------.
                                  | nginx |---------------------------.
                                  '-------'                           |
                   .------------------|-                              |
                   |                  |                               v
                   v                  |                               |
   .-------------------------------.  |    .---------------------.    |
   | coursecatalog_root-redirect_1 |  '--->| coursecatalog_app_1 |    |
   '-------------------------------'       '---------------------'    |
                                                      |               |
                                                      v               |
                                           .--------------------.     |
                                           | coursecatalog_db_1 |     |
                                           '--------------------'     |
                                                                      |
                                                                      |
                                .-----------.                         |
                                | nginx-gen |<------------------------'
                                '-----------'
                                      ^
                                      |
                                      |
                    .-----------------------------------.
                    | letsencrypt-nginx-proxy-companion |
                    '-----------------------------------'
```