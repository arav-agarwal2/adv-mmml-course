---
layout: schedule
permalink: /spring2022/schedule/
title: Schedule
---

** Exact topics and schedule subject to change, based on student interests and course discussions. **

{% assign current_module = 0 %}
{% assign skip_classes = 0 %}
{% assign prev_date = 0 %}

{% for item in site.data.lectures %}
{% if item.date %}
{% assign lecture = item %}
{% assign event_type = "upcoming" %}
{% assign today_date = "now" | date: "%s" | divided_by: 86400 %}
{% assign lecture_date = lecture.date | date: "%s" | divided_by: 86400 %}
{% if today_date > lecture_date %}
    {% assign event_type = "past" %}
{% elsif today_date <= lecture_date and today_date > prev_date %}
    {% assign event_type = "warning" %}
{% endif %}
{% assign prev_date = lecture_date %}

<tr class="{{ event_type }}">
    <th scope="row">{{ lecture.date }}</th>
    {% if lecture.title contains 'lectures' %}
    {% assign skip_classes = skip_classes | plus: 1 %}
    <td colspan="4">{{ lecture.title }}</td>
    {% else %}
    <td>
        <h2>{{ lecture.title }}<h2> <br/>
            <ul>
                {% for topic in lecture.topics %}
                <li style="font-size:10px;">
                {topic}
                </li>
                {% endfor %}
            </ul>
    </td>
    <td>
        {{ lecture.readings }}
    </td>
    {% endif %}
</tr>
{% else %}
{% assign current_module = current_module | plus: 1 %}
{% assign module = item %}
<tr class="info">
    <td colspan="5" align="center"><strong>{{ module.title }}</strong></td>
</tr>
{% endif %}
{% endfor %}
