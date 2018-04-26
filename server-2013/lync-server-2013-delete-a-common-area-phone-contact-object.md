---
title: 刪除公共區域電話連絡人物件
TOCTitle: 刪除公共區域電話連絡人物件
ms:assetid: f4c139dc-f07c-4c75-9345-e291aea41173
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994087(v=OCS.15)
ms:contentKeyID: 52056264
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除公共區域電話連絡人物件

 

_**上次修改主題的時間：** 2013-02-20_

您可能想刪除與公共區域電話相關聯的連絡人物件。例如，若您將電話從員工休息室移除，那麼不需要具備與該電話相關聯的連絡人物件。**Remove-CsCommonAreaPhone** Cmdlet 提供一個方法，可讓您刪除公共區域電話帳號。當您執行此 Cmdlet 時，將會透過回傳的 **Get-CsCommonAreaPhone** 從公共區域電話清單刪除該電話。另外，與該電話相關聯的連絡人物件將從 Active Directory 網域服務 刪除。

使用 **Remove-CsCommonAreaPhone** 移除一個或所有具有共同項目 (如：顯示名稱或國家/區域代碼) 的公共區域電話。您可以從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這個 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。


## 移除指定的公共區域電話

  - 下列命令透過 SIP 位址 sip:mainlobby@litwareinc.com 移除公共區域電話：
    
        Remove-CsCommonAreaPhone -Identity "sip:mainlobby@litwareinc.com"

## 根據顯示名稱移除公共區域電話

  - 此命令會移除所有顯示名稱包含 "Building 14" 字串值的公共區域電話：
    
        Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -match "Building 14"} | Remove-CsCommonAreaPhone

## 根據國家及區域代碼移除公共區域電話

  - 此命令會移除所有美國 (國家代碼 1) 及區域代碼為 425 的公共區域電話：
    
        Get-CsCommonAreaPhone | Where-Object {$_.LineUri  -match "^tel:\+1425"} | Remove-CsCommonAreaPhone

如需詳細資訊，請參閱＜[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)＞ Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)

