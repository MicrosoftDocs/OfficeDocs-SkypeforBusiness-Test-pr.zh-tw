---
title: Lync Server 2013：設定電話撥入式會議的撥號對應表
TOCTitle: 設定電話撥入式會議的撥號對應表
ms:assetid: a3e0958e-384f-43e5-b4c9-686b6ecac7ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412768(v=OCS.15)
ms:contentKeyID: 49291888
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定電話撥入式會議的撥號對應表

 

_**上次修改主題的時間：** 2013-02-25_

當您部署電話撥入式會議時，需要建立或修改一個或多個用於路由傳送撥入存取電話號碼的撥號對應表。請確認在每個撥號對應表中，至少有一個正規化規則會將電話分機號碼轉換成 E.164 格式的完整電話號碼。電話撥入式會議的使用者會藉由輸入其個人識別碼 (PIN) 和其電話號碼，以經過驗證的企業使用者身分加入會議。您需要使用正規化規則將分機號碼轉換成完整電話號碼，才能在使用者只輸入電話分機時驗證使用者。

若要設定電話撥入式會議的撥號對應表，請執行下列動作：

  - 無論您是否部署企業語音，請修改全域撥號對應表以新增電話撥入式會議地區，並確認正規化規則正確地轉換您的撥入存取號碼。如需詳細指示，請參閱[在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)。

  - 如果您沒有部署 企業語音，請為您的電話撥入式會議存取號碼建立撥號對應表。請務必包含電話撥入式會議地區。如需詳細指示，請參閱＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞。

  - 若您已部署 企業語音，請視需要修改 企業語音撥號對應表以加入地區，並將適當的正規化規則用於撥入存取號碼。如需詳細指示，請參閱＜ [在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)＞。您也可以建立只用於撥入存取號碼的專用撥號對應表。如需詳細指示，請參閱＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞。

如需有關規劃地區的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的電話撥入式會議需求](lync-server-2013-dial-in-conferencing-requirements.md)＞。

## 本章節內容

  - [檢視 Lync Server 2013 中的撥號對應表資訊](lync-server-2013-view-dial-plan-information.md)

  - [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)

  - [在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)

  - [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)

