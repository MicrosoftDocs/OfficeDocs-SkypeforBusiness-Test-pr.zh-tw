---
title: Lync Server 2013：安裝規劃工具
TOCTitle: 安裝規劃工具
ms:assetid: ebdc9e26-4b22-4b02-85b9-7462bcfe7c93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615046(v=OCS.15)
ms:contentKeyID: 52056250
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中安裝規劃工具

 

_**上次修改主題的時間：** 2013-11-07_

在您開始使用 Microsoft Lync Server 2013 規劃工具設計及規劃 Lync Server 2013 基礎結構之前，必須先安裝 規劃工具。部署 規劃工具的工作站或伺服器，不需要是您計劃安裝 Lync Server 2013 之網域或基礎結構的一部分。 規劃工具隨附的讀我檔案詳細說明安裝及使用該工具的重要資訊。讀我檔案中的某些資訊會在此重複以清楚說明。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安裝 規劃工具的使用者必須對要安裝工具的電腦擁有系統管理員權限和授權。</td>
</tr>
</tbody>
</table>


支援安裝及操作 規劃工具的作業系統為：

  - Windows 8

  - Windows 8.1

  - Windows Server 2012

  - Windows Server 2012 R2

  - Windows 7 32 位元版本

  - Windows 7 64 位元版本，使用 Windows on Win32 (WOW)

  - Windows Server 2008 R2，使用 WOW

此外， 規劃工具需要 Microsoft .NET Framework 4.5。

在符合安裝前需求之後，您可以接著安裝 規劃工具。

## 若要安裝規劃工具

1.  以 Administrators 群組成員的身分登入本機電腦。

2.  使用 \[Windows 檔案總管\] 或命令視窗，找出您下載 規劃工具安裝檔案的目錄。

3.  找出 LyncPlanningTool.msi。在 \[Windows 檔案總管\] 中，按兩下該檔案。在命令視窗中，輸入檔案名稱，然後按 **Enter** 以執行該檔案。

4.  在 \[Microsoft Lync Server 2013 規劃工具安裝精靈\] 的「歡迎」頁面上，按 \[下一步\] 。

5.  檢閱 **\[使用者授權合約\]** ，並選取 **\[我接受授權合約中的條款\]** 以接受授權合約中的使用規定，然後按 **\[下一步\]** 。

6.  選擇要安裝規劃工具檔案的位置。預設位置為 C:\\Program Files (x86)\\Microsoft Lync Server 2013\\Planning Tool。如果您要變更安裝位置，請按一下 \[變更\] 。在 \[變更目的地資料夾\] 上，瀏覽或輸入檔案的安裝位置，並按一下 \[確定\] ，然後按 **\[下一步\]** 。

7.  安裝程式現在已準備好安裝 規劃工具。按一下 **\[安裝\]** 開始安裝程序。

8.  安裝將會開始並顯示進度。成功完成安裝後，按一下 **\[完成\]** 。

9.  規劃工具已準備好供使用。

## 請參閱

#### 概念

[在 Lync Server 2013 中安裝選用軟體](lync-server-2013-installing-optional-software.md)

