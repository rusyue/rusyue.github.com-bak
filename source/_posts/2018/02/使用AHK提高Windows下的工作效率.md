---
title: 使用AHK提高Windows下的工作效率
date: 2018-02-20 00:37:06
categories: 工具
tags:
    - AHK
    - AutoHotkey
    - Tools
    - 工具
    - 脚本
    - 效率
---

|   快捷键    |        功能描述       | 快捷键 |       功能描述      |
| :---------: | :-------------------: | :----: | :-----------------: |
|     `m`     |   `Ctrl + S - 保存`   |  `,`   |      `鼠标左键`     |
|     `n`     |   `Ctrl + Z - 撤销`   |  `q`   |      `鼠标左键`     |
|     `z`     |   `Ctrl + Z - 撤销`   |  `.`   |      `鼠标右键`     |
|     `y`     |   `Ctrl + Y - 重做`   |  `e`   |      `鼠标右键`     |
|     `c`     |   `Ctrl + C - 复制`   |  `r`   |      `滚轮向上`     |
|     `v`     |   `Ctrl + V - 粘贴`   |  `f`   |      `滚轮向下`     |
|     `x`     |   `Ctrl + X - 剪切`   |  `h`   |      `退格键`       |
|     `t`     |  `PageUp - 向上翻页`  |  `u`   | `Home - 光标至行首` |
|     `g`     | `PageDown - 向下翻页` |  `o`   | `End - 光标至行尾`  |
|     `w`     |     `向上移动鼠标`    |  `i`   |   `Up - 光标上移`   |
|     `d`     |     `向右移动鼠标`    |  `l`   |  `Right - 光标右移` |
|     `s`     |     `向下移动鼠标`    |  `k`   |  `Down - 光标下移`  |
|     `a`     |     `向左移动鼠标`    |  `j`   |  `Left - 光标左移`  |
| `shift + w` |   `向上快速移动鼠标`  |  `F9`  |      `重载脚本`     |
| `shift + d` |   `向右快速移动鼠标`  | `F10`  |      `编辑脚本`     |
| `shift + s` |   `向下快速移动鼠标`  | `F11`  |      `挂起脚本`     |
| `shift + a` |   `向左快速移动鼠标`  | `F12`  |      `暂停脚本`     |

<!-- more -->

```autohotkey
; =======================================
; 单击 CapsLock 键切换键盘鼠标
; 长按 CapsLock 键切换大写锁定
; =======================================

$CapsLock::
KeyWait, CapsLock
If (A_PriorKey <> "CapsLock")
    return
If (A_TimeSinceThisHotkey > 300)
{
    SetCapsLockState, % GetKeyState("CapsLock", "T") ? "Off" : "On"
    ; Tip("大写锁定: " . (GetKeyState("CapsLock", "T") ? "开启" : "关闭"))
    ShowTIPS("大写锁定: " . (GetKeyState("CapsLock", "T") ? "开启" : "关闭"))
}
Else
{
    CapsLockMode := !CapsLockMode
    ; Tip(CapsLockMode ? "CapsLockMode" : "", "INF", 20, 0, 600)
    ; TIP("键盘鼠标: " . (CapsLockMode ? "开启" : "关闭"))
    ShowTIPS("键盘鼠标: " . (CapsLockMode ? "开启" : "关闭"))
    SetTimer, Beep, -300
    If CapsLockMode
        SetTimer, CapsLockModeTimeOut, 2500
    Else
        SetTimer, CapsLockModeTimeOut, Off
}
Return

CapsLockModeTimeOut:
; ShowTIPS("键盘鼠标: " . A_TimeSinceThisHotkey)
If (A_TimeSinceThisHotkey < 5000)
    return
SetTimer, CapsLockModeTimeOut, Off
CapsLockMode := !CapsLockMode
ShowTIPS("键盘鼠标: " . (CapsLockMode ? "开启" : "超时"))
SetTimer, Beep, -300
Return

; =================================================================
; 按住 CapsLock 键、或者 键盘鼠标 开启时，有如下快捷键：
; =================================================================
; |  快捷键   |       功能描述      | 快捷键 |      功能描述     |
; | :-------: | :-----------------: | :----: | :---------------: |
; |     m     |   Ctrl + S - 保存   |   ,    |      鼠标左键     |
; |     n     |   Ctrl + Z - 撤销   |   q    |      鼠标左键     |
; |     z     |   Ctrl + Z - 撤销   |   .    |      鼠标右键     |
; |     y     |   Ctrl + Y - 重做   |   e    |      鼠标右键     |
; |     c     |   Ctrl + C - 复制   |   r    |      滚轮向上     |
; |     v     |   Ctrl + V - 粘贴   |   f    |      滚轮向下     |
; |     x     |   Ctrl + X - 剪切   |   h    |      退格键       |
; |     t     |  PageUp - 向上翻页  |   u    | Home - 光标至行首 |
; |     g     | PageDown - 向下翻页 |   o    | End - 光标至行尾  |
; |     w     |     向上移动鼠标    |   i    |   Up - 光标上移   |
; |     d     |     向右移动鼠标    |   l    |  Right - 光标右移 |
; |     s     |     向下移动鼠标    |   k    |  Down - 光标下移  |
; |     a     |     向左移动鼠标    |   j    |  Left - 光标左移  |
; | shift + w |   向上快速移动鼠标  |   F9   |      重载脚本     |
; | shift + d |   向右快速移动鼠标  |  F10   |      编辑脚本     |
; | shift + s |   向下快速移动鼠标  |  F11   |      挂起脚本     |
; | shift + a |   向左快速移动鼠标  |  F12   |      暂停脚本     |
; =================================================================
; 需要更多快捷键的话自己添加到下面两个 #If 之间……
; =================================================================

#If CapsLockMode Or GetKeyState("CapsLock", "P")
Up::MouseMove, 0, -1, 0, R    ;w::Send, {Up}
Left::MouseMove, -1, 0, 0, R    ;a::Send, {Left}
Down::MouseMove, 0, +1, 0, R    ;s::Send, {Down}
Right::MouseMove, +1, 0, 0, R    ;d::Send, {Right}
,::LButton
q::LButton
.::RButton
e::RButton
r::MouseClick, WheelUp, , , 3
f::MouseClick, WheelDown, , , 3
t::PgUp
g::Pgdn
i::Up
l::Right
k::Down
j::Left
h::Backspace
u::Home
o::End
w::MoveCursor("w", 1)
a::MoveCursor("a")
s::MoveCursor("s", 1)
d::MoveCursor("d")
+w::MoveCursor("w", 80)
+a::MoveCursor("a", 80)
+s::MoveCursor("s", 80)
+d::MoveCursor("d", 80)
m::^s
n::^z
y::^y
z::^z
c::^c
v::^v
x::^x
F9::Reload
F10::Edit
F11::Suspend
F12::Pause
#If

Beep:
SoundBeep, CapsLockMode ? 1900 : 600, 100
Return
```
