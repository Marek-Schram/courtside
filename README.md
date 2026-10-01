# Courtside

A motion-controlled tennis game for Windows that uses ordinary Android phones as the controllers. Hold a phone like a racket and swing it: the phone streams its gyroscope to the PC, and the game reads the swing's timing, direction, spin and power. A phone propped up as a camera can instead track a player's body with on-device pose estimation.

Courtside is a solo side project and a working prototype: singles against a CPU opponent or a friend, practice drills, saved player profiles with photo faces, instant replays and a match-win spotlight. It's the first game for a planned open motion-game console: a PC hub that pairs the phones, with separate games that plug into it.

| Instant replay | Match-win spotlight |
|---|---|
| ![Side-on instant replay with a REPLAY tag](screenshots/instant-replay.png) | ![The winner in a spotlight under a VICTORY title](screenshots/match-win-spotlight.png) |

## Try it

Download **Courtside-Windows.zip** and **Courtside-Sensor.apk** from the [latest release](../../releases/latest).

1. Unzip and run `Run-Courtside.cmd` on a Windows PC. Keyboard play works with no phone: Q / W / E swing (slow, medium, fast), A / D aim, and the first press on your serve tosses the ball.
2. For motion play, install the APK on one or two Android phones (Android 8+). Put the PC and phones on the same Wi-Fi, enter the four-digit room code shown on the PC, choose **Remote**, and tap **Join game**. Each phone is assigned a player automatically and asked for a face photo.
3. Use a wrist strap.

It's an unsigned prototype: Windows SmartScreen may ask you to confirm, and the APK installs from outside the Play Store.

## How it works

- **Game:** Godot 4.4 (GDScript), with the GL Compatibility renderer so it runs smoothly on integrated laptop graphics (about 70 FPS on an Intel Iris Xe during replays).
- **Phone app:** native Android (Java). In Remote mode it streams the gyroscope at 200 Hz over UDP. In Camera mode it runs MediaPipe pose estimation on the phone and sends body landmarks instead of video.
- **Pairing:** a four-digit room code with UDP broadcast discovery, per-session tokens, automatic player assignment, and an experimental offline mode in which one phone hosts its own Wi-Fi hotspot (not yet tested on real hardware).
- **Swing reading:** the swing detector is tuned against recordings of real swings, not guesses. A replay-regression suite re-reads 14 real recordings on every change and flags any swing that is now read worse.
- **Gameplay:** ball flight with topspin and slice, timing-based aim (early pulls the ball cross-court, late pushes it down the line), a four-level CPU opponent, and assists for smashes and volleys.
- **Presentation:** procedurally animated players, an instant replay from a recorded frame buffer with slow motion on the winning shot, and a spotlight finale. The music and sound effects are original: composed as note data and rendered in code, or synthesized.
- **Testing:** an automated suite of about 760 assertions (unit, swing-pipeline and full-scene tests), an integration test over real UDP, and self-play visual audits of racket-to-ball contact.

## Status

This is a prototype. The latest build is tested in software and against recorded swings; play with real phones is being tested in short playtest cycles. The source code is private for now.

## Credits

Built with [Godot Engine](https://godotengine.org) (MIT), the TweenFX Godot add-on (MIT) and [Google MediaPipe](https://github.com/google-ai-edge/mediapipe) (Apache 2.0), using the Inter typeface (SIL Open Font License). The full notices ship in the download's `licenses` folder. All art, music and sound were made for this project.
