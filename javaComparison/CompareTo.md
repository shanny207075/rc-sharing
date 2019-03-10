## Java CompareTo, Comparator

Java 物件的 `CompareTo` 方法可以用來比大小(現實生活中我們也常在比大小，例如...年紀或輩份...題外話)，至於如何決定誰大誰小(例如：'A' 跟 'B' 誰大)，就需要更明確的定義。

**先來看一個簡單好理解的例子** [live demo](http://tpcg.io/NiNOpd)
```java
public class SimpleCompareTo {
	public static void main(String[] args) {
        Integer I99 = new Integer(99);
        Integer I50 = new Integer(50);        
        int compareInteger = I99.compareTo(I50);
        
        if(compareInteger < 0) {
        		System.out.println("I99 小於 I50");
        }else if(compareInteger ==0) {
        		System.out.println("I99 等於 I50");
        }else {
        		System.out.println("I99 大於 I50");
        }        
    }
}
```

> 結果會印出 I99 大於 I50，也就是 compareInteger 會回傳大於零的整數

能夠比較出大小之後，就可以進一步**作一個排序的動作**，先來看一下以下的例子： 
```java
public class Sort1 {
	public static void main(String[] args) {
		List<Integer> numbers = Arrays.asList(10, 2, 3, 1, 9, 15, 4);
        Collections.sort(numbers);
        System.out.println(numbers);
	}
}
```

很順利地就排出由小到大的順序了
> [1, 2, 3, 4, 9, 10, 15]

那如果有一天我想要列出員工資料並將它排序，應該就可以比照辦理了對吧 [live demo](http://tpcg.io/KVlAjP)
**員工資料結構**
```java
class Employee {
    private String name;	//姓名
    private String number;	//員工編號
    private int salary;		//薪資

    Employee(String name, String number, int salary) {
        this.name = name;
        this.number = number;
        this.salary = salary;
    }

    @Override
    public String toString() {
        return String.format("Account(%s, %s, %d)", name, number, salary);
    } 
}
```

**Main class Sort2**
```java
public class Sort2 {
	public static void main(String[] args) {		
        List employees = Arrays.asList(
                new Employee("Justin", "X1234", 34000),
                new Employee("Monica", "X5678", 50000),
                new Employee("Irene", "X2468", 42000)
        );
        Collections.sort(employees);
        System.out.println(employees);
	}
}
```

執行結果
```java
Exception in thread "main" java.lang.ClassCastException: Employee cannot be cast to java.lang.Comparable
	at java.util.ComparableTimSort.countRunAndMakeAscending(ComparableTimSort.java:320)
	at java.util.ComparableTimSort.sort(ComparableTimSort.java:188)
	at java.util.Arrays.sort(Arrays.java:1246)
	at java.util.Arrays.sort(Arrays.java:1433)
	at java.util.Arrays$ArrayList.sort(Arrays.java:3895)
	at java.util.Collections.sort(Collections.java:141)
	at Sort1.main(Sort1.java:18)
```

發生錯誤了。原因是你沒有明確告訴系統要依什麼規則作排序，於是我們必須先實作 `Comparable` 介面，這個介面需要實作 `compareTo()` 方法。[live demo](http://tpcg.io/4r7PLb)

**稍稍改寫一下 `Employee` 類別** 
```java
class Employee implements Comparable<Employee>{
    ...

    @Override
    public int compareTo(Employee other) {
        return this.salary - other.salary;
    }
}
```

再執行一次，就可以看到排序後的結果了
> [ Employee2(Irene, X2468, 200) , Employee2(Monica, X5678, 500) , Employee2(Justin, X1234, 1000) ]

> _Note:_ 若 `compareTo` 傳回負數，表示傳入的物件要排在自己的後方 ; 反之排在自己的前方。所以如果要降冪排列，只要在前面加個負號即可：`return -(this.salary - other.salary);`

那現在我們來試試字串的排列：
```java
public class Sort1 {
	public static void main(String[] args) {
		List<String> chars = Arrays.asList("B", "X", "A", "M", "F", "W", "O");
        Collections.sort(chars);
        System.out.println(chars);
	}
}
```

It's Easy, right ?
> [A, B, F, M, O, W, X]

可是如果我想改成降冪排序的話，該怎麼做呢? 改寫 `String` 的 `compareTo` 再存回 jar 檔? 這樣的話你的 `String` 就跟別人不一樣了耶，只要換個環境就不起作用了。而且如果有別的地方要用到升冪排序，你就會陷入兩難了。

幸好這些問題都有人幫我們解決了，方法是使用 `Comparator` 介面。我們要先自訂一個 String 的 Comparator： [live demo](http://tpcg.io/kZcoRq)
```java
class StringComparator implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
        return -s1.compareTo(s2);
    }
}
```

有了它，只要將 **Sort1** 稍作修改：
```java
public class Sort1 {
	public static void main(String[] args) {
		...
        Collections.sort(chars, , new StringComparator());
        ...
	}
}
```

大功告成
> [X, W, O, M, F, B, A]

> _Note:_ live demo 連結中有提供匿名寫法，可以不用另外宣告一個class，有興趣可以看看
