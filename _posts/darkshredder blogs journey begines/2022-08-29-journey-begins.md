---
layout: post
title:  "journey begins"
date:   2022-08-16 03:29:20 +05:30
categories: darkshredder blogs journey begins
---

# The Idea
So it all started when I was just scrolling through Hacker News and saw this [post](https://news.ycombinator.com/item?id=23094876) by Alex West. How he manages his own [website](https://www.alexwest.co/) and documents about his journey and learning of launching products and reporting how much monthly recurring revenue (MRR) they make. It's a really great read.

What struck me was his clean, fast website that presented information in an easy to read way. I also admired his writing style. Therefore, I decided to build a micro website of my own.

# The Setup

The following elements are used here :

- [Name.com](https://www.name.com/) as a domain registrar.
- [Cloudflare](https://www.cloudflare.com/) as a DNS provider.
- [Netlify](https://www.netlify.com/) as a static site hosting provider.
- [Google Analytics](https://analytics.google.com/) as a tracking provider.
- [Jekyll](https://jekyllrb.com/) as a static site generator.

Got the domain for free right now through GitHub Education Pack for a year. Setting up CI/CD pipeline on Netlify was really easy, just needed to add Repository as a new site and it got deployed automatically :tada:.

For the custom domain, I used Cloudflare to add a  `@ A record` and a `www CNAME 'custom-netlify-domain'` as suggested by Netlify and the website was live along with Let's Encrypt certificate! 

# Monetization

Currently, this website is operating at a free cost. But after next year will be operating at a $45 loss year on year from domain renewal. This amount could increase if I have to pay for hosting in the future.


# Conclusion

The website is live now! I'm excited to keep going with this journey.

Follow my progress: [darkshredder.codes](https://darkshredder.codes/)