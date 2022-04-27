### Java程序中的输入与输出

#### 文本界面：使用Scanner类

* 使用java.util.Scanner类
  * 用其nextInt()方法
  * 还有nextDouble()
  * next()得到下一个单词
* ScannerTest.java

```java
import java.util.Scanner;
class ScannerTest{
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入一个数");
        int a = scanner.nextInt();
        System.out.printf("%d的平方是%d\n",a,a*a);
    }
}
```

#### 文本界面：使用in及out

* java.io 包
* System.in.read()
* System.out.print()及 println、printf（类似于C语言）
* AppcharInOut.java

```java
char c = ' ';
System.out.print("Please input a char: ");
try{
    c = (char)System.in.read();
}catch(IOException e){}  
System.out.println("You have entered: " + c );
```

* AppLineInOut.java（封装成输入流）
  * 输入输出行
  * 更复杂一些

```java
try{
    BufferedReader in = new BufferedReader(
    	new InputStreamReader( System.in ));
    s = in.readLine();
}catch (IOException e){}
```

* AppNumInOut.java
  * 输入输出数字
  * 用Integer.parseInt(s);
  * 用Double.parseDouble(s)

```java
BufferedReader in = new BufferedReader(
	new InputStreamReader( System.in ));
System.out.print("Please input an int: ");
s = in.readLine();
n = Integer.parseInt(s);
```

