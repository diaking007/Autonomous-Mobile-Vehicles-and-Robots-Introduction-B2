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

[![IMAGE ALT TEXT](https://github.com/diaking007/Autonomous-Mobile-Vehicles-and-Robots-Introduction-B2/blob/main/Task%20III%20Video.png)](https://youtu.be/T5CafZBQyEs)


<details>
<summary><h3>Task III Video<h3></summary>

```
城市輸入

```

</details>
