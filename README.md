# Shopify-Top-Text-Bar
Create top bar in shopify
### First in your Sections part  create template top-text-bar.liquid  and input code
```html
<div data-section-id="{{ section.id }}"  id="flexslider-{{ section.id }}" class="flexslider bar-slider" data-section-type="bar-section">
  <ul class="textbar_slides">
  	 {% for block in section.blocks %}
         <li {{ block.shopify_attributes }} id="slide-{{block.id}}" data-index="{{forloop.index0}}">   
          <div class="slide-bar"> 
               {{ block.settings.bar_text  }}   
          </div>  
        </li>      
    {% endfor %}
  </ul>
</div>
<style>
  ul.textbar_slides{
   margin:0;
   padding:0;
  }
  ul.textbar_slides li:nth-of-type(n+2){
   display:none; 
  }
 .slide-bar {
    color:{{section.settings.text_color}};
    background:{{section.settings.bg_color}};
   text-align: center;
   padding:{{section.settings.text_size}}px 0;
  }
 .slide-bar p{
   padding:0px;
   margin:0px;
   color:{{section.settings.text_color}} !important;
   font-size:{{section.settings.font_size}}px;
 }
</style>
<script>
  jQuery(function($){
    let slidetotal = $("ul.textbar_slides li").length;
    let num = 2;
    let textbarInterval = setInterval(function(){
      $("ul.textbar_slides li").hide();
      $("ul.textbar_slides li:nth-child("+num+")").show();
      num++;
      if(num>slidetotal){
        num=1; 
      }
    }, {{section.settings.text_time}}*1000);
    window.addEventListener("unload", function(event) {
      clearInterval(textbarInterval)  
    });
  })
</script>
{% schema %}
 {
    "name": "bar",
    "max_blocks": 5,
    "settings": [
      {
        "type": "color",
        "id": "bg_color",
        "label": "Background",
        "default": "#fff"
      },
	 {
        "type": "color",
        "id": "text_color",
        "label": "Text Color",
        "default": "#333"
      },
	{
        "type": "text",
        "id": "text_size",
        "label": "TOP/Bottom Space",
        "default": "10"
      },
      {
        "type": "range",
        "id": "font_size",
        "min": 10,
        "max": 36,
        "step": 1,
        "unit": "px",
        "label": "Font size",
        "default": 18
      },
	{
        "type": "text",
        "id": "text_time",
        "label": "Interval of a few seconds",
        "default": "5"
      }
	],
     "blocks" : [
      {
        "type": "slide",
        "name": "Slide",
        "settings": [
        {
          "type": "richtext",
          "id": "bar_text",
          "label": "Text"
        }
	  ]
 	 }
	]
 }
{% endschema %}
```
### Then in theme.liquid insert this section before section header 
```html
{% section 'top-text-bar' %}
```
### Now you can edit top bar text in Customize
![](https://s3.bmp.ovh/imgs/2022/02/66390ee7b3d43d75.png)
