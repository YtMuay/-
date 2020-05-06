## 当代大学生快乐工具集合

* #### 超星学习通自动签到
使用方法 
1. 把[chaoxingsign.py](https://github.com/YtMuay/3CCKfHtw/blob/master/chaoxinsign/chaoxi.py)的内容 弄到腾讯云函数
1. 配置你所需的参数 参数详情请看[chaoxingsign.py's params.md](https://github.com/YtMuay/3CCKfHtw/blob/master/chaoxinsign/576J8jPF/5/7/6J8jP/F/chaoxingsign.py's%20params.md)

## 本地使用教程
1. python3环境
2. 安装模块: pip install requests
3. 在同目录下的conf.json中写入配置
4. 双击运行...
## 云函数使用教程
1. 去腾讯云创建一个云函数,目前测试广州好像不能用.其他地区可以.
2. 环境选择`Python 3.6`
3. 内存最低实测`64M`可以跑.
4. 时间看个人课程数量.详细解释看下面
5. 测试运行,成功后设定定时触发.关于如何设定Cron也可以看下面

#### 关于时间设定
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

在`Serverless`版里面,所有课程扫描/签到一次就会停止,这样做是为了符合云函数的设计,同时也节省运行时间.  
最简单的估算办法就是:
* 签到或扫描的请求撑死不会超过2S,记为`x`
* 中间等待时间由`account.json`决定,记为`y`
* 课程数量,记为`z`
那么最后总时间应该是:   
$$z*(x+y)$$

绝大多数情况下这个请求时间可以直接忽略.

再懒人一点的话,可以直接在命令行运行并统计时间,参考Linux命令`time` 

#### 关于Cron设定
我们先来看一个例子

```
0 */10 8-12,14-18 * * 1-5
```

云函数的Cron跟Linux Cron非常相似,不过左边多了一个秒.  
以上Cron可以解释为: 

```
0 */10 8-12,14-18 * * 1-5
| |    |          | |  |
| |    |          | |  .------- 在周几     (周一到周五)
| |    |          | .---------- 在哪个月   (所有)  
| |    |          .------------ 在哪一天   (所有)
| |    .----------------------- 在几点     (8-12和14-18) 
| .---------------------------- 在第几分钟 (每隔10分钟)
.------------------------------ 在第几秒   (第0秒)
```
这是比较符合现在上课的情况的Cron,各位也可以根据这个列表进行自定义

贡献此来源原作者是[@yuban10703](https://github.com/yuban10703/chaoxingsign)
