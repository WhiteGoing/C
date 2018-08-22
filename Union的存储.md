#Union的存储

Union中的元素都存在同一内存中，其大小为最大类型所占内存大小

在32bit系统下，执行下述程序：

```c++
union aa{
    int a;
    double c;
};
int main() {
    union aa x;
    x.c = 111111.111111;
    x.a = 3;
    cout << x.a << endl;
    cout << x.c << endl;
    cout << &x << endl;
    cout << &x.a <<endl;
    cout << &x.c <<endl;
    while(1);
    return 0;
}
```

结果如图：![Union的存储(1)](https://github.com/WhiteGoing/picture/blob/master/Union%E7%9A%84%E5%AD%98%E5%82%A8(1).png)

111111.111111对应的hex是：0x40 fb 20 71 c7 1c 53 f4，由此可见，只存了**double数的前四个字节**，后四个字节用来存其他元素。

**由此猜想：是不是union最多为每个变量分配4字节空间,还是尽可能的多为变量分配空间，但是每增加一个赋值变量，空间平分一次？**

当只给double型变量赋值时

```c++
union aa{
    int a;
    double c;
};
int main() {
    union aa x;
    x.c = 111111.111111;
    cout << x.c << endl;
    cout << &x << endl;
    while(1);
    return 0;
}
```

结果如下图：

![Union的存储(2)](https://github.com/WhiteGoing/picture/blob/master/Union%E7%9A%84%E5%AD%98%E5%82%A8(2).png)

省略实验步骤。。。

最终发现，Union的步骤：

​	首先按照最大的类型给Union实例分配空间，接着按照赋值的顺序依次将空间的值替换成当前值（且按照当前类型的大小进行部分替换，每次替换的都是从前一类型的尾端开始），由于x86是小端模式，所以就出现了上述结果。读数的时候也是按照目前的类型，从低地址开始读相应的字节，并进行类型转换。如:对图二的结果执行```cout << x.a << endl;```其输出值为-954444812（即十六进制0xc71c53f4对于的int型数值）。

大小端模式：

![Union的存储(3)](https://github.com/WhiteGoing/picture/blob/master/Union%E7%9A%84%E5%AD%98%E5%82%A8(1).png)

