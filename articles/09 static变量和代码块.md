#	第1章	static静态关键字

## 1.1 静态的概述
当在定义类的时候，类中都会有相应的属性和方法。而属性和方法都是通过创建本类对象调用的。当在调用对象的某个方法时，这个方法没有访问到对象的特有数据时，方法创建这个对象有些多余。可是不创建对象，方法又调用不了，这时就会想，那么我们能不能不创建对象，就可以调用方法呢？  

可以的，我们可以通过static关键字来实现。static它是静态修饰符，一般用来修饰类中的成员。

## 1.2	静态的特点
- 被static修饰的成员变量属于类，不属于这个类的某个对象。  
也就是说，多个对象在访问或修改static修饰的成员变量时，其中一个对象将static成员变量值进行了修改，其他对象中的static成员变量值跟着改变，即多个对象共享同一个static成员变量

- 被static修饰的成员可以并且建议通过类名直接访问  
**访问静态成员的格式:**
  - 类名.静态成员变量名 
  - 类名.静态成员方法名(参数)

- 静态的加载优先于对象,随着类的加载而加载

## 1.3	静态的注意事项
静态成员只能直接访问静态成员  
非静态成员既可以访问非静态成员也可以访问静态成员


static的注意事项：  
- 静态方法：  
  - 可以调用静态的成员变量
  - 可以调用静态的成员方法
  - 不可以调用非静态成员变量
  - 不可以调用非静态成员方法
  - 静态方法只能调用静态的成员
- 非静态方法：
  - 可以调用静态的成员变量
  - 可以调用静态的成员方法
  - 可以调用非静态的成员变量
  - 可以调用非静态的成员方法

静态的方法中是否有this这个对象？
没有的


## 1.4	静态的优缺点
- 静态优点:
  - 对对象的共享数据提供单独空间的存储，节省空间，没有必要每一个对象都存储一份
  - 可以直接被类名调用,不用在堆内存创建对象
  - 静态成员可以通过类名直接访问,相对创建对象访问成员方便
- 静态弊端:  
访问出现局限性。（静态虽好，但只能访问静态）

## 1.5	静态应用
### 1.5.1	Math类使用
- Math 类包含用于执行基本数学运算的方法。数学操作常用的类。
- Math类的构造方法被private,无法创建对象,也就无法通过对象来访问Math类中的成员
- Math类中所有的成员都被静态修饰,因此我们可以直接通过类名访问

### 1.5.2 案例代码
```java
public class MathDemo {
	public static void main(String[] args) {
		//Math:包含了一些基本的数学运算方法
		//static double PI  
		//System.out.println(Math.PI);

		//static double abs(double a)  :返回绝对值
		//System.out.println(Math.abs(15));
		//System.out.println(Math.abs(-10));

		//static double ceil(double a) 天花板   向上取整
		//System.out.println(Math.ceil(1.2));
		//System.out.println(Math.ceil(1.6));
		//static double floor(double a)  地板  向下取整
		//System.out.println(Math.floor(1.2));
		//System.out.println(Math.floor(1.6));

		//static long round(double a)  ：四舍五入
		//System.out.println(Math.round(1.2));
		//System.out.println(Math.round(1.6));

		//static double max(double a, double b)
		//System.out.println(Math.max(3, 4));

		//static double pow(double a, double b) :返回第一个参数的第二个参数次幂
		//System.out.println(Math.pow(3, 2));

		//static double random() :返回一个随机数，大于零且小于一
		System.out.println(Math.random());
	}
}
```

## 1.6 类变量与实例变量辨析
- 类变量:其实就是静态变量
  - 定义位置: 定义在类中方法外
  - 所在内存区域: 方法区
  - 生命周期: 随着类的加载而加载
  - 特点: 无论创建多少对象,类变量仅在方法区中,并且只有一份

- 实例变量:其实就是非静态变量
  - 定义位置: 定义在类中方法外
  - 所在内存区域: 堆
  - 生命周期: 随着对象的创建而加载
  - 特点: 每创建一个对象,堆中的对象中就有一份实例变量

# 第2章	代码块
## 2.1	局部代码块
局部代码块是定义在方法或语句中


```java
//代码示例
public class BlockDemo {
	public static void main(String[] args) {
		//局部代码块：存在于方法中，控制变量的生命周期（作用域）
		 {
			for(int x = 0;x < 10;x++) {
				System.out.println("我爱Java");
			}
			int num = 10;
		}
		//System.out.println(num);//无法访问num,超出num的作用域范围
	}
}
```

## 2.2	构造代码块
构造代码块是定义在类中成员位置的代码块

```java
//代码示例
class Teacher {
	String name;
	int age;
	{
		for(int x = 0;x < 10;x++) {
			System.out.println("我爱Java");
		}
		System.out.println("我爱Java");
	}

	public Teacher() {
		System.out.println("我是无参空构造");
	}

	public Teacher(String name,int age) {
		System.out.println("我是有参构造");

		this.name = name;
		this.age = age;
	}
}
```

## 2.3	静态代码块
静态代码块是定义在成员位置，使用static修饰的代码块

```java
//代码示例
class Teacher {
	String name;
	int age;

	//静态代码块：随着类的加载而加载，只加载一次，加载类时需要做的一些初始化，比如加载驱动
	static {
		System.out.println("我爱Java");
	}

	public Teacher() {
		System.out.println("我是无参空构造");
	}

	public Teacher(String name,int age) {
		System.out.println("我是有参构造");

		this.name = name;
		this.age = age;
	}
}
```

## 2.4	每种代码块特点
### 2.4.1	局部代码块:
- 以”{}”划定的代码区域，此时只需要关注作用域的不同即可
- 方法和类都是以代码块的方式划定边界的

### 2.4.2	构造代码块:
- 优先于构造方法执行，构造代码块用于执行所有对象均需要的初始化动作
- **每创建一个对象均会执行一次构造代码块。**

### 2.4.3	静态代码块
- 它优先于主方法执行、优先于构造代码块执行，当以任意形式第一次使用到该类时执行.
- 该类不管创建多少对象，静态代码块只执行一次。
- 可用于给静态变量赋值，用来给类进行初始化。

### 2.4.4	代码实例
```java
//代码示例
/*
 *   Coder静态代码块执行 --- Coder构造代码块执行 --- Coder无参空构造执行
 *   
 *   
 *   BlockTest静态代码块执行 --- BlockTest的主函数执行了 --- Coder静态代码块执行 --- Coder构造代码块执行 --- Coder无参空构造执行
 *   Coder构造代码块执行 --- Coder无参空构造执行
 *
 */
public class BlockTest {
	static {
		System.out.println("BlockTest静态代码块执行");
	}

	{
		System.out.println("BlockTest构造代码块执行");
	}


	public BlockTest(){
		System.out.println("BlockTest无参构造执行了");
	}

	public static void main(String[] args) {
		System.out.println("BlockTest的主函数执行了");
		Coder c = new Coder();
		Coder c2 = new Coder();
	}
}

class Coder {

	static {
		System.out.println("Coder静态代码块执行");
	}

	{
		System.out.println("Coder构造代码块执行");
	}

	public Coder() {
		System.out.println("Coder无参空构造执行");
	}

}
````
