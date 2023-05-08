# Abra Developer Docs

Welcome to Abra's developer docs! We know that your business needs as a merchant are diverse and we want Abra to work for you, not against you.

## Schema

The Abra schema is a core concept to running your promotions. You can hook up richer integration points between Abra and your theme and give your buyers a better experience.

[Read more about the Abra schema](schema.md)

### Blocks

#### `announcement-bar`

```json
{
  "schema": {
    "all": {
      "gift-announcement-bar": {
        "type": "announcement-bar",
        "icon": "gift",
        "text": "FREE GIFT ON ORDERS OVER $50"
      }
    }
  }
}
```

| Name      | Description                                                                                      |
| --------- | ------------------------------------------------------------------------------------------------ |
| `type`    | announcement-bar                                                                                 |
| `onEvent` | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `icon`    | gift \| discount \| percentage \| undefined                                                      |
| `text`    | The text for the announcement bar                                                                |

#### `banner`

```json
{
  "schema": {
    "all": {
      "gift-banner": {
        "type": "banner",
        "icon": "gift",
        "text": "FREE GIFT ON ORDERS OVER $50"
      }
    }
  }
}
```

| Name      | Description                                                                                      |
| --------- | ------------------------------------------------------------------------------------------------ |
| `type`    | banner                                                                                           |
| `onEvent` | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `icon`    | gift \| discount \| percentage \| undefined                                                      |
| `text`    | The text for the banner                                                                          |

#### `popup`

```json
{
  "schema": {
    "all": {
      "popup-applied": {
        "type": "popup",
        "icon": "percentage",
        "text": "20% OFF APPLIED"
      }
    }
  }
}
```

| Name      | Description                                                                                      |
| --------- | ------------------------------------------------------------------------------------------------ |
| `type`    | popup                                                                                            |
| `onEvent` | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `icon`    | gift \| discount \| percentage \| undefined                                                      |
| `text`    | The text for the popup                                                                           |

### Rules

#### `add-class`

```json
{
  "schema": {
    "all": {
      "update-footer": {
        "type": "add-class",
        "selector": ".footer",
        "value": "footer--promo"
      }
    }
  }
}
```

| Name       | Description                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------ |
| `type`     | add-class                                                                                        |
| `onEvent`  | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `selector` | The DOM selector for the element                                                                 |
| `value`    | The class to add to the element                                                                  |

#### `cart`

```json
{
  "schema": {
    "cart": {
      "promo-cart": {
        "type": "cart",
        "discounts": {
          "selector": ".totals",
          "html": "<div><ul class=\"discounts list-unstyled\" role=\"list\" aria-label=\"Discount\"><li class=\"discounts__discount discounts__discount--position\">{{code}} (-{{total_discount}})</li></ul></div>"
        },
        "items": {
          "selector": "tr.cart-item"
        },
        "subtotal": {
          "selector": ".totals__subtotal-value"
        }
      }
    }
  }
}
```

| Name        | Description                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------ |
| `type`      | cart                                                                                             |
| `onEvent`   | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `discounts` | The `selector` and `html` for the cart discounts                                                 |
| `items`     | The `selector` and `html` for the cart items                                                     |
| `subtotal`  | The `selector` and `html` for the cart subtotal                                                  |
| `total`     | The `selector` and `html` for the cart total                                                     |

#### `remove-class`

```json
{
  "schema": {
    "all": {
      "update-footer": {
        "type": "remove-class",
        "selector": ".footer",
        "value": "footer--primary-bg"
      }
    }
  }
}
```

| Name       | Description                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------ |
| `type`     | remove-class                                                                                     |
| `onEvent`  | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `selector` | The DOM selector for the element                                                                 |
| `value`    | The class to remove from the element                                                             |

#### `hide`

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

| Name       | Description                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------ |
| `type`     | hide                                                                                             |
| `onEvent`  | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`. |
| `selector` | The DOM selector for the element                                                                 |

#### `price`

```json
{
  "schema": {
    "all": {
      "dynamic-price": {
        "type": "price",
        "selector": ".price",
        "html": "<div class=\"price\"><div class=\"price--sale\">{{sale_price}}</div><div class=\"price--regular\">{{regular_price}}</div></div>"
      }
    }
  }
}
```

| Name       | Description                                                                                              |
| ---------- | -------------------------------------------------------------------------------------------------------- |
| `type`     | price                                                                                                    |
| `onEvent`  | The name of JavaScript event to trigger this rule. The event must be dispatched on the `window`.         |
| `html`     | Custom markup for the price element. You can use `{{regular_price}}` and `{{sale_price}}` in the markup. |
| `selector` | The DOM selector for the element                                                                         |

## Global

These are global CSS and JavaScript integration points for you to use in your theme.

### CSS classes

| Name                          | Description                                                                                                          |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `.abra--initialized`          | A modifier class applied to the body element when window.Abra is initialized                                         |
| `.abra--activated`            | A modifier class applied to the body element when a promotion is active                                              |
| `.abra--applied`              | A modifier class applied to the body element when a promotion is applied                                             |
| `.abra--{{ code }}-activated` | A modifier class, where `{{ code }}` is your promotion code, applied to the body element when a promotion is active  |
| `.abra--{{ code }}-applied`   | A modifier class, where `{{ code }}` is your promotion code, applied to the body element when a promotion is applied |

For example, you can set your background to hearts and your button color to red for a Valentine's Day promotion.

```css
.abra--valentines-10-activated {
  background-image: url('https://cdn.shopify.com/hearts.png');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.abra--valentines-10-activated .btn {
  background-color: #d6352b;
  color: #ffffff;
}
```

### JavaScript actions

#### `activateAndApply`

You can call this function to programatically activate and apply a promotion.

```javascript
window.Abra.activateAndApply('YOUR_CODE');
```

#### `activate`

You can call this function to programatically activate a promotion. When a promotion is activated and not applied, the customer will see the promotional content, but they won't receive the offers at checkout until they apply it.

```javascript
window.Abra.activate('YOUR_CODE');
```

#### `apply`

You can call this function to programatically apply a promotion's offers. When the promotion is applied, the customer will receive the offers at checkout.

```javascript
window.Abra.apply('YOUR_CODE');
```

#### `deactivateAndUnapply`

You can call this function to programatically deactivate and unapply a promotion.

```javascript
window.Abra.deactivateAndUnapply('YOUR_CODE');
```

#### `deactivate`

You can call this function to programatically activate a promotion. Make sure that the promotion hasn't been applied if you're calling this.

```javascript
window.Abra.deactivate('YOUR_CODE');
```

#### `unapply`

You can call this function to programatically unapply a promotion.

```javascript
window.Abra.unapply('YOUR_CODE');
```

### JavaScript events

#### `initialized`

This event is dispatched once Abra.js is initialized. Because it's possible your script runs before Abra is ready, you'll need to listen to this event on the window object.

For example, you can listen to this event and run additional logic.

```javascript
window.addEventListener('abra:initialized', event => {
  console.log('Abra is ready');
});
```

#### `activated`

This event is dispatched when a promotion is activated.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.addListener('activated', event => {
  console.log(`${event.detail.promotion} is activate`);
});

// Once you're ready to remove the listener
removeListener();
```

#### `applied`

This event is dispatched when a promotion's offers have been applied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.addListener('applied', event => {
  console.log(`${event.detail.promotion} is applied`);
});

// Once you're ready to remove the listener
removeListener();
```

#### `deactivated`

This event is dispatched when a promotion is deactivated.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.addListener('deactivated', event => {
  console.log('The promotion is deactivated');
});

// Once you're ready to remove the listener
removeListener();
```

#### `unapplied`

This event is dispatched when a promotion's offers have been unapplied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.addListener('unapplied', event => {
  console.log('The promotion is unapplied');
});

// Once you're ready to remove the listener
removeListener();
```

## Announcement bar

The announcement bar is an app embed you can enable for your store.

### CSS variables

| Name                                      | Description                                                                      | Value      |
| ----------------------------------------- | -------------------------------------------------------------------------------- | ---------- |
| `--abra-announcement-bar-background`      | The background of the announcement bar                                           | #000000    |
| `--abra-announcement-bar-border-color`    | The border color of the announcement bar                                         | #000000    |
| `--abra-announcement-bar-color`           | The color of the text in the announcement bar                                    | #FFFFFF    |
| `--abra-announcement-bar-font-size`       | The font size of the text in the announcement bar                                | 14px       |
| `--abra-announcement-bar-gap`             | The space between the icon and the text in the announcement bar                  | 1rem       |
| `--abra-announcement-bar-height`          | The height of the announcement bar<br />You can set this to improve layout shift | calculated |
| `--abra-announcement-bar-icon-color`      | The color of the icon in the announcement bar                                    | #FFFFFF    |
| `--abra-announcement-bar-icon-size`       | The size of the icon in the announcement bar                                     | 32px       |
| `--abra-announcement-bar-justify-content` | The alignment of the text in the announcement bar                                | center     |
| `--abra-announcement-bar-padding-x`       | The horizontal padding inside of the announcement bar                            | 1rem       |
| `--abra-announcement-bar-padding-y`       | The vertical padding inside of the announcement bar                              | 1rem       |
| `--abra-announcement-bar-z-index`         | The z-index of the announcement bar                                              | 4          |

For example, you can change the colors and the padding to match your online store.

```css
.abra-announcement-bar {
  --abra-announcement-bar-background: rgba(246, 246, 247, 1);
  --abra-announcement-bar-color: rgba(32, 34, 35, 1);
  --abra-announcement-bar-padding-x: 2rem;
  --abra-announcement-bar-padding-y: 1.25rem;
}
```

### CSS classes

| Name                              | Description                                                               |
| --------------------------------- | ------------------------------------------------------------------------- |
| `.abra-announcement-bar-block`    | The element wrapping the announcement bar                                 |
| `.abra-announcement-bar`          | The root element                                                          |
| `.abra-announcement-bar__content` | The element wrapping the text, and icon if present                        |
| `.abra-announcement-bar__icon`    | The element wrapping the SVG for the icon                                 |
| `.abra-announcement-bar__item`    | The element wrapping the slide for this content                           |
| `.abra-announcement-bar__link`    | The link element                                                          |
| `.abra-announcement-bar__text`    | The element used for content                                              |
| `.abra-announcement-bar--show`    | A modifier class applied to the root element to show the announcement bar |

For example, you can change the text element entirely.

```css
.abra-announcement-bar__text {
  letter-spacing: 0.1rem;
  line-height: 1.3;
  text-transform: none;
}
```

### JavaScript actions

#### `show`

You call this function to programatically show the announcement bar.

```javascript
window.Abra.AnnouncementBar.show();

// or

window.Abra.AnnouncementBar.show({
  text: 'Summer sale',
});
```

#### `hide`

You call this function to programatically hide the announcement bar.

```javascript
window.Abra.AnnouncementBar.hide();
```

#### `render`

You call this function to programatically render the announcement bar with new options.

| Name | Description                | Value                                       |
| ---- | -------------------------- | ------------------------------------------- |
| icon | The name of the icon       | discount \| gift \| percentage \| undefined |
| text | The text for the paragraph | string \| undefined                         |

For example, you can render the announcement bar with an icon.

```javascript
window.Abra.AnnouncementBar.render({
  icon: 'gift',
  text: 'Summer sale',
});
```

### JavaScript events

#### `shown`

This event is dispatched after the announcement bar is shown from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.AnnouncementBar.addListener(
  'shown',
  event => {
    console.log('The announcement bar is visible');
  },
);

// Once you're ready to remove the listener
removeListener();
```

#### `hidden`

This event is dispatched after the announcement bar is hidden from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.AnnouncementBar.addListener(
  'hidden',
  event => {
    console.log('The announcement bar is hidden');
  },
);

// Once you're ready to remove the listener
removeListener();
```

## Banner

The banner is an app block you can add to any page on your store.

### CSS variables

| Name                            | Description                                           | Value   |
| ------------------------------- | ----------------------------------------------------- | ------- |
| `--abra-banner-background`      | The background of the banner                          | #000000 |
| `--abra-banner-border-radius`   | The border radius of the banner                       | 0       |
| `--abra-banner-color`           | The color of the text in the banner                   | #FFFFFF |
| `--abra-banner-font-size`       | The font size of the text in the banner               | 14px    |
| `--abra-banner-gap`             | The space between the icon and the text in the banner | 1rem    |
| `--abra-banner-icon-color`      | The color of the icon in the banner                   | #FFFFFF |
| `--abra-banner-icon-size`       | The size of the icon in the banner                    | 32px    |
| `--abra-banner-justify-content` | The alignment of the text in the banner               | center  |
| `--abra-banner-margin-x`        | The horizontal space around the banner                | 1rem    |
| `--abra-banner-margin-y`        | The vertical space around the banner                  | 1rem    |
| `--abra-banner-padding-x`       | The horizontal padding inside of the banner           | 1rem    |
| `--abra-banner-padding-y`       | The vertical padding inside of the banner             | 1rem    |

For example, you can change the colors and the spacing to match your online store.

```css
.abra-banner {
  --abra-banner-background: rgba(246, 246, 247, 1);
  --abra-banner-color: rgba(32, 34, 35, 1);
  --abra-banner-padding-x: 2rem;
  --abra-banner-padding-y: 1.25rem;
}
```

### CSS classes

| Name                    | Description                                                     |
| ----------------------- | --------------------------------------------------------------- |
| `.abra-banner-block`    | The element wrapping the banner                                 |
| `.abra-banner`          | The root element                                                |
| `.abra-banner--show`    | A modifier class applied to the root element to show the banner |
| `.abra-banner__content` | The element wrapping the text, and icon if present              |
| `.abra-banner__icon`    | The element wrapping the SVG for the icon                       |
| `.abra-banner__link`    | The link element                                                |
| `.abra-banner__text`    | The element used for content                                    |

For example, you can change the text element entirely.

```css
.abra-banner__link {
  text-decoration: none;
}

.abra-banner__text {
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}
```

### JavaScript actions

#### `show`

You call this function to programatically show a banner, where the first parameter is the identifier from the app block settings.

For example, you can show a banner.

```javascript
window.Abra.Banner.show('default');

// or

window.Abra.Banner.show('default', {
  text: 'Get a free sample',
});
```

#### `hide`

You call this function to programatically hide a banner, where the first parameter is the identifier from the app block settings.

For example, you can hide a banner with the name of `default`.

```javascript
window.Abra.Banner.hide('default');
```

### JavaScript events

#### `shown`

This event is dispatched after the banner is shown from a promotion being applied, where the first parameter is the identifier from the app block settings.

For example, you can listen to this event and run additional logic for a banner with an id of `default`.

```javascript
const removeListener = window.Abra.Banner.addListener(
  'default',
  'shown',
  event => {
    console.log('default is visible');
  },
);

// Once you're ready to remove the listener
removeListener();
```

#### `hidden`

This event is dispatched after the banner is hidden from a promotion being applied, where the first parameter is the identifier from the app block settings.

For example, you can listen to this event and run additional logic for a banner with an id of `default`.

```javascript
const removeListener = window.Abra.Banner.addListener(
  'default',
  'hidden',
  event => {
    console.log('default is hidden');
  },
);

// Once you're ready to remove the listener
removeListener();
```

## Popup

The popup is an app embed you can enable for your store.

### CSS variables

| Name                           | Description                                     | Value   |
| ------------------------------ | ----------------------------------------------- | ------- |
| `--abra-popup-background`      | The background of the popup                     | #000000 |
| `--abra-popup-close-icon-size` | The size of the close icon                      | 1.6rem  |
| `--abra-popup-color`           | The color of the text in the popup              | #FFFFFF |
| `--abra-popup-font-size`       | The font size of the text in the popup          | 14px    |
| `--abra-popup-gap`             | The space between the text and the close button | 1rem    |
| `--abra-popup-icon-color`      | The color of the icon in the popup              | #FFFFFF |
| `--abra-popup-icon-size`       | The size of the icon in the popup               | 32px    |
| `--abra-popup-margin-x`        | The horizontal space around the popup           | 1rem    |
| `--abra-popup-margin-y`        | The vertical space around the popup             | 1rem    |
| `--abra-popup-padding-x`       | The horizontal padding inside of the popup      | 1rem    |
| `--abra-popup-padding-y`       | The vertical padding inside of the popup        | 1rem    |
| `--abra-popup-z-index`         | The z-index of the popup                        | 4       |

For example, you can change the colors and the spacing to match your online store.

```css
.abra-popup {
  --abra-popup-background: rgba(246, 246, 247, 1);
  --abra-popup-color: rgba(32, 34, 35, 1);
  --abra-popup-gap: 2rem;
  --abra-popup-padding-x: 2rem;
  --abra-popup-padding-y: 1.25rem;
}
```

### CSS classes

| Name                         | Description                                                    |
| ---------------------------- | -------------------------------------------------------------- |
| `.abra-popup-block`          | The element wrapping the popup                                 |
| `.abra-popup`                | The root element                                               |
| `.abra-popup--bottom-center` | A modifier class applied to the root element for placement     |
| `.abra-popup--bottom-left`   | A modifier class applied to the root element for placement     |
| `.abra-popup--bottom-right`  | A modifier class applied to the root element for placement     |
| `.abra-popup--show`          | A modifier class applied to the root element to show the popup |
| `.abra-popup__close`         | The element wrapping the close button                          |
| `.abra-popup__close-button`  | The close button element                                       |
| `.abra-popup__content`       | The element wrapping the text, and icon if present             |
| `.abra-popup__icon`          | The element wrapping the SVG for the icon                      |
| `.abra-popup__text`          | The element used for content                                   |

For example, you can change the text element entirely.

```css
.abra-popup__text {
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}
```

### JavaScript actions

#### `show`

You call this function to programatically show the popup.

For example 1, you can show the popup.

```javascript
window.Abra.Popup.show();

// or

window.Abra.Popup.show({
  text: '20% off storewide',
});
```

For example 2, you can show the popup and set it to automatically close after 3 seconds.

```javascript
window.Abra.Popup.show({ autohide: 3000 });
```

#### `hide`

You call this function to programatically hide the popup.

```javascript
window.Abra.Popup.hide();
```

### JavaScript events

#### `shown`

This event is dispatched after the popup is visible from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.Popup.addListener('shown', event => {
  console.log('The popup is visible');
});

// Once you're ready to remove the listener
removeListener();
```

#### `hidden`

This event is dispatched after the popup is hidden from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.Popup.addListener('hidden', event => {
  console.log('The popup is hidden');
});

// Once you're ready to remove the listener
removeListener();
```

## Price

The price element after you've activated a promotion on your store.

### CSS variables

| Name                              | Description                                        | Value        |
| --------------------------------- | -------------------------------------------------- | ------------ |
| `--abra-price-font-size`          | The font size for both prices                      | 1rem         |
| `--abra-price-gap`                | The space between the regular price and sale price | 0.6rem       |
| `--abra-regular-price-color`      | The color of the regular price                     | unset        |
| `--abra-regular-price-decoration` | The text decoration of the regular price           | line-through |
| `--abra-regular-price-font-size`  | The font size of the regular price                 | 0.9em        |
| `--abra-sale-price-color`         | The color of the sale price                        | #FF0000      |
| `--abra-sale-price-decoration`    | The text decoration of the sale price              | none         |
| `--abra-sale-price-font-size`     | The font size of the sale price                    | unset        |

For example, you can change the colors and the spacing to match your online store.

```css
.abra-price {
  --abra-price-gap: 2rem;
  --abra-regular-price-color: rgba(32, 34, 35, 1);
  --abra-sale-price-color: #0000ff;
}
```

### CSS classes

| Name                         | Description                                   |
| ---------------------------- | --------------------------------------------- |
| `.abra-price`                | The root element                              |
| `.abra-price__item`          | A price element                               |
| `.abra-price__item--regular` | A modifier class applied to the regular price |
| `.abra-price__item--sale`    | A modifier class applied to the sale price    |

For example, you can change the sale price entirely.

```css
.abra-price__item--sale {
  background-color: red;
  border-radius: 50%;
  color: black;
  letter-spacing: 0.1rem;
  padding: 0.6rem 1rem;
}
```
