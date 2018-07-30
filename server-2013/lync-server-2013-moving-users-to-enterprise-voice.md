---
title: Lync Server 2013：將使用者移至企業語音
TOCTitle: 將使用者移至企業語音
ms:assetid: a2df6d51-5cf2-4d3e-8f97-496af5fd5e5e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412758(v=OCS.15)
ms:contentKeyID: 49291860
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將使用者移至企業語音

 

_**上次修改主題的時間：** 2012-10-18_

如果您要將使用者從現有的 PBX 電話語音基礎結構移至 企業語音，部署程序中包含一些不屬於 [在 Lync Server 2013 中規劃企業語音](lync-server-2013-planning-for-enterprise-voice.md)中已描述之規劃程序的步驟。如需有關從先前的 企業語音部署移轉使用者的資訊，請參閱安裝媒體隨附的移轉文件。

將使用者從現有電話語音基礎結構移到 企業語音的程序包含下列步驟：

1.  指定主要電話號碼。

2.  啟用使用者的 企業語音。

3.  為使用者準備撥號對應表。

4.  規劃使用者語音原則。

5.  規劃電話路由。

6.  設定 PBX 或 SIP 主幹以重新路由已啟用 Enterprise Voice 之使用者的通話。

7.  將使用者移至 Exchange 整合通訊 (UM) (建議)。

本主題將說明以上各個步驟所需的規劃。

## 步驟 1. 指定主要電話號碼

企業語音會將語音與其他訊息媒體整合在一起，如此一來，當來電到達伺服器時，伺服器就會將號碼對應到使用者的 SIP-URI，然後將電話分送到與該 SIP-URI 關聯的所有用戶端端點。此程序需要每一個使用者都要與一個主要電話號碼關聯。

主要電話號碼必須：

  - 在全域中是唯一的，或是在企業中是唯一的 (如果是內部分機)。

  - 由企業所擁有，且在企業內可路由傳送。不應該使用個人號碼。

在 Active Directory 網域服務 中可針對企業使用者列出兩個或多個電話號碼。與特定使用者有關聯的所有電話號碼，都可以在 \[Active Directory 使用者和電腦\] 嵌入式管理單元中，於該使用者的內容表上進行檢視或變更。

在 **\[使用者內容\]** 對話方塊中， **\[一般\]** 索引標籤上的 **\[電話號碼\]** 方塊應該包含使用者的主要工作號碼。這個號碼通常會指定為使用者的主要電話號碼。

某些使用者可能會有特別的需求 (例如，某位主管希望所有來電都透過行政助理路由傳送)，但是應該限制只有在需求很明確且重要時才能使用特例。

在選擇主要號碼之後，該號碼必須：

  - 盡可能正規化為 E.164 格式。

  - 複製到 Active Directory 的 **msRTCSIP-line** 屬性。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>與遠端呼叫控制 (RCC) 並存</strong><br />
    RCC 是使用 Lync Server 監視和控制桌面 PBX 電話的能力。它會透過伺服器路由傳送控制，並將此伺服器當做通往 PBX 的閘道。雖然您無法為使用者同時設定 RCC 和 企業語音，但是在任一情況下，[線路 URI] 設定都會指定使用者的主要電話號碼。<br />
    如果您希望所選使用者繼續使用現有的 PBX 基礎結構，可以使用漸進方式將 企業語音引進組織內。如需此部署案例的詳細資訊，請參閱規劃文件中的 <a href="lync-server-2013-direct-sip-deployment-options.md">Lync Server 2013 中的 SIP 直接部署選項</a>。<br />
    您可以在舊版中為使用者同時啟用 RCC 和 企業語音，但前提是您也為使用者設定了雙重分支處理，這項功能會使來電同時在使用者的 PBX 電話和 Communicator 上響鈴。 Lync Server 2010 不支援雙重分支處理。</td>
    </tr>
    </tbody>
    </table>


有三種方法可填入 **msRTCSIP-line** 屬性：

  - Microsoft Identity Integration Server (建議)

  - Lync Server 控制台中的 **\[使用者\]** 頁面

當您必須處理多個電話號碼時，貴組織開發的自訂指令碼是更好的選擇。根據您的組織在 Active Directory 網域服務中表示電話號碼的方式而定，指令碼可能必須將主要電話號碼正規化成 E.164 格式，然後再將其複製到 **msRTCSIP-line** 屬性。

  - 如果您的組織在 Active Directory 網域服務中以單一格式維護所有的電話號碼，而且該格式為 E.164，則指令碼只需要將每一個主要電話號碼寫入 **msRTCSIP-line** 屬性。

  - 如果您的組織在 Active Directory 網域服務中以單一格式維護所有的電話號碼，但是該格式不是 E.164，則指令碼應該定義適當的正規化規則，以便將主要電話號碼從現有的格式轉換成 E.164，然後再將其寫入 **msRTCSIP-line** 屬性。

  - 如果您的組織未在 Active Directory 網域服務中強制電話號碼符合某標準格式，則指令碼應該定義適當的正規化規則，以便將主要電話號碼從各種格式轉換成 E.164 的格式，然後再將主要電話號碼寫入 **msRTCSIP-line** 屬性。

您的指令碼也必須在每一個主要電話號碼前面插入首碼 **Tel:**，然後再將其寫入 **msRTCSIP-line** 屬性。

這個屬性中指定之號碼的預期格式如下：

  - Tel:+14255550100;ext=50100。

  - Tel:5550100 (適用於整個企業中唯一的分機)
    
    > [!IMPORTANT]  
    > 通訊錄服務 (ABS) 所執行的正規化作業，不會取代或排除將 Active Directory 網域服務中每位使用者的主要電話號碼正規化的需求，因為 ABS 並沒有 Active Directory 網域服務的存取權，所以無法將主要電話號碼複製到 <strong>msRTCSIP-line</strong> 屬性。
    


## 步驟 2. 讓使用者啟用 Enterprise Voice

完成此步驟除了識別要啟用的使用者以外，不需要進行特殊規劃。

## 步驟 3. 為使用者準備撥號對應表。

已啟用 企業語音的使用者將無法撥打電話給未具備撥號對應表的 PSTN。撥號對應表是一個具名的正規化規則集，可將具名位置、個別使用者或連絡人物件的電話號碼轉譯成單一標準 (E.164) 格式，以便進行電話授權和電話路由傳送。正規化規則會針對每個指定位置、使用者或連絡人物件，定義要如何路由傳送以各種格式表達的電話號碼。

如需準備撥號對應表的相關資訊，請參閱＜ [Lync Server 2013 中的撥號對應表和正規化規則](lync-server-2013-dial-plans-and-normalization-rules.md)＞。

## 步驟 4. 規劃使用者語音原則

舊式 PBX 上的使用者服務類別設定，例如，從公司電話撥打長途電話或國際電話的權限，必須針對移到 Enterprise Voice 的使用者重新設定為 VoIP 原則。如需有關規劃及建立 Enterprise Voice 原則的詳細資訊，請參閱＜ [Lync Server 2013 中的語音原則](lync-server-2013-voice-policies.md)＞。

## 步驟 5. 規劃撥出電話路由

電話路由會指定 Lync Server 如何處理 Enterprise Voice 使用者所撥出的電話。當使用者撥號時，伺服器就會在必要時將撥號字串正規化成 E.164 格式，並嘗試將它與 SIP URI 比對。如果伺服器無法進行比對，就會根據號碼套用傳出電話的路由邏輯。定義該邏輯的最後一步是為每個撥號對應表中列出的每組目標電話號碼建立單獨指定的電話路由。

如需有關規劃通話路由的詳細資訊，請參閱＜ [Lync Server 2013 中的語音路由](lync-server-2013-voice-routes.md)＞。

## 步驟 6. 設定 PBX 或 SIP 主幹以重新路由 Enterprise Voice 使用者的電話

之前在傳統 PBX 上或連至網際網路電話語音服務提供者 (ITSP) 之 SIP 主幹連線上主控的使用者，在移動之後會保留其電話號碼。唯一的需求是在移動之後，必須重新設定 PBX 或 SIP 主幹，以便將撥打給 Enterprise Voice 使用者的來電路由傳送到 中繼伺服器。

## 步驟 7. 將使用者移至 Exchange 整合通訊 (建議)

將使用者移到 Exchange 整合通訊的程序包含下列工作：

  - 設定 Exchange 整合通訊與 Lync Server 以共同運作。

  - 啟用使用者的 Exchange Unified Messaging 來電接聽和 Outlook 語音存取。這項工作是在 Exchange Unified Messaging 伺服器上執行。如需詳細資訊，請參閱 Exchange Server 2010 TechNet Library，網址為 [http://go.microsoft.com/fwlink/?linkid=139372\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=139372%26clcid=0x404)。

