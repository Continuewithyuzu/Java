# 大数类

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

```java
import java.math.BigInteger;

public class BigIntegerExample {
    public static void main(String[] args) {
        // 创建 BigInteger 对象
        BigInteger num1 = new BigInteger("1234567890123456789012345678901234567890");
        BigInteger num2 = new BigInteger("9876543210987654321098765432109876543210");

        // 加法
        BigInteger sum = num1.add(num2);
        System.out.println("加法结果: " + sum);

        // 减法
        BigInteger difference = num1.subtract(num2);
        System.out.println("减法结果: " + difference);

        // 乘法
        BigInteger product = num1.multiply(num2);
        System.out.println("乘法结果: " + product);

        // 除法
        BigInteger quotient = num1.divide(num2);  // 注意：这里会丢弃小数部分
        System.out.println("除法结果: " + quotient);

        // 取余
        BigInteger remainder = num1.mod(num2);
        System.out.println("取余结果: " + remainder);

        // 最大值
        BigInteger max = num1.max(num2);
        System.out.println("最大值: " + max);

        // 最小值
        BigInteger min = num1.min(num2);
        System.out.println("最小值: " + min);

        // 幂运算
        BigInteger power = num1.pow(2);  // num1 的 2 次方
        System.out.println("幂运算结果: " + power);

        // 比较
        int comparison = num1.compareTo(num2);
        if (comparison < 0) {
            System.out.println("num1 小于 num2");
        } else if (comparison == 0) {
            System.out.println("num1 等于 num2");
        } else {
            System.out.println("num1 大于 num2");
        }

        // 判断是否为零
        boolean isZero = num1.equals(BigInteger.ZERO);
        System.out.println("num1 是否为零: " + isZero);

        // 绝对值
        BigInteger negativeNum = num1.negate();  // num1 的相反数
        System.out.println("num1 的相反数: " + negativeNum);
        BigInteger absValue = negativeNum.abs();  // 取绝对值
        System.out.println("num1 的绝对值: " + absValue);

        // 转换为字符串
        String str = num1.toString();
        System.out.println("num1 转换为字符串: " + str);

        // 转换为 long
        long longValue = num1.longValue();  // 如果超出 long 范围会丢失精度
        System.out.println("num1 转换为 long: " + longValue);

        // 使用 BigDecimal 来计算平方根（演示平方根计算，BigInteger 本身不支持）
        // 需要导入 java.math.BigDecimal 类
        BigDecimal bigDecimal = new BigDecimal(num1);
        BigDecimal sqrtValue = bigDecimal.sqrt(new java.math.MathContext(100));  // 精度100位
        System.out.println("num1 的平方根: " + sqrtValue);
    }
}

```
