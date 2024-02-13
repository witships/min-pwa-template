# pwa ミニマム

- sw.js を用意
  ```jsx
  // 中身の無いserviceWorker
  self.addEventListener("fetch", function (event) {})
  ```
- manifest.webmanifest を用意
  ```json
  {
    "name": "Hello PWA", // アプリ名
    "short_name": "Hello", // アプリ名
    "start_url": ".",
    "display": "standalone", // windowのモード:standalone=ヘッダーメニューなし
    "background_color": "#4E526F",
    "theme_color": "#4E526F",
    "icons": [
      // iconは192と512の２つ用意を推奨
      {
        "src": "images/icons-192.png",
        "sizes": "192x192",
        "type": "image/png"
      },
      {
        "src": "images/icons-512.png",
        "sizes": "512x512",
        "type": "image/png"
      }
    ]
  }
  ```
- index.html で呼び出し
  ```html
  <!DOCTYPE html>
  <html lang="ja">
    <head>
      <meta charset="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1" />
      <link rel="icon" href="./images/icon192.png" />
      <title>Hello PWA</title>
      　　
      <!-- manifest -->
      <link rel="manifest" href="manifest.webmanifest" />
    </head>
    <body>
      <h1>Hello PWA</h1>
      <!-- ここからserviceWorker -->
      <script>
        window.addEventListener("load", () => {
          if ("serviceWorker" in navigator) {
            navigator.serviceWorker
              .register("sw.js")
              .then((registration) => console.log("registered", registration))
              .catch((error) => console.log("error", error))
          }
        })
      </script>
      <!-- ここまで -->
    </body>
  </html>
  ```
