
# Japanese Speech Synthesis Guide

這個存儲庫旨在提供有關如何在 Firefox 和其他瀏覽器中使用日文語音合成的簡單指導，包括安裝所需的語音包和設定，以及範例代碼。

## 目錄
- [簡介](#簡介)
- [Firefox 中的日文語音安裝指南](#firefox-中的日文語音安裝指南)
- [Chrome 語音合成範例](#chrome-語音合成範例)
- [Firefox 可用語音檢查範例](#firefox-可用語音檢查範例)
- [操作系統指南](#操作系統指南)
  - [Windows](#windows-操作系統)
  - [macOS](#macos-操作系統)
  - [Linux](#linux-操作系統)
- [注意事項](#注意事項)

## 簡介
Firefox 本身並不內建語音合成系統，而是依賴操作系統提供的語音包來實現多語言的語音合成功能。因此，Firefox 無法自動提供日文語音，需要手動安裝。

## Firefox 中的日文語音安裝指南
要在 Firefox 中啟用日文語音合成，請確保你的操作系統已安裝相應的日文語音包。

### 操作系統指南

#### Windows 操作系統
1. 打開 **設定** > **時間與語言** > **語言與地區**。
2. 點擊 **添加語言**，選擇 **日文**，然後安裝。
3. 在安裝日文後，點擊 **日文** 語言，選擇 **語言選項**，確認安裝了「語音」部分。

#### macOS 操作系統
1. 打開 **系統設定** > **輔助功能** > **語音**。
2. 點擊 **系統語音** 下拉菜單，然後選擇 **管理語音**。
3. 在列表中選擇 **日文** 語音，並下載。

#### Linux 操作系統
- 大多數 Linux 發行版依賴開源的語音合成引擎如 `espeak` 或 `festival`。
- 在基於 Debian 的系統（如 Ubuntu）上，你可以執行以下命令來安裝語音引擎：
  ```bash
  sudo apt-get install espeak
  ```

## Chrome 語音合成範例
以下是使用 Web Speech API 在 Chrome 中實現日文語音合成的範例代碼：

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Japanese Speech Synthesis Example</title>
</head>
<body>
    <h1>日文語音合成範例</h1>
    <button id="speakButton">朗讀</button>

    <script>
        document.getElementById('speakButton').onclick = function() {
            const utterance = new SpeechSynthesisUtterance('こんにちは、これは日本語の音声合成の例です。');
            utterance.lang = 'ja-JP';
            window.speechSynthesis.speak(utterance);
        };
    </script>
</body>
</html>
```

## Firefox 可用語音檢查範例
以下代碼可以用於檢查 Firefox 中可用的語音，並確認是否有日文語音可用：

```javascript
function checkVoices() {
    const voices = window.speechSynthesis.getVoices();
    if (voices.length === 0) {
        console.log("尚未加載任何語音。");
        return;
    }
    
    voices.forEach(voice => {
        console.log(`${voice.name} (${voice.lang})`);
    });

    const japaneseVoice = voices.find(voice => voice.lang === 'ja-JP');
    if (!japaneseVoice) {
        alert('無法找到日文語音，請確認系統已安裝日文語音包。');
    } else {
        alert('找到日文語音：' + japaneseVoice.name);
    }
}

// 手動觸發檢查語音列表
window.speechSynthesis.onvoiceschanged = checkVoices;
checkVoices();
```

## 注意事項
- 確保操作系統中已正確安裝日文語音包。
- 如果你需要更即時的解決方案，可以考慮使用 Chrome，因為它已經內建支持日文語音。

## 貢獻
歡迎對本指南進行貢獻！如果你有更好的方法或建議，請提出 Pull Request 或開啟 Issue。

## 授權
本專案採用 [MIT License](LICENSE)。
