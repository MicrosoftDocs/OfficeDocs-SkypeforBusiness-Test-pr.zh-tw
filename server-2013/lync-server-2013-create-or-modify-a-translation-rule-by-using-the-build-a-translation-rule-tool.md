---
title: 使用組建轉譯規則工具建立或修改轉譯規則
TOCTitle: 使用組建轉譯規則工具建立或修改轉譯規則
ms:assetid: ba112df8-3bb4-48e4-a353-4bf9110ccd71
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412909(v=OCS.15)
ms:contentKeyID: 49292120
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用組建轉譯規則工具建立或修改轉譯規則

 

_**上次修改主題的時間：** 2012-10-05_

如果您要在 \[建置轉譯規則\] 工具中輸入一組值，並啟用 Lync Server 控制台為您產生對應的符合模式和轉譯規則，以便定義轉譯規則，請遵循步驟進行。或者，您可以手動撰寫規則運算式，以定義符合模式和轉譯規則。如需詳細資訊，請參閱＜[手動建立或修改轉譯規則](lync-server-2013-create-or-modify-a-translation-rule-manually.md)＞。

## 若要使用建置轉譯規則工具定義規則

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  若要開始定義轉譯規則，請遵循[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)中的步驟 1 至 10 或[在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)中的步驟 1 至 9。

4.  在 \[新增轉譯規則\] 或 \[編輯轉譯規則\] 頁面的 \[名稱\] 下方，輸入可描述所轉譯號碼模式的名稱。

5.  (選用) 在 \[描述\] 下方，輸入轉譯規則的描述，例如**美國國際長途撥號**。

6.  在對話方塊的 **\[建置轉譯規則\]** 區段，將值輸入下列欄位：
    
      - **開頭數字**：(選用) 指定要讓模式比對之號碼的前置數字。例如，在此欄位中輸入 **+** 以符合 E.164 格式的號碼 (開頭為 +)。
    
      - **長度**：指定比對模式中的位數，並且選擇要讓此模式精確比對此長度、至少為此長度或任何長度的號碼。例如，輸入 **11** 並在下拉式清單中選取 **\[至少\]**，以符合長度至少為 11 位數的號碼。
    
      - **要移除的數字**：(選用) 指定要移除的開頭位數。例如，輸入 **1** 以去掉號碼開頭的 **+**。
    
      - **要加入的數字**：(選用) 指定要加在轉譯之號碼之前的數字。例如，如果您希望在套用規則時將 011 加在轉譯的號碼前面，請輸入 **011**。
    
    您在這些欄位中輸入的值會反映在 **\[要比對的模式\]** 和 **\[轉譯規則\]** 欄位中。例如，若您指定上述範例的值，**\[要比對的模式\]** 欄位中的結果規則運算式為：
    
    **^\\+(\\d{9}\\d+)$**
    
    **\[轉譯規則\]** 欄位會指定轉譯號碼格式的模式。此模式有兩個部分：
    
      - 代表比對模式中位數的值 (例如，**$1**)
    
      - (選用) 您可以在 **\[要加入的數字\]** 欄位中輸入以加在前面的值
    
    使用上述範例的值時，**011$1** 會顯示在 **\[轉譯規則\]** 欄位中。
    
    套用此轉譯規則時，+441235551010 會成為 011441235551010。

7.  按一下 **\[確定\]** 儲存轉譯規則。

8.  按一下 **\[確定\]** 儲存主幹組態。

9.  在 **\[主幹組態\]** 頁面上，按一下 **\[認可\]**，再按一下 **\[全部認可\]**。
    
    > [!NOTE]  
    > 當您建立或修改轉譯規則時，您都必須執行 [全部認可] 命令才能發行組態變更。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。
    


## 請參閱

#### 工作

[手動建立或修改轉譯規則](lync-server-2013-create-or-modify-a-translation-rule-manually.md)  
[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 概念

[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)

