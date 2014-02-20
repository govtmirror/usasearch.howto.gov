---
permalink: /blog/legacy-domains.html
layout: post
title: "Six legacy domains are expiring"
tags: get-code
---

As part of the federal [.gov web reform](http://www.usa.gov/WebReform.shtml) project, we're eliminating six of our legacy domains. Going forward, our only supported domain is search.usa.gov (or search.yoursite.gov, if you've requested [DNS masking](/sites/manual/cname.html)).
What do you need to do? If your URL starts with any of the following six legacy domains, you must update your HTML form code.

1. firstgovsearch.gov
2. searchusa.gov
3. usasearch.gov
4. (Spanish) buscador.gov
5. (Spanish) buscadorusa.gov
6. (Spanish) usabuscador.gov

Specifically, you have to update the action of your [form code](/sites/manual/code.html) to call search.usa.gov (or search.yoursite.gov).

`<form method="get" action="http://search.usa.gov/search">`

Note that, if you don't update your form code, your search results page will no longer work.