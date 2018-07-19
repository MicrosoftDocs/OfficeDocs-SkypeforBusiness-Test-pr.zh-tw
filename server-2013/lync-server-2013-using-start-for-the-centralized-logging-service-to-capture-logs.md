---
title: 將 Start 用於集中式記錄服務以擷取記錄
TOCTitle: 將 Start 用於集中式記錄服務以擷取記錄
ms:assetid: 0512b9ce-7f5b-48eb-a79e-f3498bacf2de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687958(v=OCS.15)
ms:contentKeyID: 49889924
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Start 用於集中式記錄服務以擷取記錄

 

_**上次修改主題的時間：** 2013-02-21_

若要使用集中記錄服務擷取追蹤記錄，請發出命令，在一或多部電腦和集區上開始記錄。您也可以發出參數，定義要記錄的電腦或集區、要執行的案例 (例如，AlwaysOn、其他預先定義的案例或已建立的案例)，以及要追蹤的 Lync Server 元件 (例如，S4、SipStack)。

為了擷取正確的資訊，您必須確定使用正確的案例來收集問題的相關資訊。在集中記錄服務中，案例是指根據收集的伺服器元件、記錄層次及旗標啟動記錄的概念，這麼做比必須在個別伺服器上定義這些元素更有效率且更有用。您可以定義及指定要執行的案例，這些案例會在基礎結構範圍內的所有伺服器和集區上持續執行。

預設案例稱為 **AlwaysOn**。AlwaysOn 的預定目的是持續執行案例 (如案例名稱所指)。AlwaysOn 案例針對許多最常見的伺服器元件，收集資訊層級的資訊 (請注意，資訊記錄層次除了資訊訊息之外，還包含 \[嚴重\]、\[錯誤\] 及 \[警告\])。AlwaysOn 會收集發生問題前後及期間的資訊。這與之前的記錄工具 (例如 OCSLogger) 的一般行為大不相同。您會在發生問題之後執行 OCSLogger，這讓疑難排解工作更加困難，因為您擁有的資料只會被動回應，而無法主動解決問題。如果 AlwaysOn 所包含的資訊，不是您想要指向問題元件及指出修正步驟的資訊 (在 AlwaysOn 提供者的深度和廣度下，此情形並不常見)，AlwaysOn 會指出合理的資訊層級，以決定必須執行的其他動作，例如建立新的案例、收集其他資訊、執行其他搜尋以收集更集中的詳細資料等。

集中記錄服務提供兩種發出命令的方式。目前有一些主題是關於如何透過 Lync Server 管理命令介面使用 Windows PowerShell。集中記錄服務偏好使用 Windows PowerShell 的原因，是因為能夠使用許多複雜的設定和命令。由於透過 Lync Server 管理命令介面使用 Windows PowerShell 幾乎會用到 Lync Server的所有功能，因此將只討論 Windows PowerShell 命令。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果決定從命令列使用一組有限的可用命令，可輸入 <code>ClsController.exe</code> 取得 CLSController.exe 的協助。預設會將 <strong>ClsController.exe</strong> 安裝在下列目錄： C:\Program Files\Microsoft Lync Server 2013\ClsAgent。</td>
</tr>
</tbody>
</table>


## 使用 Windows PowerShell 搭配基本命令執行 Start-CsClsLogging

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  若要啟動集中記錄服務的記錄案例，請輸入下列命令：
    
        Start-CsClsLogging -Scenario <name of scenario>
    
    例如，若要啟動 **AlwaysOn** 案例，請輸入：
    
        Start-CsClsLogging -Scenario AlwaysOn
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>AlwaysOn 案例沒有預設期間。此案例會一直執行，直到您使用 <strong>Stop-CsClsLogging</strong> Cmdlet 明確加以停止。如需詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging">Stop-CsClsLogging</a>＞。其他所有案例的預設期間為 4 小時。</td>
    </tr>
    </tbody>
    </table>


3.  按 Enter 鍵執行命令。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可能需要一點時間 (30 到 60 秒) 才能執行命令，並接收部署中的電腦傳回的狀態。</td>
    </tr>
    </tbody>
    </table>
    
    ![執行 Start-CsClsLogging。](images/JJ687958.c5be7413-8cef-4de7-9712-944d20cc2fa4(OCS.15).jpg "執行 Start-CsClsLogging。")

4.  若要啟動其他案例，請如下所示使用 **Start-CsClsLogging** Cmdlet，並提供要執行的其他案例名稱 (例如「驗證」案例)：
    
        Start-CsClsLogging -Scenario Authentication
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在任何時候，最多可以在任何指定的電腦上執行兩個案例。如果命令的範圍為全域，部署中的所有電腦都會執行這些案例。若要啟動第三個案例，您必須從要執行新案例的電腦、集區、網站或全域範圍停止記錄。如果已啟動全域範圍，您可以在一或多部電腦和集區上停止記錄一或兩個案例。如需管理執行案例的詳細資訊，請參閱＜<a href="lync-server-2013-using-stop-for-the-centralized-logging-service.md">將 Stop 用於集中式記錄服務</a>＞及＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging">Stop-CsClsLogging</a>＞。</td>
    </tr>
    </tbody>
    </table>


## 使用 Windows PowerShell 搭配進階命令執行 Start-CsClsLogging

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  您還可使用其他參數管理記錄命令。–Duration 可用於調整執行案例的時間長度；–Computers 還可定義電腦完整網域名稱 (FQDN) 的清單 (以逗號分隔)；或–Pools 可定義要執行記錄之集區的 FQDN 清單 (以逗號分隔)。
    
    在集區 "pool01.contoso.net" 上啟動 *UserReplicator* 案例的記錄工作階段，並將記錄工作階段期間定義為 8 小時。若要執行這項操作，請輸入：
    
        Start-CsClsLogging -Scenario UserReplicator -Duration 8:00 -Pools "pool01.contoso.net"
    
    成功執行此案例會傳回類似如下的結果：
    
    ![執行 Start-CsClsLogging。](images/JJ687958.399f0c2e-c08c-40ab-b6c6-381dddc12fe9(OCS.15).jpg "執行 Start-CsClsLogging。")
    
    請注意，在此範例中，AlwaysOn 案例和 UserReplicator 案例都在執行中。

## 請參閱

#### 概念

[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)

