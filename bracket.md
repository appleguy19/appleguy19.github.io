---
layout: page
title: Embedded Bracket
---

<div id="brackify-iframe-wrap" style="position:relative;">
<iframe style="position:absolute; width:1px; min-width:100%; height:100%;" id="brackify-iframe" height="2350" scrolling="no" frameborder="0" src="https://brackify.com/b/36768/Best-Sports-Movies"></iframe>
</div>
<script type="text/javascript">
var eventMethod = window.addEventListener ? "addEventListener" : "attachEvent";
var messageEvent = eventMethod == "attachEvent" ? "onmessage" : "message";
window[eventMethod](messageEvent, function(e) {
  if (e.origin != "https://brackify.com") { return;}
  var iframeWrap = document.getElementById("brackify-iframe-wrap");
  if (iframeWrap) {
    if (e.data["scroll"]) {
      var bodyRect = document.body.getBoundingClientRect();
      var elemRect = iframeWrap.getBoundingClientRect();
      var offset = elemRect.top - bodyRect.top + e.data["scroll"];
      window.scrollTo(0, offset);
    }
    if (e.data["bracket-completed"]) {
      if (window.brackifyBracketCompletedHandler) {  window.brackifyBracketCompletedHandler() }
    }
    if (e.data["resize"]) { iframeWrap.style.height = (parseInt(e.data["resize"])) + "px"; }
  }
}, false);
</script>
