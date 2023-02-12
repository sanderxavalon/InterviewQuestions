# 環境架設

## Java

==**注意：因公司使用問題，本釋例為AdoptOpenJDK 8**==

### 下載Java並安裝

1. 點擊連結 [https://adoptium.net/temurin/releases/?version=8](https://adoptium.net/temurin/releases/?version=8)
![](images/Java/1_download.png)

2. 下載後開啟
![](images/Java/2_1.png)
![](images/Java/2_2.png)
![](images/Java/2_3.png)

3. 確認安裝成功

   1. 開啟CMD
   2. 輸入`java -version`與`javac`，看到以下訊息便表示安裝成功
   ![](images/Java/3.png)

## Maven

### 下載Maven並且解壓縮

![](./images/maven/1_download.png)

選定一個資料夾解壓縮，==請記住路徑==

### 設定Maven Home

1. 
![](images/maven/2_1_setting.png)
2. 
![](images/maven/2_2_advanceSetting.png)
3. 
![](images/maven/2_3_environmentSetting.png)
4. 
![](images/maven/2_4_newPath.png)
5.
![](images/maven/2_5_editPathEnv.png)
6. 
![](images/maven/2_6_setPath.png)
7. 
![](images/maven/2_7_addPathEvn.png)

以上便設定完成。

### 確認安裝成功

1. 開啟CMD
2. 輸入`mvn -v`，看到以下訊息便表示安裝成功

![](images/maven/3_mavenVersion.png)

# 基礎語法

## 第一個程式

```java
public class App {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

### 定義類別

> *撰寫 Java 程式通常都是由定義「類別」開始，"class" 是 Java 用來定義類別的關鍵字，範例中類別的名稱是 App，這與您編輯的檔案（App.java）主檔名必須相同，App 類別使用關鍵字 "public" 宣告。*
> 
> *在編寫 Java 程式時，**一個檔案中可撰寫數個類別，但是只能有一個公開（public）類別，而且檔案主檔名必須與這個公開類別的名稱相同**，在定義類別名稱時，建議將類別首字母大寫，並在類別名稱上表明類別的作用。*
>
> *Java SE 6 技術手冊，[第一個Java程式](https://github.com/JustinSDK/JavaSE6Tutorial/blob/master/docs/CH03.md#31-%E7%AC%AC%E4%B8%80%E5%80%8B-java-%E7%A8%8B%E5%BC%8F)*

### main()方法解說

main() 是 Java 程式的「進入點」（Entry point），程式的執行是由進入點開始的。

- public：表示此方法可以被外部呼叫。
- static: Main方法不需要實例化物件便可執行
- void：主方法是程式的起點，所以不需要任何的返回值。
- main: 系統規定好預設呼叫的方法名稱，執行時預設找到main方法名稱。

### System.out.print

這裡不琢磨太多IO相關的問題，簡單來講就是調用了System類別中的out去把文字輸出。

### 註解

跟大部分語言一樣，語法為`//`，或是`/* */`，要注意的是`/** */`為Javadoc，生成Java手冊用的工具，可以再查API的時候看到。

```java
public class App {
    public static void main(String[] args) {

        // This is comment
        /*
         * Hello world!
         */
        /** 
         * This is javadoc
         * @authoer  Sander Chen
         */
        System.out.println("Hello World!");
    }
}
```

## 基礎資料型態與運算子

### 基礎資料型態(Primitive Type)

![](images/java-data-types.jpg)

```
short 	數值範圍：32767 ~ -32768
int 	數值範圍：2147483647 ~ -2147483648
long 	數值範圍：9223372036854775807 ~ -9223372036854775808
byte 	數值範圍：127 ~ -128
float 	數值範圍：3.402823e+38 ~ 1.401298e-45
double 	數值範圍：1.797693e+308 ~ 4.900000e-324
```

### 運算子

- 算數運算子
![](images/Arithmetic-operators.jpg)

- 邏輯運算子
![](images/Logical-operators.jpg)

- 比較運算子
![](images/Relational-operators.jpg)

## 流程控制

請參考FlowControl.java

# 物件基礎

![](images/Declare-Class.gif)



## `finalize()`

**==Java 9 已棄用==**

## 類別宣告

分為兩個部分，第一行的類別宣告與後面的類別體

### 宣告內容

# Exception

# Collection Framework與Map

# Java 8 Lambda


