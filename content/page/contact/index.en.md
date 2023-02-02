---
title: "Contact"
excludeFromTopNav: false
showDate: false
showComments: false
readingTime: 0
---

<form action="https://formspree.io/f/myyvjzzp" method="post">
    <div>
        <label for="name">Full Name</label>
        <input type="text" id="name" name="name" required="">
    </div>
    <div>
        <label for="email">Email</label>
        <input type="email" id="email" name="email" required="">
    </div>
    <div>
        <label for="subject">Subject</label>
        <input type="text" id="subject" name="subject" required="">
    </div>
    <div>
        <label for="message">Message</label>
        <textarea id="message" rows="4" name="message" required=""></textarea>
    </div>
    <button type="submit" aria-label="Send Message">
        Send Now
    </button>
</form>
<style>
  form {
    display: grid;
    grid-template-columns: max-content 1fr;
    grid-gap: 1rem;
    text-align: left;
    padding: 2rem 0;
    margin: 0;
  }
</style>
