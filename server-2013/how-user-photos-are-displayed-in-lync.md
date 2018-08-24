---
title: Lync 中使用者相片的顯示方式
TOCTitle: Lync 中使用者相片的顯示方式
ms:assetid: b44a364d-a1d2-4d45-b27a-b5f77775e233
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn783119(v=OCS.15)
ms:contentKeyID: 62833683
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync 中使用者相片的顯示方式

 

_**上次修改主題的時間：** 2015-03-09_

**摘要：**根據您執行的 Lync 功能，例如在會議或 IM 聊天時，Lync 用戶端中顯示的使用者相片可能不同。

Lync 2010 引進一項功能，可在您的 Lync 設定檔案包含相片，其他 Lync 使用者會看到此相片。您也可以選擇是否在 Lync 用戶端中顯示連絡人的相片。在 Lync 2013 中，支援使用者的高解析度相片。本主題說明 Lync 用戶端如何取得和顯示使用者相片、影像的儲存位置、每個影像來源的限制，以及不同的 Lync 服務如何使用使用者相片。

## 規劃考量事項

規劃使用者相片支援時，您應考量下列事項。

  - 高畫質使用者相片支援需要將使用者的信箱放在 Exchange 2013，以及將 Lync 使用者帳戶放在 Lync 2013 集區。

  - 只有同時使用 Lync Server 2013 和 Exchange 2013 的環境才支援高畫質使用者相片。

  - 在 Exchange 2010 上擁有信箱的使用者，一律可將 AD DS 的 **thumbnailPhoto** 屬性作為其使用者相片的來源。

  - 儲存為 AD DS 的 **thumbnailPhoto** 屬性的使用者相片，不會向外部/同盟連絡人顯示。

  - 若使用者連絡人的相片是儲存在 AD DS 中，使用的影像檔案限制為 96×96 像素，且檔案大小不超過 100 KB。

  - 如果 Lync Server 與 Exchange Server 之間的連線中斷，將顯示使用者來自 AD DS 的低解析度 **thumbnailPhoto**，並只向內部使用者顯示。

  - 當目前發言者未啟用視訊時，會在 Lync 2013 會議中顯示高解析度使用者相片。此外，將滑鼠移到圖庫的縮圖相片上時，將顯示高解析度相片。

## Lync 2010 中的使用者相片

在 Lync 2010 用戶端，您可以從兩個選項選擇 (\[預設公司圖片\] 和 \[從網址顯示圖片\])，為您的設定檔顯示相片。

## 預設公司圖片

當您選擇 \[預設公司圖片\] 選項時，Lync 會從 Active Directory 網域服務 向您顯示相片。使用的影像是定義為 Active Directory 網域服務 中 **thumbnailPhoto** 屬性值的影像。這是 Exchange 在 Outlook 中顯示影像時所使用的相同檔案。

從 Active Directory 網域服務 使用影像必須考量下列事項：

  - 最多僅支援維度 96 像素 x 96 像素的影像。影像的檔案大小限制為 100 KB。

  - 依預設，使用者可變更用於 **thumbnailPhoto** 屬性的影像，但無法直接透過 Lync 用戶端變更。您可以透過 Active Directory 網域服務 停用此動作。

  - 即使您組織的外部連絡人是同盟連絡人，也不會向這些連絡人顯示 Active Directory 網域服務 中儲存的影像。

  - 在大型組織中，儲存和擷取大量使用者的影像可能會影響 Active Directory 網域服務 資料庫大小和效能。

  - 有限的影像維度和檔案大小意味只能使用低解析度影像。

## 使用者如何在 Active Directory 網域服務 中管理其使用者相片

使用者無法透過 Lync 2010 用戶端，直接變更其 Active Directory 網域服務 設定檔中使用的影像。他們可使用下列其中一個選項來執行這項工作 (如果選項可供使用)：

  - **SharePoint Server**   使用者可將相片上傳到 SharePoint Server 上的「我的網站」，然後[在 SharePoint 中設定設定檔同步](http://go.microsoft.com/fwlink/p/?linkid=507466)，以同步相片與 Active Directory 網域服務 中的 **thumbnailPhoto** 屬性。

  - **儲存於可公開存取之 URL 中的相片**   使用者可設定其使用者相片，針對欲使用的影像指定可公開存取的 URL。影像必須可公開存取，且存取時不必使用密碼。系統會透過目前狀態資訊中的連絡人卡片類別，將儲存於指定網址的影像傳送給其他使用者。當 Lync 用戶端需要顯示使用者相片時，便會從指定的網址擷取影像。

  - **Windows PowerShell 適用的 Exchange 2010 Cmdlet**   系統管理員可在 Exchange 2010 管理命令介面中執行 [Import-RecipientDataProperty](http://go.microsoft.com/fwlink/p/?linkid=507468) Cmdlet 來管理 **thumbnailPhoto** 屬性。使用 Exchange 2010 Cmdlet 匯入影像時，檔案大小限制為 10 KB。

  - **協力廠商工具**   使用者只能針對 **thumbnailPhoto** 屬性上傳其本身的相片。

## 從網址顯示圖片

選擇 \[從網址顯示圖片\] 選項時，Lync 會在您輸入的位址取得影像，並在 Lync 中顯示為您的使用者相片。

從網址使用影像時必須考量下列事項：

  - 檔案大小限制是由用戶端原則中的 **MaxPhotoSizeKB** 屬性所決定，而用戶端原則是由 [New-CsClientPolicy](http://go.microsoft.com/fwlink/p/?linkid=507463) Cmdlet 定義。預設的大小限制為 30 KB。最大值是 100 KB。影像的解析度沒有限制，但如果嘗試使用超出大小限制的影像檔案，該檔案不會下載至 Lync 用戶端。您可以將值設定為 0，在 Lync 中停止使用所有使用者相片。

  - 外部的同盟連絡人可看見來自網址的使用者相片。

## 使用用戶端原則 Cmdlet 管理使用者的相片

在 Lync Server 2010 中，用戶端原則設定值是使用 CsClientPolicy Cmdlet 所設定。設定的原則設定值是透過頻內佈建傳送給用戶端。CsClientPolicy Cmdlet 有兩個參數可決定使用者相片體驗，即 **DisplayPhoto** 和 **MaxPhotoSizeKB**。**DisplayPhoto** 和 **MaxPhotoSizeKB** 的對應頻內佈建參數名稱為 **PhotoUsage**。**PhotoUsage** 參數值會透過 **endpointConfigurationprovisionGroup** 傳送至用戶端。如需詳細資訊，請參閱[用戶端原則和設定概觀](http://go.microsoft.com/fwlink/?linkid=507470)。

**DisplayPhoto** 參數值可決定使用者的相片影像來源。下表包含支援的值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>DisplayPhoto 參數值</th>
<th>影像來源</th>
<th>Lync 2010 用戶端設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NoPhoto</p></td>
<td><p>none</p></td>
<td><p><strong>不要顯示我的圖片</strong></p></td>
</tr>
<tr class="even">
<td><p>PhotoFromADOnly</p></td>
<td><p>Active Directory</p></td>
<td><p><strong>預設公司圖片</strong></p></td>
</tr>
<tr class="odd">
<td><p>AllPhotos</p></td>
<td><p>網址</p></td>
<td><p><strong>從網址顯示圖片</strong></p></td>
</tr>
</tbody>
</table>


## Lync 2010 用戶端如何取得相片

在 Lync 2010 中，使用者相片是由伺服器上的通訊錄服務所管理。Lync 用戶端會先在伺服器上查詢「通訊錄 Web 查詢 (ABWQ)」服務 (透過 Distribution List Expansion Web 服務公開) 來取得使用者相片。用戶端接收影像檔案，然後將檔案複製到使用者的快取，以避免在每次需要顯示影像時下載該影像。查詢傳回的屬性值也會儲存在使用者的快取通訊錄服務項目中。通訊錄服務每 24 小時會刪除所有快取的影像，這意味若要在伺服器的快取中更新新的使用者影像，最長可能耗費 24 小時。您可以使用 [Update-CsAddressBook](https://docs.microsoft.com/en-us/powershell/module/skype/Update-CsAddressBook) Cmdlet 來強制更新快取。

「目前狀態」中包含的使用者相片也具備相關的雜湊值，可讓 Lync 用戶端用來判斷是否有較新的影像可用。系統會將「目前狀態」中使用的影像檔案變更自動通知用戶端。

> [!NOTE]  
> 由於相片不會儲存於 GalContacts.db 資料庫，因此用戶端原則 (<a href="http://go.microsoft.com/fwlink/p/?linkid=507508">Set-CsClientPolicy</a>) 中的 <strong>AddressBookAvailability</strong> 設定與使用者相片的下載無關。



ABWQ 服務的查詢包含下列屬性：

  - **PhotoHash**   二進位相片資料的雜湊值，並且用來判定目前的相片是否已變更。

  - **PhotoRelPath**   伺服器上儲存之影像檔案的相對路徑。

  - **PhotoSize**   影像檔案的大小，以位元組為單位。

  - **TimeStamp**   前次從伺服器下載影像檔案並複製到用戶端快取的日期和時間。

接下來在擷取影像檔案後，Lync 2010 用戶端會比較查詢傳回的屬性值與用戶端從頻內佈建接收的屬性值做，查看是否不同。如果值不同，用戶端會使用 HTTP GET 要求來擷取登入使用者的影像檔案。

此外，用戶端會從快取版本的影像檔案的建立時間開始，每 24 小時檢查伺服器一次，比較伺服器上的 **PhotoHash** 屬性值與用戶端上的值。如果值不同，用戶端即得知影像檔案已變更。為了取得更新的影像檔案，用戶端會再次查詢 ABWQ 服務，將用戶端快取上的影像檔案更新為伺服器上的影像檔案，同時也會重設用戶端快取的檔案 **TimeStamp**。

以下是 ABWQ 服務查詢的回應範例：

    <Attribute>
              <Name>PhotoRelPath</Name>
              <Value>efa6096aed2746cb9ab2037f7dbdde9d.f2eeeb5946db54a7aa607ecd3ae09d
              95.photo</Value>
              <Values xmlns:d6p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays" i:nil="true" />
    </Attribute>
    <Attribute>
              <Name>PhotoHash</Name>
              <Value>f2eeeb5946db54a7aa607ecd3ae09d95</Value>
              <Values xmlns:d6p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays" i:nil="true" />
    </Attribute>
    <Attribute>
         <Name>PhotoSize</Name>
         <Value>4620</Value>
         <Valuesxmlns:d6p1="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
    i:nil="true" />
    </Attribute>

## Lync 2013 中的使用者相片

Lync 2013 針對使用者相片引進了高解析度影像支援。而且，Lync 2013 現已支援在 Exchange 2013 的使用者信箱中儲存使用者相片，因此您不必擔心 Lync 2010 中的影像解析度和大小限制。Lync 2013 中的使用者相片可高達 648 像素 x 648 像素，檔案大小則高達 20 MB。Lync 2013 的高解析度相片必須存放在使用者位於 Exchange 2013 的信箱中，並且僅支援 Lync 2013 用戶端。此個整合 Exchange 的作法，善用了 2013 版 Lync、Exchange 和 SharePoint 包含的新授權架構 (稱為 Oauth)。

如果您的部署未使用 Exchange 2013，則使用者相片支援與 Lync 2010 提供的支援相同。不過，使用者在 Lync 2013 用戶端中必須使用不同的選項，才能選擇要使用的相片。在 Lync 2013 用戶端中，使用者可選取 \[隱藏我的圖片\] 或 \[顯示我的圖片\]。預設無法使用 \[從網站顯示圖片\] 選項，但可指派用戶端原則來啟用。

## 隱藏我的圖片

使用者相片設定位於 Lync 2013 的 \[選項\] 對話方塊。選擇 \[隱藏我的圖片\] 時，Lync 用戶端中不會顯示您的使用者相片，但您的連絡人卡片及 Lync 以外的地方仍會顯示您的相片。

## 顯示我的圖片

選擇 \[顯示我的圖片\] 選項時，會在您的 Lync 用戶端中，以及向 Lync 交談中的其他使用者顯示您的使用者相片。系統會使用 AD DS 中儲存的影像。

## 從網站顯示圖片

設定用戶端原則來啟用 \[從網站顯示圖片\] 選項後，即可在 Lync 2013 中使用該選項。用戶端版本必須比 15.0.4535.1002 更新 (與[Lync 累計更新：2013 年 11 月](http://go.microsoft.com/fwlink/p/?linkid=509908) 一起安裝)。使用者可能需要登出再重新登入，才能在用戶端中看到變更。

您可以在 Lync Server 管理命令介面 中執行 [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy) 原則，設定用戶端原則來啟用 \[從網站顯示圖片\] 設定。下列 Cmdlet 範例示範如何為部署中的所有使用者全域設定原則：

  ```
  $pe=New-CsClientPolicyEntry -Name EnablePresencePhotoOptions -Value True
  ```
  ```
  $po=Get-CsClientPolicy -Identity Global
  ```
  ```
  $po.PolicyEntry.Add($pe)
  ```
  ```
  Set-CsClientPolicy -Instance $po
  ```

將影像上傳到使用者的信箱時，Exchange 會自動建立解析度較低的影像版本，以便在用戶端應用程式中使用。AD DS 中的使用者相片也會更新。

> [!NOTE]  
> AD DS 中的影像檔案更新後，系統會建立 48 x 48 像素的影像，並將其使用於 AD DS 中的 thumbnailPhoto。任何現有的影像都會遭到取代。因此，若將 96 x 96 影像新增至 AD DS，會遭到新的 48 x 48 影像覆寫。唯有當您的環境中有使用者使用 Lync 2010 用戶端時，才需要注意上述情況，因為那些用戶端將從 AD DS 取得使用者相片。如果您的組織使用 Lync 2010 用戶端，您可以匯入 96 x 96 像素影像來取代 AD DS 所建立的影像。



## Lync 2013 中的使用者相片支援

如下表所述，Lync 2013 針對使用者相片支援三種影像解析度。使用的影像是由指派給 Lync 使用者的用戶端原則設定所決定。如需詳細資訊，請參閱本主題的＜使用用戶端原則 Cmdlet 管理使用者的相片＞。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>影像 解析度 (像素)</th>
<th>Application</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>48 x 48</p></td>
<td><p>使用於未選取更高解析度的影像時</p></td>
</tr>
<tr class="even">
<td><p>96 x 96</p></td>
<td><p>使用於 Outlook Web App 和 Outlook 2013</p></td>
</tr>
<tr class="odd">
<td><p>648 x 648</p></td>
<td><p>使用於 Lync 2013 桌面用戶端和 Lync 2013 Web App</p></td>
</tr>
</tbody>
</table>


在 Exchange 2013 中啟用信箱的任何使用者都可以透過 Outlook Web Access 或 Lync 2013 用戶端選項來上傳不同的影像，包括高解析度相片。使用之影像的建議設定包含：

  - **影像解析度**   648 x 648 像素

  - **色彩深度**   24 位元

  - **影像檔案大小**   最大 20 MB

  - **檔案格式**   JPEG

一般 24 位元、648 像素 x 648 像素的 JPEG 影像，檔案大小約 240 KB，因此每 4 張使用者相片大約需要 1 MB 儲存空間。

