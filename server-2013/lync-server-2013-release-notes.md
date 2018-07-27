---
title: Lync Server 2013 版本資訊
TOCTitle: 版本資訊
ms:assetid: 9f9e864c-3365-4800-803c-5289bd8fd363
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205120(v=OCS.15)
ms:contentKeyID: 49291829
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的版本資訊

 

_**上次修改主題的時間：** 2015-03-23_

歡迎使用 Lync Server 2013 版本資訊。請參閱本檔案，以取得 Lync Server 2013 已知問題的相關資訊。

## 關於本文件

本文件包含您在部署及使用 Lync Server 2013 之前應該知道的重要資訊。如需 Lync Server 2013 的詳細資訊，請參閱 [Microsoft Lync Server 2013](microsoft-lync-server-2013.md) 文件。

本文件包含下列各節：

   Lync 2013 用戶端

   Lync Server

   安裝

   行動性

   會議

   企業語音

   目前狀態

   回應群組應用程式和通話駐留應用程式

   Lync Server 控制台、拓撲產生器和規劃工具

   當地語系化

   著作權

## Lync 2013 用戶端

## 如果檔案已在其他應用程式中開啟，則在立即訊息中傳輸檔案便會失敗 (1920369)

**問題：**

如果您嘗試將像是 Word 文件的檔案包含在立即訊息中並傳給其他 Lync 使用者，則傳輸動作看似成功實則傳輸檔案失敗。Lync 用戶端中將會顯示檔案類型的圖示，但是預定接收者無法開啟該檔案。並不會顯示錯誤訊息通知您傳輸不成功。

**因應措施：**

若要解決此問題，請關閉開啟的檔案或開啟該檔案的應用程式，然後再嘗試於立即訊息中傳輸檔案。

## Lync Server

## 如果 Lync Server Storage Service 資料複寫失敗，系統管理員就必須檢查過時的 Storage Service 佇列項目的效能計數器 (3225121)

**問題：**

Lync Server Storage Service 使用 Windows Fabric 進行複寫。如果已在主要前端伺服器上刪除資料，但在次要前端伺服器上卻刪除失敗 (例如，前端伺服器發生未預期的關閉或錯誤)，則資料可能會留下並呈「孤立」狀態。孤立的資料可能會導致效能衰退且浪費磁碟空間。

**因應措施：**

若要解決此問題，如果事件記錄檔中已產生 LYSS\_DB\_SPACE\_USED\_ERROR (Id=32058) 和 LYSS\_DB\_SPACE\_USED\_CRITICAL (Id=32059) 事件，則系統管理員必須在名稱為 **LYSS - 目前的 Storage Service 過時佇列項目數目**的 **LS:LYSS - Storage Service API** 之下檢查前端伺服器的效能計數器。如果此效能計數器的值很大 (例如，大於 50,000)，則系統管理員應執行 Lync Server 2013 Resource Kit 中的 CleanuUpStorageServiceData.exe 工具，該工具會刪除集區中的所有孤立資料。如需此工具的詳細資訊，請參閱 Lync Server 2013 Resource Kit 文件。

## 當伺服器或集區的 IP 位址設定變更時，就必須重新啟動 Lync Server 服務 (3212447)

**問題：**

當 Lync Server 2013 部署的 IP 位址設定變更 (例如：從 IPv4 變更為 Dual Stack，或從 Dual Stack 變更為 Ipv6) 時，直到重新啟動服務後，所有伺服器元件才能掌握設定變更。

**因應措施：**

若要解決此問題，請在變更部署的 IP 位址設定後重新啟動 Lync Server 服務。若要這麼做，請在 Lync Server 管理命令介面中執行下列 Cmdlet：

  ```
  Stop-CsWindowsService -graceful
  ```
  ```
  Start-CsWindowsService
  ```

## Lync Server 2013 管理組件已不再提供電話撥入式會議綜合交易 Cmdlet (3212342)

**問題：**

Lync Server 2013 管理組件已不再提供電話撥入式會議綜合交易 Cmdlet **Test-CsDialInConferencing**。

**因應措施：**

只有企業內部才能使用電話撥入式會議綜合交易 Cmdlet **Test-CsDialInConferencing**。

系統管理員可以繼續在 Lync Server 管理命令介面中使用此 Cmdlet 進行疑難排解。如有必要，企業也可以開發私人管理組件以在內部執行此 Cmdlet。

## 將記錄檔複製到網路共用時，如果網路流量中斷，則集中式記錄服務會停止 (3212464)

**問題：**

若集中式記錄服務已設定為使用網路路徑 ( **Get-CsClsConfiguration** Cmdlet 的 CacheFileNetworkFolder 參數值是有效的 UNC 路徑)，則快取的記錄檔會複製到網路共用。如果網路流量在複製檔案時中斷，則會發生例外狀況，導致集中式記錄服務停止。

此服務已設定為最多自動重新啟動三次，所以此服務會從前三次例外狀況中復原。

**因應措施：**

這個問題沒有任何因應措施。 若要找出問題所在，請監控事件記錄中「服務控制管理員」在「 Lync Server集中式記錄服務代理程式」服務意外終止時記錄的事件 ID 7031。如果發生這種情況三次以上，請使用 **Start-CsWindowService** Cmdlet 手動重新啟動服務。

## 需要手動匯入 Storage Service 佇列項目 (3211368)

**問題：**

Lync Server 2013 會在每個 前端伺服器的資料庫上儲存有關會議和立即訊息的資料，例如封存的訊息和詳細通話記錄 (CDR)。為了改善效能， Lync Server 2013 會從本機資料庫定期匯出一段時間未處理的佇列項目，並且儲存在檔案存放區上。如果無法使用檔案存放區，這些項目就會儲存在 前端伺服器上。為了避免在集區容錯移轉期間遺失資料，因此會發生同樣的作業。

在匯出作業期間， Lync Server Storage Service 會在事件記錄檔中記錄每一個階段，其事件 ID 包含 32075 (已開始完全清除作業)、32076 (已完成完全清除)、32082 (已開始維護層級清除)、32083 (維護層級清除完成)、32089 (因為資料庫填滿而發生清除)。此資料不會自動匯回到系統進行處理並傳送到其最終目的地 ( SQL Server 或 Exchange Server)。

**因應措施：**

若要將資料匯入系統中，系統管理員必須使用 Lync Server 資源組件中的 ImportStorageServiceData 工具，該工具會將資料送回系統進行處理並傳送到其最終目的地。

## 如果 UseNormalizationRules 的預設值變更為 False，Address Book Web Query 搜尋就會失敗 (3175514)

**問題：**

如果 UseNormalizationRules 的預設值變更為 False，Address Book Web Query 搜尋就會失敗。預設值變更之後，Lync 用戶端使用者便無法使用 Lync Address Book Web Query 來搜尋使用者。

**因應措施：**

如果 UseNormalizationRules 的預設值變更為 False，使用者可以使用 Active Directory 網域服務 中定義的電話號碼，而 Lync Server 2013 不需套用正規化規則，執行下列動作即可解決此問題：

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列其中一項作業：
    
      - 如果您的部署僅包含 Lync Server 2013 伺服器，在全域層級執行下列 Cmdlet，將 UseNormalizationRules 和 IgnoreGenericRules 的值變更為 True：
        
            Set-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true
    
      - 如果您的部署包含 Lync Server 2013 與 Lync Server 2010 或 Office Communications Server 2007 R2 的組合，請執行下列 Cmdlet 並將其指派給拓撲中的每一個 Lync Server 2013 集區：
        
            New-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true

3.  等待所有集區發生 CMS 複寫。

4.  修改部署的電話正規化規則檔案，以清除內容。該檔案位於每個 Lync Server 2013 集區的檔案共用上。如果此檔案不存在，則建立名稱為 "Company\_Phone\_Number\_Normalization\_Rules.txt" 的空白檔案。

5.  請稍候幾分鐘，讓所有前端集區讀取新檔案。

6.  在部署中的每一個 Lync Server 2013 集區上執行下列 Cmdlet。
    
        Update-csAddressBook

## 系統會針對每個 Lync 2013 集區每天產生一次 Address Book Server 錯誤事件 21054 (3195918)

**問題：**

Lync Server 2013 Address Book Server 會在執行每日維護時每天產生一次錯誤事件 21054。 即使更新成功，系統管理員每次執行 **Update-csAddressBook** Cmdlet 時，也會產生此錯誤。但是，若更新成功，即可放心地忽略此錯誤事件。

**因應措施：**

當您遇到此錯誤事件時，請執行下列 Cmdlet：

    Debug-csAddressBookReplication -Poolfqdn <Pool FQDN for which the event was generated>

如果 Cmdlet 回報沒有未編製索引或放棄的物件，即可放心地忽略錯誤事件 21054。

此外，應在 System Center Operations Manager 中關閉重要運作情況指標 (Key Health Indicator, KHI)「通訊錄使用者已正確編製索引」。

## 在 Edge 集區上設定 IPv6 時，要求可能會失敗 (3205810)

**問題：**

在 Edge 集區上設定 IPv6 時，對 Edge 集區的某些要求可能會失敗。

**因應措施：**

若要解決此問題，請勿使用 IPv6 設定 Edge 集區。

## invoke-csPoolFailback Cmdlet 可能會在集區容錯回復期間失敗 (3206153)

**問題：**

嘗試容錯回復集區時， **invoke-csPoolFailback** Cmdlet 可能會因為下列錯誤而失敗：無法在反覆嘗試後完成水合程序。

**因應措施：**

若要解決此問題，請再次執行此 Cmdlet，並等到 Cmdlet 成功為止。請注意，容錯回復程序可能需要幾分鐘時間才能完成。具有 20,000 個使用者的集區最久需要 60 分鐘才能完成。

## 當您將前端伺服器新增至已經建立的集區時，可能會發生資料遺失 (3015990) – 混合式 商務用 Skype Online

**問題：**

在集區有一個以上 前端伺服器的環境中，您可能會遇到此問題，您可重新啟動其中一個 前端伺服器，或新增先前不屬於集區的新 前端伺服器。

為集區建立資料封存的穩定分佈之前，資料正在封存的使用者可能會遇到資料遺失情形。一對一交談的這對可能遺失資料期間受限於 15 分鐘 ，而會議交談則限於 30 分鐘。

**因應措施：**

當您執行維護時，您不用逐一啟動集區中的 前端伺服器，應將此集區容錯移轉至其他集區，然後在伺服器上執行維護工作。您也可以在執行維護工作前讓服務無法使用，然後在維護完成時恢復可用性。

## 系統管理員無法利用 Get-CsClientAccessLicense Cmdlet 取得使用人數 (3012255)

**問題：**

系統管理員無法利用 **Get-CsClientAccessLicense** Cmdlet 取得正確的用戶端授權使用量。

**因應措施：**

若要檢查伺服器授權類型，您可以執行 **Get-CsService** Cmdlet 來擷取所有資料庫的完整網域名稱 (FDQN)。如果 前端伺服器的 FQDN 與後端資料庫的 FQDN 相同，此授權為 Standard Edition 授權，否則為 Enterprise Edition 授權。

## 未正確回報用戶端使用人數 (3010175)

**問題：**

在判斷用戶端授權計數時，您可能會遇到下列情況：

1.  **行動使用者的授權計數不正確**
    
    授權計數是以裝置使用者的唯一 IP 位址數目為基礎。授權計數的限制如下：
    
      - 如果使用者的 IP 位址在 Lync 工作階段內變更，則會高估授權數量。當使用者透過桌面用戶端從一個以上的位置連線至 Lync Server 時，可能會發生這種情況。
    
      - 如果使用者透過行動用戶端連線，則會低估授權數量，因為無法判斷裝置的 IP 位址。

2.  **公用交換電話網路 (PSTN) 撥打到 Lync 用戶端的電話、Lync 用戶端撥打到 PSTN 線路的電話，以及轉接至 PSTN 線路的 Lync 電話都會被計算兩次授權**
    
    在下列案例中，將會額外計算兩個授權，而非一個授權，這是因為電話號碼和 Lync 使用者都會納入計算，以判斷使用的授權數量。若要取得正確的授權資料，請手動移除電話號碼所產生的授權。
    
      - 撥打到 Lync 的 PSTN 電話
    
      - 撥打到 PSTN 線路的 Lync 電話
    
      - PSTN 電話撥打到 Lync，然後 Lync 會將這通電話轉接到 PSTN 線路。其中一條 PSTN 線路將會納入計算。

3.  **不會計算已登入 Lync 電話的授權**
    
    當使用者使用 Lync 認證的電話時，此電話若已登入並保持連線 (以持續其登入狀態)，如果在電話登入後發生授權查詢，則不會將此電話算成使用授權。

4.  **針對加入會議的 PSTN 電話所計算的授權**
    
    當使用者透過 PSTN 電話加入會議時，針對加入會議所計算的授權會不正確。然而，不需授權即可透過 PSTN 電話加入會議。

**因應措施：**

1.  **行動使用者的授權計數不正確**
    
      - 您可以手動識別屬於相同裝置的 IP 位址，然後移除授權計數中的其中一個。
    
      - 若是透過 Lync 用戶端連線的行動裝置，這個問題就沒有因應措施。

2.  **PSTN 撥打到 Lync 用戶端的電話、Lync 用戶端撥打到 PSTN 線路的電話，以及轉接至 PSTN 線路的 Lync 電話都會被計算兩次授權**
    
    您必須手動識別 PSTN 電話號碼，並移除為其產生的授權計數。

3.  **不會計算已登入 Lync 電話的授權**
    
    您可以將 Lync 電話設為登出，然後定期 (如每隔 3 個月) 重新登入。

4.  **針對加入會議的 PSTN 電話所計算的授權**
    
    您可以手動識別用於加入會議的 PSTN 電話號碼，並移除此電話號碼產生的授權。

## 升級至 Silverlight 5 後，VMware 環境中的 Lync Server 控制台會停止運作 (3010077)

**問題：**

如果您在 VMware 環境中使用 Lync Server 控制台，將 Microsoft Silverlight 升級至版本 5 後， Lync Server 控制台可能會停止運作。

**因應措施：**

若要解決此問題，請執行下列其中一個動作：

  - 解除安裝 Silverlight 5，然後從 [http://go.microsoft.com/fwlink/p/?LinkID=149156](http://go.microsoft.com/fwlink/p/?linkid=149156) 安裝 Silverlight 4。

  - 從不是 VMware 虛擬電腦的電腦存取 Lync Server 控制台。
    
    若要這麼做，如果電腦上已安裝 Lync Server 管理工具，即可從伺服器的 Windows \[開始\] 功能表啟動 Lync Server 控制台。
    
    您也可以利用 Web 瀏覽器存取 Lync Server 控制台。URL 類似於 https://\<frontend\_pool\_fqdn\>/cscp。

## 在 Active Directory 中修改使用者的辨別名稱後，通訊錄服務中的使用者資訊並未更新 (3211549)

**問題：**

如果在 Active Directory 網域服務中變更使用者的辨別名稱 (也稱為 DN)，則不會在通訊錄服務 (ABS) 中更新任何其他變更。這不會影響使用者的登入或顯示狀態，但如果 SIP 位址同時變更，則會讓使用者無法通訊，因為搜尋會傳回過時的 SIP 位址。

**因應措施：**

若要解決此問題，請勿變更使用者的 DN。如果您將使用者的 DN 還原為先前的值，更新就會反映在通訊錄服務中。

## 安裝

## 使用非 ASCII 字元可能會導致 Lync Server 無法啟動

**問題：**

如果目的地資料夾名稱含有非 ASCII 字元 (包括 UNICODE、雙位元組字集 (DBCS)、UTF-8 和 UTF-16)，安裝將會失敗。此外，如果下列項目包含非 ASCII 字元，則安裝可能會成功，但是伺服器將無法啟動：

  - 電腦名稱

  - 網域名稱

  - 使用者名稱

  - 使用者 SIP URI

  - 服務帳戶名稱

**因應措施：**

在目的地資料夾名稱、電腦名稱、網域名稱、使用者名稱、使用者 SIP URI 和服務帳戶名稱中，只使用 ASCII 字元。

## 安裝 Lync Server 2013 前，必須先安裝「當模組在 IIS 7.5 中呼叫 InsertEntityBody 方法時發生堆積損毀」的 Hotfix

**問題：**

安裝 Lync Server 2013 之前，必須先安裝 Microsoft 知識庫文章 264886 ( [http://go.microsoft.com/fwlink/?linkid=268603\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268603%26clcid=0x404)) 中描述之「當模組在 IIS 7.5 中呼叫 InsertEntityBody 方法時發生堆積損毀」的 Hotfix ( [http://go.microsoft.com/fwlink/?linkid=268602\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268602%26clcid=0x404))。

**因應措施：**

從 Microsoft 下載中心下載及安裝 Hotfix，網址為 [http://go.microsoft.com/fwlink/?linkid=268602\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268602%26clcid=0x404)。

## Lync Server 2013 無法安裝於 ITA Windows Server 2012 OS RTM 版本 (3179467)

**問題：**

因為 Windows Fabric 安裝失敗，所以無法在 ITA Windows Server 2012 上安裝 Lync Server 2013。

因為使用時間格式 HH:MM:SS 建立網狀架構追蹤，所以 Windows Fabric 安裝失敗。但是，在 ITA Windows Server 中，時間格式為 HH.MM.SS。

**因應措施：**

若要解決此問題，請在安裝 Lync Server 2013 前更新登錄。必須更新的登錄機碼為：HKEY\_USERS\\.DEFAULT\\Control Panel\\International\\sTimeFormat。使用 Windows PowerShell 命令列介面將 sTimeFormat 的值變更為 HH:mm:ss，如下所述：

1.  啟動 Windows PowerShell 並執行下列 Cmdlet：
    
    ```
    New-PSDrive -Name HKU -PSProvider Registry -Root HKEY_USERS
    ```
    ```
    $a="HKU:\.Default\Control Panel\International"
    ```

2.  若要檢視目前的值，請執行下列 Cmdlet：
    
        Get-itemproperty $a -Name sTimeFormat
    
    請記下 sTimeFormat 的值，以便在安裝完成後還原。

3.  若要設定為新的值，請執行下列 Cmdlet：
    
        Set-ItemProperty $a -Name sTimeFormat -Value "HH:mm:ss"

4.  Lync Server 2013 安裝成功後，請執行下列 Cmdlet 以還原 sTimeFormat 的原始值：
    
        - Set-ItemProperty $a -Name sTimeFormat -Value "<Value noted down in Step 3. above>"

## 行動性

## 伺服器容錯移轉程序期間的行動用戶端問題 (3345992)

**問題：**

當 Lync Server 發生失敗且容錯移轉程序開始時，下列問題可能會影響行動用戶端使用者：

  - 容錯移轉開始後長達 10 分鐘沒有任何傳入 Lync 通話或訊號。

  - 無法接受傳入交談要求。

  - 如果失敗的伺服器是使用者的主伺服器，使用者將無法加入會議。

**因應措施：**

這個問題沒有任何因應措施。容錯移轉完成後，將會恢復正常運作。

## 如果行動使用者拒絕其他 Lync 端點的傳入通話，通話會顯示為 Lync Mobile 用戶端上的未接交談 (3346251)

**問題：**

如果行動使用者拒絕傳入通話，而該通話是來自其他 Lync 端點，則通話會顯示為 Lync Mobile 用戶端上的未接交談，而不會顯示為裝置通話清單中的通話。

**因應措施：**

這個問題沒有任何因應措施。

## 搜尋連絡人時，行動用戶端可能不會顯示同盟連絡人的顯示名稱 (3346256)

**問題：**

在部分情況下 (例如在連絡人清單中搜尋同盟連絡人)，可能不會顯示同盟連絡人的顯示名稱。當 Lync Mobile 用戶端的連絡人沒有作用中目前狀態訂閱時，就可能發生這種情形。

**因應措施：**

這個問題沒有任何因應措施。

## 在行動用戶端中，性質為會議邀請之未接交談中的受邀者和時間戳記資訊遺失 (3346265)

**問題：**

在行動用戶端中，當未接交談的性質為會議邀請時，受邀者和時間戳記資訊會從未接交談的訊息中遺失。

**因應措施：**

這個問題沒有任何因應措施。

## 使用 VoIP 撥打電話的行動用戶端使用者，無法在使用 Exchange 2010 或較舊版本設定之語音信箱使用者的語音信箱留言 (3346260)

**問題：**

如果行動用戶端使用者使用 VoIP 撥打電話，使用者將無法在設為使用 Microsoft Exchange Server 2007 或 Microsoft Exchange Server 2010 語音信箱使用者的語音信箱留言。

**因應措施：**

若要解決此問題，請使用 Exchange 2010 SP1 或更新版本的 Microsoft Exchange Server。

## 在行動用戶端上使用「以 URL 封鎖」配合「用戶端版本設定」時可能會顯示不正確的錯誤訊息 (3346258)

**問題：**

在行動用戶端上為「用戶端版本設定」使用 **以 URL 封鎖**時，如果用戶端版本不受支援，可能會顯示不正確的錯誤訊息。

**因應措施：**

若要解決此問題，請設定「用戶端版本設定」使用 **封鎖**而不要使用 **以 URL 封鎖**。

## 會議

## 在 Lync Server 2013前端伺服器上執行的防毒軟體可能會造成應用程式定義域回收，這會暫時中斷 Lync Web App 2013、Lync Mobile 2010 和 Lync Mobile 2013 用戶端的服務 (3212531)

**問題：**

防毒軟體可能會誘使應用程式定義域重新啟動，這會導致 Lync Mobility Service 2013 和整合通訊 (UC) Web API 用戶端應用程式 ( Lync Web App 2013、Lync Mobile 2010 和 Lync Mobile 2013) 喪失其狀態。

**因應措施：**

若要解決此問題，請將含有 Web 元件和 .NET Framework 的資料夾排除在防毒掃描外。如需詳細資訊，請參閱 Microsoft 知識庫文章 312592＜PRB：ASP.NET 中出現「正在重新啟動應用程式」錯誤的隨機應用程式重新啟動＞，網址為 [http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x404)。

需排除下列資料夾：

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Mcx\\Ext

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Mcx\\Int

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Ucwa\\Int

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Ucwa\\Ext

  - %Windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\Config

## 必須在 Windows Internet Explorer 中啟用 ActiveX 控制項或原生 XMLHTTP 支援，才能成功加入會議 (2798163)

**問題：**

如果使用者在 Windows Internet Explorer 的網際網路瀏覽器設定中同時停用 ActiveX 控制項與原生 XMLHTTP 支援，Internet Explorer 若獲選為預設瀏覽器，使用者就無法加入會議。

**因應措施：**

在 Internet Explorer 中啟用 ActiveX 控制項或「原生 XMLHTTP 支援」。

## Lync Server Web 會議服務無法從關鍵模式復原 (2788663)

**問題：**

如果關閉關鍵模式以便進行封存 (在系統失敗的情況下)，關鍵模式將會啟動，而且參與者無法再進行會議。系統管理員修正系統失敗 (如修正資料庫問題) 後，不會自動復原會議服務資料，而且系統管理員必須手動重新啟動會議服務，才能繼續進行會議。

**因應措施：**

系統管理員必須在修正系統失敗後手動重新啟動會議服務。

## Web 會議服務忽略外部 Office Web App 伺服器的 HTTP Proxy (2602182)

**問題：**

如果您在網際網路、周邊網路中部署 Web 會議服務外的 Office Web Apps Server (也就是，不在公司內部網路中的伺服器)，而且 Web 會議服務需要 HTTP Proxy 才能連線至此，則 Office Web Apps Server 探索會失敗。Web 會議服務會忽略 Office Web Apps Server 設定的 拓撲產生器中定義的 HTTP Proxy 設定。因此，Lync 用戶端將無法與會議中的其他參與者進行 Microsoft PowerPoint 2010 共用。如果您安裝 Lync Server 內部部署，並且在內部網路中設定 Office Web Apps Server 內部部署，則不需要設定 Proxy。

**因應措施：**

唯一的因應措施就是不要有需使用 HTTP Proxy 才能與外部 Office Web Apps Server 通訊的部署組態。

## 不支援將視訊新增至音訊會議提供者的會議 (2603861)

**問題：**

如果使用者已加入音訊會議提供者的音訊會議，則不支援新增視訊。

**因應措施：**

這個問題沒有任何因應措施。

## 已啟用 IPv6 的拓撲會強迫 Lync Web App Silverlight 外掛程式自動更新，確保可從 Lync Web App 使用螢幕共用功能 (2604634)

**問題：**

將拓撲設成啟用 IPv6 後，如果已經安裝舊版的螢幕共用外掛程式，使用者就無法從 Lync Web App 用戶端共用其螢幕。

**因應措施：**

若要強迫在透過 Lync Web App 加入會議時更新為最新版的螢幕共用外掛程式，請在下列兩個檔案中將 **MinSupportedBuildVersion** 的值從 "4.0.7457.0" 修改為 "4.0.7577.380"：

  - %ProgramFiles%\\Microsoft Lync Server 15\\Web Components\\Reach\\Int\\Client\\Plugins\\ReachAppShPluginProperties.xml

  - %ProgramFiles%\\Microsoft Lync Server 15\\Web Components\\Reach\\Ext\\Client\\Plugins\\ReachAppShPluginProperties.xml

## 企業語音

## 在某些情況下，在設為使用 IPv4 和 IPv6 雙重堆疊的電腦上執行的 Lync 用戶端可能不支援依賴電腦 IP 子網路的功能，例如 E911、媒體旁路、通話許可控制和位置基礎路由 (3335508)

> [!NOTE]  
> 本節所包含的資訊與 Lync Server 2013 ：2013 年 2 月的累計更新相關



**問題：**

當 Lync 用戶端在啟用 IPv4 和 IPv6 雙重堆疊且以 Proxy 伺服器 DNS 解析為基礎的電腦上執行時，用戶端可能會使用電腦的 IPv6 位址登入。登入後，Lync 用戶端將只支援 IPv6 支援的功能，這些功能不包括 E911、媒體旁路、通話許可控制和位置基礎路由。

**因應措施：**

若要解決這個問題，請在用戶端電腦上停用 IPv6 支援：

## 如果未設定使用者的 企業語音，使用者就必須使用 E164 格式才能從會議撥出 (3215342)

**問題：**

如果未設定使用者的 企業語音，該使用者就必須使用 E164 格式才能從會議成功撥出。如果未使用 E164 格式，使用者就無法從會議撥出。

**因應措施：**

若要解決此問題，未啟用 企業語音的使用者應使用 E164 格式的數字從會議撥出。

## 目前狀態

## 如果使用者在整合連絡人存放區已開啟時選取「封鎖所有邀請和通訊」，則不會拒絕目前狀態 (3204526)

**問題：**

如果使用者在整合連絡人存放區已開啟時選取「封鎖所有邀請和通訊」，則不會拒絕目前狀態。

**因應措施：**

若要解決此問題，您可以關閉使用者的整合連絡人存放區。若要這麼做，請執行下列 Cmdlet：

    Set-CsUserServicesPolicy -Identity "<user display name>" -UcsAllowed $False

例如：

    Set-CsUserServicesPolicy -Identity "Ken Myer" -UcsAllowed $False

## 內部部署所屬的 Office Communications Server 2007 R2 使用者無法查看混合式部署中 商務用 Skype Online 使用者的目前狀態 (3014624) - 混合式

**問題：**

當您使用 Lync Server 2013 Director 時，這個問題可能會發生於混合式部署中。

對內部部署使用者而言， 商務用 Skype Online 所屬使用者的目前狀態會顯示為 \[目前狀態未知\]。此外， 商務用 Skype Online 所屬使用者無法查看 Office Communications Server R2 內部部署使用者的目前狀態。

**因應措施：**

若要部分解決此問題，請變更 商務用 Skype Online 使用者的主伺服器 (msrtcsip-presencehomeserver)，以指向 Lync Server 2013 內部部署集區，而非 Lync Server 2013 Director。您可以在內部部署 前端伺服器上修改此設定。

此因應措施將對 商務用 Skype Online 使用者正確顯示 Office Communications Server 2007 R2 所屬使用者的目前狀態。

## 回應群組應用程式、 通話駐留應用程式 和群組來電接聽

## 來電者可能會在與受話方建立通話期間聽到一秒的等候音樂 (3334097)

> [!NOTE]  
> 本節所包含的資訊與 Lync Server 2013 ：2013 年 2 月的累計更新相關



**問題：**

透過群組來電接聽擷取通話時，來電者可能會在與受話方建立通話期間聽到一秒的等候音樂。

**因應措施：**

這個問題沒有任何因應措施。

## 回應群組代理人只能透過 Lync Server 2010 Agent Console 登入和登出 Lync Server 2010 正式代理人群組 (2773455)

**問題：**

Lync Server 2013回應群組代理人只能透過 Lync Server 2010 Agent Console 登入和登出 Lync Server 2010 正式代理人群組。在 Lync Server 2010 Agent Console 中，使用者只能看見其所屬的 Lync Server 2010回應群組。他們看不見其所屬的任何 Lync Server 2013 回應群組。

**因應措施：**

如果 回應群組代理人是 Lync Server 2013 使用者並屬於 Lync Server 2013 正式代理人群組，使用者必須在瀏覽器中透過 Web 連結直接存取 Lync Server 2013 Agent Console，以登入和登出 Lync Server 2013 代理人群組。

## Lync Server 2010回應群組代理人不能代表 Lync Server 2013回應群組撥打電話 (2773471)

**問題：**

身為 Lync Server 2013回應群組代理人的 Lync Server 2010 使用者不能代表 回應群組撥打電話。 Lync Server 2013回應群組不適用於在 Lync 用戶端中撥打電話。

**因應措施：**

若要解決此問題，您必須將 Lync Server 2010 使用者移到 Lync Server 2013。

## 在 回應群組移轉至 Lync Server 2013 後從 Lync Server 2010 進行移除，會使 回應群組無法接受任何來電 (3016227)

**問題：**

如果透過 Lync Server 控制台或 Lync Server 管理命令介面，從 Lync Server 2010 移除由 Lync Server 2010 移轉至 Lync Server 2013 的 回應群組，則 Lync Server 2013 中的 回應群組會停止接收所有來電。

**因應措施：**

若要解決此問題，請勿從 Lync Server 2010 移除任何由 Lync Server 2010 移轉至 Lync Server 2013 的回應群組。

如果已經移除 回應群組，您應在 Lync Server 2013 中予以重新部署。

## 若在建立新的管理工作流程時將其設定為非使用中，則工作流程會部署失敗 (3207527)

**問題：**

若在建立新的管理工作流程時將其設定為非使用中，則工作流程會部署失敗。在建立工作流程時將其設定為非使用中，就會遇到這個問題，但不會影響在部署後才進行編輯以設為非使用中的工作流程。

**因應措施：**

在建立及部署工作流程時，將工作流程設定為使用中，然後進行部署。在工作流程部署成功後，即可編輯此工作流程並設定為非使用中。

## 如果 回應群組已匯入備份集區中，則從擁有者集區移除 回應群組，會使備份集區的 回應群組無法在容錯移轉期間接受任何來電 (3016214)

**問題：**

如果主要集區擁有的 回應群組已匯入備份集區中但未覆寫擁有者，而且已從擁有者集區移除 回應群組，則備份集區中的回應群組不會在容錯移轉期間接受任何來電。

**因應措施：**

您必須在主要集區中重新部署 回應群組。您還必須從主要集區匯出 回應群組組態，然後再次匯入備份集區中。

您也可以在備份集區中重新建立 回應群組。在此情況下，備份集區會是 回應群組的擁有者集區。

## 如果代表 回應群組完成擷取要求，則無法從 通話駐留應用程式擷取駐留通話 (3211798)

**問題：**

下列條件成立時，駐留通話的擷取要求就會失敗：

  - 代理人屬於匿名 回應群組

  - 代理人嘗試透過匿名 回應群組從 通話駐留應用程式擷取駐留通話

  - 代理人嘗試透過 \[代理撥號\] 選項或透過 Lync Attendant 用戶端中的相同選項來撥打軌道號碼，以便擷取通話

**因應措施：**

這個問題沒有任何因應措施。擷取駐留通話時，不需代表 回應群組這麼做

## Lync Server 控制台、 拓撲產生器和規劃工具

## 規劃工具限制 (3331056 和 3331059)

> [!NOTE]  
> 本節所包含的資訊與 Lync Server 2013 ：2013 年 2 月的累計更新相關



**問題：**

為您的部署進行規劃時，規劃工具有下列限制：

  - 最多支援 10 個中央網站

  - 每個中央網站最多可設有 14 個分支網站

  - 每個中央網站最多可供 240,000 名使用者使用

此外，在計算建議的拓撲時，規劃工具不包括下列項目的值：

  - 位於線上的使用者數目

  - 啟用 XMPP 同盟的使用者百分比

  - 目前使用 Lync Web App 的使用者百分比

**因應措施：**

這些問題沒有任何因應措施。如需更多有關規劃工具的資訊，請參閱＜ [使用規劃工具設計 Lync Server 2013 的拓撲](lync-server-2013-designing-the-topology-by-using-the-planning-tool.md)＞。

## 更新選項時，規劃工具無法為邊緣網路使用先前定義的 IP 位址

**問題：**

使用規劃工具完成設計後，如果您對 Edge 網路選項進行變更，可能會新增其他 IP 位址到設計中，而不會更新現有的 IP 位址。當您檢視 Edge 網路圖的詳細資訊時，選取 **\[按一下這裡以更新選項\]** ，接著在 \[組態選項\] 對話方塊中，選取 \[Edge 網路\] 並選取 **\[我要使用相同的 FQDN 和 IP 位址，但要為 Edge Server 上的 Edge Service 使用不同的連接埠\]** ，就可能發生這種情形。套用任何變更都可能導致新增 IP 位址和 Edge Server 到設計中。

**因應措施：**

這個問題目前沒有任何因應措施。

## 在 Lync Server 控制台中，\[將所有使用者移至集區\] 無法如預期般運作 (3199270)

**問題：**

在複雜的 Active Directory 環境 (如具有多個網域控制站和父/子網域的環境) 中，使用 Lync Server 控制台在不同集區間移動所有使用者，可能會傳回以下錯誤訊息：「指定的使用者不是舊版使用者，請改用 Move-CsUser Cmdlet。」這是在複雜的 Active Directory 環境中覆寫時間較長的結果。

**因應措施：**

若要解決此問題，請執行下列其中一個動作：

  - 在 Lync Server 控制台中使用篩選條件來搜尋舊版使用者，選取這些使用者，然後使用 \[將選取的使用者移至集區\] 命令，而非 \[將所有使用者移至集區\] 。

  - 透過 Lync Server Cmdlet，使用 Lync Server 管理命令介面分批移動舊版使用者。

## 在 Microsoft Silverlight 瀏覽器外掛程式 更新至版本 5 後， Lync Server 控制台會在 VMware 環境中停止運作 (3199270)

**問題：**

如果您在 VMware 環境中使用 Lync Server 控制台，將 Silverlight 升級至版本 5 後， Lync Server 控制台可能會停止運作。

**因應措施：**

若要解決此問題，請執行下列其中一個動作：

  - 解除安裝 Silverlight 5，然後從 [http://go.microsoft.com/fwlink/?linkid=149156\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=149156%26clcid=0x404) 安裝 Silverlight 4。

  - 從不是 VMware 虛擬電腦的電腦開啟 Lync Server 控制台。
    
    若要從遠端電腦開啟 Lync Server 控制台，在電腦上安裝 Lync Server 管理工具，然後從 Windows \[開始\] 功能表啟動 Lync Server 控制台。
    
    您也可以在 Web 瀏覽器中輸入 URL 以開啟 Lync Server 控制台。URL 類似於 https://\<frontend\_pool\_fqdn\>/cscp。

## 在 拓撲產生器中移除鏡像資料庫後，系統管理員就無法執行 Uninstall-csMirrorDB Cmdlet (3199266)

**問題：**

當系統管理員在 拓撲產生器中停用鏡像資料庫，然後在 拓撲產生器中刪除鏡像資料庫時，系統管理員的待辦事項清單中會顯示一則訊息，要求執行 **Uninstall-csMirrorDatabase** Cmdlet ，以從 SQL Server 移除鏡像。當系統管理員嘗試執行此 Cmdlet 時，此 Cmdlet 失敗。

**因應措施：**

若要在 拓撲產生器中移除集區的 SQL 鏡像，您必須先使用 Cmdlet 在 SQL Server 中移除鏡像。您可以接著使用 拓撲產生器從拓撲中移除鏡像。若要在 SQL Server 中移除鏡像，請使用下列 Cmdlet：

    Uninstall-CsMirrorDatabase -SqlServerFqdn <SQLServer FQDN> [-SqlInstanceName <SQLServer instance name>] -DatabaseType <Application | Archiving | CentralMgmt | Monitoring | User | BIStaging | PersistentChat | PersistentChatCompliance> [-DropExistingDatabasesOnMirror] [-Verbose]

例如，若要移除使用者資料庫的鏡像並捨棄此資料庫，請輸入下列資訊：

    Uninstall-CsMirrorDatabase -SqlServerFqdn primaryBE.contoso.com -SqlInstanceName rtc -Verbose -DatabaseType User -DropExistingDatabasesOnMirror

*DropExistingDatabasesOnMirror* 參數會導致受影響的資料庫從鏡像中刪除。若要從拓撲中移除鏡像，請執行下列動作：

1.  在 拓撲產生器中，用滑鼠右鍵按一下集區，然後按一下 \[編輯內容\] 。

2.  清除 \[啟用 SQL 存放區鏡像\] ，然後按一下 \[確定\] 。

3.  發行拓撲。

> [!IMPORTANT]  
> 當您變更後端資料庫鏡像關係時，您必須重新啟動集區中的所有 前端伺服器。



## 當系統管理員嘗試移除具有前端集區 (內含相關聯的見證存放區) 的部署時， 拓撲產生器會傳回驗證錯誤 (3199266)

**問題：**

如果系統管理員嘗試在 拓撲產生器中使用 \[移除部署\] 命令，以移除包含前端集區 (內含相關聯的見證存放區) 的部署，則 拓撲產生器會顯示驗證錯誤且動作無法繼續。

**因應措施：**

若要解決此問題，請執行下列其中一個動作：

  - 在嘗試移除部署前，先移除見證存放區。

  - 新增前端集區的見證存放區，然後加以移除。

## 規劃工具與 拓撲產生器之間的 常設聊天室伺服器 部署資訊不一致 (3012228)

**問題：**

當 Lync Server 2013 規劃工具針對已啟用災害復原的 常設聊天室伺服器 部署輸出網站拓撲圖表時，網站拓撲圖表包含多個 (實體) 網站，而各網站都有公平指派的 常設聊天室伺服器。在 拓撲產生器中，所有 常設聊天室伺服器 都被表示為屬於單一 (邏輯) 網站，並列在相同的 Persistent Chat Server 集區節點之下。

**因應措施：**

這個問題目前沒有任何因應措施。 使用者應分析 常設聊天室伺服器 部署的 規劃工具輸出，並修改計劃以符合特定需求。

## 當地語系化

## 監控

## 使用東亞版的 Lync Server 時，「部署監控報告」精靈在某些情況下會顯示不正確的字元 (3113565)

**問題：**

在系統地區設定未設為東亞語系的作業系統上使用東亞版的 Lync Server 2013 (例如，簡體中文、繁體中文、日文或韓文) 時，部署監控報告精靈會顯示問號或其他字元，而非當地語系化訊息。

**因應措施：**

若要更正此問題，請將作業系統的地區設定與 Lync Server 2013 設為相同語言，即可正確顯示所有訊息。

## Lync Server 控制台

## 在某些情況下，按一下 Lync Server 控制台 頁面的上方導覽列中的最後一個項目時，上方導覽列中的第一個項目會消失 (3158118)

**問題：**

在下個三個已知案例中，按一下 Lync Server 控制台 頁面的上方導覽列中的最後一個項目會導致上方導覽列中的第一個項目消失：

  - 在法文版的 "Federation et acces externe" 頁面上，"Strategie d'acces externe" 項目會在按一下 "Partenaires federes XMPP" 時消失。

  - 在德文版的 "Clients" 頁面上，"Clientversionskonfiguration" 項目會在按一下 "Pushbenachrichtigungskonfiguration" 時消失。

  - 在俄文版的 "Конфигурация сети" 頁面上，"Глобально" 項目會在按一下 "Маршрут региона" 時消失。

**因應措施：**

若要解決此問題，請在瀏覽器中重新整理 Lync Server 控制台的頁面。此頁面會載入瀏覽器中，並顯示上方導覽列中的所有項目。

## 通訊錄

## 部分語言通訊錄中的索引無法如預期般運作 (3336047)

> [!NOTE]  
> 本節所包含的資訊與 Lync Server 2013 ：2013 年 2 月的累計更新相關



如果某個使用者的內容包含索引欄位，且該欄位僅含有無法編制索引的字元，則該使用者不會顯示在通訊錄搜尋結果中。

下列字元和地區設定無法編製索引：

  - 大寫斯拉夫文、希臘文和亞美尼亞文字元

  - 大寫重音符號

  - 泰文

  - 寮文

  - 緬甸文

  - 梵文字母

  - 衣索比亞文

  - 西藏文

  - 孟加拉文

  - 古吉拉特文

  - 特拉古文

  - 所有其他印度文字集

## Lync Web App、Web Schedule 和 Web 元件

## Lync Web Scheduler、Dial-In、Join Launcher、Persistent Chat Room Management 和 OCTab 中某些語言的語言遞補可能無法如預期般運作 (3079700)

**問題：**

在 Web 瀏覽器中選取中性地區設定 (例如 Internet Explorer 中沒有進一步規格的語言名稱，像是 "Norwegian \[no\]") 而非地區設定時，指定語言、指令碼和地區設定 (例如 "Norwegian、Bokmal (Norway) \[nb-NO\]") 可能會導致 Lync Web Scheduler、Dial-In、Join Launcher、Persistent Chat Room Management 和 OCTab 中某些語言出現非預期的顯示行為。例如，選取下列其中一種語言時，使用者可能會看見英文頁面：

  - 挪威文

  - 葡萄牙文

  - 塞爾維亞文

**因應措施：**

如果您想選取具有中性地區設定的語言，永遠確定您也將具有特定地區設定 (含指令碼和/或國家/地區代碼) 的語言新增為瀏覽器的語言喜好設定清單中的額外語言。

## 在部分 Web 瀏覽器中使用 Lync Web Scheduler、Dial-In、Join Launcher、Persistent Chat Room Management 和 OCTab 時，對阿澤里文和烏茲別克文地區設定僅提供有限的支援 (3336748)

> [!NOTE]  
> 本節所包含的資訊與 Lync Server 2013 ：2013 年 2 月的累計更新相關



**問題：**

當您使用 Internet Explorer 8 或 Internet Explorer 9，且將瀏覽器語言設為阿澤里文 (拉丁) 或烏茲別克文 (拉丁) 時，Dial-in 和 Join Launcher 頁面將會以英文或瀏覽器中設定的慣用語言顯示。

當您使用 Firefox 或 Chrome 瀏覽器，且將瀏覽器語言設為阿澤里文 (拉丁) 或烏茲別克文 (拉丁) 時， Lync Web App、Lync Web Scheduler 和 RGS OCTab 將會以英文或瀏覽器中設定的慣用語言顯示。

Safari 瀏覽器不支援烏茲別克文 (拉丁) 地區設定。

**因應措施：**

這些問題沒有任何因應措施。

## 羅馬尼亞文版的 Lync Web App 中的 \[加入會議\] 清單缺少下拉式箭號 (3154899)

**問題：**

當使用羅馬尼亞文版的 Lync Web App 的使用者執行下列步驟時，下拉式清單中的 \[加入會議\] 不會顯示下拉式箭號：

1.  在 \[一般\] 索引標籤上選取 \[請在電腦上記住我的資訊\] 。

2.  選取 \[電話\] 索引標籤。

3.  按一下 \[加入會議\] 的下拉式清單。
    
    使用看不見箭號，該箭號表示有預設 **Lync Web App** 以外的其他選項，包含：\[不加入音訊\] (在羅馬尼亞文版中為 "Nu se asociaža la componenta audio") 和 \[新號碼\] (在羅馬尼亞文版中為 "Număr nou")。

**因應措施：**

即使未顯示此下拉式清單的箭號，使用者仍可按一下預設值，以選取清單中的其他設定。

## 使用土耳其文版的 Lync Web Scheduler 時，若使用 \[誰是簡報者\] 下的 \[我選擇的人員\] 選項，就無法儲存會議 (3169483)

**問題：**

在土耳其文版的 Lync Web Scheduler 中建立或編輯會議時，不支援 \[誰是簡報者\] 下的 \[我選擇的人員\] 選項。選取此選項後，便無法儲存會議。此時會出現錯誤訊息，表示有一或多個人員不能成為簡報者。

**因應措施：**

若要解決此問題，使用者可以使用 \[我公司中的人員\] 預設選項，或任何其他選項，例如 \[僅限召集人\] 或 \[包括公司外部人員在內的所有人員\]。召集人可以在人員加入會議之後，稍後將其降級或升級至正確的角色。

此外，瞭解其他語言的使用者可以將瀏覽器的語言選擇變更為其他 43 種支援語言中的其中一種，並嘗試使用 \[我選擇的人員\] 選項。

## 著作權

本文件是 Microsoft Corporation 的機密和專屬資訊，可支援在最終商業發行前可能會大幅變動之軟體產品的初步發行。根據收受者與 Microsoft 之間的保密合約不得公開。本文件僅供參考之用，Microsoft 不在本文件中做任何明示或暗示的擔保。本文件中的資訊 (包含 URL 及其他網際網路網站參考資料) 如有變更恕不另行通知。使用本文件所造成之風險或結果，應由使用者自行承擔。除非另有說明，否則範例中所描述之公司、組織、產品、網域名稱、電子郵件位址、商標圖樣、人員、地點及事件均屬虛構，並非影射任何真實的公司、組織、產品、網域名稱、電子郵件位址、商標圖樣、人員、地點及事件。遵守所有適用的著作權法是使用者的責任。非經 Microsoft Corporation 書面許可，本文之敘述不會限制任何依著作權本得享有之權利，您不得為任何目的使用任何形式或方法 (電子形式、機械形式、影印、記錄或其他方式) 複製或傳送本文件的任何部份，也不得將本文件的任何部份儲存或放入檢索系統 (retrieval system)。

Microsoft 對於本文件中所提及之內容可能擁有專利權、專利申請、商標、著作權或其他智慧財產權。 除非 Microsoft 書面授權合約所明示規定者外，提供本文件並不授予　貴用戶上述專利權、商標、著作權或其他智慧財產權。

© 2012 Microsoft Corporation. 版權所有，並保留一切權利。

Microsoft、Windows、Windows Live、Active Directory、Internet Explorer、MSN、Outlook 和 SQL Server 是 Microsoft Corporation 在美國及 (或) 其他國家/地區的註冊商標或商標。

所有其他商標為其各自擁有者的商標。

