### 利用Pyautocad批量打开并替换CAD文件(.dwg)中文字或特定字符
#### 遇到的问题
- 纯Python代码运行速度缓慢, 特别是进行多个文件中特定文字的批量替换时, 反倒不如CAD自带的find命令好用,唯一不足的是find命令需要手动输入并点击.

#### 目前已有思路
- 参考*[Autocad社区里的这篇帖子]*(https://forums.autodesk.com/t5/visual-lisp-autolisp-and-general/how-to-interface-with-autocad-from-python/td-p/9760099), 利用SendCommand运行AutoLisp命令, 结合Python代码, 将要替换的文字或者特定字符以AutoLisp参数的形式传递到SendCommand中的AutoLisp代码中. 从而实现文字或者字符的快速自动替换. 
