---
title: Lync Server 2013：執行架構準備
TOCTitle: 執行架構準備
ms:assetid: 9d02bdb1-ff29-417a-bcce-b068b31207d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412729(v=OCS.15)
ms:contentKeyID: 49291809
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中執行 Active Directory 架構準備

 

_**上次修改主題的時間：** 2012-10-29_

您可以使用安裝程式或 Lync Server 管理命令介面 Cmdlet 來準備 Active Directory 架構。用來擴充 Active Directory 架構的 Cmdlet 是 **Install-CsAdServerSchema**。

> [!NOTE]  
> 此架構準備 Cmdlet ( <strong>Install-CsAdServerSchema</strong>) 必須存取架構主機，這將需要同時執行遠端登錄服務，並啟用遠端登錄機碼。如果無法在架構主機上啟用遠端登錄服務，您可以在架構主機上，以本機方式執行 Cmdlet。如需關於遠端存取登錄的詳細資訊，請參閱 Microsoft 知識庫文件 314837＜如何管理遠端登錄存取權＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=125769%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=125769&amp;clcid=0x404</a>。



在完成架構準備之後，請手動驗證架構分割已複寫，再繼續進行樹系準備。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中驗證 Active Directory 結構描述複寫](lync-server-2013-verifying-schema-replication.md)＞。

## 若要使用安裝程式準備目前樹系的架構

1.  以架構管理員群組成員的身分以及架構主機上系統管理員的權限，登入樹系中的伺服器。

2.  從 Lync Server 2013 安裝資料夾或媒體，執行 Setup.exe 以啟動部署精靈。

3.  如果系統提示您安裝 Microsoft Visual C++ 可轉散發套件，請按一下 \[是\] 。

4.  Lync Server 2013 安裝程式對話方塊會提示您指定安裝 Lync Server 檔案的位置。請選擇預設位置或 \[瀏覽\] 至您想要的位置，然後按一下 \[安裝\] 。

5.  在 \[授權合約\] 頁面上，勾選 \[我接受授權合約中的條款\] ，然後按一下 \[確定\] 。

6.  安裝程式隨即安裝 Lync Server 核心元件。

7.  當部署精靈準備就緒時，按一下 **\[準備 Active Directory\]** 並等候部署狀態判斷完成。

8.  在 **\[步驟 1：準備架構\]** 中按一下 **\[執行\]** 。

9.  按一下 **\[準備架構\]** 頁面中的 **\[下一步\]** 。

10. 在 **\[執行命令\]** 頁面上，尋找 **\[工作狀態：完成\]** ，然後按一下 **\[檢視記錄檔\]** 。

11. 展開 **\[動作\]** 欄下方的 **\[架構準備\]** ，並在每項工作結尾的執行結果中尋找 **\<成功\>** ，確認已順利完成架構準備，關閉記錄檔，然後按一下 **\[完成\]\>** 。

12. 等待 Active Directory 複寫完成或強制執行複寫。

13. 手動驗證架構變更是否已複寫到所有其他的網域控制站。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中驗證 Active Directory 結構描述複寫](lync-server-2013-verifying-schema-replication.md)＞。

## 使用 Cmdlet 準備目前樹系的架構

1.  以架構管理員群組成員的身分以及架構主機上系統管理員的權限，登入樹系中的電腦。

2.  如下所述安裝 Lync Server 核心元件：
    
    1.  從 Lync Server 2013 安裝資料夾或媒體，執行 Setup.exe 以啟動 Lync Server 部署精靈。
    
    2.  如果系統提示您安裝 Microsoft Visual C++ 可轉散發套件，請按一下 \[是\] 。
    
    3.  Lync Server 2013 安裝程式對話方塊會提示您指定安裝 Lync Server 檔案的位置。請選擇預設位置或 \[瀏覽\] 至您想要的位置，然後按一下 \[安裝\] 。
    
    4.  在 \[授權合約\] 頁面上，勾選 \[我接受授權合約中的條款\] ，然後按一下 \[確定\] 。安裝程式隨即安裝 Lync Server 2013 核心元件。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

4.  執行：
    
        Install-CsAdServerSchema [-Ldf <directory where the .ldf file is located>] 
    
    如果您沒有指定 Ldf 參數，則預設值是從登錄讀取的 Lync Server 2013 安裝路徑。
    
    例如：
    
        Install-CsAdServerSchema -Ldf "C:\Program Files\Microsoft Lync Server 2013\Deployment\Setup"

5.  使用下列 Cmdlet，確認已完成執行架構準備。
    
        Get-CsAdServerSchema 
    
    如果架構準備成功，則此 Cmdlet 會傳回 **SCHEMA\_VERSION\_STATE\_CURRENT** 的值。

6.  等待 Active Directory 複寫完成或強制執行複寫。

7.  手動驗證架構變更是否已複寫到所有其他的網域控制站。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中驗證 Active Directory 結構描述複寫](lync-server-2013-verifying-schema-replication.md)＞。

## 請參閱

#### 工作

[在 Lync Server 2013 中驗證 Active Directory 結構描述複寫](lync-server-2013-verifying-schema-replication.md)  

#### 概念

[在 Lync Server 2013 中準備 Active Directory 結構描述](lync-server-2013-preparing-the-active-directory-schema.md)

