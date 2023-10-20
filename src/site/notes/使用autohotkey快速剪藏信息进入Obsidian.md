---
{"dg-publish":true,"permalink":"/使用autohotkey快速剪藏信息进入Obsidian/"}
---


### 背景介绍
#### 动机
有时候在即刻、知乎、小红书之类的地方，或者看见特别有意思的观点或者知识，想要复制进自己的笔记软件。

正常流程是：
复制文字->打开笔记软件->打开今天的笔记->粘贴；
复制链接->粘贴；
这个流程太过繁琐。

所以使用AutoHotkey简化这一流程，使用[[AutoHotkey\|AutoHotkey]]快速剪藏信息进入[[Cards/Concept/obsidian\|obsidian]]。
#### AutoHotkey

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



#### 什么是AutoHotkey

AutoHotkey是一个windows上的开源软件，用于做自动化的处理，将所有用键盘操作和鼠标点击的事件自动化。

</div></div>

### 演示结果
在即刻网页版，选中文字，按下`ctrl+shift+x`，
按照想要的格式自动复制到Obsidian的今日日记中，
![autohotkey示例.png|500](/img/user/Others/Assets/autohotkey%E7%A4%BA%E4%BE%8B.png)
### 代码编写
注意：以下代码为即刻专用，其他App的暂时没有编写。

设置快捷键
```
+^x:: 
{
}
```
将选中的文字复制，并且在开头添加列表状态，方便在obsidian中形成列表格式。
```
Send  "{Ctrl down}"
Send "c"
Send "{Ctrl up}"
Sleep 100
textNow:=A_Clipboard
textNow := Format("`t- {1}", textNow)
```
进行格式化处理，防止删去所有空行，并且在最后进行列表格式处理。
```
textNow := StrReplace(textNow, "`r`n","`n`n")
textNow := StrReplace(textNow, "`n`n","`n")
textNow := StrReplace(textNow, "`n`n","`n")
textNow := StrReplace(textNow, "`r","`n")
textNow := StrReplace(textNow, "`n","`n`t- ")
```
获取窗口title，并且根据title得到博主名字
```
WinGetPos &X, &Y, &W, &H, "A"
tinTitle := WinGetTitle("A")
owner := StrSplit(tinTitle, ":")[1]
```
根据edge的位置点击链接栏，复制链接
```
if (InStr(tinTitle,"Edge")!=0){
	;获得edge的位置
	WinGetClientPos &X, &Y, &W, &H, "Edge"
	;复制链接
	click X+300+90, Y+20+70
	Sleep 100
	Send  "^c"
	Sleep 100
	link_all := ClipboardAll()
	link:= A_Clipboard
	Sleep 50
}
else{
	isChrome:=0
	link :=tinTitle
	appOld:=tinTitle
}
```
打开obsidian，跳转到今日日记页面。
注意：obsidian应该装有Calendar插件，并且将打开今日日记的快捷键设置为：`shift+ctrl+t`
```
if WinExist("Obsidian")
	WinActivate
else
	{
		Run "C:\\Users\\Kyle\\Desktop\\Obsidian.lnk"
		sleep(500)
	}
Sleep 500
;打开今天的日记
Send  "{Ctrl down}"
Send  "{Alt down}"
Send "t"
Send "{Ctrl up}"
Send  "{Alt up}"
Sleep 300
```
移动到最上行，并且按两个回车+上
```
Send  "{Ctrl down}"
Send "{Home}"
Send "{Ctrl up}"
sleep 100
Send "{Enter}"
sleep 100
Send "{Enter}"
sleep 100
Send "{Up}"
sleep 100
```
最后按照想要的格式将信息粘贴
```
SendInput "- "
; A_Clipboard := "[[即刻post]]"owner
A_Clipboard :=Format("[[即刻post]], [[博主-{1}]]",owner)
Send  "{Ctrl down}"
Send "v"
Send "{Ctrl up}"
Sleep 100
Send "{Enter}"
Send "{Enter}"

A_Clipboard := textNow
Send  "{Ctrl down}"
Send "v"
Send "{Ctrl up}"

Sleep 100

;构建链接
up_name := "链接"
link := Format("[{2}]({1})",link,up_name)
A_Clipboard := link

sleep 50
; MsgBox link
Send "{Enter}"
Send  "{Ctrl down}"
Send "v"
Send "{Ctrl up}"
```
最后返回Edge
```
if WinExist("Edge")
	WinActivate
```
