# 內參校正與手眼校正

## 目的
* 內參校正：校正相機的內部參數矩陣
* 手眼校正：獲得相機到手臂末端點的座標轉換矩陣

## 使用
* ### 內參校正
1. 拍攝不同姿態的棋盤格照片  
(如 eye_hand/innermatrix_calibration/L515_1920_20210515 所示 )
3. 執行 calibration_charuco.py
4. 生成相機內部參數矩陣 (.txt)

> :bulb: 程式內的變數 `img_num` 須設定為照片張數


---

* ### 手眼校正(Hand-Eye Calibration)
1. 開啟機械手臂教導器程式，連線後按下 SMON
2. 執行 camera_eye_hand.py
3. 手臂會自動移動至各個姿態點並拍照
4. 所有姿態點皆拍完照後，會進行手眼校正計算出轉換矩陣 (.txt)

![](https://i.imgur.com/q0f0KA6.jpg)
