---
title: 'Guides and Resources'
description: 'Guides, articles, tips/tricks and resources on customer engagement and related products and services.'
layout: default-post
---
{% for item in site.resources limit:1 %}
<div
  class="lg:flex block mt-20 justify-between items-start lg:px-24 px-8"
>
  <div class="lg:w-1/2 w-full">
    <img src="/images/resources/banners/{{item.banner}}" alt="" />
  </div>
  <div class="__note flex flex-col lg:mt-0 mt-8 lg:pl-12">
    <div class="mt-2">
      <h2
      >
        <a href="{{item.url}}"
        class="lg:text-4xl text-2xl font-semibold md:text-center lg:text-left __headline hover:opacity-80">
        {{item.title}}</a
        >
      </h2>
      <p
        class="text-base __text mt-4 md:text-center lg:text-left"
      >{{item.excerpt}}
      </p>
    </div>
    <div
      class="mt-8 flex items-center lg:justify-start md:justify-center"
    >
      <div class="">
        <img src="/images/authors/{{item.author_avi}}" class="rounded-full w-14" alt="" />
      </div>
      <div class="ml-3">
        <p class="text-sm font-semibold __name">{{item.author}}</p>
        <p class="text-xs __date">Posted: {{item.date | date: "%a, %b %d, %Y"}}</p>
      </div>
    </div>
  </div>
</div>
{% endfor %}

<!-- Blogs -->

<div
  class="lg:flex block items-start mt-24 lg:mx-16 mx-8"
>
  {% for item in site.resources offset:1 %}
  <div class="flex flex-col lg:w-1/3 w-full lg:mx-5 mt-8">
    <div
      class="__tags py-12"
      style="background:{{item.bg}}"
    >
      <img
        src="/images/resources/banners/{{item.banner}}"
        class="mx-auto __article"
        alt="{{item.title | escape}}"
      />
    </div>
    <div class="mt-4 lg:text-left md:text-center">
      <h3 class="lg:mt-3 mt-4"><a href="{{item.url}}" class="text-2xl font-semibold __name hover:opacity-80">{{item.title}}</a></h3>
      <p class="text-base __text lg:mt-3 mt-4">
        {{item.excerpt}}
      </p>
    </div>
    <div class="lg:mt-5 mb-8 lg:my-0 my-4 flex items-center lg:justify-start md:justify-center">
      <div class="">
        <img src="/images/authors/{{item.author_avi}}" class="rounded-full w-14" alt="" />
      </div>
      <div class="ml-3">
        <p class="text-sm font-semibold __name">{{item.author}}</p>
        <p class="text-xs __date">Posted: {{item.date | date: "%a, %b %d, %Y"}}</p>
      </div>
    </div>
  </div>
  {% endfor %}
</div>
