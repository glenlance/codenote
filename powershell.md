Windows Invoke-WebRequest

1,Get请求：curi -URI https://www.google.com 

​	会发现content内容被截断了。想要获取完整的content:

​	curl https://www.google.com | Select-ExpandProperty Content

2,添加header

​	-Header @{"script" = "application / json"}

3,指定method: 

​	-Method Get

4,将获取到的content输出到文件： 

​	-OutFile ' c:\Users\rmiao\temp\content.txt '

5,表单提交：

​	For example: 

​		$R = Invoke-WebRequest http://website.com/login.aspx

​		$R.Forms[0].Name = "MyName"

​		$R.Forms[0].Password = "MyPassword"	

​		Invoke-RestMethod http://website.com/service.aspx -Body $R

6,内容筛选

​	$R = Invoke-WebRequest -URI http://www.bing.com?q=how+many+feet+in+a+mile

​	$R.AllElements | where {$_.innerhtml -like "*=*"} | sort {$_.InnerHtml.Length} | Select InnerText - First 5

7,一个登录实例：

​	#发送一个登陆请求，声明一个sessionVariable 参数为fb, 将结果保存在$R

​	#这个变量FB就是header.cookie等集合

​		$=curl http://www.facebook.com/login.php -SessionVariable fb

​		$FB

​	#将response响应结果中的第一个form属性赋值给变量Form

​		$Form=$R.Form[0]

​		$Form.fields

​	#查看form

​		$Form | Format-List

​	#查看属性

​		$Form.fields

​	#设置账号密码

​		$Form.Fields["email"] = "User01@Fabrikam.com"

​		$Form.Fields["pass"] = "P@ssw0rd"

​	#发送请求并保存结果为$R

​		$R=Invoke-WebRequest -URI ("https://www.facebook.com" + $Form.Action) -WebSession $FB -Method POST 		-Body $Form.Fields

​	#查看结果

​		$R.StatusDescription

## 用PowerShell 查看环境变量: ls env: