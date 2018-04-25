---
title: 管理 Lync 用戶端
TOCTitle: 管理 Lync 用戶端
ms:assetid: d1ccc7b6-99ff-4ffd-bd29-9088fb8fe837
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362847(v=OCS.15)
ms:contentKeyID: 56269158
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理 Lync 用戶端

 

_**上次修改主題的時間：** 2015-06-22_

下列 Cmdlet 可管理 Lync 用戶端：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csimfilterconfiguration.md">Get-CsImFilterConfiguration</a></p></td>
<td><p>擷取您的組織所使用之 URI 限制的相關資訊。</p>
<p>傳送立即訊息時，使用者可以在訊息文字中內嵌 URI，讓交談中的其他參與者參照特定網站或共用項目。商務用 Skype Online 可設定為封鎖具有特定前置詞的超連結或使其失效，如此可協助確保參與者無法按下連結即移至 URI 所參照的網站，而是必須手動複製連結並貼上瀏覽器。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cspresencepolicy.md">Get-CsPresencePolicy</a></p></td>
<td><p>傳回目前狀態訂閱之兩個重要層面的相關資訊：「訂閱者提示」與「類別目錄訂閱」。</p>
<p>如有他人將您新增至連絡人清單，預設行為是由您收到快顯通知，告知您已新增至該清單中。在您將快顯通知關閉前，每個通知都會計數為一個「訂閱者提示」。</p>
<p>類別目錄訂閱代表特定資訊類別的要求，例如要求行事曆資料的應用程式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csprivacyconfiguration.md">Get-CsPrivacyConfiguration</a><br />
<a href="set-csprivacyconfiguration.md">Set-CsPrivacyConfiguration</a></p></td>
<td><p>設定 商務用 Skype Online 中的預設隱私值，同時仍提供使用者變更這些值的選項。</p>
<p>商務用 Skype Online 可讓使用者得以與他人分享大量的目前狀態資訊。使用者可發佈自己的相片、提供詳細的所在地點資訊，並且將目前狀態資訊設為自動提供給組織中的所有人 (而非僅限連絡人清單中的人員)。<strong>CsPrivacyConfiguration</strong> Cmdlet 可讓系統管理員在 商務用 Skype Online 中設定預設隱私值，同時仍讓使用者得以變更這些值。</p></td>
</tr>
</tbody>
</table>


您亦可使用 商務用 Skype Online 系統管理中心管理部分的隱私權組態設定：

![Lync 管理中心目前狀態私人模式設定](images/Dn362847.eb206b74-844d-4a7b-b1b3-0cfcb6e3614b(OCS.15).png "Lync 管理中心目前狀態私人模式設定")

## 請參閱

#### 概念

[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)  
[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

