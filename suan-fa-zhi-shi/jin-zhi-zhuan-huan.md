# 进制转换

```java
public class BaseConversion {
    public static void main(String[] args) {
        int number = 42;
        
        // 十进制转二进制
        String binary = Integer.toBinaryString(number);
        System.out.println("Binary: " + binary);
        
        // 十进制转八进制
        String octal = Integer.toOctalString(number);
        System.out.println("Octal: " + octal);
        
        // 十进制转十六进制
        String hex = Integer.toHexString(number);
        System.out.println("Hex: " + hex);
        
         // 二进制转十进制
        int binary = Integer.parseInt("101010", 2);
        System.out.println("Decimal from binary: " + binary);
        
        // 八进制转十进制
        int octal = Integer.parseInt("52", 8);
        System.out.println("Decimal from octal: " + octal);
        
        // 十六进制转十进制
        int hex = Integer.parseInt("2a", 16);
        System.out.println("Decimal from hex: " + hex);
    }
}
```
