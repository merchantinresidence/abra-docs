# Customize the styling

!> If you're new to working with CSS, we recommend that you contact us to integrate with your theme.

Abra has many CSS variables and CSS classes you can override to style your online store when a promotion is active.

## Global styling

### CSS classes

| Name                          | Description                                                                                                          |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `.abra--initialized`          | A modifier class applied to the body element when Abra is initialized                                                |
| `.abra--activated`            | A modifier class applied to the body element when a promotion is active                                              |
| `.abra--applied`              | A modifier class applied to the body element when a promotion is applied                                             |
| `.abra--{{ code }}-activated` | A modifier class, where `{{ code }}` is your promotion code, applied to the body element when a promotion is active  |
| `.abra--{{ code }}-applied`   | A modifier class, where `{{ code }}` is your promotion code, applied to the body element when a promotion is applied |

#### Example

Change your background to hearts and your button color to red for a Valentine's Day promotion.

```css
.abra--VALENTINES-10-activated {
  background-image: url('https://cdn.shopify.com/hearts.png');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.abra--VALENTINES-10-activated .btn {
  background-color: #d6352b;
  color: #ffffff;
}
```

## Announcement bar styling

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

### Example

Change the announcement bar colors and customize the text styling

```css
.abra-announcement-bar {
  --abra-announcement-bar-background: rgba(246, 246, 247, 1);
  --abra-announcement-bar-color: rgba(32, 34, 35, 1);
  --abra-announcement-bar-padding-x: 2rem;
  --abra-announcement-bar-padding-y: 1.25rem;
}

.abra-announcement-bar__text {
  letter-spacing: 0.1rem;
  line-height: 1.3;
  text-transform: none;
}
```

## Banner styling

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

### Example

Change the colors and the spacing to match your online store and update text styling

```css
.abra-banner {
  --abra-banner-background: rgba(246, 246, 247, 1);
  --abra-banner-color: rgba(32, 34, 35, 1);
  --abra-banner-padding-x: 2rem;
  --abra-banner-padding-y: 1.25rem;
}

.abra-banner__text {
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}
```

## Popup styling

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

### Example

Change the colors and the spacing to match your online store and update text styling

```css
.abra-popup {
  --abra-popup-background: rgba(246, 246, 247, 1);
  --abra-popup-color: rgba(32, 34, 35, 1);
  --abra-popup-gap: 2rem;
  --abra-popup-padding-x: 2rem;
  --abra-popup-padding-y: 1.25rem;
}

.abra-popup__text {
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}
```

## Price styling

### CSS classes

| Name                          | Description                                    |
| ----------------------------- | ---------------------------------------------- |
| `.abra-price`                 | The root element                               |
| `.abra-price__item`           | A price element                                |
| `.abra-price__item--original` | A modifier class applied to the original price |
| `.abra-price__item--final`    | A modifier class applied to the final price    |

### CSS variables

| Name                               | Description                                          | Value        |
| ---------------------------------- | ---------------------------------------------------- | ------------ |
| `--abra-price-font-size`           | The font size for both prices                        | 1rem         |
| `--abra-price-gap`                 | The space between the original price and final price | 0.6rem       |
| `--abra-original-price-color`      | The color of the original price                      | unset        |
| `--abra-original-price-decoration` | The text decoration of the original price            | line-through |
| `--abra-original-price-font-size`  | The font size of the original price                  | 0.9em        |
| `--abra-final-price-color`         | The color of the final price                         | #FF0000      |
| `--abra-final-price-decoration`    | The text decoration of the final price               | none         |
| `--abra-final-price-font-size`     | The font size of the final price                     | unset        |

### Example

Change the colors and the spacing to match your online store and update text styling

```css
.abra-price {
  --abra-price-gap: 2rem;
  --abra-regular-price-color: rgba(32, 34, 35, 1);
  --abra-sale-price-color: #0000ff;
}

.abra-price__item--final {
  background-color: red;
  border-radius: 50%;
  color: black;
  letter-spacing: 0.1rem;
  padding: 0.6rem 1rem;
}
```
