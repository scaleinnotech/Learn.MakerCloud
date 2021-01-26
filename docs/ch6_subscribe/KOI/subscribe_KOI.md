# 使用KOI訂閱主題
在編程發布訊息到創客雲前，使用者必先學習如何令KOI連接創客雲MQTT，連接方法可根據硬件參考上面的教學。  
[使用KOI連接創客雲](../../ch4_connect/KOI/connect_KOI.md)

[TOC]

## KOI
只要成功連接創客雲後，便可以使用以下同樣的訂閱積木編程接收訊息。  
**注意每次編程必須要在當啟動時先連接Wi-Fi和創客雲MQTT。**
### 訂閱積木
在創客雲KOI擴展中，有不同類型的訂閱積木。

**訂閱主題**  
![img_1.png](img/img_1.png){:width="25%"}  
在連接創客雲後，透過KittenWiFi訂閱創客雲主題。  
建議放在「當啟動時」之中及「連接創客雲MQTT」積木之後。

**處理創客雲MQTT訊息 "data" "topic"**  
![img_0.png](img/img_0.png){:width="55%"}  
當KOI收到MQTT訊息後，把資料和主題加入此積木，然後資料會轉送到以下相對應的訊息積木。  
需配合KOI擴展的 "on Mqtt Data" 積木使用。

**當MQTT "topic"收到文字訊息**  
![img_2.png](img/img_2.png){:width="60%"}  
當指定主題收到文字訊息，便會運行此積木

**當MQTT "topic"收到鍵文字對訊息**  
![img_3.png](img/img_3.png){:width="70%"}  
當指定主題收到鍵文字對訊息，便會運行此積木

**當MQTT "topic"收到鍵值對訊息**  
![img_4.png](img/img_4.png){:width="70%"}  
當指定主題收到鍵值對訊息，便會運行此積木

使用者可以根據數據類型使用相對應的訂閱積木。

### 訂閱文字訊息
#### 學習重點
- 學習如何透過KOI從訂閱的主題收到文字訊息

#### 練習 - 向micro:bit打招呼
##### 目標
- 訂閱主題
- 從創客雲接收MQTT訊息  
![img_5.png](img/img_5.png){:width="90%"}

**在Makecode編程前，我們需要在創客雲上:**

1. 創建項目
2. 創建主題

**然後便可到Makecode編程:**

1. 新增專案
2. 加入KOI擴展  
   [https://github.com/KittenBot/pxt-koi]()
3. 加入創客雲KOI擴展  
   [https://github.com/scaleinnotech/pxt-makercloud-koi]()
4. 當啟動時:  
   更新KOI接口、連接WiFi及創客雲MQTT
5. 加入訂閱創客雲主題積木，然後複製並貼上需訂閱的主題名稱  
![img_topic_message.png](img/img_topic_message.png){:width="70%"}
</br></br>
![img_7.png](img/img_7.png){:width="90%"}
</br></br>
6. 加入KOI擴展中的"on Mqtt Data"積木，然後加入"處理創客雲MQTT訊息"積木。  
   把接收的資料和主題加入到"處理創客雲MQTT訊息"積木中。  
![img_8.gif](img/img_8.gif)
</br></br>
7. 加入「當MQTT 收到文字訊息」，然後貼上已訂閱的主題名稱  
![img_9.png](img/img_9.png)
</br></br>
8. 把接收到的文字訊息顯示出來  
![img_10.gif](img/img_10.gif){:width="40%"}
</br></br>
9. 下載編程到micro:bit

完成編程後，回到創客雲的項目主頁。  
按下主題中的「詳細資料」按鈕，進入主題主頁。  
在「發送消息到主題」的文字輸入框中，輸入「hello」，然後按「發送」。  
![img_publishhello.gif](img/img_publishhello.gif)

從創客雲發送訊息後，micro:bit上的LED便會顯示「hello」。  
![img_12.gif](img/img_12.gif){:width="40%"}