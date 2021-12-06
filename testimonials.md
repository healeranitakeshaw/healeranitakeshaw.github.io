<style>
textarea, input {
  margin-top: 5px;
  margin-bottom: 10px;
  width: 98%;
  max-width: 570px;
}
textarea, button, input {
  font-size: 16px;
}
button {
  margin: 10px;
}
textarea {
  resize: vertical;
}
#testimonialform {
  display: none;
}
button {
  background: linear-gradient(to bottom,#f7dfa5,#f0c14b);
  border-radius: 4px;
  border: solid lightgrey 1.3px;
  padding: 6px 12px;
  cursor: pointer;
}
button:-moz-focusring {
  outline: none;
}
hr:last-child {
  display: none;
}
.fa {
  margin-left: -12px;
  margin-right: 8px;
}
#submitbutton {
  padding: 6px 24px;
}
form label {
  display: block;
  margin-top: 10px;
}
</style>
<div class="w3-card w3-padding-24">
  <div class="w3-xxlarge">Testimonials</div><br>
  <div class="w3-large fontgrey" style="font-size:15px!important;text-align:justify">
  {% assign testimonials = site.data.testimonials | sort: date %}
  {% for testimonial in testimonials reversed %}
    {% assign name = testimonial[1].name %}
    {% assign date = testimonial[1].date %}
    {% assign message = testimonial[1].message %}
    {% assign accountlink = testimonial[1].accountlink %}
    {{ message }}
    <br>
    <div style="font-size: 14px"><a href="{{ accountlink }}">{{ name }}</a> ~ {{ date | date: '%a %-d %b %Y' }}</div>
    <!--{{ date | date: '%a %-d %b %Y @%H:%M' }}-->
    <hr>
  {% endfor %}
  </div><br>
</div>
<br>
<script>
  function toggle_formvisibility() {
    var btn = document.getElementById("btn-toggle");
    var form = document.getElementById("testimonialform");
    if (form.style.display === "block") {
      form.style.display = "none";
      btn.innerText = "Write Testimonial";
    } else {
      form.style.display = "block";
      btn.innerText = "Hide Testimonial Form";
    }
  }
</script>
<script>
(function ($) {
  $('form').submit(function () {
    var form = this;
    $(form).addClass('disabled');
    $("#submitbutton").css({"padding":"6px 24px"});
    var submitbutton = document.getElementById("submitbutton");
    submitbutton.innerHTML = '<i class="fa fa-spinner fa-spin"></i>Loading...';
    $('form .js-notice').removeClass('w3-pale-green').removeClass('w3-pale-red').addClass('w3-pale-yellow');
    showAlert('Please wait for some seconds...');
    $.ajax({
      type: $(this).attr('method'),
      url: $(this).attr('action'),
      data: $(this).serialize(),
      contentType: 'application/x-www-form-urlencoded',
      success: function (data) {
        $('#submitbutton').html('Submitted');
        $('form .js-notice').removeClass('w3-pale-yellow').removeClass('w3-pale-red').addClass('w3-pale-green');
        showAlert('<strong>Thank you for your testimonial.</strong> Once it has been checked it will appear here.');
        submitbutton.disabled = true;
        submitbutton.style.cursor = 'not-allowed';
        submitbutton.style.opacity = '0.66';
      },
      error: function (err) {
        console.log(err);
        $('#submitbutton').html('Submit Testimonial');
        $('form .js-notice').removeClass('w3-pale-yellow').removeClass('w3-pale-green').addClass('w3-pale-red');
        showAlert('<strong>There was an error with your submission.</strong> Please make sure you filled all required fields and try again.');
        $(form).removeClass('disabled');
      }
    });
    return false;
  });
  function showAlert(message) {
    $('form .js-notice').removeClass('hidden');
    $('form .js-notice-text').html(message);
  }
})(jQuery);
</script>