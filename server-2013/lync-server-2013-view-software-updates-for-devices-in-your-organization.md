---
title: 在 Lync Server 2013 檢視裝置的軟體更新
TOCTitle: 在 Lync Server 2013 檢視裝置的軟體更新
ms:assetid: d2cca12b-ed43-4e1f-90ab-d14bca8b482c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182592(v=OCS.15)
ms:contentKeyID: 49292403
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 檢視裝置的軟體更新

 

_**上次修改主題的時間：** 2012-11-01_

在 Lync Server 2013 中，您可以使用裝置更新 Web 服務檢視及管理組織裝置的軟體更新。Microsoft 技術支援網站 ([http://go.microsoft.com/fwlink/?linkid=204091\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=204091%26clcid=0x404)) 會以 .cab (封包) 檔案的形式從提供這些更新。請在下載 .cab 檔案之後執行 **Import-CSdeviceUpdate** Cmdlet，以從 .cab 檔案匯入裝置更新規則。如需 **Import-CSdeviceUpdate** Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件中的＜[Import-CsDeviceUpdate](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsDeviceUpdate)＞。

> [!TIP]
> 在將新的更新部署至組織之前，請先在測試裝置上確認更新是否功能正常。


## 若要檢視 UC 裝置的軟體更新

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  從 Microsoft 支援網站 ([http://go.microsoft.com/fwlink/?linkid=204091\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=204091%26clcid=0x404)) 將 .cab 檔案下載到 Lync Server 2013 電腦上的某處 (例如 C:\\Updates\\UCUpdates.cab)。

3.  執行下列其中一個 Cmdlet，從 C:\\Updates\\UCUpdates.cab 檔匯入裝置更新規則：
    
      - 如果 .cab 檔位於執行要更新之服務的電腦上 (service:Redmond-websvc-2)，請執行下列 Cmdlet：
        
            Import-CsDeviceUpdate -Identity service:Redmond-websvc-2 -FileName C:\Updates\UCUpdates.cab
    
      - 如果 .cab 檔不是位於執行要更新之服務的電腦上 (service:Redmond-websvc-3)，請執行下列 Cmdlet：
        
            Import-CsDeviceUpdate -Identity service:Redmond-websvc-3 -ByteInput C:\Updates\UCUpdates.cab

4.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

5.  在左導覽列中，按一下 **\[用戶端\]**，然後按一下 **\[裝置更新\]**。

6.  在 **\[裝置更新\]** 頁面上，按一下清單中的某項更新，然後執行下列其中一項操作：
    
      - **取消擱置的更新。** 若要避免將選取的更新部署到您組織的裝置上，請按一下 **\[執行\]** 功能表，然後按一下 **\[取消擱置的更新\]**。
    
      - **核准更新。** 若要允許將選取的更新部署到您組織的裝置上，請按一下 **\[執行\]** 功能表，然後按一下 **\[核准\]**。
    
      - **還原更新。** 若要允許將之前核准的更新部署到您組織的裝置上，請按一下 **\[執行\]** 功能表，然後按一下 **\[還原\]**。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

