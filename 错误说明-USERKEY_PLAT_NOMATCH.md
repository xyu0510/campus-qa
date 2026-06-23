# ❌ 错误：USERKEY_PLAT_NOMATCH

## 问题原因

API密钥的平台类型与调用的API不匹配。

### 高德地图API有两种平台：

| 平台类型 | 用途 | 需要的Key类型 |
|---------|------|--------------|
| **Web端(JS API)** | 前端JavaScript调用 | Web端Key |
| **Web服务** | HTTP请求调用 | Web服务Key |

### 当前问题：

```
你的Key: 08acb33f872751f0e26e83a01552eba9
平台类型: Web服务

地图显示: ✅ 可以（JS API支持）
定位功能: ✅ 可以（JS API支持）
路线规划: ❌ 不可以（需要Web端Key）
```

---

## 🔧 解决方案

### 方案一：创建两个Key（推荐）

#### 步骤1：创建Web端Key（用于地图显示和定位）

1. 登录 [高德开放平台](https://console.amap.com/)
2. 进入"应用管理" → "我的应用"
3. 点击"添加Key"
4. 配置：
   - **服务平台**：选择 **Web端(JS API)** ⭐
   - **Key名称**：地图显示Key
   - 勾选服务：
     - ✅ Web端JS API
     - ✅ 地图显示
     - ✅ 定位

5. 提交后复制Key（记为Key1）

#### 步骤2：创建Web服务Key（用于路线规划）

1. 在同一应用下，再次点击"添加Key"
2. 配置：
   - **服务平台**：选择 **Web服务** ⭐
   - **Key名称**：路线规划Key
   - 勾选服务：
     - ✅ Web服务API
     - ✅ 路径规划
     - ✅ 地理/逆地理编码

3. 提交后复制Key（记为Key2）

#### 步骤3：更新代码

在 `map-navigation.html` 中：

```html
<!-- 地图显示和定位 -->
<script src="https://webapi.amap.com/maps?v=2.0&key=Key1"></script>

<!-- 路线规划需要在JS中配置 -->
<script>
window._AMapSecurityConfig = {
    serviceHost: 'https://restapi.amap.com',
    // 使用Web服务Key进行路线规划
}
</script>
```

---

### 方案二：使用高德地图APP（最简单）⭐ 推荐

**无需配置API密钥，直接使用高德APP导航！**

#### 使用方法：

1. 点击页面上的 **"📱 高德地图打开"** 按钮
2. 自动跳转到高德地图APP
3. APP会自动：
   - 定位当前位置
   - 设置目的地为厦门工学院
   - 选择交通方式
   - 开始导航

#### 优势：

- ✅ 无需配置API密钥
- ✅ 无配额限制
- ✅ 功能更强大（实时导航、语音播报）
- ✅ 体验更好

---

### 方案三：使用HTTP API（开发者方案）

直接调用Web服务API，不使用JS API的路线规划：

```javascript
// 驾车路线规划
fetch('https://restapi.amap.com/v3/direction/driving?' + 
    'origin=' + currentLng + ',' + currentLat +
    '&destination=118.066797,24.616296' +
    '&key=08acb33f872751f0e26e83a01552eba9')
.then(res => res.json())
.then(data => {
    // 处理路线数据
});
```

---

## 📊 方案对比

| 方案 | 难度 | 功能 | 推荐度 |
|------|------|------|--------|
| 方案一：双Key | 中等 | 完整Web端功能 | ⭐⭐⭐ |
| 方案二：高德APP | 简单 | APP导航 | ⭐⭐⭐⭐⭐ |
| 方案三：HTTP API | 困难 | 仅显示数据 | ⭐⭐ |

---

## 💡 建议

**对于普通用户：**
直接使用 **方案二（高德APP）**，无需任何配置，体验最好！

**对于开发者：**
使用 **方案一（双Key）**，获得完整的Web端路线规划功能。

---

## 🎯 快速解决

### 现在就可以使用：

点击页面上的 **"📱 高德地图打开"** 按钮，立即开始导航！

无需等待，无需配置，直接可用！✨

---

**更新时间：** 2026年6月23日