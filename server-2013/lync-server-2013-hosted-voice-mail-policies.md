---
title: Lync Server 2013：主控語音信箱原則
TOCTitle: 主控語音信箱原則
ms:assetid: d62a35ed-cbe2-4f06-86b4-e192c18435c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398932(v=OCS.15)
ms:contentKeyID: 49292425
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主控語音信箱原則

 

_**上次修改主題的時間：** 2012-10-01_

「裝載語音信箱原則」 提供資訊給 Lync Server 2013 ExUM Routing 應用程式，指定撥給信箱位於所裝載 Exchange 服務上使用者的電話應路由至何處。

> [!NOTE]  
> 只有與裝載的 Exchange UM 進行 Lync Server 2013 整合時，才需要裝載語音信箱原則。與內部部署 Exchange UM 整合時則不需要。



## 裝載語音信箱原則範圍

裝載語音信箱原則範圍會決定套用原則的階層式層級。您可以使用下列範圍層級，設定裝載語音信箱原則：

  - 「全域」 原則會影響 Lync Server 2013 部署中的所有使用者。如果使用者可以存取裝載的 Exchange UM，且尚未被指派個別使用者原則，如果尚未將網站原則指派給使用者的網站，則會套用全域原則。全域原則會隨 Lync Server 2013 一起安裝。您可以修改該原則以符合您的需求，但無法將它重新命名或刪除。

  - 「網站」 原則會影響為其定義原則之網站所屬的所有使用者。如果使用者已針對主控 Exchange UM 存取進行設定，且未獲指派個別使用者原則，便會套用網站原則。

  - *個別使用者* 原則只會影響個別使用者或群組。若要強制執行個別使用者原則，必須明確地將原則指派給個別使用者、群組和連絡人物件。

> [!NOTE]  
> 在大多數情況下，只需要一個裝載的語音信箱原則。您通常可以修改全域原則來符合所有需求。如果部署多個裝載語音信箱原則，所有這類原則都會有個別使用者範圍。



## 裝載語音信箱原則屬性

語音信箱原則會定義兩個屬性， Lync Server 2013 ExUM 路由應用程式會將其插入 INVITE 訊息的要求 URI 中，此 INVITE 訊息會傳送至裝載的 Exchange UM 實作：

  - **Destination ：**裝載的 Exchange UM 服務的完整網域名稱 (FQDN)。這個值是供內部部署 Lync Server Edge Server 用於路由目的。
    
    > [!NOTE]  
    > Exchange Online 的 FQDN 為 exap.um.outlook.com。
    


  - **Organization ：**您的 Lync Server 2013 使用者信箱所屬之裝載 Exchange UM 服務的承租人 FQDN。語音信箱原則可能包含多個組織。如果原則中包含一個以上的組織，這個屬性必須是您的 Lync Server 2013 使用者信箱所屬之 Exchange Server 承租人的逗號分隔清單。

> [!NOTE]  
> 您的裝載 Exchange UM 服務的承租人系統管理員，將會為 Destination 和 Organization 屬性設定提供必要值。若要設定您的原則，必須執行 New-CsHostedVoicemailPolicy Cmdlet，或使用 Set-CsHostedVoicemailPolicy Cmdlet 來修改現有的原則 (例如，全域原則)。



如需管理裝載語音信箱原則的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - New-CsHostedVoicemailPolicy

  - Set-CsHostedVoicemailPolicy

  - Get-CsHostedVoicemailPolicy

## 個別使用者語音信箱原則指派

如果是以個別使用者範圍定義裝載的語音信箱原則，您必須明確地指派它。您可以執行 Grant-CsHostedVoicemailPolicy Cmdlet，將原則指派給個別使用者或群組。

如需指派或移除個別使用者裝載語音信箱原則的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - Grant-CsHostedVoicemailPolicy

  - Remove-CsHostedVoicemailPolicy

