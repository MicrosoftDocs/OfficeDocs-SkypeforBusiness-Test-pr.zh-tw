---
title: 移動會議目錄
TOCTitle: 移動會議目錄
ms:assetid: 71a28308-1f3b-4717-b535-2f4bfe3499a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204994(v=OCS.15)
ms:contentKeyID: 49291285
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移動會議目錄

 

_**上次修改主題的時間：** 2012-10-04_

在解除委任集區前，您必須針對 Office Communications Server 2007 R2 中的每個會議目錄執行下列程序。

## 將會議目錄移至 Lync Server 2013

1.  開啟 Lync Server 管理命令介面。

2.  若要取得組織中會議目錄的識別資料，請執行下列命令：
    
        Get-CsConferenceDirectory
    
    由於此 Cmdlet 會傳回組織中的所有會議目錄，所以您可能會想要將結果限定在您要解除委任的集區。例如，如果您想要解除委任完整網域名稱 (FQDN) 為 pool01.contoso.net 的集區：
    
        Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "pool01.contoso.net"}
    
    此 Cmdlet 會傳回內含 FQDN pool01.contoso.net 之服務 ID 的所有會議目錄。

3.  若要移動會議目錄，請針對集區中的每個會議記錄執行下列動作：
    
        Move-CsConferenceDirectory -Identity <Numeric identity of conference directory> -TargetPool <FQDN of pool where ownership is to be transitioned>
    
    例如：
    
        Move-CsConferenceDirectory -Identity 3 -TargetPool pool02.contoso.net

> [!NOTE]  
> 可能會發生錯誤 (顯示於下方)，原因在於 Lync Server 管理命令介面需要 Active Directory 的已更新權限集合。若要解決錯誤，請關閉目前視窗，開啟新的 Lync Server 管理命令介面並再執行一次命令。



![Move-CsConferenceDirectory 錯誤輸出](images/JJ204994.4748b9e8-9651-4527-afe1-cbdc6d5ce4a8(OCS.15).jpg "Move-CsConferenceDirectory 錯誤輸出")

