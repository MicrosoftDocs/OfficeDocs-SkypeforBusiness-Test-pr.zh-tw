---
title: 設定受支援的用戶端版本
TOCTitle: 設定受支援的用戶端版本
ms:assetid: aebf7b48-9aa2-4a06-adc5-0c9d11b6358d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412832(v=OCS.15)
ms:contentKeyID: 49291999
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定受支援的用戶端版本

 

_**上次修改主題的時間：** 2012-12-14_

在 Lync Server 2013 中，您可以設定用戶端版本原則，以指定您環境中支援的用戶端版本。此外，您可以使用全域用戶端版本設定，為還沒有定義版本原則 (且因此沒有明確受支援或限制) 的用戶端指定預設動作。

您也可以使用用戶端版本原則來管理用戶端更新。當您設定用戶端版本原則，並使用 \[允許並升級\] 和 \[封鎖並升級\] 選項時，用戶端會從 Windows Server Update Service (如果您使用此服務) 或 Microsoft Update 收到更新的軟體。

## 用戶端版本原則設定

預設用戶端版本原則要求所有用戶端執行 Lync 或 Microsoft Office Communicator 2007 R2。如果環境中的用戶端執行舊版 Communicator，則您可能需要重新設定用戶端版本規則，以防止用戶端和裝置被意外封鎖或在連接到 Lync Server 2013 時更新。您可以修改預設規則，也可以在用戶端版本原則清單中新增更高的規則以覆寫預設值。此外，發行累計更新 (CU) 時，應該設定用戶端版本原則以索取最新更新。

