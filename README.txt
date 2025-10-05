StrokeGPT Handy Controller

Welcome to StrokeGPT! This is a simple guide to help you set up your own private, voice-enabled AI companion for The Handy.

WINDOWS ONLY.

## What Does It Do?

* AI-Controlled Fun: Chat with an AI that controls your Handy's movements in real-time.
* Fully Customizable Persona: Change the AI's name, personality, and even their profile picture to create your perfect partner.
* Interactive Modes: Go beyond simple chat with advanced, interactive modes for Edging, Milking, and Auto-play. You can even influence the AI's patterns mid-session with chat messages!
* It Remembers You: The AI learns your preferences and remembers details from past chats.
* Internet-Connected for Control & Voice: The app requires an internet connection to send commands to The Handy's servers. If you enable voice, it also connects to the ElevenLabs API. Your AI model (Ollama) still runs 100% locally on your computer.
* Hidden Easter Eggs: A few secrets are tucked away.
* Built-in Safety: The app includes safety limiters to ensure movements always stay within your comfortable range.

## How to Get Started (easier than it looks!)

### Step 1: Install Prerequisites

You need two free programs to run the app.

**Python:**
* Download the latest version from the official Python website.
* During installation, you **must check the box** that says "Add Python to PATH."

**Ollama (The AI's "Brain"):**
* Download Ollama from the Ollama website.
* After installing, open a terminal (Command Prompt on Windows) and run the following command **once** to download the AI model:
    ```
    ollama run llama3:8b-instruct-q4_K_M

    ```
* This will take a few minutes because, much like your mum, models are chonky. Once it's finished, you can close the terminal. Make sure the Ollama application is running in the background before you start StrokeGPT.

### Step 2: Download & Install StrokeGPT

* Download the Project: Go to the project's GitHub page and click the green `<> Code` button, then select "Download ZIP".
* Unzip the file into a folder you can easily access, like your Desktop.
* Install Required Libraries:
    * Open a terminal directly in your new project folder:
    * Open the folder, click the address bar at the top, type `cmd`, and press Enter.
    * In the terminal, run this command:
        ```
        pip install -r requirements.txt

        ```

### Step 3: Run the App!

* Start the Server:
    * In the same terminal (still in your project folder), run this command:
        ```
        python app.py

        ```
    * The server is working when you see a message ending in `Running on http://127.0.0.1:5000`[cite: 88]. Keep this terminal window open.
* Open in Browser:
    * Open your web browser and go to the following address:
        http://127.0.0.1:5000
* The splash screen will appear. Press Enter to begin the on-screen setup guide. Enjoy!

### Using a Different LLM Backend (KoboldCPP, etc.)

StrokeGPT now supports multiple local LLM providers. By default it speaks to Ollama, but you can switch to KoboldCPP (or point it at another Ollama host) by updating `my_settings.json` after the app creates it the first time you run the server.

```json
{
  "llm_provider": "koboldcpp",           // "ollama" or "koboldcpp"
  "llm_base_url": "http://127.0.0.1:5001", // Base URL without the path segment
  "llm_model": "kobold_model_name"
}
```

* **Ollama:** keep `llm_provider` as `"ollama"`. `llm_base_url` should point at your Ollama instance (e.g., `http://127.0.0.1:11434`).
* **KoboldCPP:** set `llm_provider` to `"koboldcpp"` and point `llm_base_url` at the KoboldCPP server root. The service uses the `/api/v1/generate` endpoint and sends conversation history with sensible defaults for temperature, top-p, repetition penalty, and stop sequences.

Restart the app after changing the file so the new backend is loaded.

### Silly Tavern / External Client API

Third-party chat clients can talk to StrokeGPT via the new synchronous endpoint:

* **Endpoint:** `POST http://127.0.0.1:5000/api/chat`
* **Request body:**

  ```json
  {
    "message": "Your chat text",
    "key": "<handy api key>",
    "persona_desc": "Optional persona override"
  }
  ```

* **Response body:**

  ```json
  {
    "status": "ok",
    "chat": "Assistant reply text",
    "move": {"sp": 50, "dp": 50, "rng": 100},
    "new_mood": "Playful"
  }
  ```

The endpoint mirrors the in-app `/send_message` logic: it validates your Handy key, honours STOP/auto/edging commands, and executes motion instructions immediately when no background mode is active. When a command takes over (e.g., `stop`), the JSON `status` describes the outcome instead of returning chat text.
 

*A Quick Note on Speed

Don't be fooled by the 0-100 scale! The Handy is a powerful device. For many people, a Max Speed setting between 10 and 25 is more than intense enough. It's highly recommended to start low and find what works for you.

* Enjoying StrokeGPT?
This app is a passion project and is completely free. If you're having fun and want to support future development, consider buying me a coffee!

https://ko-fi.com/strokegpt
