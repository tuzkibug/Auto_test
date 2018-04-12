# rally  
## 安装  
* 安装最简centos系统后，缺少一些必备软件和epel源，所以补充安装：  
yum install -y epel-release  
yum install gcc python-pip python-devel  
* 执行rally自动化安装程序，wget和curl任选其一    
wget -q -O- https://raw.githubusercontent.com/openstack/rally/master/install_rally.sh | bash   
curl https://raw.githubusercontent.com/openstack/rally/master/install_rally.sh | bash  
* 安装成功后，重建数据库  
rally db recreate  

## 使用  
* 执行注册程序，向rally注册openstack环境，需要拷贝openstack的rc文件至测试机下，以openrc为例  
. openrc admin admin  
* 创建执行环境  
rally deployment create --fromenv --name=existing  
* 检查环境  
rally deployment check  
* 执行用例，所有用例的实例模板均在/usr/share/rally/samples下，可拷贝至特定路径使用，如/root下  
rally task start samples/tasks/scenarios/nova/boot-and-delete.json  
* 输出结果为html文件  
rally task report 4b1fdfbb-7526-4874-a346-30415d216f6b --out output.html  
* 根据网络环境，编辑output.html中的css文件来源，由于国内网络环境（防火墙），几个css的网址均无法连接，改为国内免费css  
```
<link rel="stylesheet" href="https://cdn.bootcss.com/nvd3/1.1.15-beta/nv.d3.min.css">
  <script type="text/javascript" src="http://cdn.bootcss.com/angular.js/1.3.3/angular.min.js"></script>
  <script type="text/javascript" src="https://cdn.bootcss.com/d3/3.4.13/d3.min.js"></script>
  <script type="text/javascript" src="https://cdn.bootcss.com/nvd3/1.1.15-beta/nv.d3.min.js"></script>
```  
* 桌面环境点击该html文件即可图形化呈现结果  
