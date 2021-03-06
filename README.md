# tmpl2pdf
根据PDF模板动态生成PDF文件<br />
使用场景：各类电子协议、电子证书、电子发票的制作<br />
要求自行使用 Adobe Acrobat 制作PDF表单模板，网上资料很多，请自己查阅。

<table>
  <tr>
    <th colspan="2" align="left">结构说明</th>
  </tr>
  <tr>
    <th>目录/文件</th>
    <th>说明</th>
  </tr>
  <tr>
    <td>./tmpl/</td>
    <td>PDF模板文件夹</td>
  </tr>
<tr>
    <td>./tmpl/tmpl.pdf</td>
    <td>测试模板，此模板中含有name,addr两个表单文本域</td>
  </tr>
	<tr>
    <td>./out/</td>
    <td>存放生成后的PDF文件</td>
  </tr>
	
	
<tr>
    <td>./font/</td>
    <td>字体文件夹</td>
  </tr>
	
	
<tr>
    <td>./serv.jar</td>
    <td>服务文件</td>
  </tr>
	</tr>
		<tr>
    <td>./run.bat</td>
    <td>Windows下启动脚本</td>
  </tr>
</table>


## 服务端
### 环境要求
JDK：jdk1.8

### 服务启动
&#35;&#35; Linux下启动（PDF输出目录需要有写权限；对于中文字体文件而言，可能是一个字体组合包，此时需要在字体路径后加上：,0 或 ,1 代表使用字体包中的某种风格）<br />
&#35; nohup java -jar serv.jar --server.port=端口号 --pdftmpl.dir.src=PDF模板目录 --pdfout.dir.dest=PDF输出目录 --pdf.font=使用的字体文件 >>./serv.log &<br />
如：<br />&#35; nohup java -jar serv.jar --server.port=8091 --pdftmpl.dir.src=/root/tmpl2pdf/tmpl/ --pdfout.dir.dest=/root/tmpl2pdf/out/ --pdf.font=/root/tmpl2pdf/font/simsun.ttc,1  >>./serv.log &

&#35;&#35; Linux下检测服务是否正常<br />
&#35; netstat -anp | grep 上一步指定的端口号

&#35;&#35; Windows下启动<br />
编辑run.bat，修改pdftmpl.dir.src 、pdfout.dir.dest <br />双击run.bat启动服务



## 客户端调用
任何客户端可通过HTTP请求来调用服务
### 版本查看
<table>
  <tr>
    <th colspan="2" align="left">GET http://192.168.1.88:8091/info</th>
  </tr>
  <tr>
    <th>参数</th>
    <th>说明</th>
  </tr>
  <tr>
    <td>无</td>
    <td>无</td>
  </tr>
</table>

### 根据PDF模板动态生成PDF文件
<table>
  <tr>
    <th colspan="3" align="left">POST http://192.168.1.88:8091/create</th>
  </tr>
  <tr>
    <th>参数</th>
    <th>是否必须</th>
    <th>说明</th>
  </tr>
  <tr>
    <td>tmpl</td>
    <td>*</td>
    <td>PDF模板文件名（不含后缀，如tmplfile1）</td>
  </tr>
  <tr>
    <td>out</td>
    <td>*</td>
    <td>生成的PDF文件名（不含后缀，如pdffile1）</td>
  </tr>
  <tr>
    <td>data</td>
    <td>*</td>
    <td>PDF模板中的表单域及对应的值，以json格式传递，如：<br/>{
	"name": "张三丰2222",
	"addr": "中国上海市"
}</td>
  </tr>
	  <tr>
    <td>fontSize</td>
    <td></td>
    <td>定义PDF文字字号，如：8，默认值为8</td>
  </tr>
  <tr>
    <td>lastModifiedTime</td>
    <td></td>
    <td>若指定，则将生成的PDF文件的最后修改时间置为指定值，如：<br />2008-12-12 12:00:00</td>
  </tr>
</table>


## 问题反馈
使用中若有问题请联系QQ：46926125
