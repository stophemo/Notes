### String与integer

parseInt



装箱：Integer,valueOf()       (int => integer)

拆箱：i (integer类型).intValue()     (integer => int)

### Data与SimpleDateFormat

Data()   

Data(long date)    :自标准基准时间（1970/01/01/00:00:00）+ long data 的指定毫秒数

### 字符串方法

equal()

chatAt()

subString()

replace()

split()

![image-20220710135155659](D:\Java\notes\Java.assets\image-20220710135155659.png)

![image-20220710135404101](D:\Java\notes\Java.assets\image-20220710135404101.png)



### 集合

#### ArrayList

![image-20220710135909697](D:\Java\notes\Java.assets\image-20220710135909697.png)

 ![image-20220710135949232](D:\Java\notes\Java.assets\image-20220710135949232.png)

常用成员方法

![image-20220710140602250](D:\Java\notes\Java.assets\image-20220710140602250.png)



#### Set

![image-20220710153631719](D:\Java\notes\Java.assets\image-20220710153631719.png)



**set遍历**

![image-20220710153832475](D:\Java\notes\Java.assets\image-20220710153832475.png)



#### TreeSet

![image-20220710154233947](D:\Java\notes\Java.assets\image-20220710154233947.png)

#### 二叉树

#### 红黑树



#### Map集合

![image-20220710154626037](D:\Java\notes\Java.assets\image-20220710154626037.png)









### static

![image-20220710142906204](D:\Java\notes\Java.assets\image-20220710142906204.png)

注意事项

/*/![image-20220710143634243](D:\Java\notes\Java.assets\image-20220710143634243.png)

### 继承

抽象类





### Stream流

![image-20220710155111425](D:\Java\notes\Java.assets\image-20220710155111425.png)



### IO

> 一切文件数据(文本、图片、视频等)在存储时，都是以二进制的形式保存，传输时同样如此。所以字节流可以传输任意数据。 在操作流的时候，无论使用什么样的流对象，底层传输的始终为二进制数据。

> 根据数据的流向分为：**输入流** 和 **输出流**

- 输入流 ：硬盘 --> 内存
- 输出流 ：内存 --> 硬盘

> 根据数据的类型分为：**字节流** 和 **字符流**。 另外还有：**缓冲流**、**转换流**、**序列流**、**打印流**。

#### 字节流

#### 字符流

#### 缓冲流&转换流

#### 对象操作流



