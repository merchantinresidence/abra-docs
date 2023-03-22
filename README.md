# Abra Developer Docs

Welcome to Abra's developer docs! We know that your business needs as a merchant are diverse and we want Abra to work for you, not against you.

Many of our components are customizable at different levels depending on how much you need to change. We'll walk through each level in detail.

## Announcement bar

The announcement bar is an app embed you can enable for your store.

### CSS variables

| Name                                   | Description                                                                      | Value      |
| -------------------------------------- | -------------------------------------------------------------------------------- | ---------- |
| `--abra-announcement-bar-background`   | The background of the announcement bar                                           | #000000    |
| `--abra-announcement-bar-border-color` | The border color of the announcement bar                                         | #000000    |
| `--abra-announcement-bar-color`        | The color of the text in the announcement bar                                    | #FFFFFF    |
| `--abra-announcement-bar-font-size`    | The font size of the text in the announcement bar                                | 14px       |
| `--abra-announcement-bar-height`       | The height of the announcement bar<br />You can set this to improve layout shift | calculated |
| `--abra-announcement-bar-padding-x`    | The horizontal padding inside of the announcement bar                            | 1rem       |
| `--abra-announcement-bar-padding-y`    | The vertical padding inside of the announcement bar                              | 1rem       |
| `--abra-announcement-bar-text-align`   | The alignment of the text in the announcement bar                                | center     |
| `--abra-announcement-bar-z-index`      | The z-index of the announcement bar                                              | 4          |

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

| Name                              | Description                                                                            |
| --------------------------------- | -------------------------------------------------------------------------------------- |
| `.abra-announcement-bar-block`    | The element wrapping the announcement bar                                              |
| `.abra-announcement-bar`          | The root element                                                                       |
| `.abra-announcement-bar--compact` | A modifier class applied to the root element when the compact style setting is enabled |
| `.abra-announcement-bar--show`    | A modifier class applied to the root element to show the announcement bar              |
| `.abra-announcement-bar__heading` | The element used for heading content                                                   |
| `.abra-announcement-bar__item`    | The element wrapping the text, or link if present                                      |
| `.abra-announcement-bar__link`    | The link element                                                                       |
| `.abra-announcement-bar__text`    | The element used for content                                                           |

For example, you can change the heading element entirely.

```css
.abra-announcement-bar__heading {
  letter-spacing: 0.1rem;
  line-height: 1.3;
  text-transform: none;
}
```

### JavaScript actions

#### `abra:announcement-bar:show`

You can dispatch this event to programatically show the announcement bar.

```javascript
window.Abra.AnnouncementBar.show();

// or

window.Abra.AnnouncementBar.show({
  heading: 'Summer sale',
  link: '/collections/summer-sale',
});
```

#### `abra:announcement-bar:hide`

You can dispatch this event to programatically hide the announcement bar.

```javascript
window.Abra.AnnouncementBar.hide();
```

#### `abra:announcement-bar:render`

You can dispatch this event to programatically render the announcement bar with new options.

| Name    | Description                | Value               |
| ------- | -------------------------- | ------------------- |
| heading | The text for the heading   | string \| undefined |
| link    | The URL for the link       | string \| undefined |
| text    | The text for the paragraph | string \| undefined |

For example, you can render the announcement bar with a link.

```javascript
window.Abra.AnnouncementBar.render({
  heading: 'Summer sale',
  link: '/collections/summer-sale',
});
```

### JavaScript events

#### `abra:announcement-bar:shown`

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

#### `abra:announcement-bar:hidden`

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

| Name                          | Description                                 | Value   |
| ----------------------------- | ------------------------------------------- | ------- |
| `--abra-banner-background`    | The background of the banner                | #000000 |
| `--abra-banner-border-radius` | The border radius of the banner             | 0       |
| `--abra-banner-color`         | The color of the text in the banner         | #FFFFFF |
| `--abra-banner-font-size`     | The font size of the text in the banner     | 14px    |
| `--abra-banner-margin-x`      | The horizontal space around the banner      | 1rem    |
| `--abra-banner-margin-y`      | The vertical space around the banner        | 1rem    |
| `--abra-banner-padding-x`     | The horizontal padding inside of the banner | 1rem    |
| `--abra-banner-padding-y`     | The vertical padding inside of the banner   | 1rem    |

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

| Name                     | Description                                                        |
| ------------------------ | ------------------------------------------------------------------ |
| `.abra-banner-block`     | The element wrapping the banner                                    |
| `.abra-banner`           | The root element                                                   |
| `.abra-banner--show`     | A modifier class applied to the root element to show the banner    |
| `.abra-banner--{{ id }}` | A modifier class applied to the root element for a specific banner |
| `.abra-banner__heading`  | The element used for heading content                               |
| `.abra-banner__link`     | The link element                                                   |
| `.abra-banner__text`     | The element used for content                                       |

For example, you can change the text element entirely.

```css
.abra-banner--banner-1 {
  background-color: purple;
}

.abra-banner__link {
  text-decoration: none;
}

.abra-banner__text {
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}
```

### JavaScript actions

#### `abra:banner:{{ id }}:show`

You can dispatch this event to programatically show a banner, where `{{ id }}` is the identifier from the app block settings.

For example, you can show a banner with the id of `banner-1`.

```javascript
window.Abra.Banner.show('banner-1');
```

#### `abra:banner:{{ id }}:hide`

You can dispatch this event to programatically hide a banner, where `{{ id }}` is the identifier from the app block settings.

For example, you can hide a banner with the id of `banner-1`.

```javascript
window.Abra.Banner.hide('banner-1');
```

### JavaScript events

#### `abra:banner:{{ id }}:shown`

This event is dispatched after the banner is shown from a promotion being applied, where `{{ id }}` is the identifier from the app block settings.

For example, you can listen to this event and run additional logic for a banner with an id of `banner-1`.

```javascript
const removeListener = window.Abra.Banner.addListener(
  'banner-1',
  'shown',
  event => {
    console.log('banner-1 is visible');
  },
);

// Once you're ready to remove the listener
removeListener();
```

#### `abra:banner:{{ id }}:hidden`

This event is dispatched after the banner is hidden from a promotion being applied, where `{{ id }}` is the identifier from the app block settings.

For example, you can listen to this event and run additional logic for a banner with an id of `banner-1`.

```javascript
const removeListener = window.Abra.Banner.addListener(
  'banner-1',
  'hidden',
  event => {
    console.log('banner-1 is hidden');
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

| Name                        | Description                                                    |
| --------------------------- | -------------------------------------------------------------- |
| `.abra-popup-block`         | The element wrapping the popup                                 |
| `.abra-popup`               | The root element                                               |
| `.abra-popup--bottom-left`  | A modifier class applied to the root element for placement     |
| `.abra-popup--bottom-right` | A modifier class applied to the root element for placement     |
| `.abra-popup--show`         | A modifier class applied to the root element to show the popup |
| `.abra-popup__close`        | The element wrapping the close button                          |
| `.abra-popup__close-button` | The close button element                                       |
| `.abra-popup__text`         | The element used for content                                   |

For example, you can change the text element entirely.

```css
.abra-popup__text {
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}
```

### JavaScript actions

#### `abra:popup:show`

You can dispatch this event to programatically show the popup.

For example 1, you can show the popup.

```javascript
window.Abra.Popup.show();
```

For example 2, you can show the popup and set it to automatically close after 3 seconds.

```javascript
window.Abra.Popup.show({ autohide: 3000 });
```

#### `abra:popup:hide`

You can dispatch this event to programatically hide the popup.

```javascript
window.Abra.Popup.hide();
```

### JavaScript events

#### `abra:popup:shown`

This event is dispatched after the popup is visible from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
const removeListener = window.Abra.Popup.addListener('shown', event => {
  console.log('The popup is visible');
});

// Once you're ready to remove the listener
removeListener();
```

#### `abra:popup:hidden`

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
