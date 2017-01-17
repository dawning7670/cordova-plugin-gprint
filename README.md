### 接口参数格式

所有接口的参数形式

```
gprinter.func(success: function, error: function, params: JSON)
```

### 具体参数

具体参数

当func为下列函数时，具体的参数格式如下

- openPort

  **功能：**打开打印机端口

  **参数说明：**

  ```
  success = function(err_code){}
  error = function(err_msg)
  params = {
    "printId": Int,         // 打印机序号 取值为 0 1 2, 后面就使用这个序号标识某台打印机
    "portType": Int,        // 端口类型 USB->2, ETHERNET->3, BLUETOOTH->4
    "deviceName": String,   // 设备名 USB->USB设备的DeviceName, ETHERNET->IP地址, BLUETOOTH->蓝牙MAC地址
    "portNumber": Int       // 端口号 USB->0, ETHERNET->端口号, BLUETOOTH->0
  }

  // err_code说明
  0 //正常
  1 //失败
  2 // 超时
  3 //无效的参数
  4 //端口已经打开
  5 //无效的端口号
  6 //无效的ip地址
  7 //无效的回调
  8 //设备不支持蓝牙
  9 //请打开蓝牙
  10 //端口未打开
  11 //无效的蓝牙地址
  12 //端口连接断开
  ```


- closePort

  **功能：**关闭打印机端口

   **参数说明：**

  ```
  success = function(){}
  error = function(err_msg){}
  params = {
    "printId": Int           // 打印机序号
  }
  ```

- getPrinterConnectStatus

  **功能：**获取打印机连接状态

  **参数说明：**

  ```
  success = function(conn_status){}
  error = function(err_msg){}
  params = {
    "printId": Int           // 打印机序号
  }

  // conn_status说明
  0 //连接断开
  1 //监听状态
  2 //正在连接
  3 //已连接
  ```

- getPrinterCommandType

  **功能：**获取打印机命令类型

  **参数说明：**

  ```
  success = function(command_type){}
  error = function(err_msg){}
  params = {
    "printId": Int           // 打印机序号
  }

  // command_type说明
  0 //ESC
  1 //TSC
  ```

- queryPrinterStatus

  **功能：**获取打印机运行状态

  **参数说明：**

  ```
  success = function(printer_status){}
  error = function(err_msg){}
  params = {
    "printId": Int,
    "timeOut": Int   //超时时间
  }

  // printer_status说明
  0 //正常
  0x1 //脱机
  0x2 //缺纸
  0x4 //开盖
  0x8 //过热 错误
  ```

- sendEscCommand

  **功能：**发送ESC命令 需要确保打印机处于票据模式

  **参数说明：**

  ```
  success = function(err_code){}
  error = function(err_msg){}
  params = {
    "printId": Int,
    "base64": String  // 票据数据
  }

  // err_code同上
  ```

- sendTscCommand

  **功能：**发送TSC命令 需要确保打印机处于标签模式

  **参数说明：**

  ```
  success = function(err_code){}
  error = function(err_msg){}
  params = {
    "printId": Int,
    "base64": String  // 票据数据
  }

  // err_code同上
  ```

- getCommand

  **功能：**根据参数组成待发送的ESC命令数据

  **参数说明：**

  ```
  success = function(base64){}
  error = function(err_msg){}
  params = [
   {
     "functionName": String
   },...
  ]
  ```

- printTestPage

  **功能：**打印测试页面

  **参数说明：**

  ```
  success = function(err_code){}
  error = function(err_msg){}

  // err_code同上
  ```

- listBT

  **功能：**列出所有蓝牙设备

  **参数说明：**

  ```
  success = function(device){}
  error = function(err_msg){}

  // 返回值device说明
  [
    {
      "name": String,
      "address": String
    },...
  ]
  ```

  ​
