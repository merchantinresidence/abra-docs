# Abra SDK

Welcome to Abra's developer documentations. We've built this Shopify app to be flexible and extensible. We know that your business needs as a merchant are diverse and we want Abra to work with, not against you.

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
| `--abra-announcement-bar-py`           | The vertical padding inside of the announcement bar   | 1rem    |
| `--abra-announcement-bar-px`           | The horizontal padding inside of the announcement bar | 1rem    |

For example, you can change the colors and the padding to match your online store.

```css
:root {
  --abra-announcement-bar-background: rgba(246, 246, 247, 1);
  --abra-announcement-bar-color: rgba(32, 34, 35, 1);
  --abra-announcement-bar-py: 1.25rem;
  --abra-announcement-bar-px: 2rem;
}
```

### CSS classes

| Name                              | Description                                                                                      |
| --------------------------------- | ------------------------------------------------------------------------------------------------ |
| `.abra-announcement-bar-block`    | The `<div />` element wrapping the announcement bar                                              |
| `.abra-announcement-bar`          | The `<abra-announcement-bar />` element                                                          |
| `.abra-announcement-bar__item`    | The `<div />` element wrapping the text, or link if present                                      |
| `.abra-announcement-bar__link`    | The `<a />` element                                                                              |
| `.abra-announcement-bar__heading` | The `<h2 />` element used for content                                                            |
| `.abra-announcement-bar__text`    | The `<p />` element used for content                                                             |
| `.abra-announcement-bar--compact` | A modifier class applied to the `<abra-announcement-bar />` element when the compact style is on |

For example, you can change the heading element entirely.

```css
.abra-announcement-bar__heading {
  font-size: 2rem;
  letter-spacing: 0.1rem;
  text-transform: none;
}
```

### JavaScript

#### `abra:announcement-bar:rendered`

This event is dispatched after the announcement bar renders from a promotion being applied. The event will return the value of the element that has changed.

| Name    | Description                | Value               |
| ------- | -------------------------- | ------------------- |
| heading | The text for the heading   | string \| undefined |
| link    | The URL for the link       | string \| undefined |
| text    | The text for the paragraph | string \| undefined |

You can listen to this event and run additional logic.

```javascript
window.addEventListener('abra:announcement-bar:rendered', event => {
  if (event.detail.heading) {
    console.log('The heading has changed');
  }
});
```
