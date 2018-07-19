---
title: 設定監看員節點測試使用者及組態設定
TOCTitle: 設定監看員節點測試使用者及組態設定
ms:assetid: ab00e9cb-f539-4aa6-bcb4-5533fbe7bc44
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205152(v=OCS.15)
ms:contentKeyID: 49291957
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定監看員節點測試使用者及組態設定

 

_**上次修改主題的時間：** 2013-07-29_

設定將作為監看員節點的電腦之後您必須進行下列動作：

1.  建立監看員節點使用的測試帳戶。如果您使用 Negotiate 驗證方法，您也必須使用 [Set-CsTestUserCredential](https://docs.microsoft.com/en-us/powershell/module/skype/) Cmdlet 來啟用要在監看員節點上使用的這些測試帳戶。

2.  更新監看員節點設定。

本章節將說明：

  - 設定測試使用者帳戶

  - 使用預設綜合交易來設定基本監看員節點

  - 設定擴充測試

  - 新增與移除綜合交易

  - 檢視與測試監看員節點設定

## 設定測試使用者帳戶

測試使用者不一定代表真實的人員，但是他們必須為有效的 Active Directory 網域服務 帳戶；此外，這些帳戶必須啟用 Lync Server 2013、必須具有有效的 SIP 位址，且他們應該啟用企業語音 (以使用 Test-CsPstnPeerToPeerCall 綜合交易)。如果您使用 TrustedServer 驗證方式，您所需要做的就是確定這些帳戶存在，且依此處所指定的進行設定。您應該為想要測試的每個集區指派至少 3 個測試使用者。

如果您使用 Negotiate 驗證方法，您也必須使用 **Set-CsTestUserCredential** Cmdlet 與 Lync Server 管理命令介面，讓這些測試帳戶使用綜合交易。只要執行類似以下的命令即可。(這些命令假設您已建立 3 個 Active Directory 使用者帳戶，且這些帳戶已啟用 Lync Server 2013。)：

    Set-CsTestUserCredential -SipAddress "sip:watcher1@litwareinc.com" -UserName "litwareinc\watcher1" -Password "P@ssw0rd"
    Set-CsTestUserCredential -SipAddress "sip:watcher2@litwareinc.com" -UserName "litwareinc\watcher2" -Password "P@ssw0rd"
    Set-CsTestUserCredential -SipAddress "sip:watcher3@litwareinc.com" -UserName "litwareinc\watcher3" -Password "P@ssw0rd"

請注意，您必須同時包含 SIP 位址與使用者名稱和密碼。如果您未包含密碼，Set-CsTestUserCredential 會提示您輸入密碼資訊。可使用上面顯示的「網域名稱\\使用者名稱」格式來指定使用者名稱，或使用「使用者名稱@網域名稱」格式；例如：

    -UserName "watcher3@litwareinc.com"

若要驗證測試使用者認證已建立，請從 Lync Server 管理命令介面執行這些命令：

    Get-CsTestUserCredential -SipAddress "sip:watcher1@litwareinc.com"
    Get-CsTestUserCredential -SipAddress "sip:watcher2@litwareinc.com"
    Get-CsTestUserCredential -SipAddress "sip:watcher3@litwareinc.com"

應將此類似資訊傳回給每位使用者：

    UserName                        Password
    --------                        --------
    Litwareinc\watcher1              System.Security.SecureString

## 使用預設綜合交易來設定基本監看員節點

建立測試使用者之後，您可使用類似以下的命令來建立監看員節點：

    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers @{Add= "sip:watcher1@litwareinc.com","sip:watcher2@litwareinc.com", "sip:watcher3@litwareinc.com"}

這個命令會建立使用預設設定的新監看員節點，並執行預設的綜合交易組。新監看員節點也會使用測試使用者 watcher1@litwareinc.com、watcher2@litwareinc.com 與 watcher3@litwareinc.com。如果監看員節點使用 TrustedServer 驗證，則這 3 個測試帳戶可以是任何啟用 Active Directory 與 Lync Server 的有效使用者帳戶。如果監看員節點使用 Negotiate 驗證方法，則您也必須使用 **Set-CsTestUserCredential** Cmdlet 來啟用監看員節點的使用者帳戶。

## 設定擴充測試

如果您想啟用公用交換電話網路 (PSTN 測試) 來驗證公用交換電話網路的連線，在設定監看員節點時，您必須進行一些額外設定。首先，您需要將測試使用者與 PSTN 測試類型關聯。若要這樣做，請從 Lync Server 管理命令介面 執行類似以下的命令：

    $pstnTest = New-CsExtendedTest -TestUsers "sip:watcher1@litwareinc.com", "sip:watcher2@litwareinc.com", "sip:watcher3@litwareinc.com"  -Name "Contoso Provider Test" -TestType PSTN

請注意，必須將此命令的結果儲存為變數。在此範例中，結果是名為 $pstnTest 的變數。

此時，您可使用 **New-CsWatcherNodeConfiguration** Cmdlet 將測試類型 (儲存為 $pstnTest 變數) 關聯至 Lync Server 2013 集區。例如，下列命令會為 atl-cs-001.litwareinc.com 集區建立新監看員節點設定、新增之前已建立的 3 個測試使用者，並新增 PSTN 測試類型：

    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers @{Add= "sip:watcher1@litwareinc.com","sip:watcher2@litwareinc.com", "sip:watcher3@litwareinc.com"} -ExtendedTests @{Add=$pstnTest}

請注意，若未在監看員節點電腦上安裝 Lync Server 核心檔案與 RTCLocal 資料庫，上述命令會失敗。

若要測試多個語音原則，您必須使用 **New-CsExtendedTest** Cmdlet 為每個原則建立一個擴充測試。應使用想要的語音原則來設定指派到此測試的使用者。然後使用類似以下的命令將擴充測試傳遞到 **New-CsWatcherNodeConfiguration** Cmdlet：

    -ExtendedTests @{Add=$pstnTest1,$pstnTest2,$pstnTest3}

如果不使用 Tests 參數呼叫 New-CsWatcherNodeConfiguration，這表示只會為新監看員節點啟用「預設」綜合交易 (與指定的擴充綜合交易)。這表示監看員節點將測試下列元件：

  - 登錄

  - IM

  - GroupIM

  - P2PAV (對等音訊/視訊工作階段)

  - AvConference (音訊/會議)

  - 目前狀態

  - ABS (通訊錄服務)

  - ABWQ (通訊錄網頁服務)

  - PSTN (PSTN 閘道呼叫、指定為擴充測試。依預設會停用 PSTN。因為該命令使用 ExtendedTests 參數來啟用 PSTN，所以才會在此案例中啟用測試。)

這也表示預設不會測試下列元件：

  - AVEdgeConnectivity

  - MCXP2PIM (行動裝置立即訊息)

  - ExumConnectivity (Exchange Unified Messaging)

  - JoinLauncher

  - PersistentChatMessage

  - DataConference

  - XmppIM

  - UnifiedContactStore

## 新增與移除綜合交易

監看員節點設定後，您可使用 **Set-CsWatcherNodeConfiguration** Cmdlet 從節點新增或移除綜合交易。例如，若要將 PersistentChatMessage 測試新增至監看員節點，請使用 Add 方法與類似以下的命令：

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Add="PersistentChatMessage"}

可使用逗號分隔多個測試名稱來新增多個測試。例如：

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Add="PersistentChatMessage","DataConference","UnifiedContactStore"}

請注意，如果已在監看員節點上啟用以上一或多個測試 (例如，DataConference)，則會發生錯誤。在此案例中，您會收到類似以下的錯誤訊息：

    Set-CsWatcherNodeConfiguration : 'urn:schema:Microsoft.Rtc.Management.Settings.WatcherNode.2010:TestName' 索引鍵或唯一識別條件約束中有重複的索引鍵順序 'DataConference'。

當此錯誤發生時，將不會套用任何變更。應移除重複的測試來重新執行命令。

若要從監看員節點移除綜合交易，請使用 Remove 方法，而不要使用 Add 方法。例如，以下命令會從監看員節點移除 ABWQ 測試：

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Remove="ABWQ"}

您也可以使用 Replace 方法，以一或多個新測試來取代目前啟用的所有測試。例如，如果您只想要監看員節點執行 IM 測試，您可使用以下命令進行設定：

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -Tests @{Replace="IM"}

當您執行上述命令時，將會停用指定監看員節點上的所有綜合交易，除了 IM 之外。

## 檢視與測試監看員節點設定

如果您想要檢視已指派給監看員節點的測試，請使用類似以下的命令：

    Get-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" | Select-Object -ExpandProperty Tests

上述命令將根據指派給節點的綜合交易，傳回類似以下的資訊：

    Registration
    IM
    GroupIM
    P2PAV
    AvConference
    Presence
    PersistentChatMessage
    DataConference

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要以字母順序檢視綜合交易，請改用以下命令：<br />
Get-CsWatcherNodeConfiguration –Identity &quot;atl-cs-001.litwareinc.com&quot; | Select-Object –ExpandProperty Tests | Sort-Object</td>
</tr>
</tbody>
</table>


若要確認監看員節點已建立，請從 Lync Server 管理命令介面輸入下列命令：

    Get-CsWatcherNodeConfiguration

您會收到類似以下的資訊：

    Identity      : atl-cs-001.litwareinc.com
    TestUsers     : {sip:watcher1@litwareinc.com, sip:watcher2@litwareinc.com ...}
    ExtendedTests : {TestUsers=IList<System.String>;Name=PSTN Test; Te...}
    TargetFqdn    : atl-cs-001.litwareinc.com
    PortNumber    : 5061

若要確認已正確設定監看員節點，請從 Lync Server 管理命令介面輸入下列命令：

    Test-CsWatcherNodeConfiguration

上述命令會測試您部署中的每一個監看員節點，並提供以下資訊：

  - 是否已安裝登錄器角色。

  - 當您執行 Set-CsWatcherNodeConfiguration 時，是否為您建立所需的登錄機碼。

  - 您的伺服器是否執行正確的 Lync Server 版本。

  - 是否正確設定連接埠。

  - 指派的測試使用者是否擁有必要的認證。

