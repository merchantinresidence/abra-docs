# Abra Schema

The Abra schema is a core concept to running your promotions. If you've created a promotion in our embedded app, you've already interacted with the schema. This guide will walk you through how the schema works, how does it interact with your storefront, and what you can do with it.

## Getting started

```json
{
  "schema" {
    "all" {
      "dd1627cb-428e-4b7d-bc05-dd96cc6cb50a": {
        "type": "popup",
        "text": "20% APPLIED"
      }
    }
  }
}
```

## Examples

### Dawn

```json
{
  "schema": {
    "all": {
      "cart-drawer-subtotal": {
        "type": "cart",
        "selector": "#CartDrawer .cart-drawer__footer .totals__subtotal-value",
        "html": "<p class=\"totals__subtotal-value\">{{items_subtotal_price}} (-{{total_discount}})</p>"
      },
      "price": {
        "type": "product",
        "selector": ".price",
        "html": "<div class=\"price\">{{ original_price }}</div>"
      },
      "compare-at-price": {
        "type": "product",
        "selector": ".compare-price",
        "html": "<div class=\"compare-price\">{{ final_price }}</div>"
      }
    },
    "cart": {
      "cart-subtotal": {
        "type": "cart",
        "selector": ".cart__footer .js-contents",
        "html": "<div class=\"js-contents\"><div class=\"totals\"><h2 class=\"totals__subtotal\">Subtotal</h2><p class=\"totals__subtotal-value\">{{items_subtotal_price}}</p></div><div><ul class=\"discounts list-unstyled\" role=\"list\" aria-label=\"Discount\"><li class=\"discounts__discount discounts__discount--position\">{{code}} (-{{total_discount}})</li></ul></div><div></div><small class=\"tax-note caption-large rte\">Taxes and shipping calculated at checkout</small></div>"
      },
      "cart-items-price": {
        "type": "cart-item",
        "item": "#cart .cart-item",
        "selector": "div.product-option",
        "html": "<div class=\"product-option\">{{ original_price }}</div>"
      },
      "cart-items-line-price": {
        "type": "cart-item",
        "item": "#cart .cart-item",
        "selector": ".cart-item__totals.small-hide .price",
        "html": "<span class=\"price price--end\">{{ final_line_price }} <s>{{ original_line_price }}</s></span>"
      }
    }
  }
}
```
