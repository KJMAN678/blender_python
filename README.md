## Blender + Python
#### Blender の Script で Pythonコードを実行できる
<img src="images/image.png" width="1000px">

- [Blender ダウンロードページ](https://www.blender.org/download/)
- [Blender で Python スクリプトを実行](https://www.kkaneko.jp/db/cg/bpy.html)
- [Blender API (bpy) リファレンス(英語)](https://docs.blender.org/api/current/index.html)
- Blender で Unity 向けにエクスポート (メッシュだけの方がよさそう？)
  - モデルを選択し、 ファイル > エクスポート > FBX
- Unity で Blender からインポート
  - Assets > Import New Assets > FBXを選択して Import
- [Blender Macでコンソール出力を表示させる](https://www.patec-tech.jp/process/?p=3762)

```python
import bpy
import mathutils
import math

# 円錐 https://docs.blender.org/api/current/bpy.ops.mesh.html#bpy.ops.mesh.primitive_cone_add

# 回転
x_cone = 0.0
y_cone = 90.0
z_cone = 0.0
rotation_cone = mathutils.Euler((math.radians(x_cone), math.radians(y_cone), math.radians(z_cone)), 'XYZ')

params_cone = {
"vertices": 32, # 多いほど丸みを帯びる
"radius1": 5.0, # 底面の半径
"radius2": 0.0, # 頂点の半径
"depth": 5.0, # 高さ
"rotation": rotation_cone, # 回転
} 
#bpy.ops.mesh.primitive_cone_add(**params_cone)


# 立方体 https://docs.blender.org/api/current/bpy.ops.mesh.html#bpy.ops.mesh.primitive_cube_add

# 回転
x_cube = 0.0
y_cube = 0.0
z_cube = 45.0
rotation_cube = mathutils.Euler((math.radians(x_cube), math.radians(y_cube), math.radians(z_cube)), 'XYZ')

params_cube = {
"size": 4.0, # 1辺の長さ
"rotation": rotation_cube
}

#bpy.ops.mesh.primitive_cube_add(**params_cube)


# 円柱 https://docs.blender.org/api/current/bpy.ops.mesh.html#bpy.ops.mesh.primitive_cylinder_add

# 回転
x_cylinder = 0.0
y_cylinder = 0.0
z_cylinder = 45.0
rotation_cylinder = mathutils.Euler((math.radians(x_cylinder), math.radians(y_cylinder), math.radians(z_cylinder)), 'XYZ')

params_cylinder = {
"vertices": 32, # 多いほど丸みを帯びる
"radius": 5.0, # 底面の半径
"depth": 5.0, # 高さ
"rotation": rotation_cylinder, # 回転
}

#bpy.ops.mesh.primitive_cylinder_add(**params__cylinder)


# 球 https://docs.blender.org/api/current/bpy.ops.mesh.html#bpy.ops.mesh.primitive_uv_sphere_add

# 回転
x_sphere = 0.0
y_sphere = 0.0
z_sphere = 45.0
rotation_sphere = mathutils.Euler((math.radians(x_sphere), math.radians(y_sphere), math.radians(z_sphere)), 'XYZ')

params_sphere = {
"segments": 32, # 多いほど周囲に丸みを帯びる
"ring_count": 32, # 多いほど縦方向に丸みを帯びる
"radius": 5.0, # 底面の半径
"rotation": rotation_sphere, # 回転
}

#bpy.ops.mesh.primitive_uv_sphere_add(**params_sphere)


# 直方体 https://docs.blender.org/api/current/bpy.ops.transform.html#bpy.ops.transform.resize

params_cuboid = {
"size": 2.0, # 1辺の長さ
"rotation": rotation_cube
}

depth_cuboid = 1 # 奥行を何倍にするか
width_cuboid = 1 # 幅を何倍にするか
height_cuboid = 1 # 高さを何倍にするか
bpy.ops.mesh.primitive_cube_add(**params_cuboid)
bpy.ops.transform.resize(value=(depth_cuboid, width_cuboid, height_cuboid))
```


