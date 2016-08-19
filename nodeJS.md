# nodeJS 服务 Linux 開机启动
1. 在 /etc/init.d/ 下建立 nodeJS 文件，内容如下
```
  #!/bin/bash
  # chkconfig: 35 95 1
  # description: script to start/stop nodeJS
  case $1 in
  start)
  forever start -a ~/Dna/express/app.js
  ;;
  stop)
  forever stop ~/Dna/express/app.js
  ;;
  *)
  echo "Usage: $0 (start|stop)"
  ;;
  esac
```
2. 变更权限  
chmod 775 nodeJS
3. 加入自动启动  
chkconfig --add nodeJS  
4. 以后启动脚本命令如下  
service nodeJS start  
service nodeJS stop
