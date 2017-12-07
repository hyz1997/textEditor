# textEditor
this is a Rich Text Editor
您只需在您的html中插入这样的代码
```
<div  onmousedown="show_element(event)" style="clear:both" id="customized-buttonpane" class="editor"></div>
```
如需对插入的图片进行放大缩小，请添加一下代码
```
<div id="odiv" style="display:none;position:absolute;z-index:100;">
    <img src="assets/pic/sx.png" title="缩小" border="0" alt="缩小" onclick="sub(-1);"/>
    <img src="assets/pic/fd.png" title="放大" border="0" alt="放大" onclick="sub(1)"/>
    <img src="assets/pic/cz.png" title="重置" border="0" alt="重置" onclick="sub(0)"/>
    <img src="assets/pic/sc.png" title="删除" border="0" alt="删除" onclick="del();odiv.style.display='none';"/>
</div>
```
对于文章的ajax交互，我在这里做如下说明：
您插入在文章中的图片不用单独保存，整个文章会以字符串的方式传给后台，生成字符串的时侯自动生成"<span>"等html标签，所以您在展示页面只用直接获取文章内容，不用再对其进行排版
这里举一个交互的例子


```
$('#submit').click(function() {
        var content = '';
        var myID = new Date().getTime();
        console.log(myID);
		var title = $("input[type='text']").val();
		content = $('#customized-buttonpane').html();
        console.log(content);
        
		
        $.ajax({
			type:"POST",
			url:"http://172.22.4.202:8888/blog/management/insertArticle",
			data:{
				articleTitle:title,
				articleContent:content,
				articleId:myID

			},
			success:function(data) {
				if(data=="1"){
                    alert("保存成功！");
                    window.open("listArticel.html");
				}
				console.log(title);
			},
			error:function(jqXHR, textStatus, errorThrown){
			  if(errorThrown != 'abort'){
			   //ajax被调用abort后执行的方法
			   alert('出错了');
			  }
			}
		})
	});
```
html部分
```
<div class="main-content" id="articel">
			<h1 class="content-header">文章编辑
			</h1>

			<hr>
			<div class="articel-title">
				<label>标题</label>
				<input type="text" class="form-control" id="articel-title">
				<p style="margin-top: 2%; font-weight: 700;">内容</p>
			</div>
			<div id="odiv" style="display:none;position:absolute;z-index:100;">
			<img src="../assets/pic/sx.png" title="缩小" border="0" alt="缩小" onclick="sub(-1);"/>
				<img src="../assets/pic/fd.png" title="放大" border="0" alt="放大" onclick="sub(1)"/>
				<img src="../assets/pic/cz.png" title="重置" border="0" alt="重置" onclick="sub(0)"/>
				<img src="../assets/pic/sc.png" title="删除" border="0" alt="删除" onclick="del();odiv.style.display='none';"/>
			</div>
			<div onmousedown="show_element(event)" style="clear:both" id="customized-buttonpane" class="editor"></div>
			<div id="s1"></div>
			<a style="margin-left: 2%" href="javascript:void(0)" onclick="javascript:showlocs()">恢复上次编辑文档</a>
			<div style="margin-left: 2%">
			    <input type="button" class="btn btn-info" value="保存" id="submit">
			    <input type="button" class="btn btn-danger" value="取消">
			</div>
		</div>
```
如有任何问题，请联系我QQ:425910502
