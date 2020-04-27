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
    <br>
    <button type="submit">Submit Testimonial</button>
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