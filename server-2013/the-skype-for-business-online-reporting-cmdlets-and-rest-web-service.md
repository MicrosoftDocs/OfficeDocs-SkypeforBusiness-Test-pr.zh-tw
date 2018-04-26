---
title: Lync Online：Lync Online 報告 Cmdlet 與 REST Web 服務
TOCTitle: Lync Online 報告 Cmdlet 與 REST Web 服務
ms:assetid: cadd73a7-c08a-4102-b73a-ccb3ad4987bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362845(v=OCS.15)
ms:contentKeyID: 56269155
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online 報告 Cmdlet 與 REST Web 服務

 

_**上次修改主題的時間：** 2015-06-22_

與報告功能結合的 商務用 Skype Online 可提供五個 Windows PowerShell Cmdlet，不僅有助於產生報告，亦可供系統管理員用於傳回自訂報告資料。商務用 Skype Online 另外也包含 REST (具體狀態傳輸)，可由開發人員用於擷取自訂報告資訊。

可供系統管理員使用的報告 Cmdlet 包括：

  - Get-CsActiveUserReport，提供作用中使用者 (即登入 商務用 Skype Online 並參與至少一個會議或對等通訊工作階段的使用者) 人數的相關資訊。

  - Get-CsAVConferenceTimeReport，提供使用者參與音訊/視訊會議之所用時間量 (以分鐘數計) 的相關資訊。

  - Get-CsConferenceReport，提供使用者參與的會議數與會議類型的相關資訊。

  - Get-CsP2PAVTimeReport，提供使用者參與包含音訊及/或視訊之對等工作階段之所用時間量的相關資訊。

  - Get-CsP2PSessionReport，提供使用者參與之對等工作階段的數量與類型的相關資訊。

大多數系統管理員都會使用 Office 365 管理中心中提供的報告。這些報告不僅是由系統自動產生，而且會以圖形呈現資料，相較於報告 Cmdlet 傳回的原始數值，通常更能夠輕鬆解譯。然而，熟悉 Windows PowerShell 的系統管理員可以使用報告 Cmdlet 傳回 Lync Online 報告未提供的資料。例如，報告 Cmdlet 可傳回工作階段持續時間 (各個工作階段的持續時間，以分鐘計) 的相關資訊。個別工作階段持續時間無法透過 Lync Online 報告提供。同樣地，在 Lync Online 報告的每日檢視中，僅會顯示過去 14 天的相關資訊。若要檢閱其他日期的每日總計 (例如四個月前的日期)，您可以使用報告 Cmdlet 達到此目的。

系統管理員也可能會想要閱讀[使用 Excel 擷取 Office 365 報告資料](http://msdn.microsoft.com/en-us/library/dn781442.aspx)一文。該文章說明如何使用 Microsoft Excel 中的 OData 資料查詢功能來建立自訂的 Office 365 報告。自訂報告可讓您規定要從 Office 365 報告服務傳回哪些資料 (及資料量)。自訂報告也能讓您執行許多工作 (例如指定資料的排序和分組方式)，以及存取 Office 365 管理中心未顯示的資訊。

具有開發背景的系統管理員可以使用 REST Web 服務取得 商務用 Skype Online 系統管理中心所未顯示的資訊。REST 服務類似 SOAP 服務；這兩項技術均可用於在用戶端與伺服器之間傳輸 XML 資料。然而，REST 服務比起 SOAP 服務多了至少兩項優勢：首先，REST 會使用標準化格式執行 XML 資料傳輸，稱為 ATOM Syndication 格式。相較之下，SOAP 在傳輸資料時使用的是非標準格式。再者，REST 能夠在封鎖 GET 與 POST 以外之 HTTP 指令動詞的網站上傳輸資料。

## 請參閱

#### 概念

[Lync Online 報告](https://technet.microsoft.com/zh-tw/library/dn362827\(v=ocs.15\))  

#### 其他資源

[Office 365 報告 Web 服務](http://msdn.microsoft.com/en-us/library/office/jj984325.aspx)  
[了解 Office 365 報告 Web 服務](http://msdn.microsoft.com/en-us/library/office/jj984321.aspx)  
[Exchange Online 線上報告 Cmdlet](http://technet.microsoft.com/en-us/library/jj200780\(v=exchg.150\).aspx)  
[使用 Excel 擷取 Office 365 報告資料](http://msdn.microsoft.com/en-us/library/dn781442.aspx)

