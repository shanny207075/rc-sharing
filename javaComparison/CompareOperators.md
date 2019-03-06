## Java == 及 equals 的差別

首先我們先了解一下 Java 宣告參數及物件在記憶體的配置。

宣告為基本型態的參數可以直接用 `==` 來判斷是否相等 ; 而參考型態則有不同的判斷方式。 
以下程式的執行結果相信大家都不會有什麼問題
```markdown
public class ComparisonDemo1 {
	public static void main(String[] args) {
		//基本型態的比較
		byte 	b1=1, b2=1;
		short 	s1=2, s2=2;
		int 	i1=3, i2=3;
		long 	l1=4, l2=4;
		float 	f1=5.1f, f2=5.1f;
		double 	d1=6.2, d2=6.20;
		
		System.out.println("b1==b2: " + String.valueOf(b1==b2));
		System.out.println("s1==s2: " + String.valueOf(s1==s2));
		System.out.println("i1==i2: " + String.valueOf(i1==i2));
		System.out.println("l1==l2: " + String.valueOf(l1==l2));
		System.out.println("f1==f2: " + String.valueOf(f1==f2));
		System.out.println("d1==d2: " + String.valueOf(d1==d2));
		
	}

}
```


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
