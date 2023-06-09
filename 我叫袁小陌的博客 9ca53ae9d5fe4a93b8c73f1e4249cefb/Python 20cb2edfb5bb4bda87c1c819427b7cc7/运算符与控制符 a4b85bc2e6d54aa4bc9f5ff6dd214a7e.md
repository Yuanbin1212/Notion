# 运算符与控制符

Last edited time: May 4, 2023 2:00 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: Python

1. 算数运算符

```python
print(10 + 3.1)
print(10 + 3)
print(10 / 3)  # 结果带小数
print(10 // 3)  # 只保留整数部分
print(10 % 3) # 取模、取余数
print(10 ** 3) # 取模、取余数
```

1. 比较运算符

```python
# 2、比较运算符: >、>=、<、<=、==、!=
print(10 > 3)
print(10 == 10)

print(10 >= 10)
print(10 >= 3)

name=input('your name: ')
print(name == 'egon')
```

1. 赋值运算符

```python
3.1 =：变量的赋值
3.2 增量赋值：
age = 18
# age += 1  # age=age + 1
# print(age)

age*=3
age/=3
age%=3
age**=3 # age=age**3

3.3 链式赋值
x=10
y=x
z=y
z = y = x = 10 # 链式赋值
print(x, y, z)
print(id(x), id(y), id(z))

3.4 交叉赋值
# m=10
# n=20
print(m,n)
交换值
temp=m
m=n
n=temp
print(m,n)

m,n=n,m # 交叉赋值
print(m,n)

3.5 解压赋值
# salaries=[111,222,333,444,555]
把五个月的工资取出来分别赋值给不同的变量名
mon0=salaries[0]
mon1=salaries[1]
mon2=salaries[2]
mon3=salaries[3]
mon4=salaries[4]

解压赋值
mon0,mon1,mon2,mon3,mon4=salaries
print(mon0)
print(mon1)
print(mon2)
print(mon3)
print(mon4)

mon0,mon1,mon2,mon3=salaries # 对应的变量名少一个不行
mon0,mon1,mon2,mon3,mon4,mon5=salaries # 对应的变量名多一个也不行

引入*，可以帮助我们取两头的值，无法取中间的值
取前三个值
x,y,z,*_=salaries=[111,222,333,444,555] # *会将没有对应关系的值存成列表然后赋值给紧跟其后的那个变量名，此处为_
print(x,y,z)
print(_)

取后三个值
*_,x,y,z=salaries=[111,222,333,444,555]
print(x,y,z)

x,*_,y,z=salaries=[111,222,333,444,555]
print(x,y,z)

salaries=[111,222,333,444,555]
_,*middle,_=salaries
print(middle)

解压字典默认解压出来的是字典的key
# x,y,z=dic={'a.txt':1,'b':2,'c':3}
# print(x,y,z)
```

1. 可变与不可变类型

```python
可变类型：值改变，id不变，证明改的是原值，证明原值是可以被改变的
不可变类型：值改变，id也变了，证明是产生新的值，压根没有改变原值，证明原值是不可以被修改的

2、验证
2.1 int是不可变类型
x=10
print(id(x))
x=11 # 产生新值
print(id(x))

2.2 float是不可变类型
x=3.1
print(id(x))
x=3.2
print(id(x))

2.3 str是不可变类型
x="abc"
print(id(x))
x='gggg'
print(id(x))

小结：int、float、str都被设计成了不可分割的整体，不能够被改变

2.4 list是可变类型
l=['aaa.txt','bbb','ccc']
print(id(l))
l[0]='AAA'
print(l)
print(id(l))

2.5 dict
dic={'k1':111,'k2':222}
print(id(dic))
dic['k1']=3333333333
# print(dic)
print(id(dic))

2.6 bool不可变

关于字典补充：
定义：{}内用逗号分隔开多key:value,
          其中value可以是任意类型
          但是key必须是不可变类型

dic={
    'k1':111,
    'k2':3.1,
    'k3':[333,],
    'k4':{'name':'egon'}
}

dic={
    2222:111,
    3.3:3.1,
    'k3':[333,],
    'k4':{'name':'egon'}
}
print(dic[3.3])

dic={[1,2,3]:33333333}
dic={{'a.txt':1}:33333333}
```

1. 条件的类型

```python
什么是条件？什么可以当做条件？为何要要用条件？
第一大类：显式布尔值
1 条件可以是：比较运算符
age = 18
print(age > 16)  # 条件判断之后会得到一个布尔值

2 条件可以是：True、False
is_beautiful=True
print(is_beautiful)

第二大类：隐式布尔值，所有的值都可以当成条件去用
其中**0、None、空**(空字符串、空列表、空字典)=》代表的布尔值为False，其余都为真
```

1. 逻辑运算符

```python
一：not、and、or的基本使用
not：就是把紧跟其后的那个条件结果取反
ps:not与紧跟其后的那个条件是一个不可分割的整体
print(not 16 > 13)
print(not True)
print(not False)
print(not 10)
print(not 0)
print(not None)
print(not '')

and：逻辑与，and用来链接左右两个条件，两个条件同时为True，最终结果才为真
print(True and 10 > 3)

print(True and 10 > 3 and 10 and 0) # 条件全为真，最终结果才为True
print( 10 > 3 and 10 and 0 and 1 > 3 and 4 == 4 and 3 != 3)  # 偷懒原则

or：逻辑或，or用来链接左右两个条件，两个条件但凡有一个为True，最终结果就为True，
           两个条件都为False的情况下，最终结果才为False
print(3 > 2 or 0)
print(3 > 4 or False or 3 != 2 or 3 > 2 or True) # 偷懒原则

二：优先级not>and>or
ps：
如果单独就只是一串and链接，或者说单独就只是一串or链接，按照从左到右的顺讯依次运算即可（偷懒原则）
如果是混用，则需要考虑优先级了

res=3>4 and not 4>3 or 1==3 and 'x' == 'x' or 3 >3
print(res)

#       False                 False              False
res=(3>4 and (not 4>3)) or (1==3 and 'x' == 'x') or 3 >3
print(res)

res=3>4 and ((not 4>3) or 1==3) and ('x' == 'x' or 3 >3)
print(res)
```

1. 成员运算与身份运算

```python
1、成员运算符
print("egon" in "hello egon") # 判断一个字符串是否存在于一个大字符串中
print("e" in "hello egon") # 判断一个字符串是否存在于一个大字符串中

print(111 in [111,222,33]) # 判断元素是否存在于列表

判断key是否存在于字典
print(111 in {"k1":111,'k2':222})
print("k1" in {"k1":111,'k2':222})

not in
print("egon" not in "hello egon") # 推荐使用
print(not "egon" in "hello egon") # 逻辑同上，但语义不明确，不推荐

2、身份运算符
is # 判断的是id是否相等
```

1. 流程控制之if

```python
print(1)
# print(2)
# print(3)
# if 条件:
    # 代码
# print(4)
# print(5)
'''
语法1:
if 条件:
    代码

'''
age = 60
is_beautiful = True
star = '水平座'

if age > 16 and age < 20 and is_beautiful and star == '水平座':
    print('我喜欢，我们在一起吧。。。')

print('其他代码.............')

'''
语法2:
if 条件:
    代码
else:
    代码
'''

age = 60
is_beautiful = True
star = '水平座'

if age > 16 and age < 20 and is_beautiful and star == '水平座':
    print('我喜欢，我们在一起吧。。。')
else:
    print('阿姨好，我逗你玩呢，深藏功与名')

print('其他代码.............')

'''
语法3:
if 条件1:
    代码
elif 条件2:
    代码
elif 条件3:
    代码
'''
score=73
if score >= 90:
    print('优秀')
elif score >= 80 and score < 90:
    print('良好')
elif score >= 70 and score < 80:
    print('普通')

改进
score = input('请输入您的成绩：') # score="18"
score=int(score)

if score >= 90:
    print('优秀')
elif score >= 80:
    print('良好')
elif score >= 70:
    print('普通')

'''
语法3:
if 条件1:
    if 条件:
        代码1
    代码2
elif 条件2:
    代码
elif 条件3:
    代码
...
else:
    代码
'''
score = input('请输入您的成绩：') # score="18"
score=int(score)

if score >= 90:
    print('优秀')
elif score >= 80:
    print('良好')
elif score >= 70:
    print('普通')
else:
    print('很差，小垃圾')

print('=====>')

'''
if嵌套if
'''
age = 17
is_beautiful = True
star = '水平座'

if 16 < age < 20 and is_beautiful and star == '水平座':
    print('开始表白。。。。。')
    is_successful = True
    if is_successful:
        print('两个从此过上没羞没臊的生活。。。')
else:
    print('阿姨好，我逗你玩呢，深藏功与名')

print('其他代码.............')
```

1. 流程控制之while循环

```python
1、循环的语法与基本使用
# '''
# print(1)
# while 条件:
     # 代码1
     # 代码2
     # 代码3
# print(3)
# '''

count=0
while count < 5: # 5 < 5
    print(count) # 0,1,2,3,4
    count+=1 # 5

print('顶级代码----->')

2、死循环与效率问题
count=0
while count < 5: # 5 < 5
    print(count) # 0,1,2,3,4

while True:
    name=input('your name >>>> ')
    print(name)

纯计算无io的死讯会导致致命的效率问题
while True:
    1+1

while 1:
    print('xxxx')

3、循环的应用
# username = 'egon'
# password = '123'

两个问题：
1、重复代码
2、输对了应该不用再重复
while True:
    inp_name=input('请输入您的账号：')
    inp_pwd=input('请输入您的密码：')

    if inp_name  == username and inp_pwd == password:
        print('登录成功')
    else:
        print('账号名或密码错误')

4、退出循环的两种方式
方式一：将条件改为False,等到下次循环判断条件时才会生效
tag=True
while tag:
    inp_name=input('请输入您的账号：')
    inp_pwd=input('请输入您的密码：')

    if inp_name  == username and inp_pwd == password:
        print('登录成功')
        tag = False # 之后的代码还会运行，下次循环判断条件时才生效
    else:
        print('账号名或密码错误')

    # print('====end====')

方式二：break，只要运行到break就会立刻终止本层循环
while True:
    inp_name=input('请输入您的账号：')
    inp_pwd=input('请输入您的密码：')

    if inp_name  == username and inp_pwd == password:
        print('登录成功')
        break # 立刻终止本层循环
    else:
        print('账号名或密码错误')

    # print('====end====')

7、while循环嵌套与结束
# '''
# tag=True
# while tag:
    # while tag:
        # while tag:
            # tag=False
    

每一层都必须配一个break
# while True:
    # while True:
        # while True:
            # break
        # break
    # break
# '''
# break的方式
while True:
    inp_name=input('请输入您的账号：')
    inp_pwd=input('请输入您的密码：')

    if inp_name  == username and inp_pwd == password:
        print('登录成功')
        while True:
            cmd=input("输入命令>: ")
            if cmd == 'q':
                break
            print('命令{x}正在运行'.format(x=cmd))
        break # 立刻终止本层循环
    else:
        print('账号名或密码错误')

    # print('====end====')

# 改变条件的方式
tag=True
while tag:
    inp_name=input('请输入您的账号：')
    inp_pwd=input('请输入您的密码：')

    if inp_name  == username and inp_pwd == password:
        print('登录成功')
        while tag:
            cmd=input("输入命令>: ")
            if cmd == 'q':
                tag=False
            else:
                print('命令{x}正在运行'.format(x=cmd))
    else:
        print('账号名或密码错误')

8、while +continue：结束本次循环，直接进入下一次
强调：在continue之后添加同级代码毫无意义，因为永远无法运行
count=0
while count < 6:
    if count == 4:
        count+=1
        continue
        # count+=1 # 错误
    print(count)
    count+=1

9、while +else：针对break
count=0
while count < 6:
    if count == 4:
        count+=1
        continue
    print(count)
    count+=1
else:
    print('else包含的代码会在while循环结束后，并且while循环是在没有被break打断的情况下正常结束的，才会运行')

count=0
while count < 6:
    if count == 4:
        break
    print(count)
    count+=1
else:
    print('======>')

应用案列：
版本1：
count=0
tag=True
while tag:
    if count == 3:
        print('输错三次退出')
        break
    inp_name=input('请输入您的账号：')
    inp_pwd=input('请输入您的密码：')

    if inp_name  == username and inp_pwd == password:
        print('登录成功')
        while tag:
            cmd=input("输入命令>: ")
            if cmd == 'q':
                tag=False
            else:
                print('命令{x}正在运行'.format(x=cmd))
    else:
        print('账号名或密码错误')
        count+=1

版本2：优化
count = 0
while count < 3:
    inp_name = input('请输入您的账号：')
    inp_pwd = input('请输入您的密码：')

    if inp_name == username and inp_pwd == password:
        print('登录成功')
        while True:
            cmd = input("输入命令>: ")
            if cmd == 'q':  # 整个程序结束，退出所有while循环
                break
            else:
                print('命令{x}正在运行'.format(x=cmd))
        break
    else:
        print('账号名或密码错误')
        count += 1
else:
    print('输错3次，退出')

# while True:
    # print('ok')
# else:
    # print('====>')
```

1. 流程控制之for循环

```python
'''
# 1、什么是for循环
    # 循环就是重复做某件事，for循环是python提供第二种循环机制

# 2、为何要有for循环
    # 理论上for循环能做的事情，while循环都可以做
    # 之所以要有for循环，是因为for循环在循环取值（遍历取值）比while循环更简洁

# 3、如何用for循环
# 语法：
# for 变量名 in 可迭代对象:# 可迭代对象可以是：列表、字典、字符串、元组、集合
    # 代码1
    # 代码2
    # 代码3
    # ...
# '''
一：for基本使用之循环取值
案例1：列表循环取值
简单版
l = ['alex_dsb', 'lxx_dsb', 'egon_nb']
for x in l:  # x='lxx_dsb'
    print(x)

复杂版：
l = ['alex_dsb', 'lxx_dsb', 'egon_nb']
i=0
while i < 3:
    print(l[i])
    i+=1

案例2：字典循环取值
简单版
dic={'k1':111,'k2':2222,'k3':333}
for k in dic:
    print(k,dic[k])

复杂版：while循环可以遍历字典，太麻烦了

案例3：字符串循环取值
简单版
msg="you can you up,no can no bb"
for x in msg:
    print(x)

复杂版：while循环可以遍历字典，太麻烦了

二：总结for循环与while循环的异同
1、相同之处：都是循环，for循环可以干的事，while循环也可以干
2、不同之处：
          while循环称之为条件循环，循环次数取决于条件何时变为假
          for循环称之为"取值循环"，循环次数取决in后包含的值的个数
for x in [1,2,3]:
    print('===>')
    print('8888')

三：for循环控制循环次数：range()
in后直接放一个数据类型来控制循环次数有局限性：
                当循环次数过多时，数据类型包含值的格式需要伴随着增加
for x in 'a.txt c':
    inp_name=input('please input your name:   ')
    inp_pwd=input('please input your password:   ')

range功能介绍
# '''
# >>> range(10)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
# >>> 
# >>> range(1,9) # 1...8
# [1, 2, 3, 4, 5, 6, 7, 8]
# >>> 
# >>> range(1,9,1) # 1 2 3 4 5 6 7 8 
# [1, 2, 3, 4, 5, 6, 7, 8]
# >>> range(1,9,2) # 1 3 5 7 
# [1, 3, 5, 7]
# '''
for i in range(30):
    print('===>')

for+break: 同while循环一样
for+else：同while循环一样
username='egon'
password='123'
for i in range(3):
    inp_name = input('请输入您的账号：')
    inp_pwd = input('请输入您的密码：')

    if inp_name == username and inp_pwd == password:
        print('登录成功')
        break
else:
    print('输错账号密码次数过多')

四：range补充知识（了解）
1、for搭配range，可以按照索引取值，但是麻烦，所以不推荐
l=['aaa.txt','bbb','ccc'] # len(l)
for i in range(len(l)):
    print(i,l[i])

for x in l:
    print(l)
2、range()在python3里得到的是一只"会下蛋的老母鸡"

五：for+continue
for i in range(6):  # 0 1 2 3 4 5
    if i == 4:
        continue
    print(i)

六：for循环嵌套:外层循环循环一次，内层循环需要完整的循环完毕
for i in range(3):
    print('外层循环-->', i)
    for j in range(5):
        print('内层-->', j)

补充：终止for循环只有break一种方案

print('hello %s' % 'egon')
1、print之逗号的使用
print('hello','world','egon')
2、换行符
print('hello\n')
print('world')
3、print值end参数的使用
print('hello\n',end='')
print('word')
# print('hello',end='*')
# print('world',end='*')
```