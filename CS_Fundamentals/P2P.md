# P2P

## ORTC

Microsoft supported object real time connection focused on expert developers

## RTC

Google supported standard for easy p2p communication that can then scale to use an intermediate server for > 4

Handles everything from stabilization, codecs, etc for ez use and multi platform including many browsers and matching native performance

Beyond about 3/4, probably need a server to communicate because all the devices will connect and send data to every other device

Need signal server to let the peers communicate session data to begin connection

Need a hosted STUN / TURN server to handle fallback when because of NAT or other, the p2p connection fails

##### Interface

MediaStreams

P2P Connections

