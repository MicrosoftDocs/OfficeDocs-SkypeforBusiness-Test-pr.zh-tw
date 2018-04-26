---
title: Lync Server 2013：主控 Exchange 使用者管理
TOCTitle: 主控 Exchange 使用者管理
ms:assetid: e8723af5-0604-4d7d-bad2-463a9832efb4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399037(v=OCS.15)
ms:contentKeyID: 49292667
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主控 Exchange 使用者管理

 

_**上次修改主題的時間：** 2015-03-09_

若要提供語音信箱服務給 Lync Server 2013 使用者，且該使用者的信箱位在裝載的 Exchange 服務上，則您必須為裝載的語音信箱啟用其使用者帳戶。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您可以為 Lync Server 2013 使用者啟用裝載的語音信箱之前，必須部署套用至對應使用者帳戶的裝載語音信箱原則。原則的範圍可以是全域、網站或個別使用者，只要適用於您要啟用的使用者即可。如需詳細資訊，請參閱＜ <a href="lync-server-2013-hosted-voice-mail-policies.md">Lync Server 2013 中的主控語音信箱原則</a>＞。</td>
</tr>
</tbody>
</table>


## msExchUCVoiceMailSettings 屬性

Lync Server 2013 引進名為 **msExchUCVoiceMailSettings** 的新使用者屬性，該屬性是做為 Lync Server 2013 Active Directory 架構準備的一部分所建立。此多重值屬性會保留語音信箱設定，且這些設定是由 Lync Server 2013 和裝載的 Exchange 服務所共用。

在某些情況下，裝載的 Exchange 服務會在啟用 Exchange UM 的程序中，或是將信箱傳輸至裝載的 Exchange Server 期間，設定 msExchUCVoiceMailSettings 屬性的值。如果 Exchange 未設定這個屬性， Lync Server 2013 系統管理員必須執行 Set-CsUser Cmdlet 來設定它，如本主題稍早所述。

屬性的索引鍵/值組及其作者在下表中顯示。

### msExchUCVoiceMailSettings 屬性索引鍵/值組

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>作者</th>
<th>意義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeHostedVoiceMail=1</p></td>
<td><p>Exchange</p></td>
<td><p>Exchange Server 已啟用使用者的裝載 UM 存取。 Exchange UM 路由應用程式會檢查使用者的裝載語音信箱原則，以取得路由詳細資料。</p></td>
</tr>
<tr class="even">
<td><p>ExchangeHostedVoiceMail=0</p></td>
<td><p>Exchange</p></td>
<td><p>Exchange Server 已停用使用者的裝載 UM 存取。</p></td>
</tr>
<tr class="odd">
<td><p>CsHostedVoiceMail=1</p></td>
<td><p>Lync Server</p></td>
<td><p>Lync Server 2013 已啟用使用者的裝載 UM 存取。 Lync Server 2013 ExUM 路由應用程式會檢查使用者的裝載語音信箱原則，以取得路由詳細資料。</p></td>
</tr>
<tr class="even">
<td><p>CsHostedVoiceMail=0</p></td>
<td><p>Lync Server</p></td>
<td><p>Lync Server 2013 已停用使用者的裝載 UM 存取。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果屬性已經有值，且該值不是 Lync Server 2013 索引鍵/值組的其中一個 (CSHostedVoiceMail=0 或 CSHostedVoiceMail=1)，則會出現警告，指出屬性可能由不同的應用程式所管理。例如，如果索引鍵/值組 ExchangeHostedVoiceMail=0 或 ExchangeHostedVoiceMail=1 已存在，則會顯示警告。在此情況下，您可以在 Active Directory 中進行編輯以變更該值，或是執行下列 Cmdlet 以將值設為 Null：<br />
Set-CsUser –identity user –HostedVoicemail $null</td>
</tr>
</tbody>
</table>


## 為使用者啟用裝載的語音信箱

若要讓使用者的語音信箱呼叫可路由傳送至裝載的 Exchange UM，您必須執行 Set-CsUser Cmdlet，以設定 *HostedVoiceMail* 參數的值。此參數也會以訊號通知 Lync Server 2013，以亮起「撥打語音信箱」指示燈。

  - 下列範例會為 Pilar Ackerman 的使用者帳戶啟用裝載的語音信箱：
    
        Set-CsUser -Identity "Pilar Ackerman" -HostedVoiceMail $True
    
    Cmdlet 會確認裝載的語音信箱原則 (全域、網站層級、個別使用者) 適用於這個使用者。如果沒有任何原則適用，則 Cmdlet 會失敗。

  - 下列範例會為 Pilar Ackerman 的使用者帳戶停用裝載的語音信箱：
    
        Set-CsUser -Identity "Pilar Ackerman" -HostedVoiceMail $False
    
    Cmdlet 會確認沒有任何裝載的語音信箱原則 (全域、網站層級、個別使用者) 適用於這個使用者。如果有原則可適用，則 Cmdlet 會失敗。

如需使用 Set-CsUser Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件。

