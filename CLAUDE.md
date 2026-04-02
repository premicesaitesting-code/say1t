# Say1t

A Progressive Web App (PWA) for content creators: AI-powered script writing, teleprompter with live camera, video recording with audio, auto-captioning from script, video filters, and export with burned-in captions.

## Architecture

Single-page HTML/CSS/JS app (no build step). The file `public/index.html` is the entire application.

### Core Flow
1. **Write** (Step 1): Script editor with AI generation via Anthropic API. Script stats (word count, estimated time).
2. **Record** (Step 2): Teleprompter overlay on live camera feed. MediaRecorder captures video+audio. CSS filters apply to camera. Guide line, focus dimming, mirror mode, countdown.
3. **Edit** (Step 3): Script auto-splits into timed captions. 8 caption style presets (Classic, Bold, Outline, Karaoke, Neon, Minimal, Boxed, Gradient). 12 video filters with intensity control. Trim handles on timeline. Canvas-based export burns filters+captions into video.

### Key Technologies
- MediaRecorder API for video/audio capture
- Canvas API for export rendering (filters + captions burned in)
- CSS filters for live preview (camera + editor)
- Web Audio API for mic metering
- PWA: manifest.json, service worker for offline caching

### Known Issues / TODO
- Export audio capture can fail on some mobile browsers (createMediaElementSource limitation)
- MP4 export only works on browsers that support it in MediaRecorder (Chrome). Falls back to WebM.
- Filters use CSS for preview but canvas color overlays for export. Some visual difference is expected.
- No WebGL shaders yet (would improve filter quality and add more options)
- Single HTML file is 870+ lines. Could benefit from splitting into modules.

## File Structure
```
public/
  index.html      -- Main application
  manifest.json   -- PWA manifest
  sw.js           -- Service worker
  icon-192.png    -- App icon 192x192
  icon-512.png    -- App icon 512x512
```

## Deployment
- Static site: drag `public/` folder to Netlify Drop, Cloudflare Pages, or Vercel
- PWA install: Add to Home Screen on mobile browsers
- App stores: Wrap with Capacitor (iOS/Android) or PWABuilder (Android)

## Style Guide
- Dark theme, accent color #ff5535
- Fonts: Outfit (display), DM Mono (monospace)
- Never use em dashes in any text content
- No "made by Claude" or attribution comments in code
