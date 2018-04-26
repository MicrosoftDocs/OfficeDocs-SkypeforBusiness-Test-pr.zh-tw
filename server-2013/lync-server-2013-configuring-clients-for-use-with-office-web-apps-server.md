---
title: 設定用戶端與 Office Web Apps Server 搭配使用
TOCTitle: 設定用戶端與 Office Web Apps Server 搭配使用
ms:assetid: e5eaead7-0b32-42fb-97eb-ca203af59a9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205339(v=OCS.15)
ms:contentKeyID: 49292624
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定用戶端與 Office Web Apps Server 搭配使用

 

_**上次修改主題的時間：** 2013-02-25_

若您要使用者體驗 Office Web App Server 的完整功能，您必須將使用者升級到 Microsoft Lync 2013；只有 Lync 2013 使用者能夠單獨捲動整個 PowerPoint 投影片，而不影響真正的 PowerPoint 簡報。(也就是說，這些使用者可以在做簡報時隨時檢閱任何一張投影片，不會中斷真正的簡報。) 未使用 Lync 2013 的使用者仍能加入線上會議並檢視 PowerPoint 簡報；但是無法自由捲動整個投影片，也無法看到投影片切換或檢視內嵌影片。

請注意，這些功能一律開放給 Lync 2013 使用者使用；即使 PowerPoint 簡報者正在執行 Microsoft Lync 2010 也一樣。若執行 Lync 2010 的使用者在主持 PowerPoint 簡報，則 Lync Server 2013 將搭配 Office Web Apps Server，確認 Lync 2013 使用者可檢視該簡報的 Office Web Apps Server 版本。執行 Lync 2013 用戶端以外的使用者將無法使用 Office Web Apps Server 提供的 PowerPoint 服務。這些使用者只能連接到會議伺服器服務，並依 Microsoft Lync Server 2010 的檢視方式檢視 PowerPoint 簡報。也就是說，這些使用者將只能使用 Lync Server 2010 提供的受限功能。

雖然 Office Web Apps Server (不同於將使用者升級到 Lync 2013) 不需要設定用戶端，但是建議與會者升級到 Internet Explorer 9。雖然可透過 Internet Explorer 8 參加會議，但是使用該瀏覽器仍有些許限制。例如 Internet Explorer 8 的使用者將無法將 PowerPoint 階段調整到自訂尺寸；只能使用預設的三種階段尺寸。Internet Explorer 8 使用者也無法播放媒體檔案。

