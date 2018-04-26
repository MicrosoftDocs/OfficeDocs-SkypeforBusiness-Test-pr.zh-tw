---
title: Lync Server 2013：定義 Enterprise Voice 的需求
TOCTitle: 定義組織的 Enterprise Voice 需求
ms:assetid: 3310f78e-c658-4557-95fa-159ce3c22953
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425826(v=OCS.15)
ms:contentKeyID: 49290528
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義 Enterprise Voice 的需求

 

_**上次修改主題的時間：** 2012-08-07_

本主題將概要說明您對於拓撲中的地區、網站、與網站間的連結所應考量的事項，並說明這些事項在您部署 企業語音時有何重要性。如需制訂這些決策的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的進階企業語音功能的網路設定](lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md)＞。

## 網站和地區

首先，請在您的拓撲中識別要部署 企業語音的網站，以及這些網站所屬的網路地區。明確而言，請考量您要如何為各個網站提供公用交換電話網路 (PSTN) 連線。就管理性與物流的考量而言，這些網站的所屬地區可能會是決定性因素。決定要將閘道部署於該地區的何處、要將 Survivable Branch Appliance (SBA) 部署於何處，以及您可於何處設定網際網路電話語音服務提供者 (ITSP) 的 SIP 主幹 (在該地區或在中央網站)。

## 網站間的網路連結

您也必須考量 中央網站及其 分支網站之間的網路連結預定會使用多少頻寬。如果您的網站間有可恢復的 WAN 連結，或您打算部署這類連結，建議您在每個 分支網站上部署一個閘道，為這些網站上的使用者提供地區的直接向內撥號 (DID) 終端。如果您有彈性的 WAN 連結，但 WAN 連結的頻寬可能受限，請為該連結設定通話許可控制。如果您沒有彈性的 WAN 連結、在 分支網站上裝載少於 1000 名使用者，且您當地沒有經過訓練的 Lync Server 系統管理員，建議您在 分支網站上部署 Survivable Branch Appliance。如果您在 分支網站上裝載 1000 到 5000 名使用者、缺少彈性的 WAN 連線、經訓練的 Lync Server 系統管理員，建議您在 分支網站上部署 Survivable Branch 伺服器和小型閘道。如果您有支援媒體旁路的閘道對等，也請考慮對受限的連結啟用媒體旁路。

## 請參閱

#### 概念

[Lync Server 2013 中的進階企業語音功能的網路設定](lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md)

