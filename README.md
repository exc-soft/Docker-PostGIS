### 简介

  该容器是根据 https://github.com/GeographicaGS/Docker-Postgis 里面 Quick_Quail 改的，增加了 pgrouting 扩展

### 安装方法

1、服务器安全组开启 5432 端口允许访问

2、执行以下命令安装

    # 安装 postgis
    cd Docker-Postgis
    docker-compose up -d --build
    
    # 进入容器
    docker exec -it dockerpostgis_postgis_1 /bin/bash

    # 编译 pgrouting
    apt-get update && apt-get install -y wget cmake g++ libboost-graph-dev libcgal-dev
    
    cd /usr/local/share/postgresql
    
    wget -O pgrouting-2.6.1.tar.gz https://github.com/pgRouting/pgrouting/archive/v2.6.1.tar.gz
    
    tar xvfz pgrouting-2.6.1.tar.gz && cd pgrouting-2.6.1 && mkdir build && cd build && cmake -L .. && make && make install

    # 退出容器，下载 pgAdmin，将备份数据导入
    选择 Databases
    展开菜单在 postgres 右击选择 Restore
  