---
title: Lync Server 2013 的 Active Directory 網域服務
TOCTitle: Lync Server 2013 的 Active Directory 網域服務
ms:assetid: 5483afd5-d8af-4825-ae95-a82dbe941dbf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn481129(v=OCS.15)
ms:contentKeyID: 59679123
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 Active Directory 網域服務

 

_**上次修改主題的時間：** 2015-03-09_

Active Directory 網域服務 的功能是作為 Windows Server 2003、Windows Server 2008、Windows Server 2012 及 Windows Server 2012 R2 網路的目錄服務。Active Directory 網域服務 也是 Microsoft Lync Server 2013 安全性基礎結構的建立基礎。本節的目的在於說明 Lync Server 2013 如何使用 Active Directory 網域服務，來為 IM、Web 會議、媒體和語音建立值得信任的環境。如需 Active Directory 網域服務 之 Lync Server 延伸的詳細資料，以及為 Active Directory 網域服務 準備環境的詳細資料，請參閱＜部署＞文件中的[為 Lync Server 2013 準備 Active Directory 網域服務](lync-server-2013-preparing-active-directory-domain-services.md)。如需 Windows Server 網路中Active Directory 網域服務 的角色詳細資料，請參閱所使用作業系統版本的文件。

Lync Server 2013 使用 Active Directory 網域服務 儲存：

  - 在樹系中執行 Lync Server 2013 之所有伺服器需要的通用設定。

  - 在樹系中可識別執行 Lync Server 2013 之所有伺服器角色的服務資訊。

  - 一些使用者設定。

## Active Directory 基礎結構

Active Directory 的基礎結構需求包括下列：

  - 網域控制站的作業系統需求

  - 網域和樹系功能等級需求

  - 通用類別目錄網域需求

如需詳細資訊，請參閱＜部署＞文件中的 [Lync Server 2013 的 Active Directory 基礎結構需求](lync-server-2013-active-directory-infrastructure-requirements.md)。

## Active Directory 網域服務 準備

> [!NOTE]  
> 建議您將通用設定部署到設定容器，而不要部署到系統容器。這樣不會增強安全性，但可以為部分 Active Directory 網域服務 拓撲提升延展性。如果您是從 Microsoft Office Communications Server 2007 移轉，而且已使用系統容器，但是計劃要使用設定容器，則「必須先」移動系統容器中的設定，「之後」再進行任何升級準備工作。若要將您的系統容器設定移轉至設定容器，請參閱＜Office Communications Server 2007 通用設定移轉工具＞(英文)：<a href="http://go.microsoft.com/fwlink/p/?linkid=145236">http://go.microsoft.com/fwlink/p/?LinkId=145236</a>。



部署 Lync Server 2013 時，第一步是準備 Active Directory 網域服務。為 Lync Server 2013 準備 Active Directory 網域服務 時，包含下列三個步驟：

  - **準備架構**。這項工作會擴充 Active Directory 網域服務 中的架構，以包含 Lync Server 2013 專用的類別和屬性。如需準備架構的詳細資料，請參閱＜部署＞文件中的[在 Lync Server 2013 中執行 Active Directory 架構準備](lync-server-2013-running-schema-preparation.md)。如需詳細資料，請參閱[從 Office Communications Server 2007 R2 移轉至 Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md)。

  - **準備樹系**。這項工作會在樹系根網域中建立通用設定和物件，以及控管這些設定和物件存取權的萬用服務和系統管理群組。如需準備樹系的詳細資料，請參閱＜部署＞文件中的[針對 Lync Server 2013 執行樹系準備](lync-server-2013-running-forest-preparation.md)。

  - **準備網域**。這項工作會將必要的存取控制項目 (ACE) 新增至萬用群組，而這些群組會授予權限來裝載和管理網域內的使用者。在要部署執行 Lync Server 2013 之伺服器的所有網域中，以及 Lync Server 使用者所在的任何網域中，都必須完成這項工作。如需準備網域的詳細資料，請參閱＜部署＞文件中的[為 Lync Server 2013 執行網域準備](lync-server-2013-running-domain-preparation.md)。

如需準備 Active Directory 之完整程序及執行每個步驟所需之權限的概觀，請參閱＜部署＞文件中的 [Lync Server 2013 的 Active Directory 基礎結構需求](lync-server-2013-active-directory-infrastructure-requirements.md)。

## 萬用群組

在準備樹系期間，Lync Server 2013 會在有權存取及管理通用設定和服務的 Active Directory 網域服務 內，建立各種萬用群組。這些萬用群組包括：

  - **系統管理群組**。這些群組定義了 Lync Server網路的基本系統管理員角色。在準備樹系期間，這些系統管理員群組會新增到 Lync Server 基礎結構群組。

  - **服務群組**。這些群組是存取 Lync Server 所提供各種服務時所需的服務帳戶。

  - **基礎結構群組**。這些群組提供了存取 Lync Server 基礎結構中特定區域的權限。其功能是作為系統管理群組的元件，因此您不應修改這些群組或直接將使用者新增到其中。在準備樹系期間，會新增特定服務及系統管理群組到適當的基礎結構群組。

如需深入瞭解在為 Lync Server 準備 AD 時建立的特定萬用群組，以及新增至基礎結構群組的服務和系統管理群組，請參閱＜部署＞文件中的[Lync Server 2013 中的樹系準備所進行的變更](lync-server-2013-changes-made-by-forest-preparation.md)。

> [!NOTE]  
> Lync Server 2013 可針對執行 Lync Server 2013 的伺服器，支援 Windows Server 2012 中的萬用群組，並支援網域控制站使用 Windows Server 2003 作業系統。 萬用群組的成員可以包括網域樹狀目錄或樹系中任何網域的其他群組和帳戶，而且可在網域樹狀目錄或樹系中的任何網域獲指派權限。萬用群組支援加上系統管理員委派，即可簡化 Lync Server 部署的管理工作。例如，您不需要為了讓系統管理員能夠同時管理兩個網域，而將一個網域加入另一個網域。



## 角色型存取控制

除了建立萬用服務和系統管理群組，以及新增服務和系統管理群組至適當的萬用群組之外，樹系準備工作也會建立角色型存取控制 (RBAC) 群組。如需樹系準備工作所建立之特定 RBAC 群組的詳細資料，請參閱＜部署＞文件中的[Lync Server 2013 中的樹系準備所進行的變更](lync-server-2013-changes-made-by-forest-preparation.md)。如需 RBAC 群組的詳細資訊，請參閱 [Lync Server 2013 的角色型存取控制 (RBAC)](lync-server-2013-role-based-access-control-rbac.md)。

## 存取控制項目 (ACE) 及繼承

樹系準備會建立私人與公用 ACE，並為其建立的萬用群組新增 ACE。它會在 Lync Server 使用的通用設定容器上建立特定的私人 ACE。此容器僅會由 Lync Server 使用，且位於根網域的設定容器或系統容器中，視您儲存通用設定的位置而定。

網域準備步驟會將必要的存取控制項目 (ACE) 新增至萬用群組，而這些群組會授與權限來裝載和管理網域內的使用者。網域準備作業會在網域根目錄和三個內建容器上建立 ACE：使用者、電腦和網域控制站。

如需樹系準備及網域準備所建立和新增之公用 ACE 的詳細資料，請參閱＜部署＞文件中的[Lync Server 2013 中的樹系準備所進行的變更](lync-server-2013-changes-made-by-forest-preparation.md)及[Lync Server 2013 中的網域準備所進行的變更](lync-server-2013-changes-made-by-domain-preparation.md)。

組織經常會鎖定 Active Directory 網域服務 (AD DS) ，以減低安全性風險。不過，鎖定的 Active Directory 環境可能會限制 Lync Server 2013 所需的權限。這其中可能包括從容器和 OU 移除 ACE，以及停用 User、Contact、InetOrgPerson 或 Computer 物件的權限繼承。在鎖定的 Active Directory 環境中，必須在需要權限的容器和 OU 上手動設定權限。如需詳細資料，請參閱＜部署＞文件中的[在 Lync Server 2013 中準備鎖定的 Active Directory 網域服務](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md)。

## 伺服器資訊

在啟動期間， Lync Server 2013 會將伺服器資訊發行到 Active Directory 網域服務 中的下列三個位置：

  - 每個 Active Directory 電腦物件上對應於 Lync Server 2013 安裝所在之實體電腦的服務連線點 (SCP)。

  - 在 **msRTCSIP-Pools** 類別的容器中建立的伺服器物件。

  - 拓撲產生器 中指定的受信任伺服器。

## 服務連線點

Active Directory 網域服務 中的每個 Lync Server 2013 物件都有一個稱為「RTC 服務」的 SCP，其中包含許多屬性，可識別每部電腦並指定其提供的服務。其中較重要的 SCP 屬性包括 *serviceDNSName*、*serviceDNSNameType*、*serviceClassname* 和 *serviceBindingInformation*。 協力廠商資產管理應用程式可比對這些項目和其他 SCP 屬性來執行查詢，以在部署中擷取伺服器資訊。

## Active Directory 伺服器物件

每個 Lync Server 2013 伺服器角色都有對應的 Active Directory 物件，其屬性會定義該角色提供的服務。此外，啟動 Standard Edition 伺服器 伺服器或建立 Enterprise Edition 集區時，Lync Server 2013 就會在**msRTCSIP-Pools** 容器中建立新的 **msRTCSIP-Pool** 物件。**msRTCSIP-Pool** 類別會指定集區的完整網域名稱 (FQDN)，以及集區前端和後端元件之間的關聯性。(Standard Edition 伺服器 會視為邏輯集區，其前端和後端會配置在同一部電腦上。)

## 受信任伺服器

在 Lync Server 2013 中，受信任伺服器是您在執行 拓撲產生器 及發行拓撲時指定的伺服器。發行的拓撲 (包括所有伺服器資訊) 會儲存在中央管理存放區中。 只有中央管理存放區中定義的伺服器會受到信任。在 Lync Server 2013 中，受信任伺服器符合下列準則：

  - 伺服器的 FQDN 出現在儲存於中央管理存放區的拓撲中。

  - 伺服器顯示來自受信任 CA 的有效憑證。如需詳細資料，請參閱 [Lync Server 2013 的憑證基礎結構需求](lync-server-2013-certificate-infrastructure-requirements.md)。

如果不符合這些條件，則伺服器就不受信任，其連線也會遭拒。這項雙重需求能避免惡意伺服器嘗試佔用有效伺服器 FQDN 的可能 (即使不太可能) 攻擊。

此外，為了讓 Microsoft Office Communications Server 2007 R2 及 Microsoft Office Communications Server 2007 部署能夠與 Lync Server 2013 伺服器通訊，Lync Server 2013 會在樹系準備期間建立容器，以容納舊版受信任伺服器的清單。下表說明為與舊版部署相容而建立的容器。

### 與舊版間的相容性：受信任伺服器清單及其 Active Directory 容器

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>受信任伺服器清單</th>
<th>Active Directory 容器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Standard Edition 伺服器和 Enterprise 集區前端伺服器</p></td>
<td><p>RTC 服務/通用設定</p></td>
</tr>
<tr class="even">
<td><p>會議伺服器</p></td>
<td><p>RTC 服務/信任的 MCU</p></td>
</tr>
<tr class="odd">
<td><p>Web 元件伺服器</p></td>
<td><p>RTC 服務/TrustedWebComponentsServers</p></td>
</tr>
<tr class="even">
<td><p>中繼伺服器及 Communicator Web Access Server、應用程式伺服器、含 QoE 的登錄器、A/V 會議服務 (還有協力廠商 SIP 伺服器)</p></td>
<td><p>RTC 服務/信任的服務</p></td>
</tr>
<tr class="odd">
<td><p>Proxy 伺服器</p></td>
<td><p>Lync Server 2013 不支援 Proxy 伺服器的回溯相容性</p></td>
</tr>
</tbody>
</table>


若要支援舊版的受信任伺服器，您必須執行最佳做法分析程式工具。如需執行最佳做法分析程式的詳細資料，請參閱 [http://go.microsoft.com/fwlink/p/?LinkId=330633](http://go.microsoft.com/fwlink/p/?linkid=330633)。

