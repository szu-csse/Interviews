#python：直接赋值、浅拷贝和深拷贝的区别

题目来源：
腾讯运营开发一面

定义：
直接赋值：对象的引用，比如a=b
浅拷贝：拷贝父对象，不拷贝子对象，比如：c=copy.copy(a)
深拷贝：拷贝父对象和子对象（其实就是完全独立了），比如d=b.copy.deepcopy(a)

代码参考：
```
import copy
a=[1,2,3,4,['abc','d']]
#在a中，1,2,3,4均为其父对象，而['abc','d']为子对象
b=a
c=copy.copy(a)
d=copy.deepcopy(a)
a.append([6,1])#改变了对象，直接添加[6,1],影响a和b
a.extend([3,4])#不改变对象， 分别添加3，4，影响a和b
a[4].append('?')#对子对象做操作，会影响c
a[4].extend(['@'])#对子对象做操作，会影响c
a[4][0]='s' #对子对象做操作，会影响c
a[0]=0 #对父对象做操作，只影响a和b
print('a:',a)
#b为赋值，因此对a的操作基本都会影响b
print('b:',b)
#c为浅拷贝，所以父对象的操作是不会受影响，只会影响子对象，即原来的['abc','d']
print('c:',c)
#d为深拷贝，所以对a的所有操作与d无关
print('d:',d)
```
![代码结果参考](https://gitee.com/allen_lo/test/raw/master/img/test.png)


解释：
extend和append的区别在于extend是不会改变list的对象的，因此需要将列表传进去，而且确保是单个元素的添加，而append是会改变对象的，直接把列表整个对象添加进去。
值得注意的是，上面举例是对a的操作，其实对b进行一样的操作也是有同样效果。

[参考](https://blog.csdn.net/colourful_sky/article/details/81263998)
