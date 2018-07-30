---
title: 在 Lync Server 2013 中管理通訊錄服務
TOCTitle: 在 Lync Server 2013 中管理通訊錄服務
ms:assetid: 801e4243-9670-4477-aa2f-88b61ecf5351
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429711(v=OCS.15)
ms:contentKeyID: 49291468
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理通訊錄服務

 

_**上次修改主題的時間：** 2015-03-09_

部署 Lync Server、Enterprise Edition 或 Standard Edition 伺服器 時，預設會安裝通訊錄服務。通訊錄服務使用的資料庫 (RTCab) 是建立在 SQL Server 上 (就 Enterprise Edition 而言，這是後端 SQL Server；就 Standard Edition 伺服器 而言，這是組合的 SQL Server)。

> [!NOTE]  
> 如需使用 [ADSI 編輯器]編輯 Active Directory 網域服務 物件屬性的相關資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=330427">ADSI 編輯器</a>。如需通訊錄服務專用之 Resource Kit 工具的相關資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=330429">Microsoft Lync Server 2013 Resource Kit 工具</a> (英文)。



## Address Book Server 電話號碼正規化

Lync Server 需要標準化的 RFC 3966/E.164 電話號碼。若要使用未經組織或格式不一致的電話號碼，Lync Server 會使用 Address Book Server 預先處理電話號碼，然後才將電話號碼交給正規化規則處理。從通訊錄中使用電話號碼並套用正規化規則後，Lync Phone Edition 和 Lync Mobile 等用戶端就可以使用這些正規化號碼。

舊版中使用的正規化規則可能需要經過一些調整才能正常使用。因為在交給正規化規則之前會先移除空格和非強制字元，所以如果 regex 運算式明確尋找虛線或其他已移除的字元，正規化規則可能會失敗。您應該檢閱正規化規則，確保它們不會尋找這類非強制字元，否則，如果規則預期字元存在而字元不存在，規則就會先按正常程序失敗再繼續運作。

## 使用者複寫器和 Address Book Server

Address Book Server 會使用 \[使用者複寫器\] 提供的資料，來更新其最初從全域通訊清單 (GAL) 取得的資訊。\[使用者複寫器\] 會將每個使用者、連絡人和群組的 Active Directory 網域服務 屬性寫入資料庫中的 AbUserEntry 資料表，而 Address Book Server 會將資料庫中的使用者資料同步到 Address Book Server 檔案存放區中的檔案以及通訊錄資料庫 RTCab。AbUserEntry 資料表的架構使用兩個資料行 **UserGuid** 和 **UserData**。**UserGuid** 是索引資料行，其中包含 Active Directory 物件的 16 位元組 GUID。**UserData** 是影像資料行，其中包含該連絡人所有先前提及的 Active Directory 網域服務 屬性。

\[使用者複寫器\] 會讀取組態資料表來判斷要寫入的 Active Directory 屬性，此資料表與 AbUserEntry 資料表位於相同的 SQL Server 執行個體。AbAttribute 資料表包含三個資料行 **ID**、**Name**、**Flags** 和 **Enable**。此資料表是在資料庫設定期間建立。如果 AbAttribute 資料表是空的，\[使用者複寫器\] 會略過其 AbUserEntry 資料表處理邏輯。Address Book Server 屬性是從 AbAttribute 資料表擷取的動態屬性，該資料表最初是在 Address Book Server 啟動時由 Address Book Server 寫入。

Address Book Server 啟動時會在 AbAttribute 資料表中填入如下表中所示的值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>識別碼</th>
<th>名稱</th>
<th>旗標</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>givenName</p></td>
<td><p>0x01400000</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Sn</p></td>
<td><p>0x02400000</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>displayName</p></td>
<td><p>0x03420000</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>Title</p></td>
<td><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p>mailNickname</p></td>
<td><p>0x05400000</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p>Company</p></td>
<td><p>0x06000000</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p>physicalDeliveryOfficeName</p></td>
<td><p>0x07000000</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>msRTCSIP-PrimaryUserAddress</p></td>
<td><p>0x08520C00</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>telephoneNumber</p></td>
<td><p>0x09022800</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>homePhone</p></td>
<td><p>0x0A302800</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p>Mobile</p></td>
<td><p>0x0B622800</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>otherTelephone</p></td>
<td><p>0x0C302000</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p>ipPhone</p></td>
<td><p>0x0D302000</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p>Mail</p></td>
<td><p>0x0E500000</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p>groupType</p></td>
<td><p>0x0F010800</p></td>
</tr>
<tr class="even">
<td><p>16</p></td>
<td><p>Department</p></td>
<td><p>0x10000000</p></td>
</tr>
<tr class="odd">
<td><p>17</p></td>
<td><p>說明</p></td>
<td><p>0x11000100</p></td>
</tr>
<tr class="even">
<td><p>18</p></td>
<td><p>Manager</p></td>
<td><p>0x12040001</p></td>
</tr>
<tr class="odd">
<td><p>19</p></td>
<td><p>proxyAddress</p></td>
<td><p>0x00500105</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>msExchHideFromAddressLists</p></td>
<td><p>0xFF000003</p></td>
</tr>
<tr class="odd">
<td><p>99</p></td>
<td><p>entryID</p></td>
<td><p>0x99000000</p></td>
</tr>
</tbody>
</table>


**ID** 資料行中的數字必須是唯一的，且絕不可重複使用。另外，保持 ID 值小於 256 可在 Address Book Server 寫入的輸出檔中節省空間。不過，ID 最大值是 65535。**Name** 資料行對應於 \[使用者複寫器\] 應在 AbUserEntry 資料表中為每個連絡人置入的 Active Directory 屬性名稱。**Flags** 資料行中的值用來定義屬性的類型。\[使用者複寫器\] 認得下列類型的 Address Book Server 屬性 (以 **Flags** 資料行中的值的低位元組表示)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x0</p></td>
<td><p>字串屬性。[使用者複寫器] 會先將此類型轉換為 UTF-8，再將之儲存於 AbUserEntry 資料表。</p></td>
</tr>
<tr class="even">
<td><p>0x1</p></td>
<td><p>二進位屬性。[使用者複寫器] 會以二進位大型物件儲存此屬性而不做任何轉換。</p></td>
</tr>
<tr class="odd">
<td><p>0x2</p></td>
<td><p>字串屬性，但只在屬性值開頭為 &quot;tel:&quot; 時才包含。這主要用於多重值字串屬性，特別是 <strong>proxyAddresses</strong>。在此情況下，Address Book Server 只會注意開頭為 &quot;tel:&quot; 的 <strong>proxyAddresses</strong> 項目。因此，為了節省空間，[使用者複寫器] 只會儲存開頭為 &quot;tel:&quot; 的項目。</p></td>
</tr>
<tr class="even">
<td><p>0x3</p></td>
<td><p>布林字串屬性，TRUE 會使 [使用者複寫器] 不將此連絡人放入 AbUserEntry 資料表中。如果是 FALSE，則會使 [使用者複寫器] 將此連絡人的屬性放入 AbUserEntry 資料表中，但不包括具有此旗標的特定屬性。這是另一個主要用於 <strong>msExchHideFromAddressLists</strong> 屬性的特殊案例類型。</p></td>
</tr>
<tr class="odd">
<td><p>0x4</p></td>
<td><p>字串屬性，但只在屬性值開頭為 &quot;smtp:&quot;且含有 &quot;@&quot; 符號時才包含。</p></td>
</tr>
<tr class="even">
<td><p>0x5</p></td>
<td><p>字串屬性，但只在屬性值開頭為 &quot;tel:&quot;或 &quot;smtp:&quot;且含有 &quot;@&quot; 符號時才包含。</p></td>
</tr>
<tr class="odd">
<td><p>0x100</p></td>
<td><p>如果設定，則這是可針對每個連絡人出現一次以上的多重值屬性。</p></td>
</tr>
<tr class="even">
<td><p>0x400</p></td>
<td><p>如果設定，則這將識別連絡人的電子郵件使用者帳戶名稱屬性。Address Book Server 會使用此旗標來識別要在電話正規化事件記錄項目中顯示的屬性值。</p></td>
</tr>
<tr class="odd">
<td><p>0x800</p></td>
<td><p>如果設定，則這將識別連絡人的必要屬性。只有當此屬性在 Active Directory 中有值時，Address Book Server 才會在 AbUserEntry 資料表中加入使用者。如果有一個以上的必要屬性，則只要其中一個有值，就會在 AbUserEntry 資料表中加入使用者。</p></td>
</tr>
<tr class="even">
<td><p>0x1000</p></td>
<td><p>如果設定，則 Address Book Server 一律會正規化此屬性的值。</p></td>
</tr>
<tr class="odd">
<td><p>0x2000</p></td>
<td><p>如果設定，則當 <strong>UseNormalizationRules</strong> CMS 設定為 FALSE 時，Address Book Server 會使用 <strong>proxyAddresses</strong> 中的正規化數字，否則其行為與旗標位元為 0x1000 時相同。</p></td>
</tr>
<tr class="even">
<td><p>0x4000</p></td>
<td><p>如果設定，則 Address Book Server 不會在 AbUserEntry 資料表中加入所指定的屬性為此值的物件。例如，如果 <strong>msRTCSIP-PrimaryUserAddress</strong> 屬性已設定此旗標位元，則不會將具有此屬性的連絡人寫入資料庫。</p></td>
</tr>
<tr class="odd">
<td><p>0x8000</p></td>
<td><p>如果設定，則 Address Book Server 不會將所指定的屬性不是此值的物件加入 AbUserEntry 資料表。如果物件上同時設定 0x4000 和 0x8000 旗標位元，則以旗標位元值設為 0x4000 的屬性為優先，且會從 AbUserEntry 資料表中排除物件。</p></td>
</tr>
<tr class="even">
<td><p>0x10000</p></td>
<td><p>如果設定，則這代表群組物件。[使用者複寫器] 會使用此旗標位元來加入具有 <strong>groupType</strong> 屬性 (表示這是群組) 的連絡人，例如，通訊群組清單或安全性群組。</p></td>
</tr>
<tr class="odd">
<td><p>0x20000</p></td>
<td><p>如果設定，則 [使用者複寫器] 會使用此旗標位元將此屬性加入裝置特定 Address Book Server 檔案 (副檔名為 .dabs 的檔案)。</p></td>
</tr>
</tbody>
</table>


在舊版 Lync Server 中，將變更套用於 Active Directory 時，系統管理員需要執行 **Update -CSUserDatabase** 和 **Update –CSAddressBook**Windows PowerShell Cmdlet，才能立即變更 Lync Server 資料庫和 RTCab 資料庫。在 Lync Server 2013 中，Lync Server 使用者複寫器將從 Active Directory 擷取變更，並按照設定的間隔更新 Lync Server 使用者資料庫。Lync Server 使用者複寫器也會將變更迅速傳播到 RTCab 資料庫，系統管理員完全不需要執行 Update-CSAddressBook。如果啟用 Address Book Web 查詢，則 Lync 用戶端會在搜尋結果中反映這些變更。如果啟用 Address Book 檔案下載，系統管理員只需要執行 Update -CSAddressBook。

> [!NOTE]  
> Lync Server 使用者複寫器會每隔 5 分鐘執行一次。您可以使用 Set -CSUserReplicatorConfiguration -ReplicationCycleInterval &lt;&gt; 設定這個間隔。



## 篩選通訊錄

您可以根據 AbAttribute 資料表中列出的 Active Directory 網域服務 屬性，控制要在 Address Book Server 檔案中填入的使用者。其中一個這類可用於篩選的屬性就是 **msExchangeHideFromAddressBook** 屬性。這是由 Exchange 架構所新增的使用者屬性。如果此屬性的值是 TRUE，Exchange Server 會使用此屬性在 Outlook 全域通訊清單 (GAL) 隱藏該連絡人。同樣地，如果此屬性的值是 TRUE，\[使用者複寫器\] 不會在 AbUserEntry 資料表中加入該使用者，而此使用者不會出現在 Address Book Server 檔案中。

您可以使用一些旗標位元來定義要在 Address Book Server 屬性上使用的篩選器。例如，某些旗標位元的存在可將屬性識別為包含屬性或排除屬性。\[使用者複寫器\] 會濾除含有排除屬性的連絡人，並濾除不含包含屬性的連絡人。

> [!WARNING]
> 如需篩選通訊錄的詳細資訊，請參閱<a href="https://technet.microsoft.com/en-us/library/gg415643(v=ocs.15)">Address Book Server Cmdlet</a> 和<a href="http://go.microsoft.com/fwlink/?linkid=330430">篩選 Lync 2013 通訊錄</a> (英文)


目前，有三種不同的篩選器。下表列出這些篩選器。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x800</p></td>
<td><p>如果設定，則這將識別連絡人的必要屬性。[使用者複寫器] 會使用此旗標位元來濾除不含至少一個必要屬性的連絡人。OuPathId 是一律會設定的必要屬性。因此，至少應該再設定另一個必要屬性。否則，仍然不會將連絡人 (具有必要屬性 OuPathId 的值) 寫入資料庫。例如，如果 <strong>telephoneNumber</strong> 和 <strong>homePhone</strong> 是定義為必要屬性，則只會將具有至少其中一個屬性的連絡人寫入資料庫。</p></td>
</tr>
<tr class="even">
<td><p>0x4000</p></td>
<td><p>如果設定，則這將識別排除屬性。[使用者複寫器] 會使用此旗標位元來濾除包含此屬性的連絡人。例如，如果 <strong>msRTCSIP-PrimaryUserAddress</strong> 是定義為排除屬性，則不會將具有此屬性的連絡人寫入資料庫。</p></td>
</tr>
<tr class="odd">
<td><p>0x8000</p></td>
<td><p>如果設定，則這將識別包含屬性。[使用者複寫器] 會使用此旗標位元來濾除不含此屬性的連絡人。例如，如果 <strong>msRTCSIP-PrimaryUserAddress</strong> 是定義為包含屬性，則只會將具有此屬性的連絡人寫入資料庫。</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 如果同時設定 0x4000 (排除屬性) 和 0x8000 (包含屬性) 旗標位元，則 0x4000 位元會覆寫 0x8000 位元，並排除該連絡人。



雖然您可以篩選通訊錄來僅包含某些使用者，但限制項目並不會限制其他使用者連絡被濾除的使用者，或查看其顯示狀態的能力。使用者一律可以輸入使用者的完整登入名稱，以尋找不在通訊錄中的使用者，或是對其手動傳送即時訊息或手動進行呼叫。另外，在 Outlook 中也可以找到使用者的連絡資訊。

雖然在通訊錄檔案中有完整的連絡人記錄，可讓您使用 Lync Server 對工作階段初始通訊協定 (SIP) 未設定的使用者進行電子郵件、電話或 Enterprise Voice 呼叫 (如果伺服器上已啟用 Enterprise Voice)，但有些組織仍偏好僅在 Address Book Server 項目中包含啟用 SIP 的使用者。您可以在下列必要屬性的**旗標**資料行中清除 0x800 位元，以篩選通訊錄來僅包含啟用 SIP 的使用者。**mailNickname**、**telephoneNumber**、**homePhone** 和 **mobile**。您可以在 **msRTCSIP-PrimaryUserAddress** 屬性的**旗標**資料行中設定 0x8000 (包含屬性)，以篩選通訊錄來僅包含啟用 SIP 的使用者。這也有助於從通訊錄檔案中排除服務帳戶。

修改 AbAttribute 資料表之後，您可以執行 Cmdlet **Update-CsUserDatabase** 命令，以重新整理 AbUserEntry 資料表中的資料。在 UR 複寫完成之後，您可以手動執行 Cmdlet **UpdateCsAddressBook** 命令，以更新 Address Book Server 檔案存放區中的檔案。

> [!NOTE]  
> Address Book Server 所在的前端伺服器無法利用系統管理權限來設定。在部署期間就已選擇一個前端 – 通常是第一個部署的前端伺服器。如果失敗，則會將通訊錄服務移至另一個前端伺服器，而不需要系統管理人員介入。



> [!IMPORTANT]  
> 如果您已在多樹系部署或父系/子系部署中合併或修改基礎結構 (例如，在移至 Lync Server 之前合併基礎結構)，可能會發現某些使用者執行通訊錄服務下載和 Address Book Web Query 時會失敗。在具有多個網域或樹系的部署中，出現此問題的使用者物件上已填入屬性 <strong>MsRTCSIP-OriginatorSid</strong>。您必須將這些物件的 <strong>MsRTCSIP-OriginatorSid</strong> 屬性設為 NULL，才能解決此問題。


