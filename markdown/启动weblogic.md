# 启动weblogic #

    cd /home/weblogic/Oracle/Middleware/user_projects/domains/domain9001/bin/

    nohup ./startWebLogic.sh > admin.log &

如果下面挂有server

    nohup ./startManagedWebLogic.sh zwfwserver > zwfwserver.log http://172.16.69.74:9001/ &


# 关闭weblogic #

   `netstat -apn|grep 9001 `

然后kill相应的进程