---
title: Test-CsCertificateConfiguration
TOCTitle: Test-CsCertificateConfiguration
ms:assetid: 8086bdf7-d283-4666-9f6c-0d5a3a31b3a6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398647(v=OCS.15)
ms:contentKeyID: 49291480
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsCertificateConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回本機電腦所使用之 Lync Server 憑證的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsCertificateConfiguration [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 Lync Server 目前 (在本機電腦上) 使用之憑證的資訊。

    Test-CsCertificateConfiguration

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化。但在此範例中，當您執行 **Test-CsCertificateConfiguration** Cmdlet 時，會使用 Report 參數指定所產生輸出檔案的檔案路徑 (C:\\Logs\\Certificates.xml)。

    Test-CsCertificateConfiguration -Report "C:\Logs\Certificates.xml"

## 詳細描述

**Test-CsCertificateConfiguration** Cmdlet 是「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

**Test-CsCertificateConfiguration** Cmdlet 會傳回 Lync Server 使用之憑證的資訊。**Test-CsCertificateConfiguration** Cmdlet 主要是供 \[憑證精靈\] 使用。建議系統管理員可以使用 **Get-CsCertificate** Cmdlet 擷取憑證資訊。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsCertificateConfiguration"}

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
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Certificates.html&quot;。執行此 Cmdlet 時，這個檔案若已存在，便會遭到覆寫。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsCertificateConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsCertificateConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment,CertificateExists 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCertificate](get-cscertificate.md)

