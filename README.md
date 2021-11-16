# web-crawler(爬蟲)
## selenium
動態網頁爬蟲
* 安裝
```cmd
pip install selenium
```

*  Webdriver 下載
    * Chrome(https://sites.google.com/a/chromium.org/chromedriver/downloads)

* 使用範例:
```python=
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import Select

options= Options()
options.add_argument("--disable-notifications")
options.add_argument("headless") #設定無介面選項
chrome= webdriver.Chrome('chromedriver',chrome_options = options) #Chromedriver 使用
chrome.get("https://www.ncbi.nlm.nih.gov/pmc/articles/pmid/%s"%(df))
content = chrome.find_element_by_id('mc')
content.close() # 關閉瀏覽器視窗
```

* 定位元素
    * id定位：driver.find_element_by_id()
    * name定位：driver.find_element_by_name()
    * class定位：driver.find_element_by_class_name()
    * link定位：driver.find_element_by_link_text()
    * partial link定位：driver.find_element_by_partial_link_text()
    * tag定位：driver.find_element_by_tag_name()
    * css定位：driver.find_element_by_css_selector()
    * xpath定位：driver.find_element_by_xpath()
* 定位一組元素取下標定位(加[])
    * driver.find_elements_by_id()[]

* 等待
    * 強制等待: time.sleep(5)
    * 隱式等待(果在規定的時間內頁面載入完成後，會立馬執行下一步，否則會等待時間截止才執行下一步): driver.implicitly_wait(10)


* 輸入及點擊
```python=
# 定位搜尋框
element = driver.find_element_by_class_name(“gLFyf.gsfi”)
# 傳入字串
element.send_keys(“Selenium Python”)
element.clear()
button = driver.find_element_by_class_name(“gNO89b”)
button.click()
```

* send_keys模擬鍵盤輸入
```python=
from selenium.webdriver.common.keys import Keys
"""Set of special keys codes."""
NULL = '\ue000'
CANCEL = '\ue001' # ^break
HELP = '\ue002'
BACKSPACE = '\ue003'
BACK_SPACE = BACKSPACE
TAB = '\ue004'
CLEAR = '\ue005'
RETURN = '\ue006'
ENTER = '\ue007'
SHIFT = '\ue008'
LEFT_SHIFT = SHIFT
CONTROL = ‘\ue009’
LEFT_CONTROL = CONTROL
ALT = ‘\ue00a’
LEFT_ALT = ALT
PAUSE = ‘\ue00b’
ESCAPE = ‘\ue00c’
SPACE = ‘\ue00d’
PAGE_UP = ‘\ue00e’
PAGE_DOWN = ‘\ue00f’
END = ‘\ue010’
HOME = ‘\ue011’
LEFT = ‘\ue012’
ARROW_LEFT = LEFT
UP = ‘\ue013’
ARROW_UP = UP
RIGHT = ‘\ue014’
ARROW_RIGHT = RIGHT
DOWN = ‘\ue015’
ARROW_DOWN = DOWN
INSERT = ‘\ue016’
DELETE = ‘\ue017’
SEMICOLON = ‘\ue018’
EQUALS = ‘\ue019’
NUMPAD0 = ‘\ue01a’ # number pad keys
NUMPAD1 = ‘\ue01b’
NUMPAD2 = ‘\ue01c’
NUMPAD3 = ‘\ue01d’
NUMPAD4 = ‘\ue01e’
NUMPAD5 = ‘\ue01f’
NUMPAD6 = ‘\ue020’
NUMPAD7 = ‘\ue021’
NUMPAD8 = ‘\ue022’
NUMPAD9 = ‘\ue023’
MULTIPLY = ‘\ue024’
ADD = ‘\ue025’
SEPARATOR = ‘\ue026’
SUBTRACT = ‘\ue027’
DECIMAL = ‘\ue028’
DIVIDE = ‘\ue029’
F1 = ‘\ue031’ # function keys
F2 = ‘\ue032’
F3 = ‘\ue033’
F4 = ‘\ue034’
F5 = ‘\ue035’
F6 = ‘\ue036’
F7 = ‘\ue037’
F8 = ‘\ue038’
F9 = ‘\ue039’
F10 = ‘\ue03a’
F11 = ‘\ue03b’
F12 = ‘\ue03c’
META = ‘\ue03d’
COMMAND = ‘\ue03d’ 
```

* 填充表單
```python=
s1 = Select(chrome.find_element_by_css_selector('body > table:nth-child(8) > tbody > tr > td:nth-child(3) > table.b1.r10_0 > tbody > tr > td > table > tbody > tr > td:nth-child(1) > nobr:nth-child(1) > select'))
s1.select_by_index(2)
```

## BeautifulSoup (解析html)
* 範例
```python=
from bs4 import BeautifulSoup
soup = BeautifulSoup(chrome.page_source, 'html.parser')
data = soup.select_one("#txtFinDetailData")

import pandas as pd
dfs = pd.read_html(data.prettify())
df = dfs[0]
df
```
* 解析HTML內容
``` python=
from bs4 import BeautifulSoup
soup = BeautifulSoup(text, "html.parser")
print(soup.prettify())  #輸出排版後的HTML內容
text = soup.get_text()  #remove HTML markup
print(text)
```

## requests
* 安裝
```cmd
pip install requests
```
* 使用範例:
```python=
import requests
headers = {'user-agent': 'Mozilla/5.0'}
r = requests.get('https://api.github.com/events')
r = requests.post('http://httpbin.org/post', data = {'key':'value'})
r = requests.put('http://httpbin.org/put', data = {'key':'value'})
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('http://httpbin.org/get', params=payload, headers=headers)

print(r.url) #查看傳送的 URL
print(r.text) #列出文字
print(r.encoding) #列出編碼
print(r.status_code) #列出 HTTP 狀態碼
print(r.headers) #列出 HTTP Response Headers
print(r.headers['Content-Type']) #印出 Header 中的 Content-Type

```

# 工具箱
## NLTK
全名是 Natural Language Tool Kit， 是一套基於 Python 的自然語言處理工具箱
官方文件: http://www.nltk.org/book/
* 安裝
```cmd
pip install nltk
```
```python=
# 安裝 NLTK 相關套件
nltk.download()
```
![](https://i.imgur.com/iuH2a7u.png)
![](https://i.imgur.com/G9Mbflr.png)
* 舉例
```python=
#載入內建的書籍文字檔
from nltk.book import *
# 搜尋字詞功能
text3.concordance("lived")
# 近似字
text1.similar("monstrous")
# 相異字詞
set(text4)
# 相異字詞排序
sorted(set(text4))
# 構造文本的詞彙分佈圖
text4.dispersion_plot(["citizens", "democracy", "freedom", "duties", "America", "liberty", "constitution"])


```
* 基本功能統整
    * book.concordance()
        * 搜尋字詞：顯現字詞出現的上下文
    * book.similar()、book.common_contexts()
        * 找近似字
    * len(set(book))/ len(book)
        * 詞彙多樣性
    * book.dispersion_plot()
        * 詞彙分布圖
    * sent1 + sent2
        * 文本的結合
* 分開英文句子(斷句)
```python=
from nltk.tokenize import sent_tokenize
mytext = "Hello Adam, how are you? I hope everything is going well. Today is a good day, see you dude."
print(sent_tokenize(mytext))
```
```python
['Hello Adam, how are you?', 'I hope everything is going well.', 'Today is a good day, see you dude.']
```
