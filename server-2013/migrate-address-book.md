---
title: 移轉通訊錄
TOCTitle: 移轉通訊錄
ms:assetid: ac7f0f39-4c6d-4702-8e25-93a73e3d800f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205160(v=OCS.15)
ms:contentKeyID: 49291993
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉通訊錄

 

_**上次修改主題的時間：** 2012-10-09_

一般而言， Lync Server 2010 通訊錄會隨拓撲的其餘部分一起移轉。不過，如果您在 Lync Server 2010 環境中自訂下列項目，則必須執行部份移轉後續步驟：

  - 將 \[PartitionbyOU\] WMI 屬性設為依組織單位 (OU) 來為通訊錄項目分組。

  - 自訂通訊錄正規化規則。

  - 將 **UseNormalizationRules** 參數的預設值變更為 False。

**分組的通訊錄項目**

若將 \[PartitionbyOU\] WMI 屬性設為 True，以建立每個 OU 的通訊錄，如想持續分組通訊錄項目的話，則必須設定使用者和連絡人上的 \[msRTCSIP-GroupingId\] Active Directory 屬性。您可能會想分組通訊錄項目，以限制通訊錄搜尋的範圍。若要使用 \[msRTCSIP-GroupingId\] 屬性，請撰寫指令碼來填入屬性、指派相同值給所有您想分在同一組的使用者。例如，指派單一值給 OU 中的所有使用者。

**通訊錄正規化規則**

若您先前在 Lync Server 2010 環境中自訂了通訊錄正規化規則，便須將自訂規則移轉到試驗集區。若您未曾自訂通訊錄正規化規則，即無須對通訊錄服務執行任何移轉動作。 Lync Server 2013 的預設正規化規則與 Lync Server 2010 的預設規則相同。請遵照本節稍後的程序來移轉自訂的正規化規則。

> [!NOTE]  
> 若組織使用遠端呼叫控制，而您也自訂了通訊錄正規化規則，您必須執行本主題中所述的程序，才能使用遠端呼叫控制。本程序需具備 RTCUniversalServerAdmins 群組成員資格，或同等的權限。



**UseNormalizationRules 設為 False**

如果您將 **UseNormalizationRules** 值設為 False，讓使用者可使用他們在 Active Directory 網域服務 中定義的電話號碼，且 Lync Server 2013 不需套用任何正規化規則，您需要將 **UseNormalizationRules** 與 **IgnoreGenericRules** 參數設定為 True。 請遵照本節稍後的程序將這些參數設為 True。

## 移轉通訊錄自訂的正規化規則

1.  在通訊錄共用資料夾的根目錄中尋找 Company\_Phone\_Number\_Normalization\_Rules.txt 檔案，並加以複製到 Lync Server 2013 試驗集區中通訊錄共用資料夾的根目錄。
    
    > [!NOTE]  
    > 範例通訊錄正規化規則已安裝在您的 ABS Web 元件檔案目錄。路徑為 <strong>$installedDriveLetter:\Program Files\Microsoft Lync Server 2013\Web Components\Address Book Files\Files\ Sample_Company_Phone_Number_Normalization_Rules.txt</strong>。可重新命名此檔案為  <strong>Company_Phone_Number_Normalization_Rules.txt</strong> 並複製到通訊錄共用資料夾的根目錄。例如，在 <strong>$serverX</strong> 中共用的通訊錄路徑類似於 <strong>\\$serverX \LyncFileShare\2-WebServices-1\ABFiles</strong>。
    


2.  使用文字編輯器 (如筆記本) 開啟 Company\_Phone\_Number\_Normalization\_Rules.txt 檔案。

3.  特定類型的項目將無法在 Lync Server 2013 中正確運作。檢查檔案是否存在本步驟中所述的類型項目，視需要加以編輯，並儲存變更至試驗集區中的通訊錄共用資料夾。
    
    若您必須在字串中包含空格或標點符號，將會導致正規化規則失敗，因為字串在輸入正規化規則時，會將這些字元移除。您的字串中如有包含必要的空格或標點符號，必須加以修改。舉例來說，下列字串將會導致正規化規則失敗：
    
        \s*\(\s*\d\d\d\s*\)\s*\-\s*\d\d\d\s*\-\s*\d\d\d\d
    
    下列字串將不會導致正規化規則失敗：
    
        \s*\(?\s*\d\d\d\s*\)?\s*\-?\s*\d\d\d\s*\-?\s*\d\d\d\d

## 將 UseNormalizationRules 和 IgnoreGenericRules 設為 True

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列其中一項作業：
    
      - 若您的部署只包含 Lync Server 2013，請在全域層級執行下列 Cmdlet，將 **UseNormalizationRules** 與 **IgnoreGenericRules** 的值變更為 True：:
        
            Set-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true
    
      - 如果您的部署包含 Lync Server 2013 與 Lync Server 2010 或 Office Communications Server 2007 R2 的組合，請執行下列 Cmdlet 並將其指派給拓撲中的每一個 Lync Server 2013 集區：
        
            New-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true

3.  等候 中央管理存放區複寫在所有集區上發生。

4.  修改您部署的電話正規化規則檔案 "Company\_Phone\_Number\_Normalization\_Rules.txt"，以清除內容。該檔案位於每個 Lync Server 2013 集區的檔案共用上。如果檔案不存在，請建立名為 "Company\_Phone\_Number\_Normalization\_Rules.txt" 的空白檔案。

5.  等候數分鐘，讓所有 前端集區讀取新檔案。

6.  在您部署中的每個 Lync Server 2013 集區上執行下列 Cmdlet：
    
        Update-CsAddressBook

