# 上銀機械手臂 智慧撞球程式
## :orange_book:如何使用
1. 執行主程式 main.py
2. 出現提示文字 Continue: press c 後，輸入 c 開始程式流程
3. 進行一次撞球 (開啟 SMON 會自動擊球, 或是手動執行 NC code 的 txt 檔)
4. 撞球完畢後手臂回到原位，重複步驟 1 可以繼續打球，或是輸入其他任何字來中斷程式


## :earth_africa:程式流程
### 1. 相機拍照並分別儲存彩色照片 (color.png) 與深度影像 (config/depth.npy)
```
align_depth2color.take_pic()
```
![](https://i.imgur.com/wzxLL4S.png)

> :bulb: Note: 左邊為 RGB 影像, 右邊為深度影像

### 2. 對彩色照片與深度影像進行校正畸變 (會直接覆蓋原始照片)
```
test_undistort.undistort()
```
![](https://i.imgur.com/53jNJMv.jpg)

> :bulb: Note: 校正崎變後的照片，黑邊為校正後的結果


### 3. 找出六個球洞的 pixel 座標 (config/hole.txt)
```
findHole_new.findHole()
```
![](https://i.imgur.com/8DHfp1q.png)

### 4. 找出白球與其他球的 pixel 座標 (config/white_pixel.txt, config/ball_pixel.txt)
```
hough_circle_test.findBall()
```
![](https://i.imgur.com/NgupYDi.jpg)

### 5. 利用球與球洞的座標進行撞球演算法生成結果 (config/result.txt)
```
num_ball, isConvex = hit_ball_strategy.hit_ball_strategy()
```
![](https://i.imgur.com/CBxhUng.jpg)

### 6. 生成之結果進行座標轉換，生成機械手臂的 NC code
```
coordinate_transformation.coordinate_transformation(num_ball, isConvex)
```
![](https://i.imgur.com/TnaJwpb.png)


## :hammer:與機械手臂溝通 (讓手臂自動打撞球)
1. 開啟控制手臂程式，按下 SMON，程式會偵測 C:\RobotStateMachine\SM_ON_OFF_File.txt 為 0 或 1
2. 若是 0 ，則不會啟動；若是 1，則執行 HIWIN ROBOT NC CODE.txt ，執行完畢後自動改回 0
3. 程式流程第六點在生成新的 NC code 後，會將 SM_ON_OFF_File.txt 改為 1，讓手臂自動執行

![](https://i.imgur.com/7O9CLiL.png)

## :mag_right:實作影片

若有想看更多完整的步驟與程式流程可以點擊下方網址:

:point_right:  https://youtu.be/1msCYlrSwBo