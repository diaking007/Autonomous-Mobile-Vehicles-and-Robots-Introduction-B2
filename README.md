# Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2
[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/blob/main/Task%20III%20Video.png)](https://youtu.be/T5CafZBQyEs)


<details>
<summary><h3>Task III Video<h3></summary>

```
城市輸入

```

</details>

## Task 0: build simulation 3D models, layout, and code.  

## Task  I: Pick-n-Place.

[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/assets/136183053/929bb7a8-85b0-4173-9c34-f5de5d19d67e)
](https://youtu.be/ieajvL-u7Sk)


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

## Task III: Integration with I/O box, HMI .

[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/blob/main/Task%20III%20Video.png)](https://youtu.be/T5CafZBQyEs)


<details>
<summary><h3>Task III Video<h3></summary>

```
城市輸入

```

</details>
