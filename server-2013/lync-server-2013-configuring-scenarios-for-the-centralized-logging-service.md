---
title: 設定集中式記錄服務的案例
TOCTitle: 設定集中式記錄服務的案例
ms:assetid: 6c3bf826-e7fd-4002-95dc-01020641ef01
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688085(v=OCS.15)
ms:contentKeyID: 49890106
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定集中式記錄服務的案例

 

_**上次修改主題的時間：** 2014-02-05_

案例會定義範圍 (亦即全域、網站、集區或電腦) 及在集中記錄服務中需使用的提供者。藉由使用案例，您可啟用或停用對提供者的追蹤作業 (例如 S4、SIPStack、IM 和目前狀態)。透過設定案例，您可針對處理特定問題條件的特定邏輯集合來為所有提供者進行分類。如果您發現需修改案例以滿足疑難排解和記錄需求，Lync Server 2013「偵錯工具」可提供名為 *ClsController.psm1* 的 Windows PowerShell 模組，其中包含名為 *Edit-CsClsScenario* 的功能。模組的目的在於編輯已命名案例的屬性。在本主題中會提供此模組運作方式的範例。Lync Server 2013「偵錯工具」可從下列連結下載：[http://go.microsoft.com/fwlink/?LinkId=285257](http://go.microsoft.com/fwlink/?linkid=285257)

> [!IMPORTANT]  
> 針對任何特定範圍 (網站、全域、集區或電腦)，您可在任何特定時間執行最多兩個案例。若要判斷哪些案例目前正在執行，請使用 Windows PowerShell 和 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsScenario">Get-CsClsScenario</a>。透過使用 Windows PowerShell 和 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsScenario">Set-CsClsScenario</a>， 您可動態進行變更執行中的案例。您可在記錄工作階段期間修改執行中的案例，以便調整或微調您正在收集的資料及資料提供者的來源。



若要使用 Lync Server 管理命令介面執行集中記錄服務功能，您必須為 CsAdministrator 或 CsServerAdministrator 角色型存取控制 (RBAC) 安全性群組成員，或包含這兩個群組之一的自訂 RBAC 角色。此 Cmdlet 已指派給RBAC 角色清單，若要傳回所有這些 RBAC 角色清單 (包括您已自行建立的任何自訂 RBAC 角色)，請在 Lync Server 管理命令介面或 Windows PowerShell 提示時執行以下命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

例如：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

本主題的其餘內容會針對如何定義案例、修改案例、擷取正在執行的案例、移除案例和指定案例以包含用來最佳化疑難排解的項目特別加以說明。發行集中記錄服務命令有兩種方式。您可以使用 CLSController.exe，其預設位於目錄 C:\\Program Files\\Common Files\\Microsoft Lync Server 2013\\CLSAgent 中。或者，您可使用 Lync Server 管理命令介面來發行 Windows PowerShell 命令。其中重要的區別在於，當您在命令列上使用 CLSController.exe 時，可用的案例會有選擇上的限制。當您使用 Windows PowerShell 時，您可定義要用於記錄工作階段中的新案例。

如同在[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)中所介紹，案例具有以下元素：

  - **提供者** 如果您熟悉 OCSLogger，則提供者是您選擇的元件，用以告訴 OCSLogger 追蹤引擎該從哪個項目收集記錄。提供者是相同的元件，在許多情況下，也與 OCSLogger 中的元件擁有相同的名稱。如果您不熟悉 OCSLogger，則提供者是伺服器角色特定元件，集中記錄服務可從中收及記錄。如需提供者設定的詳細資訊，請參閱＜[設定集中式記錄服務的提供者](lync-server-2013-configuring-providers-for-centralized-logging-service.md)＞。

  - **身分識別** –Identity 參數會設定案例的範圍和名稱。例如，您可以設定「全域」範圍並以“LyssServiceScenario”來識別案例。當您將兩者結合時，您需定義身份識別 (例如“global/LyssServiceScenario”)。
    
    您可以選擇使用–Name 和–Parent 參數。您需定義 Name 參數來唯一識別案例。如果您使用 Name，您也必須使用 Parent 來將案例新增至全域或網站。
    
    > [!IMPORTANT]  
    > 如果您使用 Name 和 Parent 參數，您就無法使用<strong>–Identity</strong> 參數。
    


## 使用 New-CsClsScenario Cmdlet 建立新案例

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  若要針對記錄工作階段建立新案例，請使用 [New-CsClsProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsProvider) 並定義案例名稱 (亦即唯一識別案例的方式)。從 WPP (亦即 Windows 軟體追蹤前置處理器，此為預設)、EventLog (亦即 Windows 事件記錄格式) 或 IISLog (亦即以 IIS 記錄檔案格式為依據的 ASCII 格式檔案) 中選擇記錄格式類型。接著定義層次 (如同在本主題中的「記錄層次」下所定義) 和旗標 (如同在本主題中的「旗標」下所定義)。
    
    針對此範例案例，我們使用 LyssProvider 當作範例提供者變數。
    
    若要使用定義的選項建立案例，請鍵入：
    
        New-CsClsScenario -Identity <scope>/<unique scenario name> -Provider <provider variable>
    
    例如：
    
        New-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider $LyssProvider
    
    使用–Name 和–Parent 的替代格式：
    
        New-CsClsScenario -Name "LyssServiceScenario" -Parent "site:Redmond" -Provider $LyssProvider

## 使用 New-CsClsScenario Cmdlet 建立包含多個提供者的新案例

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  您有每個範圍兩個案例的限制。不過，您沒有設定提供者數目的限制。在此範例中，假設我們已建立三個提供者，且您想要將他們都指派給您正在定義的案例。提供者變數名稱是 LyssProvider、ABServerProvider 和 SIPStackProvider。若要定義多個提供者，並將其指派給案例，請在Lync Server 管理命令介面或 Windows PowerShell 命令提示鍵入下列項目：
    
        New-CsClsScenario -Identity "site:Redmond/CollectDataScenario" -Provider @{Add=$LyssProvider, $ABServerProvider,  $SIPStackProvider}
    
    > [!NOTE]  
    > 如同在 Windows PowerShell 中所知的，使用 <code>@{&lt;variable&gt;=&lt;value1&gt;, &lt;value2&gt;, &lt;value&gt;...}</code> 建立值的雜湊表格時，其所用慣例稱為<em>展開</em>。如需有關 Windows PowerShell 中展開的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=267760%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=267760&amp;clcid=0x404</a>。
    


## 使用 Set-CsClsScenario Cmdlet 修改現有案例

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  您有每個範圍兩個案例的限制。您可隨時變更執行中的案例，即使在記錄擷取工作階段進行時也可以。如果您重新定義正在執行的案例，目前的記錄工作階段會停止使用已移除的案例，然後開始使用新案例。不過，已移除案例的擷取記錄資料會留存在擷取記錄中。若要定義新案例，請執行下列動作 (亦即假設新增名為“S4Provider”之已定義的提供者)：
    
        Set-CsClsScenario -Identity <name of scope and scenario defined by New-CsClsScenario> -Provider @{Add=<new provider to add>}
    
    例如：
    
        Set-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider @{Add=$S4Provider}
    
    如果您想要取代提供者，請定義單一提供者或以逗號分隔的提供者清單以取代目前的組合。如果您僅想取代許多提供者之一，則將新提供者加入目前提供者，以建立新的提供者組合，而其中包含新提供者和現有提供者。若要以新的組合取代所有提供者，請鍵入下列項目：
    
        Set-CsClsScenario -Identity <name of scope and scenario defined by New-CsClsScenario> -Provider @{Replace=<providers to replace existing provider set>}
    
    例如，若要以 $LyssServiceProvider 取代目前的 $LyssProvider、$ABServerProvider 和 $SIPStackProvider 的組合：
    
        Set-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider @{Replace=$LyssServiceProvider}
    
    若僅要以 $LyssServiceProvider 取代目前 $LyssProvider、$ABServerProvider 和 $SIPStackProvider 組合中的 $LyssProvider 提供者，請鍵入下列項目：
    
        Set-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider @{Replace=$LyssServiceProvider, $ABServerProvider, $SIPStackProvider}

## 使用 Remove-CsClsScenario Cmdlet 移除現有案例

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  如果您想要移除先前定義的案例，請鍵入下列項目：
    
        Remove-CsClsScenario -Identity <name of scope and scenario>
    
    例如，若要移除已定義的案例 site:Redmond/LyssServiceScenario：
    
        Remove-CsClsScenario -Identity "site:Redmond/LyssServiceScenario"

**Remove-CsClsScenario** Cmdlet 會移除特定案例，但是記錄中仍存有已擷取的追蹤供您搜尋使用。

## 使用 ClsController.psm1 模組載入和卸載 Edit-CsClsScenario Cmdlet

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。
    
    > [!IMPORTANT]  
    > ClsController.psm1 模組可提供作為個別的 Web 下載項目。模組是 Lync Server 2013 偵錯工具的一部分。根據預設，偵錯工具會安裝於目錄 C:\Program Files\Lync Server 2013\Debugging Tools 中。
    


2.  在 Windows PowerShell 鍵入：
    
        Import-Module "C:\Program Files\Lync Server 2013\Debugging Tools\ClsController.psm1"
    
    > [!TIP]
    > 模組成功載入時，會使您返回 Windows PowerShell 命令提示字元。若要確認載入模組且 Edit-CsClsScenario 為可用，請鍵入 <code>Get-Help Edit-CsClsScenario</code>。您應參閱 EditCsClsScenario 語法基本概要。


3.  若要卸載模組，請鍵入：
    
        Remove-Module ClsController
    
    > [!TIP]
    > 模組成功卸載時，會使您返回 Windows PowerShell 命令提示字元。若要確認卸載模組，請鍵入 <code>Get-Help Edit-CsClsScenario</code>。Windows PowerShell 會嘗試尋找 Cmdlet 和失敗的說明。


## 使用 Edit-ClsController 模組從案例移除現有提供者

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  從 AlwaysOn 案例移除提供者，請鍵入：
    
        Edit-CsClsScenario -ScenarioName <string of the scenario to edit> -ProviderName <string of the provider to remove> -Remove
    
    例如：
    
        Edit-CsClsScenario -ScenarioName AlwaysOn -ProviderName ChatServer -Remove
    
    ScenarioName 和 ProviderName 參數是位置參數 (亦即這些參數須在命令列中預期的位置加以定義)。相對於 Cmdlet 的第一位置而言，如果案例名稱是在第二位置，而提供者在第三位置，則無須明確定義參數名稱。使用此資訊時，先前的命令會以下列項目鍵入：
    
        Edit-CsClsScenario AlwaysOn ChatServer -Remove
    
    參數值的位置放置僅適用於–Scenario 和–Provider。您必須明確定義所有其他參數。

## 使用 Edit-ClsController 模組將提供者新增至案例

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  若要將提供者新增至 AlwaysOn 案例，請鍵入：
    
        Edit-CsClsScenario -ScenarioName <string of the scenario to edit> -ProviderName <string of the provider to add> -Level <string of type level> -Flags <string of type flags>
    
    例如：
    
        Edit-CsClsScenario -ScenarioName AlwaysOn -ProviderName ChatServer -Level Info -Flags TF_COMPONENT
    
    \-Loglevel 可屬於以下類型：嚴重、錯誤、警告、資訊、詳細資訊、偵錯或全部。–Flags 可為提供者支援的任何旗標，例如 TF\_COMPONENT、TF\_DIAG。–Flags 也可為 ALL 值。
    
    您也可使用 Cmdlet 的位置功能鍵入先前的範例。例如，若要將提供者 ChatServer 新增至 AlwaysOn 案例，請鍵入：
    
        Edit-CsClsScenario AlwaysOn ChatServer -Level Info -Flags ALL

