![è¿éåå¾çæè¿°](https://img-blog.csdn.net/20170328111450634?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjQwMzI5MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

①解释：我根据这张图来解释java内存模型，从图中可以看出每个线程都需要从主内存中读取操作，这个就是java内存模型的规定之一，所有的变量存储在主内存中，每个线程都需要**从主内存中**获得变量的值。

然后从图中可以看到每个线程获得数据之后会放入**自己的工作内存**，这个就是java内存模型的规定之二，保证每个线程操作的都是从主内存拷贝的**副本**，也就是说线程不能直接写主内存的变量，需要把主内存的变量值读取之后放入自己的工作内存中的变量副本中，然后操作这个副本。

最后线程与线程之间**无法直接访问对方工作内存**中的变量。最后需要解释一下这个访问规则局限于对象实例字段，静态字段等，局部变量不包括在内，因为局部变量不存在竞争问题。

②基本执行步骤： 
a、lock（锁定）：在某一个线程在读取主内存的时候需要把变量锁定。 
b、unlock（解锁）：某一个线程读取玩变量值之后会释放锁定，别的线程就可以进入操作 
c、read（读取）：从主内存中读取变量的值并放入工作内存中 
d、load（加载）：从read操作得到的值放入工作内存变量副本中 
e、use（使用）：把工作内存中的一个变量值传递给执行引擎 
f、assign（赋值）：它把一个从执行引擎接收到的值赋值给工作内存的变量 
g、store（存储）：把工作内存中的一个变量的值传送到主内存中 
h、write（写入）：把store操作从工作内存中一个变量的值传送到主内存的变量中。

这里我再引入一张别的地方被我搜来的图供大家一起理解：

![è¿éåå¾çæè¿°](https://img-blog.csdn.net/20170328142908765?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjQwMzI5MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

