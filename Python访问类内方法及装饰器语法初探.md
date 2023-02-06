
之所以想到这个问题是因为今天尝试用python解LeetCode每日一题时想要在原函数之外另写一个函数做递归循环结果发现死活过不去，遂开始研究Python的相关性质

首先Python并不能直接访问类内的另一个对象


需要使用装饰器@staticmethod让方法变为静态方法

静态方法不需要self参数

我们先试试没有参数的情况

```python
class test:
    a=1
    b=2
    def dd(self,c):
        print("{},{}".format(self.a,c))
        self.tt()
    @staticmethod
    def tt():
        print("dd")
if __name__=="__main__":
    e=test()
    e.dd(3)
```
