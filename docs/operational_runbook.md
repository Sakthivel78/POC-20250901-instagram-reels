Instagram Reel Project : 

Overview:

    *The operational aspects of the Instagram Reel automation project built using n8n workflows. 
    The system automates video content creation, AI avatar presentation, subtitle generation, 
    and final video rendering for Instagram Reels.

System Architecture:

    Platform: n8n (Node-based automation platform)
    Primary Workflow: Instagram Reel Content Pipeline with AI Avatar
    Dependencies: ElevenLabs TTS API, HeyGen Avatar API, Pexels API, FFmpeg, Gmail API, Google Drive API
    Deployment: Self-hosted n8n instance on Windows

Workflow Components Analysis:

    1.Content Definition Node - Edit Fields1
    Purpose: Defines content parameters and script text

    Node Type: Set/Edit Fields
    Inputs: Manual content definition
    Outputs: Content title, slug, and script text

    2.Text-to-Speech Node - ELEVENLABS
    Purpose: Converts script text to audio using ElevenLabs API

    Node Type: HTTP Request
    API Endpoint: https://api.elevenlabs.io/v1/text-to-speech/JBFqnCBsd6RMkjVDRZzb
    Output Format: MP3 (44.1kHz, 128kbps)

    3. AI Avatar Video Node (HEYGEN)
    Purpose: Generates AI presenter video using HeyGen API

    Node Type: HTTP Request
    API Endpoint: https://api.heygen.com/v2/video/generate
    Avatar: Brandon_Lobby_Standing_Front_public
    Dimensions: 720x1280 (Instagram Reel format)

    4. B-roll Asset Node (Pexels API)
    Purpose: Fetches stock images for B-roll content

    Node Type: HTTP Request
    API Endpoint: https://api.pexels.com/v1/search
    Query: Dynamic based on content theme

    5. Video Processing Pipeline
    Purpose: Combines presenter video, B-roll, and subtitles

    Tools: FFmpeg commands
    Operations: Video overlay, subtitle burning, format optimization

    6. Distribution Nodes
    Purpose: Saves files locally and uploads to Google Drive

    Local Storage: Windows file system paths
    Cloud Backup: Google Drive integration
    Notification: Gmail alerts

Environment Variables:

    1.ElevenLabs TTS API:

    ELEVENLABS_API_KEY=sk_1c2f5409d7c7b62a9351886a913e7d35ef72bbe0eb81fe33
    ELEVENLABS_VOICE_ID=JBFqnCBsd6RMkjVDRZzb

    2.HeyGen Avatar API:

    HEYGEN_API_KEY=YTRlNGJiODQwYzcwNGEyMDg4NzM3NTliZjViYjVkN2EtMTc1NzgyNjc5Ng==
    HEYGEN_AVATAR_ID=Brandon_Lobby_Standing_Front_public
    HEYGEN_VOICE_ID=6be73833ef9a4eb0aeee399b8fe9d62b

    3.Pexels Stock Images API:

    PEXELS_API_KEY=WVz5QxjeVWSvsijnQyynXpmKijy5nFUddBcgUm6Ws67WsNueBJZJGWyO

    4.n8n Configuration:

    n8n_HOST=0.0.0.0
    n8n_PORT=5678
    

    5.File System Paths:

    PROJECT_ROOT=C:\\Users\\User\\Desktop\\Instagram Reel_Project
    AUDIO_PATH=C:\\Users\\User\\Desktop\\Instagram Reel_Project\\audio
    PRESENTER_PATH=C:\\Users\\User\\Desktop\\Instagram Reel_Project\\presenter
    BROLL_PATH=C:\\Users\\User\\Desktop\\Instagram Reel_Project\\broll
    SUBS_PATH=C:\\Users\\User\\Desktop\\Instagram Reel_Project\\subs
    RENDERS_PATH=C:\\Users\\User\\Desktop\\Instagram Reel_Project\\renders

    6.Google Services:

    GMAIL_RECIPIENT=sakthivelbabu2001@gmail.com
    GDRIVE_FOLDER_ID=1IsIywfp0cXZRGin5TL_K_zbPS-Vk8a6B

    7.FFmpeg Configuration

    FFMPEG_PATH=ffmpeg

Error Handling:

    1.ElevenLabs TTS Errors:

    Error Code: ELEVENLABS_QUOTA_EXCEEDED
    Common Causes: Monthly character limit reached. Per Month 10k credit.

    2.HeyGen Avatar Generation Errors:

    Error Code: HEYGEN_GENERATION_FAILED
    Common Causes: Script too long, invalid characters, API limits

    3.Video Status Polling Errors:

    Error Code: HEYGEN_STATUS_TIMEOUT
    Common Causes: Video generation taking longer than expected
    Resolution: Increase wait time, check HeyGen service status
    Auto-retry: Yes - polls every 3 minutes for 2 times

    4.Pexels API Errors:

    Error Code: PEXELS_NO_RESULTS
    Common Causes: No images found for search query
   
    5.FFmpeg Processing Errors:

    Error Code: FFMPEG_PROCESSING_FAILED
    Common Causes: Missing input files, code issues, path problems 
    Important :Verify all input files exist, check FFmpeg installation
 
Known Issues:

    1. HeyGen Video Generation Timeouts:

    -Avatar video generation occasionally takes longer than expected (>5 minutes)
    -Workflow hangs at status checking, may timeout
    -Increase wait time in Wai t1 node to 5 minutes, extend status check loop
   
    2. Windows File Path Escaping in FFmpeg:
    
    -Windows backslashes in file paths cause FFmpeg subtitle command to fail
    -subtitle burning step fails with path parsing errors
    -use quadruple backslashes in subtitle filter: C\\\\:\\\\\\\\Users\\\\\\\\...
    -FFmpeg Windows path handling limitation

    3. Pexels API Search Result Inconsistency:

    -Search queries sometimes return no relevant images
    -some time Generic/poor quality B-roll content
    -Implement fallback search terms array, manual image curation

    4.SRT Subtitle Timing Accuracy:

    -Generated SRT timestamps may not perfectly align with audio
    -Subtitles appear slightly early or late
    -Fine-tune timing calculation in Generate SRT Subtitles node
    -Manual quality checks on random samples

    5. Gmail Attachment:

    -Notification email sent without video attachment
    -Send Google Drive link instead of direct attachment
