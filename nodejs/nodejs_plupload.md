## nodejs+plupload 多文件拖拽上传
## 1.前端[plupload][1]
参考：

- [前端上传组件Plupload使用指南][2]
- [demo][3]
````html
</!DOCTYPE html>

 <html>
<head>
	<title></title>
    <script src="/resources/js/plupload.full.min.js"></script>
	<style>
		body{ font-size: 12px;}
		body,p,div{ padding: 0; margin: 0;}
		._wraper{ padding: 30px 0;}
		.btn-wraper{ text-align: center;}
		.btn-wraper input{ margin: 0 10px;}
		#file-list{ width: 350px; margin: 20px auto;}
		#file-list li{ margin-bottom: 10px;}
		.file-name{ line-height: 30px;}
		.progress{ height: 4px; font-size: 0; line-height: 4px; background: orange; width: 0;}
	    .tip1{text-align: center; font-size:14px; padding-top:10px;}
	    .tip2{text-align: center; font-size:12px; padding-top:10px; color:#b00}
		#drag-area{ border: 1px solid #ccc; height: 150px; line-height: 150px; text-align: center; color: #aaa; width: 600px; margin: 10px auto;}
		.catalogue{ position: fixed; _position:absolute; _width:200px; left: 0; top: 0; border: 1px solid #ccc;padding: 10px; background: #eee}
	    .catalogue a{ line-height: 30px; color: #0c0}
	    .catalogue li{ padding: 0; margin: 0; list-style: none;}
	</style>
</head>

<body>
	<p class="tip1">拖拽上传对比图库</p>
    <div class="wraper">
        <p id="drag-area">把要上传的文件拖放到这里(请使用支持html5的浏览器)</p>
        <div class="btn-wraper">
            <input type="button" class="btn" value="选择文件..." id="browse" />
            <input type="button" class="btn" value="开始上传" id="upload-btn" />
        </div>
        <ul id="file-list">
        </ul>
    </div>
<script type="text/javascript">
	var uploader = new plupload.Uploader({ //实例化一个plupload上传对象
		browse_button : 'browse',
		url : '/plupload',
		flash_swf_url : '/resources/js/Moxie.swf',
		silverlight_xap_url : '/resources/js/Moxie.xap',
		drop_element : 'drag-area'
	});
	uploader.init(); //初始化
	//绑定文件添加进队列事件
	uploader.bind('FilesAdded',function(uploader,files){
		for(var i = 0, len = files.length; i<len; i++){
			var file_name = files[i].name; //文件名
			//构造html来更新UI
			var html = '<li id="file-' + files[i].id +'"><p class="file-name">' + file_name + '</p><p class="progress"></p></li>';
			$(html).appendTo('#file-list');
		}
	});

	//绑定文件上传进度事件
	uploader.bind('UploadProgress',function(uploader,file){
		$('#file-'+file.id+' .progress').css('width',file.percent + '%');//控制进度条
	});

	//上传按钮
	$('#upload-btn').click(function(){
		uploader.start(); //开始上传
	});

</script>
</body>

</html>
````


## 2.后端node-pluploader
* 安装node-pluploader
$ npm install node-pluploader --save
* 代码
```nodejs
var Pluploader = require('node-pluploader');

var pluploader = new Pluploader({
    uploadLimit: 6, //单个文件最大，MB
    //uploadDir: './public/uploads/similar'
});

 /*
  * Emitted when an entire file has been uploaded.
  *
  * @param file {Object} An object containing the uploaded file's name, type, buffered data & size
  * @param req {Request} The request that carried in the final chunk
  */
pluploader.on('fileUploaded', function(file, req) {
    StringUtils.mkdirSync('../public/uploads/similar');
    var target_path = "./public/uploads/"+file.name
    fs.writeFile(target_path, file.data,function(err){
        console.log(file);
    }) ;

});

/*
  * Emitted when an error occurs
  *
  * @param error {Error} The error
  */
pluploader.on('error', function(error) {
    throw error;
});

// This example assumes you're using Express
router.post('/plupload', function(req, res){
  pluploader.handleRequest(req, res);
});

```




[1]: http://www.plupload.com/
[2]: http://www.cnblogs.com/2050/p/3913184.html
[3]: http://chaping.github.io/plupload/demo/index4.html
