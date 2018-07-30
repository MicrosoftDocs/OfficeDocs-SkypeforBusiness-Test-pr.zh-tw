---
title: Lync Server 2013：XMPP 同盟夥伴的交涉設定
TOCTitle: XMPP 同盟夥伴的交涉設定
ms:assetid: ef773942-ef92-4f71-85a1-738dfebdfa00
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552456(v=OCS.15)
ms:contentKeyID: 49292752
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 XMPP 同盟夥伴的交涉設定

 

_**上次修改主題的時間：** 2015-03-09_

XMPP 協力廠商組態的訊號交涉類型設定有可種可能的組合。並非所有組合都有效。本主題詳列的表格將說明有效及無效的設定。第一個表格列出常見的設定，第三個表格詳列所有可能的組合。請注意，您無法使用 *「簡單驗證及安全性階層」* (SASL) **，除非***「傳輸層安全性」* (TLS) 也可使用。SASL 是以未加密 (可讀取) 格式送入，不得傳出，除非受到其他保護，例如 TLS。

### 常見的 XMPP 同盟交涉方法

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>傳輸層安全性 (TLS)</th>
<th>簡單驗證及安全性階層 (SASL)</th>
<th>回撥驗證</th>
<th>預期的驗證方法</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必要</p></td>
<td><p>必要</p></td>
<td><p>False</p></td>
<td><p>SASL 優於 TLS</p></td>
<td><p>必要的 TLS 與 SASL 可確保 SASL 訊息串流安全無虞。若 XMPP 同盟協力廠商未將 TLS 設為必要或選用，回撥就無法使用，也不能在後援方法中使用。</p></td>
</tr>
<tr class="even">
<td><p>必要</p></td>
<td><p>選用</p></td>
<td><p>True</p></td>
<td><p>SASL 優於 TLS、TLS 回撥、TCP 回撥</p></td>
<td><p>透過要求 TLS, 若 XMPP 同盟協力廠商將 SASL 設為選用，或使用必要的 SASL。若無法使用 SASL，將使用回撥優於 TLS。</p></td>
</tr>
<tr class="odd">
<td><p>選用</p></td>
<td><p>選用</p></td>
<td><p>True</p></td>
<td><p>SASL 優於 TLS、TLS 回撥、TCP 回撥</p></td>
<td><p>雖然這些設定在交涉方法中非常有彈性，但卻倚賴 XMPP 同盟協力廠商的設定。若協力廠商將 TLS 設為選用或必要，但 SASL 未獲支援，則可使用 TLS 回撥。若協力廠商將 TLS 與 SASL 設為選用或必要，則將使用最佳選項 TLS 優於 SASL。</p></td>
</tr>
<tr class="even">
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>True</p></td>
<td><p>TCP 回撥</p></td>
<td><p>在多數情況中，TCP 回撥只是可能的解決方案，還有其他更好的選項，但 TCP 回撥的確較值得信任。</p></td>
</tr>
</tbody>
</table>


### XMPP 同盟交涉方法矩陣：完成

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>傳輸層安全性 (TLS)</th>
<th>簡單驗證及安全性階層 (SASL)</th>
<th>回撥驗證</th>
<th>預期的驗證方法</th>
<th>無效組態的註解、警告或錯誤</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必要</p></td>
<td><p>必要</p></td>
<td><p>True</p></td>
<td><p>SASL 優於 TLS</p></td>
<td><div class="alert">
> [!WARNING]
> 若同時將 SASL 與 TLS 設為必要，回撥將無法作用。

</div></td>
</tr>
<tr class="even">
<td><p>必要</p></td>
<td><p>必要</p></td>
<td><p>False</p></td>
<td><p>SASL 優於 TLS</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>選用</p></td>
<td><p>必要</p></td>
<td><p>True</p></td>
<td><p>SASL 優於 TLS、TLS 回撥、TCP 回撥</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="even">
<td><p>選用</p></td>
<td><p>必要</p></td>
<td><p>False</p></td>
<td><p>SASL 優於 TLS</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="odd">
<td><p>不支援</p></td>
<td><p>必要</p></td>
<td><p>True</p></td>
<td><p>TCP 回撥</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="even">
<td><p>不支援</p></td>
<td><p>必要</p></td>
<td><p>False</p></td>
<td><div class="alert">
> [!WARNING]
> 無效組態

</div></td>
<td><div class="alert">
> [!WARNING]
> 因為 SASL 需要 TLS，且無法使用 TLS，所以 SASL/TLS 無法成功。TCP 回撥設為 False，且無法使用。

</div></td>
</tr>
<tr class="odd">
<td><p>必要</p></td>
<td><p>選用</p></td>
<td><p>True</p></td>
<td><p>SASL 優於 TLS、TLS 回撥</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>必要</p></td>
<td><p>選用</p></td>
<td><p>False</p></td>
<td><p>SASL 優於 TLS</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>選用</p></td>
<td><p>選用</p></td>
<td><p>True</p></td>
<td><p>SASL 優於 TLS、TLS 回撥、TCP 回撥</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="even">
<td><p>選用</p></td>
<td><p>選用</p></td>
<td><p>False</p></td>
<td><p>SASL 優於 TLS</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="odd">
<td><p>不支援</p></td>
<td><p>選用</p></td>
<td><p>True</p></td>
<td><p>TCP 回撥</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="even">
<td><p>不支援</p></td>
<td><p>選用</p></td>
<td><p>False</p></td>
<td><div class="alert">
> [!WARNING]
> 無效組態

</div></td>
<td><div class="alert">
> [!WARNING]
> SASL 要求 TLS。允許 TLS 變成選用可能會導致失敗的工作階段交涉。

</div></td>
</tr>
<tr class="odd">
<td><p>必要</p></td>
<td><p>不支援</p></td>
<td><p>True</p></td>
<td><p>TLS 回撥</p></td>
<td><p>組態可用於 TLS 回撥。</p></td>
</tr>
<tr class="even">
<td><p>必要</p></td>
<td><p>不支援</p></td>
<td><p>False</p></td>
<td><p>無效組態</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 或回撥必須啟用。

</div></td>
</tr>
<tr class="odd">
<td><p>選用</p></td>
<td><p>不支援</p></td>
<td><p>True</p></td>
<td><p>TLS 回撥、TCP 回撥</p></td>
<td><p>根據其他端點的交涉選擇，將接受 TCP 或 TLS 回撥。</p></td>
</tr>
<tr class="even">
<td><p>選用</p></td>
<td><p>不支援</p></td>
<td><p>False</p></td>
<td><p>無效組態</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 或回撥必須啟用。

</div></td>
</tr>
<tr class="odd">
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>True</p></td>
<td><p>TCP 回撥</p></td>
<td><p>TCP 回撥是唯一可用的交涉方法</p></td>
</tr>
<tr class="even">
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>False</p></td>
<td><p>無效組態</p></td>
<td><div class="alert">
> [!WARNING]
> SASL 或回撥必須啟用。

</div></td>
</tr>
</tbody>
</table>

