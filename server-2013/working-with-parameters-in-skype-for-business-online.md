---
title: 使用參數
TOCTitle: 使用參數
ms:assetid: 29ebda0f-ae5f-4512-ad59-240c3605b240
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362778(v=OCS.15)
ms:contentKeyID: 56269075
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用參數

 

_**上次修改主題的時間：** 2015-06-22_

使用 Identity 參數時，您可能會發現參數值 kenmyer@litwareinc.com 包含在雙引號內：

    -Identity "kenmyer@litwareinc.com"

Windows PowerShell 的新手難免會有不知何時應使用雙引號的疑惑。這個問題沒有直接明瞭的解答，但有一定的規矩可循：

  - 如果參數值為數字，通常不需使用雙引號。例如，若要限制 [Get-CsOnlineUser](get-csonlineuser.md) Cmdlet 所傳回的使用者數，請使用下列語法：
    
        -ResultSize 100
    
    事實上，數字旁均不應加上雙引號。如果有加，Windows PowerShell 可能無法將該值解譯為數字。
    
    同樣地，請確認數字中並無包含逗號。例如，若要將結果大小設為 10,000，以下語法是錯誤示範：
    
        -ResultSize 10,000
    
    此語法將會產生錯誤，因為 Windows PowerShell 是以逗號分隔引數值。在此情況下，Windows PowerShell 將假定您所傳遞的是兩個不同的參數值：10 與 000。因為您無法將結果大小同時設為 10 與 0，所以會發生錯誤。請改為使用下列沒有逗號的語法：
    
        -ResultSize 10000

  - 如果參數值為日期，通常也不需使用雙引號：
    
        -StartDate 6/1/2013
    
    然而，這只有在時間未包含在內時才適用。如有包含時間 (亦即在日期與時間之間放上空格)，則參數值必須加上雙引號：
    
        -StartDate "6/1/2013 10:00AM"
    
    注意，上述命令的格式是針對地區設定使用美式英文的電腦。若是使用的並非美式英文，您應根據自己電腦的設定採取正確的日期與時間格式。若要檢查 Windows PowerShell 所使用的地區設定，請透過 Windows PowerShell 命令提示字元執行下列命令：
    
        Get-Host | Select-Object CurrentUICulture

  - 字串值 (例如人員姓名) 通常不需使用雙引號，然而主要的例外狀況發生在字串值包含限制字元的情形，例如空格、逗號或其他標點符號。例如，下列語法之所以可行，是因為使用者的身分識別並未包含任何限制字元：
    
        -Identity "kenmyer@litwareinc.com"
    
    然而，下列命令將會因為 Identity 包含空格而失敗：
    
        -Identity Ken Myer
    
    上述命令失敗的原因在於 Windows PowerShell 使用空格分隔不同的參數。這代表 Windows PowerShell 會因此認為 Identity 參數為 Ken 而 Myer 為全新參數。結果，畫面將會出現下列錯誤訊息：
    
        Get-CsOnlineUser : 找不到接受引數 'Myer' 的位置參數。.
    
    若要使用包含空格 (或逗號或任何其他限制字元) 的參數值，請為該值加上雙引號：
    
        -Identity "Ken Myer"
    
    在大部分情況下，Windows PowerShell 可讓您使用單引號而非雙引號。例如，下列為有效的 Windows PowerShell 語法：
    
        -Identity 'Ken Myer'
    
    然而，請注意字串的開頭與結尾必須使用相同類型的引號。下列是無效的 Windows PowerShell 語法：
    
        -Identity "Ken Myer'
    
    若是嘗試執行此命令，Windows PowerShell 主控台將會顯示下列內容：
    
    ``` 
    >>
    ```
    
    雙箭頭主要在提示您完成您的命令：因為您以雙引號開頭，所以 Windows PowerShell 會預期您使用雙引號作結。若是出現 \>\> 提示，請按 Ctrl-C 取消命令，然後再試一次。

  - 布林值 (True/False) 不應使用雙引號。另請注意，您必須使用 Windows PowerShell 變數 $True 與 $False 指定 True/False 值，例如：
    
        -EnterpriseVoiceEnabled $True

此外亦有不接受參數值的特定 Windows PowerShell 參數，稱為「切換參數」：

    -WhatIf

使用切換參數時不僅無需使用參數值，而且包含參數將會產生錯誤。例如，若是嘗試執行下列命令：

    -WhatIf $True

該命令將會失敗，並出現類似下列的錯誤訊息：

    Set-CsUserAcp :  找不到接受引數 'True' 的位置參數。

若要使用 Windows PowerShell 管理 商務用 Skype Online，您需要瞭解可供使用的 Cmdlet。此外，您也必須瞭解各個 Cmdlet 所能使用的參數及各個參數的「資料類型」(亦即參數是否接受日期值、字串值、數值等)。這些資訊 (以及如何使用 Cmdlet 的數個範例) 提供於 商務用 Skype Online Cmdlet 的說明主題中。例如，以下為可與 [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) Cmdlet 搭配使用的參數：

![特定 PowerShell Cmdlet 的參數](images/Dn362778.ead7add1-eec3-4fa4-8bbe-9aa72bb7a1ae(OCS.15).png "特定 PowerShell Cmdlet 的參數")

如您所見，參數表會提供 Cmdlet 的說明，指出參數為必要 (強制) 或選用項目，並告知各個參數的資料類型。請注意，表格所示的資料類型為 .NET Framework 所使用的正式資料類型。這代表資料類型會顯示為 System.Management.Automation.SwitchParameter，而非「切換參數」。以下為 商務用 Skype Online Cmdlet 最常用之資料類型的快速指南：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>代表使用者身分識別的字串值，通常為使用者的 UPN 或 SIP 位址：</p>
<pre><code>-Identity &quot;kenmyer@litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN 為完整網域名稱。例如：</p>
<pre><code>-Fqdn &quot;atl-lync-001.litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Boolean</p></td>
<td><p>布林值即為 True/False 值。注意，您必須使用 Windows PowerShell 變數 $True 與 $False 指定布林值：</p>
<pre><code>-Enabled $True -EnterpriseVoiceEnabled $False</code></pre></td>
</tr>
<tr class="even">
<td><p>System.Guid</p></td>
<td><p>GUID 是「全域唯一識別碼」的縮寫；在 商務用 Skype Online 中，各個 商務用 Skype Online 租用戶會指派有唯一識別碼，例如：</p>
<pre><code>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</code></pre>
<p>您可以使用下列命令擷取指派至您的 商務用 Skype Online 租用戶的 GUID：</p>
<pre><code>Get-CsTenant | Select-Object TenantId</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>切換參數之所以如此命名是因為其為開關的切換。也就是說，若是存在此參數，則開關為開啟；若是沒有此參數，則開關為關閉。例如，若要使用 Confirm 參數以在執行命令前要求確認，請將 Confirm 參數 (無參數值) 包含在命令中，例如：</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot; -Confirm</code></pre>
<p>若是無需要求確認，則請勿包含 Confirm 參數：</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>System.String</p></td>
<td><p>字串值為英數值，也就是說，通常包含任何可使用鍵盤輸入的字元，例如：</p>
<pre><code>-Password &quot;abc123%&amp;*&quot;</code></pre>
<p>為字串值加上雙引號是不錯的作法。您不一定要加上雙引號，然而，若是字串值包含空格或逗號，或正好為 Windows PowerShell 的保留關鍵字，則必須加入雙引號。(關鍵字是 Windows PowerShell 語言的命令或其他元素。舉例來說，“If” 與 “End” 均為 Windows PowerShell 關鍵字。如需更多資訊，請透過 Windows PowerShell 命令提示字元輸入下列命令：</p>
<p>Get-Help about_Reserved_Words</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Windows PowerShell 與 Lync Online 的簡介](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

