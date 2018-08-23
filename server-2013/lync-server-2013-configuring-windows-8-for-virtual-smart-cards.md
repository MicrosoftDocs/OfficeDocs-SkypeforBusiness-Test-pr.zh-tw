---
title: 設定 Windows 8 以使用虛擬智慧卡
TOCTitle: 設定 Windows 8 以使用虛擬智慧卡
ms:assetid: 4916c167-4ee3-4f3e-b65c-33e588595112
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn308564(v=OCS.15)
ms:contentKeyID: 56269079
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Windows 8 以使用虛擬智慧卡

 

_**上次修改主題的時間：** 2013-07-03_

部署雙因素驗證和智慧卡技術時的其中一個考量因素，在於實作成本。Windows 8 提供一些新的安全性功能，其中一個最有趣的新功能是對虛擬智慧卡的支援。

有了配備符合規格版本 1.2 之信賴平台模組 (TPM) 晶片的電腦，組織現在可以享有智慧卡登入的好處，而無須進行額外的硬體投資。如需詳細資訊，請參閱＜將虛擬智慧卡配合 Windows 8 使用＞(英文)，網址為：[http://go.microsoft.com/fwlink/p/?LinkId=313365](http://go.microsoft.com/fwlink/p/?linkid=313365)。

## 設定 Windows 8 以使用虛擬智慧卡

1.  使用啟用 Lync 之使用者的認證登入 Windows 8 電腦。

2.  在 Windows 8 \[開始\] 畫面中，將游標移至螢幕右下角。

3.  選取 **\[搜尋\]** 選項，接著搜尋**命令提示字元**。

4.  在 **\[命令提示字元\]** 上按一下滑鼠右鍵，接著選取 **\[以系統管理員身分執行\]**。

5.  執行下列命令，開啟信賴平台模組 (TPM) 管理主控台：
    
        Tpm.msc

6.  從 TPM 管理主控台，確認您的 TPM 規格版本至少為 1.2。
    
    > [!NOTE]  
    > 如果出現對話方塊，指出找不到相容的信賴平台模組 (TPM)，請確認電腦是否具有相容的 TPM 模組，且模組已於系統 BIOS 中啟用。
    


7.  關閉 TPM 管理主控台

8.  從命令提示字元使用下列命令，建立新的虛擬智慧卡：
    
        TpmVscMgr create /name MyVSC /pin default /adminkey random /generate
    
    > [!NOTE]  
    > 若要在建立虛擬智慧卡時提供自訂的 PIN 值，請改為使用 /pin 提示。
    


9.  從命令提示字元使用下列命令，開啟電腦管理主控台：
    
        CompMgmt.msc

10. 在電腦管理主控台上，選取 **\[裝置管理\]**。

11. 展開 **\[智慧卡讀卡機\]**。

12. 確認已成功建立新的虛擬智慧卡讀卡機。

