# Complex Blogpost Search for Adobe Business Catalyst
Search and filter blog posts of your site using title, body, tags and categories

## How to Install

1. Upload widget folder to your site
The widget is downloaded as an archive containg a folder. Upload the respective folder to the root of you site. 
*This is mandatory if you want the widget to run out-of-the-box.*

2. Initiate the widget
Add the following include to any page or template where you want the widget to be displayed.
```html
{% include "/bc-widgets/complex-blogpost-search/init.liquid" -%}
```

### Prerequisites
Already included in the **init.liquid** file, some of these can be removed if already loaded in your template.

 - [jQuery](https://jquery.com/) v1.11.3
 - [Bootstrap](http://getbootstrap.com/) v3.3.6
 - [Select2](https://select2.github.io/) v4.0.1

## How to Customize
### Change where search results are loaded
 - The results will be loaded wherever the widget finds the ```cb-results``` id in your template/page 
 - You can also rename the two instances of the id in the *assets/cb-script.js* from the following line:
```javascript
    $("#cb-results").load("/bc-widgets/complex-blogpost-search/cb-query.html?" + $(this).serialize() + " #cb-results");
```

### Modify the results template
Just edit or remove parts of the results template in the *cb-results.liquid* file.
For Liquid modifications follow the [Getting Started with Liquid](http://docs.businesscatalyst.com/developers/liquid/getting-started-with-liquid) for help.

### Modify the number of tags, categories, results
Every ```{module_data}``` has a limit parameter that specifies how many items to be included from the total number of items returned by the module. The maximum value is 500.

### Add more information on the live search
You can add an image or description to the live search.

1. Check that the field you need is called in the ```{module_data}``` of *cb-live.html* (e.g. postFeaturedImage, postBody)
2. Add them to the titles object in the HTMLtoDOM function in */assets/cb-script.js*
  ```javascript
    $.map(json.items, function(item) {
        titles.push({
            id: item.id,
            text: item.postTitle,
            image: item.postFeaturedImage,
            body: item.postBody
        });
    });
```
3. Format the live search results markup. This is done in formatResults function in */assets/cb-script.js*
  ```javascript
    var markup = "<div class='select2-result-repository clearfix'>" +
        "<div class='select2-result-repository__meta'>" +
        "<div class='select2-result-repository__title'>" + item.text + "</div>" +
        "</div></div>";
```

### Version
1.0.1

### License
----

MIT