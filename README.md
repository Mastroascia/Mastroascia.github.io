<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Camera Stream - Sender</title>
</head>
<body>
    <h1>Camera Stream - Sender</h1>
    <p>Invio del video della fotocamera...</p>

    <script>
        let peerConnection;
        const config = {
            'iceServers': [{ 'urls': 'stun:stun.l.google.com:19302' }]
        };

        // Funzione per accedere alla fotocamera
        async function startStream() {
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });

            // Crea connessione WebRTC
            peerConnection = new RTCPeerConnection(config);

            // Aggiungi lo stream video alla connessione
            stream.getTracks().forEach(track => peerConnection.addTrack(track, stream));

            // Crea offerta SDP
            const offer = await peerConnection.createOffer();
            await peerConnection.setLocalDescription(offer);

            // Mostra l'offerta SDP al ricevitore (sul PC)
            console.log("Offerta SDP per il ricevitore:", offer.sdp);

            // Invia l'offerta al ricevitore (implementazione tramite server di segnalazione necessario)
        }

        // Avvia il flusso
        startStream();
    </script>
</body>
</html>v
