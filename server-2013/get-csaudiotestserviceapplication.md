---
title: Get-CsAudioTestServiceApplication
TOCTitle: Get-CsAudioTestServiceApplication
ms:assetid: ef36a059-bf9b-4066-a817-db8d82c41e49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412984(v=OCS.15)
ms:contentKeyID: 49292746
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioTestServiceApplication

 

_**上次修改主題的時間：** 2015-03-09_

可讓您傳回組織所使用之音訊測試服務應用程式的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAudioTestServiceApplication [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

在範例 1 中，會呼叫不含任何額外參數的 **Get-CsAudioTestServiceApplication** Cmdlet，以傳回組織目前所使用之所有音訊測試服務連絡人的集合。

    Get-CsAudioTestServiceApplication

## 範例 2

範例 2 會傳回單一音訊測試服務連絡人：Identity 為 sip:RedmondAudioTest@litwareinc.com 的連絡人。

    Get-CsAudioTestServiceApplication -Identity "sip:RedmondAudioTest@litwareinc.com"

## 範例 3

範例 3 會傳回顯示名稱包含字串值 "Redmond" 的所有音訊測試服務連絡人。為達此目的，命令會使用 Filter 參數搭配篩選值 {DisplayName –like "\*Redmond\*"} (此篩選值可將傳回的資料限制在顯示名稱包含字串值 "Redmond" 的連絡人)。此命令會傳回具有下列顯示名稱的連絡人，例如 "Redmond Audio Test Service Contact"、"Redmond Audio Bot" 以及 "Test Contact for Redmond"。

    Get-CsAudioTestServiceApplication -Filter {DisplayName -like "*Redmond*"}

## 詳細描述

音訊測試服務可讓 Lync Server 使用者在進行語音通話之前測試其語音連線。為達此目的，使用者必須在 \[ Lync Server 選項\] 對話方塊中，按一下 \[音訊裝置\] 索引標籤上的 \[檢查通話品質\] 按鈕。當使用者按下此按鈕後，將會撥電話給自動音訊測試服務。來電將被接聽，並在播放一段介紹提示後，要求來電者錄製一段簡短訊息。接著會重新撥放該錄音，讓來電者利用有的連線試聽其聲音。

音訊測試服務在某種程度上會依賴 Active Directory 連絡人物件。當您安裝 Audio Bot 時，系統會為您自動建立這些物件；沒有其他方法可以手動建立這些物件。而系統管理員可以使用 **Get-CsAudioTestServiceApplication** 來擷取關於組織中目前使用之各種測試服務連絡人的資訊。系統管理員也可以使用 **Set-CsAudioTestServiceApplication**，來修改這些連絡人的內容。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAudioTestServiceApplication** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAudioTestServiceApplication"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您以替代認證來執行 Cmdlet。如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其完整網域名稱 (FQDN) (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制為擁有特定顯示名稱或使用特定語言的音訊測試連絡人物件。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只會傳回顯示名稱為「音訊測試服務連絡人」之連絡人的篩選看起來如下：DisplayName 代表 Active Directory 屬性；-eq 代表比較運算子 (等於)，而「音訊測試服務連絡人」代表篩選值：</p>
<p>-Filter {DisplayName -eq &quot;Audio Test Service Contact&quot;}</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>音訊測試服務連絡人的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您從特定 Active Directory 組織單位 (OU) 傳回連絡人。OU 參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU (如 AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回使用者。</p>
<p>指定 OU 時，請使用該容器的辨別名稱 (DN)；例如：-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制命令傳回的記錄數。例如，若要傳回七個使用者 (不考慮樹系中有多少使用者)，請加入 ResultSize 參數並將參數值設為 7。請注意，此法無法保證傳回哪七位使用者。如果您將 ResultSize 設為 7，但樹系中只有三個使用者，則命令會傳回這三個使用者，然後完成執行而不會出現錯誤。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsAudioTestServiceApplication** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsAudioTestServiceApplication](set-csaudiotestserviceapplication.md)

