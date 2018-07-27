---
title: Lync Server 2013：手動建立或修改正規化規則
TOCTitle: 手動建立或修改正規化規則
ms:assetid: fc0335e6-8830-4cfb-8c64-6aeb98c0a992
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413074(v=OCS.15)
ms:contentKeyID: 49292915
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中手動建立或修改正規化規則

 

_**上次修改主題的時間：** 2012-09-22_

若要手動建立或修改正規化規則，請完成下列步驟。若要在 Lync Server 控制台 中使用 \[建置正規化規則\] 建立或修改正規化規則，請參閱[在 Lync Server 2013 中使用 \[建置正規化規則\] 建立或修改正規化規則](lync-server-2013-create-or-modify-a-normalization-rule-by-using-build-a-normalization-rule.md)。

## 若要手動定義正規化規則

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  (選用) 依照＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞或＜ [在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)＞中的步驟進行。

4.  在 \[新增正規化規則\] 或 \[編輯正規化規則\] 的 \[名稱\] 中，輸入描述要正規化之號碼模式的名稱 (例如將正規化規則命名為 **5DigitExtension** )。

5.  (選用) 在 \[描述\] 欄位中，輸入正規化規則的描述 (例如「轉譯 5 位數分機」)。

6.  在 \[建置正規化規則\] 中，按一下 \[編輯\] 。

7.  在 \[輸入規則運算式\] 中輸入下列內容：
    
      - 在 \[比對此模式\] 中，指定要用來比對撥號電話號碼的模式。
    
      - 在 \[轉譯規則\] 中，指定轉譯的 E.164 電話號碼格式的模式。
    
    例如，如果您在 \[比對此模式\] 輸入 **^(\\d{7})$** 以及在 \[轉譯規則\] 中輸入 **+1425$1** ，此規則會將 5550100 正規化為 +14255550100。

8.  (選用) 如果正規化規則會產生您組織內部的電話號碼，請選取 \[內部分機\] 。

9.  (選用) 輸入一個號碼來測試正規化規則，然後按一下 \[執行\] 。測試結果將顯示在 \[輸入測試號碼\] 下。
    
    > [!NOTE]  
    > 您可以儲存尚未通過測試的正規化規則，並於之後將它重新設定。如需詳細資訊，請參閱＜ <a href="lync-server-2013-test-voice-routing.md">在 Lync Server 2013 中測試語音路由</a>＞。
    


10. 按一下 \[確定\] 儲存正規化規則。

11. 按一下 \[確定\] 儲存撥號對應表。

12. 在 \[撥號對應表\] 頁面上，依序按一下 \[認可\] 和 \[全部認可\] 。
    
    > [!NOTE]  
    > 只要您建立或變更正規化規則，就必須執行 [全部認可] 命令發佈組態變更。如需詳細資訊，請參閱操作文件中的 <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。
    


## 請參閱

#### 工作

[在 Lync Server 2013 中使用 \[建置正規化規則\] 建立或修改正規化規則](lync-server-2013-create-or-modify-a-normalization-rule-by-using-build-a-normalization-rule.md)  
[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)  
[在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 其他資源

[在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)

