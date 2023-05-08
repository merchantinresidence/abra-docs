# Write your own schema

!> If you're new to working with JSON, we recommend that you contact us to integrate with your theme.

Abra uses a JSON schema to configure your Abra blocks. You can change your global schema to integrate better with your theme and create richer online store experiences for buyers.

These customizations will apply to **every promotion**.

## Getting started

Before changing your JSON schema, we recommend that you:

1. Create a backup of your schema
2. Validate your changes in a [JSON validator](https://jsonformatter.curiousconcept.com/)

To change your schema, go to the "Settings" page and then select "Edit JSON". You'll see a default schema in the code editor.

> At any point, you can revert to the latest default for your theme by clicking "Revert to default".

Here's the outline of the schema:

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

You'd replace the all caps placeholder with the following values:

| Name             | Description                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| `TEMPLATE`       | all \| index \| product \| product.alternative \| collection \| collection.alternative \| cart  |
| `BLOCK_ID`       | The identifier for the block. This can be anything that helps you identify what the block does. |
| `BLOCK_TYPE`     | The type for the block                                                                          |
| `PROPERTY_NAME`  | The name of the property you're customizing within the block                                    |
| `PROPERTY_VALUE` | The value of the property you're customizing within the block                                   |

Here's an example of an Abra promotion using a popup block in the schema:

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

## Blocks

Blocks are the pieces nested within the schema. There are 3 types of blocks:

1. **Object block** - dynamically access an object and update some HTML
2. **Element block** - render elements and customize block content from your promotion
3. **Method block** - manipulate different parts of your storefront with these helpers

### Product object block

> Only applies when the product is eligible for the active promotion.

The `product` block gives you access to the product context.

#### Block properties

You can use these properties to customize the `product` block.

| Name       | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| `type`     | product                                                              |
| `selector` | The DOM selector for the element you're changing                     |
| `html`     | The HTML template to render after the promotion is activated         |
| `onevent`  | The JavaScript event name. The event must be dispatched on `window`. |

#### HTML variables

You can use these variables within the `html` property to render promotion-specific content.

| Name                     | Description                                                                      | Example                  |
| ------------------------ | -------------------------------------------------------------------------------- | ------------------------ |
| `{{ code }}`             | The active promotion code                                                        | WELCOME10                |
| `{{ compare_at_price }}` | The formatted compare at price of the product                                    | $30.00                   |
| `{{ final_price }}`      | The formatted price of the product after the promotion is activated              | $18.00                   |
| `{{ original_price }}`   | The formatted price of the product before the promotion is activated             | $20.00                   |
| `{{ title }}`            | The product title                                                                | Bicycle helmet           |
| `{{ total_discount }}`   | The formatted price discounted from the product after the promotion is activated | $2.00                    |
| `{{ url }}`              | The product url                                                                  | /products/bicycle-helmet |

#### Example

For example, you can change your `.price` element to include a slashed original price and the final price after the promotion is active.

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

### Cart object block

The `cart` block gives you access to the cart within the promotion.

> It'll only apply when a cart item within the cart is eligible for an offer within the active promotion.

_An example of a cart block to add the total discount to the cart drawer on all pages_

```json
{
  "schema": {
    "all": {
      "cart-drawer-subtotal": {
        "type": "cart",
        "selector": "#CartDrawer .cart-drawer__footer .totals__subtotal-value",
        "html": "<p class=\"totals__subtotal-value\">{{ subtotal_price }} (-{{ total_discount }})</p>"
      }
    }
  }
}
```

#### Block properties

You can use these properties to customize the `cart` block.

| Name       | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| `type`     | cart                                                                 |
| `selector` | The DOM selector for the element you're changing                     |
| `html`     | The HTML template to render after the promotion is activated         |
| `onevent`  | The JavaScript event name. The event must be dispatched on `window`. |

#### HTML variables

You can use these variables within the `html` property to render promotion-specific content.

| Name                   | Description                                            | Example   |
| ---------------------- | ------------------------------------------------------ | --------- |
| `{{ code }}`           | The promotion code                                     | WELCOME10 |
| `{{ subtotal_price }}` | The formatted subtotal price of the cart               | $20.00    |
| `{{ total_discount }}` | The formatted price of all discounts for the promotion | $2.00     |

### Cart item object block

The `cart-item` block gives you access to the cart items within the promotion.

> It'll only apply when the cart item is eligible for an offer within the active promotion.

_An example of a cart item block to slashed pricing on the cart page_

```json
{
  "schema": {
    "cart": {
      "cart-item-pricing": {
        "type": "cart-item",
        "item": "#cart .cart-item",
        "selector": "div.product-option",
        "html": "<div class=\"product-option\">{{ final_price }} <div class=\"cart-item--regular-price\">{{ original_price }}</div></div>"
      }
    }
  }
}
```

#### Block properties

You can use these properties to customize the `cart` block.

| Name       | Description                                                                                                  |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| `type`     | cart-item                                                                                                    |
| `item`     | The DOM selector for the cart items. This selector must select **exactly** the same number of items in cart. |
| `selector` | The DOM selector for the element you're changing                                                             |
| `html`     | The HTML template to render after the promotion is activated                                                 |
| `onevent`  | The JavaScript event name. The event must be dispatched on `window`.                                         |

#### HTML variables

You can use these variables within the `html` property to render promotion specific content.

| Name                        | Description                                                          | Example                  |
| --------------------------- | -------------------------------------------------------------------- | ------------------------ |
| `{{ code }}`                | The promotion code                                                   | WELCOME10                |
| `{{ final_line_price }}`    | The formatted line price after the promotion is applied              | $36.00                   |
| `{{ final_price }}`         | The formatted price after the promotion is applied                   | $18.00                   |
| `{{ original_line_price }}` | The formatted line price before the promotion is applied             | $40.00                   |
| `{{ original_price }}`      | The formatted price before the promotion is applied                  | $20.00                   |
| `{{ quantity }}`            | The cart item quantity                                               | 2                        |
| `{{ total_discount }}`      | The formatted price discounted from the cart item with the promotion | $4.00                    |
| `{{ url }}`                 | The product url                                                      | /products/bicycle-helmet |

### Element block

### Method block

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
