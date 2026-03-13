# Spotify → VB-Cable → BUTT → Listen2MyRadio Guide

This guide shows how to stream music from your computer to friends using
a **free online radio server**.

------------------------------------------------------------------------

# Quick Start (5 Minutes)

1.  Install **VB-Cable**
2.  Install **BUTT**
3.  Create a free server on **Listen2MyRadio**
4.  Enter the server details in BUTT
5.  Start streaming
6.  Share the stream URL

That's it.

------------------------------------------------------------------------

# Pipeline Overview

## Visual Diagram (GitHub Friendly)

``` mermaid
flowchart TD
    A[Spotify / Music Player]
    B[VB-Audio Virtual Cable]
    C[BUTT Broadcasting Software]
    D[Listen2MyRadio Icecast Server]
    E[Listeners]

    A --> B
    B --> C
    C --> D
    D --> E
```

------------------------------------------------------------------------

# Simple Text Diagram

    Spotify
       ↓
    VB-Cable (routes audio)
       ↓
    BUTT (broadcasts audio)
       ↓
    Listen2MyRadio (hosts the stream)
       ↓
    Friends connect to the stream URL

------------------------------------------------------------------------

# 1. Install Required Software

## Spotify - optional

Download:

https://www.spotify.com/download/

Use Spotify to play the music you want to broadcast.

------------------------------------------------------------------------

## VB-Audio Virtual Cable

Routes audio from Spotify into the broadcasting software.

Download:

https://vb-audio.com/Cable/

After installing:

1.  Restart your computer
2.  Set **CABLE Input** as your Spotify output device

------------------------------------------------------------------------

## BUTT (Broadcast Using This Tool)

Broadcasting software that sends audio to the radio server.

Download:

https://danielnoethen.de/butt/

Install and start the application.

------------------------------------------------------------------------

# 2. Create a Free Radio Server

Go to:

https://listen2myradio.com

Create a **Free Icecast server**.

You will receive something like:

    Hostname: example.listen2myradio.com
    Port: 12345
    Mount: /stream
    Stream Password: ********

Save these values.

------------------------------------------------------------------------

# 3. Configure BUTT

Open:

    Settings → Server → Add

Example configuration:

    Type: Icecast
    Address: example.listen2myradio.com
    Port: 12345
    Mountpoint: /stream
    Icecast User: source
    Password: (Stream Password)

Save the profile.

------------------------------------------------------------------------

# 4. Configure Audio Settings

Open:

    Settings → Audio

Recommended settings:

    Audio Device: CABLE Output (VB-Audio Virtual Cable)

    Codec: MP3
    Bitrate: 96 kbps
    Samplerate: 44100 Hz
    Channels: Stereo
    Bitrate Mode: CBR

These settings are stable for most streaming scenarios.

------------------------------------------------------------------------

# 5. Start Streaming

Click **Start Streaming** in BUTT.

Expected log output:

    Connecting...
    Connection established

Audio is now being sent to the Listen2MyRadio server.

------------------------------------------------------------------------

# 6. Test the Stream

Open the stream in a browser or media player:

    http://example.listen2myradio.com:12345/stream

You should hear the music.

You can also test using VLC:

    Media → Open Network Stream

Paste the stream URL.

------------------------------------------------------------------------

# 7. Share the Stream

Send the stream URL to friends:

    http://example.listen2myradio.com:12345/stream

They can listen using:

-   Web browsers
-   VLC
-   Games that support radio streams
-   Virtual worlds

------------------------------------------------------------------------

# Troubleshooting

### No Audio

Make sure Spotify(or your audio program of choice) outputs to:

    CABLE Input

------------------------------------------------------------------------

### Connection Failed

Verify:

-   Hostname
-   Port
-   Mountpoint
-   Stream password

------------------------------------------------------------------------

### Audio Stuttering

Lower the bitrate to:

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
