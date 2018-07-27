---
title: 在 Lync Server 2013 中啟用通話許可控制
TOCTitle: 在 Lync Server 2013 中啟用通話許可控制
ms:assetid: 80201105-18f7-4c02-9c71-8df5a952f6c7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398642(v=OCS.15)
ms:contentKeyID: 49291469
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用通話許可控制

 

_**上次修改主題的時間：** 2012-10-19_

在設定通話許可控制部署的網路設定後，必須啟用 CAC，您的頻寬原則才能生效。

如需詳細資訊，請參閱 Lync Server 管理命令介面文件中關於下列 Cmdlet 的部分：

  - [Get-CsNetworkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkConfiguration)

  - [Set-CsNetworkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkConfiguration)

  - [Remove-CsNetworkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkConfiguration)

## 若要使用管理命令介面啟用通話許可控制

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsNetworkConfiguration Cmdlet 以在您的網路中啟用 CAC。例如，執行：
    
        Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck 1
    
    如果您要在網路中停用 CAC，請執行下列命令：
    
        Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck 0

## 若要使用 Lync Server 控制台啟用通話許可控制

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]**。

3.  按一下 **\[通用\]** 導覽按鈕。

4.  按一下清單中的 **\[通用\]**，然後選取 **\[編輯\]** 功能表上的 **\[顯示詳細資料\]**。

5.  在 **\[編輯通用設定\]** 頁面上，選取 **\[啟用通話許可控制台\]** 核取方塊。
    
    > [!NOTE]  
    > 如果您要在整個部署中停用通話許可控制，請清除此核取方塊。
    


6.  按一下 \[認可\]。

