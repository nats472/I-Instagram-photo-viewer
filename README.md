# I-Instagram-photo-viewer
Index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>My Instagram Feed</title>
  <style>
    body { font-family: Arial; text-align: center; }
    .photo-grid { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; }
    .photo-grid img { width: 200px; border-radius: 10px; }
  </style>
</head>
<body>
  <h1>📷 My Instagram Feed</h1>
  <div class="photo-grid" id="insta-feed"></div>

  <script>
    const token = 'YOUR_ACCESS_TOKEN_HERE';
    const fields = 'media_url,caption,permalink';
    const limit = 6;

    fetch(`https://graph.instagram.com/me/media?fields=${fields}&access_token=${token}&limit=${limit}`)
      .then(res => res.json())
      .then(data => {
        const feed = document.getElementById('insta-feed');
        data.data.forEach(post => {
          const img = document.createElement('img');
          img.src = post.media_url;
          img.alt = post.caption || '';
          img.onclick = () => window.open(post.permalink, '_blank');
          feed.appendChild(img);
        });
      });
  </script>
</body>
</html>
