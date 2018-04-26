---
title: 移轉通訊錄
TOCTitle: 移轉通訊錄
ms:assetid: b6e000ce-8b2e-460c-8a8b-000254b9d778
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205198(v=OCS.15)
ms:contentKeyID: 49292086
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉通訊錄

 

_**上次修改主題的時間：** 2012-10-02_

**移轉通訊錄自訂的正規化規則**

1.  在通訊錄共用資料夾的根目錄中尋找 Company\_Phone\_Number\_Normalization\_Rules.txt 檔案，並加以複製到 Lync Server 2013 試驗集區中通訊錄共用資料夾的根目錄。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>範例通訊錄正規化規則已安裝在您的 ABS Web 元件檔案目錄。路徑為 <strong>$installedDriveLetter:\Program Files\Microsoft Lync Server 2013\Web Components\Address Book Files\Files\ Sample_Company_Phone_Number_Normalization_Rules.txt</strong>。可重新命名此檔案為  <strong>Company_Phone_Number_Normalization_Rules.txt</strong> 並複製到通訊錄共用資料夾的根目錄。例如，在 <strong>$serverX</strong> 中共用的通訊錄路徑類似於 <strong>\\$serverX \LyncFileShare\2-WebServices-1\ABFiles</strong>。</td>
    </tr>
    </tbody>
    </table>


2.  使用文字編輯器 (如筆記本) 開啟 Company\_Phone\_Number\_Normalization\_Rules.txt 檔案。

3.  特定類型的項目將無法在 Lync Server 2013 中正確運作。檢查檔案是否存在本步驟中所述的類型項目，視需要加以編輯，並儲存變更至試驗集區中的通訊錄共用資料夾。
    
    若您必須在字串中包含空格或標點符號，將會導致正規化規則失敗，因為字串在輸入正規化規則時，會將這些字元移除。您的字串中如有包含必要的空格或標點符號，必須加以修改。舉例來說，下列字串將會導致正規化規則失敗：
    
        \s*\(\s*\d\d\d\s*\)\s*\-\s*\d\d\d\s*\-\s*\d\d\d\d
    
    下列字串將不會導致正規化規則失敗：
    
        \s*\(?\s*\d\d\d\s*\)?\s*\-?\s*\d\d\d\s*\-?\s*\d\d\d\d

