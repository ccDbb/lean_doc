#### 1，display：flex|inline-flex|-webkit-flex

#### 2，容器属性===父级属性

##### 1）flex-direction: row |row-reverse|colume|colume-reverse   

​	（横排|横排反向|竖排|竖排反向）

##### 2）flex-wrap:nowrap|wrap|wrap-reverse 

​	(包裹：不换行|换行第一行在上|换行第一行在下)

##### 3）flex-flow:row nowrap  

​	 (是flex-direction和flex-wrap的合并写法)

##### 4）justify-content:flex-start|flex-end|center|space-between|space-around;

​	(主轴对齐方式也就是横轴的对方式：开始对齐|对齐末尾|中间对齐|两端对齐，项目之间的间隔都相等 | 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。)

##### 5）align-item:flex-start|flex-end|center|baseline|stretch

​		(纵轴的对齐方式：轴的开始对齐|末未对齐|居中对齐|第一条文字的地步基线对齐|（默认值）铺满整个高度)

##### 6）align-content:flex-start|flex-end|center|space-between|space-around|stretch

(多轴是对齐方式：交叉轴的起点|交叉轴的末尾|交叉轴的中心|与交叉轴两端对齐，轴线之间间隔平均分布|轴线两侧间隔相等。|轴线占满整个高度)

#### 3，项目属性

##### 1）order:<integer>(数字)（属性定义的项目拍立顺序，值越小，越靠前）

##### 2）flex-grow:<number>/defalt 0/(定义项目放大比例，如果都是1就平均)

##### 3）flex-shrink:<number>/*defalt 1*/(定义项目缩小比例，如果空间不足时当前定义最小的属性缩小)

##### 4）flex-basis：<length>|auto (定义再分配多余空间之前，项目占据主轴的空间)

##### 5）flex:none|<flex-grow><flex-shrink><flex-basie>(前三种的合并写法)

##### 6）align-self:auto|flex-start|flex-end|center|baseline|stretch

(允许单个项目不同于其他项目的对齐方式，会覆盖align-item属性。)



script start ----- script end  

async1 start----- async2 



async1 end





