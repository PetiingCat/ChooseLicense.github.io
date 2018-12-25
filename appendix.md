---
layout: default
permalink: /appendix/
title: 附錄
class: license-types
---

你可以在下面表格中檢視所有授權資訊，也可以到 [ChooseLicense](https://github.com/ChooseLicense/ChooseLicense.github.io) 檢視網站源碼，協助我們完善這個網站。

如果你想選擇一個許可授權 **[建議從首頁開始選擇](/)**，首頁會為你推薦適合你的許可授權。

<table border style="font-size: xx-small">
{% assign types = "permissions|conditions|limitations" | split: "|" %}
<tr>
  <th scope="col" style="text-align: center">開源授權</th>
  {% assign seen_tags = '' %}
  {% for type in types %}
    {% assign rules = site.data.rules[type] | sort: "label" %}
    {% for rule_obj in rules %}
      {% if seen_tags contains rule_obj.tag %}
        {% continue %}
      {% endif %}
      {% capture seen_tags %}{{ seen_tags | append:rule_obj.tag }}{% endcapture %}
      <th scope="col" style="text-align: center; width:7%"><a href="#{{ rule_obj.tag }}">
      {% if rule_obj.label == 'Commercial Use' %}
        商業用途
      {% elsif rule_obj.label == 'Distribution' %}
        分發
      {% elsif rule_obj.label == 'Modification' %}
        修改
      {% elsif rule_obj.label == 'Patent Use' %}
        專利授權
      {% elsif rule_obj.label == 'Private Use' %}
        私用
      {% elsif rule_obj.label == 'Disclose Source' %}
        公開源碼
      {% elsif rule_obj.label == 'License and Copyright Notice' %}
        放置許可授權與版權資訊
      {% elsif rule_obj.label == 'Network Use is Distribution' %}
        使用網路分發
      {% elsif rule_obj.label == 'Same License' %}
        使用相同授權
      {% elsif rule_obj.label == 'State Changes' %}
        宣告變更
      {% elsif rule_obj.label == 'Hold Liable' %}
        承擔責任
      {% elsif rule_obj.label == 'Trademark Use' %}
        使用商標
      {% else %}
        {{ rule_obj.label }}
      {% endif %}
      </a></th>
    {% endfor %}
  {% endfor %}
</tr>
{% for license in site.licenses | sort: 'path' %}
  <tr style="height: 3em"><th scope="row"><a href="{{ license.id }}">{{ license.title }}</a></th>
  {% assign seen_tags = '' %}
  {% for type in types %}
    {% assign rules = site.data.rules[type] | sort: "label" %}
    {% for rule_obj in rules %}
      {% assign req = rule_obj.tag %}
      {% if seen_tags contains req %}
        {% continue %}
      {% endif %}
      {% capture seen_tags %}{{ seen_tags | append:req }}{% endcapture %}
      {% assign seen_req = false %}
      {% for t in types %}
        {% if license[t] contains req %}
          <td class="license-{{ t }}" style="text-align:center">
            <span class="{{ req }}">
              <span class="license-sprite {{ req }}"></span>
            </span>
          </td>
          {% assign seen_req = true %}
        {% endif %}
      {% endfor %}
      {% unless seen_req %}
        <td></td>
      {% endunless %}
    {% endfor %}
  {% endfor %}
  </tr>
{% endfor %}
</table>

## 說明

<p>開源授權中標註 <span class="license-permissions"><span class="license-sprite"></span></span> <b>允許</b> 的條目表示允許進行這樣的行為，否則可能表示不允許。</p>

<p>開源授權中標註 <span class="license-conditions"><span class="license-sprite"></span></span> <b>要求</b> 的條目為使用者必須遵循的內容。</p>

<p>開源授權中標註 <span class="license-limitations"><span class="license-sprite"></span></span> <b>禁止</b> 的內容通常為作者免責授權，有時也表示明確禁止授予使用者專利或者商標使用權。</p>

<dl>
{% assign seen_tags = '' %}
{% for type in types %}
  {% assign rules = site.data.rules[type] | sort: "label" %}
  {% for rule_obj in rules %}
    {% assign req = rule_obj.tag %}
    {% if seen_tags contains req %}
      {% continue %}
    {% endif %}
    <dt id="{{ req }}">
      {% if rule_obj.label == 'Commercial Use' %}
        商業用途
      {% elsif rule_obj.label == 'Distribution' %}
        分發
      {% elsif rule_obj.label == 'Modification' %}
        修改
      {% elsif rule_obj.label == 'Patent Use' %}
        專利授權
      {% elsif rule_obj.label == 'Private Use' %}
        私用
      {% elsif rule_obj.label == 'Disclose Source' %}
        公開源碼
      {% elsif rule_obj.label == 'License and Copyright Notice' %}
        放置許可授權與版權資訊
      {% elsif rule_obj.label == 'Network Use is Distribution' %}
        使用網路分發
      {% elsif rule_obj.label == 'Same License' %}
        使用相同授權
      {% elsif rule_obj.label == 'State Changes' %}
        宣告變更
      {% elsif rule_obj.label == 'Hold Liable' %}
        承擔責任
      {% elsif rule_obj.label == 'Trademark Use' %}
        使用商標
      {% else %}
        {{ rule_obj.label }}
      {% endif %}
    </dt>
    {% capture seen_tags %}{{ seen_tags | append:req }}{% endcapture %}
    {% for t in types %}
      {% for r in site.data.rules[t] | sort: "label" %}
        {% if r.tag == req %}
          <dd class="license-{{t}}"><span class="license-sprite"></span> {{ r.description }}</dd>
        {% endif %}
      {% endfor %}
    {% endfor %}
  {% endfor %}
{% endfor %}
</dl>
