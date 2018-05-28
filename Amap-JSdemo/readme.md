## 最简单的高德地图JS调用
```
<div id="container" style="width:500px; height:300px"></div>
<!--高德地图入口脚本-->
<script src="http://webapi.amap.com/maps?v=1.4.6&key=您申请的key值&callback=init"></script>
<script>
    function init(){
        //初始化map对象，将其绑定在container上，并设定中心点（经度，纬度）zoom大小范围
        var map = new AMap.Map('container', {
            center: [117.000923, 36.675807],
            zoom: 11
        });
        //地图左侧控制器，增加插件
        map.plugin(["AMap.ToolBar"], function() {
            map.addControl(new AMap.ToolBar());
        });
    }
</script>
```
有三个重要点：
1. 设置地图容器div
2. 设置入口脚本
3. 编写初始化地图脚本，创建对象，增加插件。。