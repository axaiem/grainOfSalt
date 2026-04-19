# 🧂 grainOfSalt

> **Take every headline with a grain of salt.** An AI-powered Chrome extension that analyzes web pages for bias, credibility, manipulation, and political leaning using the Gemini API.

---

## Features

- 🔍 **Correctness Analysis** — Flags potentially unverifiable or misleading claims
- ⚖️ **Bias Detection** — Identifies loaded language and one-sided framing
- 🗳️ **Political Leaning** — Left → Centre → Right spectrum with confidence score
- 🎣 **Clickbait Score** — Compares headline intent vs. actual content
- 🧠 **Manipulation Tactics** — Detects fear-mongering, emotional appeals, strawmanning, etc.
- 🏅 **Overall Credibility Score** — A single trust verdict with supporting rationale
- ⚙️ **User-provided API Key** — Bring your own Gemini API key; nothing is stored server-side
- 🔄 **Model Switching** — Switch between supported Gemini models from Settings (useful when free-tier limits are hit)
- 💾 **Result Caching** — Cached per URL to avoid redundant API calls

---

## How It Works

grainOfSalt is a **zero-backend** Chrome extension. All analysis is done by calling the Gemini REST API directly from the extension using your own API key. No data is sent to any third-party server — only to `generativelanguage.googleapis.com`.

```
You click the icon → Extension extracts the page text →
Gemini API analyzes it → Results shown as a visual report
```

---

## Installation

### From Source (Developer Mode)

1. Clone this repository:
   ```bash
   git clone https://github.com/axaiem/grainOfSalt.git
   cd grainOfSalt
   ```

2. Open Chrome and navigate to `chrome://extensions`

3. Enable **Developer Mode** (toggle in the top-right corner)

4. Click **Load unpacked** and select the `grainOfSalt` folder

5. The 🧂 icon will appear in your Chrome toolbar

---

## Configuration

### Setting Up Your API Key

1. Get a free Gemini API key at [aistudio.google.com](https://aistudio.google.com/app/apikey)
2. Click the 🧂 icon in Chrome → click **Settings** (or right-click the icon → Options)
3. Paste your API key and click **Save**
4. Your key is validated immediately and stored securely in `chrome.storage.sync`

### Selecting a Model

In Settings, you can choose from the supported Gemini models. If you hit the free-tier limit on one model, simply switch to another.

> **Tip:** If you see a "Rate limit reached" message, head to Settings → Model Selection and pick an alternative model.

---

## Usage

1. Navigate to any news article or web page
2. Click the 🧂 **grainOfSalt** icon in your toolbar
3. Click **Analyze This Page**
4. Wait a few seconds while Gemini processes the content
5. Review the results across all dimensions

---

## Project Structure

```
grainOfSalt/
├── manifest.json                    # Chrome Extension Manifest v3
├── src/
│   ├── background/
│   │   └── service-worker.js        # API message broker (service worker)
│   ├── content/
│   │   └── content.js               # Page content extractor
│   ├── popup/
│   │   ├── popup.html               # Main popup UI
│   │   ├── popup.js                 # Popup logic & rendering
│   │   └── popup.css                # Popup styles
│   ├── settings/
│   │   ├── settings.html            # Options/settings page
│   │   ├── settings.js              # Settings logic
│   │   └── settings.css             # Settings styles
│   └── lib/
│       ├── gemini-client.js         # Gemini REST API wrapper
│       ├── content-extractor.js     # Article text extraction
│       ├── analyzer.js              # Prompt engineering & response parsing
│       ├── storage.js               # chrome.storage abstraction
│       ├── constants.js             # Supported models, config, labels
│       └── utils.js                 # Shared utilities
├── assets/
│   └── icons/                       # Extension icons (16, 48, 128px)
├── docs/
│   └── ARCHITECTURE.md              # Detailed architecture notes
└── README.md
```

---

## Supported Models

Models are configured in `src/lib/constants.js`. The extension ships with these defaults:

| Model | Tier | Notes |
|---|---|---|
| `gemini-2.5-flash` | Free | Default — fast and capable |
| *(more to be added)* | — | Expand as needed in `constants.js` |

To add a new model, edit `SUPPORTED_MODELS` in `src/lib/constants.js`:

```js
export const SUPPORTED_MODELS = [
  { id: "gemini-2.5-flash", label: "Gemini 2.5 Flash", tier: "free" },
  { id: "your-model-id",    label: "Your Model Label", tier: "free" },
];
```

---

## Privacy & Security

- ✅ Your API key is stored **only** in `chrome.storage.sync` — encrypted by Chrome
- ✅ Page content is sent **only** to `generativelanguage.googleapis.com`
- ✅ No analytics, no tracking, no third-party servers
- ✅ The extension works entirely offline except for the Gemini API call itself

---

## Disclaimer

grainOfSalt uses AI to assist in evaluating content — it is **not** a replacement for critical thinking. AI models can be wrong. Always verify important claims from multiple primary sources.

---

## Contributing

Pull requests welcome! Please open an issue first to discuss significant changes.

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes
4. Push and open a Pull Request

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

*Made with ☕ and a healthy dose of skepticism.*