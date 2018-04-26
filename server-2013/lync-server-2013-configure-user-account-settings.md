---
title: Lync Server 2013：設定使用者帳戶設定
TOCTitle: 設定使用者帳戶設定
ms:assetid: b7c74ecc-b924-4efc-8a56-3a5f94a9ef13
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412896(v=OCS.15)
ms:contentKeyID: 49292096
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定使用者帳戶設定

 

_**上次修改主題的時間：** 2012-10-05_

撥入使用者會輸入其電話號碼或分機號碼和 PIN，以經驗證的使用者身分加入會議。需要使用在 Lync Server 使用者帳戶上指定的電話語音 **\[線路 URI\]** 來進行驗證。

本主題中的程序描述如何為單一使用者帳戶指派「線路 URI」 。如果您需要為多個使用者帳戶指派「線路 URI」 ，可以建立使用 **Set-CsUser** 指令程式的指令碼。如需使用範例指令碼將「線路 URI」 指派給多個使用者帳戶的詳細資訊，請參閱＜將線路 URI 指派給多個使用者＞，網址為 [http://go.microsoft.com/fwlink/?linkid=196945\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=196945%26clcid=0x404)。

## 若要設定使用者帳戶設定

1.  以 RTCUniversalServerAdmins 群組成員身分，或是 **Cs-UserAdministrator** 或 **CsAdministrator** 角色成員的身分登入電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，按一下 \[使用者\] 。

4.  在搜尋欄位中，輸入您要為電話撥入式會議設定的使用者名稱，或按一下 **\[新增篩選\]** 以指定搜尋欄位，然後按一下 **\[尋找\]** 。

5.  按兩下使用者名稱，開啟 \[編輯 Lync Server 使用者\] 對話方塊。

6.  在 **\[電話語音\]** 下的 **\[線路 URI\]** 欄位中，輸入唯一、正規化的電話號碼 (例如，tel:+14255550200)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只有在 [電話語音] 設為 [僅限電腦對電腦] 、[企業語音] 、[遠端呼叫控制] 或 [僅限遠端呼叫控制] 時，您才能指定 [線路 URI] 。</td>
    </tr>
    </tbody>
    </table>


7.  按一下 \[認可\] 。

