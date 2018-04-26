---
title: Update-CsTenantMeetingUrl
TOCTitle: Update-CsTenantMeetingUrl
ms:assetid: 9aed3ede-bbd3-405a-997f-f7553e66aecd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn424754(v=OCS.15)
ms:contentKeyID: 59602858
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsTenantMeetingUrl

 

_**上次修改主題的時間：** 2015-03-09_

更新指定 商務用 Skype Online 租用戶的會議 URL。更新過後的 URL 採用更為簡單且標準的格式，可讓用戶端輕鬆尋找並連線至會議。

此 Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Update-CsTenantMeetingUrl [-Tenant] <guid> [-Force] [-WhatIf] [-Confirm]

## 範例

## 範例 1

範例 1 所示的命令會針對租用戶識別碼為 38aad667-af54-4397-aaa7-e94c79ec2308 之租用戶更新會議 URL。(請注意，您必須提供租用戶識別碼才可完成此命令。) 在按下 ENTER 以執行命令後，系統將詢問您是否確認更新會議 URL。您必須在收到提示時回答是，Update-CsTenantMeetingUrl 才會開始變更您的 商務用 Skype Online 組態設定。

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308"

## 範例 2

範例 2 同樣也會針對租用戶識別碼為 38aad667-af54-4397-aaa7-e94c79ec2308 之租用戶更新會議 URL。然而，此案例有加上 Force 參數；如此即會略過在您執行 Update-CsTenantMeetingUrl 時通常會出現的確認提示。在此案例中，只要按下 ENTER，即會執行命令並修改您的 商務用 Skype Online 組態設定。

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -Force

## 詳細說明

Update-CsTenantMeetingUrl 會將 商務用 Skype Online 會議 URL 更新為更為簡單且標準的格式；如此有助於避免原本會議 URL 偶而會發生的問題。例如，假設組織設定一個名稱為 contoso.onmicrosoft.com 的 Office 365 網域。執行此操作後，會議的 URL 將會類似如下：

https://meet.lync.com/onmicrosoft/contoso/user1/45GZFH99

現在，假設組織進行部分變更並決定採用虛名 URL litwareinc.com 而非 onmicrosoft.com 的 URL。組織將其使用者電子郵件地址修改為採用 litwareinc.com 的網域。然而，會議 URL 將仍會採用原本的網域名稱：

https://meet.lync.com/contoso/user1/45GZFH99

若要修正此問題，系統管理員應執行 Update-CsTenantMeetingUrl Cmdlet，如此即會以具有虛名 URL 的新會議 URL 取代舊的會議 URL：

https://meet.lync.com/litwareinc.com/user1/37JYLP71

執行 Update-CsTenantMeetingUrl Cmdlet 是進行此變更的唯一方法。

請注意，當您執行 Update-CsTenantMeetingUrl 時，您的 商務用 Skype Online 租用戶將於短暫的同步延遲後切換至新的 URL。這並不會對使用者可能排程的新會議造成任何問題：那些會議將自動以新的 URL 排程。然而，先前排程的會議將會發生問題，因為這些會議是以淘汰的舊會議 URL 排程。若要解決此問題，唯一的方法是要求您的使用者重新排程那些會議。

因為這可能會對部分組織造成問題 (特別是已有大量會議排程的組織)，所以 Update-CsTenantMeetingUrl 預設會在提示您之後才會開始更新會議 URL：

警告：這對於該租用戶中的使用者來說是重大變更。會議 URL 設定將會更新！舊的會議 URL 將無法再運作。此變更無法復原。  
您確定要繼續嗎？  
\[Y\] 是 \[A\] 全部皆是 \[N\] 否 \[L\] 全部皆否 \[S\] 暫停 \[?\] 說明 (預設為 \[Y\])：

您必須回答「是」或「全部皆是」，命令才會開始執行；若是回答「否」，則命令將會取消且會議 URL 將不會更新。請記住，會議 URL 一經變更，將無法再復原為原始 URL。命令執行後，URL 將會變更且所有先前排程的會議將需要重新排程。這也代表每個租用戶只需執行此命令一次。您無需分次執行此命令並重新更新會議 URL。

若是偏好直接執行命令而無需解除確認提示，您可以加上 Force 參數。在此情況下，Update-CsTenantMeetingUrl 將會直接執行而不會顯示確認提示：

警告：這對於該租用戶中的使用者來說是重大變更。會議 URL 設定將會更新！

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
<td><p><strong>Tenant</strong></p></td>
<td><p>必要</p></td>
<td><p>System.Guid</p></td>
<td><p>正在傳回其同盟設定之租用戶帳戶的全域唯一識別碼 (GUID)，例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>若是並未加上 Tenant 參數，則 Update-CsMeetingUrl 將提示您輸入該參數後才可繼續。</p></td>
</tr>
<tr class="even">
<td><p><strong>Confirm</strong></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p>
<p>請注意，Update-CsMeetingUrl 的預設行為是先顯示確認提示，然後再進行任何更新；也就是說，若要顯示確認提示，無需加上 Confirm 參數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Force</strong></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏原本在 Update-CsMeetingUrl 進行任何更新前應會顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><strong>WhatIf</strong></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。Update-CsMeetingUrl 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

