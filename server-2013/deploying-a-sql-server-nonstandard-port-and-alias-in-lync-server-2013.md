---
title: 在 Lync Server 2013  中部署 SQL Server 非標準連接埠和別名
TOCTitle: 在 Lync Server 2013  中部署 SQL Server 非標準連接埠和別名
ms:assetid: 2da92c1f-250e-407a-8651-fb2aec76aeb0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn776290(v=OCS.15)
ms:contentKeyID: 62634522
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署 SQL Server 非標準連接埠和別名

 

_**上次修改主題的時間：** 2015-01-06_

Microsoft Lync Server 2013 支援在 SQL Server 中使用非標準連接埠和別名。使用 SQL Server 非標準連接埠和別名可提高安全性，並為 Lync 部署建立更有彈性的環境。這些步驟只是適當保護您的 Lync Server 2013 環境的單一步驟。請務必採取額外的步驟，減少 Lync Server 2013 實作可能遭受攻擊的範圍。

下列文章說明在 Lync Server 2013 中設定 SQL Server 非標準連接埠和別名的必要步驟。

## 在 Lync Server 2013 中部署 SQL Server 非標準連接埠和別名

Lync Server 2013拓撲產生器 支援在設定 Lync Server 2013 時，使用 SQL Server 別名做為完整網域名稱 (FQDN)，取代實際的 SQL Server FQDN。這可讓實際的 SQL Server FQDN 隱藏起來，避免惡意攻擊者查看。此外，使用非標準連接埠可遮住實際的連接埠，避免潛在攻擊者嘗試攻擊標準連接埠 1433 上的資料庫，如下圖所示。

![駭客不知道攻擊的連接埠號碼。](images/Dn776290.2f3923e0-2bdc-416b-a66b-bf56599eb14e(OCS.15).jpg "駭客不知道攻擊的連接埠號碼。")

為了成功判斷 Lync Server 2013 用來與 SQL Server 進行通訊的連接埠，攻擊者必須掃描所有連接埠，才能取得連接埠資訊。攻擊者掃描連接埠的動作提高了安全性保護的偵測機率，進而停止掃描指示。此外，為提高非標準連接埠的安全性，您也可以使用 SQL Server 別名以提供彈性的部署。在必須變更 SQL Server 名稱的情況下，此功能對減少組態變更尤為重要。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SQL Server 提供二種容錯方法 (容錯叢集和鏡像)。這兩種 SQL Server 容錯方法都支援搭配 Lync Server 2013 使用 SQL Server 非標準連接埠和別名。</td>
</tr>
</tbody>
</table>


從 拓撲產生器 當中設定 SQL Server 資料庫連接或使用 Install-CsDatabase Cmdlet 時，您無法明確定義 SQL Server 非標準連接埠號碼，並將其與 SQL 執行個體建立關聯。要設定非標準連接埠，您需要使用 SQL Server 和 Windows Server 公用程式。

要設定 SQL Server 非標準連接埠和別名，以搭配 Lync Server 2013 使用，您必須完成三個主要步驟。這些步驟如下：

  - 確認 Lync Server 2013 已套用最新的更新。

  - 設定 SQL Server 非標準連接埠和別名。

  - 以 SQL Server 別名設定 Lync Server 2013 (使用 拓撲產生器)。

  - 發行拓撲並確認資料庫。

## 確認 Lync Server 2013 已套用最新的更新

讓 Lync Server 2013 保持在最新狀態是很重要的。要檢查最新的更新和如何進行套用的資訊，請參閱 [Lync Server 2013 的更新](http://support.microsoft.com/kb/2809243)。

## 設定 SQL Server 非標準連接埠和別名

SQL Server 非標準連接埠和別名必須先在資料庫上完成設定，才能從 Lync Server 2013拓撲產生器 參考。要設定 SQL Server 非標準連接埠和別名，您必須完成三個主要步驟。這些步驟如下：

  - 變更預設 TCP/IP 通訊協定值。

  - 建立及設定 SQL Server 別名。

  - 建立網域名稱系統 (DNS) 正式名稱 (CNAME) 資源記錄。

**修改預設 TCP/IP 通訊協定值**

1.  選取 **\[開始\]**，然後選擇 **\[SQL Server 組態管理員\]**，如下圖所示。
    
    ![SQL Server Management Studio 圖示](images/Dn776290.6e811f27-cea9-4437-b44c-55bff013150f(OCS.15).png "SQL Server Management Studio 圖示")

2.  在功能窗格中，選擇並展開 **\[SQL Server 執行個體\]**，選擇並展開 **\[SQL Server 網路組態\]**，然後選擇 **\[\<執行個體名稱\> 的通訊協定\]**，如下圖所示。
    
    ![瀏覽至 TCP/IP 內容](images/Dn776290.3d7a964c-f17e-47fd-8f0c-535453da7fad(OCS.15).jpg "瀏覽至 TCP/IP 內容")

3.  在右窗格中，用滑鼠右鍵按一下 **\[TCP/IP\]**，然後選擇 **\[內容\]**。「TCP/IP 內容」對話方塊就會顯示。

4.  選取 **\[IP 位址\]** 索引標籤。\[IP 位址\] 索引標籤會顯示伺服器上所有使用中的 IP 位址，其格式為 IP1、IP2 到 IPAll，如下圖所示。
    
    ![開啟 TCP/IP 內容。](images/Dn776290.ed2fd70d-1836-4ebf-80fe-09191d96585e(OCS.15).jpg "開啟 TCP/IP 內容。")

5.  清除所有 IP 位址的 **\[TCP 動態連接埠\]** 欄位。如果欄位中含有一個零字元，這表示 SQL Server 正在聆聽動態連接埠。請確定這些欄位已清除，且當中不含零。

6.  對於 Lync Server 將會用來連接至資料庫的 IP 位址，請確定 **\[已啟用\]** 已設為 **\[是\]**，如下圖所示。
    
    ![請將正確 IP 的啟用設為 \[是\]。](images/Dn776290.7f818b91-0793-4594-8932-90447270fad9(OCS.15).jpg "請將正確 IP 的啟用設為 [是]。")

7.  在對話方塊底端的 **\[IPAll\]** 區段，在 **\[TCP 連接埠\]** 欄位中輸入所要的連接埠，如下圖所示。在這個範例中，我們使用連接埠 50062，但是您可以使用介於 49152 與 65535 之間的任何連接埠。這些是指定為動態及私人使用的連接埠，並可確保您不會與用在 Lync Server 2013 部署中的其他連接埠發生衝突。
    
    ![設定 IPAll 區段的連接埠。](images/Dn776290.b5af53e2-7961-4664-b586-3ca8f3a17f06(OCS.15).jpg "設定 IPAll 區段的連接埠。")

8.  選擇 **\[確定\]**，結束「TCP/IP 內容」對話方塊。

9.  在 SQL Server 組態管理員左窗格中選取 **\[SQL Server 服務\]**，以重新啟動 SQL Server 執行個體。接著，以滑鼠右鍵按一下右窗格中的 **\[SQL Server \<執行個體名稱\>\]**，然後選取 **\[重新啟動\]**，如下圖所示。
    
    ![針對執行個體重設 SQL Server 服務。](images/Dn776290.a965c8cf-f769-4b52-bb38-c48a438cf491(OCS.15).jpg "針對執行個體重設 SQL Server 服務。")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>確定您更新了防火牆設定，以配合新的 SQL Server 連接埠。</td>
</tr>
</tbody>
</table>


**建立及設定 SQL Server 別名**

1.  選取 **\[開始\]**，然後選擇 **\[SQL Server 組態管理員\]**，如下圖所示。
    
    ![SQL Server Management Studio 圖示](images/Dn776290.6e811f27-cea9-4437-b44c-55bff013150f(OCS.15).png "SQL Server Management Studio 圖示")

2.  在左窗格中，選擇並展開 **\[SQL Server 執行個體\]**，選擇並展開 **\[SQL Native Client \<版本\> 設定\]**，然後選擇 **\[別名\]**，如下圖所示。
    
    ![SQL Server 組態管理員中的別名。](images/Dn776290.95341826-55d7-425f-ae19-d47d6668c5d8(OCS.15).jpg "SQL Server 組態管理員中的別名。")

3.  以滑鼠右鍵按一下 **\[別名\]**，然後選取 **\[新增別名…\]**。

4.  輸入 **\[別名名稱\]**、**\[連接埠號碼\]**、**\[通訊協定\]** 和 **\[伺服器\]**，如下圖所示。
    
    ![建立新別名](images/Dn776290.03653588-aecf-4fdd-b58a-95f5b372d478(OCS.15).jpg "建立新別名")
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>確定輸入您在上一個步驟使用的同一個非標準連接埠，因為這是 SQL Server 將會聆聽的連接埠。如果設定的別名連接到錯誤的 SQL Server FQDN 或執行個體，請停用後重新啟用相關的網路通訊協定。如此可以清除任何快取連接資訊，允許用戶端正常連接。</td>
    </tr>
    </tbody>
    </table>


**建立 DNS CNAME 資源記錄**

1.  登入管理 DNS 的電腦。

2.  選取 **\[開始\]**，然後選擇 **\[伺服器管理員\]**，如下圖所示。
    
    ![開啟伺服器管理員](images/Dn776290.3e4bd8ad-2a65-4a05-af40-c8dd3583bc8f(OCS.15).jpg "開啟伺服器管理員")

3.  選擇 **\[工具\]** 下拉式清單，然後選取 **\[DNS\]**，如下圖所示。
    
    ![從伺服器管理員開啟 DNS。](images/Dn776290.415e1da1-7c9a-4a4e-a896-ca34a76aaeff(OCS.15).jpg "從伺服器管理員開啟 DNS。")

4.  在左窗格中，展開伺服器名稱節點，展開 \[正向對應區域\] 節點，然後選擇相關的網域。

5.  以滑鼠右鍵按一下網域，然後選取 **\[新增別名 (CNAME)…\]**，如下圖所示。
    
    ![選取選項來建立新別名 CNAME](images/Dn776290.abe66cca-b53c-427a-9094-1a59dc6840ca(OCS.15).jpg "選取選項來建立新別名 CNAME")

6.  輸入 **\[別名名稱\]** 和 **\[SQL Server 的 FQDN\]**，如下圖所示。
    
    ![填寫新別名 CNAME 對話方塊。](images/Dn776290.dd0ebd2d-3407-4459-8bd9-2b389a7bc440(OCS.15).jpg "填寫新別名 CNAME 對話方塊。")

7.  選擇 **\[確定\]** 以儲存 CNAME，然後在 DNS 管理員中檢視。

## 驗證資料庫連線

有許多不同的方式能夠確認其運作正確無誤。建議您確認 SQL Server 伺服器正在聆聽使用別名的指定連接埠。如果要進行快速檢查，請使用 **netstat** 和 **telnet** 命令。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Telnet 用戶端功能隨附於 Windows Server 中，但必須先進行安裝。如果要安裝 Windows Server 功能，請開啟「伺服器管理員」，然後從 [管理] 功能表中選取 [新增角色及功能]。</td>
</tr>
</tbody>
</table>


**使用 netstat 和 telnet 驗證資料庫連線**

1.  選取 **\[開始\]**，然後輸入 **cmd** 以開啟命令提示。

2.  輸入 **netstat -a -f**，然後確認 SQL Server 執行的是正確的連接埠，如下圖所示。
    
    ![使用 netstat 驗證連接埠。](images/Dn776290.4ff3a1b2-c5eb-4496-8be7-374c351fa027(OCS.15).jpg "使用 netstat 驗證連接埠。")

3.  輸入 **telnet \<別名名稱\> \<連接埠 \#\>**，以確認 SQL Server 執行個體的連線。如果連線成功，telnet 即可連接，您就不會看到錯誤。這顯示 SQL Server 執行個體正在聆聽使用正確別名的正確連接埠。如果連接到 SQL 伺服器時發生問題，telnet 會顯示錯誤，表示無法連線。在資料庫伺服器上檢查資料庫連線後，您可以 (透過網路) 從 Lync Server 執行相同的操作，並確定過程中沒有任何防火牆封鎖存取。

## 總結

SQL Server 別名設定完成後，您可以用它來建立 Lync Server 2013 拓撲 (在 拓撲產生器 工具中)。如需拓撲的詳細資訊，請參閱 [在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)。

## 請參閱

#### 概念

[Microsoft Lync Server 2013](microsoft-lync-server-2013.md)  

#### 其他資源

[Lync Server 2013 中的安全性規劃](lync-server-2013-planning-for-security.md)  
[在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)  
[部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)

