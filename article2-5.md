# ロボットカー制御

ここではAndroid端末からロボットカーを制御します。

今回はFaBoのモーターシールドとBrickのBluetoothを使用します。

モーターシールド
<br>
https://fabo.gitbooks.io/module/content/shield_motor/shield_motor.html

Bluetooth
<br>
https://fabo.gitbooks.io/module/content/brick_serial_bluetooth/brick_serial_bluetooth.html


## 接続

## Arduino

ここでは受信データにより前進、後退、停止するプログラムを書いてみます。
```c
#include <SoftwareSerial.h>

#define led1 A0     // A0番ピンにてLEDを制御
#define led2 A1     // A1番ピンにてLEDを制御

#define right_f 4   // 右タイヤのモーター前進用ピン
#define right_pow 3 // 右タイヤのモーター出力設定用ピン
#define right_b 2   // 右タイヤのモーター後退用ピン

#define left_f 5    // 左タイヤのモーター用ピン(前進用)
#define left_pow 6  // 左タイヤのモーター出力設定用ピン
#define left_b 7    // 左タイヤのモーター用ピン(後退用)

SoftwareSerial android(11, 10); // Bluetooth用シリアル通信ピン

char readData = 0;  // androidからのテキスト取得用

void setup() {
  // 右側のタイヤ制御用
  pinMode(right_f, OUTPUT);
  pinMode(right_b, OUTPUT);
  pinMode(right_pow, OUTPUT);

  // 左側のタイヤ制御用
  pinMode(left_f, OUTPUT);
  pinMode(left_b, OUTPUT);
  pinMode(left_pow, OUTPUT);

  // Bluetooth用のシリアルのポートを設定
  android.begin(115200);
  
  // arduinoのシリアルモニタ用
  Serial.begin(19200);

  Serial.println("start");
}

void loop() {

  if (android.available()) {
    // Androidからデータ受信
    readData = android.read();
    Serial.write(readData);
    Serial.write(10);

    // 受信データによりロボカーの制御を行う
    // 前進
    if (readData == '1') {
      // 右タイヤ前進(H/L)
      digitalWrite(right_f, HIGH);
      digitalWrite(right_b, LOW);
      analogWrite(right_pow, 255); // 0-255 強さ

      // 左タイヤ前進(H/L)
      digitalWrite(left_f, HIGH);
      digitalWrite(left_b, LOW);
      analogWrite(left_pow, 255);  // 0-255 強さ
    }
    // 後退
    else if ( readData == '2') {
      // 右タイヤ後退(L/H)
      digitalWrite(right_f, LOW);
      digitalWrite(right_b, HIGH);
      analogWrite(right_pow, 255); // 0-255 強さ

      // 左タイヤ後退(L/H)
      digitalWrite(left_f, LOW);
      digitalWrite(left_b, HIGH);
      analogWrite(left_pow, 255);  // 0-255 強さ
    }
    // 停止
    else {
      // 右タイヤ停止(L/L)
      digitalWrite(right_f, LOW);
      digitalWrite(right_b, LOW);
      analogWrite(right_pow, 0);   // 0-255 強さ

      // 左タイヤ後退(L/L)
      digitalWrite(left_f, LOW);
      digitalWrite(left_b, LOW);
      analogWrite(left_pow, 0);    // 0-255 強さ
    }
  }
}
```
## Android
