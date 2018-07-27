---
title: 確認組態設定
TOCTitle: 確認組態設定
ms:assetid: 41dbf91c-f2e1-4b9a-88cf-959575558cf2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204848(v=OCS.15)
ms:contentKeyID: 49290724
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認組態設定

 

_**上次修改主題的時間：** 2015-03-09_

在您合併拓撲及執行 **Import-CsLegacyConfiguration** Cmdlet 後，請驗證您的 Office Communications Server 2007 R2 原則與設定都已匯入 Lync Server 2013。下表列出您應驗證的原則及設定。

## 移轉後所需檢查的原則與設定


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>若是使用此工作負載：</th>
<th>驗證下列原則與設定：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>立即訊息 (IM) 和會議</p></td>
<td><p>目前狀態原則</p>
<p>會議原則</p></td>
</tr>
<tr class="even">
<td><p>電話撥入式會議</p></td>
<td><p>撥入存取號碼</p>
<p>撥號對應表</p></td>
</tr>
<tr class="odd">
<td><p>企業語音</p></td>
<td><p>語音原則</p>
<p>語音路由</p>
<p>撥號對應表</p>
<p>PSTN 使用方式設定</p></td>
</tr>
<tr class="even">
<td><p>Communicator Web Access</p></td>
<td><p>簡單 URL</p></td>
</tr>
<tr class="odd">
<td><p>外部使用者</p></td>
<td><p>外部存取原則</p></td>
</tr>
<tr class="even">
<td><p>封存</p></td>
<td><p>封存原則</p></td>
</tr>
</tbody>
</table>


## 驗證原則與設定

1.  在您的 Office Communications Server 2007 R2 環境中，請記下撥號對應表 (之前稱為位置設定檔) 名稱、撥入存取號碼 (會議服務員存取電話號碼和地區)、語音路由以及上表所列的各項原則，加上 Communicator Web Access 所用的 URL。

2.  在 Lync Server 2013 前端伺服器中，開啟 Lync Server 控制台。

3.  若要驗證左側窗格中匯入的會議原則，請依序按一下 **\[會議\]** 、 **\[會議原則\]** ，然後驗證您 Office Communications Server 2007 R2 環境的所有會議原則都包含在清單中。
    
    > [!NOTE]  
    > 舊版 Office Communications Server 的 <strong>[會議]</strong> (Meeting) 原則，目前在 Lync Server 2013 中改稱為會議原則 (conferencing policy) 。此外，舊版 Office Communications Server 的 <strong>[匿名參與者]</strong> 設定，在 Lync Server 2013 中則為會議原則中的設定。
    
    
    > [!NOTE]  
    > 在 Office Communications Server 2007 R2 環境中，會議原則若未設為 <strong>[使用個別使用者]</strong> ，將只會匯入全域原則設定。在此情況下，將不會匯入其他的會議原則。
    
    
    > [!NOTE]  
    > Office Communications Server 2007 R2 會議原則中的 <strong>[匿名參與者]</strong> 若是設為 <strong>[依個別使用者強制執行]</strong> ，會在移轉時建立兩個會議原則，其中一個是設為 <strong>[True]</strong> 的 <strong>AllowAnonymousParticipantsInMeetings</strong> ，而另一個則是設為 <strong>[False]</strong> 的 <strong>AllowAnonymousParticipantsInMeetings</strong> 。
    


4.  若要驗證匯入的撥號對應表，請依序按一下 **\[語音路由\]** 與 **\[撥號對應表\]** ，然後驗證您 Office Communicator 2007 R2 環境的所有撥號對應表都包含在清單中。
    
    > [!NOTE]  
    > 在 Lync Server 2013 中， <strong>位置設定檔</strong> 現在稱為 <strong>撥號對應表</strong> 。
    


5.  若要驗證匯入的語音原則，請依序按一下 **\[語音路由\]** 與 **\[語音原則\]** ，然後驗證您 Office Communicator 2007 R2 環境的所有語音原則都包含在清單中。
    
    > [!NOTE]  
    > 如果 Office Communications Server 2007 R2 環境中的語音原則未設為 <strong>[使用個別使用者]</strong> ，將只會匯入全域原則設定。在此情況下，將不會匯入其他的語音原則。
    


6.  若要驗證匯入的語音路由，請依序按一下 **\[語音路由\]** 及 **\[路由\]** ，然後驗證您 Office Communicator 2007 R2 環境中的所有語音路由都包含在清單中。

7.  若要驗證匯入的 PSTN 使用方式設定，請依序按一下 **\[語音路由\]** 及 **\[PSTN 使用方式\]** ，然後驗證您 Office Communicator 2007 R2 環境中的 PSTN 使用方式設定包含在清單中。

8.  若要驗證匯入的外部存取原則，請依序按一下 **\[同盟與外部存取\]** 及 **\[外部存取原則\]** ，然後驗證您 Office Communicator 2007 R2 環境中的所有外部存取原則都包含在清單中。

9.  若要驗證封存原則，請依序按一下 **\[監控和封存\]** 及 **\[封存原則\]** ，然後驗證您 Office Communications Server 2007 R2 環境中的各項封存原則都包含在清單中。

10. 開啟 Lync Server 管理命令介面。

11. 若要驗證命令列的顯示狀態原則，請輸入下列內容：
    
        Get-CsPresencePolicy
    
    透過查看 **Identity** 參數中的名稱，驗證您 Office Communications Server 2007 R2 環境中的所有目前狀態原則都已匯入。

## 使用 Cmdlet 驗證原則與設定

1.  開啟 Lync Server 管理命令介面。

2.  執行下表中的 Cmdlet 以驗證原則與設定。
    
    這些 Cmdlet 的語法會類似下列範例：
    
        Get-CsConferencingPolicy
    
    如需這些 Cmdlet 的詳細資料，請執行：
    
        Get-Help <cmdlet name> -Detailed


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>若為下列原則或設定：</th>
<th>請使用此 Cmdlet：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目前狀態原則</p></td>
<td><p><strong>Get-CsPresencePolicy</strong></p></td>
</tr>
<tr class="even">
<td><p>會議原則</p></td>
<td><p><strong>Get-CsConferencingPolicy</strong></p></td>
</tr>
<tr class="odd">
<td><p>撥入存取號碼</p></td>
<td><p><strong>Get-CsDialInConferencingAccessNumber</strong></p></td>
</tr>
<tr class="even">
<td><p>撥號對應表</p></td>
<td><p><strong>Get-CsDialPlan</strong></p></td>
</tr>
<tr class="odd">
<td><p>語音原則</p></td>
<td><p><strong>Get-CsVoicePolicy</strong></p></td>
</tr>
<tr class="even">
<td><p>語音路由</p></td>
<td><p><strong>Get-CsVoiceRoute</strong></p></td>
</tr>
<tr class="odd">
<td><p>PSTN 使用方式</p></td>
<td><p><strong>Get-CsPstnUsage</strong></p></td>
</tr>
<tr class="even">
<td><p>URL</p></td>
<td><p><strong>Get-CsSimpleUrlConfiguration</strong></p></td>
</tr>
<tr class="odd">
<td><p>外部存取原則</p></td>
<td><p><strong>Get-CsExternalAccessPolicy</strong></p></td>
</tr>
<tr class="even">
<td><p>封存原則</p></td>
<td><p><strong>Get-CsArchivingPolicy</strong></p></td>
</tr>
</tbody>
</table>

