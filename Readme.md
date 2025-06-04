**manifest.json**

    {
      "name": "App-Web",
      "start_url": "/",
      "display": "standalone",
      "background_color": "#ffffff",
      "theme_color": "#0d6efd",
      "icons": [
        {
          "src": "asset/icons/icon-192x192.png",
          "sizes": "192x192",
          "type": "image/png"
        },
        {
          "src": "asset/icons/icon-512x512.png",
          "sizes": "512x512",
          "type": "image/png"
        }
      ]
    }

**sw.js**

    // Enable immediately after installation
    self.addEventListener('install', () => {
        self.skipWaiting();
    });
    
    // Take over immediately after enabling
    self.addEventListener('activate', () => {
        clients.claim();
    });
    
    self.addEventListener('fetch', (event) => {
        if (event.request.method !== 'GET') return;
        event.respondWith(fetch(event.request));
    });

**Html Page**

    <head>
	    <link rel="manifest" href="asset/pwa/manifest.json" />
    </head>
    
	<script>try{"serviceWorker"in navigator&&navigator.serviceWorker.register("asset/pwa/sw.js");}catch(r){console.log("Init PWA Errro: "+r.message);}</script>
