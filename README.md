# cdnfly-


需要最新版联系Tg:cdnflya
https://t.me/cdnflya
已删除后门 确保无后门稳定运行






cdnfly安装需知
主控维护相关
重启主控命令 supervisorctl -c /opt/cdnfly/master/conf/supervisord.conf restart all;
关闭主控 supervisorctl -c /opt/cdnfly/master/conf/supervisord.conf stop all
导出数据库命令 mysqldump -uroot -p@cdnflypass -h127.0.0.1 -P3306 cdn > /root/cdn_backup_$(date +%Y%m%d_%H%M%S).sql 导出请查看文件大小验证一下
数据库启动命令 service mysqld restart 什么情况数据库无法启动 硬盘满了会导致数据库关闭 
注意请把es安装到数据盘不要安装到系统盘 以免硬盘跑满导致系统故障
网站数量比较多 请求比较高建议主控es 分开  用户网站比较多建议主控配置 16C32G 150G SSD或者M2 或u2盘 建议独立服务器 
独立ES 配置 32C64G 1T ssd 或者m2
节点重启通信命令 supervisorctl -c /opt/cdnfly/agent/conf/supervisord.conf restart all;
节点重启NG命令 /usr/local/openresty/nginx/sbin/nginx -s reload 

当elasticsearch出现无法解决的异常，或者elasticsearch数据占满了硬盘，可以执行此操作来初始化elasticsearch，注意：初始化elasticsearch会清空所有的网站访问日志。
执行如下命令初始化:
cd /tmp;
wget http://us.centos.bz/cdnfly/int_es.sh -O int_es.sh;
chmod +x int_es.sh;
./int_es.sh /home/es;

当安装节点完成时，没有在cdn后台的待初始化列表发现此节点时，可以执行如下命令来重新注册。/opt//cdnfly/agent/sh/add-node.sh && supervisorctl -c /opt/cdnfly/agent/conf/supervisord.conf restart all

卸载主控
cd /tmp/;
curl -m 5 http://dl2.lotcdn.com/cdnfly/master_uninstall.sh -o master_uninstall.sh  curl -m 5 http://us.centos.bz/cdnfly/master_uninstall.sh;
chmod +x master_uninstall.sh;
./master_uninstall.sh;


卸载节点
cd /tmp/;
curl -m 5 http://dl2.lotcdn.com/cdnfly/agent_uninstall.sh -o agent_uninstall.sh  curl -m 5 http://us.centos.bz/cdnfly/agent_uninstall.sh;
chmod +x agent_uninstall.sh;
./agent_uninstall.sh;

更多教程请到 http://doc.cdnfly.com/ 学习
