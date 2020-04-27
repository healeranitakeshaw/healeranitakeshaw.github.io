<div class="w3-card w3-padding-24 paddingbottom32">
  <div class="w3-xxlarge">Latest Video</div><br>
  <div class="w3-large fontgrey" style='max-width: 570px;'>
    <div class='iframecontainer'><iframe id="latestvideo" width="800" height="600" frameborder="0" allowfullscreen></iframe></div>
    <div id='latestvideotitle'></div>
    <br>
    <a href="https://www.youtube.com/channel/UCb1gNzGJqls5borB6EApcDg/videos">More videos</a>
    <script>
      // source: https://codegena.com/auto-embed-latest-video-youtube-channel/
      // https://api.rss2json.com/v1/api.json?rss_url=https://www.youtube.com/feeds/videos.xml?channel_id=UCb1gNzGJqls5borB6EApcDg
      window.onload = function() {
        var channelid = 'UCb1gNzGJqls5borB6EApcDg';
        var channelfeed = encodeURIComponent("https://www.youtube.com/feeds/videos.xml?channel_id=" + channelid)
        var channeljson = 'https://api.rss2json.com/v1/api.json?rss_url=' + channelfeed;
        $.getJSON(channeljson,
          function(data) {
            var videolink = data.items[0].link;
            var embedlink = videolink.replace('watch?v=', 'embed/')
            var iframe = document.getElementById('latestvideo');
            iframe.setAttribute('src', embedlink);
            var latestvideotitle = document.getElementById('latestvideotitle');
            latestvideotitle.innerHTML = data.items[0].title;
          }
        );
      }
    </script>
  </div>
</div>