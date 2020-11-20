# 使用Inkscape + Blender 2D 的動畫製作筆記

## 簡介
* 版本： v0.0.1
* 作者： [lian0123](https://github.com/Lian0123/)

## 前言
因為最近在工作時，剛好要弄一個類似MG動畫的動畫，因為沒有太多的資源，所以就在自己的Linux上的幾個開源軟體去做了個動畫。

雖然有在inkscape官網上看到，雖然inkscape官方不支援動畫製作，但是能用blender做成動畫，於是我就這樣踩坑了，然後就把踩坑紀錄寫成筆記，給各位先進與後人參考，雖然不保證是完全正確或是最好的方法。

由於本人非藝術相關科系出生，嚴格上來說是個理工人，所以有些流程上的錯誤與使用一些較工程的描述也請見諒。

同時本人也會將文章備份一份在github，同時提供pdf版本，如果要看pdf版請點此下載。

## 章節
在此將以專案導向的方式去簡單說明，目前預計分成以下幾個章節：
1. 設計動畫與規格 
2. 使用Inkscape繪製人物
3. Blender匯入SVG圖片與一些細節
4. Blender綁定骨架
5. 製作姿勢庫與簡單動畫
6. 使用Eevee Render輸出
7. 使用Cycle Render的節點使用[還沒寫]
8. 對於節點的打光與陰影處理[還沒寫]
9. 設計背景[還沒寫]
10. 設計前景[還沒寫]
11. 實現一幕簡單的動畫[還沒寫]

## 環境
以下皆是使用開源軟體進行創作：
1. 作業系統： Linux(Arch Linux Base)
2. 視窗管理器：Openbox 3.6.1
3. 向量圖繪製：Inkscape 1.0.1
4. 動畫軟體：Blender 2.90.1
5. 後製軟體：Openshot 2.5.1

## 1.設計動畫與規格
### 1.1. 建立劇情的腳本方向
\ ( O w O)/ : 嗯…那就做一個東方的同人小動畫看看吧～

### 1.2. 首先先寫個亂七八糟的小劇本的大綱吧：
```
就弄一個琪露諾在霧之湖把大妖精冰住的小動畫
```

### 1.3. 制定規格
```
人物：
 │
 ├── 琪露諾：
 │     │
 │     └── fllow 紅魔鄉的設計
 │
 └── 大妖精：
       │
       └── fllow 紅魔鄉的設計

背景：
 |
 ├── 背景：
 │     │
 │     ├── 霧之湖與山林：湖占需小於畫面1/3，符合井字構圖。
 │     │
 │     ├── 紅魔館：東京立教大學為原型
 │     │
 │     ├── 天空：色彩淺藍
 │     │
 │     └── 雲朵：白
 │
 └── 前景：
       │
       └── 草：深綠
```

### 1.4. 以下我們先省略草稿與分鏡的流程
~~其實是懶得寫~~

### 1.5. 劇本檔案
```
```

## 2. 使用inkscape繪製人物
本段將講述如何使用inscape進行基本常見的操作。

### 2.1. inkscape介紹
inkscape為一款開源的向量圖繪製軟體，[原始碼以GPLv3+授權](https://en.wikipedia.org/wiki/Inkscape#cite_ref-3)，所謂的開源軟體就是將軟體的程式碼公開，任何人都人對此進行貢獻與使用。

當然在使用其原始碼時也是需要顧慮其授權協定，但在此的[GPLv3+](https://en.wikipedia.org/wiki/GPLv3%2B)是對於原始碼的授權，而非對於使用其創作的演伸發行SVG圖片創作。

所以如果你要使用該原始碼去寫另一個程式時需遵守GPLv3+的授權，但由於我們只是使用該原始碼的程式進行創作，在此我們不會對於程式原始碼做變動與發佈，我們的SVG創作不會被授權綁住，我們能保有我們的著作權與使用權利。

對於開源軟體的歷史有興趣的讀者，本人建議可以去了解看看一些著名的[開源軟體](https://zh.wikipedia.org/wiki/%E5%BC%80%E6%BA%90%E8%BD%AF%E4%BB%B6)：[Linux](https://zh.wikipedia.org/wiki/Linux)、[Firefox](https://zh.wikipedia.org/wiki/Firefox%E7%80%8F%E8%A6%BD%E5%99%A8)、[VLC](https://zh.wikipedia.org/zh-tw/VLC%E5%A4%9A%E5%AA%92%E9%AB%94%E6%92%AD%E6%94%BE%E5%99%A8)、[VS Code(限原始碼)](https://zh.wikipedia.org/wiki/Visual_Studio_Code)、[Apache Server](https://zh.wikipedia.org/zh-tw/Apache_HTTP_Server)等.....。

### 2.2. svg介紹與標準
首先SVG標準，是[w3c](https://zh.wikipedia.org/zh-tw/%E4%B8%87%E7%BB%B4%E7%BD%91%E8%81%94%E7%9B%9F)提供的標準，目前的現有標準為[REC-SVG11-20110816](https://www.w3.org/TR/SVG11/REC-SVG11-20110816.pdf)的SVG 1.1版本。

#### 2.2.1. 標準是否會被實做
當然標準只是參考用的，實際上在實做上不一定被實現或是完全實現，主要有兩種情況：第一種是實做不完整，第二種則是實做上會增加自己的標準來輔助，我知道這不容易使人理解，在此舉了機個例子。

#### 2.2.2. 標準實做不完整例子
然而標準基本上在實做中，有些不一定會完全實現，著名的就是[Visual C對ISO9899:2011的實現](https://zh.wikipedia.org/wiki/C11#%E6%94%AF%E6%8F%B4)。

#### 2.2.3. 實做不完整的例子
當然也有的是在實做上使用一些自己的規格來輔助，像是office的[OpenXML](https://zh.wikipedia.org/zh-tw/Office_Open_XML)格式標準[ECMA376](http://www.ecma-international.org/publications/standards/Ecma-376.htm)，[微軟使用了一些非規範外的標準來設計](https://zh.wikipedia.org/wiki/Office_Open_XML#%E6%89%B9%E8%A9%95)，要不然使用libreOffice或OpenOffice做文書處理時，在檢視文件的兼容上就會更好了。

#### 2.2.4. Inkscape的情況
而在此inkscape輸出的SVG，[除了部份幾個功能沒有符合標準，大致遵從SVG標準外，就官方的說法他們連還是草稿的SVG 2.0標準都有去進行支援](https://inkscape.org/zh-hant/learn/faq/#what-svg-features-does-inkscape-implement)，也使用自己的規格來進行輔助的設計，預設是提供inkscape SVG的格式，當然你也可以選擇導出一般的SVG格式進行儲存，但實際上你即便是使用一般SVG格式進行儲存，在檔案中還是能看到 **<inkscape:** 開頭的標籤，這就是屬於inkscape的獨有標籤，當然這在一般未實施此標準的檢視上，[會被當成無效標籤](https://inkscape.org/zh-hant/learn/faq/#what-inkscape-svg-opposed-plain-svg)，所以檔案還是能開，但可能不一定是你想要的結果。

另一個inkscape的代表例子是輔助線，像是一般SVG圖片中是沒有輔助線的，但為了設計SVG上的方便，所以inkscape有提供輔助線的功能。


### 2.3. 使用幾何繪製物件
<center>
    <img src="./source/ch2/0010.png">
    <div>打開inkscape頁面</div><br>
</center>

<center>
    <img src="./source/ch2/0020.png">
    <div>首先先畫個圓</div><br>
</center>

<center>
    <img src="./source/ch2/0030.png">
    <div>再畫第二個圓</div><br>
</center>

<center>
    <img src="./source/ch2/0040.png">
    <div>設成相同色彩</div><br>
</center>

<center>
    <img src="./source/ch2/0050.png">
    <div>再用左右鍵調整位置與拉展物件</div><br>
</center>

<center>
    <img src="./source/ch2/0060.png">
    <div>接著選起兩個物件</div><br>
</center>

* 按住shift時，我們能連選物件，同樣的shift選取時按下兩次能取消選取。

<center>
    <img src="./source/ch2/0070.png">
    <div>將物件相加以方便後續的操作</div><br>
</center>

* 在此的相加是[集合](https://zh.wikipedia.org/zh-tw/%E9%9B%86%E5%90%88_(%E6%95%B0%E5%AD%A6))的相加，基本上數學課應該都是有教過，但有一個重點，如果是減去之類的指令，是**先選的區域**減去**後選的區域**，請記得順序不要選錯。

* 另一方面是，由於該SVG在改變後會以路徑形式進行取代，這意謂著，有可能在集合處理後，可能會有一點點的偏移或亂掉發生，當然這發生機率很低，甚至可以忽略，但如果發生，請用節點去調整。

<center>
    <img src="./source/ch2/0080.png">
    <div>兩物件就變成一個物件了</div><br>
</center>

<center>
    <img src="./source/ch2/0090.png">
    <div>而且是由其svg底下的節點進行變更</div><br>
</center>

<center>
    <img src="./source/ch2/0100.png">
    <div>而且是由其svg底下的節點進行變更然後使用貝茲曲線工具畫頭髮</div><br>
</center>

* 在此的貝茲曲線工具有數個模式，情參照圖片左上的**模式**，每個模式在操作上都有不同。

* 當然其實也可以使用鉛筆工具進行繪製，但在此筆者沒有特別研究，但是有看過使用鉛筆工具進行調整，達到很好的繪圖效果之案例。

<center>
    <img src="./source/ch2/0110.png">
    <div>在此我們能看到按下去後會拉動一條直線</div><br>
</center>

<center>
    <img src="./source/ch2/0120.png">
    <div>如果我們直接點下來，就會變成曲線，前面的路徑會隨著後面變更</div><br>
</center>

<center>
    <img src="./source/ch2/0130.png">
    <div>但如果是按住shift一併接點下來，該段就會變成純直線，不會受到後面路徑影響</div><br>
</center>

<center>
    <img src="./source/ch2/0140.png">
    <div>然後在此先化一個頭髮物件，在此當快要拉好時，對開始點按一下就可以變成平面</div><br>
</center>

<center>
    <img src="./source/ch2/0150.png">
    <div>接著可以用對點編輯模式去對向量物件的點進行編輯</div><br>
</center>

<center>
    <img src="./source/ch2/0160.png">
    <div>拉伸完對物件進行填色</div><br>
</center>

<center>
    <img src="./source/ch2/0170.png">
    <div>如果對於預設色卡不滿意可以按下填充色彩預覽的位置右鍵後，按下的編輯填色</div><br>
</center>

* 在此使用的色卡是Inkscape預設色卡，我們可以按下右下的三角型切換成其他色卡，有些滿有趣的色卡，可以玩看看：Android icon palette、Bootstrap 5、Ubuntu、Windows XP icon。

<center>
    <img src="./source/ch2/0180.png">
    <div>然後選擇一個適合的顏色作為填充</div><br>
</center>

<center>
    <img src="./source/ch2/0190.png">
    <div>由於我們不要邊框，所以在此在邊框的預覽色下右鍵後按下移除邊框</div><br>
</center>

* 在此不使用邊框的原因如下：因為之後匯入blender做動畫時，外框的解析匯出問題，你所設定的框線的粗細不一定能正常維持。

* 解決此問題的方式非常簡單，我們能透過**工具列**的**路徑**下的**邊框轉路徑**選項，去對於我們選取的邊框轉成路徑，這時我們就能像是一般物件去進行操作了。

<center>
    <img src="./source/ch2/0200.png">
    <div>再來畫個頭皮</div><br>
</center>

<center>
    <img src="./source/ch2/0210.png">
    <div>沿著頭部邊緣畫並如前所述，留下填充</div><br>
</center>

<center>
    <img src="./source/ch2/0220.png">
    <div>在此可以透過滴管來選色</div><br>
</center>

<center>
    <img src="./source/ch2/0230.png">
    <div>當然在此建議頭皮色彩先不用設的和髮色一樣，能比較方便辨識，並重複動作到頭髮完成</div><br>
</center>

<center>
    <img src="./source/ch2/0240.png">
    <div>在此以畫好額前的頭髮，接著要去處理兩側與後方的頭髮</div><br>
</center>

<center>
    <img src="./source/ch2/0250.png">
    <div>在此又用另一種顏色來描述兩側與後面的頭髮，以說明層次的問題</div><br>
</center>

<center>
    <img src="./source/ch2/0260.png">
    <div>除了用按下往前往後一層的按鍵外，也能透過pgup_pgdown等按鍵直接操作</div><br>
</center>

<center>
    <img src="./source/ch2/0270.png">
    <div>當然後面的頭髮也是先在前面弄好後放到後面</div><br>
</center>

<center>
    <img src="./source/ch2/0280.png">
    <div>最終完成頭髮部份</div><br>
</center>

<center>
    <img src="./source/ch2/0290.png">
    <div>然後把頭髮分成前後兩色</div><br>
</center>

<center>
    <img src="./source/ch2/0300.png">
    <div>以防怕這張變成赤蠻其(誤)先補上個脖子</div><br>
</center>

<center>
    <img src="./source/ch2/0310.png">
    <div>然後再造一個蝴蝶結(在此為了方便辨識暫用紅色)</div><br>
</center>

<center>
    <img src="./source/ch2/0320.png">
    <div>一個移到最下層，然後再造一個蝴蝶結</div><br>
</center>

<center>
    <img src="./source/ch2/0330.png">
    <div>組合成半組蝴蝶結</div><br>
</center>

<center>
    <img src="./source/ch2/0340.png">
    <div>再微調一下就完成了</div><br>
</center>

<center>
    <img src="./source/ch2/0350.png">
    <div>如果你想要，可以在頭部的頭髮下方的臉先加入一組陰影</div><br>
</center>

<center>
    <img src="./source/ch2/0360.png">
    <div>然後再微調一下</div><br>
</center>

<center>
    <img src="./source/ch2/0370.png">
    <div>也能在脖子上增加陰影</div><br>
</center>

<center>
    <img src="./source/ch2/0380.png">
    <div>把下半部蝴蝶結完成</div><br>
</center>

<center>
    <img src="./source/ch2/0390.png">
    <div>是時候把蝴蝶結調回藍色了</div><br>
</center>

<center>
    <img src="./source/ch2/0400.png">
    <div>然後使用貝茲曲線繪製主幹</div><br>
</center>

<center>
    <img src="./source/ch2/0410.png">
    <div>大概使用3塊填充物件完成主幹雛型</div><br>
</center>

<center>
    <img src="./source/ch2/0420.png">
    <div>使用SVG圖的節點編輯將直線彎曲化</div><br>
</center>

<center>
    <img src="./source/ch2/0430.png">
    <div>完成第一塊的主幹</div><br>
</center>

<center>
    <img src="./source/ch2/0440.png">
    <div>完成第二塊的主幹</div><br>
</center>

<center>
    <img src="./source/ch2/0450.png">
    <div>最後完成第三塊的主幹</div><br>
</center>

<center>
    <img src="./source/ch2/0460.png">
    <div>去除外框再上色</div><br>
</center>

<center>
    <img src="./source/ch2/0470.png">
    <div>再用同方法繪製鎖骨</div><br>
</center>

<center>
    <img src="./source/ch2/0480.png">
    <div>然後畫出四肢的連階段附近的關節處</div><br>
</center>

<center>
    <img src="./source/ch2/0490.png">
    <div>開始繪製四肢(右手)</div><br>
</center>

<center>
    <img src="./source/ch2/0500.png">
    <div>上色後請注意不要蓋掉關節處(讓該四肢移到最下層)</div><br>
</center>

<center>
    <img src="./source/ch2/0510.png">
    <div>這時就能看到不錯的樣子了</div><br>
</center>

<center>
    <img src="./source/ch2/0520.png">
    <div>進入選取模式</div><br>
</center>

<center>
    <img src="./source/ch2/0530.png">
    <div>對於選取物件再按第二下變成旋轉物件模式</div><br>
</center>

<center>
    <img src="./source/ch2/0540.png">
    <div>再來把中間的錨點移動至你未來想再動畫中的定位點位置(也就是你要旋轉關節的點)</div><br>
</center>

<center>
    <img src="./source/ch2/0550.png">
    <div>我們可以看到目前手臂的位置轉到這程度時會偏移掉</div><br>
</center>

<center>
    <img src="./source/ch2/0560.png">
    <div>逐漸精修至符合到動畫範圍</div><br>
</center>


* 在此這麼做的目的是確保之後到blender上關節的綁定能正常操作，在選轉時不會飛掉，我們的定位點實際上就是我們到時綁骨架最適合的定位點。

* 其實我們的操作，就像是[皮影戲](https://zh.wikipedia.org/wiki/%E7%9A%AE%E5%BD%B1%E6%88%B2)一樣，對著人偶的關節做控制，來達到動畫效果。

<center>
    <img src="./source/ch2/0570.png">
    <div>逐一對於子關節進行調整</div><br>
</center>

* 雖然我們骨架延伸的部份，未因為上方的骨架而受影響（白話文：轉動你的手部關節就能知道下方關節會受到上方影響），所以在實際上找到一個好定位點不容易，但在此還是得要確保轉動上能正常執行。

<center>
    <img src="./source/ch2/0580.png">
    <div>然後進行測試</div><br>
</center>

<center>
    <img src="./source/ch2/0590.png">
    <div>繼續進行測試</div><br>
</center>

<center>
    <img src="./source/ch2/0600.png">
    <div>試用複製與鏡像完成另一隻手</div><br>
</center>

<center>
    <img src="./source/ch2/0610.png">
    <div>開始繪製腿部</div><br>
</center>

<center>
    <img src="./source/ch2/0620.png">
    <div>測試腿部關節</div><br>
</center>

<center>
    <img src="./source/ch2/0630.png">
    <div>再加上一點輪廓細調後，最終基本身體大致上是完成了</div><br>
</center>

<center>
    <img src="./source/ch2/0640.png">
    <div>然後進入製作衣服的流程</div><br>
</center>

<center>
    <img src="./source/ch2/0650.png">
    <div>先製作出衣服的上半部份</div><br>
</center>

<center>
    <img src="./source/ch2/0660.png">
    <div>在上面放一個遮罩(領口用的空間)</div><br>
</center>

<center>
    <img src="./source/ch2/0670.png">
    <div>然後先選白色衣服，再選擇遮罩</div><br>
</center>

<center>
    <img src="./source/ch2/0680.png">
    <div>再從路徑下選擇減去</div><br>
</center>

<center>
    <img src="./source/ch2/0690.png">
    <div>這時我們就能看到完美的領口了</div><br>
</center>

<center>
    <img src="./source/ch2/0700.png">
    <div>當然裙子也要一併處理</div><br>
</center>

<center>
    <img src="./source/ch2/0710.png">
    <div>當然裙子也是一下子就能完成，如果要做出層次的效果可以去疊多個物件</div><br>
</center>

<center>
    <img src="./source/ch2/0720.png">
    <div>然後做袖子的時候，請記得符合原本肢體與定位點的移動範圍，否則再轉的時候就會出現奇杷的破洞</div><br>
</center>

<center>
    <img src="./source/ch2/0730.png">
    <div>同時也要記得層次要正確(雖然到了blender要重弄一次)</div><br>
</center>

<center>
    <img src="./source/ch2/0740.png">
    <div>像是袖子的袖口則是可以往後拉一點，方便動畫的實現</div><br>
</center>

<center>
    <img src="./source/ch2/0750.png">
    <div>然後完成後可以再轉一次看看，檢查有無問題</div><br>
</center>

<center>
    <img src="./source/ch2/0760.png">
    <div>這時我們就可以看到衣服有破洞</div><br>
</center>

<center>
    <img src="./source/ch2/0770.png">
    <div>拉動衣服的節點使衣服符合動作，來補破洞</div><br>
</center>

<center>
    <img src="./source/ch2/0780.png">
    <div>然後最底層的衣服就完成了</div><br>
</center>

<center>
    <img src="./source/ch2/0790.png">
    <div>繼續疊圖完成服飾</div><br>
</center>

<center>
    <img src="./source/ch2/0800.png">
    <div>逐漸修正至能遮住主幹上的底層衣服，不含其他和衣領與袖子銜接的部份</div><br>
</center>

<center>
    <img src="./source/ch2/0810.png">
    <div>微調一下後，最後填入色彩</div><br>
</center>

<center>
    <img src="./source/ch2/0820.png">
    <div>另外一半的衣服也是一樣</div><br>
</center>

<center>
    <img src="./source/ch2/0830.png">
    <div>已經能識別出這是一隻⑨了</div><br>
</center>

<center>
    <img src="./source/ch2/0840.png">
    <div>然後開始處理衣領與的領口細部</div><br>
</center>

<center>
    <img src="./source/ch2/0850.png">
    <div>然後考量之後會運動到細部的背面可能也要準備</div><br>
</center>

<center>
    <img src="./source/ch2/0860.png">
    <div>同時要調整到適當的層次</div><br>
</center>

<center>
    <img src="./source/ch2/0870.png">
    <div>微調之後，是個完美的衣領呢</div><br>
</center>

<center>
    <img src="./source/ch2/0880.png">
    <div>然後是拉出蝴蝶結的底</div><br>
</center>

<center>
    <img src="./source/ch2/0890.png">
    <div>微調並設定層次後，就能夠得到一個蝴蝶結了</div><br>
</center>

<center>
    <img src="./source/ch2/0900.png">
    <div>然後我們移動至空白處或是其他空白檔案，開始繪製眼睛</div><br>
</center>

<center>
    <img src="./source/ch2/0910.png">
    <div>先拉出一個角膜</div><br>
</center>

<center>
    <img src="./source/ch2/0920.png">
    <div>再用選取模式複製出另一個作為瞳孔用</div><br>
</center>

<center>
    <img src="./source/ch2/0930.png">
    <div>在選取模式下按住ctrl_shift做等比縮放</div><br>
</center>

<center>
    <img src="./source/ch2/0940.png">
    <div>然後放到適當位置</div><br>
</center>

<center>
    <img src="./source/ch2/0950.png">
    <div>這時你可能會發現一件事情，使用inkscape產生的圓型(方形)在節點上都是只能調參數而已，不能像是路徑一樣直接控制</div><br>
</center>

<center>
    <img src="./source/ch2/0960.png">
    <div>這應該是不如你預期的奇杷拉動情況吧</div><br>
</center>


* 這時就得要從SVG標準談起，實際上由於inkscape中對於基本圖形，如：方形、圓形的產生都是固定的參數調整，所以在此我們要將物體改成path。

* 講的白話一點就是svg檔的描述問題，當我們在用文字編輯器開svg檔案時，我們可以發現svg實際上是xml結構的方式進行儲存。

* 在此我們能開啟一個Inkscape新檔案，建立一個長方形，並點下**工具列**中的**編輯**下的**XML編輯器**進行查看，這樣比較方便說明。

* 首先我們在此先產生出一個方形，這時我們會看到XML編輯器中會出現：

    ```
    <svg:rect id="rect???">
    ```

* 這時我們就能發現到xml上是直接使用rect的格式，而在此我們將會受到rect這物件屬性的限制而無法直接編輯該圖形的節點，所以在此就需要將該物件轉為path，也就是轉成路徑。

* 在此我們若先選取物件，然後點選選項的路徑下的物件轉換為路徑，這時我們再看看XML編輯器中的描述，原本的svg:rect描述，就會變成：

    ```
    <svg:path id="rect???">
    ```

* 這時他就會變成path路徑的描述，當然變成path各有優缺，因為path是用點構成路徑，而在blender中我們的svg物件會因為圖學理論中的[三角網格](https://zh.wikipedia.org/zh-tw/%E4%B8%89%E8%A7%92%E7%B6%B2%E6%A0%BC)的方式去處理，而使得path物件會用到非常多的三角形去填補，這也意謂著在render中對於vector與shader上的處理也會變得相對繁多。

* 當然如果是rect物件到blender則會被稱作Curve，而path則依然叫path。在此我們在此透過畫一個方形與一個隨便畫的路徑並存成一個svg檔，然後將svg檔案匯入blender，並只檢視框線，我們就能看到Curve基本上就是2個三角形組合，而path將會由我們物件的平滑度決定了會用多少個三角形去組合成該平面。

* 而在此的圓形物件也是如此，由原本是SVG下的圓形物件，所以目前只能對圓型的參數進行控制。

<center>
    <img src="./source/ch2/0970.png">
    <div>這時我們就得要先選取物件</div><br>
</center>

<center>
    <img src="./source/ch2/0980.png">
    <div>請選擇路徑下的物件轉路徑</div><br>
</center>

<center>
    <img src="./source/ch2/0990.png">
    <div>我們再從節點模式看，這時看到節點的樣子與剛才不一樣</div><br>
</center>


* 在此使用物件轉路徑後，像是我們的基本圖形如：原型、方形等基本物件都會變成路徑，在此我們就能像是我們畫出來了物件一樣對於節點進行調整了。

<center>
    <img src="./source/ch2/1000.png">
    <div>是不是能正常拉動了</div><br>
</center>

<center>
    <img src="./source/ch2/1010.png">
    <div>首先對於最外層的虹膜進行調整，調整到正常的樣子</div><br>
</center>

<center>
    <img src="./source/ch2/1020.png">
    <div>在動到瞳孔前我們先複製一份瞳孔做成反光</div><br>
</center>

<center>
    <img src="./source/ch2/1030.png">
    <div>為了方便說明，在此先上顏色並移動漸層</div><br>
</center>

<center>
    <img src="./source/ch2/1040.png">
    <div>下拉微調後，就有反光的樣子了(當然因每個人的眼睛畫法不同而有差異)</div><br>
</center>

<center>
    <img src="./source/ch2/1050.png">
    <div>下然後對於外部的虹膜進行複製</div><br>
</center>

<center>
    <img src="./source/ch2/1060.png">
    <div>我們先刪除最下方的節點</div><br>
</center>

<center>
    <img src="./source/ch2/1070.png">
    <div>然後對兩條線進行調整</div><br>
</center>

<center>
    <img src="./source/ch2/1080.png">
    <div>另一部份的陰暗部份就完成了</div><br>
</center>

<center>
    <img src="./source/ch2/1090.png">
    <div>貼齊後有眼睛雛型了</div><br>
</center>

<center>
    <img src="./source/ch2/1100.png">
    <div>用同樣的方式，反光的部份也完成了</div><br>
</center>

<center>
    <img src="./source/ch2/1110.png">
    <div>然後開始畫睫毛</div><br>
</center>

<center>
    <img src="./source/ch2/1120.png">
    <div>當然我們的睫毛不只有一橫，所以要多加幾條</div><br>
</center>

<center>
    <img src="./source/ch2/1130.png">
    <div>再微調後上色</div><br>
</center>

<center>
    <img src="./source/ch2/1140.png">
    <div>還有側邊</div><br>
</center>

<center>
    <img src="./source/ch2/1150.png">
    <div>繪製眼白</div><br>
</center>

<center>
    <img src="./source/ch2/1160.png">
    <div>然後再再再細調，由於在此為了方便展示用淺灰色上色</div><br>
</center>

<center>
    <img src="./source/ch2/1170.png">
    <div>眼睛部份就完成了</div><br>
</center>

* 在此每個人對於眼睛繪製的方式都有所不同，當然也有其他類型的眼睛，但筆者相對熟悉的只有這種。

<center>
    <img src="./source/ch2/1180.png">
    <div>然後選取眼睛，並按下ctrl_g群組化</div><br>
</center>

* 在此我們能由**XML編輯器**或是**物件**去查看我們的物件，群組，也就是用一個<g>標籤去囊括我們所群組化的物件。

<center>
    <img src="./source/ch2/1190.png">
    <div>同時在複製一份 做另一隻眼用</div><br>
</center>

<center>
    <img src="./source/ch2/1200.png">
    <div>把左眼放到適合的位置並進行縮放等調整</div><br>
</center>

<center>
    <img src="./source/ch2/1210.png">
    <div>另一個眼睛也是如此，先複製一個（以防出事）</div><br>
</center>

<center>
    <img src="./source/ch2/1220.png">
    <div>看個人決定要丟到的上下層</div><br>
</center>

<center>
    <img src="./source/ch2/1230.png">
    <div>另一隻眼先水平反轉</div><br>
</center>

<center>
    <img src="./source/ch2/1240.png">
    <div>然後點兩下後，對於群組內的物件進行選取</div><br>
</center>

<center>
    <img src="./source/ch2/1250.png">
    <div>在對內部進行水平反轉</div><br>
</center>

* 大概到了綁骨架時才發現下方的反光沒有轉到，這部份請見諒。

<center>
    <img src="./source/ch2/1260.png">
    <div>然後可以稍微旋轉進行調整</div><br>
</center>

<center>
    <img src="./source/ch2/1270.png">
    <div>也是移動到你覺得適合的位置</div><br>
</center>

<center>
    <img src="./source/ch2/1280.png">
    <div>如果沒問題的話備用的也可以刪掉了</div><br>
</center>

<center>
    <img src="./source/ch2/1290.png">
    <div>補上嘴巴牙齒</div><br>
</center>

<center>
    <img src="./source/ch2/1300.png">
    <div>然後使用與繪製眼睛相同方式做出眉毛</div><br>
</center>

<center>
    <img src="./source/ch2/1310.png">
    <div>然後把眉毛放到對應位置</div><br>
</center>

<center>
    <img src="./source/ch2/1320.png">
    <div>然後把眉毛放到對應層</div><br>
</center>

<center>
    <img src="./source/ch2/1330.png">
    <div>做出翅膀</div><br>
</center>

<center>
    <img src="./source/ch2/1340.png">
    <div>上好顏色後將這部份群組化，並複製</div><br>
</center>

<center>
    <img src="./source/ch2/1350.png">
    <div>複製完後，大致就大公告成了</div><br>
</center>

* 在此有些細節的點，有再進行調整，但在此沒有特別紀錄，也請見諒。

### 2.4. 存檔的檢視問題

<center>
    <img src="./source/ch2/1360.png">
    <div>而當你存檔後，會發現在檢視上只有A4的框框</div><br>
</center>

<center>
    <img src="./source/ch2/1370.png">
    <div>這時我們先按下檔案下的文件屬性</div><br>
</center>

<center>
    <img src="./source/ch2/1380.png">
    <div>你會看到文件屬性的設定視窗</div><br>
</center>

<center>
    <img src="./source/ch2/1390.png">
    <div>按下按鍵</div><br>
</center>

<center>
    <img src="./source/ch2/1400.png">
    <div>這時外面的框框就變得和繪圖區一樣大了</div><br>
</center>

<center>
    <img src="./source/ch2/1410.png">
    <div>這時再存一次檔案後就沒問題了</div><br>
</center>

### 2.5. 其他常見問題與補充事項

#### 2.5.1. 繪製一般物件與路徑物件
如上面所說的，因為一般物件(圓形、方形)的實做SVG其格式，我們在使用時只要指定位置、大小或是長寬就能建立了，所以我們只能對於參數進行操作。

而路徑構成的物件又是另一回事，路徑物件的構成就是路徑，而且是路徑上的各關鍵節點而構成的，所以操作的自由度相對較高，但也比較不容易調整。

#### 2.5.2. 文字物件的處理
在此的inkscape的文字物件，字體是沒有封裝的，所以要保留字體的樣貌建議使用**工具列**下的**路徑**之**物件轉路徑**，若文字想要匯入至blender，請也使用這方法。


#### 2.5.3 匯出為png問題
在此我們能發現，以png匯出我們的繪圖時會有4個選項，由左至右的選項分別為：頁面、繪圖部份、選擇範圍、自訂。

在設定匯出png的頁面中，當我們使用頁面匯出時，會發現我們回匯出的圖片都指囊括於A4大小的框框內（雖然其實在儲存svg圖片時就會發現預覽與瀏覽時，我們的畫面都會被限定在A4大小的白色框框下）。

而調整方法其實很簡單，請於：檔案->文件屬性->頁面->頁面尺寸(自訂尺寸)->按下**將頁面調整成內容大小**->跳出**將頁面調整成圖畫或選擇範圍大小**的按鍵後將其按下。

請注意，當我們是要對於單一物件或多物件進行選取時，inkscape就會自動跳到選擇範圍並設定為我們所選的區域。

另一方面我們前後用VS Code等文字檢視器來較該svg檔案，我們能發現在我們匯出png後，會多了：
```
inkscape:export-filename="/YOU/USER/PATH/FileName.png"
inkscape:export-xdpi="???"
inkscape:export-ydpi="???"
```

這也就是為什麼檔案會發生變動的原因，我們的inkscape的SVG檔案會紀錄你的png檔案輸出位置，下次將會自動指向此位置進行輸出。

### 2.6. 小結
Inkscape確實是一個很好的開源向量圖繪製工具，但請確定下載最新的版本，早期版本有一個神奇的bug，當你連選檔案時就會崩潰的bug。

同時若是要以繪製動畫而言需要非常細心，需要考慮到後續的處理方式進行調整。

## 3. Blender匯入svg圖片與一些細節

### 3.1. Blender介紹
Blender也是一款開源軟體，[原始碼是採用GPLv2+](https://www.blender.org/about/license/)的授權形式進行授權。

基本上，Blender算是在開源軟體中算是滿成功的案例，能有非常好的render引擎、效能管理、甚至是200MB不到的安裝檔。尤其在2.8版本後Blender將界面設計優化，從早期的反人類操作，到現在的符合主流操作習慣的界面。

Blender有提供三種render引擎(彩現引擎)，如下：
* workbench
* eevee
* cycle

而我們比較常用的eevee render引擎與cycle render引擎都有其優勢：
* eevee 就是使用較低的資源進行輸出。
* cycle 就如名字一樣，循環的計算，雖然慢，但效果會非常好。

但在使用上，還是case by case，看要做什麼而定。

### 3.2. 使用Blender匯入svg

<center>
    <img src="./source/ch3/0010.png">
    <div>打開blender，並選擇Animate 2D</div><br>
</center>

* 在此blender在初始啟動且未指定語言時會跳出語言設定，在語言設定後才會看到此畫面。

* 在此的New File有三個選項，分別是：
    * General：也就是預設的3D場景，就是背面的那個。
    * 2D Animation：2D動畫設計模式，也就是我們接下來要用的模式。
    * sculpting：雕刻模式，你可以向是個雕刻家一樣去雕刻出你的模型。
    * VFX：全名為Visual effects，製作特效的模式。
    * Video Editing：影片編輯器，負責後續影片的裁切與組合。

* 當然，以上的選項其實都能靠上面的分頁選項去開啟，但在用new file開啟檔案時，blender會將其他常用的頁面排版模式與設定準備好。

<center>
    <img src="./source/ch3/0020.png">
    <div>我們要先更改模式到物體模式</div><br>
</center>

* 因為我們在用blender 2D時，blender會自動幫我們準備一個繪製用的畫布頁面。

* 但由於我們使用的是使用Inkscape繪製的SVG，所以在此不需要使用此繪製用的畫布。

<center>
    <img src="./source/ch3/0030.png">
    <div>按下物體模式</div><br>
</center>

<center>
    <img src="./source/ch3/0040.png">
    <div>這時選取Stroke的畫布</div><br>
</center>

<center>
    <img src="./source/ch3/0050.png">
    <div>再按下右鍵清除</div><br>
</center>

<center>
    <img src="./source/ch3/0060.png">
    <div>接著匯入svg檔案</div><br>
</center>

<center>
    <img src="./source/ch3/0070.png">
    <div>這時我們能看到右側場景選集會出現我們svg下的各物件</div><br>
</center>

<center>
    <img src="./source/ch3/0080.png">
    <div>然後用滑鼠中鍵選轉畫面並放大畫面至中心頂點，這時我們會看到我們匯入的svg圖檔</div><br>
</center>

* 預設匯入的svg檔都會躺在平面上，所以我們的攝影機其實在預設的角度與位置上，都不太能看到我們匯入的svg物件。

<center>
    <img src="./source/ch3/0090.png">
    <div>由於匯入svg是在0度，我們要讓他轉到面對攝影機，收先需要先選取所有svg物件</div><br>
</center>

* 當然在此也能夠將攝影機x軸位置轉到0度，並將y軸位置設為0m，z軸位置設為-12m，這樣也等同物件翻轉90度後的結果。

<center>
    <img src="./source/ch3/0100.png">
    <div>先選取所有物件，並對於物件按下shift與左鍵選取指定物件</div><br>
</center>

* 在選取多個物件時，我們能用同時按下shift與左鍵對於物件進行選取與取消。

<center>
    <img src="./source/ch3/0110.png">
    <div>然後再到物件座標設定中，將X軸角度設為90度</div><br>
</center>

<center>
    <img src="./source/ch3/0120.png">
    <div>這時我們確發現只有一個物件轉</div><br>
</center>

* 這選取的物件就是我們剛才按下shift與左鍵時最後選取的物件。如果你是其他東西轉動，像是攝影機或是其他東西轉動，這就意謂著，你為後所點選的物件就是這個，即便該物件是否被選取。

* 要了解這件事其實很簡單，這時我們可以先看到右下角的物件**屬性**，只要我們的物件是，就像是這邊最後所選的path1110-9，也就是右邊的小腿。

* 請切記，不論我們在左側的場景中選取到了什麼，由屬性編輯物件的參數時，他一定是按照屬性上所指向的物件去選取。

* 即便是按下shift與左鍵來取消選取時，也會因為最後一次選的物件是那個取消選取物件，而屬性依然指向到那個物件，也就是在參數更改上也就會依然是對於那個物件進行操作。

* 而這種選取取消但屬性依然指向那取消選取的物件問題，在處理上也非常容易，因為shift與左鍵按下一次後是指定選取，按第二次才是取消選取，所以在此只要對你要選的物件按一下就行了。

* 但shift與左鍵選取時，很容易會直接點到相近的物件，而不會被視為第二次點選，這部份也請注意。

<center>
    <img src="./source/ch3/0130.png">
    <div>對此按下右鍵，選擇複製到全部</div><br>
</center>

<center>
    <img src="./source/ch3/0140.png">
    <div>這時角度已調整完成，接著要去處理的是圖層分層的問題</div><br>
</center>

* 這時我們按下右鍵複製到全部時，blender會將物件屬性中的我們右鍵的參數資料，複製到左側場景中，我們所選的部份。

* 當然，除了選取物件編輯屬性，再複製到其他所選的物件的方法外，其實你也能透過選取物件，並透過同時按下ctrl與l去連接物件的屬性資訊。

<center>
    <img src="./source/ch3/0150.png">
    <div>為了方便操作，在此我們先要調整攝影機位置(預設負12m)</div><br>
</center>

* 在此由於預設的-12m確實太遠了，所以在此我們可以選擇將物件放大，或是對於攝影機屬性參數做調整來拉近攝影機的距離，在此選擇後者來進行操作。

<center>
    <img src="./source/ch3/0160.png">
    <div>先按下數字鍵0到攝影機鏡頭畫面</div><br>
</center>

* 在此的數字0鍵，並非是指鍵盤上方的數字鍵，而是指鍵盤右側的數字鍵盤上的數字。

* 如果沒有右側數字鍵盤，請由**工具列**中點下**編輯**，並按下最下方的選項，這時會跳出一個Blender偏好設定的視窗，請由底下的**Keymap**取調整右側數字鍵盤的快捷鍵到我們想要的按鍵上。

<center>
    <img src="./source/ch3/0170.png">
    <div>再來對於攝影機的y軸位置或是焦距進行調整</div><br>
</center>

* 在此的教學上是直接改動y軸，但筆者還是對這兩者的差異進行說明。

* 我們可以理解成一個情境，我們是一個攝影師，我們在一個空曠的地點扛著一個攝影機，改動y軸就是我們扛著攝影機去靠近與遠離物件。

* 而改變攝影機參數，流程上是按下物件屬性中的攝影機，去調整鏡頭的類型、透視方式、焦長，其實這部份還是建議要對於有攝影有基本認知才行，而這部份轉成情境就是，你人不動，但你可以調整你的攝影機(好到幾乎市場上不存在的高級品)來拉近距離。

* 當然如果是調整攝影機參數部份，有兩個設定滿有趣的，所以在此特別介紹：
    * 透視法下的正視法：因為不會產生[透視](https://zh.wikipedia.org/wiki/%E9%80%8F%E8%A7%86%E5%8F%98%E5%BD%A2)，和長焦鏡頭一樣適合拍攝建築類的
    * 景深：有學過攝影或許就會知道，相機有對焦的功能(除非你都是用全自動模式進行拍攝)，因為個物體的距離不同，在我們拍攝時，對焦點的前後部份會模糊化，這就是所謂的景深，只要能善用好景深，畫面自然會變得更加完美，而景深的產生原理請回去讀國中自然課本，在此不加贅述，而在此我們能透過指定對焦距離或是對焦物件來設定景深。

<center>
    <img src="./source/ch3/0180.png">
    <div>然後對於x軸與z軸進行左右位置的微調，將物件顯示於正中央</div><br>
</center>

### 3.3. 重新調整svg物件位置

<center>
    <img src="./source/ch3/0190.png">
    <div>然後針對於對下層物件用shift連選</div><br>
</center>

* 這時，你會發現由於svg檔案會因為其SVG標準中，SVG檔案分層方式是依據各物件在XML標籤中的先後而決定其高度的，這也意謂著高度的概念無法直接被數值化，所以在解析上svg圖檔案都會黏在一起。

* 所以在此要手動去調整物件高度，讓檔案變成原本的樣子。

<center>
    <img src="./source/ch3/0200.png">
    <div>對於其中一物件的y軸進行設定，設定為0.001</div><br>
</center>

* 在此為了考量實際上不要讓物件分層的距離太遠，所以在此盡可能不要將距離設的太大，當然如果我們所有的物件等比放大到夠大時，那麼物件分層的距離也可以提高。

* 請注意，物件y軸的方向，匯入時svg物件是放在y軸=0的位置上，而網我們靠近的方向是負數值域的方向，-0.0001~可輸入的負數最大值。

* 反之，與我們越遠的方向，即正數值域的方向，即：0.0001~可輸入的正數最大值。

<center>
    <img src="./source/ch3/0210.png">
    <div>這時你會看到只有一個物件移動，在此對於y軸的部份按右鍵選下複製到全部</div><br>
</center>

<center>
    <img src="./source/ch3/0220.png">
    <div>我們就能看到物件以移動至最下層</div><br>
</center>

<center>
    <img src="./source/ch3/0230.png">
    <div>然後選擇第二底層的後方頭髮</div><br>
</center>

<center>
    <img src="./source/ch3/0240.png">
    <div>設定至第二底層(0.0009)</div><br>
</center>

<center>
    <img src="./source/ch3/0250.png">
    <div>一樣複製到全部所選</div><br>
</center>

<center>
    <img src="./source/ch3/0260.png">
    <div>然後選擇第三底層的主要身體</div><br>
</center>

<center>
    <img src="./source/ch3/0270.png">
    <div>同前面將其移動至第三底層(0.0008)</div><br>
</center>

<center>
    <img src="./source/ch3/0280.png">
    <div>選擇之前所畫了肢體邊界與陰影處</div><br>
</center>

<center>
    <img src="./source/ch3/0290.png">
    <div>再設為第四底層(0.0007)</div><br>
</center>

<center>
    <img src="./source/ch3/0300.png">
    <div>這時我們會發現我們的衣領部份還在上面，這時我們將其移動至2至3層之間</div><br>
</center>

<center>
    <img src="./source/ch3/0310.png">
    <div>然後移動至(0.00085)</div><br>
</center>

* 因為我們是是使用0.000X的位置去分層，即便突然發現任兩相近層要加入n層物件時，如：0.0009與0.0008兩層中間要加入新的一層物件，這時我們就只要任一挑一個位於0.0009至0.0008中間的任意數就行了。

<center>
    <img src="./source/ch3/0320.png">
    <div>在選擇內部衣服的底部物件</div><br>
</center>

<center>
    <img src="./source/ch3/0330.png">
    <div>在此複製至0.0006</div><br>
</center>

<center>
    <img src="./source/ch3/0340.png">
    <div>再選擇內部衣服主體</div><br>
</center>

<center>
    <img src="./source/ch3/0350.png">
    <div>在此複製至0.0005</div><br>
</center>

<center>
    <img src="./source/ch3/0360.png">
    <div>再選擇外部衣服</div><br>
</center>

<center>
    <img src="./source/ch3/0370.png">
    <div>在此調整至0.0004</div><br>
</center>

<center>
    <img src="./source/ch3/0380.png">
    <div>再選擇繩子</div><br>
</center>

<center>
    <img src="./source/ch3/0390.png">
    <div>在此調整至0.0003</div><br>
</center>

<center>
    <img src="./source/ch3/0400.png">
    <div>再選擇眼白，因為臉的陰影位置0.0007所以一切都要在比其小的基準層</div><br>
</center>

<center>
    <img src="./source/ch3/0410.png">
    <div>眼白移至0.00069</div><br>
</center>

<center>
    <img src="./source/ch3/0420.png">
    <div>睫毛與眉毛移至0.00068</div><br>
</center>

<center>
    <img src="./source/ch3/0430.png">
    <div>瞳孔底移至0.00067</div><br>
</center>

<center>
    <img src="./source/ch3/0440.png">
    <div>瞳孔上半陰影底移至0.00066</div><br>
</center>

<center>
    <img src="./source/ch3/0450.png">
    <div>瞳孔下半陰影底移至0.00065</div><br>
</center>

<center>
    <img src="./source/ch3/0460.png">
    <div>瞳孔移至0.00064</div><br>
</center>

<center>
    <img src="./source/ch3/0470.png">
    <div>瞳孔反光移至0.00063</div><br>
</center>

<center>
    <img src="./source/ch3/0480.png">
    <div>當然我們如果直接用選的會有些漏掉，在此建議是用右側的管理來進行分類並進行選取</div><br>
</center>

<center>
    <img src="./source/ch3/0490.png">
    <div>最後把翅膀放到最底下的0.002</div><br>
</center>

<center>
    <img src="./source/ch3/0500.png">
    <div>調整分層的部份就大致大公告成了</div><br>
</center>

<center>
    <img src="./source/ch3/0510.png">
    <div>當然請勿必再次確認各物件的位置並進行微調</div><br>
</center>

### 3.6. 其他常見問題與補充事項

#### 3.6.1. Inkscpae匯入漸層消失問題
雖然我們能在Inkscape中設定物件的漸層色彩，但由於在此將svg檔案匯入到blender時，我們的單一平面上的色彩會轉成材質球，而漸層色彩無法被轉成材質球，而使得物件變成亮白色。

這問題發生的主因除了SVG檔案上漸層描述無法被blender解析外，同時也是因為材質球上的色彩預設只能使用單一色彩，除了使用節點編輯製作漸層與使用貼圖外，基本上SVG漸層應該無法用預設的SVG匯入方式去處理。

#### 3.6.2. 匯入檔案貼圖節點未上色問題
* 有時我們在匯入SVG檔案時，有些節點即便從編輯模式去看，線是存在的，但沒有平面，這時有3種方式可以解決：
    1. 回到 Inkscape進行調整
    2. 使用編輯模式慢慢校正個點位置
    3. 使用編輯模式重新為此區域弄出個平面


#### 3.6.3. 匯入文字問題
基本上我們從Inkscpae弄的文字不論是中英文或是其他語言文字，到了Blender的SVG圖檔匯入時，字都會消失不見，原因應該也是資料無法被解析或是在解析上發生了錯誤，在此建議，文字先轉成路徑後，再匯入到Blender。

#### 3.6.4. 使用uv貼圖問題
* 在此使用UV貼圖的話，我反而比較建議去看參考資料中兩個UV貼圖教學文章的說明，寫的相對較細，流程大致如下：
    1. 點選指定物件
    2. 點下**屬性**下**Material properties**
    3. 打開使用節點的選項
    4. 律表上的編輯器類型改選**著色器編輯器**
    5. 由著色器編輯器畫面中點下**添加**->**紋理**->**影像紋理**
    6. 將影像紋理的色彩與alpha值連接至著色器Principled BSDF上的**基礎色彩**與**Alpha**
    7. 然後在影像紋理的節點上按下**開啟**
    8. 然後進行調整，除了預設的選項外，也可以去添加**輸入**->**紋理座標**和**向量**->**映射方法**
    9. 紋理座標**生成的**連接映射方法的**向量**
    10. 映射方法的**向量**連接影像紋理的**向量**

#### 3.6.5. 還原ctrl+z的問題
我們在使用Blender時會發我們有時按下，ctrl+z時東西沒有被還原的情況，但實際上你會發現你可能回到前一個選取的物件上，這就是因為Blender會將你的點選動作視為動作，所以還原也就還原你的點選。

注意，這部份後面還會再提到，該用法能用在一個很特別的地方。

#### 3.6.6. 視接口與物件顯示的問題
視接口，英文叫做[viewport](https://developer.mozilla.org/zh-TW/docs/Glossary/Viewport)，基本上就是我們在畫面中看到的東西。

而在此我們將右上角眼睛關掉時，我們雖然在編輯時看不到物件，但在render時，我們還是會看到被我們關掉的東西。

* 這問題的處理也滿簡單的，三個步驟完成：
    1. 先在場景選集按右鍵增加一個New Collection
    2. 將我們要隱藏的物件塞至那個New Collection中
    3. 再將那個New Collection的勾勾關掉，就完全隱藏了

### 3.7. 小結
Blender真的是一款很強大的3D動畫製作軟體，雖然說我想由我這邊應該很難看出來，但建議可以從Google上去搜尋Blneder的作品就能知道Blender的強大在哪裡了。

然而回到現實面，我們不得不承認，從Inkscape輸出的SVG匯入到Blender是個複雜流程，但到此我們已完成SVG匯入與基本的調整了。

## 4. Blender綁定骨架

### 4.1. 骨架是什麼
骨架，簡單來說就是骨頭，想想看如果人沒有骨頭的話，大概就是都趴在地上用爬的吧。

基本上人的肢體行動都是靠肌肉與骨頭去實現，而在Blender中就是靠著骨架來簡單實現。

### 4.2. 綁定骨架

<center>
    <img src="./source/ch4/0010.png">
    <div>接著開始要綁定骨架，在此先對於一些概念去進行說明</div><br>
</center>

<center>
    <img src="./source/ch4/0020.png">
    <div>先到線框的視接口查看各物件</div><br>
</center>

* 這時我們能看到的所有構築物件成所有三角型，但基本上是一片黑就是了。

<center>
    <img src="./source/ch4/0030.png">
    <div>首先先在場景選集中，按下右鍵</div><br>
</center>

<center>
    <img src="./source/ch4/0040.png">
    <div>然後按下Select Object的選項</div><br>
</center>

<center>
    <img src="./source/ch4/0050.png">
    <div>再按下物體轉換為網格的選項</div><br>
</center>

<center>
    <img src="./source/ch4/0060.png">
    <div>如果不滿意目前的三角網格方式，可以到編輯模式下進行修改</div><br>
</center>

<center>
    <img src="./source/ch4/0070.png">
    <div>在編輯模式下按下選取，再按下All，以選取全部該物件的點</div><br>
</center>

<center>
    <img src="./source/ch4/0080.png">
    <div>這時我們就能看到已選取物件所有的點</div><br>
</center>

<center>
    <img src="./source/ch4/0090.png">
    <div>在此為了考量除了Y軸轉動外，轉動Z軸或X軸時能不會因為三角而凹一塊，在此採用四角網格</div><br>
</center>

---

* 在此使用一個簡單的比較案例：
    <center>
        <img src="./source/other/A001_0010.png">
        <div>僅單一一次細分綁定骨架</div><br>
    </center>

    <center>
        <img src="./source/other/A001_0020.png">
        <div>僅單一一次細分在轉動時</div><br>
    </center>
        
    <center>
        <img src="./source/other/A001_0030.png">
        <div>多次細分(方形)綁定骨架</div><br>
    </center>

    <center>
        <img src="./source/other/A001_0040.png">
        <div>多次細分(方形)在轉動時</div><br>
    </center>

    * 細分一次的方形，在旋轉時，實際上只綁到上面兩塊，而上面兩塊會隨著骨架旋轉而拉動。
    
    * 而在多次細分後，我們的物件在旋轉上是被我們覆蓋的上方部份轉動外，也有在下方的區域受到影響而選轉。

    * 在此表現出兩個骨架重要的特性，骨架的區域覆蓋性：基本上骨架是會抓其綁定網格的覆蓋區域而轉動，覆蓋的越大，所能控制的範圍越大。
    
    * 但精緻操作上，要網格切的越細，才能夠產生更精緻的轉動，也許在此是看不太出來，但因為骨架要綁定網格，如果綁定的網格太少，甚至會在轉動上出問題。
---

<center>
    <img src="./source/ch4/0100.png">
    <div>這時我們就能看到一些能轉的三角網格，都變成四角網格了</div><br>
</center>

* 在此筆者使用四角網格的用意如下：
    * 必面過多不規則三角面影響綁定的骨架
    * 若要做x軸或z軸旋轉時，四角面造成的彎曲會比三角面好一點

<center>
    <img src="./source/ch4/0110.png">
    <div>同時我們也要對其再細分</div><br>
</center>

* 細分的用途就是增加網格在實際轉動時的精細程度，否則手腳四肢關節在旋轉上無法保證旋轉時會如我們所想的去旋轉。

---

* 除了細分外，在此也有提供取消細分的功能，在此以三角網格為案例說明取消細分：

    <center>
        <img src="./source/other/A002_0010.png">
        <div>如果覺得預設幫你判斷的三角網格點太多，要減少的話，能按下邊線取消細分</div><br>
    </center>

    <center>
        <img src="./source/other/A002_0020.png">
        <div>我們就能看到點變少了</div><br>
    </center>

    * 我們能看到取消細分時三角網格點數量就會減少，但細分與取消細分不是像還原與重複一樣的進行處理，而是取消細分後再按下細分，會得到與一開始不同的結果。

    * 基本上取消細分，就是盡可能維持原本的樣子，但讓網格數減少，而細分則是對於既有的網格去切。
---

<center>
    <img src="./source/ch4/0120.png">
    <div>這時我們就能看到細分的各網格點</div><br>
</center>

<center>
    <img src="./source/ch4/0130.png">
    <div>然後我們再回到物體模式</div><br>
</center>

<center>
    <img src="./source/ch4/0140.png">
    <div>然後再回到原本的視接口，準備綁骨架</div><br>
</center>

<center>
    <img src="./source/ch4/0150.png">
    <div>在此我們先按下右上方的選擇，按下骨架，再按下Single Bone</div><br>
</center>

<center>
    <img src="./source/ch4/0160.png">
    <div>然後你就會看到一個大到超出你螢幕的骨架出現在你面前 骨架(Bone)</div><br>
</center>

* 沒錯，預設的骨架大小就是這麼大一根，所以我們要縮小骨架的大小，到我們要綁定的網格上。

<center>
    <img src="./source/ch4/0170.png">
    <div>在調整骨架時，我們先選取骨架，再按下Object Proterties</div><br>
</center>

<center>
    <img src="./source/ch4/0180.png">
    <div>然後按下所有的縮放控制欄位(一次按拉)</div><br>
</center>

* 一次拉下來縮放X、Y、Z的三個按鍵，由X向下按住輸入格，拉到Z的輸入格這時就能一次更改三個方向的縮放大小。

<center>
    <img src="./source/ch4/0190.png">
    <div>將縮放調整至0.04</div><br>
</center>


* 請注意縮放的大小會和綁定網格的覆蓋率有所關聯，請確保該骨架要和網格在同一平面，且骨架得要能覆蓋到網格上，最好是骨架完全覆蓋過物件上的網格為前提。

<center>
    <img src="./source/ch4/0200.png">
    <div>然後按下旋轉</div><br>
</center>

* 請切記，如果不是直接用參數控制的方式進行旋轉而是要手動旋轉，一定要再按下數字鍵盤上的數字0鍵，進入攝影機鏡頭模式時，去做旋轉，不然在3D模式下旋轉，很容易出現轉到X軸與Z軸發生一些方向歪掉的情形，尤其是等會的延伸骨架的部份。

<center>
    <img src="./source/ch4/0210.png">
    <div>我們只對Y軸綠色的框進行旋轉</div><br>
</center>

<center>
    <img src="./source/ch4/0220.png">
    <div>首先我們先做出左手骨架，將骨架放置對應關節開始位置附近</div><br>
</center>

* 在此請確保，骨架的底(定位點)，得要在我們當時使用Inkscape上測試旋轉的旋轉定位點。

<center>
    <img src="./source/ch4/0230.png">
    <div>選取骨架後，進入編輯模式</div><br>
</center>

<center>
    <img src="./source/ch4/0240.png">
    <div>在此的編輯模式與物件的編輯模式不同，是針對於骨架的編輯</div><br>
</center>

<center>
    <img src="./source/ch4/0250.png">
    <div>按住你要的開始點</div><br>
</center>

* 去造出延伸骨架的位置有：底部的點延伸、中間的骨架處前後一併延伸、頂部的點延伸的方式，基本上先點一下位置就能選擇。

<center>
    <img src="./source/ch4/0260.png">
    <div>按E拉出延伸骨架</div><br>
</center>

* 如果拉出延伸骨架時，真的建議要在在按下數字鍵盤的數字0鍵的攝影機模式下執行，因為在此的拉伸是由開始點拉到你的滑鼠點，所以也因為如此會**很容易**使得出現非純Y軸旋轉的情形發生。

<center>
    <img src="./source/ch4/0270.png">
    <div>拉好延伸骨架</div><br>
</center>

---
* 在此針對於骨架的綁法舉一個例子，以兩個以四角網格的矩形物件當作手臂而言：
    
    <center>
        <img src="./source/other/A003_0010.png">
        <div>在此我們先準備細分的長方體作為物件</div><br>
    </center>
    
    <center>
        <img src="./source/other/A003_0020.png">
        <div>使用二骨架作為骨頭時，物件因為綁定的拉扯而有過度扭曲</div><br>
    </center>

    <center>
        <img src="./source/other/A003_0030.png">
        <div>使用三骨架作為骨頭時，因為有一骨頭被視為關節，物件因為關節作為緩衝而能減少扭曲</div><br>
    </center>

    <center>
        <img src="./source/other/A003_0040.png">
        <div>關掉骨架的檢視後我們能看到明顯的彎曲情況</div><br>
    </center>

    <center>
        <img src="./source/other/A003_0050.png">
        <div>關掉骨架的檢視後我們能看到明顯的彎曲情況(2)</div><br>
    </center>

    <center>
        <img src="./source/other/A003_0060.png">
        <div>由視接口能看到實際上四角網格是如何被骨架所影響的</div><br>
    </center>

    <center>
        <img src="./source/other/A003_0070.png">
        <div>由視接口能看到實際上四角網格是如何被骨架所影響的(2)</div><br>
    </center>

    * 在此我們可以知道，因為我們的肢體是平面，所以在旋轉上直接轉會因為骨架的權重干涉，而出現不合理的彎曲。

    * 而如果我們增加了一個關節用的骨架，該骨架將成為兩個骨架的緩衝，而讓我們在旋轉時，能透過旋轉關節骨架與末端骨架去以避免因為骨架權重而產生不符合肢體行為的扭曲發生。
---

<center>
    <img src="./source/ch4/0280.png">
    <div>然後回到物體模式</div><br>
</center>

<center>
    <img src="./source/ch4/0290.png">
    <div>先用shift連選骨架要綁的物件</div><br>
</center>

<center>
    <img src="./source/ch4/0300.png">
    <div>最後再shift連選到骨架</div><br>
</center>

* 請注意，骨架一定要最後選

<center>
    <img src="./source/ch4/0310.png">
    <div>按下右鍵，選親子，按下使用封裝權重</div><br>
</center>

<center>
    <img src="./source/ch4/0320.png">
    <div>這時你會看到一條虛線</div><br>
</center>

<center>
    <img src="./source/ch4/0330.png">
    <div>單選骨架，再到姿勢模式下</div><br>
</center>

<center>
    <img src="./source/ch4/0340.png">
    <div>為了方便測試選擇最上方的初始骨架</div><br>
</center>

<center>
    <img src="./source/ch4/0350.png">
    <div>我們先轉一下Y軸骨架如果沒有任何一塊網格因為沒有綁定而不動，那恭喜成功了</div><br>
</center>

---
* 而在此舉兩個沒有綁定到的情況，第一種是當你是給路徑而不是骨架，會造成無法綁定：
    <center>
        <img src="./source/other/A004_0010.png">
        <div>如果物件還是path去綁骨架，雖然在物體模式下能轉動</div><br>
    </center>

    <center>
        <img src="./source/other/A004_0020.png">
        <div>但在姿勢模式下是無法轉動的，所以請務必將path轉成網格</div><br>
    </center>

    * 在此，只要ctrl+z還原到封裝前，重新將路徑轉成骨架後，重新封裝一次。

    * 如果無法用ctrl+z還原回去，請在物體模式對骨架按一下右鍵後，選擇**親子**->**清除親代並保持變換**，這樣也能解除封裝。

* 另一種則是骨架未封裝完全，看起來向是有東西黏住一樣的失敗奘況：
    <center>
        <img src="./source/other/A005_0010.png">
        <div>若骨架沒有綁定好會發生這類的狀況</div><br>
    </center>

    <center>
        <img src="./source/other/A005_0020.png">
        <div>調整至每一個四角區域都被覆蓋</div><br>
    </center>
    
    * 這時也是要還原到封裝前，由編輯模式下，去拉動我們的骨架，像是縮放、偏移等方式來完成骨架的封裝。
---

<center>
    <img src="./source/ch4/0360.png">
    <div>測試完後ctrl z進行還原至旋轉前的位置</div><br>
</center>

<center>
    <img src="./source/ch4/0370.png">
    <div>回到物體模式繼續綁其他部份的骨架</div><br>
</center>

<center>
    <img src="./source/ch4/0380.png">
    <div>但為了方便管理，在此對骨架物件改名</div><br>
</center>

<center>
    <img src="./source/ch4/0390.png">
    <div>在此將左手上的骨架命名為RightHand</div><br>
</center>

<center>
    <img src="./source/ch4/0400.png">
    <div>用同樣方式完成右手</div><br>
</center>

<center>
    <img src="./source/ch4/0410.png">
    <div>用同樣方式完成左腳</div><br>
</center>

<center>
    <img src="./source/ch4/0420.png">
    <div>用同樣方式完成右腳</div><br>
</center>

<center>
    <img src="./source/ch4/0430.png">
    <div>然後對於身體的部份也要進行骨架綁定</div><br>
</center>

<center>
    <img src="./source/ch4/0440.png">
    <div>用同樣方式完成身體內部</div><br>
</center>

<center>
    <img src="./source/ch4/0450.png">
    <div>再來是對於外部的衣服死物件進行骨架綁定，在此因為要考慮是布料飾品而不是肢體而有所變化</div><br>
</center>

<center>
    <img src="./source/ch4/0460.png">
    <div>先關掉會擋住我們操作的body視接口</div><br>
</center>

<center>
    <img src="./source/ch4/0470.png">
    <div>這樣能比較容易去進行操作</div><br>
</center>

<center>
    <img src="./source/ch4/0480.png">
    <div>首先是繩子(1)</div><br>
</center>

<center>
    <img src="./source/ch4/0490.png">
    <div>由於一次對於所有的繩子做操作會黏在一起，所以一個個處理</div><br>
</center>

<center>
    <img src="./source/ch4/0500.png">
    <div>完成繩子(2)</div><br>
</center>

<center>
    <img src="./source/ch4/0510.png">
    <div>完成繩子(3)</div><br>
</center>

<center>
    <img src="./source/ch4/0520.png">
    <div>完成繩子(4)</div><br>
</center>

<center>
    <img src="./source/ch4/0530.png">
    <div>再來對衣物進行骨架綁定</div><br>
</center>

<center>
    <img src="./source/ch4/0540.png">
    <div>由於骨架太大會使得要選的物件會被擋住，為此先將是接口骨架的顯示關閉</div><br>
</center>

<center>
    <img src="./source/ch4/0550.png">
    <div>這時我們就看不到所有的骨架了</div><br>
</center>

<center>
    <img src="./source/ch4/0560.png">
    <div>先選取物件</div><br>
</center>

<center>
    <img src="./source/ch4/0570.png">
    <div>再由視接口顯示骨架</div><br>
</center>

<center>
    <img src="./source/ch4/0580.png">
    <div>再選取骨架</div><br>
</center>

<center>
    <img src="./source/ch4/0590.png">
    <div>完成衣物本體的骨架綁定</div><br>
</center>

<center>
    <img src="./source/ch4/0600.png">
    <div>開始去綁翅膀</div><br>
</center>

<center>
    <img src="./source/ch4/0610.png">
    <div>完成翅膀1</div><br>
</center>

<center>
    <img src="./source/ch4/0620.png">
    <div>完成翅膀2</div><br>
</center>

<center>
    <img src="./source/ch4/0630.png">
    <div>完成翅膀3</div><br>
</center>

<center>
    <img src="./source/ch4/0640.png">
    <div>完成翅膀4</div><br>
</center>

<center>
    <img src="./source/ch4/0650.png">
    <div>完成翅膀5</div><br>
</center>

<center>
    <img src="./source/ch4/0660.png">
    <div>完成翅膀6</div><br>
</center>

<center>
    <img src="./source/ch4/0670.png">
    <div>身體的骨架綁好後，接著要去處理頭部(含脖子的部份)</div><br>
</center>

<center>
    <img src="./source/ch4/0680.png">
    <div>首先我們先去處理緞帶</div><br>
</center>

<center>
    <img src="./source/ch4/0690.png">
    <div>為了讓動緞帶時，能有動的效果，在此則一個個去綁</div><br>
</center>

<center>
    <img src="./source/ch4/0700.png">
    <div>完成緞帶(六個骨架)</div><br>
</center>

<center>
    <img src="./source/ch4/0710.png">
    <div>再來是要對頭部(含頭髮底部)與頸部進行骨架綁定</div><br>
</center>

<center>
    <img src="./source/ch4/0720.png">
    <div>完成頭部底部</div><br>
</center>

<center>
    <img src="./source/ch4/0730.png">
    <div>再來是要對頭部瀏海去進行綁定，這部份非常繁瑣</div><br>
</center>

<center>
    <img src="./source/ch4/0740.png">
    <div>請注意頭髮的綁定部份都得要被覆蓋</div><br>
</center>

<center>
    <img src="./source/ch4/0750.png">
    <div>綁好第一塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0760.png">
    <div>綁好第二塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0770.png">
    <div>綁好第三塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0780.png">
    <div>綁好第四塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0790.png">
    <div>綁好第五塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0800.png">
    <div>綁好第六塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0810.png">
    <div>綁好第七塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0820.png">
    <div>綁好第八塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0830.png">
    <div>綁好第九塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0840.png">
    <div>綁好第十塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0850.png">
    <div>綁好第十一塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0860.png">
    <div>綁好第十二塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0870.png">
    <div>綁好第十三塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0880.png">
    <div>綁好第十四塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0890.png">
    <div>綁好第十五塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0900.png">
    <div>綁好第十六塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0910.png">
    <div>綁好第十七塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0920.png">
    <div>經歷千辛萬苦後終於綁好，接著要處理後面的頭髮了</div><br>
</center>

<center>
    <img src="./source/ch4/0930.png">
    <div>總共要處理十三根QAO</div><br>
</center>

<center>
    <img src="./source/ch4/0940.png">
    <div>綁好背面第一塊頭髮</div><br>
</center>
<center>
    <img src="./source/ch4/0950.png">
    <div>綁好背面第二塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0960.png">
    <div>綁好背面第三塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0970.png">
    <div>綁好背面第四塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0980.png">
    <div>綁好背面第五塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/0990.png">
    <div>綁好背面第六塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1000.png">
    <div>綁好背面第七塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1010.png">
    <div>綁好背面第八塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1020.png">
    <div>綁好背面第九塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1030.png">
    <div>綁好背面第十塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1040.png">
    <div>綁好背面第十一塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1050.png">
    <div>綁好背面第十二塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1060.png">
    <div>綁好背面第十三塊頭髮</div><br>
</center>

<center>
    <img src="./source/ch4/1070.png">
    <div>終於綁好背面頭髮了(哭)</div><br>
</center>

### 4.3. 各元件重新命名整理
```
Body：底部身體物件與四肢連接處的邊框與其骨架
c：服裝，白色部份與藍色部份與其骨架
f1：左上翅膀與其骨架
f2：左中翅膀與其骨架
f3：左下翅膀與其骨架
f4：右上翅膀與其骨架
f5：右中翅膀與其骨架
f6：右下翅膀與其骨架
hear：頭部與其骨架
hearB1：由右邊數來的第1個後方頭髮與其骨架
hearB2：由右邊數來的第2個後方頭髮與其骨架
hearB3：由右邊數來的第3個後方頭髮與其骨架
hearB4：由右邊數來的第4個後方頭髮與其骨架
hearB5：由右邊數來的第5個後方頭髮與其骨架
hearB6：由右邊數來的第6個後方頭髮與其骨架
hearB7：由右邊數來的第7個後方頭髮與其骨架
hearB8：由右邊數來的第8個後方頭髮與其骨架
hearB9：由右邊數來的第9個後方頭髮與其骨架
hearBA：由右邊數來的第10個後方頭髮與其骨架
hearBB：由右邊數來的第11個後方頭髮與其骨架
hearBC：由右邊數來的第12個後方頭髮與其骨架
hearBD：由右邊數來的第13個後方頭髮與其骨架
hearF1：由右邊數來的第1個後方頭髮與其骨架
hearF2：由右邊數來的第2個後方頭髮與其骨架
hearF3：由右邊數來的第3個後方頭髮與其骨架
hearF4：由右邊數來的第4個後方頭髮與其骨架
hearF5：由右邊數來的第5個後方頭髮與其骨架
hearF6：由右邊數來的第6個後方頭髮與其骨架
hearF7：由右邊數來的第7個後方頭髮與其骨架
hearF8：由右邊數來的第8個後方頭髮與其骨架
hearF9：由右邊數來的第9個後方頭髮與其骨架
hearFA：由右邊數來的第10個後方頭髮與其骨架
hearFB：由右邊數來的第11個後方頭髮與其骨架
hearFC：由右邊數來的第12個後方頭髮與其骨架
hearFD：由右邊數來的第13個後方頭髮與其骨架
hearFE：由右邊數來的第14個後方頭髮與其骨架
hearFF：由右邊數來的第15個後方頭髮與其骨架
hearFG：由右邊數來的第16個後方頭髮與其骨架
hearFH：由右邊數來的第17個後方頭髮與其骨架
LeftHand：左邊手臂與其骨架
LeftLeg：左邊的腳與其骨架
RightHand：右邊手臂與其骨架
RightLeg：右邊的腳與其骨架
s1：左上到右下的蝴蝶結直線與其骨架
s2：右上到左下的蝴蝶結直線與其骨架
s3：左邊的蝴蝶結兔耳朵與其骨架
s4：右邊的蝴蝶結兔耳朵與其骨架
sh1：頭上的緞帶左邊上方與其骨架
sh2：頭上的緞帶左邊中間與其骨架
sh3：頭上的緞帶左邊下方與其骨架
sh4：頭上的緞帶右邊上方與其骨架
sh5：頭上的緞帶右邊中間與其骨架
sh6：頭上的緞帶右邊下方與其骨架
path-***：臉部網格物件，在此先不對此綁骨架(其實是忘了)
```

### 4.4. 其他常見問題與補充事項

#### 4.4.1. 如果不綁骨架的話會如何？
如果不綁骨架的話，雖然有些東西還是能做出來，但在後續處理上會比較麻煩。

我們在做姿勢與運動時，比較不好調整與還原，因為直接變動物體動作時，你得要讓定位點重新調到你的指定位置後，控制物體旋轉，且你的角色動作記憶只能記在律表上，同時也因為律表上的紀錄方式，有些時後動到一點東西其他的姿勢也受到影響。

#### 4.4.2 節點數與骨架綁定的抉擇
當我們網格數過多時，綁定上不容易，但實際上用多骨架時能在姿勢旋轉時，讓肢體的選轉轉的很好，但付出的代價是，多網格多運算時間，同時封裝綁定上，要多做調整。

### 4.5. 小結
Blender骨架的綁定是一個學問，其實在此講到的也只是最基本的綁法，實際上還能用鏡像的方式進行處左右骨架的綁定。

## 5. 製作姿勢庫與簡單動畫

### 5.1. 姿勢庫與其用途
首先我們先來討論姿勢庫是什麼？姿勢庫，顧名思義就是儲存姿勢的函式庫，我們能將姿勢儲存於此。

那為什麼要用姿勢庫呢？原因很簡單，如果我們在單一一個人物檔案中，直接用律表上的自動幀來錄製動作，到時搬移到其他檔案時，如果要做一個簡單平移時，那動作就會亂掉，所以使用姿勢庫是相對安全的作法。

### 5.2. 使用物體模式與姿勢模式的差異
物體模式就是存物體的位置與資訊，其定位點預設會在svg檔的左下角，一開始對齊(0,0,0)位址的點最為定位點，所以在未綁定骨架前旋轉物體時，你應該是會隨著這個點轉。

而綁定骨架後，你由物體模式轉骨架，只是對骨架的物體去轉，而不是用姿勢去轉，只要給一個簡單的平移或是旋轉之需求就有機會讓動畫中的姿勢爆掉。

### 5.3. 建立一個姿勢庫與動畫

#### 5.3.2. 備份一個物件
<center>
    <img src="./source/ch5/0010.png">
    <div>接著開始做動作，先到選集的物件上按下右鍵</div><br>
</center>

<center>
    <img src="./source/ch5/0020.png">
    <div>再按下select object</div><br>
</center>

<center>
    <img src="./source/ch5/0030.png">
    <div>在物體模式下按下copy object</div><br>
</center>

<center>
    <img src="./source/ch5/0040.png">
    <div>建立一個new collection</div><br>
</center>

<center>
    <img src="./source/ch5/0050.png">
    <div>點一下new collection</div><br>
</center>

<center>
    <img src="./source/ch5/0060.png">
    <div>然後貼上</div><br>
</center>

<center>
    <img src="./source/ch5/0070.png">
    <div>重新命名為原名的backup</div><br>
</center>

<center>
    <img src="./source/ch5/0080.png">
    <div>取消物件在視接口上的顯示</div><br>
</center>

#### 5.3.3. 建立飛行姿勢
<center>
    <img src="./source/ch5/0090.png">
    <div>然後回到姿式模式</div><br>
</center>

<center>
    <img src="./source/ch5/0100.png">
    <div>律表選擇動作編輯器</div><br>
</center>

<center>
    <img src="./source/ch5/0110.png">
    <div>回到物件模式選擇所有翅膀物件</div><br>
</center>

<center>
    <img src="./source/ch5/0120.png">
    <div>進入姿勢模式按下object data properties</div><br>
</center>

<center>
    <img src="./source/ch5/0130.png">
    <div>按下姿勢庫(我們先做個簡單的翅膀拍動的動作)</div><br>
</center>

<center>
    <img src="./source/ch5/0140.png">
    <div>按下新增</div><br>
</center>

<center>
    <img src="./source/ch5/0150.png">
    <div>添加姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0160.png">
    <div>添加新的</div><br>
</center>

<center>
    <img src="./source/ch5/0170.png">
    <div>只要按下此按鍵骨架就會套用成我們指定的姿式</div><br>
</center>

<center>
    <img src="./source/ch5/0180.png">
    <div>請注意我們目前只對f1做操作，所以我們先點一下f1的骨架</div><br>
</center>

<center>
    <img src="./source/ch5/0190.png">
    <div>旋轉一下</div><br>
</center>

<center>
    <img src="./source/ch5/0200.png">
    <div>同樣也是進行新增</div><br>
</center>

<center>
    <img src="./source/ch5/0210.png">
    <div>這時我們打開自動鍵處理</div><br>
</center>

<center>
    <img src="./source/ch5/0220.png">
    <div>對於第0幀套用Pose</div><br>
</center>

* 在此直接在新增姿勢庫時，一併製作簡單的飛行動畫。

<center>
    <img src="./source/ch5/0230.png">
    <div>這時你就會看到第0幀真的變成Pose了</div><br>
</center>

<center>
    <img src="./source/ch5/0240.png">
    <div>對於第20幀套用Pose.001</div><br>
</center>

<center>
    <img src="./source/ch5/0250.png">
    <div>對於第40幀套用Pose</div><br>
</center>

<center>
    <img src="./source/ch5/0260.png">
    <div>為了方便顯示我們將結束時間暫時設定在40幀</div><br>
</center>

<center>
    <img src="./source/ch5/0270.png">
    <div>按下播放</div><br>
</center>

<center>
    <img src="./source/ch5/0280.png">
    <div>為了方便檢示我先使用eevee(預設)模擬輸出的視接口與關閉骨架顯示</div><br>
</center>

<center>
    <img src="./source/ch5/0290.png">
    <div>為了方便管理在此對於姿勢庫與姿勢重新命名</div><br>
</center>

* 在此命名方式為：
    * basePose：一般姿勢。
    * flyPose：飛行姿勢。

* 也就是要做成飛行動作的話，就是：
    ```
    basePose -> flyPose -> basePose -> (循環)
    ```

* 也就是對應幀率：
    ```
    0幀～20幀（basePose -> flyPose）：  
        揮動翅膀，向下使力，拍動。

    20幀～40幀（flyPose -> basePose）：  
        收回翅膀的揮動，向上拉回，即前一動作的反向。
    ```

<center>
    <img src="./source/ch5/0300.png">
    <div>我們點選f2物件繼續進行一樣的操作</div><br>
</center>

<center>
    <img src="./source/ch5/0310.png">
    <div>然後是f3物件</div><br>
</center>

<center>
    <img src="./source/ch5/0320.png">
    <div>然後是f4物件</div><br>
</center>

<center>
    <img src="./source/ch5/0330.png">
    <div>然後是f5物件</div><br>
</center>

<center>
    <img src="./source/ch5/0340.png">
    <div>然後是f6物件(在此以此來當作開著自動鍵處理時的範例)</div><br>
</center>

<center>
    <img src="./source/ch5/0350.png">
    <div>一樣按下新增</div><br>
</center>

<center>
    <img src="./source/ch5/0360.png">
    <div>一樣建立初始姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0370.png">
    <div>直接套用姿勢至第0幀</div><br>
</center>

<center>
    <img src="./source/ch5/0380.png">
    <div>滑鼠點第20幀</div><br>
</center>

<center>
    <img src="./source/ch5/0390.png">
    <div>轉一下翅膀</div><br>
</center>

<center>
    <img src="./source/ch5/0400.png">
    <div>新增至姿勢庫</div><br>
</center>

<center>
    <img src="./source/ch5/0410.png">
    <div>滑鼠點第40幀</div><br>
</center>

<center>
    <img src="./source/ch5/0420.png">
    <div>滑鼠點一下basePose</div><br>
</center>

<center>
    <img src="./source/ch5/0430.png">
    <div>然後再套用此姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0440.png">
    <div>這樣就能快速完成姿勢動畫</div><br>
</center>

<center>
    <img src="./source/ch5/0450.png">
    <div>我們就能看到會動的翅膀了</div><br>
</center>

<center>
    <img src="./source/ch5/0460.png">
    <div>同樣為了方便檢示我先使用eevee(預設)模擬輸出的視接口與關閉骨架顯示</div><br>
</center>

<center>
    <img src="./source/ch5/0470.png">
    <div>這時我們先回到物體模式(我們接著要對手腳做動作)</div><br>
</center>

<center>
    <img src="./source/ch5/0480.png">
    <div>先關閉已經完成的翅膀的視接口顯示</div><br>
</center>

<center>
    <img src="./source/ch5/0490.png">
    <div>先選擇手腳</div><br>
</center>

<center>
    <img src="./source/ch5/0500.png">
    <div>進入姿勢模式</div><br>
</center>

<center>
    <img src="./source/ch5/0510.png">
    <div>我們就要對四肢骨架進行姿勢的處理</div><br>
</center>

<center>
    <img src="./source/ch5/0520.png">
    <div>我們先從右手開始</div><br>
</center>

<center>
    <img src="./source/ch5/0530.png">
    <div>一樣建立姿勢庫的姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0540.png">
    <div>請切記骨架關聯中延伸段是會跟個動，但不會被一併指定成關鍵幀</div><br>
</center>

<center>
    <img src="./source/ch5/0550.png">
    <div>如果要一併指定的話，請將此部份的延伸關節一併選取，並套用動作以新增至關鍵幀</div><br>
</center>

<center>
    <img src="./source/ch5/0560.png">
    <div>一樣移至於第20幀，設定完整體右手動作後，並添加至姿勢庫</div><br>
</center>

<center>
    <img src="./source/ch5/0570.png">
    <div>一樣移至於第40幀，套用姿勢庫中的basePose</div><br>
</center>

<center>
    <img src="./source/ch5/0580.png">
    <div>右手完成</div><br>
</center>

<center>
    <img src="./source/ch5/0590.png">
    <div>右手飛行動作完成(無骨架與輸出視接口顯示)</div><br>
</center>

<center>
    <img src="./source/ch5/0600.png">
    <div>我們再建立一個舉手的姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0610.png">
    <div>記得舉手的動作，自己試一次時關節運動來說，是手臂先再手腕(所以會有順序)</div><br>
</center>

<center>
    <img src="./source/ch5/0620.png">
    <div>當然還是得要先建出姿勢，但這時我們發現手和身體間出現了縫隙</div><br>
</center>

<center>
    <img src="./source/ch5/0630.png">
    <div>這時我們要再姿勢模式下做移動(千萬不要再物體模式下)</div><br>
</center>

<center>
    <img src="./source/ch5/0640.png">
    <div>拉到能遮住的位置結束</div><br>
</center>

<center>
    <img src="./source/ch5/0650.png">
    <div>用符合人體工學的方式轉動骨架位置</div><br>
</center>

<center>
    <img src="./source/ch5/0660.png">
    <div>完成舉手的姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0670.png">
    <div>全選後加入姿勢庫</div><br>
</center>

<center>
    <img src="./source/ch5/0680.png">
    <div>命名Pose為bagaPose(バガ)</div><br>
</center>

<center>
    <img src="./source/ch5/0690.png">
    <div>然後先清除第60幀的鍵幀</div><br>
</center>

<center>
    <img src="./source/ch5/0700.png">
    <div>這時我們能看到動作因為清除第60幀而變成第40幀</div><br>
</center>

<center>
    <img src="./source/ch5/0710.png">
    <div>移動至第50幀，並選擇上半段的骨架套用姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0720.png">
    <div>移動至第60幀，並選擇下半段的骨架套用姿勢</div><br>
</center>

<center>
    <img src="./source/ch5/0730.png">
    <div>我們將結束時間調至80幀以方便檢視</div><br>
</center>

<center>
    <img src="./source/ch5/0740.png">
    <div>因為速度太快，所以要進行調整，我們能直接去拉動關鍵幀去調整位置(50->60且60->80)</div><br>
</center>

<center>
    <img src="./source/ch5/0750.png">
    <div>這時我們就能看到飛行加上舉手的動畫了</div><br>
</center>

<center>
    <img src="./source/ch5/0760.png">
    <div>然後用同樣的方式處理左手</div><br>
</center>

<center>
    <img src="./source/ch5/0770.png">
    <div>我們這時就能看到雙手舉手的動畫畫面了</div><br>
</center>

<center>
    <img src="./source/ch5/0780.png">
    <div>然後同樣的方式去處理右腳</div><br>
</center>

<center>
    <img src="./source/ch5/0790.png">
    <div>然後同樣的方式去處理左腳</div><br>
</center>

<center>
    <img src="./source/ch5/0800.png">
    <div>這時我們就完成了一個飛行的動作了(大概)</div><br>
</center>

<center>
    <img src="./source/ch5/0810.png">
    <div>當然只讓身體動也是不夠的，其實也要對衣服進行動畫的設計</div><br>
</center>

<center>
    <img src="./source/ch5/0820.png">
    <div>一樣是關閉肢體的骨架視接口後，選擇衣服與身體的骨架後到姿勢模式</div><br>
</center>

<center>
    <img src="./source/ch5/0830.png">
    <div>由於選擇身體骨架的目的是在衣服移動時不要破圖，所以可以暫時關起來</div><br>
</center>

<center>
    <img src="./source/ch5/0840.png">
    <div>請記得因為骨架的連接會造成連鎖效應，所以請確實拉動適當骨架位置</div><br>
</center>

<center>
    <img src="./source/ch5/0850.png">
    <div>衣服也跟著動了</div><br>
</center>

* 在此由於所有的東西不可能是同時動的，所以像是服飾、頭髮等物件都可以微調幾個幀率位置。

<center>
    <img src="./source/ch5/0860.png">
    <div>衣服動了，那領帶也要動，這時我們先關掉剛才的衣服身體的骨架</div><br>
</center>

<center>
    <img src="./source/ch5/0870.png">
    <div>選擇領帶進入姿勢模式</div><br>
</center>

<center>
    <img src="./source/ch5/0880.png">
    <div>請切記領帶這邊也是4個物件駔合而成的，所以也要弄4個姿勢庫</div><br>
</center>

<center>
    <img src="./source/ch5/0890.png">
    <div>完成s1</div><br>
</center>

<center>
    <img src="./source/ch5/0900.png">
    <div>完成s2</div><br>
</center>

<center>
    <img src="./source/ch5/0910.png">
    <div>完成s3</div><br>
</center>

<center>
    <img src="./source/ch5/0920.png">
    <div>完成s4</div><br>
</center>

<center>
    <img src="./source/ch5/0930.png">
    <div>回到物體模式，接著要調整頭髮，在那之前先把頭髮的視接口關了</div><br>
</center>

<center>
    <img src="./source/ch5/0940.png">
    <div>我們先對後面的頭髮做調整，所以需要先把其他會擋到操作的物件關掉</div><br>
</center>

<center>
    <img src="./source/ch5/0950.png">
    <div>一樣是進入姿勢模式</div><br>
</center>

<center>
    <img src="./source/ch5/0960.png">
    <div>在此一樣是對於一塊塊頭髮進行姿勢設定</div><br>
</center>

<center>
    <img src="./source/ch5/0970.png">
    <div>完成hearB1</div><br>
</center>

<center>
    <img src="./source/ch5/0980.png">
    <div>完成hearB2</div><br>
</center>

<center>
    <img src="./source/ch5/0990.png">
    <div>完成hearB3</div><br>
</center>

<center>
    <img src="./source/ch5/1000.png">
    <div>完成hearB4</div><br>
</center>

<center>
    <img src="./source/ch5/1010.png">
    <div>完成hearB5</div><br>
</center>

<center>
    <img src="./source/ch5/1020.png">
    <div>完成hearB6</div><br>
</center>

<center>
    <img src="./source/ch5/1030.png">
    <div>由於左右是成對的，所以在此先對於hearBD物件先進行操作</div><br>
</center>

<center>
    <img src="./source/ch5/1040.png">
    <div>完成hearBD</div><br>
</center>

<center>
    <img src="./source/ch5/1050.png">
    <div>完成hearBC</div><br>
</center>

<center>
    <img src="./source/ch5/1060.png">
    <div>完成hearBB</div><br>
</center>

<center>
    <img src="./source/ch5/1070.png">
    <div>完成hearBA</div><br>
</center>

<center>
    <img src="./source/ch5/1080.png">
    <div>完成hearB9</div><br>
</center>

<center>
    <img src="./source/ch5/1090.png">
    <div>完成hearB8</div><br>
</center>

<center>
    <img src="./source/ch5/1100.png">
    <div>完成hearB7</div><br>
</center>

<center>
    <img src="./source/ch5/1110.png">
    <div>效果看起來不錯</div><br>
</center>

<center>
    <img src="./source/ch5/1120.png">
    <div>然後回到物體模式，關閉後方頭髮骨架，並顯示前方瀏海的骨架</div><br>
</center>

<center>
    <img src="./source/ch5/1130.png">
    <div>同樣也是進入姿勢模式</div><br>
</center>

<center>
    <img src="./source/ch5/1140.png">
    <div>在此先對於hearF1開始進行姿勢的新增</div><br>
</center>

<center>
    <img src="./source/ch5/1150.png">
    <div>完成hearF1</div><br>
</center>

<center>
    <img src="./source/ch5/1160.png">
    <div>完成hearF2</div><br>
</center>

<center>
    <img src="./source/ch5/1170.png">
    <div>完成hearF3</div><br>
</center>

<center>
    <img src="./source/ch5/1180.png">
    <div>完成hearF4</div><br>
</center>

<center>
    <img src="./source/ch5/1190.png">
    <div>完成hearF5</div><br>
</center>

<center>
    <img src="./source/ch5/1200.png">
    <div>完成hearF6</div><br>
</center>

<center>
    <img src="./source/ch5/1210.png">
    <div>完成hearF7</div><br>
</center>

<center>
    <img src="./source/ch5/1220.png">
    <div>完成hearF8</div><br>
</center>

<center>
    <img src="./source/ch5/1230.png">
    <div>完成hearF9</div><br>
</center>

<center>
    <img src="./source/ch5/1240.png">
    <div>完成hearFA</div><br>
</center>

<center>
    <img src="./source/ch5/1250.png">
    <div>同樣也要從反方向開始，也就是對hearFH進行姿勢的新增</div><br>
</center>

<center>
    <img src="./source/ch5/1260.png">
    <div>完成hearFH</div><br>
</center>

<center>
    <img src="./source/ch5/1270.png">
    <div>完成hearFG</div><br>
</center>

<center>
    <img src="./source/ch5/1280.png">
    <div>完成hearFF</div><br>
</center>

<center>
    <img src="./source/ch5/1290.png">
    <div>完成hearFE</div><br>
</center>

<center>
    <img src="./source/ch5/1300.png">
    <div>完成hearFD</div><br>
</center>

<center>
    <img src="./source/ch5/1310.png">
    <div>完成hearFC</div><br>
</center>

<center>
    <img src="./source/ch5/1320.png">
    <div>完成hearFB</div><br>
</center>

<center>
    <img src="./source/ch5/1330.png">
    <div>總算完成頭髮的部份了(雖然再有骨架時真的看不太清楚)</div><br>
</center>

<center>
    <img src="./source/ch5/1340.png">
    <div>我們回到物體模式選擇髮帶</div><br>
</center>

<center>
    <img src="./source/ch5/1350.png">
    <div>同樣也是到姿式模式</div><br>
</center>

<center>
    <img src="./source/ch5/1360.png">
    <div>從sh1到sh6</div><br>
</center>

<center>
    <img src="./source/ch5/1370.png">
    <div>完成sh1</div><br>
</center>

<center>
    <img src="./source/ch5/1380.png">
    <div>完成sh2</div><br>
</center>

<center>
    <img src="./source/ch5/1390.png">
    <div>完成sh3</div><br>
</center>

<center>
    <img src="./source/ch5/1400.png">
    <div>完成sh4</div><br>
</center>

<center>
    <img src="./source/ch5/1410.png">
    <div>完成sh5</div><br>
</center>

<center>
    <img src="./source/ch5/1420.png">
    <div>完成sh6</div><br>
</center>

<center>
    <img src="./source/ch5/1430.png">
    <div>完成所有肢體骨架與姿勢動畫</div><br>
</center>

### 5.4. 其他常見問題與補充事項

#### 5.4.1. 運用取消對collection的打勾來隱藏物件，但在因為有整體動畫的物體模式運動，在其他幀打開時物件已不在指定位置
這部份處理其實比較簡單，就是在原本的取消打勾時的那幀位置重新打勾就行了。

#### 5.4.2 轉動X軸與Z軸
在此轉動X軸與Z軸其實也是可以的，只是要注意我們的人是個紙片人，所以在轉動上，請注意這類情況。

#### 5.4.3 清除動畫的方法
* 在此我們是以邊做動畫邊弄姿勢庫的方式去建立動畫，而我們要如何快速的去清除我們在此設定人物的所有動畫呢？
    1. 在此我們先將律表放到我們想要維持的姿式位置
    2. 對於物體模式中所有人物物件先進行選取
    3. 再來進入姿勢模式，並按下左上的**選取**->**All**
    4. 然後我們看到律表上，點一下律表，在選擇律表（或是到時間軸也行）
    5. 點一下律表，用鼠標把所有的摘要框起來
    6. 這時所有的物體動作與姿勢動作的動作幀都被我們所選
    7. 然後右鍵，按下清除鍵幀
    8. 這時所有對於人物的動畫就清除了


### 5.5. 小結
雖然建立姿勢庫的流程非常繁瑣，但實際上在後續的動畫上是有很大的用途的。

## 6. 使用Eevee Render輸出

### 6.1. 什麼是eevee？

### 6.2. 輸出動畫

<center>
    <img src="./source/ch6/0010.png">
    <div>接著我們就用eevee去render</div><br>
</center>

<center>
    <img src="./source/ch6/0020.png">
    <div>我們接著點下render properties</div><br>
</center>

<center>
    <img src="./source/ch6/0030.png">
    <div>請先確認我們是使用eevee render engine</div><br>
</center>

<center>
    <img src="./source/ch6/0040.png">
    <div>我們接再著點下output properties</div><br>
</center>

<center>
    <img src="./source/ch6/0050.png">
    <div>我們調整我們的輸出幀率(基本上只要欺騙過人的眼睛就夠了)</div><br>
</center>

<center>
    <img src="./source/ch6/0060.png">
    <div>點下時間重新映射(因為這樣輸出只有1點多秒)</div><br>
</center>

<center>
    <img src="./source/ch6/0070.png">
    <div>設定old40 new150</div><br>
</center>

<center>
    <img src="./source/ch6/0080.png">
    <div>往下拉，到輸出的選擇上檔案格式由png改成AVI_JPEG</div><br>
</center>

<center>
    <img src="./source/ch6/0090.png">
    <div>品質拉到100％，並將色彩選擇RGB，此外請確定輸出檔案的指定位置</div><br>
</center>

<center>
    <img src="./source/ch6/0100.png">
    <div>此外由於new是mapping到150，所以結束幀也需設定成150幀</div><br>
</center>

<center>
    <img src="./source/ch6/0110.png">
    <div>這時我們按下算繪，再按下Render Animatrion</div><br>
</center>

<center>
    <img src="./source/ch6/0120.png">
    <div>這時就會看到算繪的視窗，這時就已經在輸出了</div><br>
</center>

### 6.3. 其他常見問題與補充事項

#### 6.3.1. eevee透明輸出問題

#### 6.3.2. render設定

#### 6.3.3. 輸出的時間重新mapping後調整

#### 6.3.4. 使用雲端主機去算繪的問題

### 6.4. 小結

---

## 施工線
由於後面需要花更多時間去完成，Cycle Render、光源、動畫前後景控制的能講的部份太多了，所以在此先容許我休息一陣子(可能半年到一年的時間後再更第六章)。

---
## 參考文獻
[1] 
[2]
[3]
[4]
[5]
[6] 



