# 🌍 Universal Translator: Multilingual Text-to-Speech Application

A powerful and accessible web application built with **Python** and **Gradio** for instant text translation and integrated text-to-speech (TTS) functionality. It supports a vast array of global languages, with a special focus on including major **regional languages of India**.

[](https://www.python.org/)[](https://gradio.app/)[](https://opensource.org/licenses/MIT)

-----

## ✨ Key Features

  * **Multilingual Translation:** Leverages the **Google Translator API** via `deep-translator` to provide accurate translation into over 100 languages.
  * **Integrated Text-to-Speech (TTS):** Generates high-quality audio pronunciation of the translated text using **gTTS**, making the app inclusive and helpful for language learning.
  * **Extensive Indian Language Support:** Includes major regional languages like **Hindi, Tamil, Telugu, Bengali, Marathi, Gujarati,** and **Kannada**, helping bridge communication gaps within the subcontinent.
  * **Intuitive Web Interface:** The UI is rapidly developed using **Gradio**, offering a clean, interactive experience directly in your browser.
  * **Automatic Setup:** The Python script handles all dependency checks and installations using `pip` and `subprocess`, ensuring a smooth launch.

-----

## ⚙️ Technical Stack

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Backend/Core** | Python 3.x | Application logic and environment setup. |
| **Translation Engine** | `deep-translator` | Python wrapper for Google Translate. |
| **Text-to-Speech** | `gTTS` | Google Text-to-Speech library for audio generation. |
| **Web Interface** | `gradio` | Creates the interactive, shareable web UI. |
| **Utility** | `tempfile`, `subprocess` | Handles temporary file management and dependency installation. |

-----

## 🚀 Getting Started

This project is designed for quick deployment.

### Prerequisites

You only need **Python 3.8+** and **`pip`** installed on your system.

### Installation and Running the App

1.  **Save the Code:** Save the complete Python code (including the `install_and_import()` function and the `gr.Blocks` definition) into a single file named `translator_app.py`.

2.  **Run the Script:** Execute the file from your terminal. The script will automatically install all necessary Python libraries (`deep-translator`, `gtts`, `gradio`).

    ```bash
    python translator_app.py
    ```

3.  **Access the App:**

      * A link to the application (e.g., `Running on local URL: http://127.0.0.1:7860`) will appear in your console.
      * A public share link will also be generated temporarily, as the script uses `app.launch(share=True)`.

-----

## 🌐 Language Support Highlights

The application supports an extensive list of global languages. A selection of the available options is listed below:

| Language | Code | Language | Code |
| :--- | :--- | :--- | :--- |
| 🇺🇸 **English** | `en` | 🇮🇳 **Hindi** | `hi` |
| 🇪🇸 **Spanish** | `es` | 🇮🇳 **Bengali** | `bn` |
| 🇫🇷 **French** | `fr` | 🇮🇳 **Tamil** | `ta` |
| 🇩🇪 **German** | `de` | 🇮🇳 **Telugu** | `te` |
| 🇷🇺 **Russian** | `ru` | 🇮🇳 **Marathi** | `mr` |
| 🇯🇵 **Japanese** | `ja` | 🇮🇳 **Gujarati** | `gu` |
| 🇰🇷 **Korean** | `ko` | 🇮🇳 **Kannada** | `kn` |
| 🇨🇳 **Chinese (Simplified)** | `zh-CN` | 🇵🇰 **Urdu** | `ur` |
| 🇸🇦 **Arabic** | `ar` | 🇹🇷 **Turkish** | `tr` |

-----

## 📝 Usage Instructions

1.  **Enter Text:** Type or paste your source text into the "📝 Enter text to translate" box.
2.  **Select Target Language:** Choose your desired language from the "🎯 Target Language" dropdown menu.
3.  **Translate:** Click the **🚀 Translate** button.
4.  **Review Output:** The "✨ Translation Result" box will display the text, and the "🔊 Pronunciation" player will instantly provide the audio output, which can also be downloaded.
5.  **Clear:** Use the **🗑️ Clear** button to reset all fields.
