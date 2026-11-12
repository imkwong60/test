我的影視資料庫 PWA

檔案：
- index.html：搜尋、篩選、收藏、觀看狀態、本機儲存及 JSON／CSV 匯入匯出
- manifest.webmanifest：PWA 安裝設定，使用資料夾內的 PNG 圖示
- sw.js：快取介面、圖示及 dramalist.csv，供離線使用
- icon-192.png、icon-512.png：本機 App 圖示
- dramalist.csv：隨附影視清單；首次開啟時會嘗試從同資料夾載入

開始使用：
1. 將整個資料夾部署至支援 HTTPS 的靜態網站主機，或在本機啟動靜態伺服器。所有介面、圖示、字型及資料檔皆由本機資料夾提供，不使用外部 CDN。
2. 打開網頁；首次成功載入後，Service Worker 會快取資料以支援離線使用。若以 file:// 開啟而無法自動載入 CSV，請從「資料管理」選擇「從裝置匯入 CSV」。
3. 篩選設定可個別收藏；收合時會保留關鍵字搜尋欄和已收藏設定。
4. 定期匯出完整 JSON 備份。匯入 JSON 會還原作品、收藏及觀看狀態。

Supabase email 備份：
- 只需設定一次 Supabase Project URL 與 anon/public key，並輸入 email 備份或還原；相同 email 會對應同一筆備份。
- 使用既有 public.notepad_data 資料表（id、data、updated_at），需設定允許 anon key 存取的 RLS policy。
- email 僅作為備份識別碼，不是登入或身分驗證。請勿在共用資料庫中把 email 當作保護資料的密碼；勿輸入 service_role/secret key。
- 雲端備份需要連線 Supabase；其餘本機搜尋、資料管理和已快取資料可離線使用。
- 既有 id=dramalist 或 id=Yan 的備份不會自動對應 email；請先從舊版匯出 JSON，再匯入或以 email 建立新備份。
