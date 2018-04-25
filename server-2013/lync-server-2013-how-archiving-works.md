---
title: 在 Lync Server 2013 中封存的運作方式
TOCTitle: 在 Lync Server 2013 中封存的運作方式
ms:assetid: 536a52a9-cfb7-4392-9620-ffc5b319b31b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204900(v=OCS.15)
ms:contentKeyID: 49290932
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中封存的運作方式

 

_**上次修改主題的時間：** 2014-02-04_

Lync Server 2013 封存提供選項，協助您符合規範需求。若要以符合組織需求的最有效率方式來進行實作和維護，則您需要了解：

  - 可以封存哪些資訊。

  - 如何在部署中啟用和停用封存。

  - 您可以設定來控制如何實作封存的封存選項。

## 可以封存哪些資訊？

可以封存下列類型的內容：

  - 對等立即訊息

  - 會議，其為多方立即訊息

  - 會議內容，包括上傳的內容 (例如，講義) 和事件相關內容 (例如，加入、離開、上傳共用，以及可見度變更)

  - 在會議期間共用白板與投票

不會封存下列類型的內容：

  - 對等檔案傳輸

  - 對等立即訊息和會議的音訊/視訊

  - 對等立即訊息和會議的桌面與應用程式共用

Lync Server 也不會封存常設聊天室的交談。若要封存常設聊天室的交談，您必須啟用和設定 Compliance Service，此為可以利用 Microsoft Lync Server 2013 的 常設聊天室伺服器 部署的元件。如需詳細資訊，請參閱規劃文件中的[在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)。

## 如何開始使用封存？

當您部署伺服器時，封存會自動安裝於每部前端伺服器上，但在您設定封存之前不會加以啟用。您設定封存的方式是根據您部署封存的方式來決定：

  - **使用 Microsoft Exchange 整合進行封存。**如果您的使用者位於 Exchange 2013 且其信箱狀態為 \[就地保留\]，則您可以選取選項來將 Lync Server 2013 儲存與 Exchange 儲存整合。如果您選擇 Microsoft Exchange 整合選項，就可以使用 Exchange 2013 原則和設定來控制這些使用者的 Lync Server 2013 資料封存。

  - **使用 Lync Server 封存資料庫進行封存。**如果您的使用者並未位於 Exchange 2013 或他們的信箱狀態不是 \[就地保留\]，或者如果您不想針對部署中的任何或所有使用者使用 Microsoft Exchange 整合，則您可以使用 SQL Server 來部署 Lync Server 封存資料庫，以儲存這些使用者的封存資料。在此情況下，Lync Server 2013 封存原則和設定會決定是否要啟用封存及實作封存的方式。若要使用 Lync Server 2013，您必須將適當的 SQL Server 資料庫新增至您的拓撲並發行該拓撲。

## 使用 Microsoft Exchange 整合時進行封存設定

如果您的使用者位於 Exchange 2013 且其信箱的狀態為 \[就地保留\]，則您可以選擇 \[Microsoft Exchange 整合\] 選項 (如本節稍後所述)，為這些使用者封存 Lync Server 2013，接著可以指定 Exchange 就地保留原則和設定，以及 Lync Server 設定來控制這些使用者的封存功能，以控制下列動作：

  - 是否要封存 IM、會議或兩者。

  - 是否要針對您的 Lync Server 部署實作關鍵模式。

  - 選取 Microsoft Exchange 整合選項，以使用 Exchange 2013 來儲存封存的資料。

這些 Lync Server 2013 封存設定選項將於本節後續內容中加以說明。如需關於如何設定 Exchange 就地保留原則與設定以支援封存的資訊，請參閱 Exchange 2013 產品文件。

## 使用 Lync Server 封存資料庫儲存時進行封存設定

如果您想要使用 Lync Server 封存資料庫 (使用 SQL Server 資料庫) 來為部署中的所有使用者封存資料，您可以設定 Lync Server 封存原則，以控制是否要針對這些使用者啟用封存。在每個封存原則中，您可以針對下列其中一項或兩項來啟用或停用封存：

  - 內部通訊

  - 外部通訊

依預設，不會針對任何 Lync Server 封存原則中的內部通訊或外部通訊啟用封存。您可以使用 Lync Server 2013 控制台或使用 Lync Server 2013 管理命令介面中的 Cmdlet ，來啟用或停用通訊。

Lync Server 2013 封存原則包含下列項目：

  - **全域封存原則**。此為預設的封存原則，可以套用至您的整個部署。它是在您部署 Lync Server 2013 時所建立，並且預設會針對內部與外部通訊停用封存。您無法刪除此原則。如果您選擇刪除選項，即會將全域原則重設為預設設定。

  - **網站封存原則**。您可以選擇性地為一或多個指定網站啟用或停用封存，作法是針對該網站建立和設定網站層級的封存原則。當您建立網站層級的封存原則時，預設不會啟用封存。您可以刪除任何您建立之網站層級的封存原則。網站層級的封存原則優先於全域原則，但僅適用於原則中指定的網站。例如，如果您在全域原則中針對內部與外部通訊啟用封存，然後建立一個網站原則以針對外部通訊停用封存，則只會針對該網站封存內部通訊。

  - **使用者封存原則**。您可以選擇性地為一或多個特定使用者或使用者群組啟用或停用封存，作法是為指定的使用者和使用者群組建立、設定及套用使用者層級的封存原則。當您建立使用者層級的封存原則時，預設不會啟用封存。您可以刪除任何您建立之使用者層級的封存原則，而且可以變更要套用封存原則的使用者與使用者群組。使用者層級的封存原則優先於全域原則及所有網站原則，但僅適用於套用原則的使用者和使用者群組。例如，如果您在全域原則中針對內部與外部通訊停用封存、建立一個網站層級的原則以針對內部與外部通訊啟用封存，然後建立一個使用者層級的原則以針對外部通訊停用封存，則系統將針對所有網站使用者的外部與內部通訊封存通訊，但您套用使用者層級原則的使用者例外，只會為他們封存內部通訊。

如需有關如何在部署封存時設定內部封存原則的詳細資訊，請參閱部署文件中的[設定和指派封存原則](lync-server-2013-configuring-and-assigning-archiving-policies.md)。如需有關在部署之後使用封存原則來啟用和停用通訊的詳細資訊，請參閱作業文件中的[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您實作這兩個 Lync Server 2013 封存資料庫並啟用 Microsoft Exchange 整合，Exchange 2013 原則就會優先於 Lync Server 封存原則，但僅限於 Exchange 2013 中信箱狀態為 [就地保留] 的使用者。Lync 封存僅會根據 Microsoft Exchange 就地保留原則而定。</td>
</tr>
</tbody>
</table>


## 我可以使用哪些選項來設定封存？

除了使用原則及啟用與停用封存，您還有其他封存選項可用來為整個部署進行設定，而且可以選擇性地針對特定的網站與集區進行設定。您可以使用一或多個封存設定 (位於 Lync Server 2013 控制台中) 來設定大部分的封存選項，但是也有其他選項只有在使用 Lync Server 2013 管理命令介面進行設定時才能使用。

## Lync Server 2013 控制台中的封存設定選項

每個封存設定都會提供下列選項：

部署封存時會自動建立全域層級的設定，全域層級的設定可加以設定，但不能刪除。如果您選取選項來刪除全域設定，即會將設定重設為預設值。您可以建立多個網站與集區設定，與全域設定一起使用來控制封存設定。針對全域設定及每個台站與集區設定，您會有下列選項：

  - 停用封存、僅針對立即訊息 (IM) 啟用封存，或者針對 IM 和會議啟用封存

  - 設定關鍵模式，在發生 Lync Server 失敗時封存 IM 和會議工作階段。失敗包含下列項目：
    
      - **IM**。Lync Server 儲存服務發生問題。在此情況下，會針對已啟用封存的使用者封鎖 IM。
    
      - **會議**。失敗可能是無法使用的檔案共用，或是儲存服務發生問題。在此情況下，所有失敗時於集區中舉行的作用中會議都會切換為限制模式，並且無法啟動新會議。
    
    IM 和會議會在更正失敗之後自動復原。

  - 指定使用 Microsoft Exchange Server 2013 整合，使用 Exchange 2013 來儲存封存的資料，而不是設定個別的 SQL Server 資料庫來儲存 Lync Server 2013 封存資料。

  - 設定封存資料的清除選項。這包含指定何時清除封存的資料，可以是下列其中一項：
    
      - 在您指定的特定天數之後
    
      - 在匯出封存資料之後 (這包括已上傳至 Exchange 的資料 (如果您啟用了 Microsoft Exchange 整合))。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您啟用 Microsoft Exchange 整合，則針對位於 Exchange 2013 且其信箱狀態為 [就地保留] 的使用者進行清除的動作是由 Exchange 來控制。唯一的資格是適用於會議檔案，這些檔案儲存於 Lync Server 檔案共用中。如果您選取選項要在匯出封存資料之後清除資料，則只有在將檔案匯出 (上傳至 Exchange) 之後，才會從檔案共用中清除這些檔案，或者，如果您指定要保留的天數上限，則會在指定的天數上限之後清除檔案。</td>
    </tr>
    </tbody>
    </table>


預設不會啟用任何封存選項。您可以使用 Lync Server 2013 控制台來管理封存設定。

您可以指定下列封存設定：

  - **全域封存設定**。此為預設的封存設定，可套用至您的整個部署。它是在您部署 Lync Server 2013 時所建立，而且預設不會啟用封存功能。您可以修改全域設定，但無法刪除它。如果您針對設定選擇刪除選項，即會將全域設定重設為預設設定。

  - **網站封存設定**。您可以選擇性地為一或多個指定的網站設定封存，作法是針對個別網站建立和設定網站層級的封存設定。網站層級的封存設定只有在您建立它時才會存在。您可以修改或刪除任何網站層級的封存設定。網站層級的封存設定優先於全域設定，但僅適用於網站層級設定中指定的網站。例如，如果您在全域設定中僅針對 IM 啟用封存，並建立一個網站設定以針對 IM 和會議啟用封存，則只會針對該網站封存會議，而不會為貴組織的其餘部分封存會議。

  - **集區封存設定**。您可以選擇性地為一或多個指定的集區指定封存設定，作法是為個別集區建立和設定集區層級的設定。集區層級的封存設定只有在您建立它時才會存在。您可以修改和刪除任何集區層級的封存設定。集區層級的封存設定優先於全域設定，以及您可能已建立的任何網站封存設定。例如，如果您在全域設定中僅針對 IM 啟用封存，並建立一個網站層級的設定以針對該網站的 IM 和會議啟用封存，接著建立一個集區層級的設定以便僅針對 IM 啟用封存，則會針對網站的所有使用者封存 IM 與會議的通訊，但位於集區層級設定中指定之集區中的使用者例外。針對組織中所有的其他使用者，就只會針對 IM 啟用封存。

如需有關如何在部署封存時設定最初封存設定的詳細資訊，請參閱部署文件中的[設定封存選項](lync-server-2013-configuring-archiving-options.md)。如需有關在部署之後使用封存原則來啟用和停用通訊的詳細資訊，請參閱作業文件中的[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)。

## 僅能在 Windows PowerShell 中使用的封存選項

使用 Lync Server 2013 管理命令介面，您可以使用 Cmdlet，來實作 Lync Server 2013 控制台中所沒有的選項。這些選項包括下列各項：

  - **封存重複的訊息**。如需詳細資訊，請參閱作業文件中的 [New-CsArchivingConfiguration](new-csarchivingconfiguration.md) 和 [Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)。

  - **匯出封存的資料**。如需詳細資訊，請參閱 [Export-CsArchivingData](export-csarchivingdata.md)

## 如何存取封存的資料？

存取封存的資料會根據儲存資料的地方而定：

  - **Microsoft Exchange 儲存**。如果您選擇 Exchange 整合選項，Lync Server 便會為位於 Exchange 2013 的所有使用者和其信箱狀態為 \[就地保留\] 的所有使用者，在 Exchange 2013 存放區中儲放封存內容。封存的資料會儲存於使用者信箱的可復原項目資料夾下方，使用者通常不會看見此資料夾，只有具備 Exchange**探索管理**角色的使用者可以搜尋此資料夾。Exchange 會啟用同盟的搜尋與探索以及 SharePoint (如果已部署)。如需更多有關儲存、保留及探索 Exchange 中所儲存之資料的詳細資訊，請參閱＜Exchange 2013＞及＜SharePoint＞文件。

  - **Lync Server 儲存**。如果您設定 Lync Server 2013 封存資料庫來儲存 Lync Server 資料，Lync Server 會針對位於 Exchange 2013 的所有使用者和其信箱狀態不是 \[就地保留\] 的所有使用者，在 Lync Server 封存資料庫 (SQL Server 資料庫) 中儲放封存內容。此資料是無法搜尋的，但可匯出為可使用其他工具搜尋的格式。如需有關匯出封存資料庫中所儲存之資料的詳細資訊，請參閱作業文件中的[從 Lync Server 2013 匯出封存資料](lync-server-2013-exporting-archived-data.md)。

如需有關 Lync Server 2013 和 Exchange 2013 如何一起運作的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中的 Exchange Server 與 SharePoint 整合支援](lync-server-2013-exchange-and-sharepoint-integration-support.md)。

