
###hashMap的JDK8实现：
   1、首先对hashMap中的定义的变量进行解释 
      ````  
     static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // 16 默认初始化大小为16 
      ````
   备注：有时候别人会问你为什么初始化参数为什么是16而不是其他值？
   
   在低版本JDK中计算hashMap中table下标的方法代码如下：
   ````
    static int indexFor(int h,int length){//低版本的源码
      return h & (length - 1);//第三步，取模运算
    }
   ````
  其中 h 参数为key的hash值 ， length为hashMap的容量大小即： DEFAULT_INITIAL_CAPACITY参数
  length - 1 为 15 。我们知道二进制的15表示为：1111 所以h进行&操作可保证计算的值分布足够均匀。
  
  JDK8中hash值计算与之前版本稍有差异:
  ````
  先通过该方法进行hash值的操作
  static final int hash(Object key) {
          int h;
          return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
      }
      
   然后 再计算table下标 
   n = table.length;
   index  = (n - 1) & hash
   ````   
   通过hashCode()的高16位异或低16位实现,具体这样实现的好处是啥呢：
  
