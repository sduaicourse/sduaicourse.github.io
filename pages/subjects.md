---
layout: publications
title: 课题列表
description: 
keywords: 3D Increment Introduction
comments: false
permalink: /subjects/
---

{% assign number_printed = 0 %}
{% forsubject in site.subjects %}
{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">

 <div class="thumbnail">
		<div class="caption">
				<h5>{{subject.title }}</h5>
		
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