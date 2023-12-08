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
x_rotation_cone = 0.0
y_rotation_cone = -90.0
z_rotation_cone = 0.0
rotation_cone = mathutils.Euler((math.radians(x_rotation_cone), math.radians(y_rotation_cone), math.radians(z_rotation_cone)), 'XYZ')

# 位置
x_location_cone = 0.5
y_location_cone = 0.0
z_location_cone = 0.0
location_cone = mathutils.Vector((x_location_cone, y_location_cone, z_location_cone))

params_cone = {
"vertices": 32, # 多いほど丸みを帯びる
"radius1": 1.0, # 底面の半径
"radius2": 0.0, # 頂点の半径
"depth": 1.0, # 高さ
"location": location_cone, # 位置
"rotation": rotation_cone, # 回転
} 
bpy.ops.mesh.primitive_cone_add(**params_cone)


# 立方体 https://docs.blender.org/api/current/bpy.ops.mesh.html#bpy.ops.mesh.primitive_cube_add

# 回転
x_rotation_cube = 0.0
y_rotation_cube = 0.0
z_rotation_cube = 0.0
rotation_cube = mathutils.Euler(
    (
        math.radians(x_rotation_cube),
        math.radians(y_rotation_cube),
        math.radians(z_rotation_cube),
    ),
    "XYZ",
)

# 位置
x_location_cube = 0.0
y_location_cube = 0.0
z_location_cube = 0.0
location_cube = mathutils.Vector(
    (x_location_cube, y_location_cube, z_location_cube)
)

params_cube = {
    "size": 1.0,
    "location": location_cube,
    "rotation": rotation_cube,
}  # 1辺の長さ

bpy.ops.mesh.primitive_cube_add(**params_cube)


# 円柱 https://docs.blender.org/api/current/bpy.ops.mesh.html#bpy.ops.mesh.primitive_cylinder_add

# 回転
x_cylinder = 0.0
y_cylinder = 0.0
z_cylinder = 0.0
rotation_cylinder = mathutils.Euler((math.radians(x_cylinder), math.radians(y_cylinder), math.radians(z_cylinder)), 'XYZ')

# 位置
x_location_cylinder = 0.0
y_location_cylinder = 0.0
z_location_cylinder = 0.0
location_cylinder = mathutils.Vector((x_location_cylinder, y_location_cylinder, z_location_cylinder))

params_cylinder = {
"vertices": 32, # 多いほど丸みを帯びる
"radius": 2.0, # 底面の半径
"depth": 5.0, # 高さ
"location": location_cylinder, # 位置
"rotation": rotation_cylinder, # 回転
}

bpy.ops.mesh.primitive_cylinder_add(**params_cylinder)

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

bpy.ops.mesh.primitive_uv_sphere_add(**params_sphere)


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

```python
# オブジェクトの名前の変更 円錐の場合
bpy.data.objects["円錐"].name = "任意の名前"

# 選択したオブジェクトの名前を変更
for obj in bpy.context.selected_objects:
    obj.name = "任意の名前"
```

