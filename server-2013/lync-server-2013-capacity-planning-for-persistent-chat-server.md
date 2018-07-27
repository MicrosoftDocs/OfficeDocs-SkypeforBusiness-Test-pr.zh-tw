---
title: Lync Server 2013：常設聊天室伺服器的容量規劃
TOCTitle: 常設聊天室伺服器的容量規劃
ms:assetid: 7a850cd5-c789-4795-a8ff-083be21ae784
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615006(v=OCS.15)
ms:contentKeyID: 49291407
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室伺服器的容量規劃

 

_**上次修改主題的時間：** 2015-03-09_

常設聊天室伺服器 可以執行多使用者的即時聊天，其可持續進行進一步擷取和搜尋。不同於已儲存於使用者信箱中的群組立即訊息 (IM)，如果已設定交談記錄， 常設聊天室伺服器 工作階段保持開啟狀態的時間會更久，而且內容會與在進行中交談用到的訊息、檔案、URL 和其他資料一起儲存於伺服器上。

容量規劃是準備部署 常設聊天室伺服器 時的重要工作。本主題詳述支援的 常設聊天室伺服器 拓撲，以及可用來判斷您部署之最佳組態的容量規劃表格。同時也會說明如何對在尖峰時間需要較大容量的 常設聊天室伺服器 部署進行最佳管理。

若要下載 常設聊天室伺服器，請參閱＜Microsoft Lync Server 13 常設聊天室伺服器＞，網址為 [http://go.microsoft.com/fwlink/?linkid=209539\&clcid=0x404 (英文)](http://go.microsoft.com/fwlink/?linkid=209539%26clcid=0x404)。

如需有關安裝 常設聊天室伺服器 的詳細資訊，請參閱＜部署＞文件中的 [在 Lync Server 2013 中安裝常設聊天室伺服器](lync-server-2013-installing-persistent-chat-server.md) 和 [在 Lync Server 2013 中設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server.md)。

支援工具 (例如 Lync Server 規劃工具) 可以進一步協助您進行容量規劃。如需有關規劃工具的詳細資訊，請參閱＜規劃＞文件中的 [開始 Lync Server 2013 的規劃程序](lync-server-2013-beginning-the-planning-process.md)。

## 常設聊天室伺服器 支援的拓撲

您可以在單一伺服器或多伺服器集區中，利用單一伺服器或多伺服器拓撲來部署 常設聊天室伺服器。

我們現在也針對新的 Lync Server 2013 部署，在 Standard Edition 伺服器上支援 常設聊天室伺服器。但是，效能與範圍將受到影響，因為沒有適用於這個新部署的高可用性，我們預期您主要會基於概念證明、評估等目的來使用此支援。

> [!NOTE]  
> 如需其他有關這兩種拓撲的詳細資訊，請參閱此文件集中的 <a href="lync-server-2013-planning-for-persistent-chat-server.md">在 Lync Server 2013 中規劃常設聊天室伺服器</a> 和＜部署＞文件中的 <a href="lync-server-2013-deploying-persistent-chat-server.md">在 Lync Server 2013 中部署常設聊天室伺服器</a>。



## 單一伺服器拓撲

常設聊天室伺服器 的最基本組態和最簡單部署為單一 常設聊天室伺服器前端伺服器拓撲。此部署需要一部執行 常設聊天室伺服器 的伺服器 (如果已啟用規範，則可選擇性地執行 Compliance Service)、一部裝載這兩個 SQL Server 資料庫的伺服器，而且如果需要規範，則需要使用 SQL Server 資料庫來儲存規範資料。

> [!IMPORTANT]  
> 您可以將其他伺服器新增至 Persistent Chat Server 集區，其會啟動為 拓撲產生器中的單一伺服器部署。建議使用多伺服器集區拓撲，即使您使用單一伺服器也一樣，如此一來，您日後將能視需要新增多部伺服器。



下圖會針對含規範的單一 常設聊天室伺服器前端伺服器顯示拓撲的所有必要和選項元件。

**單一 Persistent Chat Server**

![安裝有 Compliance Service 的單一伺服器拓撲](images/Gg398500.9168fa52-61e0-4d17-a14d-45fd32e81456(OCS.15).jpg "安裝有 Compliance Service 的單一伺服器拓撲")

## 多部伺服器拓撲

若要提供較大的容量和可靠性，您可以部署多伺服器拓撲 (如 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md) 中所述)。多伺服器拓撲最多可以包含四部執行 常設聊天室伺服器 的作用中電腦 (高可用性和災害復原將允許最多八部，但只有四部可處於作用中狀態，其餘四部則為待命狀態)。每部伺服器支援最多 20,000 位使用者同時使用，總共 80,000 位使用者可以同時連線至含有 4 部伺服器的 Persistent Chat Server 集區。多伺服器拓撲與單一伺服器拓撲相同，差別在於有多部伺服器可裝載 常設聊天室伺服器，而且範圍更大。多部執行 常設聊天室伺服器 的電腦應該與 Lync Server 和 Compliance Service 位在相同的 Active Directory 網域服務 網域中。

下圖顯示多伺服器拓撲的所有元件，包括多部執行 常設聊天室伺服器 的電腦、選用的 Compliance Service 和獨立的規範資料庫。

**多部 Persistent Chat Server**

![多部伺服器拓撲](images/Gg398500.19aea898-28df-4d9b-903c-f72ef062d919(OCS.15).jpg "多部伺服器拓撲")

在四部伺服器的 常設聊天室伺服器部署中，可以有 80,000 位使用者同時登入和使用 常設聊天室，產生的負載會依每部伺服器 20,000 位使用者的方式平均分配。如果其中一部伺服器無法使用，則連線至該伺服器的使用者將遺失對 常設聊天室伺服器 的存取。連線遭中斷的使用者會自動被轉接到其餘伺服器，直到無法使用的伺服器還原為止。依網路上的 常設聊天室流量而定，此轉接程序可能需要數分鐘或更久。因為其餘的每部伺服器最多可裝載 30,000 位使用者，所以建議您盡快還原無法使用的伺服器，以避免發生效能問題。否則，您可以使用 拓撲產生器或 Windows PowerShell Cmdlet **set-CsPersistentChatActiveServer**，讓其他 常設聊天室伺服器 可供使用。

## 常設聊天室伺服器 容量規劃

下列表格可協助您進行 常設聊天室伺服器 的容量規劃。它們會針對變更各項 常設聊天室伺服器 設定如何影響容量功能來建立模型。

## 規劃 常設聊天室伺服器 的最大容量

使用下列範例表格，來判斷您可以支援的使用者數目。

### Persistent Chat Server 集區 最大容量範例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>作用中 常設聊天室 服務執行個體數</p></td>
<td><p><em>4</em></p></td>
</tr>
<tr class="even">
<td><p>常設聊天室服務執行個體數</p></td>
<td><p><em>8 (4 must be inactive; only a maximum of 4 can be active)</em></p></td>
</tr>
<tr class="odd">
<td><p>已連線的作用中使用者數</p></td>
<td><p><em>80,000</em></p></td>
</tr>
<tr class="even">
<td><p>已佈建的使用者總數</p></td>
<td><p>150,000</p></td>
</tr>
<tr class="odd">
<td><p>端點數</p></td>
<td><p>120,000</p></td>
</tr>
</tbody>
</table>


在上述範例中，我們計畫支援 常設聊天室伺服器 所允許的最大使用者數目： 常設聊天室服務的四個伺服器/執行個體 (針對高可用性和災害復原，可以有四部以上執行 常設聊天室伺服器 的被動伺服器) ，每部伺服器 20,000 位使用者，總共 80,000 位作用中使用者。

## 管理 常設聊天室存取的容量規劃

下列範例表格可協助您規劃管理 Persistent Chat Server 集區中的 常設聊天室存取。

### 聊天室存取管理範例

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>小型聊天室</th>
<th>中型聊天室</th>
<th>大型聊天室</th>
<th>合計</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>聊天室的大小 (已連線的使用者數目)</p></td>
<td><p>每個聊天室 30 位使用者</p></td>
<td><p>每個聊天室 150 位使用者</p></td>
<td><p>每個聊天室 16,000 位使用者</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>聊天室數</p></td>
<td><p>32,000</p></td>
<td><p>1,067</p></td>
<td><p>10</p></td>
<td><p>33,077</p></td>
</tr>
<tr class="odd">
<td><p>做為聽眾席的聊天室 %</p></td>
<td><p>1%</p></td>
<td><p>1%</p></td>
<td><p>50%</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>開放的聊天室 %</p></td>
<td><p>3%</p></td>
<td><p>3%</p></td>
<td><p>50%</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>開放的聊天室數 (沒有明確的成員資格)</p></td>
<td><p>960</p></td>
<td><p>32</p></td>
<td><p>5</p></td>
<td><p>997</p></td>
</tr>
<tr class="even">
<td><p>非開放的聊天室數 (具備明確成員資格的一般聊天室)</p></td>
<td><p>31,040</p></td>
<td><p>1.035</p></td>
<td><p>5</p></td>
<td><p>32,080</p></td>
</tr>
<tr class="odd">
<td><p>聽眾席聊天室數 (其他簡報者項目)</p></td>
<td><p>0</p></td>
<td><p>32</p></td>
<td><p>5</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>透過直接成員資格管理的聊天室數</p></td>
<td><p>50%</p></td>
<td><p>10%</p></td>
<td><p>0%</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>依使用者群組管理的聊天室數</p></td>
<td><p>50%</p></td>
<td><p>90%</p></td>
<td><p>100%</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每個聊天室的成員資格 (未明確指定) 清單中的使用者群組數 (適用於開放的聊天室)</p></td>
<td><p>0</p></td>
<td><p>0</p></td>
<td><p>0</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每個聊天室的成員資格清單中的使用者數 (適用於非開放的聊天室)</p></td>
<td><p>30</p></td>
<td><p>150</p></td>
<td><p>16,000</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每個聊天室的成員資格清單中的使用者群組數 (適用於非開放的聊天室)</p></td>
<td><p>3</p></td>
<td><p>5</p></td>
<td><p>10</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每個聊天室的管理員清單中的使用者與使用者群組數 (適用於開放與非開放的聊天室)</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每個聽眾席聊天室的簡報者清單中的使用者與使用者群組數 (適用於開放與非開放的聊天室)</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>所有非開放聊天室的使用者型成員資格實體數</p></td>
<td><p>465,600</p></td>
<td><p>15,520</p></td>
<td><p>-</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>所有非開放聊天室的使用者群組型成員資格實體數</p></td>
<td><p>46,560</p></td>
<td><p>4656</p></td>
<td><p>50</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>所有聽眾聊天室的使用者與使用者群組型實體數</p></td>
<td><p>0</p></td>
<td><p>192</p></td>
<td><p>50</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>所有聊天室管理員清單的使用者與使用者群組型管理員實體</p></td>
<td><p>192,000</p></td>
<td><p>6,400</p></td>
<td><p>60</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每個聊天室的作用中使用者數</p></td>
<td><p><em>30</em></p></td>
<td><p><em>150</em></p></td>
<td><p><em>16,000</em></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每位使用者的聊天室數</p></td>
<td><p><em>12</em></p></td>
<td><p><em>2</em></p></td>
<td><p><em>2</em></p></td>
<td><p><em>16</em></p></td>
</tr>
<tr class="odd">
<td><p>每個聊天室之成員資格清單中的使用者群組數</p></td>
<td><p><em>10</em></p></td>
<td><p><em>10</em></p></td>
<td><p><em>15</em></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>依使用者群組管理的聊天室數</p></td>
<td><p><em>50%</em></p></td>
<td><p><em>50%</em></p></td>
<td><p><em>50%</em></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>所有聊天室的使用者群組型成員資格實體數</p></td>
<td><p>155,200</p></td>
<td><p>5173</p></td>
<td><p>68</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>所有聊天室的使用者型成員資格實體數</p></td>
<td><p>465,600</p></td>
<td><p>77,600</p></td>
<td><p>72,000</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每個聊天室的管理員、簡報者和範圍清單中的使用者與使用者群組數</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>所有聊天室的管理員、簡報者和範圍清單中的使用者與使用者群組數</p></td>
<td><p>192,000</p></td>
<td><p>6400</p></td>
<td><p>60</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>存取控制項目數</p></td>
<td><p>704,160</p></td>
<td><p>26,768</p></td>
<td><p>160</p></td>
<td><p>731,088</p></td>
</tr>
<tr class="even">
<td><p>最大存取控制項目數</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>2,000,000</p></td>
</tr>
</tbody>
</table>


當您在上述範例中根據建議的方針來部署 常設聊天室伺服器時，它們在啟用規範的情況下，可以透過四部伺服器的集區來處理最多 80,000 位作用中使用者。

此範例顯示的聊天室分為三種：小型聊天室 (隨時都有 30 位作用中使用者)、中型聊天室 (150 位作用中使用者) 和大型聊天室 (16,000 位作用中使用者)。特定大小聊天室的數目是依下列項目的總數計算而來：

  - 系統中的作用中使用者

  - 特定大小聊天室中的作用中使用者

  - 單一使用者加入的特定大小聊天室

針對每個聊天室，上述容量規劃表格會指定與聊天室相關聯的存取控制項目數 (包括直接指派給聊天室的項目)。您可以使用存取控制清單 (ACL)，控制對個別聊天室的存取。您也可以在類別層級控制存取。在 ACL 中，個別存取控制項目可以是使用者群組 (例如，安全性群組、通訊群組清單或單一使用者)。您可以定義聊天室管理員、簡報者和成員的存取控制項目。

> [!IMPORTANT]  
> 在規劃聊天室的管理策略時，請記住，允許的存取控制項目總數是 2 百萬個。如果存取控制項目總計超過 2 百萬個，伺服器效能可能會大幅下降。為了避免此問題，請盡可能確定存取控制項目是使用者群組，而非個別使用者。



## 邀請式聊天室存取的容量管理規劃

您可以使用下列容量規劃表格，來了解 常設聊天室伺服器 在設定為傳送邀請時所建立並儲存於 常設聊天室資料庫中的邀請數目。您可以使用 Lync Server 控制台中的 **\[聊天室類別設定\]** 頁面或使用 Windows PowerShell Cmdlet **set-csPersistentChatCategory**，在 \[類別\] 上管理邀請。您可以使用從 Lync 用戶端啟動的 **\[聊天室管理\]** 或使用 Windows PowerShell Cmdlet **set-csPersistentChatRoom**，在聊天室上管理邀請 (與該類別允許的項目一致)。

下表中的範例資料假設在 50% 的聊天室上，其 **\[聊天室設定\]** 頁面上的 **\[邀請\]** 選項都是設定為 **\[是\]** 。

> [!IMPORTANT]  
> 如果伺服器產生的邀請總計超過 1 百萬個，則伺服器效能可能會大幅下降。為了避免此問題，請務必減少設為傳送邀請的聊天室，或是限制可加入已設為傳送邀請之聊天室的使用者數目。



### 邀請式聊天室存取範例

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>小型聊天室</th>
<th>中型聊天室</th>
<th>大型聊天室</th>
<th>合計</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>可以存取聊天室的使用者</p></td>
<td><p>每個聊天室 30 位使用者</p></td>
<td><p>每個聊天室 150 位使用者</p></td>
<td><p>每個聊天室 16,000 位使用者</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>具備邀請的聊天室百分比</p></td>
<td><p>50%</p></td>
<td><p>50%</p></td>
<td><p>50%</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>設成傳送邀請的聊天室數</p></td>
<td><p><em>16,000</em></p></td>
<td><p><em>533</em></p></td>
<td><p><em>5</em></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>可以存取該聊天室的使用者</p></td>
<td><p><em>60</em></p></td>
<td><p><em>225</em></p></td>
<td><p><em>16,000</em></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>常設聊天室伺服器 產生的邀請數</p></td>
<td><p>960,000</p></td>
<td><p>120,000</p></td>
<td><p>80,000</p></td>
<td><p>1,160,000</p></td>
</tr>
<tr class="even">
<td><p>最大允許的邀請數</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>2,000,000</p></td>
</tr>
<tr class="odd">
<td><p>模型 1 - 每個聊天室每天會從預期的訊息數開始</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>每個聊天室的聊天比率 (每天)</p></td>
<td><p>50</p></td>
<td><p>500</p></td>
<td><p>100</p></td>
<td><p>650</p></td>
</tr>
<tr class="odd">
<td><p>所有聊天室的聊天比率 (每秒)</p></td>
<td><p>55.56</p></td>
<td><p>18.52</p></td>
<td><p>0.03</p></td>
<td><p>74</p></td>
</tr>
<tr class="even">
<td><p>模型 2 - 每位使用者每天會從張貼的訊息數開始</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>每位使用者每天的聊天比率</p></td>
<td><p>15</p></td>
<td><p>5</p></td>
<td><p>0.1</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>每個聊天室的聊天比率 (每天)</p></td>
<td><p>38</p></td>
<td><p>375</p></td>
<td><p>800</p></td>
<td><p>1,213</p></td>
</tr>
<tr class="odd">
<td><p>所有聊天室的聊天比率 (每秒)</p></td>
<td><p>41.67</p></td>
<td><p>13.89</p></td>
<td><p>0.28</p></td>
<td><p>56</p></td>
</tr>
</tbody>
</table>


## 常設聊天室伺服器 效能使用者模型

下表說明 常設聊天室伺服器 的使用者模型。這提供了容量規劃需求的基礎，並代表同時有 80,000 位使用者在四部伺服器上進行活動的典型組織。

### 常設聊天室伺服器 效能使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>已連線的作用中使用者數</p></td>
<td><p>80,000</p></td>
</tr>
<tr class="even">
<td><p>常設聊天室伺服器 服務執行個體數</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>小型聊天室大小</p></td>
<td><p>30 位使用者</p></td>
</tr>
<tr class="even">
<td><p>中型聊天室大小</p></td>
<td><p>150 位使用者</p></td>
</tr>
<tr class="odd">
<td><p>大型聊天室大小</p></td>
<td><p>16,000 位使用者</p></td>
</tr>
<tr class="even">
<td><p>聊天室總數</p></td>
<td><p>33,077</p></td>
</tr>
<tr class="odd">
<td><p>小型聊天室數</p></td>
<td><p>32,000</p></td>
</tr>
<tr class="even">
<td><p>中型聊天室數</p></td>
<td><p>1,067</p></td>
</tr>
<tr class="odd">
<td><p>大型聊天室數</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>每位使用者的聊天室總數</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>每位使用者的小型聊天室數</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>每位使用者的中型聊天室數</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>每位使用者的大型聊天室數</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>每位使用者加入的聊天室數</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>尖峰加入速率</p></td>
<td><p>10/秒</p></td>
</tr>
<tr class="even">
<td><p>總聊天速率</p></td>
<td><p>24/秒</p></td>
</tr>
<tr class="odd">
<td><p>小型聊天室的聊天速率</p></td>
<td><p>22.22/秒</p></td>
</tr>
<tr class="even">
<td><p>中型聊天室的聊天速率</p></td>
<td><p>1.67/秒</p></td>
</tr>
<tr class="odd">
<td><p>大型聊天室的聊天速率</p></td>
<td><p>~0.15/秒</p></td>
</tr>
<tr class="even">
<td><p>設成傳送邀請的聊天室百分比</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>直接成員資格的百分比</p></td>
<td><p>50%</p></td>
</tr>
<tr class="even">
<td><p>群組成員資格的百分比</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Active Directory 網域服務 中的平均上階聯盟數</p></td>
<td><p>100 - 200</p></td>
</tr>
<tr class="even">
<td><p>每位使用者的已訂閱連絡人數</p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p>每位使用者的平均端點數目</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="even">
<td><p>每個端點中可見聊天室的平均數目</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>每位使用者的可見聊天室平均數目</p></td>
<td><p>2.25 (1 個聊天室為 50%，2 個聊天室為 50%)；最多開放 6 個聊天室，每個監視器一個</p></td>
</tr>
<tr class="even">
<td><p>每段間隔輪詢的參與者數</p></td>
<td><p>每個可見聊天室 25 位</p></td>
</tr>
<tr class="odd">
<td><p>輪詢間隔的長度</p></td>
<td><p>5 分鐘</p></td>
</tr>
<tr class="even">
<td><p>每秒輪詢的參與者數</p></td>
<td><p>15,000</p></td>
</tr>
<tr class="odd">
<td><p>每位使用者每小時的目前狀態變更次數</p></td>
<td><p>6</p></td>
</tr>
<tr class="even">
<td><p>每秒的目前狀態變更次數</p></td>
<td><p>133.33</p></td>
</tr>
</tbody>
</table>

