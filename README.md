import subprocess
import sys

def install_and_import():
    packages = {'deep-translator': 'deep_translator', 'gtts': 'gtts', 'gradio': 'gradio'}
    
    for package, import_name in packages.items():
        try:
            __import__(import_name)
        except ImportError:
            print(f"Installing {package}...")
            subprocess.check_call([sys.executable, "-m", "pip", "install", package])

install_and_import()

from deep_translator import GoogleTranslator
from gtts import gTTS
import gradio as gr
import tempfile
import time

# FIXED: Proper language code mapping
LANGUAGES = [
    ('🇺🇸 English', 'en'),
    ('🇪🇸 Spanish', 'es'), 
    ('🇫🇷 French', 'fr'),
    ('🇩🇪 German', 'de'),
    ('🇮🇹 Italian', 'it'),
    ('🇵🇹 Portuguese', 'pt'),
    ('🇷🇺 Russian', 'ru'),
    ('🇯🇵 Japanese', 'ja'),
    ('🇰🇷 Korean', 'ko'),
    ('🇨🇳 Chinese (Simplified)', 'zh-CN'),
    ('🇮🇳 Hindi', 'hi'),  # ✅ FIXED: Use 'hi' code, not 'हिन्दी'
    ('🇸🇦 Arabic', 'ar'),
    ('🇹🇷 Turkish', 'tr'),
    ('🇳🇱 Dutch', 'nl'),
    ('🇸🇪 Swedish', 'sv'),
    ('🇳🇴 Norwegian', 'no'),
    ('🇩🇰 Danish', 'da'),
    ('🇫🇮 Finnish', 'fi'),
    ('🇵🇱 Polish', 'pl'),
    ('🇨🇿 Czech', 'cs'),
]

def translate_text(input_text, target_lang):
    """Fixed translation function with proper language code handling"""
    if not input_text.strip():
        return "Please enter text to translate.", None, "❌ No input"
    
    if not target_lang:
        return "Please select a target language.", None, "❌ No language"
    
    try:
        print(f"🔄 Translating to language code: {target_lang}")  # Debug log
        
        start_time = time.time()
        
        # ✅ FIXED: Ensure we're using the correct language code
        translator = GoogleTranslator(target=target_lang)
        translated = translator.translate(input_text)
        
        if not translated:
            return "Translation failed - empty result", None, "❌ Empty result"
        
        translation_time = time.time() - start_time
        
        # Get language name for display
        lang_name = next((name for name, code in LANGUAGES if code == target_lang), target_lang)
        
        result = f"**Translation:** {translated}\n\n**Language:** {lang_name}\n**Time:** {translation_time:.2f}s"
        
        # Generate audio
        audio_path = None
        try:
            tts = gTTS(text=translated, lang=target_lang, slow=False)
            with tempfile.NamedTemporaryFile(delete=False, suffix=".mp3") as tmp:
                tts.save(tmp.name)
                audio_path = tmp.name
        except Exception as e:
            print(f"Audio generation failed: {e}")
        
        status = f"✅ Success in {translation_time:.2f}s"
        return result, audio_path, status
        
    except Exception as e:
        error_msg = f"❌ Error: {str(e)}\n\n**Debug Info:**\n• Target language code: {target_lang}\n• Input length: {len(input_text)}\n\n**Solutions:**\n• Check internet connection\n• Try shorter text\n• Try different language"
        return error_msg, None, f"❌ Failed: {str(e)}"

def clear_all():
    return "", "", None, ""

# Create interface with FIXED language options
with gr.Blocks(title="🌍 Universal Translator ") as app:
    
    gr.HTML("""
    <div style="text-align: center; padding: 20px; background: linear-gradient(90deg, #667eea, #764ba2); color: white; border-radius: 10px; margin-bottom: 20px;">
        <h1>🌍 Universal Translator </h1>
    </div>
    """)
    
    with gr.Row():
        with gr.Column():
            input_text = gr.Textbox(
                label="📝 Enter text to translate",
                placeholder="Type your text here...",
                lines=4
            )
            
            # ✅ FIXED: Use proper language code mapping
            target_lang = gr.Dropdown(
                choices=LANGUAGES,  # This ensures proper (display_name, code) mapping
                label="🎯 Target Language",
                value="hi"  # Default to Hindi with correct code
            )
            
            with gr.Row():
                translate_btn = gr.Button("🚀 Translate", variant="primary", size="lg")
                clear_btn = gr.Button("🗑️ Clear", variant="secondary")
        
        with gr.Column():
            result_output = gr.Markdown(label="✨ Translation Result")
            status_output = gr.Textbox(label="📊 Status", interactive=False)
    
    audio_output = gr.Audio(label="🔊 Pronunciation", show_download_button=True)
    
    # Event handlers
    translate_btn.click(
        fn=translate_text,
        inputs=[input_text, target_lang],
        outputs=[result_output, audio_output, status_output]
    )
    
    clear_btn.click(
        fn=clear_all,
        outputs=[input_text, result_output, audio_output, status_output]
    )

# Launch
if __name__ == "__main__":
    print("\n🚀 Starting Fixed Universal Translator...")
    print("✅ Language code mapping issue resolved!")
    
    app.launch(
        share=True,
        server_port=None,
        show_error=True,
        inbrowser=True
    )


