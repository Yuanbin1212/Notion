# 文件与文件模式介绍

Last edited time: May 4, 2023 2:00 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: Python

1. 文件相关介绍
    1. 什么是文件
    文件是操作系统提供给用户/应用程序操作硬盘的一种虚拟的概念/接口
        1. 用户/应用程序(open())
        2. 操作系统（文件）
        3. 计算机硬件（硬盘）
    2. 为何要用文件
        1. 用户/应用程序可以通过文件将数据永久保存的硬盘中，即操作文件就是操作硬盘
        2. 用户/应用程序直接操作的是文件，对文件进行的所有的操作，都是在向操作系统发送系统调用，然后再由操作将其转换成具体的硬盘操作
    3. 如何用文件：open()
        1. 控制文件读写内容的模式：t和b  强调：t和b不能单独使用，必须跟r/w/a连用
        2. t文本（默认的模式）
            1. 读写都以str（unicode）为单位的
            2. 文本文件
            3. 必须指定encoding='utf-8'
        3. 二进制/bytes
        4. 控制文件读写操作的模式
            1. r只读模式
            2. w只写模式
            3. a只追加写模式
            4. +：r+、w+、a+
    
    ## 基本操作
    
    ```python
    1、打开文件
    windows路径分隔符问题
    open('C:\a.txt\nb\c\d.txt')
    解决方案一：推荐
    open(r'C:\a.txt\nb\c\d.txt')
    解决方案二：
    open('C:/a.txt/nb/c/d.txt')
    
    # f=open(r'aaa/a.txt',mode='rt') # f的值是一种变量，占用的是应用程序的内存空间
    print(f)
    x=int(10)
    
    2、操作文件：读/写文件，应用程序对文件的读写请求都是在向操作系统发送
    系统调用，然后由操作系统控制硬盘把输入读入内存、或者写入硬盘
    # res=f.read()
    # print(type(res))
    print(res)
    3、关闭文件
    # f.close() # 回收操作系统资源
    print(f)
    f.read() # 变量f存在，但是不能再读了
    
    del f     # 回收应用程序资源
    ```
    
    ## with上下文管理
    
    ```python
    # 文件对象又称为文件句柄
    
    # with open('a.txt',mode='rt') as f1: # f1=open('a.txt',mode='rt')
    #     res=f1.read()
    #     print(res)
    
    with open('a.txt',mode='rt') as f1,\
            open('b.txt',mode='rt') as f2:
        res1=f1.read()
        res2=f2.read()
        print(res1)
        print(res2)
    
        # f1.close()
        # f2.close()
    
    #指定字符编码
    '''
    强调：t和b不能单独使用，必须跟r/w/a连用
    
    t文本（默认的模式）
    1、读写都以str（unicode）为单位的
    2、文本文件
    3、必须指定encoding='utf-8'
    
    '''
    # 没有指定encoding参数操作系统会使用自己默认的编码
    # linux系统默认utf-8
    # windows系统默认gbk
    with open('c.txt',mode='rt',encoding='utf-8') as f:
        res=f.read() # t模式会将f.read()读出的结果解码成unicode
        print(res,type(res))
    
    # 内存：utf-8格式的二进制-----解码-----》unicode
    # 硬盘（c.txt内容：utf-8格式的二进制）
    ```
    
    ## 文件操作模式详解
    
    ```python
    #以t模式为基础进行内存操作
    
    1、r（默认的操作模式）：只读模式，当文件不存在时报错，当文件存在时文件指针跳到开始位置
    with open('c.txt',mode='rt',encoding='utf-8') as f:
        print('第一次读'.center(50,'*'))
        res=f.read() # 把所有内容从硬盘读入内存
        print(res)
    
    # with open('c.txt', mode='rt', encoding='utf-8') as f:
        print('第二次读'.center(50,'*'))
        res1=f.read()
        print(res1)
    
    ===============案例==================
    inp_username=input('your name>>: ').strip()
    inp_password=input('your password>>: ').strip()
    
    # 验证
    with open('user.txt',mode='rt',encoding='utf-8') as f:
        for line in f:
            # print(line,end='') # egon:123\n
            username,password=line.strip().split(':')
            if inp_username == username and inp_password == password:
                print('login successfull')
                break
        else:
            print('账号或密码错误')
    
    应用程序====》文件
    应用程序====》数据库管理软件=====》文件
    
    2、w：只写模式，当文件不存在时会创建空文件，当文件存在会清空文件，指针位于开始位置
    with open('d.txt',mode='wt',encoding='utf-8') as f:
        f.read() # 报错，不可读
        f.write('擦勒\n')
    
    强调1：
    在以w模式打开文件没有关闭的情况下，连续写入，新的内容总是跟在旧的之后
    with open('d.txt',mode='wt',encoding='utf-8') as f:
        f.write('擦勒1\n')
        f.write('擦勒2\n')
        f.write('擦勒3\n')
    
    强调2：
    如果重新以w模式打开文件，则会清空文件内容
    with open('d.txt',mode='wt',encoding='utf-8') as f:
        f.write('擦勒1\n')
    with open('d.txt',mode='wt',encoding='utf-8') as f:
        f.write('擦勒2\n')
    with open('d.txt',mode='wt',encoding='utf-8') as f:
        f.write('擦勒3\n')
    
    案例：w模式用来创建全新的文件
    文件文件的copy工具
    
    src_file=input('源文件路径>>: ').strip()
    dst_file=input('源文件路径>>: ').strip()
    with open(r'{}'.format(src_file),mode='rt',encoding='utf-8') as f1,\
        open(r'{}'.format(dst_file),mode='wt',encoding='utf-8') as f2:
        res=f1.read()
        f2.write(res)
    
    3、a：只追加写，在文件不存在时会创建空文档，在文件存在时文件指针会直接调到末尾
    with open('e.txt',mode='at',encoding='utf-8') as f:
        # f.read() # 报错，不能读
        f.write('擦嘞1\n')
        f.write('擦嘞2\n')
        f.write('擦嘞3\n')
    
    强调 w 模式与 a 模式的异同：
    1 相同点：在打开的文件不关闭的情况下，连续的写入，新写的内容总会跟在前写的内容之后
    2 不同点：以 a 模式重新打开文件，不会清空原文件内容，会将文件指针直接移动到文件末尾，
    					新写的内容永远写在最后
    
    案例：a模式用来在原有的文件内存的基础之上写入新的内容，比如记录日志、注册
    注册功能
    name=input('your name>>: ')
    pwd=input('your name>>: ')
    with open('db.txt',mode='at',encoding='utf-8') as f:
        f.write('{}:{}\n'.format(name,pwd))
    
    了解：+不能单独使用，必须配合r、w、a
    with open('g.txt',mode='rt+',encoding='utf-8') as f:
        # print(f.read())
        f.write('中国')
    
    with open('g.txt',mode='w+t',encoding='utf-8') as f:
        f.write('111\n')
        f.write('222\n')
        f.write('333\n')
        print('====>',f.read())
    
    with open('g.txt',mode='a+t',encoding='utf-8') as f:
        print(f.read())
    
        f.write('444\n')
        f.write('5555\n')
        print(f.read())
    ```
    
    ## 文件高级使用方法
    
    ### 文件模式
    
    1. x模式（控制文件操作的模式）-》了解
        
        x， 只写模式【不可读；不存在则创建，存在则报错】
        
    2. b模式补充（控制文件读写内容的模式）
        1. bytes类型转换
            1. x=10 # int(10)
            2. '你'.encode('gbk') # bytes()
    3. 文件的高级操作：控制文件指针的移动
    
    ```python
    x模式（控制文件操作的模式）-》了解
        x， 只写模式【不可读；不存在则创建，存在则报错】
    """
    # with open('a.txt',mode='x',encoding='utf-8') as f:
    #     pass
    
    # with open('c.txt',mode='x',encoding='utf-8') as f:
    #     f.read()
    
    with open('d.txt', mode='x', encoding='utf-8') as f:
        f.write('哈哈哈\n')
    
    # 控制文件读写内容的模式
    # t：
        # 1、读写都是以字符串（unicode）为单位
        # 2、只能针对文本文件
        # 3、必须指定字符编码，即必须指定encoding参数
    # b：binary模式
        # 1、读写都是以bytes为单位
        # 2、可以针对所有文件
        # 3、一定不能指定字符编码，即一定不能指定encoding参数
    
    # 总结：
    # 1、在操作纯文本文件方面t模式帮我们省去了编码与解码的环节，
    			b模式则需要手动编码与解码，所以此时t模式更为方便
    # 2、针对非文本文件（如图片、视频、音频等）只能使用b模式
    # """
    
    错误演示：t模式只能读文本文件
    with open(r'爱nmlgb的爱情.mp4',mode='rt') as f:
        f.read() # 硬盘的二进制读入内存-》t模式会将读入内存的内容进行decode解码操作
    
    with open(r'test.jpg',mode='rb',encoding='utf-8') as f:
        res=f.read() # 硬盘的二进制读入内存—>b模式下，不做任何转换，直接读入内存
        print(res) # bytes类型—》当成二进制
        print(type(res))
    
    with open(r'd.txt',mode='rb') as f:
        res=f.read() # utf-8的二进制
        print(res,type(res))
    
        print(res.decode('utf-8'))
    
    with open(r'd.txt',mode='rt',encoding='utf-8') as f:
        res=f.read() # utf-8的二进制->unicode
        print(res)
    
    with open(r'e.txt',mode='wb') as f:
        f.write('你好hello'.encode('gbk'))
    
    with open(r'f.txt',mode='wb') as f:
        f.write('你好hello'.encode('utf-8'))
        f.write('哈哈哈'.encode('gbk'))
    
    #文件拷贝工具
    src_file=input('源文件路径>>: ').strip()
    dst_file=input('源文件路径>>: ').strip()
    with open(r'{}'.format(src_file),mode='rb') as f1,\
        open(r'{}'.format(dst_file),mode='wb') as f2:
        #res=f1.read() # 内存占用过大
        #f2.write(res)
    
        for line in f1:
            f2.write(line)
    
    循环读取文件
    方式一：自己控制每次读取的数据的数据量
    with open(r'test.jpg',mode='rb') as f:
        while True:
            res=f.read(1024) # 1024
            if len(res) == 0:
                break
            print(len(res))
    
    方式二：以行为单位读，当一行内容过长时会导致一次性读入内容的数据量过大
    with open(r'g.txt',mode='rt',encoding='utf-8') as f:
        for line in f:
            print(len(line),line)
    
    with open(r'g.txt',mode='rb') as f:
        for line in f:
            print(line)
    
    with open(r'test.jpg',mode='rb') as f:
        for line in f:
            print(line)
    
    一：读相关操作
    1、readline：一次读一行
    with open(r'g.txt',mode='rt',encoding='utf-8') as f:
        # res1=f.readline()
        # res2=f.readline()
        # print(res2)
    
        while True:
            line=f.readline()
            if len(line) == 0:
                break
            print(line)
    
    2、readlines：
    with open(r'g.txt',mode='rt',encoding='utf-8') as f:
        res=f.readlines()
        print(res)
    
    强调：
    f.read()与f.readlines()都是将内容一次性读入内存，
    如果内容过大会导致内存溢出，若还想将内容全读入内存，
    
    二：写相关操作
    f.writelines()：
    with open('h.txt',mode='wt',encoding='utf-8') as f:
        # f.write('1111\n222\n3333\n')
    
        # l=['11111\n','2222','3333',4444]
        l=['11111\n','2222','3333']
        # for line in l:
        #     f.write(line)
        f.writelines(l)
    
    with open('h.txt', mode='wb') as f:
        # l = [
        #     '1111aaa1\n'.encode('utf-8'),
        #     '222bb2'.encode('utf-8'),
        #     '33eee33'.encode('utf-8')
        # ]
    
        # 补充1：如果是纯英文字符，可以直接加前缀b得到bytes类型
        # l = [
        #     b'1111aaa1\n',
        #     b'222bb2',
        #     b'33eee33'
        # ]
    
        # 补充2：'上'.encode('utf-8') 等同于bytes('上',encoding='utf-8')
        l = [
            bytes('上啊',encoding='utf-8'),
            bytes('冲呀',encoding='utf-8'),
            bytes('小垃圾们',encoding='utf-8'),
        ]
        f.writelines(l)
    
    3、flush：
    with open('h.txt', mode='wt',encoding='utf-8') as f:
        f.write('哈')
        # f.flush()
    
    4、了解
    with open('h.txt', mode='wt', encoding='utf-8') as f:
        print(f.readable())
        print(f.writable())
        print(f.encoding)
        print(f.name)
    
    print(f.closed)
    
    #指针移动的单位都是以bytes/字节为单位
    #只有一种情况特殊：
    #      t模式下的read(n),n代表的是字符个数
    
    with open('aaa.txt',mode='rt',encoding='utf-8') as f:
        res=f.read(4)
        print(res)
    
    f.seek(n,模式):n指的是移动的字节个数
    模式：
    模式0：参照物是文件开头位置
    f.seek(9,0)
    f.seek(3,0) # 3
    
    模式1：参照物是当前指针所在位置
    f.seek(9,1)
    f.seek(3,1) # 12
    
    模式2：参照物是文件末尾位置，应该倒着移动
    f.seek(-9,2) # 3
    f.seek(-3,2) # 9
    
    强调：只有0模式可以在t下使用，1、2必须在b模式下用
    
    f.tell() # 获取文件指针当前位置
    
    示范
    with open('aaa.txt',mode='rb') as f:
        f.seek(9,0)
        f.seek(3,0) # 3
        # print(f.tell())
        f.seek(4,0)
        res=f.read()
        print(res.decode('utf-8'))
    
    with open('aaa.txt',mode='rb') as f:
        f.seek(9,1)
        f.seek(3,1) # 12
        print(f.tell())
    
    with open('aaa.txt',mode='rb') as f:
        f.seek(-9,2)
        # print(f.tell())
        f.seek(-3,2)
        # print(f.tell())
        print(f.read().decode('utf-8'))
    
    #seek应用
    import time
    
    with open('access.log', mode='rb') as f:
        # 1、将指针跳到文件末尾
        # f.read() # 错误
        f.seek(0,2)
    
        while True:
            line=f.readline()
            if len(line) == 0:
                time.sleep(0.3)
            else:
                print(line.decode('utf-8'),end='')
    
    # 文件修改的两种方式
    # 方式一：文本编辑采用的就是这种方式
    # 实现思路：将文件内容发一次性全部读入内存,然后在内存中修改完毕后再覆盖写回原文件
    # 优点: 在文件修改过程中同一份数据只有一份
    # 缺点: 会过多地占用内存
    with open('c.txt',mode='rt',encoding='utf-8') as f:
        res=f.read()
        data=res.replace('alex','dsb')
        print(data)
    
    with open('c.txt',mode='wt',encoding='utf-8') as f1:
        f1.write(data)
    
    # 方式二：
    import os
    # 实现思路：以读的方式打开原文件,以写的方式打开一个临时文件,一行行读取原文件内容,
    #					  修改完后写入临时文件...,删掉原文件,将临时文件重命名原文件名
    # 优点: 不会占用过多的内存
    # 缺点: 在文件修改过程中同一份数据存了两份
    with open('c.txt', mode='rt', encoding='utf-8') as f, \
            open('.c.txt.swap', mode='wt', encoding='utf-8') as f1:
        for line in f:
            f1.write(line.replace('alex', 'dsb'))
    
    os.remove('c.txt')
    os.rename('.c.txt.swap', 'c.txt')
    
    f = open('a.txt')
    res = f.read()
    print(res)
    ```