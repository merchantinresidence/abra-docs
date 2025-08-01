# Write your own schema

!> If you're new to working with JSON, we recommend that you [contact us](mailto:help@abrapromotions.com?subject=Abra%20integration%20help) to integrate with your theme.

Abra uses a JSON schema to configure your Abra blocks. You can change your global schema to integrate better with your theme and create richer online store experiences for buyers.

These customizations will apply to **every promotion**.

## Getting started

Before changing your JSON schema, we recommend that you:

1. Create a backup of your schema
2. Validate your changes in a [JSON validator](https://jsonformatter.curiousconcept.com/)

To change your schema, go to the "Settings" page and then select "Edit JSON". You'll see a default schema in the code editor.

> At any point, you can revert to the latest default for your theme by clicking "Revert to default".

The schema uses the outline shown below. You can replace the capitalized placeholders with the values found in the table under the example.

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
| `TEMPLATE`       | all \| index \| product \| product.alternative \| collection \| collection.alternative \| cart  |
| `BLOCK_ID`       | The identifier for the block. This can be anything that helps you identify what the block does. |
| `BLOCK_TYPE`     | The type for the block                                                                          |
| `PROPERTY_NAME`  | The name of the property you're customizing within the block                                    |
| `PROPERTY_VALUE` | The value of the property you're customizing within the block                                   |

### Example <!-- {docsify-ignore} -->

A promotion using a popup block in the schema

```json
{
  "schema" {
    "all" {
      "dd1627cb-428e-4b7d-bc05-dd96cc6cb50a": {
        "type": "popup",
        "persistentState": true,
        "states": [
          {
            "state": "DEFAULT",
            "text": "20% APPLIED"
          }
        ]
      }
    }
  }
}
```

## Blocks

Blocks are the pieces nested within the template in your schema. There are 3 types of blocks:

1. **Object block** - dynamically access an object and update some HTML
2. **Element block** - render elements and customize block content from your promotion
3. **Method block** - manipulate different parts of your storefront with these helpers

### Product object block

> Only applies when the product is eligible for the active promotion.

The `product` block allows you to replace a block of HTML with new HTML. You have access to the product context in the new HTML.

#### Block properties

| Name        | Description                                                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `type`      | product                                                                                                                      |
| `container` | (optional) The DOM selector for the element wrapping the product. This element must contain an `<a>` linking to the product. |
| `selector`  | The DOM selector for the element you're changing                                                                             |
| `html`      | The HTML template to render after the promotion is activated                                                                 |
| `onevent`   | (optional) The JavaScript event name. The event must be dispatched on `window`.                                              |

#### Liquid variables

| Name                                | Description                                                                                                                                             | Example                  |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `code`                              | The active promotion code                                                                                                                               | WELCOME10                |
| `url`                               | The product url                                                                                                                                         | /products/bicycle-helmet |
| `title`                             | The product title                                                                                                                                       | Bicycle helmet           |
| `currency.iso_code`                 | The ISO code of the active currency                                                                                                                     | CAD                      |
| `compare_at_price`                  | The formatted compare at price of the product                                                                                                           | $30.00                   |
| `compare_at_price_cents`            | The compare at price of the product in cents                                                                                                            | 3000                   |
| `selected_variant.compare_at_price` | The formatted compare at price of the selected variant                                                                                                  | $18.00                   |
| `selected_variant.selected_selling_plan.compare_at_price` | The formatted selling/subscription plan compare at price of the selected variant                                                                                                  | $18.00                   |
| `selected_variant.selected_selling_plan_or_variant.compare_at_price` | The formatted selling/subscription plan or variant compare at price of the selected variant                                                                                                  | $18.00                   |
| `final_price`                       | The formatted price of the product after the discount is applied                                                                                     | $18.00                   |
| `final_price_cents`                       | The price of the product after the discount is applied in cents                                                                                     | 1800                   |
| `selected_variant.final_price`      | The formatted price of the selected variant after the discount is applied                                                                            | $18.00                   |
| `selected_variant.selected_selling_plan.final_price`      | The formatted selling/subscription plan price of the selected variant after the discount is applied                                                                            | $18.00                   |
| `selected_variant.selected_selling_plan_or_variant.final_price`      | The formatted selling/subscription plan or variant price of the selected variant after the discount is applied                                                                            | $18.00                   |
| `original_price`                    | The formatted price of the product before the discount is applied                                                                                    | $20.00                   |
| `original_price_cents`                    | The price of the product before the discount is applied in cents                                                                                    | 2000                   |
| `selected_variant.original_price`   | The formatted price of the selected variant before the discount is applied                                                                           | $20.00                   |
| `selected_variant.selected_selling_plan.original_price`                    | The formatted selling/subscription plan price of the selected variant before the discount is applied                                                                                    | $20.00                   |
| `selected_variant.selected_selling_plan_or_variant.original_price`                    | The formatted selling/subscription plan or variant price of the selected variant before the discount is applied                                                                                    | $20.00                   |
| `total_discount_dollar`                    | The formatted dollar amount discounted from the product after the discount is applied. It'll use the "compare at" pricing if there's a "compare at" variable | $2.00                    |
| `selected_variant.total_discount_dollar`   | The formatted dollar amount discounted from the selected variant after the discount is applied                                                               | $20.00                   |
| `selected_variant.selected_selling_plan.total_discount_dollar`   | The formatted dollar amount discounted from the selected selling/subscription plan option after the discount is applied                                                               | $20.00                   |
| `selected_variant.selected_selling_plan_or_variant.total_discount_dollar`   | The formatted dollar amount discounted from the selected selling/subscription plan option or variant after the discount is applied                                                               | $20.00                   |
| `total_discount_percentage`                    | The formatted percentage discounted from the product after the discount is applied. It'll use the "compare at" pricing if there's a "compare at" variable | 10%                    |
| `selected_variant.total_discount_percentage`   | The formatted percentage discounted from the selected variant after the discount is applied                                                               | 10%                   |
| `selected_variant.selected_selling_plan.total_discount_percentage`   | The formatted percentage amount discounted from the selected selling/subscription plan option after the discount is applied                                                               | 10%                   |
| `selected_variant.selected_selling_plan_or_variant.total_discount_percentage`   | The formatted percentage amount discounted from the selected selling/subscription plan option or variant after the discount is applied                                                               | 10%                   |

#### Example

Change your `.price` element to include a slashed original price and the final price

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

> Only apply when an item within the cart is eligible for the active promotion.

The `cart` block allows you to replace a block of HTML with new HTML. You have access to the cart context in the new HTML.

#### Block properties

| Name       | Description                                                                     |
| ---------- | ------------------------------------------------------------------------------- |
| `type`     | cart                                                                            |
| `selector` | The DOM selector for the element you're changing                                |
| `html`     | The HTML template to render after the promotion is activated                    |
| `onevent`  | (optional) The JavaScript event name. The event must be dispatched on `window`. |

#### Liquid variables

| Name                        | Description                                                                                                                                             | Example   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| `code`                      | The promotion code                                                                                                                                      | WELCOME10 |
| `compare_at_subtotal_price` | The formatted compare at subtotal price of the cart                                                                                                     | $30.00    |
| `currency.iso_code`         | The ISO code of the active currency                                                                                                                     | CAD       |
| `final_subtotal_price`      | The formatted subtotal price of the cart after the promotion is activated                                                                               | $18.00    |
| `original_subtotal_price`   | The formatted subtotal price of the cart before the promotion is activated                                                                              | $20.00    |
| `subtotal_price`            | Alias for `final_subtotal_price`                                                                                                                        | $18.00    |
| `total_discount_dollar`            | The formatted dollar amount of all discounts for the promotion. It'll use the "compare at" pricing if the cart block has a `compare_at_subtotal_price` variable | $2.00     |
| `total_discount_percentage`            | The formatted percentage of all discounts for the promotion. It'll use the "compare at" pricing if the cart block has a `compare_at_subtotal_price` variable | 10%     |

#### Example

Update the subtotal of your cart drawer and add the total discount

```json
{
  "schema": {
    "all": {
      "cart-drawer-subtotal": {
        "type": "cart",
        "selector": "#CartDrawer .cart-drawer__footer .totals__subtotal-value",
        "html": "<p class=\"totals__subtotal-value\">{{ final_subtotal_price }} (-{{ total_discount }})</p>"
      }
    }
  }
}
```

### Cart item object block

> Only apply when the item is eligible for the active promotion.

The `cart-item` block allows you to replace a block of HTML with new HTML. You have access to the cart item context in the new HTML.

#### Block properties

| Name       | Description                                                                                                  |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| `type`     | cart-item                                                                                                    |
| `item`     | The DOM selector for the cart items. This selector must select **exactly** the same number of items in cart. |
| `selector` | The DOM selector for the element you're changing                                                             |
| `html`     | The HTML template to render after the promotion is activated                                                 |
| `onevent`  | (optional) The JavaScript event name. The event must be dispatched on `window`.                              |

#### Liquid variables

| Name                    | Description                                                                                                                                                    | Example                  |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `code`                  | The promotion code                                                                                                                                             | WELCOME10                |
| `compare_at_line_price` | The formatted compare at line price before the promotion is applied                                                                                            | $40.00                   |
| `compare_at_price`      | The formatted compare at price before the promotion is applied                                                                                                 | $20.00                   |
| `currency.iso_code`     | The ISO code of the active currency                                                                                                                            | CAD                      |
| `final_line_price`      | The formatted line price after the promotion is applied                                                                                                        | $36.00                   |
| `final_price`           | The formatted price after the promotion is applied                                                                                                             | $18.00                   |
| `original_line_price`   | The formatted line price before the promotion is applied                                                                                                       | $40.00                   |
| `original_price`        | The formatted price before the promotion is applied                                                                                                            | $20.00                   |
| `quantity`              | The cart item quantity                                                                                                                                         | 2                        |
| `total_discount`        | The formatted price discounted from the cart item with the promotion. It'll use the "compare at" pricing if there's a "compare at" variable                    | $4.00                    |
| `total_line_discount`   | The formatted price discounted from the cart item including quantity with the promotion. It'll use the "compare at" pricing if there's a "compare at" variable | $8.00                    |
| `url`                   | The product url                                                                                                                                                | /products/bicycle-helmet |

#### Example

Change your cart item to show the final price and slash the original price

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

### Announcement bar element block

The `announcement-bar` block allows you to show and update the content of your announcement bar.

#### Block properties

| Name              | Description                                                                     |
| ----------------- | ------------------------------------------------------------------------------- |
| `type`            | announcement-bar                                                                |
| `persistentState` | Whether the default state is persistent or not.                                 |
| `states`          | The announcement bar's content by state.                                        |
| `onevent`         | (optional) The JavaScript event name. The event must be dispatched on `window`. |

#### Block state properties

A block state allows you to show different content based on the state of the promotion and discount.

| Name    | Description                                                                                 |
| ------- | ------------------------------------------------------------------------------------------- |
| `icon`  | (optional) discount \| gift \| percentage                                                   |
| `state` | The name of the state: DEFAULT\| PROGRESS_ZERO \| PROGRESS_ONE \| PROGRESS_OTHER \| SUCCESS |
| `text`  | The announcement bar's text content.                                                        |

#### Liquid variables

| Name                | Description                         | Example   |
| ------------------- | ----------------------------------- | --------- |
| `code`              | The promotion code                  | WELCOME10 |
| `currency.iso_code` | The ISO code of the active currency | CAD       |
| `discount_value`    | The value of a discount used in the promotion | 10%       |

#### Example

Showing an announcement bar with a gift icon and some text

```json
{
  "schema": {
    "all": {
      "gift-announcement-bar": {
        "type": "announcement-bar",
        "persistentState": true,
        "states": [
          {
            "icon": "gift",
            "state": "DEFAULT",
            "text": "FREE GIFT ON ORDERS OVER $50"
          }
        ]
      }
    }
  }
}
```

### Banner element block

The `banner` block allows you to show and update the content of your banner.

#### Block properties

| Name              | Description                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------- |
| `type`            | banner                                                                                   |
| `name`            | The identifier for the banner. This must match the identifier in Shopify's Theme Editor. |
| `persistentState` | Whether the default state is persistent or not.                                          |
| `states`          | The banner's content by state.                                                           |
| `onevent`         | (optional) The JavaScript event name. The event must be dispatched on `window`.          |

#### Block state properties

A block state allows you to show different content based on the state of the promotion and discount.

| Name    | Description                                                                                 |
| ------- | ------------------------------------------------------------------------------------------- |
| `icon`  | (optional) discount \| gift \| percentage                                                   |
| `state` | The name of the state: DEFAULT\| PROGRESS_ZERO \| PROGRESS_ONE \| PROGRESS_OTHER \| SUCCESS |
| `text`  | The banner's text content.                                                                  |

#### Liquid variables

| Name                | Description                         | Example   |
| ------------------- | ----------------------------------- | --------- |
| `code`              | The promotion code                  | WELCOME10 |
| `currency.iso_code` | The ISO code of the active currency | CAD       |
| `discount_value`    | The value of a discount used in the promotion | 10%       |
| `discount.progress_total`    | (Gift with purchase banner) Minimum spend amount or quantity of items that need to be added to cart to get the free gift | $20.00       |
| `discount.progress_remaining`    | (Gift with purchase banner) Amount or quantity remaining to be added to cart to get the free gift | $15.00       |

#### Example

Showing a banner with a discount icon and some text

```json
{
  "schema": {
    "all": {
      "gift-banner": {
        "type": "banner",
        "name": "default",
        "persistentState": true,
        "states": [
          {
            "icon": "discount",
            "state": "DEFAULT",
            "text": "FREE GIFT ON ORDERS OVER $50"
          }
        ]
      }
    }
  }
}
```

### Popup element block

The `popup` block allows you to show and update the content of your popup.

#### Block properties

| Name              | Description                                                                     |
| ----------------- | ------------------------------------------------------------------------------- |
| `type`            | popup                                                                           |
| `persistentState` | Whether the default state is persistent or not.                                 |
| `states`          | The popup's content by state.                                                   |
| `onevent`         | (optional) The JavaScript event name. The event must be dispatched on `window`. |

#### Block state properties

A block state allows you to show different content based on the state of the promotion and discount.

| Name    | Description                                                                                 |
| ------- | ------------------------------------------------------------------------------------------- |
| `icon`  | (optional) discount \| gift \| percentage                                                   |
| `state` | The name of the state: DEFAULT\| PROGRESS_ZERO \| PROGRESS_ONE \| PROGRESS_OTHER \| SUCCESS |
| `text`  | The popup's text content                                                                    |

#### Liquid variables

| Name                | Description                         | Example   |
| ------------------- | ----------------------------------- | --------- |
| `code`              | The promotion code                  | WELCOME10 |
| `currency.iso_code` | The ISO code of the active currency | CAD       |
| `discount_value`    | The value of a discount used in the promotion | 10%       |

#### Example

Showing a popup with some text

```json
{
  "schema": {
    "all": {
      "custom-popup": {
        "type": "popup",
        "persistentState": true,
        "states": [
          {
            "state": "DEFAULT",
            "text": "{{ code }} APPLIED"
          }
        ]
      }
    }
  }
}
```

### Hide method block

The `hide` block allows you to hide an element when the promotion is active.

#### Block properties

| Name       | Description                             |
| ---------- | --------------------------------------- |
| `type`     | hide                                    |
| `selector` | The DOM selector for the target element |

#### Example

Hiding your footer

```json
{
  "schema": {
    "all": {
      "hide-footer": {
        "type": "hide",
        "selector": ".footer"
      }
    }
  }
}
```

### Add class method block

The `add-class` block allows you to add a class to an element when the promotion is active.

#### Block properties

| Name       | Description                             |
| ---------- | --------------------------------------- |
| `type`     | add-class                               |
| `selector` | The DOM selector for the target element |
| `value`    | The CSS class - do not include a `.`    |

#### Example

Adding a `vip-customer` class to the body element

```json
{
  "schema": {
    "all": {
      "vip-customer-style": {
        "type": "add-class",
        "selector": "body",
        "value": "vip-customer"
      }
    }
  }
}
```

### Remove class method block

The `remove-class` block allows you to remove a class to an element when the promotion is active.

#### Block properties

| Name       | Description                             |
| ---------- | --------------------------------------- |
| `type`     | remove-class                            |
| `selector` | The DOM selector for the target element |
| `value`    | The CSS class - do not include a `.`    |

#### Example

Removing a `hidden` class from a navigation item

```json
{
  "schema": {
    "all": {
      "show-special-nav-item": {
        "type": "remove-class",
        "selector": ".nav .nav-item--vip",
        "value": "hidden"
      }
    }
  }
}
```

## Theme examples

See our [GitHub repository](https://github.com/merchantinresidence/abra-schemas/tree/main/example-schemas) for more examples.
