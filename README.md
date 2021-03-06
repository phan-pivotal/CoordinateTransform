# CoordinateTransform
用于将少量点叠加各个在线网络底图纠偏库

在做WebGIS开发时，常常使用在线网络底图，由于我国的特殊国情，在线底图都是实行加密措施，导致我们想把自己采集的经纬度数据在地图展示时，令人苦恼的是坐标“飞了”。显而易见的思路是，根据网络底图的偏移，对自己的采集数据加减偏移量，从而达到比较好的叠加。但更令人痛苦的是，不同的底图，如百度和谷歌，和天地图等等不同地图，偏移量却又各不相同，如之奈何？本文作者对常用地图偏移总结如下：
- ** 火星坐标系组  高德地图，谷歌地图,ESRI的部分服务底图等都是使用火星坐标系（谷歌地图中国数据由高德提供，两者数据本质其实是一模一样的）
- ** 几乎无偏移组  天地图，OpenStreetMap是几乎没有偏移的，也就是我们的坐标不用加减偏移，直接转墨卡托就可以叠加上
- ** 万恶的百度  百度地图是最最恶心的，一般，先将自己无偏移的坐标转火星坐标系，再由火星转百度经纬度，而你叠加的一定是百度的墨卡托投影的地图，百度墨卡托不等于我们常用的墨卡托，所以仍然是特例，将百度经纬转百度墨卡托。幸运的是，我们这个库都已经能支持了。
本文于南京市中心采集某一个坐标，根据不同底图的切换，验证我们的纠偏js库的正确性。（注意：本库只用于叠加底图显示，不等于严格坐标解密，基本满足业务需求）
	
![Alt 天地图底图](http://freegis.github.io/images/demo/tianditu.png "天地图")
![Alt 百度底图](http://freegis.github.io/images/demo/baidu.png "百度地图")
![Alt 谷歌底图](http://freegis.github.io/images/demo/google.png "谷歌地图")

例子请参考[ol3坐标纠正][1].
本js代码只适用于少量点在前台叠加，如果是点线面等复杂图层且存放在PostGIS中，应进行全部图层批量转换。PostGIS转换库地址：[postgis_LayerTransform][2].

[1]: http://freegis.github.io/examples/CoordinateTransform.html
[2]: https://github.com/FreeGIS/postgis_LayerTransform

