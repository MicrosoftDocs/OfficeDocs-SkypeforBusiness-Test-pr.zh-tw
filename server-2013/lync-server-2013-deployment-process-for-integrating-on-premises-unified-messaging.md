---
title: Lync Server 2013：整合內部部署 Unified Messaging 的部署程序
TOCTitle: 整合內部部署 Unified Messaging 和 Lync Server 的部署程序
ms:assetid: 269a4436-f09f-415b-96ab-49a64370a385
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425737(v=OCS.15)
ms:contentKeyID: 49290382
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合內部部署 Unified Messaging 和 Lync Server 2013 的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

如果您要整合 Exchange 整合通訊 (UM) 與 Lync Server 2013，則必須執行本主題中所說明的工作。同時請確實檢閱＜ [整合內部部署 Unified Messaging 和 Lync Server 2013 的指導方針](lync-server-2013-guidelines-for-integrating-on-premises-unified-messaging.md)＞中所說明的規劃與部署最佳作法。本主題假設您已使用組合的中繼伺服器部署 Lync Server 2013，且您的使用者已可使用 Lync Server 2013，但假設您並不一定已依照部署文件的＜ [在 Lync Server 2013 中部署企業語音](lync-server-2013-deploying-enterprise-voice.md)＞中所說明，執行所有用以啟用 企業語音的部署與設定步驟。

## Unified Messaging 整合程序

> [!IMPORTANT]  
> 請務必洽詢組織的 Exchange 系統管理員，確認你們將執行的各項工作，以協助確保整合作業能夠順利完成。




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>所需群組和角色</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>部署下列其中一項：</p>
<ul>
<li><p>Microsoft Exchange Server 2007 Service Pack 1 (SP2) 或最新的 Service Pack</p></li>
<li><p>Microsoft Exchange Server 2010 或最新的 Service Pack</p></li>
<li><p>Microsoft Exchange Server 2013</p></li>
</ul></td>
<td><p>若您是使用 Microsoft Exchange Server 2013，請在與 Lync Server 2013 相同或不同的樹系中，安裝下列 Exchange Server 角色：</p>
<ul>
<li><p>Client Access</p></li>
<li><p>Mailbox</p></li>
</ul>
<p>如果 Microsoft Exchange Server 2013 與 Exchange 整合通訊 (UM) 安裝在不同的樹系中，請將每個 Exchange 樹系設定為信任 Lync Server 2013 樹系。</p>
<p>若您是使用 Exchange 2010，請在與 Lync Server 2013 相同或不同的樹系中，安裝下列 Exchange Server 角色：</p>
<ul>
<li><p>Unified Messaging</p></li>
<li><p>Hub Transport</p></li>
<li><p>Client Access</p></li>
<li><p>Mailbox</p></li>
</ul>
<p>如果 Lync Server 2013 與 Exchange 整合通訊 (UM) 安裝在不同的樹系中，請將每個 Exchange 樹系設定為信任 Lync Server 2013 樹系。</p></td>
<td><p>企業的系統管理員 (如果這是組織中的第一部 Exchange Server)</p>
<p>- 或者 -</p>
<p>Exchange 組織系統管理員 (如果這不是組織中的第一部 Exchange Server)</p></td>
<td><p>請參閱您的 Exchange Server 版本所適用的文件：</p>
<dl>
<dt><span></span></dt>
<dd><p>Exchange Server 2007 的部署文件，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268694%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268694&amp;clcid=0x404</a>。</p>
</dd>
<dt><span></span></dt>
<dd><p>Exchange Server 2010 或最新的 Service Pack 部署文件，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268695%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268695&amp;clcid=0x404</a>。</p>
</dd>
<dt><span></span></dt>
<dd><p>Microsoft Exchange Server 2013 規劃及部署，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=266569%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=266569&amp;clcid=0x404</a>。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>安裝憑證。</p></td>
<td><p>從信任的根憑證授權 (CA) 下載憑證，並為每部 Exchange UM 伺服器安裝。必須要有這些憑證，執行 Exchange UM 與 Lync Server 2013 的伺服器之間才會有相互傳輸層級安全性 (MTLS)。</p></td>
<td><p>系統管理員</p></td>
<td><p><a href="lync-server-2013-configure-certificates-on-the-server-running-microsoft-exchange-server-unified-messaging.md">在執行 Microsoft Exchange Server Unified Messaging 的伺服器上設定憑證</a></p></td>
</tr>
<tr class="odd">
<td><p>建立並設定新的 Exchange UM SIP 撥號對應表。</p></td>
<td><p>在 Exchange UM 伺服器上，根據組織的特定部署需求建立 SIP 撥號對應表。</p></td>
<td><p>Exchange 組織系統管理員</p></td>
<td><p>對於 Exchange 2007 (SP1) 或最新的 Service Pack，請參閱＜如何建立整合通訊 SIP URI 撥號對應表＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268632%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268632&amp;clcid=0x404</a>。</p>
<p>對於 Exchange 2010 或最新的 Service Pack，請參閱＜建立 UM 撥號對應表＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268674%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268674&amp;clcid=0x404</a>。</p>
<p>若為 Exchange 2013，請參閱＜整合通訊＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=266579&amp;clcid=0x404</a>。</p></td>
</tr>
<tr class="even">
<td><p>設定 Exchange UM SIP 撥號對應表的安全性設定。</p></td>
<td><p>若要為 Enterprise Voice 流量加密，請將 Exchange UM SIP 撥號對應表的安全性設定設為 [SIP 安全] 或 [安全] 。如果您已在環境中部署或預定要部署 Lync Phone Edition 裝置，此步驟就更為重要。若要讓 Lync Phone Edition 裝置在整合了 Exchange UM 的環境中順利運作， Lync Server 加密設定必須要與 Exchange UM 撥號對應表的安全性設定相互配合。如需詳細資訊，請參閱部署文件。</p></td>
<td><p>Exchange 組織系統管理員</p></td>
<td><p><a href="lync-server-2013-configure-unified-messaging-on-microsoft-exchange.md">針對 Lync Server 2013 在 Microsoft Exchange 上設定整合通訊</a></p>
<p>對於 Exchange 2007 (SP1) 或最新的 Service Pack，另請參閱：</p>
<p>＜在整合通訊撥號對應表上設定安全性設定＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268696%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268696&amp;clcid=0x404</a>。</p>
<p></p>
<p>對於 Exchange 2010 或最新的 Service Pack，另請參閱：</p>
<p>＜設定 UM 撥號對應表上的 VoIP 安全性＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268697%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268697&amp;clcid=0x404</a>。</p>
<p></p>
<p>若為 Exchange 2013，請參閱＜整合通訊＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=266579&amp;clcid=0x404</a>。</p></td>
</tr>
<tr class="odd">
<td><p>將 Unified Messaging 伺服器新增至 Exchange UM SIP 撥號對應表。</p></td>
<td><p>若要讓新安裝的 Unified Messaging 伺服器能夠接聽及處理來電，您必須將 Unified Messaging 伺服器新增至 UM 撥號對應表。在此案例中，請將伺服器新增至 Exchange UM SIP 撥號對應表。</p></td>
<td><p>系統管理員</p>
<p>Exchange Server 系統管理員</p></td>
<td><p>對於 Exchange 2007 SP1 或最新的 Service Pack，請參閱＜如何將 Unified Messaging Server 新增至撥號對應表＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268681%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268681&amp;clcid=0x404</a>。</p>
<p>對於 Exchange 2010 或最新的 Service Pack，請參閱＜檢視或設定 UM 伺服器的內容＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268682%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268682&amp;clcid=0x404</a>。</p>
<p></p>
<p>若為 Exchange 2013，請參閱＜整合通訊＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=266579&amp;clcid=0x404</a>。</p></td>
</tr>
<tr class="even">
<td><p>以 SIP 位址設定信箱。</p></td>
<td><p>將 SIP 位址指派給將會使用 Exchange UM 功能之 Enterprise Voice 使用者的信箱。</p></td>
<td><p>Lync Server 2013 系統管理員</p>
<p>Exchange 收件者系統管理員</p></td>
<td><p>對於 Exchange 2007 SP1 或最新的 Service Pack，請參閱＜如何新增、移除或修改已啟用 UM 功能的使用者之 SIP 位址＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268698%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268698&amp;clcid=0x404</a>。</p>
<p>對於 Exchange 2010 或最新的 Service Pack，請參閱＜修改已啟用 UM 之使用者的 SIP 位址＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268699%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268699&amp;clcid=0x404</a>。</p>
<p></p>
<p>若為 Exchange 2013，請參閱＜整合通訊＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=266579&amp;clcid=0x404</a>。</p></td>
</tr>
<tr class="odd">
<td><p>執行 exchucutil.ps1 指令碼。</p></td>
<td><p>在執行 Exchange UM 服務的伺服器上開啟 Exchange 管理命令介面，並執行 exchucutil.ps1 指令碼；此指令碼會執行下列作業：</p>
<ul>
<li><p>授與 Lync Server 2013 讀取 Exchange UM  Active Directory 網域服務 物件的權限，尤其是在之前的工作中所建立的 SIP 撥號對應表。</p></li>
<li><p>在 Active Directory 中，針對主控已啟用 Enterprise Voice 之使用者的每個 Lync Server 2013 Enterprise Edition 集區或 Standard Edition Server，建立 Unified Messaging IP 閘道物件。</p></li>
<li><p>為每個閘道建立 Exchange UM 群組搜尋。群組搜尋引導識別碼將會是與對應閘道關聯的撥號對應表名稱。如果有多個撥號對應表，則這些項目必須要一一對應。</p></li>
</ul></td>
<td><p>Exchange 組織系統管理員</p>
<p>Exchange 收件者系統管理員</p></td>
<td><p><a href="lync-server-2013-configure-unified-messaging-on-microsoft-exchange.md">針對 Lync Server 2013 在 Microsoft Exchange 上設定整合通訊</a></p></td>
</tr>
<tr class="even">
<td><p>設定 Lync Server 2013 撥號對應表。</p></td>
<td><p>如果要與 Exchange 2007 SP1 或最新的 Service Pack 或是 Exchange 2010 整合，請使用與 Exchange UM 撥號對應表完整網域名稱 (FQDN) 相符的名稱建立新的 企業語音撥號對應表。</p>
<div class="alert">
> [!NOTE]  
> 您必須針對每個 UM 撥號對應表執行此動作。


</div>
<p>如果要與 Exchange 2010 SP1 整合，請確定您已設定適當的全域/網站層級或集區層級的 企業語音撥號對應表。</p>
<div class="alert">
> [!NOTE]  
> 如果要與 Exchange 2010 SP1 整合，則 Lync Server 撥號對應表與 Exchange UM SIP 撥號對應表的名稱不需相符。


</div></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-configuring-dial-plans.md">在 Lync Server 2013 中設定撥號對應表</a></p></td>
</tr>
<tr class="odd">
<td><p>執行 Exchange UM 整合工具。</p></td>
<td><p>在 Lync Server 2013 上執行 <strong>ocsumutil.exe</strong>，這會：</p>
<ul>
<li><p>建立「訂戶存取」與「自動語音應答」連絡人物件。</p></li>
<li><p>驗證有 企業語音撥號對應表的名稱與 Exchange UM 撥號對應表 FQDN 相符。如果您執行 Exchange 2010 SP1 或更新版本，則撥號對應表的名稱不需相符，且您可以忽略工具針對這點所發出的相關警告。</p></li>
</ul>
<p>這項工具在運作時會掃描 Active Directory 中的 Exchange UM 設定，並且讓 Lync Server 2013 系統管理員能夠檢視、建立及編輯連絡人物件。</p></td>
<td><p>RTCUniversalServerAdmins <em>與</em> RTCUniversalUserAdmins</p>
<div class="alert">
> [!IMPORTANT]  
> 使用者必須同時屬於這兩個群組，ocsumutil.exe 才能順利執行。


</div>
<div class="alert">
> [!NOTE]  
> 若要建立連絡人物件，執行 ocsumutil.exe 的使用者對於新連絡人物件存放所在的 Active Directory 組織單位 (OU) 必須具備正確的權限。執行 <strong>Grant-CsOUPermission</strong> Cmdlet，即可授與此權限。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。


</div></td>
<td><p><a href="lync-server-2013-configure-lync-server-2013-to-work-with-unified-messaging-on-microsoft-exchange-server.md">設定 Lync Server 2013 以搭配 Microsoft Exchange Server 上的 Unified Messaging 使用</a></p></td>
</tr>
<tr class="even">
<td><p>如有必要，請執行其他 企業語音設定步驟。</p></td>
<td><p>如果您尚未設定伺服器或使用者的 企業語音設定，請執行下列一或多項作業：</p>
<ul>
<li><p>部署並設定</p>
<p>公用交換電話網路 (PSTN) 閘道及中繼伺服器</p></li>
<li><p>定義語音原則、PSTN 使用方式記錄與撥出電話路由。</p></li>
<li><p>啟用使用者的 Enterprise Voice。</p></li>
<li><p>(選用) 設定特定使用者的撥號對應表。</p></li>
</ul>
<p>視您所啟用的 企業語音功能之不同，您可能必須執行其他設定步驟。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>RTCUniversalUserAdmins</p></td>
<td><p>請參閱以下幾節中的主題：</p>
<ul>
<li><p><a href="lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md">在 Lync Server 2013 中設定語音原則、PSTN 使用方式記錄和語音路由</a></p></li>
<li><p><a href="lync-server-2013-deploying-enterprise-voice.md">在 Lync Server 2013 中部署企業語音</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>為 Enterprise Voice 使用者啟用 Exchange UM。</p></td>
<td><p>在 Exchange UM 伺服器上確定已建立 Unified Messaging 信箱原則，並且已為每位使用者指派唯一的分機號碼，然後為使用者啟用 Unified Messaging。</p></td>
<td><p>Exchange 收件者系統管理員</p></td>
<td><p>對於 Exchange 2007 SP1 或最新的 Service Pack，請參閱＜如何啟用使用者的整合通訊功能＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268700%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268700&amp;clcid=0x404</a>。</p>
<p>對於 Exchange 2010 或最新的 Service Pack，請參閱＜啟用使用者的整合通訊功能＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=268701%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=268701&amp;clcid=0x404</a>。</p>
<p></p>
<p>若為 Exchange 2013，請參閱＜整合通訊＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=266579%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=266579&amp;clcid=0x404</a>。</p></td>
</tr>
</tbody>
</table>

