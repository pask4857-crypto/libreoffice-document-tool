\# LibreOffice 客戶文件自動化工具



使用 LibreOffice Basic 與 UNO API 開發的文件自動化工具，透過 Calc 讀取客戶資料，並依照 Writer 文件範本自動產生客戶文件。



本專案展示試算表資料讀取、文件內容替換、表格建立、文件格式設定及檔案處理等功能。



\## 專案功能



\- 從 Calc 試算表讀取客戶資料。

\- 依照客戶編號搜尋指定客戶。

\- 使用 Writer 範本建立新的客戶文件。

\- 自動替換文件中的客戶資料標記。

\- 自動建立客戶資料表格。

\- 設定表格標題粗體、背景顏色及欄位寬度。

\- 檢查來源檔案及輸出檔案是否存在。

\- 避免覆蓋已存在的客戶文件。

\- 保留原始 Writer 範本，不直接修改來源文件。



\## 使用技術



\- LibreOffice Basic

\- LibreOffice UNO API

\- LibreOffice Writer

\- LibreOffice Calc



\## 專案結構



```text

libreoffice-document-tool/

│

├── customer\_template.odt

├── customers.ods

├── README.md

└── .gitignore

```



| 檔案 | 說明 |

|---|---|

| `customer\_template.odt` | Writer 文件範本，包含待替換的客戶資料標記及 Basic 巨集 |

| `customers.ods` | Calc 客戶資料來源 |

| `.gitignore` | 排除暫存檔案及產生的客戶文件 |



\## 環境需求



\- Windows

\- LibreOffice（包含 Writer、Calc）

\- 支援 LibreOffice Basic 與 UNO API 的環境



本專案使用 LibreOffice 的內建 Basic 與 UNO API，不需要另外安裝第三方程式庫。



\## 資料格式



`customers.ods` 的第一個工作表使用以下欄位：



| 欄位 | 說明 |

|---|---|

| CustomerId | 客戶編號 |

| CustomerName | 客戶姓名 |

| Email | 電子郵件 |

| Remarks | 客戶備註 |



範例資料：



| CustomerId | CustomerName | Email | Remarks |

|---|---|---|---|

| C001 | 王小明 | ming@example.com | 一般客戶 |

| C002 | 陳小華 | hua@example.com | 長期合作客戶 |

| C003 | 林小美 | mei@example.com | 新客戶 |

| C004 | 張小明 | ming4@example.com | 測試新增資料 |



第一列為欄位名稱，客戶資料從第二列開始。



\## 操作方式



1\. 將專案下載或複製到本機。

2\. 使用 LibreOffice Writer 開啟 `customer\_template.odt`。

3\. 確認 `customers.ods` 與 Writer 範本位於同一個資料夾。

4\. 允許文件執行巨集（依照 LibreOffice 的安全性設定操作）。

5\. 開啟 Writer Basic 巨集編輯器。

6\. 執行 `GenerateCustomerDocumentFromCalc()`。

7\. 在輸入視窗輸入客戶編號，例如 `C002`。

8\. 程式會讀取 Calc 資料，並產生對應的客戶文件。



產生的文件會儲存在專案資料夾中，檔名格式如下：



```text

Customer\_C002.odt

```



\## 文件範本



Writer 範本使用以下標記作為客戶資料的替換位置：



```text

{{CustomerId}}

{{CustomerName}}

{{Email}}

{{Remarks}}

```



執行巨集後，程式會將標記替換成從 Calc 讀取的實際資料，並在文件結尾建立客戶資料表格。



\## 錯誤處理



程式包含以下檢查：



\- 未輸入客戶編號時取消操作。

\- 找不到 `customers.ods` 時顯示錯誤訊息。

\- 找不到指定客戶編號時顯示搜尋結果。

\- 輸出文件已存在時停止產生，避免覆蓋既有文件。

\- 產生文件時保留原始 Writer 範本。



\## 技術實作重點



\### 1. 使用 UNO API 操作文件



透過 UNO API 建立文件搜尋物件、替換文字、建立表格及調整文件格式。



\### 2. 讀取 Calc 資料



使用 UNO API 開啟 Calc 文件，取得第一個工作表，再透過迴圈搜尋指定客戶編號。



\### 3. 文件範本處理



以原始 Writer 範本建立新的文件，完成資料替換及表格建立後，另存為獨立的客戶文件。



\### 4. 檔案路徑處理



根據目前 Writer 範本的位置取得專案資料夾，再組合 Calc 資料檔案及輸出文件的路徑，避免將完整路徑寫死在程式中。



\## 注意事項



\- Writer 範本與 Calc 資料檔案必須放在同一個資料夾。

\- 請勿任意變更 Calc 工作表的欄位順序，因為目前程式依照固定欄位位置讀取資料。

\- 如果輸出文件已存在，請先移除舊文件，再重新執行巨集。

\- 執行巨集前，請確認 LibreOffice 的巨集安全性設定允許執行該文件中的巨集。

\- 本專案使用 LibreOffice Basic 與 UNO API，不是 Microsoft Word VBA 或 Windows COM Automation 的實作。



\## 專案目的



本專案以小型實用工具的形式，練習辦公室文件自動化及跨應用程式資料處理，並展示透過程式讀取試算表資料、自動產生格式化文件的能力。

