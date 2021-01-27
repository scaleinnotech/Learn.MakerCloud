# 使用Python訂閱主題
在編程訂閱訊息到創客雲前，使用者必先學習如何令Python連接創客雲MQTT，連接方法可參考上面的教學。  
[使用Python連接創客雲](../../ch4_connect/python/connect_python.md)

[TOC]

## 訂閱函數
在Python創客雲MakerCloudMQTT中，有不同類型的訂閱函數。

#### MakerCloudMQTT.subscribe()
訂閱創客雲主題
```python
MakerCloudMQTT.subscribe(topic)
```
**topic**  
在「創客雲」上創建的主題名稱

#### MakerCloudMQTT.message_handler
當收到文字訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```python
def message_handler(topic, message):
    print('Topic: ' + topic + ' Message: ' + message)

MakerCloudMQTT.message_handler = message_handler
```

**topic**  
訂閱了的主題名稱

**message**  
收到的文字訊息

#### MakerCloudMQTT.key_message_handler
當收到鍵文字對訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```python
def key_message_handler(topic, key, message):
    print('Topic: ' + topic + 'Key: ' + key + ' Message: ' + message)

MakerCloudMQTT.key_message_handler = key_message_handler
```

**topic**  
訂閱了的主題名稱

**key**  
收到的鍵

**message**  
收到的文字訊息

#### MakerCloudMQTT.key_value_handler
當收到鍵值對訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```python
def key_value_handler(topic, key, value):
    print('Topic: ' + topic + 'Key: ' + key + ' Value:' ,value)

MakerCloudMQTT.key_value_handler = key_value_handler
```

**topic**  
訂閱了的主題名稱

**key**  
收到的鍵

**value**  
收到的值

#### MakerCloudMQTT.coordinate_handler
當收到鍵值對訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```python
def coordinate_handler(topic, latitude, longitude):
    print('Topic: ' + topic + 'Latitude: ',latitude + ' longitude:' ,Longitude)

MakerCloudMQTT.coordinate_handler = coordinate_handler
```

**topic**  
訂閱了的主題名稱

**latitude**  
收到的緯度

**longitude**  
收到的經度

## 訂閱文字訊息
#### 學習重點
- 學習如何透過Python從訂閱的主題收到文字訊息

#### 目標
- 訂閱主題
- 從創客雲接收MQTT文字訊息

**在Python編程前，我們需要在創客雲上:**

1. 創建項目
2. 創建主題
3. 在創客雲複製主題名稱  
![img_topic_message.png](img/img_topic_message.png){:width="70%"}


**然後便可到Python編程:**
```python
import MakerCloudMQTT

MakerCloudMQTT.username = 'Max'
# 貼上主題名稱
topic = 'QQP4LRB0'

# 定義message_handler
def message_handler(topic, message):
    print('Topic: ' + topic + ' Message: ' + message)

# 指定message_handler到MakerCloudMQTT.message_handler
MakerCloudMQTT.message_handler = message_handler
# 訂閱主題
MakerCloudMQTT.subscribe(topic)
```

完成及運行編程後，回到創客雲的項目主頁。  
按下主題中的「詳細資料」按鈕，進入主題主頁。  
在「發送消息到主題」的文字輸入框中，輸入「hello」，然後按「發送」。  
![img_publishhello.gif](img/img_publishhello.gif)

回到Python程式，便會收到文字訊息:
```
Topic: QQP4LRB0 Message: hello
```
