+++
author = "Cesbo"
title = "HLS"
date = "2023-02-10"
tags = [
    "hls",
    "protocols",
]
categories = [
    "streaming",
]
+++
# HLS

HLS (HTTP Live Streaming protocol) - is an HTTP-based adaptive bitrate streaming communications protocol. HLS protocol is based on the division of one media file into many chanks. This allows the user to access the media file piece by piece in real time. Detailed description available in the [RFC 8216][RFC] standard.
<!--more-->
HLS is based on standard HTTP transactions. It’s compatible with any firewall or proxy server that lets through standard HTTP traffic. It also allows HLS to use a standard encryption mechanism and secure-key distribution using HTTPS.

## Multibitrate

The protocol provides mechanisms for players to adapt to unreliable network conditions without causing user-visible playback stalling. To enable a player to adapt to the bandwidth of the network, the original video is encoded in several distinct quality levels. The server serves an index, called a "master playlist", of these encodings, called "variant streams". The player can then choose between the variant streams during playback, changing back and forth seamlessly as network conditions change.

## HLS architecture

HLS uses a web server, that implements support for it, to distribute audiovisual content and requires specific software to fit the content into a proper format (codec) for transmission in real time over a network. The service architecture comprises:

- Server
- Distributor
- Client

![HLS architecture](hls.png)

### Server

Server codifies and encapsulates the input video flow in a proper format for the delivery. Then it is prepared for distribution by segmenting it into different chunks (Media Segments) and creating an index file (Playlist).

Video files codified in H.264, H.265 format and audio in AAC, MP3, AC-3 or EC-3. This is encapsulated by MPEG-2 Transport Stream or MP4 to carry it.

The stream is divided into fragments of equal duration. It also creates a Playlist that contains URIs and descriptive tags, saved in m3u8 format.

Playlist contains a list of Media Segments, which, when played sequentially, will play the full media file. A Media Playlist contains a series of Media Segments that make up the full media file. A Media Segment is specified by a URI or byte range.

Each Media Segment in a Media Playlist contains a part of the full media file and has a unique integer Media Sequence Number. The Media Sequence Number of the first segment in the Media Playlist is either 0 or declared in the Playlist. Number of every other segment is equal to the Media Sequence Number of the segment that precedes it plus one. This allows the protocol to combine Media Segments into one sequence.

### Distributor

Distributor formed by a standard web server, it is engaged in the delivery of the necessary data packages to users in accordance with their request.

### Client

The client software downloads first the Playlist through a URL and then the several media files available. The playback software assembles the sequence to allow continued display to the user.


[//]: Links
[RFC]: https://www.rfc-editor.org/rfc/rfc8216
