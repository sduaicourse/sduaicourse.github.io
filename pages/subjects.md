---
layout: publications
title: 课题列表
description: 
keywords: 3D Increment Introduction
comments: false
permalink: /subjects/
---

{% assign number_printed = 0 %}
{% for subject in site.subjects %}
{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">

 <div class="thumbnail">
		<div class="caption">
				<h4>{{subject.title }}</h4>
		<img src="{{subject.image }}" class="img-responsive" witdh="20%"/>
		<br>
			<p>{{subject.description }}</p>
			<p><strong><a href="{{ site.url }}{{ subject.url }}">详细信息</a></strong></p>
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