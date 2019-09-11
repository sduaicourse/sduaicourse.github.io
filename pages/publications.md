---
layout: publications
title: 项目展示
description: 历年项目成果
keywords: project
comments: false
permalink: /publications/
---

{% assign number_printed = 0 %}
{% for publi in site.publications %}
{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">

 <div class="thumbnail">
		<div class="caption">
				<h4>{{publi.title }}</h4>
		<img src="{{publi.image }}" class="img-responsive" witdh="20%"/>
		<br>
			<p>{{publi.description }}</p>
			<p><strong><a href="{{ site.url }}{{ publi.url }}">详细信息</a></strong></p>
		</div>
    </div>
 

</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}
<div class="row">
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

