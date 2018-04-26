---
title: Lync Server 2013：分支網站恢復解決方案
TOCTitle: 分支網站恢復解決方案
ms:assetid: 1700f99b-709c-4e47-88eb-c0a5490e26e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398234(v=OCS.15)
ms:contentKeyID: 49290209
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的分支網站恢復解決方案

 

_**上次修改主題的時間：** 2015-03-09_

為您的組織提供分支網站恢復能力的好處是顯而易見的。明確的說，當您與中央網站之間的連線中斷時，分支網站使用者仍將持續保有 企業語音服務和語音信箱功能 (若您設定語音信箱重新路由設定的話；如需詳細資訊，請參閱＜ [Lync Server 2013 的分支網站復原需求](lync-server-2013-branch-site-resiliency-requirements.md)＞)。但對於使用者人數低於 25 位的網站而言，恢復能力解決方案所提供的投資報酬率可能不夠。

如果您決定要提供分支網站恢復能力，您有三個選項。下表可協助您判斷最適合您的組織之選項。



<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果您...</th>
<th>建議您使用...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在您的分支網站上主控 25 到 1000 名使用者，且投資報酬率不足以支應完整部署，或是不具本機管理支援</p></td>
<td><p>Survivable Branch Appliance</p>
<p>Survivable Branch Appliance 是業界標準的刀鋒伺服器，配備有執行於 Windows Server 2008 R2 上的 Lync Server 登錄器與中繼伺服器。 Survivable Branch Appliance 也包含公用交換電話網路 (PSTN) 閘道。合格的第三方裝置 (由參與 Survivable Branch Appliance (SBA) 資格/認證方案的 Microsoft 協力廠商所開發) 在 WAN 失效時仍可提供持續的 PSTN 連線，但這個方法無法提供可恢復的顯示狀態與會議功能，因為這些功能依存於中央網站上的前端伺服器。</p>
<p>如需 Survivable Branch Appliance 的詳細資訊，請參閱本主題稍後的＜Survivable Branch Appliance 詳細資料＞。</p>
<p><strong>注意：</strong> 如果您還要以 SIP 主幹與 Survivable Branch Appliance 搭配使用，請與 Survivable Branch Appliance 廠商連絡，以了解您的組織最適合的服務提供者。</p></td>
</tr>
<tr class="even">
<td><p>在分支網站上主控 1000 到 2000 名使用者、缺少可恢復的 WAN 連線，有經過訓練的 Lync Server 系統管理員</p></td>
<td><p>Survivable Branch 伺服器或兩個 Survivable Branch Appliance。</p>
<p>Survivable Branch 伺服器是符合指定硬體需求的 Windows Server，上面安裝了 Lync Server 登錄器與中繼伺服器軟體。該伺服器必須將 PSTN 閘道或 SIP 主幹連線至電話服務提供者。</p>
<p>如需 Survivable Branch 伺服器的詳細資訊，請參閱本主題稍後的＜ Survivable Branch 伺服器詳細資料＞。</p></td>
</tr>
<tr class="odd">
<td><p>如果您高達 5000 名的使用者除了語音功能以外還需要目前狀態與會議功能，且您擁有經過訓練的 Lync Server 系統管理員</p></td>
<td><p>以 Standard Edition Server 部署為中央網站，而非分支網站。</p>
<p>完整的 Lync Server 部署在 WAN 失效的情況下，仍可提供持續的 PSTN 連線，以及可恢復的目前狀態與會議功能。</p>
<p>如需有關為此解決方案做準備的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-your-organization.md">Lync Server 2013 的組織規劃</a>＞、＜ <a href="lync-server-2013-determining-your-system-requirements.md">判定 Lync Server 2013 的系統需求</a>＞、＜ <a href="lync-server-2013-determining-your-infrastructure-requirements.md">判斷 Lync Server 2013 的基礎結構需求</a>＞，以及其他相關章節。</p></td>
</tr>
</tbody>
</table>


## 恢復能力拓撲

下圖顯示分支網站恢復能力所適用的建議拓撲。

**分支網站恢復能力選項**

![語音分支恢復能力選項](images/Gg398234.47eecd19-08ae-4d82-acbe-61f0de760306(OCS.15).jpg "語音分支恢復能力選項")

## Survivable Branch Appliance 詳細資料

Lync Server Survivable Branch Appliance 包含下列元件：

  - 使用者驗證、登錄與通話路由所需的登錄器

  - 用以處理登錄器與 PSTN 閘道間往來訊號的中繼伺服器

  - 在 WAN 中斷時，用以將通話路由至 PSTN 作為後援傳輸的 PSTN 閘道

  - 供本機使用者存放資料的 SQL Server Express

Survivable Branch Appliance 也包含 PSTN 主幹、類比連接埠與乙太網路介面卡。

如果分支網站對中央網站的 WAN 連線中斷，內部分支使用者仍可透過 Survivable Branch Appliance 登錄器繼續進行登錄，並且可使用 Survivable Branch Appliance 對 PSTN 的連線保有不中斷的語音服務。當分支網站的 WAN 連結無法使用時，從家中或其他遠端位置連線的分支網站使用者將可使用中央網站上的登錄器伺服器進行登錄。這些使用者將可擁有完整的整合通訊功能，但有一例外，傳入分支網站的來電會轉接至語音信箱。當 WAN 連線恢復時，分支網站使用者即應可重獲完整的功能。無論是容錯移轉至 Survivable Branch Appliance 還是還原服務，都不需要 IT 系統管理員親自處理。

Lync Server 在 分支網站最多支援兩個 Survivable Branch Appliance。

## Survivable Branch Appliance 部署概觀

Survivable Branch Appliance 是由原始設備廠商與 Microsoft 合作製造，再由加值零售商代理部署的。此部署應在 Lync Server 部署於中央網站上、分支網站的 WAN 連線建置完成，且分支網站使用者能夠使用 企業語音後，才能執行。

如需這些階段的詳細資訊，請參閱部署文件中的＜ [使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-deploying-a-survivable-branch-appliance-or-server.md)＞。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>使用者權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>為 Survivable Branch Appliance 設定 Active Directory 網域服務</p></td>
<td><p><strong>在中央網站上：</strong></p>
<ol>
<li><p>為負責在分支網站上安裝及啟動 Survivable Branch Appliance 的技術人員建立網域使用者帳戶 (或企業身分識別)。</p></li>
<li><p>為 Active Directory 網域服務中的 Survivable Branch Appliance 建立電腦帳戶 (具有適用的完整網域名稱 (FQDN))。</p></li>
<li><p>在 拓撲產生器中建立並發行 Survivable Branch Appliance。</p></li>
</ol></td>
<td><p>技術人員的使用者帳戶必須是 RTCUniversalSBATechnicians 的成員。 Survivable Branch Appliance 必須屬於 RTCSBAUniversalServices 群組，這在您使用拓撲產生器時會自動完成。</p></td>
</tr>
<tr class="even">
<td><p>安裝並啟動 Survivable Branch Appliance。</p></td>
<td><p><strong>在分支網站上：</strong></p>
<ol>
<li><p>將 Survivable Branch Appliance 連線至乙太網路連接埠與 PSTN 連接埠。</p></li>
<li><p>啟動 Survivable Branch Appliance。</p></li>
<li><p>使用在中央網站上為 Survivable Branch Appliance 建立的網域使用者帳戶，將 Survivable Branch Appliance 加入網域中。設定 FQDN 與 IP 位址，使其符合在電腦帳戶中建立的 FQDN。</p></li>
<li><p>使用 OEM 使用者介面設定 Survivable Branch Appliance。</p></li>
<li><p>測試 PSTN 連線。</p></li>
</ol></td>
<td><p>技術人員的使用者帳戶必須是 RTCUniversalSBATechnicians 的成員。</p></td>
</tr>
</tbody>
</table>


## Survivable Branch Server 詳細資料

在 拓撲產生器中建立分支網站、將 Survivable Branch 伺服器 新增至該網站，然後在要安裝角色的電腦上執行 Lync Server 部署精靈。

## 請參閱

#### 其他資源

[部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)

