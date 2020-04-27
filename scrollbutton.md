<script>
  // source: https://www.w3schools.com/howto/tryit.asp?filename=tryhow_js_scroll_to_top
  window.onscroll = function() {
    var scroll_button = document.getElementById("scroll_button");
    if (document.body.scrollTop > screen.height / 11 || document.documentElement.scrollTop > screen.height / 11) {
      scroll_button.style.display = "block";
    } else {
      scroll_button.style.display = "none";
    }
  };
  function scrollToTop() {
    document.body.scrollTop = 0;
    document.documentElement.scrollTop = 0;
  }
</script>
<div id="page_rightpanel">
  <div onclick="scrollToTop()" id="scroll_button" title="Scroll to top"><i class="fa fa-chevron-up"></i></div>
</div>