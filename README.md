# SecondHomework介绍
笔试做的是B卷的同学还记得这道题目吗？

（2019年10月20日2点08分之前fork的同学拉了不能跑起来的话【应该都能跑】，如果不知道怎么更新，直接删了重新fork【我只是把所有的东西都push上来了怕你们没点击import，后面又不知道怎么做，拉后面的应该拉下来等待结束就好】前面的拉了能跑的话不用重拉，我没改动代码和数据）

`小D学长负责安排值班，需要把一些人安排在一张值班表上，但是大多数人并不是所有时间都有空，每个人的情况都有所不同（比如有的时间段不能去），他太难了，简直快疯了，请你救救小D学长，帮忙设计一个排班的思路，可以尽量让所有人都被安排上，并且尽量让所有时间段都有人值班（情况示例：周一到到周五，假如每天有四个时间段需要安排人值班，一个时间段最多只能有两人，每个人只能被只能被安排两次，一共有20人，且这20个人各自的情况足够随机的且是可以被安排在这张表上的）（有一定思路即可酌情给分哦，解决给出的示例情况即可得满分。大鸽就直接解决通用情况吧，但是没有实际卷面加分哦（即一个学生能被安排的次数为m，时间段所能被安排的人数为n））`

我记得当时貌似还是很多同学写出思路了呀，现在需要你们来实现这样一个算法。

**因为接口概念抽象，但是运用方式不难，所以以下没有涉及到接口相关的，以下内容请完全使用面向对象的知识来解答**



## 考虑到直接实现有一定困难现在把参考答案给出来，自己用面向对象的知识去实现。

 

参考答案：（**注意**：此答案为个人解答非最终最优解答，经多次测试，不是冲突数据都能排上，如果看到以下答案有自己的更好的实现方法可自己实现，文中的m和n对应上述题中的m和n）

将所有时间段排成一个表格，并把所有人的名字映射到能去的时间段，然后进行以下操作：

1. 对能去时间段数量小于等于m的名字，进行双向绑定。将学生名字数量小于等于n的时间段上的学生进行双向绑定（即此时间段已经安排这些绑定的学生，这些学生被安排的时间段之一为该时间段）。
2. 在不是该名字绑定时间段中清除那些已经被绑定了m次的名字，并重新检查是否存在某时间段当中只有小于等于n个名字的时间段，若存在，就跳回第一步。按顺序执行。
3. 查看此时是否所有人已经都被绑定了m次，且所有班次都有小于等于n个名字，若满足，则不进行下一步，并完成排班。
4. 在所有时间段中寻找有n+1个名字的时间段，若没有找到则寻找n+2个名字的时间段，并依次递增，知道找到至少为一个时停止寻找。
5. 在上一步骤中得到的那些时间段中挑出绑定名字最多的那个时间段，若并列则随机选择。
6. 在上一步找到的那个时间段中，挑出  （m - x）值最小的那个名字，并对他与该时间段进行双向绑定。（x：该值为学生被绑定的次数）
7. 执行第2步



以上思路总体思路就是，将最不好排的几个放在前面排。



## 做作业步骤

* 把整个项目fork到你的github

  ![TIM截图20191020000643](README/TIM截图20191020000643.png)

* 进入你想存项目的文件夹使用git bash将整个工程拉下来

  进入到你fork的仓库里复制链接

  ![TIM截图20191020000804](README/TIM截图20191020000804.png)

  ```bash
  git clone https://github.com/你的github名/ThirdHomework.git
  ```

* 使用idea打开这个项目

  这个不教，跟打开普通项目一样

* 等待idea完成项目构建

* 构建完成之后开始你的艰苦一周

* 主程序在这里，data包里面是我给你提供的需要排班人员数据，这里我已经提前给你生成了Data的对象，Data的具体实现细节不用太在意。以后都会学到用到。

  ![TIM截图20191019230824](README/TIM截图20191019230824.png)

## 给定数据说明

* Data类和数据使用说明

  Data中你会用到的只有一个成员变量也就是`datas`里面有我为你准备的所有需要被排班的人员的数据

  **如何取得**`datas`？

  ```java
  Data data = new Data();//初始化实例化一个Data的对象
  data.datas//直接使用Data的实例就可以取得datas
  ```

  datas如何使用？

  * datas里面有4组数据，任选一组去实现排班即可，给你四组是让你确认你写的算法是否适用所有足够随机的且是可以被安排在这张表上的数据

    ```java
    //例如我们现在需要取得第一组数据
    data.datas.get(0);
    //以下说明一下datas你可能会用到的一些方法和属性
    datas.get(索引参数);//get用来取得里面的数据，索引同样和数组一样从0开始
    datas.size();//取得里面数据的个数
    ```

  * 一组具体数据的说明

    ```java
    //例如这里我们取得的是上面的第一组数据，并且我们把这组数据存下来为students
    ArrayList<Student> students = data.datas.get(0);//前面那个类型具体是什么可以不用在意，自己感兴趣可以去了解，这其实就是你们上一个作业里那个可以自动扩张的动态数组，只是现在里面的数据类型是Student
    
    //一些属性和方法详解
    students.get(索引参数);//get用来取得里面的数据，索引同样和数组一样从0开始
    students.size();//同上，获得里面到底有多少个元素，类似于数组的length
    ```

  * 取得具体的学生元素和学生元素里面的数据说明

    ```java
    //上面的students取得的是具体的学生类对象，例如我们也取第0个
    Student student = students.get(0);
    
    student.getName();//取得这个人的名字
    student.getSuitableTurns();//取得这个人可以去值班的所有时间段的集合，用法同上
    ```

  * 空闲时间说明

    ```java
    //假如你利用上面的student取得了他第一个可以去值班的时间段（也就是第0个索引）
    Turn turn = student.getSuitableTurns().get(0);
    
    turn.getWorkDay();//这个时间段在星期几（1就是星期一，2就是星期二以此类推）
    turn.getDayTime();//这个时间段在这一天的第几个时间段（一天有四个时间段，分别是1，2，3，4）
    
    ```



你需要实现一个算法，将这些同学合理的排到班次上：

**情况示例：**

> 周一到到周五，假如每天有四个时间段需要安排人值班，一个时间段最多只能有两人，每个人只能被只能被安排两次，一共有20人，且这20个人各自的情况足够随机的且是可以被安排在这张表上的

**学生类和时间段类（Turn）可以根据自己的情况进行拓展，也可以自己重新封装，但是切记不要改动其中原有的属性和方法，否则数据类将无法正常给予数据**

以上给出的数据都是足够随机且可以排到一张表的。

排完之后把每个时间段里面是哪些人输出用合理的方式输出到控制台。

例如：

```tiki wiki
星期一第一轮: person2,person9
星期一第二轮: person1,person19
星期一第三轮: person3,person15
星期一第四轮: person17,person7
星期一第一轮: person14,person5
星期二第二轮: person9,person8
星期二第三轮: person5,person3
		.
		.
		.
		.
星期五第四轮: person2,person9
```

我这个样子蛮丑的，你如果能输出得更漂亮，可以选择自己的输出方式。

### 完成作业之后

请按要求提交pull requests到我的仓库 （怎么提，百度）

![TIM截图20191020015027](README/TIM截图20191020015027-1571507477170.png)

标题（title）格式同发送邮件的格式，因为该pull requests提交之后是对所有人可见，本次lv4会进行重复度计算，每个人都会有自己的风格，一百个人写一个程序就有一百种写法和代码样式和结构，所以请大家不要抄袭，但是我觉得想完成lv4的同学也不会想通过抄袭来完成作业。但是遇到瓶颈是可以借鉴别人的，这也是一个学习的过程。
