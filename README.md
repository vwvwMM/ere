# 109-2 電資工程入門設計與實作 第八組

## 成員
* 班別：週一班
* 組別：第八組《儒生女巫用苡枝千鈞重的羽毛筆畫蕎薇》
* 組員1：李蕎羽、B09901010
* 組員2：廖苡鈞、B09901014
* 組員3：巫竑儒、B09901072

---

## 第五週紀錄 - 組車
* 課堂應完成事項(**下課前必須找助教檢查**)
    * 車子組裝完成Part 1(前側柱、馬達座)
    * 車子組裝完成Part 2(下盤)
    * 車子組裝完成Part 3(中盤)
    * 車子組裝完成Part 4(上蓋)
    * 車子通電可動作
> 給助教檢查[name=助教姓名]
> 車體完成
> 電源完成
> 接線完成
3/24晚上助教蔡昀哲

* 實際達成事項 (必填)
    * 車子組裝完成Part1~2+接線完成至左右馬達的部分(週一課堂上)
    * 課後完成RFID、紅外線模組、藍芽、L298N接線及頂板組裝
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 問題:鎖左右板時10mm的螺絲不夠長，鎖不起來
    * 問題:投影片第52頁跟第53頁對RFID鎖螺絲的部分不一致，52頁只出現了一次螺帽，但53頁出現了兩次
    * 問題：第一次測試紅外線模組接D0,燈未亮
    * 問題：RFID的reset不確定要接哪
* 組員分工 (必填)
    * 李蕎羽:組裝車子、焊接插頭
    * 廖苡鈞:組裝車子、焊接開關
    * 巫竑儒:焊接馬達、準備器材
* 遇到問題之處理狀況、解決方式 (必填)
    * 以更長的15mm螺絲取代
    * 經觀察過後，發現應該要鎖兩個螺帽，才能使得RFID不會卡到螺絲
    * 不確定0-13GVS對應到原本的Arduino板為何 經詢問助教,V、G皆為連通 角位和S有關
    * 將紅外線模組改成接A0 燈亮起
    * RFID的reset 依據自行設定接到角位9
* 課程建議 (選填)
    * 簡報可以按照組裝的順序擺放 ex:馬達的部分也許可以擺在電源前面
* 想說的話 (選填)
    * 謝謝教授和學長姐們不斷的更新車體的結構，讓車子看起來更美觀也更簡潔 :+1:

## 第五週批閱區 - 組車
* 助教批閱欄
    * 助教回饋
        * 整體建議可以寫更詳細一點哦（補一些圖之類的
        * 在編排上面，問題和解決方式可以擺在一起，會比較易讀喔~ :+1: 
> [name=周奕慧]
* 教授批閱欄
    * 評分等第: `B+`
    * 教授回饋
        * 基本的工作都有記錄了，但遇到的問題與嘗試的解法如果能寫在一起會更好讀唷~
        > [name=蘇柏青]

## 第六週紀錄 - 循跡
* 課堂應完成事項(**下課前必須找助教檢查**)
    * 可不輔助、不出軌，連續繞行橢圓狀地圖2圈
> 給助教檢查：有完整走過一圈，但不穩定。 [name=周奕慧]
> 3/31 openlab
> 有做出P control
> C型地圖有跑完
> [name=蔡昀哲]
> 
* 實際達成事項 (必填)
    * 用P-control做出循跡功能，讓車車能走完C型地圖
    * 用PD-control做出循跡功能，讓車車能走完C型地圖
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 我們討論了P-control那些參數分別代表何種意義，結論如下:
      1.w1~w5分別代表五個紅外線感測器讀值的權重
      2.w3越大代表在大轉彎(只有最邊邊讀到值)的時候可以轉越多
      3.w3+w2越大代表在中等轉彎(最邊邊兩個有讀到，中間沒有)的時候可以轉越多
      4.w2越大代表在小轉彎(中間跟他旁邊的有讀到)的時候可以轉越多
      5.Kp為比例常數，數值越大，兩輪轉速差越多，轉得越多
      6._Kd越大，誤差調整的影響比例越大，但我們認為仍須以當下讀值的情況為準，故_Kd不應該太大，應該只能當修正項作微調的工作
      7.Tp越大，車子總體而言跑的就越快
    * 附上實際循跡的code:
      ![](https://i.imgur.com/fsK5TpC.png)

* 組員分工 (必填)
    * 大家一起討論各項參數所代表的意義、尋找車子在循跡的時候有哪些問題、決定如何調整參數:+1:
* 遇到問題之處理狀況、解決方式 (必填)
    * 我們一開始寫的演算法是如果五個紅外線感應器都沒有讀到值(衝出軌道的時候)就執行上一個動作(通常是大轉，因為車子脫離軌道時最後一刻必然是最邊邊的感測器有讀值，另外四個沒有，此時他會做大轉)而這會出現一個很酷的現象，就是我們的車子會衝出軌道之後做一個大迴旋，最後接回軌道。雖然我們覺得這個能力超強，但為了順暢度我們後來想到另一個方法可以讓車子不要衝出軌道那麼多，就是把甚麼都沒讀到的動作改成倒退。如此一來他在剛衝出軌道的時候就會退回來了。
    * 這裡附上原本(五個都無讀值就執行上個動作)的code:
     ![](https://i.imgur.com/4sXijcz.png)
     ![](https://i.imgur.com/GbLHN52.png)
    這是還在窮舉法的時候，findpath這個函式會回傳現在遇到的是甚麼情況，分別回傳不同的值，因此我們在loop呼叫findpath時switch他的回傳值做出相對應的動作。
    * 改成倒退也遇到一個問題，就是他五個都沒讀到值發生的次數比我們想像中來的多，因此他會常常前後來回走，但這不太影響車車走完整個軌道的可行性，只是走起來會花比較多時間，也比較卡而已，為了使他更順我們還會繼續調整參數。
    * 偶爾會遇到車子停著不動的問題，猜測為給馬達運轉的力量不夠導致，所以我們一直加大Tp，但這又會造成在彎道時車速過快，紅外線感測器讀值雖顯示應要轉彎，但車子來不及而沿切線方向駛離軌道，這之間的trade off我們還在調整。
    * 車子測試期間走得不太順暢，發現其中一個萬向輪有瑕疵，因此我們改將另一完好的萬向輪鎖於車子中間。
    * 這裡附上我們車車的影片:
      橢圓軌道：https://youtu.be/x5SBpgGMPiM
      進階軌道：https://youtu.be/hRhR0JgkSE8
      PID control：
      橢圓軌道：https://youtu.be/h55GYD1mqco
      進階軌道：https://youtu.be/XAVwKQqNQMs
      
     
      
      
    
* 課程建議 (選填)
    * 教授感覺是想要一步一步帶著我們完成循跡，我們也覺得這樣挺好的。但是整個課程的時間太短，內容又有點多，導致我們可以實際操作和思考的時間有點短，而在前面那一部分還沒完成的情況下，其實有點難再回過神去繼續聽教授講解下一部分，所以課程的後半段會有點沒跟上教授的腳步。還有希望教授可以在課後給我們學生版ppt上所沒有的投影片，如果教授願意的話~
* 想說的話 (選填)
    * 其實倒退還有一個好處，就是他遇到軌道大轉彎時會一點一點地用倒退來修正方向，看起來像小寶寶在探索一樣，好可愛><

## 第六週批閱區 - 循跡
* 助教批閱欄
    * 助教回饋
    * 看到你們很認真的在解決問題，很棒:+1:
    * 也許可以觀察一下，車子在什麼情況較容易跑出軌道，是該左轉的時候轉不夠多，還是該右轉的時候轉不夠多?假設大部分情況是該右轉的時候轉不夠多，可以嘗試什麼都沒讀到時讓車子緩慢的右轉，直到重新掃到黑色，再繼續循跡，反之亦然。這樣就不用一直前前後後。
    * 你們紀錄非常詳細，繼續保持!
> [name=俞建琁]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]


## 第八週紀錄 - 指定題介紹
* 課堂應完成事項(**下課前必須找助教檢查**)
    * 問題0回答:6Vx180ma=1.08W、答案訂正
    * 問題1回答:1-1:200m+33m+75mx5+86m+1.08x2+驅動模組耗能+降壓模組耗能；1-2:功率/11.1；1-3:2250/電流(mA)、答案訂正:200m+33m+75mx5+86m+1.08x2=2.854W，降壓模組跟驅動模組在設計的時候就已經盡量降低耗能，故可以忽略；1-2:2.854/11.1=0.257(A)；1-3:2250/257=8.75(h)
    * 問題2回答:2-1:每個node用001~150的整數表示，然後將distance直接加在這三個數字前，如此就可以只用1個整數來記錄一個鄰居和距離，然後利用list的index可以當作這是第幾個node的adjacent list 資料，例如當我們在看編號009的node時，編號102是他的鄰居，距離19，009的adjacent list就可以記成19102，然後在最壞的情況下每個node旁邊都有四個鄰居，故4x150x2=1200；2-2:在BFS中需要紀錄哪些點已用過，最壞的情況是終點在最後一個被找到，故需要額外存150x2 bytes；2-3:都可以、答案訂正:2-2:BFS中還需要mark跟predecessor，各存150個node，共需要600 bytes；2-3:若加上那600 byte，地圖加BFS共需2100 bytes，這樣就裝不下了。
    * 問題3回答:3-1:4x8/0.1=320(bits/sec)=40(bytes/sec)、答案訂正:3-1:通知看到跟接收指令各還須1 byte，分別做上傳跟下載，故應為60 bytes/sec
    * 完成甘特圖
    * 完成系統方塊圖
> 給助教檢查[name=助教姓名]
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第八週批閱區 - 指定題介紹
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十週紀錄 - 指定題進度報告
* 預計完成事項 (必填)
    * 待填
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十週批閱區 - 指定題進度報告
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十一週紀錄 - 指定題進度檢視
- CHECKPOINTS
    - 車車
        - [ ] 循跡
		- [ ] 可以偵測到 node（包含十字路口和死巷）
		- [ ] 偵測到 node 之後，穩定直走、轉彎、迴轉（寫死指令）
		- [ ] 可以接收來自電腦的藍芽指令

	- python
		- [ ] 完成基本的 BFS
		- [ ] 完成第一題的設計
		- [ ] 可以透過藍芽傳輸指令

	- combined
		- [ ] 可以讀取 RFID 的值
		- [ ] 能走完 3 個點
		- [ ] 可以不輔助的情況下，完成小型 E 字地圖
		- [ ] 可以不輔助的情況下，完成進階地圖
		- [ ] 可以正確在死巷讀取 RFID
> 給助教檢查[name=助教姓名]

* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十一週批閱區 - 指定題進度檢視
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十二週紀錄 - 指定題競賽
* 預計完成事項 (必填)
    * 待填：預期表現？
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十二週批閱區 - 指定題競賽
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十三週紀錄 - 自選題介紹
* 預計完成事項 (必填)
    * 待填
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十三週批閱區 - 自選題介紹
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十四週紀錄 - 自選題proposal報告
* 預計完成事項 (必填)
    * 待填
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十四週批閱區 - 自選題proposal報告
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十五週紀錄 - 自選題進度報告
* 預計完成事項 (必填)
    * 待填
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十五週批閱區 - 自選題進度報告
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

## 第十六週紀錄 - 自選題進度報告
* 預計完成事項 (必填)
    * 待填
* 實際達成事項 (必填)
    * 待填
* 組內討論事項 (必填，如問題、構想、分工合作、時間安排...等等)
    * 待填
* 組員分工 (必填)
    * 待填
* 遇到問題之處理狀況、解決方式 (必填)
    * 待填
* 課程建議 (選填)
    * 待填
* 想說的話 (選填)
    * 待填

## 第十六週批閱區 - 自選題進度報告
* 助教批閱欄
    * 助教回饋
> [name=助教姓名]
* 教授批閱欄
    * 評分等第
    * 教授回饋
> [name=教授姓名]

###### tags: `電資工程入門設計與實作` `109-2`
