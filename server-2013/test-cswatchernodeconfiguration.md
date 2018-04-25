---
title: Test-CsWatcherNodeConfiguration
TOCTitle: Test-CsWatcherNodeConfiguration
ms:assetid: 085507a1-17e8-4dfa-aa6a-062620584335
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204652(v=OCS.15)
ms:contentKeyID: 49290005
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWatcherNodeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

驗證組織所使用中之監看員節點組態設定。監看員節點是定期使用 Microsoft System Center Operations Manager 2007 R2 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsWatcherNodeConfiguration [-FileName <String>] [-ReadCredentialsFromCurrentUserStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會驗證組織使用中之每個監看員節點的組態設定。

    Test-CsWatcherNodeConfiguration

## 詳細描述

您若是使用 Microsoft System Center Operations Manager 監視 Lync Server 2013，可以選擇是否要選定「監看員節點」(亦即定期自動執行綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦)。監看員節點會指派給集，並須透過 **CsWatcherNodeConfiguration** Cmdlet 進行管理。請注意，您若是使用 System Center Operations Manager，即無須安裝監看員節點。您無須使用監看員節點，即可監視您的系統。唯一不同在於必須手動叫用執行綜合交易，而無法由 Operations Manager 自動叫用執行。

**Test-CsWatcherNodeConfiguration** Cmdlet 可讓您確認監看員節點的設定是否正確，並將其指派到有效的 Lync Server 2013 集區。請注意，**Test-CsWatcherNodeConfiguration** Cmdlet 只可對監看員節點本身執行，而無法對遠端電腦執行。

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsWatcherNodeConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>FileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：</p>
<p>-Report &quot;C:\Logs\WatcherNode.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ReadCredentialsFromCurrentUserStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示 <strong>Test-CsWatcherNodeConfiguration</strong> Cmdlet 從使用者的認證存放區擷取使用者認證。根據預設，<strong>Test-CsWatcherNodeConfiguration</strong> Cmdlet 會在網路服務帳戶的認證存放區中尋找認證。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsWatcherNodeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsWatcherNodeConfiguration** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)  
[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)

