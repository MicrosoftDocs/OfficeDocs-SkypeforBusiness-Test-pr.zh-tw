---
title: Lync Server 2013：資料收集
TOCTitle: 資料收集
ms:assetid: e40b03e5-455d-4bbc-831a-c61b1380db53
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399008(v=OCS.15)
ms:contentKeyID: 49292611
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的資料收集

 

_**上次修改主題的時間：** 2012-09-08_

在 Microsoft Lync Server 2013  通訊軟體中，您可以執行 Microsoft Lync Server 2013 規劃工具而不必記錄現有和建議的 IP 位址與 Edge Server 完整網域名稱 (FQDN)，但是這樣做很難不造成設定錯誤。例如，如果需要共存一段時間，常見的錯誤會是重複使用您 Lync Server 2013 Edge 部署之現有 Edge 部署中的 FQDN。藉由將現有和建議的 IP 位址與 FQDN 寫在試算表、表格或其他可見的表單中，有助於避免安裝期間的設定問題。

> [!WARNING]
> 若您使用舊版 規劃工具，您可能已使用工具建立拓撲，並匯出 拓撲產生器 要使用的拓撲文件，以發佈拓撲。 規劃工具 已移除匯出拓撲功能。不建議使用舊版 規劃工具 來建立 Lync Server 2013 的拓撲文件，以免發生意外結果。


因此，建議的方式是使用下列對應至您的 Edge 拓撲的資料收集範本，它會收集各種您需要輸入 規劃工具中的 FQDN 和 IP 位址。藉由記下目前和建議的設定，您就可以將值放入生產環境中適當的內容。此外，這樣也會強迫您思考設定共存和功能的方式，例如簡單的 URL、檔案共用和負載平衡。

要成功部署 Microsoft Lync Server 2013，您必須了解各元件之間的互動與依賴程度。從現有網路與伺服器基礎結構收集資料，並在這些工作階段中套用規劃指導方針，您可以將 Lync Server 2013  Edge Server 元件整合至您的基礎結構。

＜ [在 Lync Server 2013 中選擇拓撲](lync-server-2013-choosing-a-topology.md)＞介紹過有三種主要基礎結構及兩種變化，所以可能總共有五種部署案例。其中一種案例將會是收集資料的起點。IP 位址、伺服器名稱與網域名稱皆為範例，與符合的憑證、防火牆、DNS 圖表一致，針對完整的規劃解決方案提供必要的詳細資訊。 所需憑證、DNS 與防火牆值中的圖表與內容對跨團隊 (憑證授權單位、防火牆設定與 DNS 之管理是由規劃部署以外的團隊執行) 之通訊尤其重要。圖表提供所需元件的資訊，跨團隊合作時可用來溝通彼此需求。

這些圖表全球通用，但可用來收集相關資料，跨團隊合作時可用來溝通彼此需求 (網路、防水牆、憑證建立與管理、伺服器部署、伺服器管理是由不同群組處理)。進行 Lync Server 部署時，擁有設定網站、防火牆、連接埠與通訊協定、憑證與伺服器的所需詳細資料是非常寶貴的。

**Edge Server 與 Edge 集區**

![Edge Server 和 Edge 集區](images/Gg399008.7624717a-ce99-4ae8-a929-2c4d74a2e47d(OCS.15).jpg "Edge Server 和 Edge 集區")

**反向 Proxy**

![反向 Proxy](images/Gg399008.cf63fc50-2d11-4334-afc8-2d664ba1b6bb(OCS.15).jpg "反向 Proxy")

**Director 或 Director 集區**

![Director 和 Director 集區](images/Gg399008.56ba29ff-1309-4d5d-bf5c-35372169e947(OCS.15).jpg "Director 和 Director 集區")

