---
title: 在 Lync Server 2013 中執行語音路由測試案例
TOCTitle: 在 Lync Server 2013 中執行語音路由測試案例
ms:assetid: fb4d32df-b9ea-4944-8cd7-a6102c78c465
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413068(v=OCS.15)
ms:contentKeyID: 49292893
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中執行語音路由測試案例

 

_**上次修改主題的時間：** 2013-02-24_

您可以執行語音路由測試案例套件中的所有測試案例，或是執行其中一個或多個選取的測試案例。

## 若要執行所有語音路由測試案例

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[語音路由\] 和 \[測試語音路由\]。

4.  在 \[測試語音路由\] 頁面上，按一下 \[動作\]，再按一下 \[全部執行\]。
    
    每一個測試案例的通過或失敗狀態都會在 \[通過/失敗\] 欄中顯示。如果測試案例尚未執行，則 \[通過/失敗\] 欄中會顯示 N/A。

5.  (選用) 若要查看每一個測試案例的詳細結果，請按兩下測試案例名稱。結果會在 \[編輯測試案例\] 頁面右側的灰色區域中顯示：
    
    1.  **測試結果：**執行之測試案例的整體通過或失敗狀態。
    
    2.  **正規化規則：**針對這個測試案例選取的撥號對應表中符合撥號號碼 (\[要測試的號碼\] 欄位中的值) 的第一個正規化規則。
    
    3.  **正規化的號碼：**正規化規則轉譯之後的撥號號碼值。
    
    4.  **第一個公用交換電話網路 (PSTN) 使用方式：**針對這個測試案例選取的語音原則中符合撥號號碼的第一個 PSTN 使用方式記錄。
    
    5.  **第一個路由：**第一個 PSTN 使用方式記錄中符合撥號號碼的第一個語音路由。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在語音路由測試案例設定中，[預期的 PSTN 使用方式記錄] 和 [預期的路由] 欄位是選填欄位。如果測試案例未指定這些值，測試結果中對應的欄位將會是空的。</td>
        </tr>
        </tbody>
        </table>


## 若要執行一個或多個選取的語音路由測試案例

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[語音路由\] 和 \[測試語音路由\]。

4.  在 \[測試語音路由\] 頁面上，按一下您要執行的測試案例名稱。

5.  在 \[執行\] 功能表上按一下 \[執行選取項目\]。
    
    每一個測試案例的通過或失敗狀態都會在 \[通過/失敗\] 欄中顯示。如果測試案例尚未執行，則 \[通過/失敗\] 欄中會顯示 N/A。

6.  (選用) 若要查看每一個測試案例的詳細結果，請按兩下測試案例名稱。結果會在 \[編輯測試案例\] 頁面右側的灰色區域中顯示：
    
    1.  **測試結果：**執行之測試案例的整體通過或失敗狀態。
    
    2.  **正規化規則：**針對這個測試案例選取的撥號對應表中符合撥號號碼 (\[要測試的號碼\] 欄位中的值) 的第一個正規化規則。
    
    3.  **正規化的號碼：**正規化規則轉譯之後的撥號號碼值。
    
    4.  **第一個 PSTN 使用方式：**針對這個測試案例選取的語音原則中符合撥號號碼的第一個 PSTN 使用方式記錄。
    
    5.  **第一個路由：**第一個 PSTN 使用方式記錄中符合撥號號碼的第一個語音路由。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在語音路由測試案例設定中，[預期的 PSTN 使用方式記錄] 和 [預期的路由] 欄位是選填欄位。如果測試案例未指定這些值，測試結果中對應的欄位將會是空的。</td>
        </tr>
        </tbody>
        </table>


## 請參閱

#### 其他資源

[在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)  
[在 Lync Server 2013 中執行語音路由測試](lync-server-2013-running-voice-routing-tests.md)

