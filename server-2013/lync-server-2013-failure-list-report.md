---
title: Lync Server 2013：失敗清單報告
TOCTitle: 失敗清單報告
ms:assetid: b6f3a605-e0c6-461e-b17a-41d8039ace9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615446(v=OCS.15)
ms:contentKeyID: 49292088
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的失敗清單報告

 

_**上次修改主題的時間：** 2015-03-09_

失敗清單報告可提供個別參與者參與失敗的端對端或會議工作階段的相關資訊。此資訊包含遭遇問題的使用者 URI，以及與失敗關聯的 SIP 回應碼與診斷識別碼。

## 存取失敗清單報告

按一下 [Lync Server 2013 中的失敗散佈報告](lync-server-2013-failure-distribution-report.md)上的任一計量，即可存取失敗清單報告：

  - 熱門診斷原因 (工作階段)

  - 熱門形式 (工作階段)

  - 熱門集區 (工作階段)

  - 熱門來源 (工作階段)

  - 熱門元件 (工作階段)

  - 源自使用者的熱門項目 (工作階段)

  - 流向使用者的熱門項目 (工作階段)

  - 源自使用者代理的熱門項目 (工作階段)

從失敗清單報告中，您可按一下端對端工作階段的 \[工作階段\] 詳細資料計量來存取 [Lync Server 2013 中的對等工作階段詳細資料報告](lync-server-2013-peer-to-peer-session-detail-report.md)。您也可以按一下會議的 \[會議\] 計量來存取 \[會議詳細資料報告\]。

## 善用失敗清單報告

在失敗清單報告中，只要將滑鼠停留在某個值，您就可檢視每個回應碼與診斷識別碼的說明。例如，如果您將滑鼠停留在 \[診斷識別碼 7025\]，您會在工具提示中看見下列說明：

建立使用者的媒體時發生內部伺服器錯誤。

請務必注意，失敗清單報告並未提供一個直接的方法，可直接擷取至少參與一個失敗的工作階段的所有使用者清單，也沒有提供方法可判斷哪些使用者常遭遇失敗的工作階段。(因為，失敗清單報告不具備篩選功能。) 不過，如果您將資料匯出並轉換為逗號分隔值的檔案，就能使用 Windows PowerShell 來尋找這類問題的解答。例如，假設您將資料儲存為名為 C:\\Data\\Failure\_List.csv 的 CSV 檔案。根據儲存在該檔案的資料，以下命令會列出至少遭遇一個失敗的工作階段的所有使用者：

    $failures = Import-Csv -Path " C:\Data\Failure_List.csv"
    $failure |Sort-Object "From user" | Select-Object "From user" -Unique

該命令會傳回類似以下的清單：

    From user
    ----
    Pilar.Ackerman@litwareinc.com
    Henrik.Jensen@litwareinc.com
    Gilead.Amosnino@litwareinc.com
    David.Ahs@litwareinc.com
    Ken.Myer@litwareinc.com

這兩個命令可回報告每位使用者遭遇的失敗工作階段總數：

    $failures = Import-Csv -Path "C:\Data\Failure_List.csv"
    $failures | Group-Object "From user" | Select-Object Count, Name | Sort-Object -Property Count -Descending

將傳回類似下列的資料：

    Count    Name
     -----    ----
        20    Pilar.Ackerman@litwareinc.com
        20    David.Ahs@litwareinc.com
        16    Gilead.Amosnino@litwareinc.com
        16    Ken.Myero@litwareinc.com
        14    Henrik.Jensen@litwareinc.com

## 篩選器

無。您無法篩選失敗清單報告。

## 計量

下表列出失敗清單報告針對每通失敗通話所提供的資訊。

### 失敗清單報告計量

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序這個項目嗎？</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>報告時間</strong></p></td>
<td><p>否</p></td>
<td><p>報告的記錄日期與時間</p></td>
</tr>
<tr class="even">
<td><p><strong>要求</strong></p></td>
<td><p>否</p></td>
<td><p>失敗的 SIP 要求類型。例如 INVITE 或 BYE。</p></td>
</tr>
<tr class="odd">
<td><p><strong>回應碼</strong></p></td>
<td><p>否</p></td>
<td><p>會議失敗時傳送的 SIP 回應碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>否</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。</p></td>
</tr>
<tr class="odd">
<td><p>[加入時間 (毫秒)]</p></td>
<td><p>否</p></td>
<td><p>使用者加入會議所需的時間 (毫秒)。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源使用者</strong></p></td>
<td><p>否</p></td>
<td><p>撥打通話之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>來源使用者代理程式</strong></p></td>
<td><p>否</p></td>
<td><p>撥打通話之使用者端點所用的軟體。</p></td>
</tr>
<tr class="even">
<td><p><strong>目標使用者</strong></p></td>
<td><p>否</p></td>
<td><p>受話之使用者的 SIP 位址。</p></td>
</tr>
</tbody>
</table>

