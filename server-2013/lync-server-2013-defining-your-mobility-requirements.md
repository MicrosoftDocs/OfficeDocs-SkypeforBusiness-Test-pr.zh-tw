---
title: Lync Server 2013：定義行動需求
TOCTitle: 定義行動需求
ms:assetid: b7608335-cdeb-4aae-8e4b-d80c55f0d62b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690039(v=OCS.15)
ms:contentKeyID: 49292092
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 定義 Lync Server 2013 的行動需求

 

_**上次修改主題的時間：** 2015-03-09_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

在 Lync Server 2013 行動功能的規劃階段期間，當您使用 Lync 2010 Mobile 和 Lync 2013 Mobile 用戶端時，必須制定一些決定部署步驟的決策。

以下是您必須考慮的決策：

  - **您是否要使用 Lync 行動用戶端自動探索？**
    
    如果您想支援自動探索，您必須建立新的內部和外部網域名稱系統 (DNS) 記錄，將主體替代名稱新增至 前端伺服器、 Director 及反向 Proxy 上的憑證，以及在反向 Proxy 上修改現有的發行規則。如需詳細資訊，請參閱＜ [Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)＞。透過自動探索，使用者可以從公司網路內部或外部任何位置自動尋找 Lync Server 2013 Web 服務，而不需要在其行動裝置設定中輸入 URL。
    
    如果您使用手動設定而不是自動探索，行動使用者必須在其行動裝置上手動輸入下列 URL：
    
      - https://\<外部集區 FQDN\>/Autodiscover/autodiscoverservice.svc/Root，以進行外部存取
    
      - https://\<內部集區 FQDN\>/AutoDiscover/autodiscoverservice.svc/Root，以進行內部存取
    
    強烈建議使用自動探索。手動設定的主要用途在於進行疑難排解。

  - **如果您決定支援自動探索，是否願意針對每個 SIP 網域以主體別名更新反向 Proxy 上的憑證？**
    
    如果具有許多 SIP 網域，更新反向 Proxy 上的公開憑證可能會變得很昂貴。如果發生此情況，您可以選擇實作自動探索，讓初始自動探索服務要求使用連接埠 80 上的 HTTP，而不是使用連接埠 443 上的 HTTPS。不過，這不是建議的方法。如果您決定選擇此替代方法，您不需要更新反向 Proxy 上的憑證，但是必須針對連接埠 80 上的 HTTP 建立 Web 發行規則。如需詳細資訊，請參閱＜ [Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)＞。

  - **您要同時支援公司網路內部和外部的 Lync 行動用戶端，或僅支援公司網路內部的用戶端？**
    
    如果您要支援網路內部和外部的行動用戶端，行動裝置可以從任何位置存取行動性功能。預設設定為同時支援公司網路內部和外部的用戶端。
    
    雖然預設設定允許行動用戶端流量通過外部網站，但是您可以將行動用戶端流量限定在內部公司網路。當您將流量限定在內部網路時，使用者只有在網路內部時，才可以在其行動裝置上使用 Lync 行動應用程式。
    
    針對支援使用 Mcx Mobility Service 和 Lync 2010 Mobile 之行動性的部署，執行 **Set-CsMcxConfiguration** Cmdlet。若要設定行動性僅供內部使用，可使用與下列類似的命令：
    
        Set-CsMcxConfiguration -Identity site:Redmond -ExposedWebURL Internal
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>UCWA 不需要其他設定。UCWA 沒有相當於僅限內部的設定。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您使用的是 Lync Server 2013前端伺服器或 前端集區，且您 <strong>沒有</strong>任何 Lync Server 2010前端伺服器或 前端集區， <strong>就沒有 Cookie 型持續性的需求</strong>。如果您需要保留任何 Lync Server 2010前端伺服器或 前端集區，則會為 Cookie 型持續性套用 Lync Server 2010 中的相同規則。</td>
    </tr>
    </tbody>
    </table>


  - **您是否要支援 Apple iOS 裝置和 Windows Phone 的推入通知功能？**
    
    如果您支援推入通知，支援的 Apple iOS 裝置和 Windows Phone 會收到行動應用程式非作用中時所發生的事件通知。您必須設定 Edge Server 與雲端架構的 Lync Server 推入通知服務 (位於 Lync Online 資料中心) 的同盟關係，並執行 Cmdlet 以啟用推入通知。
    
    如果您要在 Wi-Fi 網路上支援推入通知，除了在行動裝置提供者的 3G 或資料網路上支援推入通知之外，您還必須開啟企業 Wi-Fi 網路上的連接埠 5223 輸出。在 Wi-Fi 網路上支援推入通知，可支援僅使用 Wi-Fi 的行動裝置，以及室內接收情況不佳的行動裝置。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只有在支援執行 Lync 2010 Mobile 用戶端的 Apple 裝置時，才需要開啟連接埠 TCP 5223。</td>
    </tr>
    </tbody>
    </table>
    
    如果您不支援推入通知，Apple 行動裝置和 Windows Phone 的使用者將無法了解行動應用程式非作用中時所發生的事件資訊 - 例如立即訊息邀請或未接訊息。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Apple 裝置上的 Lync 2013 行動用戶端不需要推入通知。 Windows Phone 上的 Lync 2013 行動用戶端會使用推入通知。對於 Windows Phone 上的 Lync Mobile 以及無法執行 Lync 2013 行動用戶端的 Apple 裝置，推入通知的規劃和推入通知結算所會保持相同。</td>
    </tr>
    </tbody>
    </table>


  - **您想讓所有使用者都可以存取行動功能，或想指定存取這些功能的使用者？**
    
    此表格說明使用者在 Lync Server 2013 中可用的功能。預設值可以為「從公司撥號」、「Voice over IP」(VoIP)，並啟用「行動性」。此處是完整的可用選項組：
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>功能/參數名稱/範圍 (原則參數名稱不可相同)</th>
    <th>說明</th>
    <th>已導入</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>啟用行動性</p>
    <p>參數名稱： <code>EnableMobility</code></p>
    <p>範圍：全域/網站/使用者</p></td>
    <td><p>管理設定可控制已安裝 Lync Mobile 之指定範圍內的使用者。如果原則設為 False，則使用者無法登入用戶端。</p>
    <p>預設設定為 True。</p></td>
    <td><p>Lync Server 2010 累計更新 (2011 年 11 月)</p></td>
    </tr>
    <tr class="even">
    <td><p>啟用外部語音</p>
    <p>參數名稱：<code>EnableOutsideVoice</code></p>
    <p>範圍：全域/網站/使用者</p></td>
    <td><p>控制使用者使用「從公司撥號」 的能力，此功能可讓使用者利用其公司電話號碼而非行動電話號碼來撥打和接聽電話。如果設為 False，則使用者將無法從行動裝置利用其公司電話號碼來撥打和接聽電話。</p>
    <p>預設設定為 True</p></td>
    <td><p>Lync Server 2010 累計更新 (2011 年 11 月)</p></td>
    </tr>
    <tr class="odd">
    <td><p>啟用 IP 音訊和視訊</p>
    <p>參數名稱：<code>EnableIPAudioVideo</code></p>
    <p>範圍：全域/網站/使用者</p></td>
    <td><p>控制使用者是否可在其行動裝置上使用 VoIP 來撥打或接聽電話。如果設為 False，使用者將無法在其裝置上撥打或接聽 VoIP 或視訊通話。</p>
    <p>預設設定為 True。</p></td>
    <td><p>Microsoft Lync Server 2013</p></td>
    </tr>
    <tr class="even">
    <td><p>IP 音訊需要 WiFi</p>
    <p>參數名稱：<code>RequireWiFiForIPAudio</code></p>
    <p>範圍：全域/網站/使用者</p></td>
    <td><p>此設定定義用戶端是否需要在 WiFi 上而非在行動數據網路上透過 VoIP 撥打或接聽電話。如果設為 True，使用者即可僅在連線至 WiFi 網路時撥打和接聽 VoIP 電話。</p>
    <p>預設設定為 False。</p></td>
    <td><p>Microsoft Lync Server 2013</p></td>
    </tr>
    <tr class="odd">
    <td><p>IP 視訊需要 WiFi</p>
    <p>參數名稱：<code>RequireWiFiForIPVideo</code></p>
    <p>範圍：全域/網站/使用者</p></td>
    <td><p>此設定定義用戶端是否需要在 WiFi 上而非在行動數據網路上撥打或接聽視訊電話。如果設為 True，使用者即可僅在連線至 Wi-Fi 網路時撥打和接聽視訊電話。</p>
    <p>預設設定為 False。</p></td>
    <td><p>Microsoft Lync Server 2013</p></td>
    </tr>
    </tbody>
    </table>
    
    如需您可設定之原則設定的說明，以及如何管理原則的詳細資訊，請參閱＜ [New-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMobilityPolicy)＞、＜ [Set-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMobilityPolicy)＞、＜ [Get-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMobilityPolicy)＞、＜ [Grant-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsMobilityPolicy)＞和＜ [Remove-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsMobilityPolicy)＞。

  - **您是否要讓未啟用 Enterprise Voice 的使用者能夠使用 \[按一下加入\] 加入會議？**
    
    使用者必須啟用企業語音，才可以存取行動功能和「從公司撥號」 。不過，未啟用企業語音的使用者若獲派適當的語音原則，也可以在其行動裝置上按一下連結來加入會議。您可以將特定語音原則指派給這些使用者，或確定存在其所適用的全域原則或網站層級原則。您指派的語音原則必須具有公用交換電話網路 (PSTN) 使用方式記錄，以及定義使用者可撥出加入會議之區域的路由。如需設定語音原則、PSTN 使用方式記錄及路由的詳細資訊，請參閱＜ [在 Lync Server 2013 中設定語音原則、PSTN 使用方式記錄和語音路由](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)＞。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>想使用 [按一下加入] 的行動使用者需要語音原則，以及相關的 PSTN 使用方式記錄和語音路由，因為在行動裝置上按一下連結會導致從 Lync Server 2013 撥出電話。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 概念

[Lync Server 2013 行動技術需求](lync-server-2013-technical-requirements-for-mobility.md)  

#### 其他資源

[在 Lync Server 2013 中設定語音原則、PSTN 使用方式記錄和語音路由](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

