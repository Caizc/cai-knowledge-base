# Best Practices in Unity

# 1. Unity Editor

* Unity 中的长度单位是**米**。
* 检查导入的 3D 模型的尺寸是否正确时，可以将模型与标准 Cube 做对比。
* 在 Scene View 中：

    - 按下 `F` 键聚焦到选定对象
    - 移动对象时按下 `V` 键可以自动吸附到就近网格的顶点
    - 移动/旋转/缩放对象时按下 `Ctrl/Commad` 键可以保持固定位移/角度/比例进行变化，在 `Edit -> Snap settings` 中可以设置相应数值

* 使用 Layer 来管理 GameObject 可以指定对象对于 Camera、Lighting 和 RayCast 的可见性

# 2. Assets

## 3D 资源导入

* 3D 模型首选文件格式是 `FBX`，它包含了模型、UV 坐标、骨骼、蒙皮和动画；`OBJ` 格式通常用于静态网格。
* 模型导入后首先要检查 Import Settings，包括 Model、Rig 和 Animations 属性。
* 检查模型的 Model 设置：

    - Scale Factor：模型缩放系数
    - Mesh Compression：网格压缩
    - Import Materials：导入材质
    - Material Naming：材质命名
    - Material Search：材质的查找范围

* 导入在 Material 中使用的 Texture：

    - Unity 支持的 Texture 格式包括 JPEG、PNG、TGA、TIFF、BMP 等，甚至 Photoshop 的原生文件 PSD，但 Unity 会将 PSD 中的图层合并，所以一般按需求导出为 TGA 或 TIFF 文件
    - FBX 文件导出时，一般会将模型对应的 Texture 放置在一个 `xxx.fbm` 文件夹中
    - Texture 的像素大小应为 2 的 N 次幂，利于性能优化，拥有更好的压缩效果和内存利用率
    - 可以为 Texture 添加 Tag，方便在项目中查找

* 导入 Texture 后，要为不同类型的贴图指定正确的 `Texture Type`：
   
    - albedo 反射率贴图显示的是模型的原始颜色
    - `Normal map` 法线贴图可以为模型添加更多细节

## 2D 资源导入

* 2D 贴图的 `Texture Type` 必须设置为 `Sprite(2D and UI)`，并设置 Sprite Mode，如有必要，还要使用 Sprite Editor 将其切割为图集。

## 音频资源导入

# 3. Lighting

# 4. Particle System

# 5. Physics

# 6. Animation

# 7. UI

# 8. Navigation and Pathfinding

# 9. Audio

# 10. Building and Deploying

# 11. Mobile

# 12. Scripting

# 13. Multiplayer Networking

# 14. Performance Optimization

# 15. Tips

---

change log: 

	- 创建（2017-10-18）

---

