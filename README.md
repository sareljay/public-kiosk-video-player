# Kiosk Video Player

A simple, single-file HTML video player designed for kiosk displays that plays videos in an infinite loop with offline caching support.

## Usage

1. Open the HTML file in a web browser with the `?src=` query parameter:
   ```
   kiosk_video_player_supabase_single_file_html.html?src=YOUR_VIDEO_URL
   ```

2. The video will automatically play on loop in fullscreen view

## Query Parameters

- **`src`** (required) - Public URL to your video file
- **`type`** (optional) - MIME type (e.g., `video/mp4`, `video/webm`)
- **`controls`** (optional) - Set to `1` to show video controls (default: hidden)
- **`muted`** (optional) - Set to `0` to unmute (default: `1` / muted)
- **`volume`** (optional) - Volume level from `0` to `1` (ignored if muted)
- **`fit`** (optional) - Object fit mode: `cover` or `contain` (default: `cover`)
- **`cache`** (optional) - Set to `0` to disable caching (default: enabled)

### Example
```
kiosk_video_player_supabase_single_file_html.html?src=https://example.com/video.mp4&controls=1&fit=contain
```

## Features

### Video Playback
- **Autoplay** - Video starts automatically when page loads
- **Infinite Loop** - Video replays seamlessly forever
- **Muted by Default** - Ensures autoplay works across all browsers
- **Plays Inline** - No fullscreen popups on mobile devices
- **Picture-in-Picture Disabled** - Keeps video in the main view

### Display Options
- **Full Viewport Coverage** - Video fills entire screen (100vw × 100vh)
- **Object Fit Cover** - Video scales to fill screen while maintaining aspect ratio (can be changed to `contain`)
- **Black Background** - Clean appearance during loading or if video doesn't fill screen
- **Double-Click Fullscreen** - Toggle fullscreen mode by double-clicking the video

### Offline & Caching
- **Offline-First Cache** - Downloads and stores video locally using Cache Storage API
- **Smart Revalidation** - Checks if video changed using ETag/Last-Modified headers
- **Instant Playback** - Plays cached version immediately while checking for updates
- **No Service Worker Required** - Uses Cache Storage API directly

### Reliability Features
- **Auto-Reload on Error** - Page reloads automatically if video fails (1 second delay)
- **Robust Autoplay** - Falls back to muted playback if unmuted autoplay fails
- **Stall Recovery** - Attempts to resume playback if video stalls
- **Visibility Recovery** - Resumes playback when page becomes visible again
- **Network Recovery** - Resumes playback when internet connection is restored
- **Loop Enforcement** - Forces video restart if `ended` event fires

### Kiosk Protection
- **Context Menu Disabled** - Right-click menu is blocked
- **Download Prevention** - Controls list excludes download option
- **Keyboard Shortcuts Blocked** - Ctrl+S (save) and Ctrl+P (print) are disabled

## What The Code Does To The Video

1. **Loads** the video from the URL specified in the `?src=` parameter
2. **Caches** the entire video file locally in the browser for offline playback
3. **Scales** the video to fill the entire viewport while maintaining aspect ratio
4. **Mutes** the video by default to comply with browser autoplay policies
5. **Loops** the video infinitely using the `loop` attribute and manual restart on `ended` event
6. **Monitors** playback and automatically reloads the page if any errors occur
7. **Creates** a blob URL from the cached video for smooth, jitter-free looping
8. **Prevents** user interactions like right-clicking, downloading, or printing
9. **Enables** fullscreen mode via double-click for true kiosk experience
10. **Revalidates** the cached video on each page load to ensure it's up-to-date

## Browser Compatibility

Works in all modern browsers that support:
- HTML5 Video
- Cache Storage API
- Blob URLs
- Fullscreen API
