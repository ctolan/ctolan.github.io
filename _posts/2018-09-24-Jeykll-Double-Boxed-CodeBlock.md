---
layout: post
title:  "Jeykll Double Boxed Codeblock - GitHub Pages"
date:   2018-09-24 09:56:31 +0100
tags: Jeykll-blog
---

Short one today, I spent a bit of time trying to solve a minor problem with my markdown and I learned a bit along the way. I am still getting to know Markdown and that there are in fact many flavours of it not all supported everywhere.

![Boxed Code Block image]({{ site.url }}/images/DoubleBoxedQuotes.PNG)

This makes sense, since Jeykll open source it is implemented and implements other open source projects and they may not all play well together all the time.

My problem was that where I used the PowerShell code blocks it showed up in a double box. Not the end of the world I didn't hold off publishing anything due to this egregious error. As best I understand it now from looking at the page source and some issues on GitHub the problem is here:

```html
<div class="language-powershell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
```

The two divs are creating the nested divs seen above.
The fix I followed is in [this PR]( https://github.com/saveriomiroddi/saveriomiroddi.github.io/pull/18/files) and it simply changes the name of .highlight to pre.highlight in **_sass/_highlights.scss**

```css
- .highlight {
+ pre.highlight {
```

This worked for me I hope if helps you.
What else did I learn, you can obviously use Jeykll with GitHub Pages but you are limited in what parser you can use, [the documentation]( https://github.com/planetjekyll/quickrefs/blob/master/FAQ.md#github-pages) advises using the Github-Flavored Markdown, in fact as I go to get the code to quote from my **_config.yml** I see that (__if this is still correct__), GitHub Pages now only supports rouge for syntax highlighting.

```powershell
# Jekyll 3 now only supports Kramdown for Markdown
kramdown:
  # Use GitHub flavored markdown, including triple backtick fenced code blocks
  input: GFM
  # Jekyll 3 and GitHub Pages now only support rouge for syntax highlighting
  syntax_highlighter: rouge
  syntax_highlighter_opts:
    # Use existing pygments syntax highlighting css
    css_class: 'highlight'
```

Now this might seem trivial but it get complicated when you are using local Jeykll or Markdown tools and everything looks fine, then you push to GitHub and it looks screwed. Either way, a little digging on the internet and you'll find your answers. I hope this posts properly. To see, you just need to check the number of commits it took me to get [this page](https://github.com/ctolan/ctolan.github.io/blob/master/_posts/2018-09-24-Jeykll-Double-Boxed-CodeBlock.md) committed.

Thanks for reading.

Conor