---
title: "Contact"
permalink: "/contact.html"
---

<form action="https://api.staticforms.xyz/submit" method="post">
<input type="hidden" name="accessKey" value="ddac2390-00d8-42e4-800e-d0a2f3eab568">  
<p class="mb-4">Please send your message to {{site.name}}. We will reply as soon as possible!</p>
<div class="form-group row">
<div class="col-md-6">
<input class="form-control" type="text" name="name" placeholder="Name*" required>
</div>
<div class="col-md-6">
<input class="form-control" type="email" name="_replyto" placeholder="E-mail Address*" required>
</div>
</div>
<textarea rows="8" class="form-control mb-3" name="message" placeholder="Message*" required></textarea>    
<input type="hidden" name="redirectTo" value="https://souhazra.github.io/welcome-to-learn-with-souren">
<input class="btn btn-success" type="submit" value="Send">
</form>