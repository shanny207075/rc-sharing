## Java Enum 列舉

若你有維護別人的程式經驗，相信多少會看過類似這樣的程式：
```java
public class YouCantUnderstandMe {
	if(status == 1)
		doAcct();
	}else if(status == 2){
		doSubmit();
	}else if(status == 3){
		doGenPaymentReport();
	}
}
```
這種語意不明又不寫註解的程式，真的是難看出 status 等於 1 時是待立帳、2 是待確認、3 是待產生付款報表，如果你看出來了，你一定跟我一樣聰明。

為了不要接收太多接你程式的人的詛咒，宣告固定值的變數來代表這些代碼吧 ! 以下我模擬一下 ATM 操作的狀況：[[EnumDemo1](http://tpcg.io/H4l6uL)]

**設定好狀態代碼對應：AtmStatusInterface**
```java
interface AtmStatusInterface {
	public static final int WITHDRAW = 100;	//提款
	public static final int DEPOSIT = 101;	//存款
	public static final int TRANSFER = 102;	//轉帳
	public static final int CANCEL = 103;	//取消
}
```

**操作 ATM**
```java
public class EnumDemo1 {	
	public static String doAtmOperation(int problemCode) {
		switch(problemCode) {
		case AtmStatusInterface.WITHDRAW:
			return AtmTransaction.doWithdraw();
		case AtmStatusInterface.DEPOSIT:
			return AtmTransaction.doDeposit();
		case AtmStatusInterface.TRANSFER:
			return AtmTransaction.doTransfer();
		case AtmStatusInterface.CANCEL:
			return AtmTransaction.doCancel();
		default :
			return "無效的交易";
		}
	}

	public static void main(String[] args) {
		String atmStatus = doAtmOperation(AtmStatusInterface.WITHDRAW);
		System.out.println(atmStatus);
	}
}
```

有了變數名稱對應代碼，語意就清楚了一些，加上註解的加持，簡直就再清楚不過了，BUT... 這樣無法阻止接你程式的人亂搞(我是指程式方面)。

如果他硬要寫一個 `doAtmOperation( 999 )`，真的是拿他沒辦法耶 ~ 只好再寫一個檢核，但這樣又要多費一番功夫。

J2SE 5.0 加入了 Enum 類別，就可以幫我們解決這個問題，來看以下的程式：[[EnumDemo21](http://tpcg.io/z0Npqr)]

**先定義一個 enum 列舉型態**
```java
enum AtmStatusEnum1 {
	WITHDRAW, DEPOSIT, TRANSFER, CANCEL
}
```

**Main class**
```java
public class EnumDemo21 {	
	public static String getAtmResultMsg(AtmStatusEnum1 atmStatus) {
		switch(atmStatus) {
		case WITHDRAW:
			return AtmTransaction.doWithdraw();
		case DEPOSIT:
			return AtmTransaction.doDeposit();
		case TRANSFER:
			return AtmTransaction.doTransfer();
		case CANCEL:
			return AtmTransaction.doCancel();
		default :
			return "無效的交易";
		}
	}
	
	public static void main(String[] args) {
		//無法輸入設定以外的值
		String atmStatus = EnumDemo21.getAtmResultMsg(AtmStatusEnum1.DEPOSIT);
		System.out.println(atmStatus);
	}	
}
```

列舉型態提供了 `ordinal()` 取出各項目的排序數字，以及 `name()` 取得項目名稱，參考範例：[[EnumDemo22](http://tpcg.io/Fydgp0)]

另外，列舉型態在宣告時也可以輸入參數，須撰寫其**不公開的建構子(private constructor)**，參考以下程式範例：[[EnumDemo23](http://tpcg.io/nqxGaT)]
```java
enum AtmStatusEnum3 {
	WITHDRAW("提款成功"), DEPOSIT("存款成功"), TRANSFER("轉帳成功"), CANCEL("取消成功");
	
	private String description;
	
	// 不公開的建構子
	private AtmStatusEnum3(String description) {
		this.description = description;
	}
	
	public String getDescription() {
		return description;
	}	
}
```

**Main class**
```java
public class EnumDemo23 {
	public static void main(String[] args) {
		for (AtmStatusEnum3 atmOperation : AtmStatusEnum3.values()) {
			System.out.println(atmOperation.name() + "：" + atmOperation.getDescription());
		}		
	}
}
```

以上是 Java Enum 的簡介，內容幾乎都是參考[良葛格 JavaSE6](https://github.com/JustinSDK/JavaSE6Tutorial/blob/master/docs/CH11.md) 的筆記，有興趣可以透過連結閱讀他的詳細解說。

最後還是來個練習吧 ! [[練習](http://tpcg.io/1e0HbS)]

