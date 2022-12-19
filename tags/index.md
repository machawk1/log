---
layout: page
title: Tags
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
<!-- site_tags: {{ site_tags }} -->
{% assign tag_words = site_tags | split:',' | sort %}
<!-- tag_words: {{ tag_words }} -->

<div id="tags">
  <!--<ul class="tag-box inline">
  {% for tag in tag_words %}
    <li><a href="#{{ tag | slugify }}-ref">{{ tag | replace: '-', ' ' }} <span>{{ site.tags[tag] | size }}</span></a></li>
  {% endfor %}
  </ul>-->

  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
  <h2 id="{{ this_word | slugify }}-ref">{{ this_word | replace: '-', ' ' }}</h2>
  <ul class="posts">
    {% for post in site.tags[this_word] %}{% if post.title != null %}
    <li itemscope>
        <a href="{{ post.url }}">{{ post.title }}</a>
           <span class="entry-date">
              <time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">
                ({{ post.date | date: "%B %d, %Y" }})
              </time>
          </span> 
       </li>
    {% endif %}{% endfor %}
  </ul>
  {% endunless %}{% endfor %}
</div>