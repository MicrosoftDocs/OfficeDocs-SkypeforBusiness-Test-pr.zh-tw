---
title: 設定 Lync Server 2013 使用 Microsoft Exchange Server 2013 Archiving
TOCTitle: 設定 Lync Server 2013 使用 Exchange Server 2013 Archiving
ms:assetid: 260346d1-edc8-4a0c-8ad2-6c2401c3c377
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ679896(v=OCS.15)
ms:contentKeyID: 49889982
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Microsoft Lync Server 2013 使用 Microsoft Exchange Server 2013 Archiving

 

_**上次修改主題的時間：** 2014-06-24_

Microsoft Lync Server 2013 可提供系統管理員選項，以將立即訊息和 Web 會議記錄封存至使用者的 Microsoft Exchange Server 2013 信箱，而非 SQL Server 資料庫。若您啟用了此選項，系統就會將記錄寫入使用者信箱的「清理」資料夾。「清理」資料夾是「可復原項目」資料夾中的隱藏資料夾。雖然使用者看不到這個資料夾，但該資料夾是透過 Exchange 搜尋引擎來編制索引，因此可使用 Exchange 信箱搜尋及/或 Microsoft SharePoint Server 2013 來探索此資料夾。由於這些資訊是儲存在 Exchange 就地保留功能 (用於封存電子郵件和其他 Exchange 通訊) 所使用的相同資料夾中，系統管理員即可使用單一工具來搜尋針對某使用者所封存的所有電子通訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要完全停用 Lync 交談的封存，您必須同時停用 Lync 交談記錄。如需詳細資訊，請參閱下列主題：<a href="lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md">在 Lync Server 2013 中管理內部與外部通訊的封存</a>、<a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy">New-CsClientPolicy</a> 和 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy">Set-CsClientPolicy</a>。</td>
</tr>
</tbody>
</table>


若要將記錄封存到 Exchange 2013，您必須先設定好兩部伺服器間的伺服器對伺服器驗證。設定好伺服器對伺服器驗證後，即可在 Microsoft Lync Server 2013 中執行下列作業 (請注意，依據您的設定和組態而定，您可能並不需要完成下列所有作業)：

1.  修改 Lync Server 封存設定，以啟用 Exchange 封存。所有部署都必須進行此步驟。

2.  針對使用者的內部及/或外部通訊，啟用封存。所有部署都必須進行此步驟。

3.  針對每個使用者設定 ExchangeArchivingPolicy 屬性。僅有當 Lync Server 和 Exchange 位於不同樹系中時，需要進行此步驟。

## 步驟 1：啟用 Exchange 封存

Lync Server 中的封存主要是使用封存組態設定來管理。在安裝 Lync Server 2013 時，系統會自動提供您這些設定的單一全域集合。(系統管理員可以選擇性地在網站範圍建立封存組態的新集合。) 根據預設，全域設定不會啟用封存，這些設定中也不會啟用 Exchange 封存。為了使用 Exchange 封存，系統管理員必須在這些組態設定中設定 EnableArchiving 和 EnableExchangeArchiving 屬性。EnableArchiving 屬性可設定為下列三個可能值之一：

  - **None** ，會停用封存。此為預設值。若 EnableArchiving 設為 None，則 Lync Server 封存資料庫或 Exchange 2013 中都不會進行任何封存。

  - **ImOnly** ，僅會封存立即訊息記錄。若啟用 Exchange 封存，就會將這些記錄封存到 Exchange 2013。若停用 Exchange 封存，就會這些記錄封存至 Lync Server。

  - **ImAndWebConf** ，會封存立即訊息記錄和 Web 會議記錄。若啟用 Exchange 封存，就會將這些記錄封存到 Exchange 2013。若停用 Exchange 封存，就會這些記錄封存至 Lync Server。

EnableExchangeArchiving 屬性為布林值：將 EnableExchangeArchiving 設為 True ($True) 可啟用 Exchange 封存，而將 EnableExchangeArchiving 設為 False ($False) 可停用 Exchange 封存。例如，此命令可啟用立即訊息記錄的封存，並啟用 Exchange 封存：

    Set-CsArchivingConfiguration -Identity "global" -EnableArchiving ImOnly -EnableExchangeArchiving $True

若要停用 Exchange 封存，請使用類似如下的命令，其可啟用立即訊息封存，但會停用封存至 Exchange (也就是說，記錄會封存至 Lync Server)：

    Set-CsArchivingConfiguration -Identity "global" -EnableArchiving ImOnly -EnableExchangeArchiving $False

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若 EnableArchiving 屬性是設為 None， Lync Server 就完全不會封存立即訊息和 Web 會議。在這種情況下，伺服器會忽略 EnableExchangeArchiving 所設定的值。</td>
</tr>
</tbody>
</table>


您也可使用 Lync Server 控制台來啟用或停用 Exchange 封存。若要執行這項作業，請完成下列程序：

1.  在控制台中，按一下 \[監控和封存\] ，然後按一下 \[封存組態\] 。

2.  在 \[封存組態\] 索引標籤中，按兩下要修改的封存設定集合 (例如，\[全域\] 集合)。

3.  在 \[編輯封存設定\] 窗格中，按一下 \[封存設定\] 下拉式清單，然後選取 \[封存 IM 工作階段\] (若只要封存立即訊息工作階段) 或 \[封存 IM 和 Web 會議工作階段\] (若要封存立即訊息和 Web 會議工作階段)。

4.  選擇好要封存的項目之後，選取 \[Exchange 伺服器整合\] 核取方塊，以啟用 Exchange 封存。若要停用 Exchange 封存，則清除此核取方塊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若 [封存設定] 是設為 [停用封存] ，就無法使用 [Exchange 伺服器整合] 核取方塊。您必須先啟用封存，然後再啟用 Exchange 封存。</td>
</tr>
</tbody>
</table>


若 Lync Server 2013 和 Exchange 2013 是位於相同的樹系中，則個別使用者的封存 (或至少具備 Exchange 2013 電子郵件帳號的使用者) 是使用 Exchange 就地保留原則來加以管理。若您的使用者是位於舊版的 Exchange，這些使用者的封存是使用 Lync Server 封存原則來管理。請注意，僅有具備 Exchange 2013 帳戶的使用者可以將 Lync 記錄封存至 Exchange。

若 Lync Server 2013 和 Exchange 2013 是位於不同的樹系，則個別使用者的封存是透過針對個別使用者帳戶設定 ExchangeArchivingPolicy 屬性來加以管理。請參閱「步驟 3」以了解詳細資訊。

## 步驟 2：啟用內部及/或外部通訊的封存

在啟用封存 (以及 Exchange 封存) 之後，您接著必須修改適當的封存原則，以確保使用者作業階段都有實際受到封存。請注意，僅啟用封存 (步驟 1) 並不會讓 Lync Server 開始封存立即訊息和 Web 會議記錄，您必須使用封存原則才能確保內部及/或外部封存。安裝 Lync Server 2013 時，您也會安裝包含下列兩個屬性的單一全域封存原則：

  - **ArchiveInternal** ，若設為 True ($True) 表示會封存內部通訊工作階段 (僅涉及組織中具備 Active Directory 帳戶之使用者的工作階段)。

  - **ArchiveExternal** ，若設為 True ($True) 表示會封存內部通訊工作階段 (涉及組織中至少有一名具備 Active Directory 帳戶之使用者的工作階段)。

根據預設，這兩個選項值都會設為 False，亦即不論內部或外部通訊工作階段都不會受到封存。若要修改全域原則，您可使用 Lync Server 管理命令介面和 Set-CsArchivingPolicy Cmdlet。此命令可啟用內部和外部通訊工作階段的封存：

    Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $True -ArchiveExternal $True

您也可以在網站範圍或個別使用者範圍，使用 New-CsArchivingPolicy 來建立新的原則。例如，此命令會建立名為 RedmondArchivingPolicy 的新個別使用者封存原則：

    New-CsArchivingPolicy -Identity "RedmondArchivingPolicy" -ArchiveInternal $True -ArchiveExternal $True

若您要建立個別使用者的原則，您就需要將該原則指派給適當的使用者。例如：

    Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName  "RedmondArchivingPolicy"

您也可使用 Lync Server 控制台來管理封存原則。在控制台中，按一下 \[監控和封存\] ，然後按一下 \[封存原則\] 。若要修改現有的原則，按兩下原則 (例如：全域)，然後在 \[編輯封存原則\] 窗格中，視需要選取或清除 \[封存內部通訊\] 和 \[封存外部通訊\] 核取方塊。若要建立新的封存原則，請按一下 \[新增\] ，然後選取 \[站台原則\] 或 \[使用者原則\] 。若您建立新的使用者原則，接著就必須存取適當的使用者帳戶 (從 \[使用者\] 索引標籤)，然後再將新的原則指派給這些使用者。

## 步驟 3：設定 ExchangeArchivingPolicy 屬性

若 Lync Server 2013 和 Exchange 2013 位於不同的樹系，僅在封存組態設定中啟用 Exchange 封存是不夠的，這樣並不會將立即訊息和 Web 會議記錄封存至 Exchange。您還必須在每個相關的 Lync Server 使用者帳戶上設定 ExchangeArchivingPolicy 屬性。您可將此屬性設為下列四個可能值之一：

1.  Uninitialized，指出封存會以使用者 Exchange 信箱所設定的就地保留設定為依據；若使用者信箱已啟用就地保留，使用者的訊息或 Web 會議記錄就會封存至 Lync Server。

2.  **UseLyncArchivingPolicy** ，指出使用者的立即訊息或 Web 會議記錄會封存至 Lync Server 而不是 Exchange。

3.  **NoArchiving** ，指出完全不會封存使用者的立即訊息或 Web 會議記錄。請注意，此設定會覆寫指派至使用者的 Lync Server 封存原則。

4.  **ArchivingToExchange** ，指出使用者的立即訊息或 Web 會議記錄會封存至 Exchange，不論是否有 (或沒有) 將就地保留設定指派給使用者的信箱皆然。

例如，若要設定使用者帳戶，以一律將立即訊息或 Web 會議記錄封存至 Exchange，您可從 Lync Server 管理命令介面使用類似下列的命令：

    Set-CsUser -Identity "Ken Myer" -ExchangeArchivingPolicy ArchivingToExchange

若您想針對群組使用者 (例如，所有位於特定登錄器集區的使用者) 設定相同的封存原則，可使用類似下列的命令：

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Set-CsUser -ExchangeArchivingPolicy ArchivingToExchange

請注意，要設定 ExchangeArchivingPolicy 屬性的值，您必須使用 Lync Server 管理命令介面 (和 Windows PowerShell)。因為，對系統管理員來說，此屬性不會在 Lync Server 控制台中顯示出來。

若您要檢視已指派特定封存原則之所有使用者的清單，您就可以使用類似下列的命令，即可傳回已將 ExchangeArchivingPolicy 屬性設為 Uninitialized 之所有使用者的 Active Directory 顯示名稱：

    Get-CsUser | Where-Object {$_.ExchangeArchivingPolicy -eq "Uninitialized"} | Select-Object DisplayName

同樣地，此命令會傳回已將 ExchangeArchivingPolicy 屬性設為 UseLyncArchivingPolicy 之使用者的顯示名稱：

    Get-CsUser | Where-Object {$_.ExchangeArchivingPolicy -ne "UseLyncArchivingPolicy"} | Select-Object DisplayName

