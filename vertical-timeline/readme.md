# 业务所需的时间轴
## 需要实现的功能
- 时间轴，长轴，有时间节点（标示年份）；轴上左或右分布事件
- 文字区域，表示事件，有事件发生时间以及事件内容
- 有动态交互效果
    - 默认文字部分隐藏，在拉动滚动条或者刷新页面的时候文字出现
- 自响应页面伸缩变化
    - 页面较大时根据文字节点计数的奇偶分布在时间轴的左右两边
    - 页面较小时使文字节点统一分布在轴的右边
## 实现原理
- HTML部分使用ul>li标签构造时间轴结构，一个事件使用一个div
- CSS部分，更改li标签的样式，使其变长为轴；在li标签上加::after或者：：before画出时间节点；div使用:ntn-child(even)偶和:ntn-child(even)奇分别文字节点在左或者右，默认隐藏
- 使用媒体查询更改文字div的样式
- js部分主要判断文字区域是否在可见区域（fully visually），是的话增加in-view样式使其以动态效果出现

## 初级实现基本样式
- 年份节点
- 左右排布，内容时间节点

代码如下：
```
HTML文件：
<section class="timeline">
    <ul>
        <li>
            <div class="milestone">
                <div class="year">
                    <p>2016</p>
                </div>
                <div class="event">
                    <!--内容前修饰-->
                    <div class="mark"></div>
                    <div class="line"></div>
                    <!--事件内容-->
                    <time>2016.01.23</time>
                    <p>this one is event content</p>
                </div>
                <!--more event-->
            </div>
        </li>
         <!--more li item-->
    </ul>
</section>
```
```
LESS文件:
.timeline {
  ul {
    padding-bottom: 24px;
    li {
      list-style: none;
      position: relative;
      padding-top: 70px;
      width: 2px;
      margin: 0 auto;
      background-color: #EFEFEF;
      .year {
        background-color: #FD9827;
        position: absolute;
        top: 0;
        left:-28px;
        width: 58px;
        height: 58px;
        /* Rotate to demon*/
        -webkit-transform: rotate(-45deg);
        -moz-transform: rotate(-45deg);
        -ms-transform: rotate(-45deg);
        -o-transform: rotate(-45deg);
        transform: rotate(-45deg);
        p {
          color:#FFFFFF;
          text-align: center;
          font-size:16px;
          /* Rotate back to horizon*/
          -webkit-transform: rotate(45deg);
          -moz-transform: rotate(45deg);
          -ms-transform: rotate(45deg);
          -o-transform: rotate(45deg);
          transform: rotate(45deg);
        }
      }
      //偶数事件节点
      .event:nth-child(even) {
        padding-bottom:15px;
        left: 220px;
        position: relative;
        width: 400px;
        .mark {
          border:1px solid #CCCCCC;
          position: absolute;
          left:-200px;
          top:8%;
          width: 27px;
          height: 27px;
          /* Rotate to demon*/
          -webkit-transform: rotate(-45deg);
          -moz-transform: rotate(-45deg);
          -ms-transform: rotate(-45deg);
          -o-transform: rotate(-45deg);
          transform: rotate(-45deg);
        }
        .line {
          position: absolute;
          left:-166px;
          top:29%;
          width:160px;
          height:1px;
          padding:0px;
          background-color:#CCCCCC;
        }
        time {
          color: #333333;
          font-size: 16px;
        }
        p {
          margin-top: -2px;
          color: #666666;
          font-size: 14px;
        }
      }
       //奇数事件节点
      .event:nth-child(odd) {
        .....
      }
    }
  }
}
```
实现效果如图：
![image](http://osgsqkt7d.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202018-05-18%20%E4%B8%8B%E5%8D%883.10.45.png)