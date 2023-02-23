這個脚本主要幫助一個網友實現定時平倉的功能。這是一個定時平倉的脚本，它可以在設定的每天的任何時候發出平倉信號，比如：在你睡覺的時候，在你工作的時候，將他連接到TVCBOT交易機器人的市價全平訊號，即可實現定時平倉。  
以下是自動平倉的代碼，請將該代碼通過tradingview的pine編輯器保存，然後再將它添加到圖表中。  


```python
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © blockplus

//@version=5
indicator("TVCBOT定時平倉", overlay=true)
h = input.int(00, "平倉小時", minval=0, maxval=23, step=1)
m = input.int(00, "平倉分鐘", minval=0, maxval=59, step=1)
offset = input.int(8, "時區(默認UTC+8)", minval=-20, maxval=20)

// 請注意時區，我這裏是 UTC+8 時間.
label1 = label.new(bar_index, low, text="當前時間 - " + str.tostring(hour+offset) + ":" + str.tostring(minute), style=label.style_label_up, color=color.white)

label.set_x(label1, bar_index)
label.delete(label1[1])
alertcondition(hour+offset==h and minute==m, title='定時平倉訊號', message='定時平倉訊號')
```

添加完成之後，需要設定警報的時間，請在指標左上角的屬性中點設置，然後設定具體的平倉時間，設定平倉在哪個小時和哪一分鐘。
![設置警報時間](https://user-images.githubusercontent.com/94948670/220978237-68afe9b2-7424-43cb-9296-5bc5ccdb4551.png)  
  
然後點擊 “Alert” （中文：警報/快訊） 添加警報  
![添加快訊](https://user-images.githubusercontent.com/94948670/220978642-d5567af5-116d-4a04-8603-a2f0bb3a2b08.png)
  
回到TVCBOT中，依次選擇賬戶 -> 選擇交易對 -> 選擇指標 -> 選擇市價全平 -> 選擇保證金模式 -> 點生成警報
![生成TradingView警報](https://user-images.githubusercontent.com/94948670/220978987-a60d8aff-b466-4041-8673-20de9a19bf09.png)
  
將警報内容中的消息添加到TradingView的Message消息框中
![添加警報](https://user-images.githubusercontent.com/94948670/220979203-64a610ba-8750-4a64-9293-c69fa55eb0c0.png)
  
點“notification”，將 TVCBOT 的 WebHook URL 添加到tradingview對應的位置中
![添加警報](https://user-images.githubusercontent.com/94948670/220979411-8e0b7b41-c1e2-4dc2-befa-acaa358648dc.png)
  
然後點擊“create”創建警報即可，左側警報列表會出現這個定時平倉的警報，刪除警報可以停止自動平倉

原文地址：[通過TVCBOT和TradingView設定讓交易所合約定時平倉，在你睡覺的時候自動平倉](https://www.tvcbot.com/knowledgebase/65/%E9%80%9A%E9%81%8ETVCBOT%E5%92%8CTradingView%E8%A8%AD%E5%AE%9A%E8%AE%93%E4%BA%A4%E6%98%93%E6%89%80%E5%90%88%E7%B4%84%E5%AE%9A%E6%99%82%E5%B9%B3%E5%80%89%E5%9C%A8%E4%BD%A0%E7%9D%A1%E8%A6%BA%E7%9A%84%E6%99%82%E5%80%99%E8%87%AA%E5%8B%95%E5%B9%B3%E5%80%89.html)
