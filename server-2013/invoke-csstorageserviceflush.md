---
title: Invoke-CsStorageServiceFlush
TOCTitle: Invoke-CsStorageServiceFlush
ms:assetid: 3f88a70d-79b0-4614-8604-660bac35a86f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619175(v=OCS.15)
ms:contentKeyID: 49290702
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsStorageServiceFlush

 

_**上次修改主題的時間：** 2015-03-09_

排清集區中每個前端伺服器的 Lync Server 存放服務資料庫。排清資料庫需要將所有佇列資料寫入磁碟，然後清除資料庫佇列。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsStorageServiceFlush -FlushType <FullFlush | SteadyStateFlush> -PoolFqdn <Fqdn> [-Binding <String>] [-Force <SwitchParameter>] [-HostNameStorageService <String>] [-WaitTime <TimeSpan>]

## 範例

## 範例 1

範例 1 所示的命令，會在集區 atl-cs-011.litwareinc.com 上所找到的「存放服務資料庫」裡執行排清「穩定狀態」的動作。排清穩定狀態時，唯一會從佇列中移除 (和寫入磁碟) 的資料，就是移除後不會影響資料庫作業的資料。

    Invoke-CsStorageServiceFlush -PoolFqdn "atl-cs-001.litwareinc.com" -FlushType "SteadyState"

## 詳細描述

Lync Server 存放服務提供的公用介面與基礎結構，可用來管理 Lync Server 資料，包括要監控、封存的工作階段資料以及交談記錄，還可以用來整合 Microsoft Exchange Server 2013 存放系統。就像其他資料庫一樣，存放服務會將資料快取在記憶體中，然後在系統資源允許時，定期將資料寫入磁碟。

一般而言，管理員不必與此佇列資料互動。不過，有時候佇列會變得太大，或是因為與該資料庫關聯的登錄器集區正在進行容錯移轉。發生上述情況時，您可以呼叫 **Invoke-CsStorageServiceFlush** Cmdlet，以將所有佇列資料寫入磁碟，然後清除資料庫快取。

如果必須同時關閉多部前端伺服器 (例如為了進行軟體升級)，**Invoke-CsStorageServiceFlush** Cmdlet 也很有幫助。一般而言，集區中的前端伺服器應該逐一關閉並重新啟動；這有助於防止因路由群組重新平衡而遺失資料。不過，您偶爾還是有可能必須同時關閉多部伺服器。為了防範遺失資料的可能性，您可以在電腦關機之前執行 **Invoke-CsStorageServiceFlush** Cmdlet。這樣會清空集區的佇列，並在實際關閉任一部伺服器之前，將所有資料寫入磁碟。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsStorageServiceFlush"}

**Lync Server 控制台：**無法在 Lync Server 控制台中使用由 **Invoke-CsStorageServiceFlush** Cmdlet 執行的功能。

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
<td><p><em>FlushType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.FlushType</p></td>
<td><p>指定要執行的存放排清類型。允許的值為：</p>
<p>* SteadyState – 唯一會排清的資料，就是從佇列中移除後不影響存放服務正常作業的資料。這樣做通常是為了移除佇列中較舊的資料。</p>
<p>* FullFlush – 排清佇列中的所有資料。當集區正在進行容錯移轉時，以及預期佇列不會再收到任何新資料時，通常就會使用此值。</p></td>
</tr>
<tr class="even">
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>包含要排清存放服務之集區的完整網域名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Binding</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Windows Communication Foundation (WCF) 繫結。WCF 繫結可判斷用戶端與服務彼此通訊所需的傳輸方式、編碼以及通訊協定。有效值如下：</p>
<p>* NetNamedPipe</p>
<p>* NetTCP</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HostNameStorageService</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行 Lync Server 存放服務的伺服器完整網域名稱。如果 Binding 設為 NetTCP，就必須加上此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>WaitTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定 Cmdlet 在假設排清已經開始，且要繼續進行排清程序的下一個步驟前的最長等待時間。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Invoke-CsStorageServiceFlush** Cmdlet 不接受管線傳送的資料。

## 傳回類型

字串值。

## 請參閱

#### 其他資源

[Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

