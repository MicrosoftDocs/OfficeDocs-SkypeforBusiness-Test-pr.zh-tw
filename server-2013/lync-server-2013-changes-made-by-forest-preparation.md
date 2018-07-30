---
title: Lync Server 2013 中的樹系準備所進行的變更
TOCTitle: Lync Server 2013 中的樹系準備所進行的變更
ms:assetid: 2e12613e-59f2-4810-a32d-24a9789a4a6e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425791(v=OCS.15)
ms:contentKeyID: 49290458
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的樹系準備所進行的變更

 

_**上次修改主題的時間：** 2015-03-09_

本節將說明樹系準備步驟所建立的全域設定與物件，以及萬用服務和管理群組。

## Active Directory 全域設定和物件

如果您將全域設定儲存在「設定」容器中 (如同全新 Lync Server 2013 部署的作法)，則樹系準備會使用現有的「服務」容器，並在 Configuration\\Services 物件下新增 **RTC Service**物件。在 RTC 服務物件下，樹系準備會新增 msRTCSIP-GlobalContainer 類型的**Global Settings**物件。全域設定物件包含會套用到 Lync Server 部署的所有設定。如果您將全域設定儲存在「系統」容器中，則樹系準備會使用根網域「系統」容器下的 Microsoft 容器，並在 System\\Microsoft 物件下新增 RTC 服務物件。

樹系準備也會針對執行程序的根網域，新增 **msRTCSIP-Domain** 物件。

## Active Directory 萬用服務和管理群組

樹系準備也會根據您指定的網域建立萬用群組，並為這些群組新增存取控制項目 (ACE)。這個步驟會在您指定之網域的使用者容器中，建立萬用群組。

萬用群組允許管理員存取以及管理全域設定和服務。樹系準備會新增下列類型的萬用群組：

  - **系統管理群組**   這些群組會定義 Lync Server 網路的管理員角色。

  - **基礎結構群組**   這些群組提供 Lync Server 基礎結構的特定區域權限。它們可做為系統管理群組元件的功能來運作。您不應該修改這些群組或將使用者直接新增至這些群組中。

  - **服務群組**   這些群組是存取各種 Lync Server 服務時所需的服務帳戶。

下表說明系統管理群組。

### 樹系準備時建立的系統管理群組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>系統管理群組</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCUniversalServerAdmins</p></td>
<td><p>允許成員管理伺服器和集區設定，包括所有伺服器角色、全域設定以及使用者。</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>可讓成員管理使用者設定，也可以將使用者從一個伺服器或集區移到另一個伺服器或集區。</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalReadOnlyAdmins</p></td>
<td><p>可讓成員讀取伺服器、集區和使用者設定。</p></td>
</tr>
</tbody>
</table>


下表說明基礎結構群組。

### 樹系準備時建立的基礎結構群組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>基礎結構群組</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCUniversalGlobalWriteGroup</p></td>
<td><p>授與 Lync Server 之全域設定物件的寫入存取權。</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalGlobalReadOnlyGroup</p></td>
<td><p>授與 Lync Server 之全域設定物件的唯讀存取權。</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>授與 Lync Server 使用者設定的唯讀存取權。</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>授與 Lync Server 設定的唯讀存取權。這個群組沒有集區層級設定的存取權，只能存取個別伺服器特有的設定。</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalSBATechnicians</p></td>
<td><p>授與 Lync Server 設定的唯讀存取權，並且在安裝期間，會放在 Survivable Branch Appliance 的 Local Administrators 群組中。</p></td>
</tr>
</tbody>
</table>


下表說明服務群組。

### 樹系準備時建立的服務群組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>服務群組</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>包含用以執行前端伺服器和 Standard Edition Server 的服務帳戶。此群組可讓伺服器讀取/寫入 Lync Server 全域設定和 Active Directory 使用者物件。</p></td>
</tr>
<tr class="even">
<td><p>RTCComponentUniversalServices</p></td>
<td><p>包含用以執行 A/V 會議伺服器、Web 服務、中繼伺服器、封存伺服器與監控伺服器的服務帳戶。</p></td>
</tr>
<tr class="odd">
<td><p>RTCProxyUniversalServices</p></td>
<td><p>包含用以執行 Lync Server Edge Server 的服務帳戶。</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalConfigReplicator</p></td>
<td><p>包括可參與 Lync Server中央管理存放區複寫的伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>RTCSBAUniversalServices</p></td>
<td><p>授與 Lync Server 設定的唯讀存取權，但可容許設定 Survivable Branch 伺服器和 Survivable Branch Appliance 部署的安裝。</p></td>
</tr>
</tbody>
</table>


接著，樹系準備會將服務和管理群組新增到適當的基礎結構群組，如下所示：

  - 新增 RTCUniversalServerAdmins 到 RTCUniversalGlobalReadOnlyGroup、RTCUniversalGlobalWriteGroup、RTCUniversalServerReadOnlyGroup 和 RTCUniversalUserReadOnlyGroup。

  - 新增 RTCUniversalUserAdmins 做為 RTCUniversalGlobalReadOnlyGroup、RTCUniversalServerReadOnlyGroup 和 RTCUniversalUserReadOnlyGroup 的成員。

  - 新增 RTCHSUniversalServices、RTCComponentUniversalServices 和 RTCUniversalReadOnlyAdmins 做為 RTCUniversalGlobalReadOnlyGroup、RTCUniversalServerReadOnlyGroup 和 RTCUniversalUserReadOnlyGroup 的成員。

樹系準備也會建立下列角色型存取控制 (RBAC) 群組：

  - CSAdministrator

  - CSArchivingAdministrator

  - CSHelpDesk

  - CSLocationAdministrator

  - CSResponseGroupAdministrator

  - CSServerAdministrator

  - CSUserAdministrator

  - CSViewOnlyAdministrator

  - CSVoiceAdministrator

  - CsPersistentChatAdministator

  - CsResponseGroupManager

如需 RBAC 角色以及各角色可執行的工作的詳細資訊，請參閱規劃文件中的＜[在 Lync Server 2013 中規劃角色型存取控制](lync-server-2013-planning-for-role-based-access-control.md)＞。

樹系準備會同時建立私人與公用 ACE。它會在 Lync Server 所使用的全域設定容器上建立私人 ACE。只有 Lync Server 會使用此容器，且該容器會位於根網域的設定容器或系統容器中，視您儲存全域設定的位置而定。樹系準備所建立的公用 ACE 列於下表。

### 樹系準備建立的公用 ACE。

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ACE</th>
<th>RTCUniversalGlobalReadOnlyGroup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>讀取根網域系統容器 (非繼承的)<strong>*</strong></p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>讀取設定的 DisplaySpecifiers 容器 (非繼承的)</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> <strong>*</strong>非繼承的 ACE 不會授與這些容器下子物件的存取權。繼承的 ACE 則會授與這些容器下子物件的存取權。



樹系準備會在組態命名內容下的設定容器上執行下列工作：

  - 在使用者、連絡人和 InetOrgPerson 之語言顯示規範的 adminContextMenu 和 adminPropertyPages 屬性下方，為 **RTC property** 頁面新增 **{AB255F23-2DBD-4bb6-891D-38754AC280EF}** 項目 (例如 CN=user-Display、CN=409、CN=DisplaySpecifiers)。

  - 在套用到 User 和 Contact 類別的 **Extended-Rights** 下方，新增 **controlAccessRight** 類型的 **RTCPropertySet** 物件。

  - 在套用到 User、Contact、OU 與 DomainDNS 類別的 **Extended-Rights** 下方，新增 **controlAccessRight** 類型的 **RTCUserSearchPropertySet** 物件。

  - 在每一個語言組織單位 (OU) 顯示規範 (例如，CN=organizationalUnit-Display,CN=409,CN=DisplaySpecifiers) 的 **extraColumns** 屬性下新增 **msRTCSIP-PrimaryUserAddress**，並複製預設顯示 (例如，CN=default-Display、CN=409、CN=DisplaySpecifiers) 的 **extraColumns** 屬性值。

  - 在 Users、Contacts 與 InetOrgPerson 物件的每一個語言顯示規範的 **attributeDisplayNames** 屬性下，新增 **msRTCSIP-PrimaryUserAddress**、**msRTCSIP-PrimaryHomeServer** 與 **msRTCSIP-UserEnabled** 篩選屬性 (以英文為例：CN=user-Display、CN=409、CN=DisplaySpecifiers)。

