内存中是连续的
连续的存储空间分配
```Java
// 声明方法
int[] a = new int[4]{};//*
int[] b = new int[]{1,2,3,4};
int[] c = {1,2,3,4}
int d[];
a.getClass().getName();// 是[I,表示一维数组，类型为Integer
a.getClass().getSuperclass().getName();// 是Java.lang.Object

int[][] a = new int[4][3]

String[] strs = new String[]{a,b,c}
strs.getClass().getName(); // 是[Ljava.lang.String L表示是引用类型

a.length// a的长度
for (int i=0;i<a.length;i++){System.out.println(a[i])}
for (int i:a){System.out.println(i)}// 等效(foreach),这里的每一个i就是a中的元素
for (int[] row:a){
	for(int[] col:row){
		// Your code here
	}
}
// 自动构造器
对于基本类型的数组，存放的是数据，默认是各种0（int 0，false，u0000）
对于引用类型的数组，数组里存放的是引用，默认是null
String[] a=new String[4]{}
for (String i:a){System.out.println(i)}// 输出4个null

// 高维数组的存储
Java中的二维数组在内存中的存储方式和C不一样,Java中二维数组存储的是数组的引用，甚至子数组的长度可以不一样
对于每一行大小不一样的数组，我们称之为**jaggedArray**对于类似于C每一行大小一样的，称之为**regularArray**
int[][] a=new int[4][];//必须从左往右指定，不能从右往左指定

// 可变参数的方法
int myFunc(int …a){
	// a在函数内部相当于一个数组
}
```

*通过拷贝的方式，实现动态数组*

# java.util.Arrays
提供以下工具：
- 查找
- 排序
- 比较
- ……
```Java
int[] a = new int[]{4,1,2,3};
Arrays.sort(a);

#如何让Person类的数组可被排序？
#:在类定义时补全Comparable接口并且重写compareTo(compareTo来自Java.lang.compareTo)
class Person implements Comparable<Person>{
	private String name;
	private int age;
	public void Person(String name,int age){
		this.name=name;
		this.age=age;
	}
	
	@override
	public int compareTo(Person o){
		return this.age-o.age;
	}
}
Person[] = new Person[]{new Person(“Tom”,11),new Person(“Jerry”,12)} 
Arrays.sort(a);

##然而，这种情况只能对一个类写一种排序方法，但是实际上一个类可能需要多种排序方法
Arrays.sort(a, new Comparator<Person>){//在每次排序时定义一个Comparator,来自java.util.Caomparator
	@Override
	public int compare(Person o1,Person o2){
		return o1.getAge()-o2.getAge();
		// <=0,o1在前，
		// >0, o2在前。
	} 
}

# compareTo是自然排序，但是可以使用Comparator进行无线多种排序方法
# 此外，如果Comparator<父类>，那么子类也可以进行比较
```