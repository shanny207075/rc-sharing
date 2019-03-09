## Java == 及 equals 的差別

首先我們先了解一下 Java 宣告參數及物件在記憶體的配置。
![MemoryExplain](../images/memory_model_explain.jpg)

![MemoryExplain](../images/memory_model_runing.jpg)

宣告為基本型態的參數可以直接用 `==` 來判斷是否相等 ; 而參考型態則有不同的判斷方式。 

基本型態的比較 [live demo](http://tpcg.io/3l2d6v)：
```java
public class ComparisonDemo1 {
	public static void main(String[] args) {
		//基本型態的比較
		byte 	b1 = 1,      b2 = 1;
		short 	s1 = 2,      s2 = 2;
		int 	i1 = 3,      i2 = 3;
		long 	l1 = 4,      l2 = 4;
		float 	f1 = 5.1f,   f2 = 5.1f;
		double 	d1 = 6.2,    d2 = 6.20;
	}
}
```

比較結果
>true, true, true, true, true, true

參考型態的比較 [live demo](http://tpcg.io/w50qrI)：
```java
public class ComparisonDemo2 {
	public static void main(String[] args) {
		//參考型態的比較
		Byte B1 = new Byte((byte)100),            B2 = new Byte((byte)100);
		Short S1 = new Short((short)300),         S2 = new Short((short)300);
		Integer I1 = new Integer(100),            I2 = new Integer(100);
		Long L1 = new Long(1000),                 L2 = new Long(1000);
		Float F1 = new Float(100.12),             F2 = new Float(100.120);
		Double D1 = new Double(100.0123),         D2 = new Double(100.012300);
		BigDecimal BD1 = new BigDecimal(123.010), BD2 = new BigDecimal(123.0100);
	}

}
```

比較結果
```
Byte               B1==B2: false
Short              S1==S2: false
Integer            I1==I2: false
Long               L1==L2: false
Float              F1==F2: false
Double             D1==D2: false
BigDecimal       BD1==BD2: false

Byte         B1.equals(B2): true
Short        S1.equals(S2): true
Integer      I1.equals(I2): true
Long         L1.equals(L2): true
Float        F1.equals(F2): true
Double       D1.equals(D2): true
BigDecimal BD1.equals(BD2): true
```

特殊情況 [live demo](http://tpcg.io/OsaZ6W)：
```java
public class ComparisonDemo3 {
	public static void main(String[] args) {		
		
		Integer I1=3,   I2=3;
		Integer I3=300, I4=300;
		System.out.println("I1==I2: " + String.valueOf(I1==I2));
		System.out.println("I3==I4: " + String.valueOf(I3==I4) + "\n");
		
		String newString1 = new String("Oracle");
		String newString2 = new String("Oracle");
		System.out.println("newString1==newString2       : " + String.valueOf(newString1==newString2)) ;
		System.out.println("newString1.equals(newString2): " + String.valueOf(newString1.equals(newString2)) + "\n");
		
		String javaStr3="Java";
		String javaStr4="Java";
		System.out.println("javaStr3==javaStr4: " + String.valueOf(javaStr3==javaStr4));
	}
}
```

比較結果讓大家猜一猜


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ivan11182002/rc-sharing/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
