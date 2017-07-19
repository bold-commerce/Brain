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
<div class="bold-recommend__product">
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
</div>
```

### Template overriding 

Templates can be overridden by their type. Higher up on your product.liquid page, simply override the default template using the following: (Note this must be wrapped in a on dom ready to ensure the Brain widget script is loaded)

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
</div>`, false);
```