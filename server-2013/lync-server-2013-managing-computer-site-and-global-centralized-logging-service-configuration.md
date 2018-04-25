---
title: 管理電腦、網站及全域集中式記錄服務組態
TOCTitle: 管理電腦、網站及全域集中式記錄服務組態
ms:assetid: 93b9a354-9aea-4b3a-a4fe-68a89f436196
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688138(v=OCS.15)
ms:contentKeyID: 49890214
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理電腦、網站及全域集中式記錄服務組態

 

_**上次修改主題的時間：** 2014-02-04_

集中記錄服務可以在包含單一電腦的範圍、一個電腦集區、網站範圍 (亦即已定義的網站 (例如 Redmond 網站)，其中會在您的部署中包含電腦與集區的集合)，或者全域範圍 (亦即部署中的所有電腦與集區) 上執行。

若要使用 Lync Server 管理命令介面設定集中記錄服務範圍，您必須是 CsAdministrator 或 CsServerAdministrator 角色型存取控制 (RBAC) 安全性群組的成員，或是包含這兩個群組之一的自訂 RBAC 角色。為了傳回所有 RBAC 角色的清單，已指派此 Cmdlet (包含任何您自行建立的自訂 RBAC 角色)，從 Lync Server 管理命令介面或 Windows PowerShell 提示中執行下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "<Lync Server 2013 cmdlet>"}

例如：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows PowerShell 會為您提供更多無法使用 CLSController.exe 來取得的選項和其他設定選項。CLSController 提供一個快速且明確的方法來執行命令，但會限制為可供 CLSController 使用的命令組。Windows PowerShell 不會只限制在可供 CLSController 之命令處理器使用的命令，並提供一組範圍更廣泛的命令和一組更豐富的選項。例如，CLSController.exe 會為您提供適用於 –computers 和 –pools 的範圍選項。利用 Windows PowerShell，您可以在大部分的命令中指出電腦或集區，而且在您定義新案例時 (CLSController 中使用者無法修改的案例數目有限)，可以定義網站或全域範圍。這個功能強大的 Windows PowerShell 功能讓您能夠將案例定義為網站或全域範圍，但可將實際記錄限制為電腦或集區。<br />
您可在 Windows PowerShell 或 CLSController 中執行的命令列命令間有一些基本差異。Windows PowerShell 可提供一個豐富的方法來設定和定義案例，並針對您的疑難排解案例，以有意義的方式重複使用這些案例。當 CLSController 提供一個快速且有效率的方式來發出命令並取得結果時，針對 CLSController 設定的命令會受到您可以從命令列取得的有限命令所限制。不同於 Windows PowerShell Cmdlet，CLSController 無法定義新案例、在網站或全域層級管理範圍，以及許多無法動態設定之有限命令組的其他限制。儘管 CLSController 提供可用來快速執行的工具時，Windows PowerShell 也會提供工具來延伸 集中記錄服務 功能範圍，而此範圍可能會超越 CLSController。</td>
</tr>
</tbody>
</table>


單一電腦範圍可以在使用 –Computers 參數來執行 [Search-CsClsLogging](search-csclslogging.md)、[Show-CsClsLogging](show-csclslogging.md)、[Start-CsClsLogging](start-csclslogging.md)、[Stop-CsClsLogging](stop-csclslogging.md)、[Sync-CsClsLogging](sync-csclslogging.md) 及 [Update-CsClsLogging](update-csclslogging.md) 命令時進行定義。–Computers 參數會接受適用於目標電腦的完整網域名稱 (FQDN) 清單 (以逗號分隔)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以定義 –Pools 和以逗號分隔的集區清單，而您會想要在其上執行記錄命令。</td>
</tr>
</tbody>
</table>


網站和全域範圍均定義於 **New-**、**Set-** 及 **Remove-**集中記錄服務 Cmdlet 中。下列範例示範如何設定網站和全域範圍。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>顯示的命令可能包含其他小節中所涵蓋的參數和概念。範例命令可以用來示範如何使用 <strong>–Identity</strong> 參數來定義範圍，而包含其他參數能讓範例更完整且可指定範圍。如需關於 <strong>Set-CsClsConfiguration</strong> Cmdlet 的詳細資訊，請參閱作業文件中的 <a href="set-csclsconfiguration.md">Set-CsClsConfiguration</a>。</td>
</tr>
</tbody>
</table>


## 擷取目前的 集中記錄服務 設定

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        Get-CsClsConfiguration

使用 **New-CsClsConfiguration** 和 **Set-CsClsConfiguration** Cmdlet，來建立新設定或更新現有的設定。

當您執行 **Get-CsClsConfiguration** 時，它會顯示類似下列螢幕擷取畫面的資訊，其中的部署目前具備預設的全域設定，但未定義任何網站設定：

![Get-CsClsConfiguration 輸出範例。](images/JJ688029.23f98ddc-fc48-499a-b6c5-752611f2a0b0(OCS.15).jpg "Get-CsClsConfiguration 輸出範例。")

## 從電腦本機存放區擷取目前的 集中記錄服務 設定

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        Get-CsClsConfiguration -LocalStore

當您使用第一個範例時 (其中的 **Get-CsClsConfiguration** 未指定任何參數)，此命令會針對資料參考中央管理存放區。如果您指定參數 –LocalStore，則此命令會參考電腦 LocalStore，而不是中央管理存放區。

## 擷取目前定義的案例清單

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        Get-CsClsConfiguration -Identity <scope and name> | Select-Object -ExpandProperty Scenarios
    
    例如，若要擷取定義於全域範圍上的案例：
    
        Get-CsClsConfiguration -Identity "global" | Select-Object -ExpandProperty Scenarios

**Get-CsClsConfiguration** Cmdlet 一律會顯示屬於指定範圍設定一部分的案例。在大部分情況下，不會顯示所有的案例，並會加以截斷。此處所使用的命令會列出所有案例和部分相關資訊，例如，使用了哪些提供者、設定及旗標。

## 使用 Windows PowerShell 更新集中記錄服務的全域範圍

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        Set-CsClsConfiguration -Identity <scope> -EtlFileRolloverSizeMB <size for logging file in megabytes>
    
    例如：
    
        Set-CsClsConfiguration -Identity "global" -EtlFileRolloverSizeMB 40

此命令會告知部署中每個電腦和集區上的 CLSAgent，將追蹤檔上變換值的大小設定為 40 MB。所有網站上的電腦和集區都會受到此命令所影響，且會將它們設定的追蹤記錄變換值設定為 40 MB。

## 使用 Windows PowerShell 更新集中記錄服務的網站範圍

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        Set-CsClsConfiguration -Identity <scope/site name> -EtlFileRolloverSizeMB <size for logging file in megabytes> -EtlFileFolder <default location %TEMP%\Tracing>
    
    例如：
    
        Set-CsClsConfiguration -Identity "site/Redmond" -EtlFileRolloverSizeMB 40 -EtlFileFolder "C:\LogFiles\Tracing" 
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如範例中所述，記錄檔的預設位置為 %TEMP%\Tracing。但是，由於它實際上是正在寫入檔案的 CLSAgent 且 CSLAgent 會以網路服務形式來執行，所以 %TEMP% 變數會延伸至 %WINDIR%\ServiceProfiles\NetworkService\AppData\Local。</td>
    </tr>
    </tbody>
    </table>


此命令會告知 Redmond 網站中每個電腦和集區上的 CLSAgent，將追蹤檔上變換值的大小設定為 40 MB。其他網站上電腦和集區將不會受到此命令所影響，並且將繼續使用目前設定的追蹤記錄變換值，此值是預設定義 (20 MB) 或在記錄工作階段開始期間所定義。

## 建立新的集中記錄服務設定

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        New-CsClsConfiguration -Identity <scope and name> [CsClsConfiguration options for this site]
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>New-CsClsConfiguration 讓使用者可以存取大量的選用組態設定。如需關於設定選項的詳細資訊，請參閱 <a href="get-csclsconfiguration.md">Get-CsClsConfiguration</a> 和<a href="lync-server-2013-understanding-centralized-logging-service-configuration-settings.md">瞭解集中式記錄服務組態設定</a>。</td>
    </tr>
    </tbody>
    </table>
    
    例如，若要建立新設定來定義適用於快取檔案的網路資料夾、記錄檔的變換期間，以及記錄檔的變換大小，您可以輸入：
    
        New-CsClsConfiguration -Identity "site:Redmond" -CacheFileNetworkFolder "\\fs01.contoso.net\filestore\logfiles" -EtlFileRolloverMinutes 120 -EtlFileRolloverSizeMB 40

您應該謹慎規劃新設定的建立，以及如何為集中記錄服務定義新內容。您應該留意進行變更的相關資訊，並確定您了解能夠適當記錄問題案例的影響。您應該進行設定變更，這將增強您的能力，有利於管理記錄的大小，以及在發生問題時允許解決問題的變換期間。

## 移除現有的集中記錄服務設定

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在命令列提示上輸入下列命令：
    
        Remove-CsClsConfiguration -Identity <scope and name>
    
    例如，若要移除您建立來提高記錄檔變換時間的集中記錄服務設定，可增加變換記錄檔大小，並將記錄檔快取位置設定為檔案共用，如下所示：
    
        Remove-CsClsConfiguration -Identity "site:Redmond"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此為在＜建立新的集中記錄服務設定＞程序中所建立的新設定。</td>
    </tr>
    </tbody>
    </table>


如果您選擇移除網站層級的設定，網站將使用全域設定。

## 請參閱

#### 概念

[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)  

#### 其他資源

[使用 PowerShell 管理集中式記錄服務組態設定](lync-server-2013-managing-the-centralized-logging-service-configuration-settings.md)  
[Set-CsClsConfiguration](set-csclsconfiguration.md)  
[Get-CsClsConfiguration](get-csclsconfiguration.md)  
[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Remove-CsClsConfiguration](remove-csclsconfiguration.md)

