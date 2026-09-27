# Ans Ali, AI Filmmaker: website

## 1. Make your Drive folder public (required)
Open the "AI Films" folder in Google Drive, click Share, set General access to
"Anyone with the link" as Viewer. Covers and full films load from Drive, so
without this they will not show for visitors.

## 2. Add the showreel background loop
The full 395 MB showreel plays from Drive when someone clicks "Play showreel".
The moving background on the home page needs a small silent loop saved as
media/showreel.mp4 (aim for under 25 MB). With ffmpeg installed:

    ffmpeg -i "Show Reel.mp4" -t 45 -an -vf "scale=1920:-2" -c:v libx264 -crf 28 -preset slow -movflags +faststart media/showreel.mp4

Until this file exists, the home page shows a still instead.

## 3. Film intros (hover previews and the rotating screen)
The 11 Cafe Stories intros are already linked from your Drive and play on hover
and in the library's rotating screen. Drive can be slow to start short clips, so
for the smoothest feel, download each intro into media/previews/ and rename it
to the film's id. The site uses a local file first whenever one exists.
Ids: until, drawing, poppy, letter, vanishing, sloane, dove, will, perfumer,
heiress, duchess, diplomat, blackswan, london, egypt, edinburgh, sanfrancisco,
starlight, newyork, midnight, houserules

For films with no intro, you can cut one (6 to 8 seconds, silent):

    ffmpeg -ss 30 -i "THE DRAWING.mp4" -t 8 -an -vf "scale=1280:-2" -c:v libx264 -crf 28 -movflags +faststart media/previews/drawing.mp4

## 4. Toolkit images (optional)
Put an image for any tool in media/logos/ and it replaces that tool's tile.
Names: higgsfield, flow, morphic, openart, lovart, claude, chatgpt, gemini,
premiere-pro, davinci-resolve, capcut, figma, suno (.png, .svg, or .webp)

## 5. Deploy on Vercel
Easiest: push this folder to a GitHub repo, then on vercel.com choose
Add New, Project, import the repo, and Deploy. Every push redeploys.
Or from this folder run:  npx vercel --prod

## 6. Your manager
Open the Portfolio page and press "Manager login" at the bottom (or go to
your-site-url/#/studio), then enter your manager password. Tabs:
- Films: add or edit films, drop a cover image (or paste a link), and set the
  order by dragging, typing a position number, or the top/up/down/bottom buttons.
- Home and Library: pick which films show on the Home page and on the Library's
  rotating screen, and in what order.
- Blog: write, edit, reorder, or delete posts, with an optional cover image.
- Snapshots: drop new frames with their light, lens, and palette notes.
- Contact: phone, email, and LinkedIn shown at the bottom of every page.
- Showreel and categories.
Changes preview on your browser only. Press "Export works.js", replace works.js
in this folder with the downloaded file, and redeploy. Dropped images are saved
inside works.js, compressed for the web; the button shows the file size.
