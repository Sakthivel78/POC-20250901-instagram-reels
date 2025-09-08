Instagram Reels Format Guidelines:

Video Specifications
*Aspect Ratio : 9:16 
*Resolution: 1080 x 1920 pixels 
*Minimum Resolution: 720 pixels minimum
*Frame Rate: Minimum 30 FPS (some sources suggest up to 60 FPS for smoother playback)
*Format: MP4 with H.264 codec
*Bitrate: 3,500-5,000 kbps 

Key Requirements

*Instagram accepts videos with aspect ratios between 1.91:1 and 9:16
*Videos with width between 320-1080 pixels maintain original resolution if aspect ratio is between 1.91:1 and 4:5
*Full-screen vertical format provides best viewing experience

Cover Photo

*Same dimensions as video: 1080 x 1920 pixels
*Keep important elements within center 4:5 area to avoid cropping in different views
*Displays differently across profile grid, explore page, and full-screen view

Best Practices
*Target 1080 x 1920 pixels for optimal quality
*Use minimum 30 FPS for smooth playback
*Avoid black bars by maintaining 9:16 aspect ratio
*Enable "high-quality uploads" in Instagram settings for better compression

n8n:

1.Workflows - automation pipelines made of connected nodes.
2.HTTP - Request Node is the main tool for talking to external APIs.
3.Execute Command Node runs shell commands directly inside a workflow.
4.Use environment variables ({{$env.VAR_NAME}}) to inject config/secrets.
5.Always store sensitive info in Credential Manager instead of hardcoding.

ffmpeg:

Scale Filter (Resize video)
Syntax: scale=width:height[:flags]
    *width / height: target dimensions.
    *Use 1 to auto-calculate aspect ratio.
    *Use variables like iw (input width), ih (input height).

    Ex:
    
    Scale to 1280x720
    *vf "scale=1280:720"

    Scale width to 1280, auto height (maintain aspect ratio)
    *vf "scale=1280:-1"

    Half size
    *vf "scale=iw/2:ih/2"

Pad Filter (Add black borders / expand canvas)
Syntax: pad=width:height:x:y[:color]

    * width / height: final canvas size.
    * x / y: position of original video inside the padded canvas.
    * color: border color (default black).

    Ex:

    # Pad to 1920x1080, centered
    vf "pad=1920:1080:(ow-iw)/2:(oh-ih)/2"

    # Pad to square 1080x1080
    vf "pad=1080:1080:(ow-iw)/2:(oh-ih)/2"

    # White border padding
    vf "pad=1920:1080:0:0:white"

overlay Filter (Place one video/image over another)

Syntax: overlay=x:y[:enable='expression']


    * x / y: top-left placement of overlay video/image.

    enable: condition (like time-based).

    Ex:

    # Overlay watermark.png at top*left
    ffmpeg -i video.mp4 -i watermark.png -filter_complex "overlay=10:10" output.mp4

    # Overlay at bottom-right
    filter_complex "overlay=W-w-10:H-h-10"

    # Show overlay only from 5s to 10s
    filter_complex "overlay=10:10:enable='between(t,5,10)'"


