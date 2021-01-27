# 使用Arduino訂閱主題
在編程訂閱訊息到創客雲前，使用者必先學習如何令Arduino連接創客雲MQTT，連接方法可參考上面的教學。  
[使用Arduino連接創客雲](../../ch4_connect/arduino/connect_arduino.md)

[TOC]

## 訂閱函數
在Arduino創客雲MakerCloudMQTT中，有不同類型的訂閱函數。

#### MakerCloudClient.subscribe()
訂閱創客雲主題
```cpp
MakerCloudClient.subscribe(topic);
```
**topic**  
在「創客雲」上創建的主題名稱

#### MakerCloudClient.listen()
從訂閱了的主題讀取1條MQTT訊息
```cpp
MakerCloudClient.listen();
```

#### MakerCloudClient.setMessageCallback
當收到文字訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```cpp
void message_callback(String topic, String message) {

}

// setup
MakerCloudClient.setMessageCallback(message_callback);
```

**topic**  
訂閱了的主題名稱

**message**  
收到的文字訊息

#### MakerCloudClient.setKeyMessageCallback
當收到鍵文字對訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```cpp
void key_message_callback(String topic, String key, String message) {

}

// setup
MakerCloudClient.setKeyMessageCallback(key_message_callback);
```

**topic**  
訂閱了的主題名稱

**key**  
收到的鍵

**message**  
收到的文字訊息

#### MakerCloudClient.setKeyValueCallback
當收到鍵值對訊息，便會運行此函數。  
使用者需要先**自行定義**，然後指定到MakerCloudMQTT中。
```cpp
void key_value_callback(String topic, String key, int value) {

}

// setup
MakerCloudClient.setKeyValueCallback(key_value_callback);
```

**topic**  
訂閱了的主題名稱

**key**  
收到的鍵

**value**  
收到的值

## 訂閱文字訊息
#### 學習重點
- 學習如何透過Arduino從訂閱的主題收到文字訊息

#### 目標
- 訂閱主題
- 從創客雲接收MQTT文字訊息

**在Arduino編程前，我們需要在創客雲上:**

1. 創建項目
2. 創建主題
3. 在創客雲複製主題名稱  
![img_topic_message.png](img/img_topic_message.png){:width="70%"}


**然後便可到Arduino IDE編程:**
```cpp
EthernetClient ethClient;
MakerCloudMQTT MakerCloudClient(ethClient);

// This function connects Wi-Fi
void setup_wifi() {

}

// Subscribe Message Callback Function
void message_callback(String topic, String message) {
  Serial.print("Topic: ");
  Serial.print(topic);
  Serial.print("; Message: ");
  Serial.println(message);
}

void setup() {
  Serial.begin(115200);

  // MakerCloudMQTT Configuration
  MakerCloudClient.setUsername("Max");
  // Enable to print extra log
  MakerCloudClient.setLog(true);

  // Set callback function
  MakerCloudClient.setMessageCallback(message_callback);
  
  // Connect Wi-Fi
  setup_wifi();

  // Connect to MakerCloud
  if (MakerCloudClient.connect()) {
    // Subscribe to a topic
    MakerCloudClient.subscribe(topic);
  }
}

// The looping function will allow sending message to MakerCloud
void loop() {
  // Update user status and process 1 incoming MQTT message each second
  MakerCloudClient.listen();
  delay(1000);
}
```

完成及運行編程後，回到創客雲的項目主頁。  
按下主題中的「詳細資料」按鈕，進入主題主頁。  
在「發送消息到主題」的文字輸入框中，輸入「hello」，然後按「發送」。  
![img_publishhello.gif](img/img_publishhello.gif)

回到Arduino IDE，開啟Serial Monitor，便會收到文字訊息：
```
Topic: QQP4LRB0; Message: hello
```

