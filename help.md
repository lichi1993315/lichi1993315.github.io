帮助文档？？？
======
本来我并不愿意这么早就写这个，毕竟功能还没完全定型，但是还是写吧。。。
--------

文件结构
--------
img 是图片，里面存了地块和怪物图片
js/plugins 是插件
    ./MVMota.js 这是主文件，主要功能都在这里面实现的
    ./MVMotaAtcTypes.js 攻击类型
    ./MVMotaAtcTypes.js 防御类型
    ./MVMotaItem.js 物品
    ./MVMotaMonsters.js 怪物
--------
怪物设置
--------
    好吧，怪物的图片是没有绑定在数据库中的，你们都不要多想，怪物图片真的只是图片。
    另外，数组的第一项是null只是为了方便，你要是改了，MVMota.js里面的一些处理可能就坏了。

    我来给大家翻译一下。。。
    id，这项我是当作主键(key)来用的，所以，这一项尽(qian)量(wan)不要让它重复
    name，名字，不多讲
    hp，生命
    atc，攻击力
    def，防御力
    money，身上带的钱，打死就都归你啦
    atcType，攻击类型
    defType，防御类型，攻防可不是简单的数字加减，，，这个可以做出奇妙的生克关系？
    {"id":1,"name":"Green Slime","hp":35,"atc":18,"def":1,"money":1,"atcType":1,"defType":1},
    这东西，就是一个js的object，你可以随便往里面添加删除项目，不过尽量不要删，毕竟我的整个规划的数据结构就是这些，删了多不好。。。

--------
物品设置
--------
    一样，物品的图片也没有绑定，这只是个比较简单的版本。
    况且我们要内涵，图片这种浮华的东西，，，用的时候再放就好啦

    跟怪物差不多
    不过，只有 amount，数量 这一个简单的属性
    剩下的，你可以叫事件？或者叫相应事件的方法。。。
    简而言之，这些脚本，里面还可以写脚本。不过一般来讲，就让里面是一个function就好，毕竟我的数据结构就是这么安排的。
    神奇不？在这里，你可以定义响应各各事件的方法，用完全的js语言。就跟事件里面的 脚本 选项一样。
    当然，这些function的触发时机是一定的。（定义在MVMota.Item里面）
    另外，如果是""，这样的空字符串，那么他里面实际上是默认的"(function(){})"就是一个什么都不干的空函数。

    具体的一些小技巧，可以参考我已经写好的道具。
    
    另，本来想写在json里面的，结果json对function的支持就呵呵了。不过现在这么不专业，就意味着你可以缩进他们了，或者，把匿名函数写成实名的。
    又另，放在js里面也不怎么样，毕竟这次你需要把4，5个插件同时打开。。。

--------
攻击类型和防御类型
--------
    这是我迄今为止干过的最装逼的事情了
    A对B一次攻击造成的伤害=A的攻击力*A的攻击类型对B的防御类型的效果系数-B的防御力*B的防御类型对A的攻击类型的效果系数
    看着这个神奇的公式，
    你就会发现，这俩类型是类型对类型，这样我们就可以愉快的撸属性攻击和xx抗性了

    里面有个Hero的类型，这是为了神奇道具做准备的（屠龙刀，十字架）

-------
图片
-------
    图片我并没有绑定到数据上，所以，只要放上就能用，就这么，呃，简单

-------
楼层
-------
    楼层，一定要绑定在？注册在楼层表MVMota.MotaFloorList.list里面，以防不测，对。
-------
道具
-------
    道具功能的实现，实在毕竟简单？还是复杂，看代码吧，毕竟只在事件里写太费劲，还是有部分在外面漂着。