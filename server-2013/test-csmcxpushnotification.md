---
title: Test-CsMcxPushNotification
TOCTitle: Test-CsMcxPushNotification
ms:assetid: db81339b-f79a-418a-b29d-8596dff7a210
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690043(v=OCS.15)
ms:contentKeyID: 49292516
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsMcxPushNotification

 

_**上次修改主題的時間：** 2015-03-09_

確認推播通知服務是否正常運作。推播通知服務 (Apple 推播通知服務及 Microsoft 推播通知服務) 可傳送事件的通知，例如傳送給行動裝置 (如 iPhone 及 Windows Phone) 的新立即訊息或新語音信箱 ，即使這些裝置上的 Lync 應用程式目前為暫止或在背景中執行也不受影響。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Test-CsMcxPushNotification -AccessEdgeFqdn <String> [-Certificate <X509Certificate2>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 所示的命令會測試透過 Edge Server atl-edge-001.litwareinc.com 存取的推入通知服務。

    Test-CsMcxPushNotification -AccessEdgeFqdn "atl-edge-001.litwareinc.com"

## 詳細描述

Apple Push Notification Service 和 Lync Server Push Notification Service 可讓在其 Apple iPhone 或 Windows Phone 上執行 Lync 的使用者接收關於 Lync 事件的通知，即使 Lync Server 已暫停或在背景執行亦然。例如，使用者可以接收類似下列事件的通知：

\- 新立即訊息工作階段或會議的邀請

\- 新立即訊息

\- 新語音信箱

如果沒有推入通知服務，使用者只有當 Lync Server 在前景執行且做為使用中應用程式時，才會收到這些通知。

Test-CsMcxPushNotification Cmdlet 可讓系統管理員確認推入通知服務正常運作。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsMcxPushNotification** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>AccessEdgeFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>Access Edge Server 用來連線至推入通知服務的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Certificate</em></p></td>
<td><p>選用</p></td>
<td><p>System.Security.Cryptography.X509Certificates.X509Certificate2</p></td>
<td><p>可讓您指定要用於驗證的 X509 憑證</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>附註：指定變數名稱時，請勿在前面加上 $ 字元。</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsMcxPushNotification** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsMcxPushNotification** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

