# 幻影多開 PhantomBox 更新來源

這個 repo 是「幻影多開 PhantomBox」Android App 的**線上更新來源**，請保持**公開**（App 不帶任何 token，直接讀公開網址）。

## 檔案
| 路徑 | 用途 |
|---|---|
| `update.json` | 最新版資訊：versionCode、versionName、minSdk、apkUrl、sha256、size、notes |
| `apk/PhantomBox-<版本>-arm64.apk` | arm64 APK（給一般 Android 手機／OPPO） |

## 更新怎麼運作
1. App 開啟時自動檢查（或按選單「檢查更新」），讀取
   `https://raw.githubusercontent.com/dk0327/phantombox-updates/main/update.json`。
2. `versionCode` 比手機上的大才提示，並顯示 `notes`。
3. 下載 `apkUrl`（只接受 GitHub 的 HTTPS 網址）到 App 快取。
4. 核對檔案大小＝`size`、**SHA-256＝`sha256`**，不符就刪檔、拒絕安裝。
5. 交給 Android PackageInstaller；系統會跳出確認，由你按「更新」。第一次需允許「安裝不明應用程式」。

> 注意：手機上要先**手動安裝一次有更新功能的版本（4.0.1 起）**，之後才能線上更新。
> 更新用的 APK 簽章金鑰必須與手機上已安裝版本相同，否則 Android 會拒絕更新。
> raw.githubusercontent.com 有約 5 分鐘快取，剛推送的新版可能要稍等才看得到。

## 發布新版流程
1. 在 Android Studio bump `build.gradle` 的 versionCode/versionName，重建（保留 v1+v2+v3 簽章設定）。
2. 把新 APK 放到 `apk/`，更新 `update.json`（versionCode、apkUrl、sha256、size、notes）。
3. **先 commit/push APK，再 push update.json**，避免舊版讀到指向尚未上傳檔案的清單。
