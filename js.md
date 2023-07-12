# Use the JavaScript SDK

!> If you're new to working with JavaScript, we recommend that you contact us to integrate with your theme.

Abra provides a JavaScript SDK with many helpers, events and dispatchers for the different parts of your promotions. You can programmatically control these blocks and make custom experiences on your online store.

## Promotion

### Methods

#### `activate`

You can call this function to programmatically announce and apply a promotion.

```javascript
window.Abra.activate('YOUR_CODE');
```

#### `deactivate`

You can call this function to programmatically deactivate a promotion.

```javascript
window.Abra.deactivate('YOUR_CODE');
```

### Events

#### `initialized`

This event is dispatched once Abra.js is initialized.

> Note: You'll need to listen to this event on the `window` object because it's possible your script runs before Abra is ready.

```javascript
window.addEventListener('abra:initialized', event => {
  console.log('Abra is ready');
});
```

#### `activated`

This event is dispatched when a promotion is activated.

```javascript
const removeListener = window.Abra.addListener('activated', event => {
  console.log(`${event.detail.promotion} is activate`);
});

// Once you're ready to remove the listener
removeListener();
```

#### `deactivated`

This event is dispatched when a promotion is deactivated.

```javascript
const removeListener = window.Abra.addListener('deactivated', event => {
  console.log('The promotion is deactivated');
});

// Once you're ready to remove the listener
removeListener();
```

## Announcement bar block

### Methods

#### `show`

You call this function to programmatically show the announcement bar.

```javascript
window.Abra.AnnouncementBar.show();

// or

window.Abra.AnnouncementBar.show({
  text: 'Summer sale',
});
```

#### `hide`

You call this function to programmatically hide the announcement bar.

```javascript
window.Abra.AnnouncementBar.hide();
```

#### `render`

You call this function to programmatically render the announcement bar with new options.

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

### Events

#### `shown`

This event is dispatched after the announcement bar is shown from a promotion being applied.

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

## Banner block

### Methods

#### `show`

You call this function to programmatically show a banner, where the first parameter is the identifier from the app block settings.

```javascript
window.Abra.Banner.show('default');

// or

window.Abra.Banner.show('default', {
  text: 'Get a free sample',
});
```

#### `hide`

You call this function to programmatically hide a banner, where the first parameter is the identifier from the app block settings.

```javascript
window.Abra.Banner.hide('default');
```

### Events

#### `shown`

This event is dispatched after the banner is shown from a promotion being applied, where the first parameter is the identifier from the app block settings.

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

## Popup block

### Methods

#### `show`

You call this function to programmatically show the popup.

```javascript
window.Abra.Popup.show();

// or

window.Abra.Popup.show({
  text: '20% off storewide',
});
```

#### `hide`

You call this function to programmatically hide the popup.

```javascript
window.Abra.Popup.hide();
```

### Events

#### `shown`

This event is dispatched after the popup is visible from a promotion being applied.

```javascript
const removeListener = window.Abra.Popup.addListener('shown', event => {
  console.log('The popup is visible');
});

// Once you're ready to remove the listener
removeListener();
```

#### `hidden`

This event is dispatched after the popup is hidden from a promotion being applied.

```javascript
const removeListener = window.Abra.Popup.addListener('hidden', event => {
  console.log('The popup is hidden');
});

// Once you're ready to remove the listener
removeListener();
```
