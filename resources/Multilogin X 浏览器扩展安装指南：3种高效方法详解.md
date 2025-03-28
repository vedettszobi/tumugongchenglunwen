# Multilogin X 浏览器扩展安装指南：3种高效方法详解

Multilogin X 提供了多种灵活的浏览器扩展安装方式，满足不同用户的操作习惯。本文将详细介绍三种主流安装方法，帮助您快速完成扩展配置。

## 三种安装方式概览
Multilogin X 支持通过以下途径安装浏览器扩展：
- **界面安装**：与传统浏览器操作一致
- **文件夹安装**：适用于批量配置场景
- **API 安装**：适合开发者自动化操作

👉 [【点击查看】2025年最新 Multilogin 优惠码及特价套餐活动方案汇总](https://bit.ly/multIlogin)

## 方法一：界面安装（推荐新手）
此方式与常规浏览器操作流程相同：

1. 启动目标浏览器配置文件
2. 根据浏览器类型访问扩展商店：
   - **Mimic**：访问 Chrome 网上应用店
   - **Stealthfox**：访问 Firefox 附加组件页面
3. 选择所需扩展，点击"添加到 Chrome"或"添加到 Firefox"
4. 安装完成后，扩展图标将显示在浏览器窗口右上角

## 方法二：文件夹安装（批量配置）

### Mimic 浏览器配置流程
1. **获取扩展文件**：
   - 从 Chrome 网上应用店安装目标扩展
   - 访问 `chrome://version/` 查看"配置文件路径"
   - 在文件资源管理器中定位到 `Extensions` 文件夹

2. **文件准备要点**：
   - 确保包含完整的扩展文件夹结构
   - 必须存在 `manifest.json` 核心文件
   - 每个扩展需要独立文件夹存放

3. **路径配置示例**：
json
"cmd_params": {
    "params": [
        {
            "flag": "load-extension",
            "value": "path-to-extension"
        }
    ]
}

### 多扩展安装技巧
通过逗号分隔多个路径实现批量安装：
json
"value": "path-to-extension1,path-to-extension2"

## 方法三：API 安装（开发者方案）
适用于需要自动化配置的专业用户，通过 API 调用实现扩展部署。完整配置示例如下：

json
{
    "browser_type": "mimic",
    "folder_id": "folder-id",
    "name": "profile-name",
    "os_type": "windows",
    "core_version": 125,
    "parameters": {
        "flags": {
            "audio_masking": "mask",
            "fonts_masking": "natural",
            "geolocation_masking": "natural",
            "geolocation_popup": "block",
            "graphics_masking": "natural",
            "graphics_noise": "natural",
            "localization_masking": "mask",
            "media_devices_masking": "custom",
            "navigator_masking": "custom",
            "ports_masking": "natural",
            "proxy_masking": "disabled",
            "screen_masking": "natural",
            "timezone_masking": "mask",
            "webrtc_masking": "mask"
        },
        "fingerprint": {
            "navigator": {
                "user_agent": "Mozilla/5.0 (Windows NT 11.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5790.110 Safari/537.36",
                "hardware_concurrency": 4,
                "os_cpu": "windows",
                "platform": "Win32"
            },
            "media_devices": {
                "video_inputs": 1,
                "audio_inputs": 2,
                "audio_outputs": 4
            },
            "cmd_params": {
                "params": [
                    {
                        "flag": "load-extension",
                        "value": "C:\\Users\\Username\\Downloads\\Extension-folder-name"
                    }
                ]
            }
        },
        "storage": {
            "is_local": true,
            "save_service_worker": true
        }
    }
}

## 注意事项
1. 确保扩展文件完整，避免使用单独的 `.crx` 文件
2. 多扩展安装时注意路径分隔符使用
3. API 方式需要熟悉 JSON 配置格式
4. 不同浏览器类型（Mimic/Stealthfox）需对应不同的扩展源

通过以上三种方法，您可以灵活地在 Multilogin X 中配置各类浏览器扩展，满足不同场景下的使用需求。