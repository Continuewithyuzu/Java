# Page 1

int->char

```java
char c = (char)(count + '0')
```

int->string

```java
int i =6;
1.String s = Interage.toString(i);
2.String S = String.valueOf(i);//适用于int、double、boolean和Object类型
3.String str = i + "";//使用+""，java内自动将数字转化成字符串
```

String->int

```java
1.int i=Integer.parsenInt(s);
2.int i=Integer.valueOf(s).intValue();
```

取字符串单个字符

```java
String S = scan.next();
 for(int i = 1; i < N; i++) {            
   if(s.isEmpty()){                 
      s.push(S.charAt(i));
      continue;
   }
}
```
