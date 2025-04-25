![alt text](image.jpg)

<h1 align="center">🌦️ ESP32 Weather Component</h1>

<p align="center">
一个让ESP32变身智能天气站的炫酷组件<br/>
支持高德、心知、和风三种天气API<br/>
提供天气信息获取和展示功能
</p>

<p align="center">
<a href="./README_EN.md">English</a>
· 简体中文
· <a href="https://github.com/NingZiXi/weather/releases">更新日志</a>
· <a href="https://github.com/NingZiXi/weather/issues">反馈问题</a>
</p>

<p align="center">
  <a href="LICENSE">
    <img alt="License" src="https://img.shields.io/badge/License-MIT-blue.svg" />
  </a>
  <a href="https://docs.espressif.com/projects/esp-idf/">
    <img alt="ESP-IDF" src="https://img.shields.io/badge/ESP--IDF-v5.3+-orange.svg" />
  </a>
  <a href="https://www.espressif.com/">
    <img alt="ESP32" src="https://img.shields.io/badge/Platform-ESP32-green.svg" />
  </a>
  <a href="">
    <img alt="Version" src="https://img.shields.io/badge/Version-v1.0.0-brightgreen.svg" />
  </a>
  <a href="https://github.com/NingZiXi/weather/stargazers">
    <img alt="GitHub Stars" src="https://img.shields.io/github/stars/NingZiXi/weather.svg?style=social&label=Stars" />
  </a>"
  </a>
</p>

---


✨ 一个让ESP32变身智能天气站的炫酷组件 ✨
## 🚀 功能亮点

- 🌐 **三合一API支持**：高德、心知、和风天气任君选择
- 📍 **智能定位**：自动识别你的位置，省去手动配置
- 🔍 **数据丰富**：温度、湿度、风速、降水...应有尽有
- 🎨 **终端美化**：控制台输出堪比艺术品
- 🔒 **安全可靠**：HTTPS + CRT证书验证
## 📊 数据支持对比

| 功能特性       | 高德天气 | 心知天气 | 和风天气 |
|----------------|----------|----------|----------|
| 实时天气       | ✅        | ✅        | ✅        |
| 温度           | ✅        | ✅        | ✅        |
| 湿度           | ✅        | ❌        | ✅        |
| 风向风速       | ✅        | ❌        | ✅        |
| 风力           | ✅        | ❌        | ✅        |
| 气压           | ❌        | ❌        | ✅        |
| 能见度         | ❌        | ❌        | ✅        |
| 体感温度       | ❌       | ❌        | ✅        |
| 降水量         | ❌        | ❌        | ✅        |
| 云量           | ❌        | ❌        | ✅        |
| 露点温度       | ❌        | ❌        | ✅        |
| 免费调用次数   |  30 万/日  | 无次数限制  | 1000/日  |
| 是否需要付费   | 可选      | 可选      | 可选      |

以上数据均为免费服务数据，这里推荐和风天气，虽然免费次数较少，但免费版的服务和付费版是相同的。

## 🛠️ 快速开始

### 1. 克隆项目

要将组件添加到项目中请在IDF终端执行下方命令:

```bash
idf.py add-dependency "ningzixi/weather^1.1.0"
```

或者直接克隆本仓库到项目`components`目录下:

```bash
git clone https://github.com/NingZiXi/weather
```

### 2. 获取API密钥


- **高德API**: [https://lbs.amap.com/api/webservice/guide/create-project/get-key](https://lbs.amap.com/api/webservice/guide/create-project/get-key)

- **心知天气API**: [https://www.seniverse.com/dashboard](https://www.seniverse.com/dashboard)

- **和风天气API**：和风天气除了获取key外，还需要配置host，具体如下：
  - key: [https://console.qweather.com/home](https://console.qweather.com/home)
  - host: [https://console.qweather.com/setting](https://console.qweather.com/setting)

### 3. 基本用法

```c
#include "weather.h"

void app_main() {
    //省略联网部分
    weather_config_t config = {
        .api_key = WEATHER_HEFENG_KEY,
        .api_host = WEATHER_HEFENG_HOSE,    // 和风天气需要配置host
        .city = NULL, // city为NULL自动根据IP地址获取位置,也可以指定城市
        // .city = "北京",
        .type = WEATHER_HEFENG  //可更改为api配置WEATHER_AMAP或WEATHER_XINZHI
    };

    weather_info_t *info = weather_get(&config);
    if (info) {
        weather_print_info(info); // 打印天气信息
        weather_info_free(info);
    }
}
```
更多API接口请查看[weather.h](include/weather.h)

#### 串口输出如下
``` 
  🌈 WEATHER REPORT ☁️
 _ _ _ _____ _____ _____ _____ _____ _____
| | | |   __|  _  |_   _|  |  |   __| __  |
| | | |   __|     | | | |     |   __|    -|
|_____|_____|__|__| |_| |__|__|_____|__|__|

📍 位置: 常州
┌───────────────────────────────────────┐
│ ☁️  天气: 阴                           │
│ 🌡️  温度: 30.0℃                      │
│ 🤒  体感: 25.0℃                      │
│ 💧  湿度: 21.0%                       │
│ 🍃  风向: 西南风                       │
│ 💨  风力: 5                           │
│ 🌬️  风速: 29.0km/h                    │
│ ⏲️  气压: 1004.0hPa                   │
│ 👁️  能见度: 26.0km                    │
│ ☁️  云量: 99.0%                       │
│ 💦  露点: 10.0℃                      │
└───────────────────────────────────────┘

🕒 更新时间: 2025-04-16T14:18+08:00
```
## 贡献
本项目采用 MIT 许可证，详情请参阅 [LICENSE](LICENSE) 文件，本项目仍在完善中，可能会有一些功能尚未完善或存在 Bug。如果您在使用过程中遇到任何问题，请随时联系作者或提交 Issue 来帮助改进本项目！

<p align="center">
感谢您使用 ESP32 Weather Component！<br/>
如果觉得项目不错，请给个 ⭐ Star 支持一下！
</p>

