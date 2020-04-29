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
<style>
#scroll_button {
    display: none;
    position: relative;
    cursor: pointer;
    background-color: #fff;
    background-clip: padding-box;
    border: 2px solid rgba(27,31,35,.15);
    border-radius: 64px;
    box-shadow: 0 1px 15px rgba(27,31,35,.15);
    width: 48px;
    height: 48px;
    text-align: center;
    color: #b15fb3;
}
#scroll_button:hover {
    color: #b15fb3;
}
.fa {
  margin: 6px !important;
}
</style>
<div id="page_rightpanel">
  <div onclick="scrollToTop()" id="scroll_button" title="Scroll to top"><i class="fa fa-chevron-up"></i></div>
</div>