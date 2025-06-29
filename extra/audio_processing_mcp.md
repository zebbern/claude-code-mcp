
# Audio Processing MCPs: Enabling Claude to Interact with Sound

These MCPs allow Claude to process, analyze, and generate audio, opening up possibilities for voice interactions, transcription, and sound manipulation.

## `GongRzhe/Audio-MCP-Server`: Local Audio Interaction

This server enables Claude to interact with your computer's audio system, including recording from microphones and playing audio through speakers.

### Key Features

*   **Microphone Input**: Capture audio directly from your system's microphone.
*   **Speaker Output**: Play audio through your system's speakers.

### Use Cases

*   **Voice Commands**: Control Claude or other applications using spoken language.
*   **Audio Playback**: Have Claude play audio files or generated speech.
*   **Real-time Transcription**: Potentially transcribe live audio (requires integration with a transcription service).

### Installation and Configuration

(Refer to the official GitHub repository for detailed instructions: [https://github.com/GongRzhe/Audio-MCP-Server](https://github.com/GongRzhe/Audio-MCP-Server))

## `mbailey-voice-mcp` (LobeHub): Voice Interactions

A Model Context Protocol (MCP) server that enables voice interactions with Claude and other LLMs. Requires only an OpenAI API key and microphone.

### Key Features

*   **Voice Input**: Transcribe spoken language into text for Claude.
*   **Voice Output**: Convert Claude's responses into spoken language.

### Use Cases

*   **Hands-free Interaction**: Control Claude using voice commands.
*   **Accessibility**: Provide voice-based interaction for users with disabilities.

### Installation and Configuration

(Refer to the LobeHub page for detailed instructions: [https://lobehub.com/mcp/mbailey-voice-mcp](https://lobehub.com/mcp/mbailey-voice-mcp))

## `elevenlabs/elevenlabs-mcp`: Advanced Speech Synthesis and Audio

This server allows MCP clients like Claude Desktop, Cursor, Windsurf, OpenAI Agents, and others to generate speech, clone voices, transcribe audio, and more.

### Key Features

*   **Speech Generation**: High-quality text-to-speech capabilities.
*   **Voice Cloning**: Create custom voices based on audio samples.
*   **Audio Transcription**: Convert spoken audio into text.

### Use Cases

*   **Content Creation**: Generate voiceovers for videos, podcasts, or presentations.
*   **Interactive Voice Assistants**: Develop sophisticated voice-enabled applications.
*   **Audio Analysis**: Transcribe and analyze audio content.

### Installation and Configuration

(Refer to the official GitHub repository for detailed instructions: [https://github.com/elevenlabs/elevenlabs-mcp](https://github.com/elevenlabs/elevenlabs-mcp))

## General Audio Processing MCP Considerations

*   **External APIs**: Many audio MCPs will rely on external APIs for advanced functionalities like speech-to-text or text-to-speech.
*   **Real-time vs. Batch Processing**: Consider whether your use case requires real-time audio interaction or can work with batch processing.

## Related Resources

*   [Add Image Generation, Audio Transcription and much more to Claude (Reddit discussion)](https://www.reddit.com/r/ClaudeAI/comments/1haxkrq/add_image_generation_audio_transcription_and_much/)
*   [AI Audiobook Generator with Claude, Cline, and ElevenLabs MCP (YouTube)](https://www.youtube.com/watch?v=FJdV-iE_Tps)


