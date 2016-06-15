# JavaScript 開發注意事項
避免全局變量的使用
----
>原因:  
開發項目越大，使用到第三方JS庫可能導致命名沖突問題，所以在變數定義時一定要記得用 var 來定義，不然JS隱式全局可能會讓你花許多時間來debug。  
例子:  
>>    funciton foo() {  
>>>    var x=3,y=4;  
          result = x + y;     
>>>   return result;  

>>      };  
此時的 result 由於沒有定用 var 定義，所以自動提升為全域變數。  
`function foo() {var a = b = 0};`  
此例子也要注意，由於參數給值是由右向左，所以以上宣告如下:  
`var a = ( b = 0 );`  
所以 b 為全域變數了，所以可以經由 `var a,b; a = b = 0`,  這樣就行了。

忘記var的副作用
----
* 隱式全局變量能經由 delete 來刪除。  
* var 建立的全局變量不可以。  
隱式全局不是真正的全局變量，但它是全局對象的屬性，屬性可以通過 delete 操作符刪除，而變量不能。

單 var 形式
----
>在函數頂部採用單 var 的好處:  
* 提供單一地方找尋局部變量  
* 防止變在定義前使用的邏輯錯誤  

for 循環
-----
>`for(var i = 0; i < myarray.length; i++)`  
此處盡量不要在 for 循環中取長度，因為若今天的數組是一個 HTMLCollection 時每次都要去對 DOM 操作效能會較差。  
可改成`for(var i = 0,x = myarray.length; i < x; i++)`  
循環過程中就只會檢索一次長度值。  
i++ 建議改寫成 i = i + 1  
因為在 JSLint 中的 ++ 會是 false
