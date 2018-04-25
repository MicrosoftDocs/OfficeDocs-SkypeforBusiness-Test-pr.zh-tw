---
title: 設定在 Microsoft Lync Server 2013 中使用高解析度相片
TOCTitle: 設定在 Microsoft Lync Server 2013 中使用高解析度相片
ms:assetid: 995da78a-dc44-45a3-908d-16fe36cfa0d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688150(v=OCS.15)
ms:contentKeyID: 49890221
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定在 Microsoft Lync Server 2013 中使用高解析度相片

 

_**上次修改主題的時間：** 2014-02-05_

Microsoft Lync Server 2010 可讓使用者提供檢視自己所擁有連絡人的相片 (以及將自己的相片供其他人檢視)。通常這些相片是儲存在使用者在 Active Directory 上的 thumbnailPhoto 屬性中。這會對相片的大小和解析度產生很大的限制：thumbnailPhoto 屬性只能保留最大 48 像素 x 48 像素的相片。

但是在 Microsoft Lync Server 2013，相片可以儲存在使用者的 Microsoft Exchange Server 2013 信箱中，這讓相片大小可以提高到 648 像素 x 648 像素。此外，Exchange 2013 可以自動視需要調整這些相片的大小，以便用於其他產品。這通常表示有三種不同的相片大小和解析度可用：

  - 48 像素 x 48 像素，此大小用於 Active Directory thumbnailPhoto 屬性。如果您將相片上傳至 Exchange 2013，Exchange 會自動建立 48 像素 x 48 像素的相片版本，並更新使用者的 thumbnailPhoto 屬性。但是請注意，反向情況則不成立：如果您在 Active Directory 中手動更新 thumbnailPhoto 屬性，使用者 Exchange 2013 信箱中的相片並不會自動更新。

  - 96 像素 x 96 像素，用於 Microsoft Outlook 2013 Web App、Microsoft Outlook 2013、Microsoft Lync Web App 及 Lync 2013。

  - 648 像素 x 648 像素，用於 Lync 2013 和 Microsoft Lync Web App。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您有資源，建議您上傳 648x648 相片，如此可在任何 Office 2013 應用程式中提供最大的解析度和最佳的圖片品質。每張具有 648x648 大小和 24 位元深度的 JPEG 相片皆大約有 240 KB 的檔案大小。這表示每 4 張使用者相片大約就需要 1 MB 的磁碟空間。</td>
</tr>
</tbody>
</table>


執行 Outlook 2013 Web App 的使用者可以上傳高解析度相片 (以 Exchange Web Services 來存取)；使用者只能更新自己的相片。然而，系統管理員可以使用 Exchange 管理命令介面和類似下列的一系列 Windows PowerShell 命令來更新任何使用者的相片：

    $photo = ([Byte[]] $(Get-Content -Path "C:\Photos\Kenmyer.jpg" -Encoding Byte -ReadCount 0))
    Set-UserPhoto -Identity "Ken Myer" -PictureData $photo -Confirm:$False
    Set-UserPhoto -Identity "Ken Myer" -Save -Confirm:$False

上述範例中的第一個命令使用 Get-Content Cmdlet 來讀取檔案 C:\\Photos\\Kenmyer.jpg 的內容，並將資料儲存在名為 $photo 的變數中。在第二個命令中，則使用 Set-UserPhoto 這個 Exchange Cmdlet 來上傳相片並將相片附加到 Ken Myer 的使用者帳戶。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此範例中使用了 Ken Myer 的 Active Directory 顯示名稱作為使用者帳戶的 Identity。您也可以使用其他識別碼 (例如使用者的 SMTP 位址或使用者主體名稱。如需詳細資訊，請參閱位於 <a href="http://go.microsoft.com/fwlink/?linkid=268536%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268536&amp;clcid=0x404</a> 的 Set-UserPhoto Cmdlet 文件。</td>
</tr>
</tbody>
</table>


上傳相片並不等於將相片指派給 Ken Myer 的使用者帳戶。上傳相片只是讓 Outlook Web App 的 \[選項\] 頁面會顯示相片的預覽。若要真的將相片指派給使用者帳戶，使用者必須按一下 \[選項\] 頁面的 \[儲存\]，或是由系統管理員執行範例中的第三個命令。這第三個命令使用 Save 參數將相片指派給 Ken Myer 的使用者帳戶：

    Set-UserPhoto -Identity "Ken Myer" -Save -Confirm:$False

若要確認新相片已指派給使用者帳戶，Ken Myer 可以登入 Lync 2013 並依序選取 \[選項\]、\[我的圖片\]。新上傳的相片便應該會顯示為 Ken 的個人相片。或者，系統管理員也可以確認任何使用者的相片，方法是開啟 Internet Explorer 然後瀏覽至如下的 URL：

    https://atl-mail-001.litwareinc.com/ews/Exchange.asmx/s/GetUserPhoto?email=kenmyer@litwareinc.com&size=HR648x648

如果系統管理員可以使用 Internet Explorer 檢視相片，但是使用者無法在 Lync 2013 中檢視自己的相片，這通常表示有 Exchange Web 服務或 Exchange 自動探索服務連線問題。

另請注意，若要在 Lync 2013 中使用此相片，並不需要額外的組態。在上傳相片且執行 Set-UserPhoto Cmdlet 之後，相片將立即可用。

