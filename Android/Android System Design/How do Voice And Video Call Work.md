# How Do Voice and Video Calls Work?

Voice and video calling rely on real-time communication (RTC) protocols to transmit audio and video data between users over the internet or mobile networks.

## 1. Key Components:
- **Signaling**: Establishes, modifies, and terminates the call (e.g., WebRTC, SIP).
- **Media Streaming**: Transfers audio/video data using RTP (Real-Time Transport Protocol).
- **Codecs**: Compress and decompress media streams (e.g., Opus for audio, VP8/VP9 for video).
- **Network Transport**: Uses UDP/TCP with protocols like WebRTC, VoIP, or SRTP for secure communication.
- **NAT Traversal**: Handles firewalls and NAT using STUN, TURN, and ICE servers.

## 2. Call Flow:
1. **Call Initiation**:
   - User A requests a call to User B via a signaling server.
   - The signaling server negotiates connection details.
2. **Establishing Connection**:
   - ICE framework finds the best network path.
   - Secure media transport is established.
3. **Media Transmission**:
   - Audio and video data are compressed using codecs.
   - RTP transmits the media streams.
4. **Call Termination**:
   - Either user ends the call, sending a termination signal.
   - The server and clients close the connection.

## 3. Technologies Used:
- **WebRTC**: A peer-to-peer framework for browser and app-based RTC.
- **SIP (Session Initiation Protocol)**: Common in VoIP systems.
- **H.323**: Legacy standard for video conferencing.
- **TURN/STUN Servers**: Help bypass NAT/firewalls.

## 4. Challenges:
- **Latency and Jitter**: Managed via buffering and adaptive bitrate streaming.
- **Network Issues**: Handled using FEC (Forward Error Correction) and retransmissions.
- **Security**: End-to-end encryption (DTLS-SRTP) ensures privacy.

## 5. Real-World Implementations:
- **WhatsApp, Zoom, Google Meet** use WebRTC and custom signaling mechanisms.
- **Skype** uses a hybrid P2P and server-based model.
