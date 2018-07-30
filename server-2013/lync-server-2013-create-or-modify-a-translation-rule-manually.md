---
title: 手動建立或修改轉譯規則
TOCTitle: 手動建立或修改轉譯規則
ms:assetid: 049d1db3-af58-48c5-be89-52e1d068a4bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398099(v=OCS.15)
ms:contentKeyID: 49289947
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 手動建立或修改轉譯規則

 

_**上次修改主題的時間：** 2012-08-06_

若要撰寫相符樣式及轉譯規則的規則運算式以定義轉譯規則，請遵循下列步驟。或者，您可以在 \[建立轉譯規則\] 工具中輸入一組值，並啟用 Lync Server 控制台產生對應的相符樣式及轉譯規則。如需詳細資訊，請參閱＜[使用組建轉譯規則工具建立或修改轉譯規則](lync-server-2013-create-or-modify-a-translation-rule-by-using-the-build-a-translation-rule-tool.md)＞。

## 若要手動定義轉譯規則

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  若要開始定義轉譯規則，請遵循＜[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)＞中的步驟 1 至 10 或＜[在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)＞中的步驟 1 至 9。

4.  在 **\[新增轉譯規則\]** 或 **\[編輯轉譯規則\]** 頁面的 **\[名稱\]** 欄位中，輸入可描述所轉譯號碼模式的名稱。

5.  (選用) 在 \[描述\] 中，輸入轉譯規則的描述，例如**美國國際長途撥號**。

6.  按一下 **\[建置轉譯規則\]** 區段底部的 **\[編輯\]**。

7.  在 \[輸入規則運算式\] 中輸入下列內容：
    
      - 在 \[符合此模式\] 中，指定用來比對要轉譯之號碼的模式。
    
      - 在 \[轉譯規則\] 中，指定轉譯號碼的格式模式。
    
    例如，若您在 \[比對此模式\] 中輸入 **^\\+(\\d{9}\\d+)$** 以及在 \[轉譯規則\] 中輸入 **011$1**，此規則會將 +441235551010 轉譯為 011441235551010。

8.  按一下 **\[確定\]** 儲存轉譯規則。

9.  按一下 **\[確定\]** 儲存主幹組態。

10. 在 **\[主幹組態\]** 頁面上，按一下 **\[認可\]**，再按一下 **\[全部認可\]**。
    
    > [!NOTE]  
    > 當您建立或修改轉譯規則時，您都必須執行 [全部認可] 命令才能發行組態變更。如需詳細資訊，請參閱作業文件中的＜<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>＞。
    


## 請參閱

#### 工作

[使用組建轉譯規則工具建立或修改轉譯規則](lync-server-2013-create-or-modify-a-translation-rule-by-using-the-build-a-translation-rule-tool.md)  
[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 概念

[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)

