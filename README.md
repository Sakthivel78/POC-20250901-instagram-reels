# POC-2025-09-01-instagram-reels

# Instagram Reel Generator:
  
  Automatically generate engaging Instagram Reels by combining AI-powered video creation, voice synthesis, and subtitle generation.
  This tool uses HeyGen for video creation, ElevenLabs for voice synthesis,Pexels and FFmpeg for seamless video processing.

# Features:

  - AI Video Generation - Create realistic talking head videos with HeyGen
  - AI Voice Synthesis - Generate natural-sounding voiceovers with ElevenLabs
  - Automatic Subtitles - Add synchronized captions to your videos
  - Video Processing - Combine MP3 audio, MP4 video, and subtitles using FFmpeg
  - Instagram Ready - Output optimized for Instagram Reels 

# Prerequisites:
1. Node.js 18+
2. Fmpeg installed on your system
3. HeyGen account
4. ElevenLabs account
5. Pexels account
  
# FFmpeg Installation:

1.Windows:

  Download from FFmpeg official site and add to PATH
  
2.macOS:
```
  brew install ffmpeg
```
# Getting API Keys:

1.HeyGen API Key

  - Sign up at HeyGen.
  
  - Go to API settings in your dashboard.
  
  - Generate a new API key.
  
  - Copy the key to your .env file.

2.ElevenLabs API Key:

  - Create account at ElevenLabs
  
  - Navigate to Profile → API Key
  
  - Copy your API key
  
  - Add to your .env file

# Edit .env with your API credentials:

 ```env

   HEYGEN_API_KEY=your_heygen_api_key
   ELEVENLABS_API_KEY=your_elevenlabs_api_key
   PEXELS_API_KEY=your_pexels_api_key
```
# Workflow:

  1. Text Input → Script or text file
  2. Voice Generation → ElevenLabs creates MP3 audio
  3. Video Generation → HeyGen creates MP4 video with avatar
  4. Image Search → Pexels fetches photos based on search terms
  5. Subtitle Creation → Generate SRT file with timestamps
  6. Video Combining → FFmpeg merges audio, video, and subtitles
  7. Output → Instagram reel MP4 file is ready
