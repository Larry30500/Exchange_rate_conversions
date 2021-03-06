<h1 align="center">
  <br>
  [指定專題作品 (Python)] 即時匯率的換算<br>(網路爬蟲之應用)
</h1>


## 目錄
* [摘要](#摘要)
* [重點程式碼說明](#重點程式碼說明)
* [系統環境](#系統環境)
* [聯絡資訊](#聯絡資訊)
* [致謝](#致謝)
* [權限](#權限)

&nbsp;

## 摘要
### 1. 本作品內含網路爬蟲的相關技術，可自動擷取目前臺灣銀行之即時的外匯資料。
### 2. 主要功能為：當使用者輸入 (1)欲被兌換的新臺幣金額 (2)兌換的貨幣種類 之後，本程式則可即時計算出其兌換後的貨幣金額。

![conversion_point03](images/conversion_point03.gif)

<strong><em>假使想要更加了解此程式的話，請參考本頁面底部之作者的聯絡方式。</em></strong>

&nbsp;

## 重點程式碼說明
### 1. 本作品內含網路爬蟲的相關技術，可自動擷取目前臺灣銀行之即時的外匯資料。
```python
# 於臺灣銀行的外匯資訊相關網頁 (https://rate.bot.com.tw/xrt?Lang=zh-TW)，讀取其網頁資料，並找到需要擷取的特定部分。
html_page = urllib.request.urlopen('https://rate.bot.com.tw/xrt?Lang=zh-TW')
sp = BeautifulSoup(html_page, 'html.parser')

# 從爬蟲獲取的外匯資料中，擷取需要的貨幣名稱和匯率。
row_with_currency_names = sp.find_all('貨幣名稱')
cash_rates = sp.find_all('匯率')
⋮
```

&nbsp;

### 2. 主要功能為：當使用者輸入 (1)欲被兌換的新臺幣金額 (2)兌換的貨幣種類 之後，本程式則可即時計算出其兌換後的貨幣金額。
```python
# 在 while 迴圈當中，達到循環輸入的效果，並且設立設立 3 個檢測事項，以確認被輸入的資料是否存在錯誤，而需要重新輸入。  
# 目的：如果使用者輸入錯誤，則提示輸入錯誤，請再輸入一次；如果使用者輸入正確，則前往下個檢測事項，直到最後一個檢測事項將顯示換算結果後，再回到第一個檢測事項。

check_point = 1

while True:
  if check_point == 1:
    # 使用者輸入新臺幣的金額。
    input_NTD = input('請輸入新臺幣的金額：')
    ⋮

    # 若使用者輸入正確，則前往第 2 個檢測事項。
    check_point = 2

  elif check_point == 2:
    # 使用者輸入貨幣名稱
    input_currency = input('貨幣代碼：(1)美金 (2)日圓 (3)韓元 (4)人民幣 (5)澳幣\n\n請輸入您要兌換的貨幣代碼：')
    ⋮

    # 若使用者輸入正確，則前往第 3 個檢測事項。
    check_point = 3

  elif check_point == 3:
    ⋮

    print(f'總共兌換了：{exchanged_amount:.4f}')

    check_point = 1
    counter += 1
```

&nbsp;

### 第 1 個檢測事項：檢查被輸入的新臺幣金額是某有誤。
1. 被輸入的資料並非為整數或浮點數時，則顯示輸入錯誤，並重新要求輸入。
2. 被輸入的金額小於零時，則顯示輸入錯誤，並要求重新輸入。
3. 使用者輸入 Q 或者 q 時，則退出程式。

![conversion_point01](images/conversion_point01.gif)

&nbsp;

### 第 2 個檢測事項：檢查使用者輸入欲兌換的貨幣。
1. 使用者輸入僅限為整數 1 ~ 5 之間，否則顯示輸入錯誤。
2. 使用者輸入若非整數，則顯示輸入錯誤。

![conversion_point02](images/conversion_point02.gif)

&nbsp;
  
### 第 3 個檢測事項：計算出兌換後的外幣金額。
1. 計算並輸出新臺幣兌換外幣的結果。
2. 輸出結果後，自動返回第 1 個檢測事項，讓使用者可以再重新操作。

![conversion_point03](images/conversion_point03.gif)

&nbsp;

## 系統環境
### 本程式所在作業系統
* OS：Windows 7 / 10 (Mac OS、Linux 系統亦可相容)

### 相關套件
* Python 核心：3.10
* Beautiful Soup：4.9

&nbsp;

## 聯絡資訊
👤 **Larry Jhuang**
  * Email: larry30500@gmail.com

&nbsp;
 
## 致謝
*非常感謝指導老師 (Francesco Ke) 提供程式設計的靈感和方向，並充分教導程式設計的注意事項和相關細節。*

*如果您喜歡此專案，記得點擊⭐️支持作者。*

&nbsp;

## 權限
目前設定為 MIT 權限。請參閱 `LICENSE`，了解更多相關 MIT 權限的規定。

&nbsp;

[[ 返回目錄 ]](#目錄)
