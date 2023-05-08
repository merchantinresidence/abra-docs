# Abra Schema

> If you're new to working with JSON, we recommend you contact a developer or contact us to help you.

This guide will walk you through how your Abra schema works, how it interacts with your storefront, and what you can do with it.

## Getting started

The Abra schema is a core concept to running your promotions. If you've created a promotion in our embedded app, you've already interacted with the schema. The promotion creates a schema behind the scenes and Abra's app embed reads it to show your promotion on your storefront.

_An example of an Abra promotion using a popup block in the schema_

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

To customize your schema, go to "Settings" page and then select "Edit JSON". These customizations will apply to **every promotion**. We recommend using this section to integrate dynamic pricing and other storefront features with your theme.

The Abra schema starts with a `schema` key. Within the `schema`, you can specify which template you'd like the block to run on. Within each template, you specify a block identifier and the properties for the given block. The block identifier can be anything to help you remember what the rule does - just remember is has to be unique.

_The outline of a schema_

```json
{
  "schema": {
    "TEMPLATE": {
      "BLOCK_ID": {
        "type": "BLOCK_TYPE",
        "PROPERTY_NAME": "PROPERTY_VALUE"
      }
    }
  }
}
```

| Name             | Description                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| `TEMPLATE`       | all \| home \| product \| product.alternative \| collection \| collection.alternative \| cart   |
| `BLOCK_ID`       | The identifier for the block. This can be anything that helps you identify what the block does. |
| `BLOCK_TYPE`     | The type for the block                                                                          |
| `PROPERTY_NAME`  | The name of the property you're customizing within the block                                    |
| `PROPERTY_VALUE` | The value of the property you're customizing within the block                                   |

## Blocks

The next core concept is blocks. There are 3 categories of blocks we'll be working with:

1. **Object block** - this allows you to dynamically access an object within your promotion. This is typically used for showing updated pricing, or showing additional information about the promotion.
2. **Element block**
3. **Method block**

### `product` object block

The `product` block gives you access to the product within the promotion. It'll only apply when the product is eligible for an offer with the active promotion.

_An example of a product block to add slashed pricing on all pages_

```json
{
  "schema": {
    "all": {
      "slashed-product-price": {
        "type": "product",
        "selector": ".price",
        "html": "<div class=\"price\"><div class=\"price--sale\">{{ final_price }}</div><div class=\"price--regular\">{{ original_price }}</div></div>"
      }
    }
  }
}
```

#### Block

| Name       | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| `type`     | product                                                              |
| `selector` | The DOM selector for the element                                     |
| `html`     | The HTML markup after the promotion is activated.                    |
| `onEvent`  | The JavaScript event name. The event must be dispatched on `window`. |

#### HTML variables

| Name               | Description                                                        | Example                  |
| ------------------ | ------------------------------------------------------------------ | ------------------------ |
| `code`             | The promotion code                                                 | WELCOME10                |
| `compare_at_price` | The formatted compare at price of the product                      | $30.00                   |
| `final_price`      | The formatted price of the product after the promotion is applied  | $18.00                   |
| `handle`           | The product handle                                                 | bicycle-helmet           |
| `original_price`   | The formatted price of the product before the promotion is applied | $20.00                   |
| `title`            | The product title                                                  | Bicycle helmet           |
| `total_discount`   | The formatted price discounted from the product with the promotion | $2.00                    |
| `url`              | The product url                                                    | /products/bicycle-helmet |

### `cart` object block

### `cart-item` object block

### Element block

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

```

```
