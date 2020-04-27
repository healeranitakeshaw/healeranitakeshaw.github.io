<style>
textarea, input {
  width: 98%;
}
textarea, button, input {
  font-size: 16px;
}
textarea {
  max-width: 570px;
  resize: vertical;
}
input {
  max-width: 350px;
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
#hr:last-child {
  display: none;
}
.fa {
  margin-left: -12px;
  margin-right: 8px;
}
#submitbutton {
  padding: 6px 24px;
}
fieldset {
  border: 0px;
}
</style>
<div class="w3-card w3-padding-24">
  <div class="w3-xxlarge">Testimonials</div><br>
  <div class="w3-large fontgrey">
  {% assign testimonials = site.data.testimonials | sort: date %}
  {% for testimonial in testimonials reversed %}
    {% assign name = testimonial[1].name %}
    {% assign date = testimonial[1].date %}
    {% assign message = testimonial[1].message %}
    {{ message }}
    <br>
    <div style="font-size: 14px">{{ name }} ~ {{ date | date: '%a %-d %b %Y' }}</div>
    <!--{{ date | date: '%a %-d %b %Y @%H:%M' }}-->
    <hr>
  {% endfor %}
  </div>
  <br>
  <button id="btn-toggle" onclick="toggle_formvisibility()">Write Testimonial</button>
  <div class="w3-large fontgrey" id="testimonialform">
    <form method="post" action="https://staticmaninstance.herokuapp.com/v2/entry/healeranitakeshaw/healeranitakeshaw.github.io/master/testimonials">
    <!--<input name="options[redirect]" type="hidden" value="https://healeranitakeshaw.com/">-->
    <br>
    <label>Testimonial<br><textarea id="message" name="fields[message]" rows="5"></textarea></label><br>
    <br>
    <label>Name<br><input type="text" id="name" name="fields[name]"></label><br>
    <div class="hidden js-notice w3-panel" style="margin: 16px; padding: 8px; font-size: 16px; display: inline-block; max-width: 570px">
      <span class="js-notice-text"></span>
    </div>
    <fieldset><button id="submitbutton" type="submit">Submit Testimonial</button></fieldset>
    </form>
  </div>
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
        showAlert('<strong>Thank you for your testimonial.</strong> It will show on the site in some minutes.');
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