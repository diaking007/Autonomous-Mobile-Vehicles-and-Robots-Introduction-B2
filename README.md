# Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2

## Task 0: build simulation 3D models, layout, and code.  
![image](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/a7d1140b-d149-4470-b54e-3de3fb535beb)

## Task  I: Pick-n-Place.
### Task I Simuation Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/929bb7a8-85b0-4173-9c34-f5de5d19d67e)
](https://youtu.be/ieajvL-u7Sk)

### Task I Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/41ded7bd-3865-41ec-afea-7a7fc23c4d3f)
](https://youtu.be/GHq2T_IGxhY)

<details>
<summary><h3>Task I Code<h3></summary>

```
Integer Tokens
Integer Blocks
Integer B
Integer T
Double TokenHeigh
Double BlockHeigh
Function task1

Motor On
Power High
Speed 50
Accel 50, 50
SpeedS 200
AccelS 5000
Tool 1

Tokens = 0
Blocks = 0
B = 2
T = 2
TokenHeigh = 6.0
BlockHeigh = 6.0
Integer TokenID
Integer BlockID

Go Retract_Safe

For TokenID = T To 0 Step -1
	Pick_Infeed_Token()
	Alignment_Token()
	Place_Tray_Token()
	T = T - 1
Next TokenID

For BlockID = B To 0 Step -1
	Pick_Infeed_Block()
	Alignment_Block()
	Place_Tray_Block()
	B = B - 1
Next BlockID

Go Retract_Safe

Fend

Function Pick_Infeed_Token
	'Pick Token from Infeed
	Print "Picking Token from Infeed. Token ID = ", Tokens
    Go B2_Infeed_Tsafe +Z(-25) +X(156) +Y(115) /3 CP
	'圓形安全點
	On 8
	Move B2_Infeed_Tsafe +Z(-59 - (Tokens * TokenHeigh)) +X(156) +Y(115) /3 CP
	'取圓形
	Wait .2
	Go B2_Infeed_Tsafe +Z(-50) +X(156) +Y(115) /3 CP
	'回圓形安全點
	Go B2_Infeed_Tsafe +Z(-50) +X(90) +Y(115) /3 CP
	'取後安全點
Fend

Function Pick_Infeed_Block
	'Pick Block from Infeed
	Print "Picking Block from Infeed. Block ID = ", Blocks
	
	Go B2_Infeed +Z(47) +X(185.5) +Y(111.5) /3 CP
	'方形安全點
	On 8
	Move B2_Infeed +Z(17.5 - (Blocks * BlockHeigh)) +X(185.5) +Y(111.5) /3 CP
	'取方形
	Wait .2
	Go B2_Infeed +Z(47) +X(185) +Y(111.5) /3 CP
	'回方形安全點
    Go B2_Infeed +Z(47) +X(117.5) +Y(111.5) /3 CP
	'取後安全點
Fend
Function Alignment_Token
	'Alignment Token
	Print "Aligning Token. Token ID = ", Tokens
	'Go B2_Align +Z(12) +X(84) +Y(50.5) /2
	'校正安全點
	Go B2_Align +Z(6) +X(84) +Y(50.5) /2
	'放下校正點
	Move B2_Align +Z(6) +X(88) +Y(50.5) /2
    '推
    Off 8
    Wait 0.3
    Go B2_Align +Z(10) +X(88) +Y(51) /2
   '抬起
    Go B2_Align +Z(10) +X(88.5) +Y(51) /2
   '推後正中取上方
    On 8
    Move B2_Align +Z(6) +X(88.5) +Y(51) /2
   '推後正中取
    Go B2_Align +Z(15) +X(88.5) +Y(51) /2
   '推後正中取後
Fend

Function Alignment_Block
	'Alignment Block
	Print "Aligning Block. Block ID = ", Blocks
	'Go B2_Align +Z(14) +X(89) +Y(26) /2
   '校正安全點
    Go B2_Align +Z(6) +X(89) +Y(27) /2
    '放下校正點
    Move B2_Align +Z(6) +X(93.5) +Y(27.5) /2
   '推
   Off 8
   Wait 0.3
   Go B2_Align +Z(10) +X(93.5) +Y(27.5) /2
   '推完上方
   Go B2_Align +Z(10) +X(93) +Y(27.5) /2
   '推後正中取上方
   On 8
   Move B2_Align +Z(6) +X(93) +Y(27.5) /2
   '推後正中取
   Go B2_Align +Z(15) +X(93) +Y(27.5) /2
   '推後正中取上方
Fend
Function Place_Tray_Token
	'Tray Token
	Print "Placing Token in Tray. Tray Position ID = ", Tokens
	Go Tray +Z(10) +X(95) +Y(-54 + (30. * Tokens)) /1
    '圓形放置上方
    Go Tray +Z(0) +X(95) +Y(-54 + (30. * Tokens)) /1
    '圓形放置
    Off 8
	Wait 0.2
	'放置
	Go Tray +Z(10) +X(95) +Y(-54 + (30. * Tokens)) /1
	'圓形放置上方
	Tokens = Tokens + 1
Fend
Function Place_Tray_Block
	'Tray Block
	Print "Placing Block in Tray. Block Position ID = ", Blocks
	Go Tray +Z(10) +X(65) +Y(-52.5 + (30. * Blocks)) /1
    '方形放置上方
    Go Tray +Z(0) +X(65) +Y(-52.5 + (30. * Blocks)) /1
   '方形放置
	Off 8
	Wait .2
	'放置
	Go Tray +Z(10) +X(65) +Y(-52.5 + (30. * Blocks)) /1
	'放置安全點
	Blocks = Blocks + 1
Fend

```

</details>

## Task II: Stacking .
### Task II Simuation Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/33f44b01-d35e-4ef7-9ca7-73ead0b33a13)
](https://youtu.be/Mx_2KzGobEc?si=jRAcQ1cFjPl_ZIlT)

### Task II Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/952bf45e-4bc4-4181-8e02-4896a7219b8c)
](https://youtu.be/Eb1DDYEBGuA?si=vRkxmAY_--cjCTe6)

<details>
<summary><h3>Task II Code<h3></summary>

```
Integer Tokens
Integer Blocks

Integer BT

Integer tower
Double TokenHeigh
Double BlockHeigh
Function task2

Motor On
Power High
Speed 100
Accel 60, 60
SpeedS 800
AccelS 6000
Tool 1

BT = 5
Tokens = 0
Blocks = 0
TokenHeigh = 6.0
BlockHeigh = 6.0
tower = 0
Integer BlockID

Go Retract_Safe

For BlockID = BT To 0 Step -1
	Pick_Infeed_Block2()
	Alignment_Block2()
	Pick_Infeed_Token2()
	Alignment_Block2()
	Tokens = Tokens + 1
	Blocks = Blocks + 1
	BT = BT - 1
Next BlockID
Go Retract_Safe
Fend
Function Pick_Infeed_Token2
	'Pick Token from Infeed
	Print "Picking Token from Infeed. Token ID = ", Tokens
    Go B2_Infeed_Tsafe +Z(-20 - (Tokens * TokenHeigh)) +X(156) +Y(115) /3 CP
	'圓形安全點
	On 8
	Go B2_Infeed_Tsafe +Z(-49.5 - (Tokens * TokenHeigh)) +X(156) +Y(115) /3 CP
	'取圓形
    Go B2_Infeed_Tsafe +Z(-20) +X(156) +Y(115) /3 CP
	'回圓形安全點
Fend
Function Pick_Infeed_Block2
	'Pick Block from Infeed
	Print "Picking Block from Infeed. Block ID = ", Blocks
	Go B2_Infeed +Z(43 - (Blocks * BlockHeigh)) +X(185.5) +Y(111.5) /3 CP
	'方形安全點
	On 8
	Go B2_Infeed +Z(29 - (Blocks * BlockHeigh)) +X(185.5) +Y(111.5) /3 CP
	'取方形
	Go B2_Infeed +Z(43) +X(185) +Y(111.5) /3 CP
	'回方形安全點
Fend
Function Alignment_Block2
	'Alignment Block
   Print "Aligning Block. Block ID = ", Blocks
   Go B2_Align +Z(20 + (tower * BlockHeigh)) +X(92.5) +Y(27) /2
   '放置上方
   Go B2_Align +Z(4.5 + (tower * BlockHeigh)) +X(92.5) +Y(27) /2
   '放置
   Off 8
   Wait 0.1
   Go B2_Align +Z(20 + (tower * BlockHeigh)) +X(92.5) +Y(27) /2
   '放置後上抬
   tower = tower + 1
Fend

```

</details>

## Task III: Integration with I/O box, HMI .
### 3.1 
1.一開始是正常的疊疊樂<p>
2.用到緊急狀況終止Or遇到停電<p>
3.按下紅色，代表發生狀況<p>
4.檢查方的、圓的用了幾個<p>
5.用幾個就按幾下<p>
6.最後繼續<p>

### Task 3.1 Simuation Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/52cfdb90-fcf4-4337-a02a-c9468643c2b8)
](https://youtu.be/L3rI8qH2acw?si=6q4mtk-vnBReiUEP)

### Task 3.1 Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/8ce32a3b-a272-4ab2-9078-ca2eefcc99d0)
](https://youtu.be/L3rI8qH2acw)


<details>
<summary><h3>Task 3.1 Code<h3></summary>

```
Integer Tokens
Integer Blocks
Integer BT
Integer tower
Integer BlockID
Integer button_press_count_B
Integer button_press_count_T
Integer timer_B
Integer timer_T
Double TokenHeigh
Double BlockHeigh

Function task3
	
Motor On
Power High
Speed 10
Accel 10, 10
SpeedS 10
AccelS 10
Tool 1

BT = 5
Tokens = 0
Blocks = 0
TokenHeigh = 6.0
BlockHeigh = 6.0
tower = 0
button_press_count_B = 0
button_press_count_T = 0
timer_B = 0
timer_T = 0

Go B2_Infeed_Tsafe +Z(-25) +X(64) +Y(30) /3
 
If Sw(4) = On Then
	Print("")
	Check_B_Num()
	Check_T_Num() '如果亮了代表有斷電過
Else
	Print "Keep Moving~!"
EndIf


If tower = 1 Or tower = 3 Or tower = 5 Or tower = 7 Or tower = 9 Or tower = 11 Then
	For BlockID = BT To 0 Step -1
		Pick_Infeed_Token3()
		Alignment_Block3()
		If Blocks < 6 Then
			Pick_Infeed_Block3()
			Alignment_Block3()
			Blocks = Blocks + 1
		EndIf
		Tokens = Tokens + 1
		BT = BT - 1
		Print BT
	Next BlockID
ElseIf tower = 0 Or tower = 2 Or tower = 4 Or tower = 6 Or tower = 8 Or tower = 10 Then
 	For BlockID = BT To 0 Step -1
		Pick_Infeed_Block3()
		Alignment_Block3()
		Pick_Infeed_Token3()
		Alignment_Block3()
		Tokens = Tokens + 1
		Blocks = Blocks + 1
		'BT = BT - 1
	Next BlockID
EndIf


Go B2_Infeed_Tsafe +Z(-25) +X(64) +Y(30) /3
Fend
Function Check_B_Num
 '' 進入迴圈，設定條件為按鈕次數小於等於5且計時器小於5000（5秒）
Do While button_press_count_B <= 6 And timer_B < 2
Print "!!!!!!!!!! Check the Blocks_Quantity !!!!!!!!!!"
  		Wait 2.0 '等一秒給按圓的
	If Sw(7) = On Then
    '按下按鈕，增加按鈕次數並重置計時器
		button_press_count_B = button_press_count_B + 1
		Print "Blocks=", button_press_count_B
		timer_B = 0
        Wait 0.1  ' 等待一小段時間以避免連續偵測到按鈕
	Else
	' 如果按鈕沒有按下，增加計時器
		timer_B = timer_B + 1  ' 假設每100毫秒加100
        Wait 0.1
    EndIf
Loop
Fend
Function Check_T_Num
  	Do While button_press_count_T <= 6 And timer_T < 2
  		Print "!!!!!!!!!! Check the Tokens_Quantity !!!!!!!!!!"
  		Wait 2.0 '等一秒給按圓的
       If Sw(0) = On Then
          ' 按下按鈕，增加按鈕次數並重置計時器
           button_press_count_T = button_press_count_T + 1
           Print "Tokens=", button_press_count_T
           timer_T = 0
           Wait 0.1  '等待一小段時間以避免連續偵測到按鈕
       Else
          ' 如果按鈕沒有按下，增加計時器
           timer_T = timer_T + 1  '假設每100毫秒加100
           Wait 0.1
       EndIf
  Loop

If button_press_count_B = 0 Then
	Print "No power outage."
EndIf
If button_press_count_B = 1 Then
'如果方的少1個
	If button_press_count_T = 0 Then
		BT = BT
   		Blocks = Blocks + 1
   		Tokens = Tokens
  		tower = tower + 1
	ElseIf button_press_count_T = 1 Then
		BT = BT - 1
   		Blocks = Blocks + 1
   		Tokens = Tokens + 1
   		tower = tower + 2
  	EndIf
EndIf
If button_press_count_B = 2 Then
' 如果方的少2個
     If button_press_count_T = 1 Then
		BT = BT - 1
   		Blocks = Blocks + 2
   		Tokens = Tokens + 1
  		tower = tower + 3
	 ElseIf button_press_count_T = 2 Then
		BT = BT - 2
   		Blocks = Blocks + 2
   		Tokens = Tokens + 2
   		tower = tower + 4
  	EndIf
EndIf
If button_press_count_B = 3 Then
' 如果方的少3個
	If button_press_count_T = 2 Then
		BT = BT - 2
   		Blocks = Blocks + 3
   		Tokens = Tokens + 2
  		tower = tower + 5
	ElseIf button_press_count_T = 3 Then
		BT = BT - 3
   		Blocks = Blocks + 3
   		Tokens = Tokens + 3
   		tower = tower + 6
  	EndIf
EndIf
If button_press_count_B = 4 Then
' 如果方的少4個
	If button_press_count_T = 3 Then
		BT = BT - 3
   		Blocks = Blocks + 4
   		Tokens = Tokens + 3
  		tower = tower + 7
	ElseIf button_press_count_T = 4 Then
		BT = BT - 4
   		Blocks = Blocks + 4
   		Tokens = Tokens + 4
   		tower = tower + 8
  	EndIf
EndIf
If button_press_count_B = 5 Then
' 如果方的少5個
	If button_press_count_T = 4 Then
		BT = BT - 4
   		Blocks = Blocks + 5
   		Tokens = Tokens + 4
  		tower = tower + 9
	ElseIf button_press_count_T = 5 Then
		BT = BT - 5
   		Blocks = Blocks + 5
   		Tokens = Tokens + 5
   		tower = tower + 10
  	EndIf
EndIf
If button_press_count_B = 6 Then
' 如果方的少6個
	If button_press_count_T = 5 Then
		BT = BT - 5
   		Blocks = Blocks + 6
   		Tokens = Tokens + 5
  		tower = tower + 11
	ElseIf button_press_count_T = 6 Then
		BT = BT - 6
   		Blocks = Blocks + 6
   		Tokens = Tokens + 6
   		tower = tower + 12
   		Print "All Done."
  	EndIf
EndIf
Print "tower:", tower
Print "BT:", BT
Fend
Function Pick_Infeed_Token3
	'Pick Token from Infeed
	Print "Picking Token from Infeed. Token ID = ", Tokens
    Go B2_Infeed_Tsafe +Z(-25) +X(90) +Y(34) /3 CP
	'圓形安全點
	On 8
	Move B2_Infeed_Tsafe +Z(-43.5 - (Tokens * TokenHeigh)) +X(90) +Y(34) /3 CP
	'取圓形
	'Wait .3
	Go B2_Infeed_Tsafe +Z(-25) +X(85) +Y(34) /3 CP
	'回圓形安全點
	Go B2_Infeed +Z(70) +X(144) +Y(70) /3 CP
	'回方形安全點
Fend

Function Pick_Infeed_Block3
	'Pick Block from Infeed
	Print "Picking Block from Infeed. Block ID = ", Blocks
	
	Go B2_Infeed +Z(50) +X(118.5) +Y(29) /3 CP
	'方形安全點
	On 8
	Move B2_Infeed +Z(33.5 - (Blocks * BlockHeigh)) +X(118.5) +Y(29) /3 CP
	'取方形
	'Wait .3
	Go B2_Infeed +Z(55) +X(114) +Y(29) /3 CP
	'回方形安全點
	Go B2_Infeed +Z(70) +X(144) +Y(70) /3 CP
	'回方形安全點
Fend

Function Alignment_Block3
	'Alignment Block
   Print "Aligning Block. Block ID = ", Blocks

   Go B2_Align +Z(10 + (tower * BlockHeigh)) +X(90) +Y(26) /2
   '放置上方
   Go B2_Align +Z(3.5 + (tower * BlockHeigh)) +X(90) +Y(25.5) /2
   '放置
   Off 8
   Wait 0.1
   Go B2_Align +Z(5 + (tower * BlockHeigh)) +X(90) +Y(25.5) /2
   '放置後上抬
   Go B2_Align +Z(20 + (tower * BlockHeigh)) +X(70) +Y(25.5) /2
   tower = tower + 1
Fend

```

</details>

### 3.2 
做一個Tray 有傾斜角30度，一樣放料的環節
### Task 3.2 Video
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/c440efb1-8d08-4c93-9136-61b5c9a9b5f0)
](https://youtu.be/4oapPF_Quws)
<details>
<summary><h3>Task 3.2 Code<h3></summary>

```
Integer Tokens
Integer Blocks
Integer B
Integer T
Double TokenHeigh
Double BlockHeigh
Function task4

Motor On
Power High
Speed 60
Accel 60, 60
SpeedS 400
AccelS 5000
Tool 1

Tokens = 0
Blocks = 0
B = 2
T = 2
TokenHeigh = 6.0
BlockHeigh = 6.0
Integer TokenID
Integer BlockID

Go B2_Infeed_Tsafe +Z(-25) +X(156.5) +Y(111) /3 CP

For TokenID = T To 0 Step -1
	Pick_Infeed_Token4()
	Alignment_Token4()
	Place_Tray_Token4()
	Tokens = Tokens + 1
	T = T - 1
Next TokenID

For BlockID = B To 0 Step -1
	Pick_Infeed_Block4()
	Alignment_Block4()
	Place_Tray_Block4()
	Blocks = Blocks + 1
	B = B - 1
Next BlockID

Go B2_Infeed_Tsafe +Z(-25) +X(156.5) +Y(111) /3 CP

Fend

Function Pick_Infeed_Token4
	'Pick Token from Infeed
	Print "Picking Token from Infeed. Token ID = ", Tokens
    Go B2_Infeed_Tsafe +Z(-25) +X(156.5) +Y(111) /3 CP
	'圓形安全點
	On 8
	Go B2_Infeed_Tsafe +Z(-69.5 - (Tokens * TokenHeigh)) +X(156) +Y(111) /3 CP
	'取圓形
	Wait .1
	Go B2_Infeed_Tsafe +Z(-25) +X(156.5) +Y(111.5) /3 CP
	'回圓形安全點
	Go B2_Infeed_Tsafe +Z(-25) +X(104.5) +Y(111.5) /3 CP
	'取後安全點
Fend

Function Pick_Infeed_Block4
	'Pick Block from Infeed
	Print "Picking Block from Infeed. Block ID = ", Blocks
	
	Go B2_Infeed +Z(47) +X(184.5) +Y(108) /3 CP
	'方形安全點
	On 8
	Go B2_Infeed +Z(6 - (Blocks * BlockHeigh)) +X(184.5) +Y(108) /3 CP
	'取方形
	Wait .1
	Go B2_Infeed +Z(47) +X(184.5) +Y(108) /3 CP
	'回方形安全點
    Go B2_Infeed +Z(47) +X(114.5) +Y(108) /3 CP
	'取後安全點
Fend
Function Alignment_Token4
	'Alignment Token
	Print "Aligning Token. Token ID = ", Tokens
	Go B2_Align +Z(10) +X(87) +Y(46.8) /2
	'校正安全點
	Go B2_Align +Z(3.5) +X(87) +Y(46.8) /2
	'放下校正點
	Go B2_Align +Z(3.5) +X(88.2) +Y(46.8) /2
    '推
    Off 8
    Wait 0.1
    Go B2_Align +Z(10) +X(88.2) +Y(46.8) /2
   '抬起
    Go B2_Align +Z(10) +X(88.2) +Y(46.8) /2
   '推後正中取上方
    On 8
    Go B2_Align +Z(3) +X(88.2) +Y(46.8) /2
   '推後正中取
    Go B2_Align +Z(50) +X(88.5) +Y(46.5) /2
   '推後正中取後
Fend

Function Alignment_Block4
	'Alignment Block
	Print "Aligning Block. Block ID = ", Blocks
	Go B2_Align +Z(15) +X(92) +Y(24) /2
   '校正安全點
    Go B2_Align +Z(3) +X(92) +Y(24) /2
    '放下校正點
    Move B2_Align +Z(3) +X(92) +Y(24) /2
   '推
   Off 8
   Wait 0.1
   'Go B2_Align +Z(10) +X(94) +Y(24) /2
   '推完上方
   Go B2_Align +Z(15) +X(92.5) +Y(24) /2
   '推後正中取上方
   On 8
   Go B2_Align +Z(2.8) +X(92.5) +Y(24) /2
   '推後正中取
   Go B2_Align +Z(30) +X(92.5) +Y(24) /2
   '推後正中取上方
Fend
Function Place_Tray_Token4
	'Tray Token
	Print "Placing Token in Tray. Tray Position ID = ", Tokens
    Go B2_Infeed_Tsafe +Z(-70) -X(15.35) +Y(-8.5 + (30. * Tokens)) /4 CP
    '圓形放置上方
    Go B2_Infeed_Tsafe +Z(-78) -X(15.35) +Y(-8.5 + (30. * Tokens)) /4 CP
    '圓形放
    Wait 0.2
    Off 8
	Wait 0.1
	'放置
    Go B2_Infeed_Tsafe +Z(-70) -X(15.35) +Y(-8.5 + (30. * Tokens)) /4 CP
	'圓形放置上方
	
Fend
Function Place_Tray_Block4
	'Tray Block
	Print "Placing Block in Tray. Block Position ID = ", Blocks
    Go B2_Infeed_Tsafe +Z(-69) +X(14.7) +Y(-6.7 + (30. * Blocks)) /4 CP
    '方形放置上方
    Go B2_Infeed_Tsafe +Z(-77.5) +X(14.7) +Y(-6.7 + (30. * Blocks)) /4 CP
   '方形放置
    Wait 0.2
	Off 8
	Wait .1
	'放置
    Go B2_Infeed_Tsafe +Z(-79) +X(14.74) +Y(-6.7 + (30. * Blocks)) /4 CP
	'方形放置安全點

Fend

```

</details>

### Task 3.2 CAD
斜板
![image](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/3b29a4a9-b755-46ff-8be8-2fb3e74b1f3f)
![image](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/dc8a3b65-f908-489a-9972-039dacb2627a)
![image](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/cd388447-59ef-49c6-9a99-b04808633b0a)
![image](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/3375f96f-c042-46e1-a3c4-81223dd58e37)


