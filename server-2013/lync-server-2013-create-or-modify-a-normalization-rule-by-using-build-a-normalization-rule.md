---
title: Lync Server 2013：使用 建立或修改正規化規則
TOCTitle: 使用 建立或修改正規化規則
ms:assetid: e8547d7b-f74d-4a73-9a7d-df20d7a87fcd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399036(v=OCS.15)
ms:contentKeyID: 49292665
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用 [建置正規化規則] 建立或修改正規化規則
 

_**上次修改主題的時間：** 2012-11-01_

如果您要在 Lync Server 控制台中建立或修改正規化規則，請完成下列步驟。或者，如果您要手動建立或修改正規化規則，請參閱＜ [在 Lync Server 2013 中手動建立或修改正規化規則](lync-server-2013-create-or-modify-a-normalization-rule-manually.md)＞。

## 若要使用建置正規化規則定義規則

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  (選用) 依照＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞中的步驟進行至步驟 11，或＜ [在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)＞中的步驟進行至步驟 10。

4.  在 **\[新增正規化規則\]** 或 **\[編輯正規化規則\]** 的 **\[名稱\]** 中，輸入描述要正規化之號碼模式的名稱 (例如 **5DigitExtension** )。

5.  (選用) 在 **\[描述\]** 中，輸入正規化規則的描述 (例如「轉譯 5 位數分機」)。

6.  在 **\[建置正規化規則\]** 的下列欄位中輸入值：
    
      - **開頭數字** ：(選用) 指定要讓模式比對之撥號號碼的前置數字。例如，如果您要讓模式比對開頭為 425 的撥號號碼，則輸入 **425** 。
    
      - **長度** ：指定比對模式中的位數，並且選擇要讓此模式精確比對此長度，或是比對至少為此長度的撥號號碼，或是比對任意長度的撥號號碼。
    
      - **要移除的數字** ：(選用) 指定要讓模式比對的撥號號碼中，要移除的開頭數字數目。
    
      - **要加入的數字** ：(選用) 指定要加入讓模式比對之撥號號碼的數字。
    
    您在這些欄位中輸入的值會反映在 **\[要比對的模式\]** 和 **\[轉譯規則\]** 中。例如，如果您讓 **\[開頭數字\]** 空白，在 **\[長度\]** 欄位中輸入 **7** 並且選取 **\[完全相符\]** ，以及在 **\[要移除的數字\]** 中指定 **0** ，則 **\[要比對的模式\]** 中產生的規則運算式如下：
    
    **^(\\d{7})$**

7.  在 **\[轉譯規則\]** 中，依照下述指定轉譯的 E.164 電話號碼格式的模式：
    
      - 代表比對模式中所指定位數的值。例如，如果比對模式為 **^(\\d{7})$** ，則轉譯規則中的 **$1** 代表 7 位數的撥號號碼。
    
      - (選用) 在 \[要加入的數字\] 欄位中輸入值，指定要加在轉譯號碼前面的數字 (例如 **+1425** )。
    
    例如，如果 **\[要比對的模式\]** 包含 **^(\\d{7})$** 做為撥號號碼的模式，而且 **\[轉譯規則\]** 包含 **+1425$1** 做為 E.164 電話號碼的模式，則規則會將 5550100 正規化為 +14255550100。

8.  (選用) 如果正規化規則會產生您組織內部的電話號碼，請選取 \[內部分機\] 。

9.  (選用) 輸入一個號碼來測試正規化規則，然後按一下 \[執行\] 。測試結果將顯示在 \[輸入測試號碼\] 下。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以儲存尚未通過測試的正規化規則，並於之後將它重新設定。如需詳細資訊，請參閱＜ <a href="lync-server-2013-test-voice-routing.md">在 Lync Server 2013 中測試語音路由</a>＞。</td>
    </tr>
    </tbody>
    </table>


10. 按一下 \[確定\] 儲存正規化規則。

11. 按一下 \[確定\] 儲存撥號對應表。

12. 在 \[撥號對應表\] 頁面上，依序按一下 \[認可\] 和 \[全部認可\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只要您建立或變更正規化規則，就必須執行 [全部認可] 命令發佈組態變更。如需詳細資訊，請參閱操作文件中的 <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[在 Lync Server 2013 中手動建立或修改正規化規則](lync-server-2013-create-or-modify-a-normalization-rule-manually.md)  
[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)  
[在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 其他資源

[在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)

