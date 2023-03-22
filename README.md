# Abra Developer Docs

Welcome to Abra's developer docs! We know that your business needs as a merchant are diverse and we want Abra to work for you, not against you.

Many of our components are customizable at different levels depending on how much you need to change. We'll walk through each level in detail.

## Announcement bar

The announcement bar is an app embed you can enable for your store.

### CSS variables

| Name                                   | Description                                           | Value   |
| -------------------------------------- | ----------------------------------------------------- | ------- |
| `--abra-announcement-bar-background`   | The background of the announcement bar                | #000000 |
| `--abra-announcement-bar-border-color` | The border color of the announcement bar              | #000000 |
| `--abra-announcement-bar-color`        | The color of the text in the announcement bar         | #FFFFFF |
| `--abra-announcement-bar-font-size`    | The font size of the text in the announcement bar     | 14px    |
| `--abra-announcement-bar-text-align`   | The alignment of the text in the announcement bar     | center  |
| `--abra-announcement-bar-z-index`      | The z-index of the announcement bar                   | 4       |
| `--abra-announcement-bar-padding-y`    | The vertical padding inside of the announcement bar   | 1rem    |
| `--abra-announcement-bar-padding-x`    | The horizontal padding inside of the announcement bar | 1rem    |

For example, you can change the colors and the padding to match your online store.

```css
:root {
  --abra-announcement-bar-background: rgba(246, 246, 247, 1);
  --abra-announcement-bar-color: rgba(32, 34, 35, 1);
  --abra-announcement-bar-padding-y: 1.25rem;
  --abra-announcement-bar-padding-x: 2rem;
}
```

### CSS classes

| Name                              | Description                                                                            |
| --------------------------------- | -------------------------------------------------------------------------------------- |
| `.abra-announcement-bar-block`    | The element wrapping the announcement bar                                              |
| `.abra-announcement-bar`          | The root element                                                                       |
| `.abra-announcement-bar--compact` | A modifier class applied to the root element when the compact style setting is enabled |
| `.abra-announcement-bar__item`    | The element wrapping the text, or link if present                                      |
| `.abra-announcement-bar__link`    | The link element                                                                       |
| `.abra-announcement-bar__heading` | The element used for heading content                                                   |
| `.abra-announcement-bar__text`    | The element used for content                                                           |

For example, you can change the heading element entirely.

```css
.abra-announcement-bar__heading {
  font-size: 2rem;
  letter-spacing: 0.1rem;
  text-transform: none;
}
```

### JavaScript dispatchers

#### `abra:announcement-bar:render`

You can dispatch this event to programatically render the announcement bar with new options.

| Name    | Description                | Value               |
| ------- | -------------------------- | ------------------- |
| heading | The text for the heading   | string \| undefined |
| link    | The URL for the link       | string \| undefined |
| text    | The text for the paragraph | string \| undefined |

For example, you can render the announcement bar with a link.

```javascript
window.dispatchEvent(
  new CustomEvent('abra:announcement-bar:render', {
    detail: { heading: 'Summer sale', link: '/collections/summer-sale' },
  }),
);
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
:root {
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
| `.abra-popup--open`         | A modifier class applied to the root element to open the popup |
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

### JavaScript listeners

#### `abra:popup:opened`

This event is dispatched after the popup is opened from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
window.addEventListener('abra:popup:opened', event => {
  console.log('The popup opened');
});
```

#### `abra:popup:closed`

This event is dispatched after the popup is closed from a promotion being applied.

For example, you can listen to this event and run additional logic.

```javascript
window.addEventListener('abra:popup:closed', event => {
  console.log('The popup closed');
});
```

### JavaScript dispatchers

#### `abra:popup:open`

You can dispatch this event to programatically open the popup.

For example 1, you can open the popup.

```javascript
window.dispatchEvent(new CustomEvent('abra:popup:open'));
```

For example 2, you can open the popup and set it to automatically close after 3 seconds.

```javascript
window.dispatchEvent(
  new CustomEvent('abra:popup:open', { detail: { autoclose: 3000 } }),
);
```

#### `abra:popup:close`

You can dispatch this event to programatically close the popup.

```javascript
window.dispatchEvent(new CustomEvent('abra:popup:close'));
```
