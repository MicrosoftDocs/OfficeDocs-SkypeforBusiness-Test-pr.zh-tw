---
title: 設定集中式記錄服務的提供者
TOCTitle: 設定集中式記錄服務的提供者
ms:assetid: 6a197ecf-b56b-45e0-8e7c-f532ec5164ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688082(v=OCS.15)
ms:contentKeyID: 49890102
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定集中式記錄服務的提供者

 

_**上次修改主題的時間：** 2014-03-19_

在集中記錄服務中，*提供者*為亟需掌握之最重要的觀念和設定。*提供者*直接對應至 Lync Server 追蹤模式中的 Lync Server 伺服器角色元件。提供者會定義受追蹤的 Lync Server 2013 元件、需收集的訊息類型 (例如嚴重、錯誤或警告) 和旗標 (例如 TF\_Connection 或 TF\_Diag)。提供者是每個 Lync Server 伺服器角色中可追蹤的元件。藉由使用提供者，可讓您定義在元件上追蹤的層級和類型 (例如 S4、SIPStack、IM 和目前狀態)。定義的提供者會用於案例中，以針對處理特定問題狀況的某個邏輯集合來對所有提供者進行分組。

若要使用Lync Server 管理命令介面執行集中記錄服務功能，您必須是 CsAdministrator 或 CsServerAdministrator 角色型存取控制 (RBAC) 安全性群組成員，或是包含這兩個群組之一的自訂 RBAC 角色。當此 Cmdlet 已指派給角色型存取控制 (RBAC) 角色，若要傳回所有其清單 (包括您自行建立的任何自訂 RBAC 角色)，請執行來自Lync Server 管理命令介面或 Windows PowerShell 提示的下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

例如：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

本主題的其餘內容將特別針對定義提供者、修改提供者的方式，及提供者定義所包含的內容做討論，以使您的疑難排解作業獲得最佳成效。發行集中記錄服務命令有兩種方式。您可以使用 CLSController.exe，其預設位置為目錄 C:\\Program Files\\Common Files\\Microsoft Lync Server 2013\\CLSAgent。或者，您可使用Lync Server 管理命令介面來發行 Windows PowerShell 命令。其中重要區別在於，當您在命令列上使用 CLSController.exe 時，選擇會侷限於提供者已定義好而無法變更的可用案例中，但您可以定義記錄層級。藉由使用 Windows PowerShell，您就可定義新的提供者，以在您的記錄工作階段中使用，並對其建立作業、其收集內容、其收集資料的層級擁有完整控制權。

> [!IMPORTANT]
> 如前所述，提供者的功能強大。不過，案例的作用卻更為強大，因為它們包含全部所需具體資訊，可用以在提供者代表的元件上設定和執行追蹤作業。若與做為提供者集合的案例進行約略比較，它就像執行包含數百個命令的批次檔，可用來收集大量資訊，而非在命令列上以一次一個的方式發行數百個命令。<br />
> 您無需深入發掘提供者的詳細資料，集中記錄服務會提供許多已為您定義好的案例。所提供的案例涵蓋您可能會遭遇的絕大多數問題。在一些罕見的情況下，您可能需建立並定義提供者，並將其指派給案例。我們強烈建議您在調查需求以建立新提供者和案例前，先熟悉所提供的每個案例。您可在這裡找到建立提供者的資訊，以熟悉案例使用提供者元素收集追蹤資訊的方式，而此時並不會提供提供者本身的詳細資料。


如同在[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)中的介紹，定義使用者以供案例之用時，其主要元素為：

  - **提供者** 如果您熟悉 OCSLogger，提供者是您選擇的元件，可用來告訴 OCSLogger 追蹤引擎應當從何處目收集記錄。提供者為相同的元件，且在許多情況下，皆具有與 OCSLogger 之元件相同的名稱。如果您不熟悉 OCSLogger，提供者則是特定伺服器角色元件，集中記錄服務可從那裏收集記錄。在集中記錄服務的情況中，CLSAgent 是集中記錄服務的架構部分，該服務會針對您在提供者設定中定義的元件進行追蹤。

  - **記錄層次** OCSLogger 提供選項，以針對所收集的資料選擇數個層次的詳細資料。此功能是集中記錄服務和案例不可或缺的一部分，且受 **Type** 參數所定義。您可以選擇下列項目：
    
      - **全部** 針對已定義的提供者，收集類型為嚴重、錯誤、警告和記錄資訊的追蹤訊息。
    
      - **嚴重** 針對已定義的提供者，僅收集表示失敗的追蹤訊息。
    
      - **錯誤** 針對已定義的提供者，僅收集表示錯誤的追蹤訊息以及嚴重訊息。
    
      - **警告** 針對已定義的提供者，僅收集表示警告的追蹤訊息以及嚴重和錯誤訊息。
    
      - **資訊資訊** 針對已定義的提供者，僅收集表示資訊訊息的追蹤訊息以及嚴重、錯誤和警告訊息。
    
      - **詳細資訊**   針對已定義的提供者，收集類型為嚴重、錯誤、警告和資訊的所有追蹤訊息。

  - **旗標** OCSLogger 提供的選項，以針對每個提供者選擇旗標，可定義您可以從追蹤檔案中擷取什麼類型的資訊。您可以依據提供者選擇下列旗標：
    
      - **TF\_Connection** 提供連線相關記錄項目。這些記錄包括為連入和連出特定元件所建立之連線的資訊。其中可能也包括重要網路層級資訊 (即針對不具連線概念的元件)。
    
      - **TF\_Security** 提供有關安全性的所有事件/記錄項目。例如對 SipStack 而言，這些是網域驗證失敗和用戶端驗證/授權失敗等安全性事件。
    
      - **TF\_Diag** 提供診斷事件，您可用以診斷或疑難排解元件。例如對 SipStack 而言，這些是憑證失敗或 DNS 警告/錯誤。
    
      - **TF\_Protocol** 提供 SIP 和 CCCP 訊息等通訊協定訊息。
    
      - **TF\_Component** 可登入指定做為提供者的一部分的元件。
    
      - **全部** 設定可供提供者使用的所有可用旗標。

## 檢視現有集中記錄服務案例提供者的資訊

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  若要檢視現有提供者的設定，請輸入下列項目：
    
        Get-CsClsScenario -Identity <scope and scenario name>
    
    例如，若要檢視全域會議服務員的資訊，請輸入：
    
        Get-CsClsScenario -Identity "global/CAA"
    
    命令會顯示內含相關旗標、設定和元件的提供者清單。如果所顯示的資訊不足，或清單對預設的 Windows PowerShell 清單格式而言過長，您就可以定義其他輸出方法以顯示額外資訊。若要進行這項作業，請輸入：
    
        Get-CsClsScenario -Identity "global/CAA" | Select-Object -ExpandProperty Provider
    
    此命令的輸出會以五行的格式顯示每名提供者，其中包含提供者名稱、記錄類型、記錄層次、旗標、GUID 和角色，每個項目位於個別一行。

## 定義新的集中記錄服務案例提供者

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  案例提供者是由待追蹤的元件、要使用的旗標和收集的詳細資料等級所組成。若要進行這項作業，請輸入：
    
        $<variableName> = New-CsClsProvider -Name <provider component> -Type <log type> -Level <log level detail type> -Flags <provider trace log flags>
    
    例如，追蹤提供者的定義會定義收集的項目及來自如下所示之 Lyss 提供者的詳細資料層級：
    
        $LyssProvider = New-CsClsProvider -Name "Lyss" -Type "WPP" -Level "Info" -Flags "All"

–Level 會收集嚴重、錯誤、警告和資訊訊息。使用的旗標為針對 Lyss 提供者定義的所有旗標，並包括 TF\_Connection、TF\_Diag 和 TF\_Protocol。

在定義變數 $LyssProvider 之後，您可以透過 **New-CsClsScenario** Cmdlet 加以使用，以便收集來自 Lyss 提供者的追蹤。若要完成建立提供者，或將其指派給新案例，請輸入：

    New-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider $LyssProvider

當中的 $LyssProvider 是變數，其中包含與 **New-CsClsProvider** 一起建立之已定義的案例。

## 變更現有的集中記錄服務案例提供者

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  若要更新或變更現有提供者的設定，請輸入：
    
        $LyssProvider = New-CsClsProvider -Name "Lyss" -Type "WPP" -Level "Debug" -Flags "TF_Connection, TF_Diag"
    
    然後您可輸入下列項目來更新案例，以指派提供者：
    
        Set-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider $LyssProvider

命令的最終結果是，案例 site:Redmond/RedmondLyssInfo 會有更新的旗標和層級供指派給案例的提供者使用。您可以使用 Get-CsClsScenario 檢視新案例。如需詳細資訊，請參閱 [Get-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsScenario)。

> [!WARNING]
> <strong>New-ClsCsProvider</strong> 不會進行檢查來決定旗標是否有效。請確認旗標的拼字 (例如 TF_DIAG 或 TF_CONNECTION) 正確無誤。如果旗標的拼字不正確，提供者就無法傳回預期的記錄資訊。


如果您想要將其他提供者新增至此案例，請輸入下列項目：

    Set-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider @{Add=$ABSProvider, $CASProvider, S4Provider}

在那裏，使用「新增」指示詞加以定義的每個提供者，都已經使用 **New-CsClsProvider** 程序加以定義。

## 移除案例提供者

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  所提供的 Cmdlet 可讓您新增現有的提供者以及建立新的提供者。若要移除提供者，您必須針對 **Set-CsClsScenario** 的 Provider 參數使用 Replace 指示詞。完全移除提供者的唯一方式，是以相同名稱之重新定義的提供者來加以取代，並使用 Update 指示詞。例如，我們的提供者 LyssProvider 使用 WPP 定義為記錄類型，等級設為 Debug，旗標組為 TF\_CONNECTION 和 TF\_DIAG。您需將旗標變更為“All”。若要變更提供者，請輸入下列項目：
    
    ```
    $LyssProvider = New-CsClsProvider -Name "Lyss" -Type "WPP" -Level "Debug" -Flags "All"
    ```
    ```
    Set-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider @{Replace=$LyssProvider}
    ```

3.  若要完全移除某案例和與其相關的提供者，請輸入下列項目：
    
        Remove-CsClsScenario -Identity <scope and name of scenario>
    
    例如：
    
        Remove-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo"
    
    > [!WARNING]
    > Cmdlet <strong>Remove-CsClsScenario</strong> 不會提示您進行確認。案例會連同指派給它的提供者一併遭刪除。您可以重新執行一開始用來建立案例的命令以重新建立案例。您無法還原遭移除的案例或提供者。


在使用 **Remove-CsClsScenario** Cmdlet 移除案例時，您可以將案例從範圍完全移除。若要使用您建立的案例，及使用做為案例之一部分的提供者，您需建立新的提供者，並將其指派給新的案例。

## 請參閱

#### 其他資源

[Get-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsScenario)  
[New-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsScenario)  
[Remove-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClsScenario)  
[Set-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsScenario)  
[New-CsClsProvider](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsProvider)

