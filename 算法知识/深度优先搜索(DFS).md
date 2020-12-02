## 深度优先搜索（DFS）

### 简介

深度优先搜索，英文缩写为DFS，即Depth First Search 。

是针对图和树的遍历算法，其过程简要来说是对每一个可能的分支路径深入到不能深入为止，而且每个节点只能访问一次。



### 基本思路

**从一个顶点V0开始，沿着一条路走到底，如果发现不能到达目标解，那就返回上一个节点，然后从另一条路走到底，重复上述，一直找到或者确定未找到为止**，通俗点说：DFS是一条道走到黑，没路了就再换一条道走到黑，知道走通为止。


### 图解逻辑

![示例图](http://blog.guohuaden.com/DFS_1.png)



![步骤1](http://blog.guohuaden.com/DFS_2.png)



![步骤2](http://blog.guohuaden.com/DFS_3.png)



![步骤3](http://blog.guohuaden.com/DFS_4.png)



![步骤4](http://blog.guohuaden.com/DFS_5.png)



![步骤5](http://blog.guohuaden.com/DFS_6.png)



![步骤6](http://blog.guohuaden.com/DFS_7.png)



![步骤7](http://blog.guohuaden.com/DFS_8.png)



![步骤8](http://blog.guohuaden.com/DFS_9.png)



![步骤9](http://blog.guohuaden.com/DFS_10.png)



![步骤10](http://blog.guohuaden.com/DFS_11.png)



### 算法实现

**DFS核心伪代码**

```
/**

*@param n: 当前开始搜索的节点

*@param d: 当前到达的深度

*@return 是否有解 

*/

bool DFS(Node n ,int d) {

    if (isEnd(n,d)) {//判断是否达到条件
        return trun;
    }

    for (Node nextNode in n){//遍历相邻的节点nextNode

        if(!visit[nextNode]){

            visit[nextNode] = true;//在下一次搜索中，nextNode不能再次出现

            if(DFS(nextNode,d+1)){//如果搜索出有解

               //做些其他的事情，例如记录结果深度等
                return true;
            }
            //重新设置成false，因为它有可能在下一次搜索的别的 路径中
           visit[nextNode] = false;
        }
    }

    return false;
}
```



**代码框架**

```
void DFS(Node n){

    if(达到结束状态){
        ... //根据题意，做一些相应的操作
        retrun;
    }
    
    if(越界/不合法状态){
        return;
    }

    for(Node nextNode in n){
        if(扩张方法达到合法状态){
            修改操作;//根据题意，做一些相应的操作
            做访问过标记;
            DFS(nextNode);
            还原标记; //根据题意决定是否加上还原标记，如果加上就是回溯法。
        }
    }
}
```



### 伪代码分析

1. 访问路径的确定。根据不同的题目思考怎么访问一个路径，如何实现遍历

2. 起点条件。从哪个点开始访问？是否每个点都需要当作起点？所以第一次遍历调用DFS的时机至关重要

3. 递归参数。怎么在访问的节点上继续向下个节点访问，实现递归需要传递什么参数？

4. 结束条件。访问的结束条件是什么？符合题意的结束条件或者临界点作为结束的判断依据

5. 访问标志。将已访问且不符合条件的的节点做标记，防止重复访问

6. 优化。