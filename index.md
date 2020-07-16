---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
github: https://github.com/PinheiroCosta
---

{%- assign loop = site.data.author.qualities -%}

<div class="intro">
    <div class="intro-content">
        <h1>Hi, I'm Rômulo.</h1>
        <p>
        I'm a 
        <span class="cursor-write emphasis">
        {{ loop[-1] }}
        </span>
        . You may find some of my work on <a href="{{ page.github }}" target="#_blank">GitHub</a>. Feel free to contact me If you're looking for <a href="{{ baseurl }}/help/">Help</a>.<span class="cursor-blink">&nbsp;&nbsp;</span>
        </p>
    </div>
</div>

