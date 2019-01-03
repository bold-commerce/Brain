# Bold Brain

### Widget

### Templating

Brain uses [Mustache](https://mustache.github.io/) for its templates. Templates are stored in `BOLD.brain.templates`.

Brain Wrapper
```html
<div class="bold-recommend__wrap">
	<h2 class="bold-recommend__title">{{{ widgetTitle }}}</h2>
	{{{ widgetGrid }}}
</div>
```

Brain Grid
```html
<div class="bold-recommend__grid"></div>
```

Brain Grid Item
```html
<div class="bold-recommend__product bold-recommend__product_{{{ productCount }}} bold-recommend__updated">
	<div class="bold-recommend__product-content">
		<div class="bold-recommend__img-container">
			<img class="bold-recommend__img" src="{{ imgUri }}">
		</div>

		<h4>{{{ title }}}</h4>

		{{#priceVaries}}
			<h5>{{{ priceMin }}} - {{{ priceMax }}}</h5>
		{{/priceVaries}}

		{{^priceVaries}}
			<h5>{{{ priceMax }}}</h5>
		{{/priceVaries}}
	</div>

	{{#atcBtnEnabled}}
		{{#hasMultipleVariants}}
			<button class="btn bold-recommend__view-product-btn">View Product</button>
		{{/hasMultipleVariants}}

		{{^hasMultipleVariants}}
			<button class="btn add-to-cart bold-recommend__atc-btn">Add To Cart</button>
		{{/hasMultipleVariants}}
	{{/atcBtnEnabled}}
</div>
```

### Template Overriding Before the Widget is Loaded

Templates can be overridden prior to their use. To do this open theme.liquid in your Shopify theme. Find   {{ content\_for\_header }} and add the following above it:

```html
<!-- Put this before {{ content_for_header }} -->
<script>
    window.BOLD = window.BOLD || {};
    window.BOLD.brain = window.BOLD.brain || {};
    window.BOLD.brain.templates = window.BOLD.brain.templates || {};
    window.BOLD.brain.templates['brain_grid_item'] = '<div>product</div>';
</script>
```

You may need to wrap your template with `{% raw %}`/`{% endraw %}` to avoid the template variables from being rendered by [Liquid](https://help.shopify.com/themes/liquid).

### Template Overriding After the Widget is Loaded

**Note**: The Brain Widget JS is loaded asyncronously so it can be tricky to know when these functions become available. It is generally simpler to use the method described in the *Template Overriding Before the Widget is Loaded* section.

Templates can be overridden by their type. Higher up on your product.liquid page, simply override the default template using the following:

```html
window.BOLD.brain.setTemplate('brain_grid_item',
	`<div class="bold-recommend__product">
                <div>
                    <img src="{{ imgUri }}" alt="{{{ handle }}}"/>
                    <h4>{{{ title }}}</h4>
                    
                    {{#priceVaries}}
                        <h5>{{{ priceMin }}} - {{{ priceMax }}}</h5>
                    {{/priceVaries}}

                    {{^priceVaries}}
                        <h5>{{{ priceMax }}}</h5>
                    {{/priceVaries}}
                </div>
</div>`, true);
```
