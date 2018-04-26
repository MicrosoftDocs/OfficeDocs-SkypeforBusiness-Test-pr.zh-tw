---
title: Lync Server 2013：執行樹系準備
TOCTitle: 執行樹系準備
ms:assetid: 9d62f7be-bcfe-421d-8d8a-225567102a35
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412732(v=OCS.15)
ms:contentKeyID: 49291812
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 執行樹系準備

 

_**上次修改主題的時間：** 2012-10-29_

您可以使用安裝程式或 Lync Server 管理命令介面 Cmdlet 來準備樹系。用來準備樹系的 Cmdlet 是 **Enable-CsAdForest**。

準備樹系之後，您必須先確認已複寫全域設定，再執行網域準備工作。

## 若要使用安裝程式來準備樹系

1.  以樹系根網域之 Enterprise Admins 群組成員身分登入已加入網域的電腦。

2.  從 Lync Server 2013 安裝資料夾或媒體，執行 Setup.exe 以啟動部署精靈。

3.  按一下 **\[準備 Active Directory\]** ，然後等候決定部署狀態。

4.  在 **\[步驟 3：準備目前的樹系\]** ，按一下 **\[執行\]** 。

5.  在 **\[準備樹系\]** 頁面上，按 **\[下一步\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>樹系準備可讓您選擇要放置 Lync Server 2013 之萬用群組的位置。請選擇和組織需求一致的位置。</td>
    </tr>
    </tbody>
    </table>


6.  在 **\[執行命令\]** 頁面上，尋找 **\[工作狀態：完成\]** ，然後按一下 **\[檢視記錄檔\]** 。

7.  展開 **\[動作\]** 欄下方的 **\[樹系準備\]** ，並在每項工作的結尾尋找 **\<成功\>** 執行結果，確認已順利完成樹系準備，關閉記錄檔，然後按一下 **\[完成\]\>** 。

8.  等候 Active Directory 複寫完成，或是強制複寫到樹系根網域控制站 \[Active Directory 網站及服務\] 嵌入式管理單元中列出的所有網域控制站，然後再執行網域準備作業。在所有 Active Directory 網站的網域控制站之間進行強制複寫，使網站內的複寫能在數分鐘內發生。

## 若要使用 Cmdlet 準備樹系

1.  登入已加入樹系根網域中 Domain Admins 群組成員網域的電腦。

2.  如下所述安裝 Lync Server 核心元件：
    
    1.  從 Lync Server 2013 安裝資料夾或媒體，執行 Setup.exe 以啟動 Lync Server 部署精靈。
    
    2.  如果系統提示您安裝 Microsoft Visual C++ 可轉散發套件，請按一下 \[是\] 。
    
    3.  Lync Server 2013 安裝程式對話方塊會提示您指定安裝 Lync Server 檔案的位置。請選擇預設位置或 \[瀏覽\] 至您想要的位置，然後按一下 \[安裝\] 。
    
    4.  在 \[授權合約\] 頁面上，勾選 \[我接受授權合約中的條款\] ，然後按一下 \[確定\] 。安裝程式隨即安裝 Lync Server 2013 核心元件。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

4.  執行：
    
        Enable-CsAdForest [-GroupDomain <FQDN of the domain in which to create the universal groups>]
    
    例如：
    
        Enable-CsAdForest -GroupDomain domain1.contoso.com 
    
    如果您未指定 GroupDomain 參數，則預設值會是本機網域。如果之前已在不是預設網域的網域中建立萬用群組，則必須明確指定 GroupDomain 參數。

5.  等候 Active Directory 複寫完成，或是強制複寫到樹系根網域控制站 \[Active Directory 網站及服務\] 嵌入式管理單元中列出的所有網域控制站，然後再執行網域準備作業。

6.  確認樹系準備是否成功。執行：
    
        Get-CsAdForest 
    
    如果樹系準備成功，此 Cmdlet 會傳回 **LC\_FORESTSETTINGS\_STATE\_READY** 這個值。

## 請參閱

#### 工作

[使用 Cmdlet 進行 Lync Server 2013 的反向樹系準備](lync-server-2013-using-cmdlets-to-reverse-forest-preparation.md)  

#### 其他資源

[為 Lync Server 2013 準備樹系](lync-server-2013-preparing-the-forest.md)

