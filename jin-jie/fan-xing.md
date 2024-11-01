# 泛型

## 什么是泛型？

泛型，即“参数化类型”。一提到参数，最熟悉的就是定义方法时有形参列表，普通方法的形参列表中，每个形参的数据类型是确定的，而变量是一个参数。在调用普通方法时需要传入对应形参数据类型的变量（实参），若传入的实参与形参定义的数据类型不匹配，则会报错。

### 使用场景：

**在 ArrayList 集合中，可以放入所有类型的对象，假设现在需要一个只存储了 String 类型对象的 ArrayList 集合。**

代码如下：

```java
public void test() {
    ArrayList list = new ArrayList();
    list.add("aaa");
    list.add("bbb");
    list.add("ccc");
    for (int i = 0; i < list.size(); i++) {
        System.out.println((String)list.get(i));
    }
}
```

* 上面代码没有任何问题，在遍历 ArrayList 集合时，只需将 Object 对象进行向下转型成 String 类型即可得到 String 类型对象。

> **但如果在添加 String 对象时，不小心添加了一个 Integer 对象，会发生什么？**

```java
public void test() {
    ArrayList list = new ArrayList();
    list.add("aaa");
    list.add("bbb");
    list.add("ccc");
    list.add(111);
    for (int i = 0; i < list.size(); i++) {
        System.out.println((String)list.get(i));
    }
}
```

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

**那如何可以避免上述异常的出现？即我们希望当我们向集合中添加了不符合类型要求的对象时，编译器能直接给我们报错，而不是在程序运行后才产生异常。这个时候便可以使用`泛型`了。**

### 使用泛型代码：

```java
public void test() {
    ArrayList<String> list = new ArrayList<>();
    list.add("aaa");
    list.add("bbb");
    list.add("ccc");
    list.add(111);// 在编译阶段，编译器会报错
    for (int i = 0; i < list.size(); i++) {
        System.out.println((String)list.get(i));
    }
}
```

* < String > 是一个泛型，其限制了 ArrayList 集合中存放对象的数据类型只能是 String，当添加一个非 String 对象时，编译器会直接报错。这样，我们便解决了上面产生的 ClassCastException 异常的问题（这样体现了泛型的类型安全检测机制）。

### 泛型概述小结&#x20;

与使用 Object 对象代替一切引用数据类型对象这样简单粗暴方式相比，泛型使得数据类型的类别可以像参数一样由外部传递进来。它提供了一种扩展能力，更符合面向对象开发的软件编程宗旨。 当具体的数据类型确定后，泛型又提供了一种类型安全检测机制，只有数据类型相匹配的变量才能正常的赋值，否则编译器就不通过。所以说，泛型一定程度上提高了软件的安全性，防止出现低级的失误。 泛型提高了程序代码的可读性。在定义泛型阶段（类、接口、方法）或者对象实例化阶段，由于 < 类型参数 > 需要在代码中显式地编写，所以程序员能够快速猜测出代码所要操作的数据类型，提高了代码可读性。&#x20;

[_泛型有三种使用方式，分别为：泛型类、泛型接口、泛型方法，下面将正式介绍泛型的相关知识。_ ](#user-content-fn-1)[^1]

## 泛型类

### 基本语法

```java
class 类名称 <泛型标识> {
  private 泛型标识 /*（成员变量类型）*/ 变量名; 
  .....

  }
}
```

* 尖括号 <> 中的 泛型标识被称作是`类型参数`，用于指代任何数据类型。
* 泛型标识是任意设置的（如果你想可以设置为 Hello都行），Java 常见的泛型标识以及其代表含义如下：

```
  T ：代表一般的任何类。
  E ：代表 Element 元素的意思，或者 Exception 异常的意思。
  K ：代表 Key 的意思。
  V ：代表 Value 的意思，通常与 K 一起配合使用。
  S ：代表 Subtype 的意思
```

例如：

```java
public class Generic<T> { 
    // key 这个成员变量的数据类型为 T, T 的类型由外部传入  
    private T key;

	// 泛型构造方法形参 key 的类型也为 T，T 的类型由外部传入
    public Generic(T key) { 
        this.key = key;
    }
    
	// 泛型方法 getKey 的返回值类型为 T，T 的类型由外部指定
    public T getKey(){ 
        return key;
    }
}
```

```
  1.非静态的成员属性类型
  2.非静态方法的形参类型（包括非静态成员方法和构造器）
  3.非静态的成员方法的返回值类型
```

#### _泛型类中的静态方法和静态变量不可以使用泛型类所声明的类型参数_

代码如下：

```java
public class Test<T> {    
    public static T one;   // 编译错误    
    public static T show(T one){ // 编译错误    
        return null;    
    }    
}  
```

泛型类中的类型参数的确定是在创建泛型类对象的时候（例如 ArrayList< Integer >）。

而静态变量和静态方法在类加载时已经初始化，直接使用类名调用；在泛型类的类型参数未确定时，静态成员有可能被调用，因此泛型类的类型参数是不能在静态成员中使用的。&#x20;

#### _**静态泛型方法中可以使用自身的方法签名中新定义的类型参数（即泛型方法，后面会说到），而不能使用泛型类中定义的类型参数。**_

```java
public class Test2<T> {   
	// 泛型类定义的类型参数 T 不能在静态方法中使用  
    public static <E> E show(E one){ // 这是正确的，因为 E 是在静态方法签名中新定义的类型参数    
        return null;    
    }    
}  
```

#### _**泛型类不只接受一个类型参数，它还可以接受多个类型参数。**_

```java
public class MultiType <E,T> {
	E value1;
	T value2;
	
	public E getValue1(){
		return value1;
	}
	
	public T getValue2(){
		return value2;
	}
}
```

### 泛型类的使用

**在创建泛型类的对象时，必须指定类型参数 T 的具体数据类型，即尖括号 <> 中传入的什么数据类型，T 便会被替换成对应的类型。如果 <> 中什么都不传入，则默认是 < Object >。**

例子

```java
// 定义一个泛型类 Box
public class Box<T> {
    private T item;

    // 构造方法
    public Box(T item) {
        this.item = item;
    }

    // 获取 item
    public T getItem() {
        return item;
    }

    // 设置 item
    public void setItem(T item) {
        this.item = item;
    }

    @Override
    public String toString() {
        return "Box{" + "item=" + item + '}';
    }
}
```

**当创建一个 Generic< T > 类对象时，会向尖括号 <> 中传入具体的数据类型。**

```java
 public static void main(String[] args) {
        // 创建一个装 Integer 的 Box
        Box<Integer> integerBox = new Box<>(123);
        System.out.println("Integer Box: " + integerBox.getItem());
    }
```

**传入** Integer **类型时，原泛型类可以想象它会自动扩展，其类型参数会被替换。**

```java
// 定义一个泛型类 Box
public class Box<Integer> {
    private Integer item;

    // 构造方法
    public Box(Integer item) {
        this.item = item;
    }

    // 获取 item
    public Integer getItem() {
        return item;
    }

    // 设置 item
    public void setItem(Integer item) {
        this.item = item;
    }

    @Override
    public String toString() {
        return "Box{" + "item=" + item + '}';
    }
}
```

* 可以发现，泛型类中的`类型参数 T` 被 <> 中的 String 类型全部替换了。
* <mark style="background-color:orange;">使用泛型的上述特性便可以在集合中限制添加对象的数据类型，若集合中添加的对象与指定的泛型数据类型不一致，则编译器会直接报错，这也是泛型的类型安全检测机制的实现原理。</mark>

## 泛型接口

定义语法：

```java
public interface 接口名<类型参数> {
    ...
}
```

例子：

```java
public interface Inter<T> {
    public abstract void show(T t) ;
}
```

**（1）定义一个泛型接口如下：**

* 注意：在泛型接口中，静态成员也不能使用泛型接口定义的类型参数。

```java
interface IUsb<U, R> {

    int n = 10;
    U name;// 报错！ 接口中的属性默认是静态的，因此不能使用类型参数声明

    R get(U u);// 普通方法中，可以使用类型参数

    void hi(R r);// 抽象方法中，可以使用类型参数

    // 在jdk8 中，可以在接口中使用默认方法, 默认方法可以使用泛型接口的类型参数
    default R method(U u) {
        return null;
    }
}
```

**（2）定义一个接口 IA 继承了 泛型接口 IUsb，在 接口 IA 定义时必须确定泛型接口 IUsb 中的类型参数。**

```java
// 在继承泛型接口时，必须确定泛型接口的类型参数
interface IA extends IUsb<String, Double> {
	...
}

// 当去实现 IA 接口时，因为 IA 在继承 IUsu 接口时，指定了类型参数 U 为 String，R 为 Double
// 所以在实现 IUsb 接口的方法时，使用 String 替换 U,用 Double 替换 R
class AA implements IA {
    @Override
    public Double get(String s) {
        return null;
    }
    @Override
    public void hi(Double d) {
		...
    }
}

```

**（3）定义一个类 BB 实现了 泛型接口 IUsb，在 类 BB 定义时需要确定泛型接口 IUsb 中的类型参数。**

```java
// 实现接口时，需要指定泛型接口的类型参数
// 给 U 指定 Integer， 给 R 指定了 Float
// 所以，当我们实现 IUsb 方法时，会使用 Integer 替换 U, 使用 Float 替换 R
class BB implements IUsb<Integer, Float> {
    @Override
    public Float get(Integer integer) {
        return null;
    }
    @Override
    public void hi(Float afloat) {
		...
    }
}
```

**（4）定义一个类 CC 实现了 泛型接口 IUsb 时，若是没有确定泛型接口 IUsb 中的类型参数，则默认为 Object。**

```java
// 实现泛型接口时没有确定类型参数，则默认为 Object
// 建议直接写成 IUsb<Object, Object>
class CC implements IUsb {//等价 class CC implements IUsb<Object, Object> 
    @Override
    public Object get(Object o) {
        return null;
    }
    @Override
    public void hi(Object o) {
    	...
    }
}
```

**（5）定义一个类 DD 实现了 泛型接口 IUsb 时，若是没有确定泛型接口 IUsb 中的类型参数，也可以将 DD 类也定义为泛型类，其声明的类型参数必须要和接口 IUsb 中的类型参数相同。**

```java
// DD 类定义为 泛型类，则不需要确定 接口的类型参数
// 但 DD 类定义的类型参数要和接口中类型参数的一致
class DD<U, R> implements IUsb<U, R> { 
	...
}
```

## 泛型方法

### 1. 泛型方法的定义

**当在一个方法签名中的返回值前面声明了一个 < T > 时，该方法就被声明为一个`泛型方法`。< T >表明该方法声明了一个类型参数 T，并且这个类型参数 T 只能在该方法中使用。当然，泛型方法中也可以使用`泛型类中定义的泛型参数`。**

基本语法如下：

```java
public <类型参数> 返回类型 方法名（类型参数 变量名） {
    ...
}
```

**（1）只有在方法签名中声明了< T >的方法才是泛型方法，仅使用了泛型类定义的类型参数的方法并不是泛型方法。**

```java
public class Test<U> {
	// 该方法只是使用了泛型类定义的类型参数，不是泛型方法
	public void testMethod(U u){
		System.out.println(u);
	}
	
	// <T> 真正声明了下面的方法是一个泛型方法
	public <T> T testMethod1(T t){
		return t;
	}
}
```

**（2）泛型方法中可以同时声明多个类型参数。**

```java
public class TestMethod<U> {
	public <T, S> T testMethod(T t, S s) {
		return null;
	}
}
```

**（3）泛型方法中也可以使用泛型类中定义的泛型参数。**

```java
public class TestMethod<U> {
	public <T> U testMethod(T t, U u) {
		return u;
	}
}
```

**（4）特别注意的是：泛型类中`定义的类型参数`和`泛型方法中定义`的类型参数是相互独立的，它们一点关系都没有。**

```java
public class Test<T> {
	public void testMethod(T t) {
		System.out.println(t);
	}
	
	public <T> T testMethod1(T t) {
		return t;
	}
}
```

> 上面代码中，Test< T > 是泛型类，testMethod() 是泛型类中的普通方法，其使用的类型参数是与泛型类中定义的类型参数。 而 testMethod1() 是一个泛型方法，他使用的类型参数是与方法签名中声明的类型参数。 虽然泛型类中定义的类型参数标识和泛型方法中定义的类型参数标识都为< T >，但它们彼此之间是相互独立的。也就是说，泛型方法始终以自己声明的类型参数为准。

#### 注意事项：

1. < T >表明该方法声明了一个类型参数 T，并且这个类型参数 T 只能在该方法中使用。
2. 为了避免混淆，如果在一个泛型类中存在泛型方法，那么两者的类型参数最好不要同名。
3. 与泛型类的类型参数定义一样，此处泛型方法中的 T 可以写为`任意标识`，常见的如 T、E、K、V 等形式的参数常用于表示泛型。

**补充一点：将静态方法声明为泛型方法**

> **前面在泛型类的定义中提到，在静态成员中不能使用泛型类定义的类型参数，但我们可以将静态成员方法定义为一个泛型方法。**

```java
public class Test2<T> {   
	// 泛型类定义的类型参数 T 不能在静态方法中使用
	// 但可以将静态方法声明为泛型方法，方法中便可以使用其声明的类型参数了
    public static <E> E show(E one) {     
        return null;    
    }    
}  
```

### 2、泛型方法的使用&#x20;

泛型类，在创建类的对象的时候确定类型参数的具体类型；

&#x20;泛型方法，在调用方法的时候再确定类型参数的具体类型。

泛型方法签名中声明的类型参数只能在该方法里使用，而泛型接口、泛型类中声明的类型参数则可以在整个接口、类中使用。 当调用泛型方法时，根据外部传入的实际对象的数据类型，编译器就可以判断出类型参数 `T` 所代表的具体数据类型。

```java
public class Demo {  
  public static void main(String args[]) {  
    GenericMethod d = new GenericMethod(); // 创建 GenericMethod 对象  
    
    String str = d.fun("汤姆"); // 给GenericMethod中的泛型方法传递字符串  
    int i = d.fun(30);  // 给GenericMethod中的泛型方法传递数字，自动装箱  
    System.out.println(str); // 输出 汤姆
    System.out.println(i);  // 输出 30

	GenericMethod.show("Lin");// 输出: 静态泛型方法 Lin
  }  
}

class GenericMethod {
	// 普通的泛型方法
	public <T> T fun(T t) { // 可以接收任意类型的数据  
    	return t;
  	} 

	// 静态的泛型方法
	public static <E> void show(E one){     
         System.out.println("静态泛型方法 " + one);
    }
}  
```

> 不难发现，当调用泛型方法时，根据传入的实际对象，`编译器`会判断出类型形参 T 所代表的具体数据类型。

### 3、泛型方法中的类型推断&#x20;

**在调用泛型方法的时候，可以显式地指定类型参数，也可以不指定。**

当泛型方法的形参列表中有多个类型参数时，在不指定类型参数的情况下，方法中声明的的类型参数为泛型方法中的几种类型参数的共同父类的最小级，直到 Object。 在指定了类型参数的时候，传入泛型方法中的实参的数据类型必须为指定数据类型或者其子类。

```java
public class Test {

	// 这是一个简单的泛型方法  
    public static <T> T add(T x, T y) {  
        return y;  
    }

    public static void main(String[] args) {  
        // 一、不显式地指定类型参数
        //（1）传入的两个实参都是 Integer，所以泛型方法中的<T> == <Integer> 
        int i = Test.add(1, 2);
        
        //（2）传入的两个实参一个是 Integer，另一个是 Float，
        // 所以<T>取共同父类的最小级，<T> == <Number>
		Number f = Test.add(1, 1.2);

		// 传入的两个实参一个是 Integer，另一个是 String，
		// 所以<T>取共同父类的最小级，<T> == <Object>
        Object o = Test.add(1, "asd");
  
        // 二、显式地指定类型参数
        //（1）指定了<T> = <Integer>，所以传入的实参只能为 Integer 对象    
        int a = Test.<Integer>add(1, 2);
		
		//（2）指定了<T> = <Integer>，所以不能传入 Float 对象
        int b = Test.<Integer>add(1, 2.2);// 编译错误
        
        //（3）指定<T> = <Number>，所以可以传入 Number 对象
        // Integer 和 Float 都是 Number 的子类，因此可以传入两者的对象
        Number c = Test.<Number>add(1, 2.2); 
    }  
}
```

## 五、类型擦除

1. 什么是类型擦除&#x20;

泛型的本质是将数据类型参数化，它通过擦除的方式来实现，即编译器会在编译期间擦除代码中的所有泛型语法并相应的做出一些类型转换动作。

> 换而言之，泛型信息只存在于代码编译阶段，在代码编译结束后，与泛型相关的信息会被擦除掉，专业术语叫做类型擦除。也就是说，成功编译过后的 class 文件中不包含任何泛型信息，泛型信息不会进入到运行时阶段。

看一个例子，假如我们给 ArrayList 集合传入两种不同的数据类型，并比较它们的类信息。

```java
public class GenericType {
    public static void main(String[] args) {  
        ArrayList<String> arrayString = new ArrayList<String>();   
        ArrayList<Integer> arrayInteger = new ArrayList<Integer>();   
        System.out.println(arrayString.getClass() == arrayInteger.getClass());// true
    }  
}
```

在这个例子中，我们定义了两个 ArrayList 集合，不过一个是 ArrayList< String>，只能存储字符串。一个是 ArrayList< Integer>，只能存储整型对象。我们通过 arrayString 对象和 arrayInteger 对象的 getClass() 方法获取它们的类信息并比较，发现结果为true。

明明我们在 <> 中传入了两种不同的数据类型，按照上文所说的，它们的类型参数 T 不是应该被替换成我们传入的数据类型了吗，那为什么它们的类信息还是相同呢？ 这是因为，在编译期间，所有的泛型信息都会被擦除， ArrayList< Integer > 和 ArrayList< String >类型，在编译后都会变成ArrayList< Objec t>类型。

[^1]: 
