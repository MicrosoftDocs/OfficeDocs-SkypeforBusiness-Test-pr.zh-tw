---
title: 設定大型會議的支援
TOCTitle: 設定大型會議的支援
ms:assetid: 8e22d34b-b395-408d-9d48-8f2a3abe9513
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205074(v=OCS.15)
ms:contentKeyID: 49291615
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定大型會議的支援

 

_**上次修改主題的時間：** 2014-05-12_

若要支援最多 1000 位使用者的大型會議，需要建立適當的拓撲、會議硬體和軟體先決條件，以及適當地設定環境。

## 拓撲需求

單一大型會議至少需要一部前端伺服器和一部後端伺服器。但是，若要提供高可用性，建議使用兩個含有鏡像的後端伺服器的前端伺服器集區。

舉行大型會議之使用者的使用者帳戶必須位於此集區。但是，不建議您在此集區裝載其他使用者帳戶。請僅將其用於大型會議。最佳做法是在此集區中建立特殊、僅用於舉行大型會議的使用者帳戶。由於大型會議的設定是針對效能最佳化，因此以一般使用者的身分使用時，可能會發生問題，像是涉及 PSTN 端點時，會無法將 P2P 工作階段升級為會議。

管理恰有兩個前端伺服器的集區時，需要某些特別考量。如需詳細資訊，請參閱[Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的拓撲和元件](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md)。

此外，若要針對用於大型會議的集區選擇性地提供災害復原備份與容錯移轉，您可以將該集區與其他資料中心中內具有類似設定的專用集區配對。如需詳細資訊，請參閱[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)。

![大型會議集區組態](images/JJ205074.ee00e1c0-c3b2-464d-aa89-a1e877cd034d(OCS.15).jpg "大型會議集區組態")

關於拓撲的其他附註包括：

  - 儲存會議內容時需要檔案共用，而且，如果已部署並啟用封存伺服器，則在儲存封存檔案時也需要檔案共用。檔案共用可以專屬於該集區，也可以是部署該網站上其他集區所使用的相同檔案共用。如需關於設定檔案共用的詳細資訊，請參閱＜[針對 Lync Server 2013 設定檔案儲存](lync-server-2013-configure-dfs-file-storage.md)＞。

  - 需要具備 Office Web Apps Server，才能在大型會議中啟用 PowerPoint 簡報功能。Office Web Apps Server 可以專屬於大型會議集區，也可以是部署專屬集區之網站上其他集區所使用的相同 Office Web Apps Server。

  - 前端伺服器的負載平衡要求適用於 HTTP 流量的硬體負載平衡 (例如，會議內容下載)。建議針對 SIP 流量使用 DNS 負載平衡。如需詳細資訊，請參閱＜[Lync Server 2013 中的負載平衡需求](lync-server-2013-load-balancing-requirements.md)＞。

  - 如果您想要針對專屬大型會議集區使用監控伺服器，建議使用監控伺服器及其資料庫，它們可以在您的 Lync Server 部署中的所有前端伺服器集區中加以共用。 .

## 硬體與軟體需求

專屬大型會議集區中伺服器的硬體需求，與您其他 Lync Server 2013 伺服器的硬體需求相同。如需關於硬體需求的詳細資訊，請參閱＜[Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)＞。

專屬大型會議集區中的伺服器必須符合所有 Lync Server 2013 軟體需求。如需關於軟體需求的詳細資訊，請參閱下列文件：

  - [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)

  - [Lync Server 2013 中的資料庫軟體支援](lync-server-2013-database-software-support.md)

  - [Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)

此外，這兩部 Lync Server 2013 和所有的 Lync Server 2013 用戶端都必須安裝最新更新。

## 組態需求

建議特別針對大型會議建立新的會議原則，然後將該會議原則指派給位於專屬大型會議集區的使用者。使用下列設定來設定會議原則：

  - 將 \[MaxMeetingSize\] 選項設定為 \[1000\] (預設值為 \[250\])。

  - 將 \[AllowLargeMeetings\] 選項設定為 \[True\]。

  - 將 \[EnableAppDesktopSharing\] 選項設定為 \[無\]。

  - 將 \[AllowUserToScheduleMeetingsWithAppSharing\] 選項設定為 \[False\]。

  - 將 \[AllowSharedNotes\] 選項設定為 \[False\]。

  - 將 \[AllowAnnotations\] 選項設定為 \[False\]。

  - 將 \[DisablePowerPointAnnotations\] 選項設定為 \[True\]。

  - 將 \[AllowMultiview\] 選項設定為 \[False\]。

  - 將 \[EnableMultiviewJoin\] 選項設定為 \[False\]。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Lync Server 2013 中支援 1000 位使用者的大型會議時，需要在適用於會議排程器的會議原則中，將 [AllowLargeMeetings] 設定設為 True。將此設定設為 True 時，如果使用者加入這類會議，即會針對額外的大型會議，將 Lync 使用經驗最佳化。特別是在大型會議中，Lync 將不會顯示最初或更新的完整與會者清單，此為用戶端與 Lync Server 2013 的效能瓶頸。Lync 將改為僅顯示使用者的相關資訊和會議簡報者的清單。Lync 仍會正確顯示可在大型會議中的參與者總人數。</td>
</tr>
</tbody>
</table>


除了 \[最大會議大小\] 設定之外，此處指定的所有其他會議原則設定都是必要的，以停用大型會議中不需要的會議功能。

此外，您需要設定專屬的大型會議集區，如此，每個位於該集區且負責管理會議排程的 Lync Server 2013 使用者都能具備適當的權限。若要這樣做，請執行下列動作：

  - 將 \[指定為簡報者\] 選項設定為 \[無\]。一般而言，在大型會議的所有參與者中，只有一位或只有一些使用者會是簡報者，因此，不應自動准許參與者成為大型會議中的簡報者，而是應該在會議排程期間明確指定簡報者，或者在大型會議期間明確地晉升為簡報者。

  - 確定未選取 \[預設指派的會議類型\] 核取方塊。此設定會控制 Lync 2013 的線上會議增益集 是否一律會使用召集人指派的會議來排程會議，這表示排程的會議具備相同的加入 URL 和音訊資訊，在小型群組的共同作業案例中，具備這類指派的會議類型非常有用，因為每個人都會有他們自己個別指派的會議，而且固定的加入 URL 和音訊資訊有助於讓會議加入速度更快速。但是，在大型會議案例中，大型會議支援員工使用單一組的使用者認證來排程大型會議，然後將加入 URL 和音訊資訊提供給會議申請者。在此情況下，比較適合使用不同的 URL 來加入每個會議。

  - 確定未選取 \[預設允許匿名使用者\] 核取方塊 (除非它是必要選項)。若未使用指派的會議，此設定就會影響 Lync 2013 的線上會議增益集所排程的預設會議存取類型。此設定的適當選項會根據組織的需求而定。如果組織中大部分的大型會議都是內部會議，請不要選取此選項。如果大部分的大型會議都需要讓外部使用者能夠加入，則請選取此選項。

