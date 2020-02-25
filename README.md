# qqlight-websocket-aardio
QQLight机器人WebSocket插件aardio扩展库

> qqlight版本：v3.0+
>
> qqlight-websocket版本：v2.3.0
>
> 通过web.socket.jsonClient
>
> 与WebSocket-RPC插件（websocket.protocol.ql.dll）进行通信
>
> 从而实现跟QQLight机器人框架的交互
>
> WebSocket-RPC插件地址 https://github.com/Chocolatl/qqlight-websocket

## 安装

在线安装扩展库
```
import ide;
import fsys; 
import inet.downBox;
import sevenZip.lzma;
import fsys.untar;
var url = "https://github.com/nlysh007/qqlight-websocket-aardio/releases/latest/download/qqlight.tar.lzma"; 
var path = "~/download/lib/"; 
var dl = inet.downBox(,"正在下载qqligt扩展库",true); 
	if(dl.download(url,path++"qqlight.tar.lzma")){
		sevenZip.lzma.decodeFile(path++"qqlight.tar.lzma",path++"qqlight.tar")
		var tar = fsys.untar(path++"qqlight.tar");
		for(fileName,writeSize,remainSize,pos in tar.eachBlock() ){
			
		} 
		tar.close()
		fsys.delete(path++"qqlight.tar")
		ide.createThread(path++"qqlight/setup.dl.aardio")
	}
```
## 示例
这是一个复读机（Echo）的aardiot示例

```
import console; 
import win;
import qqlight;

var wsClient = qqlight.wsClient();

var pluginPath = "";
if(pluginPath==""){
    error("未指定plugin目录")
} 

wsClient.connectByPluginPath(pluginPath) //通过qqlight的plugin目录路径来连接

wsClient.onOpen = function(){
    console.dump("已连接")
}

wsClient.onMessage = function(event,params){
    console.dump("收到消息",params)
    //简单的消息复读例子
    wsClient.sendMessage({
        ["type"]    = params["type"] ;
        ["group"]   = params["group"];
        ["qq"]      = params["qq"];
        ["content"] = params["content"];
    })	
    console.dump("已复读消息",params["content"])
}

win.loopMessage()
console.pause(true);
```