
之所以想到这个问题是因为今天尝试用python解LeetCode每日一题时想要在原函数之外另写一个函数做递归循环结果发现死活过不去，遂开始研究Python的相关性质

首先Python并不能直接访问类内的另一个对象

```python
class test:

    a=1

    b=2

    def dd(self,c):

        print("{},{}".format(self.a,c))

        self.tt()

  

    def tt():

        print("dd")

  

if __name__=="__main__":

    e=test()

    e.dd(3)
```

```shell
(base) PS C:\Users\F.F.Chopin\Desktop\code\c-experiemt> python a.py
1,3
Traceback (most recent call last):
  File "C:\Users\F.F.Chopin\Desktop\code\c-experiemt\a.py", line 14, in <module>
    e.dd(3)
  File "C:\Users\F.F.Chopin\Desktop\code\c-experiemt\a.py", line 6, in dd
    self.tt()
TypeError: tt() takes 0 positional arguments but 1 was given
```

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

```shell
(base) PS C:\Users\F.F.Chopin\Desktop\code\c-experiemt> python a.py
1,3
dd
```

很顺利得执行了

当静态方法访问对象属性时

```python
class test:

    a=1

    b=2

    def dd(self,c):

        print("{},{}".format(self.a,c))

        self.tt(2)

  

    @staticmethod

    def tt():

        print("{}".format(self.a))

  
  

if __name__=="__main__":

    e=test()

    e.dd(3)
```

```shell
(base) PS C:\Users\F.F.Chopin\Desktop\code\c-experiemt> python a.py
1,3
Traceback (most recent call last):
  File "C:\Users\F.F.Chopin\Desktop\code\c-experiemt\a.py", line 15, in <module>
    e.dd(3)
  File "C:\Users\F.F.Chopin\Desktop\code\c-experiemt\a.py", line 6, in dd
    self.tt(2)
TypeError: tt() takes 0 positional arguments but 1 was given
```

很显然不行

还可以用类的名称直接访问静态方法

```python
class test:

    a=1

    b=2

    def dd(self,c):

        print("{},{}".format(self.a,c))

        test.tt()

  

    @staticmethod

    def tt():

        print("d")

  
  

if __name__=="__main__":

    e=test()

    e.dd(3)
```

```shell
(base) PS C:\Users\F.F.Chopin\Desktop\code\c-experiemt> python a.py
1,3
d
```

尝试在静态方法内访问静态方法（递归）

```python
class test:

    a=1

    b=2

    def dd(self,c):

        print("{},{}".format(self.a,c))

        test.tt(5)

  

    @staticmethod

    def tt(t):

        t=t-1

        if t==0:

            print("t")

            return 0

        test.tt(t)

        return 0

  
  

if __name__=="__main__":

    e=test()

    e.dd(3)
```

```shell
(base) PS C:\Users\F.F.Chopin\Desktop\code\c-experiemt> python a.py                                                                                                                                                         1,3
t
```

尝试传递对象作为参数试试能不能访问熟悉

```python
class test:

    a=1

    b=2

    def dd(self,c):

        print("{},{}".format(self.a,c))

        test.tt(self)

  

    @staticmethod

    def tt(t):

        print(t.a)

  
  

if __name__=="__main__":

    e=test()

    e.dd(3)
```

```shell
(base) PS C:\Users\F.F.Chopin\Desktop\code\c-experiemt> python a.py
1,3
1
```

答案是可以的