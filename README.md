# <img src="https://www.kshs.kh.edu.tw/upload/269/103_28502_media/20110920103706.gif" width="70px" alt="校徽">高雄中學體溫自動填報系統說明
###### tags: `Python` `Tools_developing` `WebCrawler` `Selenium` `BodyTemp`
## 說明
環境配置與程式碼說明，Degub的過程，以及改進的方法

## 系統要求
1. **一台Windows電腦** <font color=#FF6600>(推薦使用Windows 10以上，對Python 3的兼容性比較好，然後選擇Windows是因為有內建的"工作排程器")</font>
2. **Python 3.10** <font color=#FF6600>(為配合selenium自動化操作)</font>
3. **Visual Studio Code** <font color=#FF6600>(Spyder或PyCharm等IDE也可以，在此用VS Code做示範)</font>
4. **Google Chrome**及**Chrome Driver** <font color=#FF6600>(Firefox, Opera和Edge也可以，需要下載不同的Driver)</font>
## 開發前環境配置
### 安裝Visual Studio Code
1. 前往 [VS Code <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Visual_Studio_Code_1.35_icon.svg/2048px-Visual_Studio_Code_1.35_icon.svg.png" width=20px alt="vscode">](https://code.visualstudio.com/)，選擇**Download for Windows**
2. 安裝VS Code，有同意就選同意，有其它選項的，照以下圖片操作：
![](https://i.imgur.com/drVlqJr.png)
這邊不建議去改變安裝位置，避免出現奇奇怪怪的Bug
![](https://i.imgur.com/BMfgghK.png)
這邊選下一步即可
![](https://i.imgur.com/kSALLt4.png)
建議全部選上，方便後續操作

註：首次使用VS Code可能需要設置一些部分，下一步即可
### 安裝Python
1. 前往 [Python <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/768px-Python-logo-notext.svg.png" width=20px alt="python"> ](https://www.python.org/downloads/)，選擇**Download Python 3.10** (註：10後的小數點為例行性更新，直接下載即可)
2. 安裝Python，照以下圖片操作：
![](https://i.imgur.com/XuSitDx.png)
**Add Python 3.10 to PATH<font color=#f0000>**記得要勾上</font>，然後選**Install Now**

### 下載ChromeDriver及設定PATH
#### 下載ChromeDriver
1. 先確認現在執行的是什麼版本的Chrome，照著以下圖片操作來確認版本：
![](https://i.imgur.com/db7xPPp.png)
點擊右上角的三個點
![](https://i.imgur.com/A42jMpy.png)
選擇**設定**
![](https://i.imgur.com/xMCpEZP.png)
點擊左下角的"**進階**" --> **關於Chrome**
![](https://i.imgur.com/wHPTjEM.png)
顯示的內容即是Chrome版本，圖為**Chrome 98**
2. 前往[ChromeDriver](https://chromedriver.chromium.org/downloads)，點擊**與Chrome版本相同的ChromeDriver** --> 點擊下載"**chromedriver_win32.zip**"
3. 解壓縮ChromeDriver (這裡用Windows 11+7-Zip示範)
![](https://i.imgur.com/KNM0bof.png)
右選選擇"**顯示其他選項**" (註：Windows 10不用)
![](https://i.imgur.com/ki83NYd.png)
選擇**7-Zip** --> 解壓縮至"**chromedriver_win32**"

#### 設定PATH
1. 將解壓縮完的資料夾移動到C槽 (建議：這樣在設定PATH及日後更新會更方便)
2. 按下鍵盤上的**Windows按鍵**，輸入"**編輯系統環境變數**"
3. 點擊"**環境變數**" --> 點擊"**Path**" --> 點擊"**編輯**" --> 點擊"**新增**" --> 輸入存放ChromeDriver資料夾的位置 (如果按照上的說明操作，位置為：**C:\chromedriver_win32**） --> 按確定 --> 重開機

附圖：
![](https://i.imgur.com/S4hZxkN.png)

![](https://i.imgur.com/YnN0UIW.png)
<font color=#f0000>**注意不要編輯下面那個系統變數，亂動會搞不開機的**</font>
![](https://i.imgur.com/YVkQJcS.png)
完成後記得重開機

### 完成環境設置與測試
#### 用Visual Studio Code開啟Python檔案資料夾
1. 找一個地方建立一個專門用來放程式的資料夾 (像是在桌面建立一個Python_files資料夾。<font color=#f0000>請注意：資料夾明子最好不要出現**空格**、**中文字**或**特殊符號**，不然容易報奇怪的錯誤代碼，如需連接兩個字，請用**下引號" _ "** 進行連接</font>)
2. 在資料夾上**點擊右鍵** --> 選擇"**以Code開啟**"
#### 建立一個Python檔案
1. 點擊新增檔案按紐
2. 新增一個檔案，副檔名為"**.py**" 
![](https://i.imgur.com/V0A74RF.png)
新增檔案按紐，在滑鼠游標靠近時會自動出現
![](https://i.imgur.com/xJoXBDW.png)
命名規則與前面建立資料夾基本相同，但是**可以用中文字** (這點作者也不清楚為何，理論上資料夾也應該行，或許是ASCII碼轉換相關的Bug)
#### 用Hello World測試安裝是否正確
前面已經開好了一個Python檔案，測試一下安裝是否正確
1. 在編輯區輸入
```python=1
print("hello, world")
```
3. 點擊右上角的**三角形撥放鍵** (如果沒有出現，就把VS Code關掉，照前面開資料夾的步驟重開一次)
![](https://i.imgur.com/NWB5EdN.png)
3. 如果正常執行，會出現以下的回傳值
![](https://i.imgur.com/qt0OcCG.png)
4. 寫完程式，記得要按"**Ctrl + S**"儲存


#### 安裝相關module
這次的體溫填報城市需要使用到"**selenium**"這個module，所以要在開始編譯程式之前，需要先把這個module裝好，執行的時候才不會出現錯誤
1. 在底下terminal中輸入
``` python
pip install selenium
```
![](https://i.imgur.com/wmr2jjX.png)
</br>按**Enter**等待安裝</p>
![](https://i.imgur.com/Utp5YDQ.png)
</br>出現框起來的這行時，表示安裝已順利完成</p>
#### 設定"工作排程器"
Windows自帶了一個小功能，叫做"**工作排程器**"，這個自動填報體溫系統之所以會每天定時啟動的關鍵就在此!
以下開始設定，此方法也可用於定時啟動其他程序，例如定時開LOL之類的。
1. 按鍵盤**Windows鍵** --> 輸入"**工作排程器**"
![](https://i.imgur.com/jaB4R9v.png)
2. 選擇"**建立基本工作...**"
![](https://i.imgur.com/vH83nph.png)
3. 幫程序命名 (在此以**填體溫**作為示範)
![](https://i.imgur.com/cxyRNXU.png)
4. 依需求選擇執行週期
![](https://i.imgur.com/RKeYNfX.png)
5. 如果要定時執行程式，就選擇"**啟動程式**"
![](https://i.imgur.com/jdjYhgm.png)
6. 使用右邊的"**瀏覽**"按鈕找到存放程式的地方
![](https://i.imgur.com/W6iFgZn.png)
7. 確認**程序名稱**、**執行的時間**、**執行的程序**都正確後，按下完成即可
![](https://i.imgur.com/Q8OWjCC.png)

到此就完成了簡單自動化操作的流程了。上面所舉例的填體溫程式，可以參考下面的寫法


## 程式碼與說明
有顏色的部分為程式碼 #後方文字為說明
```python=1
from selenium import webdriver  #從selenium函式庫，引入網頁自動化操作驅動
import random   #引入random函式庫

driver = webdriver.Chrome() #調用Chrome驅動
driver.get('https://webap1.kshs.kh.edu.tw/kshsSSO/publicWebAP/bodyTemp/index.aspx') #前往"網址" //此網址為高雄中學體溫填報網站

class rand_temp:    #建立"rand_temp"類別 //用來亂數生成體溫數據
    global rand_1, rand_2   #將變數宣告為全域變數
    rand_1 = random.randint(35, 36) #變數"and_1"由"random"函式庫生成，範圍介在(35,36)之間
    rand_2 = random.randint(0, 9)   #變數"and_2"由"random"函式庫生成，範圍介在(0,9)之間

class Program:  #建立"Program"類別 //用來執行網頁自動化操作
    class part_1:   #建立"part_1"類別 //用來進入網站並填入身分證
        element_input = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[1]/td/input[1]") #由xpath找到元件 //此為身分證填入區
        element_input.send_keys("****") #對元件輸入"****" //雙引號之間要填身分證
        element_button = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[1]/td/input[2]")    #由xpath找到元件 //此為確認框
        element_button.click()  #點擊元件

    class part_2:   #建立"part_2"類別 //用來操作體溫填報區
        element_selector_1 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/span[2]/input[2]")    ##由xpath找到元件 //此為
        element_selector_1.click()  #點擊元件
        element_selector_2 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/select[1]")   ##由xpath找到元件 //此為
        element_selector_2.send_keys(rand_1)    #對元件輸入"****" //雙引號間為體溫
        element_selector_3 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/select[2]")   ##由xpath找到元件 //此為
        element_selector_3.send_keys(rand_2)    #對元件輸入"****" //雙引號間為體溫(小數點)
        element_selector_4 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/select[3]")   ##由xpath找到元件 //此為
        element_selector_4.send_keys("正常")    #對元件輸入"正常" 
        element_button_2 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/input") ##由xpath找到元件 //此為
        element_button_2.click()    #點擊元件
        
    class part_3:   #建立"part_3"類別 //完成操作後用來退出瀏覽器
        driver.quit()   #退出瀏覽器
```
## 開發動機
開學第一天，學校就要求所有人每天都要上網填體溫，沒有填要記警告；剛開始覺得還好，因為之前學校根本沒有那麼高科技的東西，所以還算挺新奇的；但是時間長了之後，新鮮感沒了，填體溫就變成一種繁雜的瑣事，藉此便想說來開發一個自動填報體溫的程式。
## 開發中的問題及修正方向
在開發這個程式的過程中，前前後後遇到過很多奇怪的Bug；像是用著用著，突然找不到ChromeDriver或是資料夾命名完，VS Code卻一直找不到之類的；這也是我第一次使用selenium開發工具，所以在很多地方還顯得很生疏，下面分享我從開始編寫及Debug的過程。

首先是安裝selenium套件的問題，我一開始其實不是用VS Code，我是用Anaconda，但是這個東西說方便是很方便，但預設的位置好像和Python預設安裝位置不太一樣，所以有出現module裝完之後無法import的情況，所以才選擇換用VS Code。

再來是程式突然沒辦法用的問題，原本這套程式我已經用了半年了，一直沒有問題；但是有一天去學校，突然收到沒有填體溫的消息，當下我就傻了，因為就算是斷網，那也會在他執行無法繼續的時候回報錯誤，而當天早上我看電腦什麼報錯的消息都沒有，程序也已正常執行，我想想算了，自己手動開一下程式罷了；但至這一開，問題就浮出來了：開啟之後馬上跳出，我想想這不對，進VS Code看看詳細是甚麼錯誤，這看一看更傻了，它的問題是"沒有安裝ChromeDriver"，這怎麼想都不對，因為它都運行大半年了，怎麼可能沒裝，所以我接著重裝VS Code、裝Python、重裝Chrome、重新設定ChromeDriver的PATH，差一點點要重灌的時候，我想到會不會是更新搞的鬼，所以我去看了一下Chrome版本...Bingo!更新到Chrome 98了，而我之前使用和Debug用的ChromeDriver是版本97的；所以原因就是這樣一個小問題，卻花了我一整天的時間，或許這就是除錯的魅力吧!

![](https://i.imgur.com/0k2Dz0l.png)
**上面這行報錯指令的意思就是chromedriver版本不相容**

對於這套程式可以改進的部分，我個人認為有以下幾點，(有些問題目前的能力還不足以解決)：
1. **語法不夠簡潔**：就像裡面用到的一堆xpath位置，如果不小心刪錯一個字，又要開始Debug了
2. **執行速度需要優化**：因為這個程序在執行多重填報任務的時候，常常卡到不行
3. **延展性不足**：因為這個網頁沒有複雜的元件，所以用"find_element_by_xpath"沒有太大的問題，但是今天如果元件多了起來，那這個方法就不太可行了
4. **無法反爬**：這邊的設計我沒有使用反爬的技巧，不然如果要去爬其他網站，像是crushninja的發文網站，還是有很大的概率觸發機器人檢測的
5. **新增多人填報的模式**：現在要填報多人的體溫，必須在工作排程器一一新增工作，不僅占用記憶體空間，執行效率也不堪入目，所以之後會新增一個list的功能上來 (這個問題會在最終的程式碼解決)
6. **安全性不足**：因為填報體溫的時，所填入的身分證並未加密，所以如果程式碼外流，那個資會直接外流，所以必須加入加密與解密的功能。

## 修正補充程式碼片段
因為新增了多人重複填報的for迴圈，所以會出現需要重複呼叫網頁的需求，故將重複開啟頁面的方式由"開啟新chrome視窗"改為"開啟新的頁面"。 

至於安全性問題，因為目標網站的填入功能並沒有隱藏輸入的字元，所以就算在程式後端完成了加密，執行的時候還是會顯示出解密的資料，所以對此就不多進行加密和解密了。

以下是主要針對多人填報的方面進行改進。
``` python=1
import pyautogui #需先執行pip install pyautogui

global ID, url, ID_input, times, count
url = "https://webap1.kshs.kh.edu.tw/kshsSSO/publicWebAP/bodyTemp/index.aspx"
ID_input = []
count = len(ID_input)    
    
for times in range (0, count):
    ID = ID_input[times]
        
    class rand_temp:
        driver.get(url)
        global rand_1, rand_2
        rand_1 = random.randint(35, 36)
        rand_2 = random.randint(0, 9)

    class Program:
        class part_1:
            element_input = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[1]/td/input[1]").send_keys(ID)
            element_button = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[1]/td/input[2]").click()

        class part_2:
            element_selector_1 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/span[2]/input[2]").click()
            element_selector_2 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/select[1]").send_keys(rand_1)
            element_selector_3 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/select[2]").send_keys(rand_2)
            element_selector_4 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/select[3]").send_keys("正常")
            element_button_2 = driver.find_element_by_xpath("/html/body/form/div[3]/table[2]/tbody/tr[2]/td/input").click()
            
        class part_3:
            pyautogui.hotkey("enter")
            pyautogui.hotkey("ctrl", "t")    #chrome開啟新分頁的快捷鍵      
            driver.switch_to.window(driver.window_handles[times+1])
```

---
<img src="https://www.kshs.kh.edu.tw/upload/269/103_28502_media/20110920103706.gif" width="50px" alt="校徽"><font size="4" font face="微軟正黑體">**高雄中學[CW-Chang](https://hackmd.io/@CW-Chang)提供**</font>