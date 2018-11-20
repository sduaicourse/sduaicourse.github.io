---
layout: publications
title: 项目展示
description: 
keywords: 3D Increment Introduction
comments: true
menu: 成果
permalink: /publications/
---

{% assign number_printed = 0 %}
{% for publi in site.data.publist %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if publi.highlight == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">

 <div class="thumbnail">
		<div class="caption">
				<h5>{{ publi.title }}</h5>
		<img src="{{ site.url }}{{ site.baseurl }}/images/pubpic/{{ publi.image }}" class="img-responsive" witdh="20%"/>
		
			<p>{{ publi.description }}</p>
			<p><em>{{ publi.authors }}</em></p>
			<p><strong><a href="{{ site.url }}{{ site.baseurl }}/member/{{ publi.link.member }}">{{ publi.link.display }}</a></strong></p>
			<p class="text-danger"><strong> {{ publi.news1 }}</strong></p>
			<p> {{ publi.news2 }}</p>
		</div>
    </div>
 

</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}
<div class="row">
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>


