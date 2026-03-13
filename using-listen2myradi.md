# Simple Online Radio Setup

**Spotify → VB-Cable → BUTT → Listen2MyRadio**

This guide explains how to stream music from your computer to friends
using a free radio server.

Pipeline:

    Spotify / Music
          ↓
    VB-Audio Virtual Cable
          ↓
    BUTT (Broadcast Using This Tool)
          ↓
    Listen2MyRadio Server
          ↓
    Listeners (Browser / Game / VLC)

------------------------------------------------------------------------

# 1. Install Required Software


## VB-Audio Virtual Cable

Routes system audio into the broadcasting software.

Download: https://vb-audio.com/Cable/

After installing:

1.  Restart your computer
2.  Set **CABLE Input** as the playback device for Spotify

------------------------------------------------------------------------

## BUTT (Broadcast Using This Tool)

Broadcasting software used to send audio to the radio server.

Download: https://danielnoethen.de/butt/

Install and start BUTT.

------------------------------------------------------------------------

# 2. Create a Free Radio Server

Go to:

https://listen2myradio.com

Create a **Free Icecast Server**.

You will receive something like:

    Hostname: example.listen2myradio.com
    Port: 12345
    Mount: /stream
    Stream Password: ********

Keep these values.

------------------------------------------------------------------------

# 3. Configure BUTT

Open:

    Settings → Server → Add

Enter the values from Listen2MyRadio.

Example:

    Type: Icecast
    Address: example.listen2myradio.com
    Port: 12345
    Mountpoint: /stream
    Icecast User: source
    Password: (Stream Password)

Save the configuration.

------------------------------------------------------------------------

# 4. Configure Audio Settings

Open:

    Settings → Audio

Recommended stable configuration:

    Audio Device: CABLE Output (VB-Audio Virtual Cable)

    Codec: MP3
    Bitrate: 96 kbps
    Samplerate: 44100 Hz
    Channels: Stereo
    Bitrate Mode: CBR

------------------------------------------------------------------------

# 5. Start Broadcasting

Press **Start Streaming** in BUTT.

You should see:

    Connecting...
    Connection established

Your computer is now sending audio to Listen2MyRadio.

------------------------------------------------------------------------

# 6. Test the Stream

Open the stream in a browser or player:

    http://example.listen2myradio.com:12345/stream

You should hear the music.

You can also test using VLC:

    Media → Open Network Stream

Paste the stream URL.

------------------------------------------------------------------------

# 7. Share With Friends

Send them your stream URL:

    http://example.listen2myradio.com:12345/stream

They can listen from:

-   web browsers
-   VLC
-   games that support radio streams
-   virtual worlds

------------------------------------------------------------------------

# Troubleshooting

### No audio

Make sure Spotify is playing to:

    CABLE Input

### Cannot connect

Check:

-   Hostname
-   Port
-   Mountpoint
-   Stream Password

### Stuttering audio

Lower bitrate to:

    96 kbps

------------------------------------------------------------------------

# Summary

    Spotify
       ↓
    VB-Cable
       ↓
    BUTT
       ↓
    Listen2MyRadio
       ↓
    Listeners
