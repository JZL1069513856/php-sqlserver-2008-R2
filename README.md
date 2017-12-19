# php-sqlserver-2008-R2
简单的描述如何用php链接sqlserver2008R2

### php 链接 sqlserver 2008

> 环境

1. phpstudy2017  php7.0
2. sql 2008 R2

> 修改php配置文件 php.ini

	extension=php_pdo_sqlsrv_7_nts_x86.dll
	extension=php_sqlsrv_7_nts_x86.dll
	将这两行语句前的;去掉,如果没有这两行代码，则需要去微软官网下载

	下载地址 (注意看需求
	https://www.microsoft.com/en-us/download/details.aspx?id=20098
	
	下载ODBC Driver 11 (顺带
	https://www.microsoft.com/en-us/download/details.aspx?id=36434

> 配置sqlserver

	打开sqlserver 在安全性里的登录名 sa 修改密码为 123
	检测远程是否开启
	打开sqlserver 配置管理工具
	在sqlserver 网络配置的选项下
	将tcp/ip 启用
	在tcp/ip 属性里的ip地址全部改为是，端口改为1433(不要和自己建的其他端口冲突)

> 测试

	cmd里输入netstat -an
	检测是否监听到有 0.0.0.0:1433
	没有则认真检查操作步骤

> php链接sql语句

	//这里展示两种
	$conn = new PDO("sqlsrv:server=localhost;database=sqlserver","sa","123");
	$sql = "select  * from admin";
	$res = $conn->query($sql);
	while ($row = $res->fetch()){
	print_r($row);
	}

	// $serverName = "localhost";
	// $connectionInfo = array( "Database"=>"sqlserver", "UID"=>"sa", "PWD"=>"123");
	// $conn = sqlsrv_connect( $serverName, $connectionInfo );
	// if( $conn === false ) {
	//     die( print_r( sqlsrv_errors(), true));
	// }


