---
title: Lync Server 2013：準備 Active Directory 網域服務
TOCTitle: 準備 Active Directory 網域服務
ms:assetid: 7b0d9aa4-f1ab-4578-b22f-b802b6ed1530
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398607(v=OCS.15)
ms:contentKeyID: 49291423
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中準備 Active Directory 網域服務

 

_**上次修改主題的時間：** 2015-03-09_

在 Lync Server 2013 中，您可以使用 Lync Server 部署精靈來準備 Active Directory 網域服務，也可以直接使用 Lync Server 管理命令介面 Cmdlet。您也可以直接在網域控制站上使用 ldifde.exe 命令列工具，如本主題稍後所述。

Lync Server 部署精靈會引導您完成每項 Active Directory 準備工作。\[部署精靈\] 會執行 Lync Server 管理命令介面 Cmdlet。這項工具對於具有單一網域和單一樹系拓撲的環境，或是其他相似拓撲的環境，都很有用，

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以將 Lync Server 部署在網域控制站執行某些 32 位元版本作業系統的樹系或網域中 (如需詳細資訊，請參閱 <a href="lync-server-2013-active-directory-infrastructure-requirements.md">Lync Server 2013 的 Active Directory 基礎結構需求</a>)。不過，您無法在這些環境中以 Lync Server 部署精靈來執行架構、樹系與網域準備工作，因為 [部署精靈] 與支援檔案都只適用於 64 位元。但您可以在 32 位元的網域控制站上使用 ldifde.exe 與相關聯的 .ldf 檔案，進行架構、樹系與網域的準備工作。請參閱本主題稍後的＜使用 Cmdlet 和 Ldifde.exe＞一節。</td>
</tr>
</tbody>
</table>


您可以使用 Lync Server 管理命令介面 Cmdlet，從遠端或在較複雜的環境執行工作。

## 準備 Active Directory 的先決條件

您必須在執行 Windows Server 2012、 Windows Server 2012 R2 或 Windows Server 2008 R2 SP1 (64 位元) 的電腦上，執行 Active Directory 準備步驟。Active Directory 準備工作必須使用 Lync Server 管理命令介面和 OCSCore。

以下是執行 Active Directory 準備工作時所需的元件：

  - Lync Server 核心元件 (OCScore.msi)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您打算使用 Lync Server 管理命令介面進行 Active Directory 準備工作，則必須先執行 Lync Server 部署精靈以安裝核心元件。</td>
    </tr>
    </tbody>
    </table>


  - Microsoft .NET Framework 4.5
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若為 Windows Server 2012 和 Windows Server 2012 R2，您可以使用 Server Manager 安裝並啟動 .NET Framework 4.5。如需詳細資訊，請參閱 <a href="lync-server-2013-additional-software-requirements.md">Lync Server 2013 的其他軟體需求</a>中的＜Microsoft .NET Framework 4.5＞。若為 Windows Server 2008 R2，請從 Microsoft 網站下載及安裝 <a href="http://www.microsoft.com/en-us/download/details.aspx?id=30653">.Net Framework 4.5</a>。</td>
    </tr>
    </tbody>
    </table>


  - 遠端伺服器管理工具 (RSAT)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在網域控制站以外的成員伺服器上執行 Active Directory 準備步驟，則需要某些 RSAT 工具。若為 Windows PowerShell，請從 Server Manager 中的 [AD DS] 和 [AD LDS 工具] 節點安裝 AD DS 嵌入式管理單元與命令列工具及 Active Directory 模組。</td>
    </tr>
    </tbody>
    </table>


  - Microsoft Visual C++ 11 可轉散發套件
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果電腦尚未安裝此必要套件，安裝程式會提示您加以安裝。此套件會隨附給您，您不需另行取得。</td>
    </tr>
    </tbody>
    </table>


  - Windows PowerShell 3.0 (64 位元)
    
    若為 Windows Server 2012 和 Windows Server 2012 R2， Windows PowerShell 3.0 應隨附於 Lync Server 2013 安裝中。若為 Windows Server 2008 R2，您必須安裝或升級為 Windows PowerShell 3.0。如需詳細資料，請參閱 [針對 Lync Server 2013 安裝 Windows PowerShell 3.0](lync-server-2013-installing-windows-powershell-3-0.md)

## 系統管理員的權限與角色

下表說明每一項 Active Directory 準備工作所需的系統管理權限和角色。

### 準備 Active Directory 時所需的使用者權限

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>程序</th>
<th>權限或角色</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>架構準備</p></td>
<td><p>樹系根網域的 Schema Admins 群組成員，以及架構主機的系統管理員權限</p></td>
</tr>
<tr class="even">
<td><p>樹系準備</p></td>
<td><p>樹系的 Enterprise Admins 群組成員</p></td>
</tr>
<tr class="odd">
<td><p>網域準備</p></td>
<td><p>所指定網域的 Enterprise Admins 或 Domain Admins 群組成員</p></td>
</tr>
</tbody>
</table>


## 準備 Active Directory 時使用的 Cmdlet

下表比較用來準備 AD DS 的 Lync Server 管理命令介面 Cmdlet 和 Microsoft Office Communications Server 2007 R2 中用來準備 AD DS 的 LcsCmd 命令。

### 各 Cmdlet 與 LcsCmd 的比較

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>LcsCmd</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Install-CsAdServerSchema</p></td>
<td><p>Lcscmd /forest /action:SchemaPrep /SchemaType:Server</p></td>
</tr>
<tr class="even">
<td><p>Get-CsAdServerSchema</p></td>
<td><p>Lcscmd /forest /action:CheckSchemaPrepState</p></td>
</tr>
<tr class="odd">
<td><p>Enable-CsAdForest</p></td>
<td><p>Lcscmd /forest /action:ForestPrep</p></td>
</tr>
<tr class="even">
<td><p>Disable-CsAdForest</p></td>
<td><p>Lcscmd /forest /action:ForestUnprep</p></td>
</tr>
<tr class="odd">
<td><p>Get-CsAdForest</p></td>
<td><p>Lcscmd /forest /action:CheckForestPrepState</p></td>
</tr>
<tr class="even">
<td><p>Enable-CsAdDomain</p></td>
<td><p>Lcscmd /domain /action:DomainPrep</p></td>
</tr>
<tr class="odd">
<td><p>Disable-CsAdDomain</p></td>
<td><p>Lcscmd /domain /action:DomainUnprep</p></td>
</tr>
<tr class="even">
<td><p>Get-CsAdDomain</p></td>
<td><p>Lcscmd /domain /action:CheckDomainPrepState</p></td>
</tr>
</tbody>
</table>


## 鎖定 Active Directory 的需求

如果您的組織中已停用權限繼承，或必須停用已驗證的使用者權限，則您在進行網域準備時需要執行額外的步驟。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中準備鎖定的 Active Directory 網域服務](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md)＞。

## 自訂容器權限

如果您的組織使用的是自訂容器，而非三個內建的容器 (也就是使用者、電腦和網域控制站)，您就必須將自訂容器的讀取存取權授與 Authenticated Users 群組。 執行網域準備工作時，必須要有容器的讀取存取權。如需詳細資訊，請參閱＜ [針對 Lync Server 2013 準備網域](lync-server-2013-preparing-domains.md)＞。

## 使用 Cmdlet 和 Ldifde.exe

Lync Server 部署精靈和 **Install-CsAdServerSchema** Cmdlet 中的 **\[準備架構\]** 步驟，會在執行 64 位元作業系統的網域控制站上擴充 Active Directory 架構。如果您需要在執行 32 位元作業系統的網域控制站上擴充 Active Directory 架構，可以遠端從成員伺服器執行 **Install-CsAdServerSchema** Cmdlet (建議方法)。如果您需要直接在網域控制站上執行架構準備工作，可以使用 Ldifde.exe 工具匯入架構檔案。大多數的 Windows 作業系統版本皆會提供 Ldifde.exe 工具。

如果您使用 Ldifde.exe 匯入架構檔案，則無論您在從舊版進行移轉，還是執行全新安裝，都必須將四個檔案全部匯入。您必須依下列順序加以匯入：

1.  ExternalSchema.ldf

2.  ServerSchema.ldf

3.  BackCompatSchema.ldf

4.  VersionSchema.ldf

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這四個 .ldf 檔案皆位於安裝媒體或下載位置的 \Support\Schema 目錄中。</td>
</tr>
</tbody>
</table>


若要使用 Ldifde.exe 在作為架構主機的網域控制站上匯入這四個架構檔案，請使用下列格式：

    ldifde -i -v -k -s <DCName> -f <Schema filename> -c DC=X <defaultNamingContext> -j logFilePath -b <administrator account> <logon domain> <password>

例如：

    ldifde -i -v -k -s DC1 -f ServerSchema.ldf -c DC=X "DC=contoso,DC=com" -j C:\BatchImportLogFile -b Administrator contoso password

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有當您以不同的使用者身分登入時，才應使用 b 參數。如需必要使用者權限的詳細資訊，請參閱本主題稍早的＜系統管理員的權限與角色＞一節。</td>
</tr>
</tbody>
</table>


若要使用 Ldifde.exe 在不是架構主機的網域控制站上匯入這四個架構檔案，請使用下列格式：

    ldifde -i -v -k -s <SchemaMasterFQDN> -f <Schema filename> -c DC=X <rootDomainNamingContext> -j logFilePath -b <administrator account> <domain> <password>

如需關於使用 Ldifde 的詳細資訊，請參閱 Microsoft 知識庫文章 237677＜使用 LDIFDE 將目錄物件匯入和匯出 Active Directory＞，網址為 [http://go.microsoft.com/fwlink/?linkid=132204\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=132204%26clcid=0x404)。

## 本節內容

  - [在 Lync Server 2013 中準備 Active Directory 結構描述](lync-server-2013-preparing-the-active-directory-schema.md)

  - [為 Lync Server 2013 準備樹系](lync-server-2013-preparing-the-forest.md)

  - [針對 Lync Server 2013 準備網域](lync-server-2013-preparing-domains.md)

