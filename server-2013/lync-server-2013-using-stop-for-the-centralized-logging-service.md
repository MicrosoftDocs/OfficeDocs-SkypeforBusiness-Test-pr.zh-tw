---
title: 將 Stop 用於集中式記錄服務
TOCTitle: 將 Stop 用於集中式記錄服務
ms:assetid: 09ac093e-8f30-4874-84b4-12548ac8c898
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687964(v=OCS.15)
ms:contentKeyID: 49889933
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Stop 用於集中式記錄服務

 

_**上次修改主題的時間：** 2012-11-01_

您可以用 Stop-CsClsLogging Cmdlet 來停止目前執行中的記錄工作階段。一般來說，並沒有很多狀況會需要停止記錄工作階段。例如，您不需要先停止記錄，就可以搜尋記錄及變更設定。如果您有兩個案例正在執行，例如 AlwaysOn 和 UserReplicator，而您需要收集有關驗證的資訊，則必須先停止其中一個案例 (在全域、網站、集區或電腦範圍)，才能開始執行驗證案例。如需詳細資訊，請參閱＜[Stop-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging)＞。

> [!NOTE]
> 在判斷您可以在給定的部署部署、集區或電腦上執行哪些案例時，必須記得您有「每部電腦」只能執行兩個案例的限制。如果您要在集區上記錄活動，則應將集區當做單一實體來處理。在大部分情況下，在集區中的每部電腦上執行不同的案例並沒有意義。但是查看您收集資料的相關問題，並思考在整體部署中，哪個案例對給定電腦的影響最大，這就有意義了。例如，您想想 UserReplicator 案例，在 Edge Server 或 Edge 集區上執行 UserReplicator 就沒有什麼價值。<br />
> 在了解問題及影響的範圍之後，應謹慎選擇要在哪些電腦和集區上執行什麼案例。雖然 AlwaysOn 案例對大範圍的應用有意義，因為它會收集各種提供者的資訊，但是特定案例對特定電腦或集區只有應用價值。此外，在未了解給定案例的價值之前，就隨機啟動記錄工作階段的話，要特別小心。如果您使用錯誤的案例，或是所使用的案例適合該工作，而您將案例套用在錯誤的範圍 (可能是全域、網站、集區或電腦)，所得到的問題資料可能不是很有用，就像根本沒有執行案例一樣。


若要使用 Lync Server 管理命令介面來控制集中記錄服務功能，您必須是 CsAdministrator 或 CsServerAdministrator 角色型存取控制 (RBAC) 安全性群組成員，或是包含上述其中一個群組的自訂 RBAC 角色。若要傳回所有獲指派此 Cmdlet 的 RBAC 角色清單 (包括您自行建立的任何自訂 RBAC 角色)，請從 Lync Server 管理命令介面或 Windows PowerShell 提示字元執行下列命令：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

例如：

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

## 停止目前執行中的集中記錄服務工作階段

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  輸入下列命令來查詢集中記錄服務，以了解目前正在執行哪些案例：
    
        Show-CsClsLogging
    
    ![呼叫 Show-CsCl 之後的 Windows PowerShell 主控台](images/JJ687964.eb190c32-529c-4277-a731-52c47d22d8fa(OCS.15).jpg "呼叫 Show-CsCl 之後的 Windows PowerShell 主控台")
    
    Show-CsClsLogging 的結果是執行中案例及其執行範圍的摘要。如需詳細資訊，請參閱＜[Show-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Show-CsClsLogging)＞。

3.  若要停止使用特定案例的目前執行中記錄工作階段，請輸入：
    
        Stop-CsClsLogging -Scenario <scenario name> -Computers <comma separated list of fully qualified computer names> -Pools <comma separated list of fully qualified pool names>
    
    例如：
    
        Stop-CsClsLogging -Scenario UserReplicator -Pools pool01.contoso.net
    
    此命令將會停止 pool01.contoso.net 上使用 UserReplicatior 案例的記錄。
    
    > [!NOTE]  
    > 在此記錄工作階段期間，使用 UserReplicator 案例來建立的記錄並不會刪除。您還是可以使用該記錄來執行使用 Search-CsClsLogging 命令的搜尋作業。如需詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Search-CsClsLogging">Search-CsClsLogging</a>＞。
    


Stop-CsClsLogging Cmdlet 與 Start-CsClsLogging 搭配使用時，會結束記錄工作階段 (由案例定義)，並保留記錄工作階段所建立的記錄。您隨時都可以在給定的電腦上執行兩個案例。用一個案例停止另一個案例來收集資訊的方法，是在大部分工作量疑難排解期間都可以執行的常用工作。

## 請參閱

#### 工作

[將 Start 用於集中式記錄服務以擷取記錄](lync-server-2013-using-start-for-the-centralized-logging-service-to-capture-logs.md)  

#### 概念

[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)  

#### 其他資源

[Show-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Show-CsClsLogging)  
[Start-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Start-CsClsLogging)  
[Stop-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging)

