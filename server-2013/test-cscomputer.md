---
title: Test-CsComputer
TOCTitle: Test-CsComputer
ms:assetid: 0b33d951-510d-445c-9b01-c6431fda6d47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398162(v=OCS.15)
ms:contentKeyID: 49290047
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsComputer

 

_**上次修改主題的時間：** 2015-03-09_

**Test-CsComputer** Cmdlet 可驗證本機電腦上所執行之 Lync Server 服務的狀態。此 Cmdlet 也可確認電腦上對應的本機群組是否已加入正確的 Lync Server Active Directory 群組，以及是否已開啟了必要的電腦防火牆連接埠。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsComputer [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會驗證本機電腦的服務啟用狀態。在命令中加入 Verbose 參數以確保畫面上會完整報告作業成功 (或失敗)。

    Test-CsComputer -Verbose

## 範例 2

範例 2 也會驗證本機電腦的服務啟用狀態。此外，此命令會將啟用狀態的相關詳細資訊寫入 C:\\Logs\\Computer.html 檔案。此記錄檔是透過加入 Report 參數，後面緊接著應該記錄資訊之記錄檔的完整路徑而產生。

    Test-CsComputer -Verbose -Report C:\Logs\Computer.html

## 詳細描述

**Test-CsComputer** Cmdlet 是 Lync Server「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

只能在本機電腦上執行的 **Test-CsComputer** Cmdlet 會驗證該電腦上所有 Lync Server 服務的狀態。該 Cmdlet 也會檢查電腦上是否已開啟適當的防火牆連接埠，並判斷當您安裝 Lync Server 時所建立的 Active Directory 群組是否已新增至對應的本機群組。例如，**Test-CsComputer** Cmdlet 會驗證 Active Directory 群組 RTCUniversalUserAdmins 是否已新增至本機 Administrators 群組。

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
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Computer.html&quot;。如果此檔案已經存在，當您執行 Cmdlet 時，會加以覆寫。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsComputer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsComputer** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)

