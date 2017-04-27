---
layout: post
title: "Nearly Table-Free Emails"
date: 2017-04-06
category: posts
permalink: /blog/nearly-table-free-emails
excerpt: ""
---
![table free emails](/assets/img/nearly-table-free.png)

After taking a few months off, I’ve restarted [my email newsletter](/newsletter). *The Intermittent Newsletter*, as it’s called (primarily because I’m lazy and won’t commit to sending on a regular schedule), delivers my latest writing and interesting links I’ve found around the web straight to your inbox. It’s a simple email, following a similar design to this site, but is one of my favorite templates I’ve ever built. Here’s why:

*It is a nearly table-free email.*

Table-free emails have been the holy grail of email design for a long time. Anyone that’s dealt with HTML email knows the pain that comes with relying on tables for building campaigns. While it’d be nice to move to divs or HTML5 sectioning elements in HTML emails, most people can’t—solely due to the fact that most versions of  Microsoft Outlook don’t support positioning and layout CSS rules.

While it's not quite completely table-free, I’ve managed to get *The Intermittent Newsletter* down to a single table—one that’s not even visible to non-Microsoft email clients. Along the way, I made an effort to make The Intermittent Newsletter accessible to more readers.

Here’s how.

## Dropping Tables

*The Intermittent Newsletter* is a simple email. It’s a single column and only has one image. I like all-text emails and simple designs, so things worked out well. All of the content in the email is contained within a single `div` element, which is used to set default styles on the text within.

```
<body style="margin: 0 !important; padding: 0 !important;">
  <div style="background-color: #ffffff; color: #001b44; font-family: -apple-system, BlinkMacSystemFont, 'avenir next', avenir, helvetica, 'helvetica neue', ubuntu, roboto, noto, 'segoe ui', arial, sans-serif; font-size: 18px; line-height: 32px; margin: 0 auto; max-width: 720px; padding: 40px 20px 40px 20px;">

  <!-- CONTENT GOES HERE -->

  </div>
</body>
```

You can see that I use the `max-width` property on that `div` to ensure that the content doesn’t stretch wider than 720 pixels. For most email clients, this works a treat. But, like I mentioned before, Outlook sucks at layout and positioning and doesn’t render the `max-width` property on that `div`. Here’s where the single table comes into play.

For Outlook, I take advantage of MSO conditional tables to add in a simple table that constrains the content to 720 pixels.

```
<body style="margin: 0 !important; padding: 0 !important;">
  <!--[if (gte mso 9)|(IE)]>
  <table cellspacing="0" cellpadding="0" border="0" width="720" align="center" role="presentation"><tr><td>
  <![endif]—>
  <div style="background-color: #ffffff; color: #001b44; font-family: -apple-system, BlinkMacSystemFont, 'avenir next', avenir, helvetica, 'helvetica neue', ubuntu, roboto, noto, 'segoe ui', arial, sans-serif; font-size: 18px; line-height: 32px; margin: 0 auto; max-width: 720px; padding: 40px 20px 40px 20px;">

  <!-- CONTENT GOES HERE -->

  </div>
  <!--[if (gte mso 9)|(IE)]>
  </td></tr></table>
  <![endif]-->
</body>
```

Now, my content is properly displayed across all email clients. With a single table and nothing but a `div`.

## Making Things Accessible

I’m increasingly concerned about accessibility, both on the web and within email. To make sure *The Intermittent Newsletter* is as accessible as possible, I’ve ditched the old **td or GTFO** method for structuring and styling copy and used semantic elements, instead. All of my copy is marked up using proper heading and paragraph elements.

```
<h1 style="color: #357edd; font-size: 24px; font-weight: normal; line-height: 28px; margin: 40px 0px 100px 0px; text-align: center;">
  The Intermittent Newsletter<span style="color: #ffb700; font-size: 16px;">by Jason Rodriguez</span>
</h1>
<h2 style="font-size: 24px; line-height: 28px; margin: 60px 0px 40px 0px; text-align: center;">
  So, it's been a while&hellip;
</h2>
<p style="margin-bottom: 20px;">
  &hellip; but I’m finally back to sending my newsletter. If you forgot who the hell I am or are shaking your head wondering why you’re receiving this, here’s a little bit of context:
</p>
```

While the default styles on the `div` control the styling of most of the email, I do rely on specific inline styles on headings and paragraphs (and the footer copy) to adjust some of those styles. Primarily `font-size`, `line-height`, and `margin` are used to make the copy look nice.

To further aid accessibility, I’ve ensured that screen readers working in Microsoft Outlook ignore that table and only read the content of the email by using the `role="presentation"` attribute on that table element. [Tip of the hat](http://blog.rebelmail.com/accessibility-in-email-part-ii/) to Mark Robbins for recommending that approach.

## It’s a Start

So far, I’m really happy with how this template has worked out. It’s kind of like the [hybrid coding approach](http://labs.actionrocket.co/the-hybrid-coding-approach) that’s been in use for a while, but the light-weight version. With just dummy content (heading, couple of paragraphs, and the footer), my code comes in at **81 lines**. It’s absurdly easy to maintain and update. So easy that I didn’t even bother creating a templatized (is that a word?) version for Campaign Monitor, my ESP of choice.

This is an approach I would definitely recommend to others that are sending simple, stationary-like email campaigns. I fully understand that it won’t work for everything (multiple columns and complex layouts don’t lend themselves to this approach), but when it works, it works well.

I’m backing everything up over on GitHub, so you can [check out the code](https://github.com/rodriguezcommaj/the-intermittent-newsletter) there.
