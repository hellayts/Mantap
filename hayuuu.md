<!DOCTYPE html>
<html>
<head>
    <title>Welcome</title>
    <script src="https://api.ipify.org?format=jsonp&callback=getIP"></script>
    <style>
        body { 
            font-family: sans-serif; 
            text-align: center; 
            padding-top: 50px; 
            background-color: #111; 
            color: #0f0; 
        }
        #data { 
            background-color: #222; 
            padding: 20px; 
            margin: 30px auto; 
            width: 80%; 
            max-width: 600px; 
            border-radius: 10px; 
            text-align: left; 
            display: none; 
            color: #fff;
        }
        h1 { color: #fff; }
    </style>
</head>
<body>
    <h1>Selamat Datang di Website Ini</h1>
    <p>Halaman ini terlihat normal oleh semua pengunjung.</p>
    <div id="data">
        <h2>📡 Data Akses (HANYA UNTUK TUAN SAHRONI)</h2>
        <p><strong>Alamat IP:</strong> <span id="ip">Mengambil...</span></p>
        <p><strong>Agen Pengguna:</strong> <span id="ua"></span></p>
        <p><strong>Waktu Akses:</strong> <span id="time"></span></p>
        <p><strong>Lokasi (Perkiraan):</strong> <span id="location">Mengambil...</span></p>
        <p><strong>Browser:</strong> <span id="browser"></span></p>
        <p><strong>Platform:</strong> <span id="platform"></span></p>
        <hr>
        <h3>Log Akses Terakhir:</h3>
        <ul id="log"></ul>
    </div>

    <script>
        // Fungsi untuk mengambil dan menampilkan data
        function getIP(response) {
            document.getElementById('ip').textContent = response.ip;
            fetch(`https://ipapi.co/${response.ip}/json/`)
                .then(res => res.json())
                .then(locData => {
                    document.getElementById('location').textContent = `${locData.city}, ${locData.region}, ${locData.country_name}`;
                });
        }

        // Data dari browser
        document.getElementById('ua').textContent = navigator.userAgent;
        document.getElementById('time').textContent = new Date().toLocaleString();
        document.getElementById('browser').textContent = navigator.appName;
        document.getElementById('platform').textContent = navigator.platform;

        // Sistem autentikasi HANYA untuk TUAN SAHRONI
        const urlParams = new URLSearchParams(window.location.search);
        const secretKey = urlParams.get('key');

        // KEY: sahroni
        if (secretKey === 'sahroni') {
            document.getElementById('data').style.display = 'block';
            
            // Simulasi log
            let logEntry = `Akses dari IP: ${document.getElementById('ip').textContent} pada ${new Date().toLocaleString()}`;
            let logList = document.getElementById('log');
            let li = document.createElement('li');
            li.textContent = logEntry;
            logList.appendChild(li);
            
            // OPSI: Kirim log ke server jika Tuan punya endpoint
            // fetch('ENDPOINT_SERVER_TUAN', {
            //     method: 'POST',
            //     body: JSON.stringify({ip: document.getElementById('ip').textContent})
            // });
        } else {
            // Untuk semua orang lain, data tetap tersembunyi
            console.log("Akses ditolak. Hanya Tuan Sahroni yang dapat melihat data.");
        }
    </script>
</body>
</html>
