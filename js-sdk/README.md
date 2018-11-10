# industrycoin SDK

## Dynamic Widget

### Example

Step 1: Include the JavaScript SDK on your page once, ideally right after the opening body tag.

```html
<div id="gc-root"></div>
<script>(function(d, s, id) {
  var js, gjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = "https://unpkg.com/industrycoin-sdk";
  gjs.parentNode.insertBefore(js, gjs);
}(document, 'script', 'industrycoin-jssdk'));</script>
```

Step 2: Place this code wherever you want the plugin to appear on your page.

```html
<div class="industrycoin-widget"
  data-limit="2"
  data-order-by="-expires_date"
  data-organization="MetaMask"
  data-repository="metamask-extension"
></div>
```

### Autoloading

Importing the SDK into your application will attempt to autoload the widget by searching for '.industrycoin-widget' selectors

```javascript
import 'industrycoin-sdk';
```
or
```javascript
require('industrycoin-sdk');
```

### Programmatically

You can also use the Widget programmatically.

```javascript
import { Widget } from 'industrycoin-sdk';
```
or
```javascript
const { Widget } = require('industrycoin-sdk');
```

Widget can be instantiated by passing a selector option, or an element reference.

```javascript
new Widget({
  limit: 10,
  orderBy: '-expires_date',
  organization: 'MetaMask',
  repository: 'metamask-extension',
  selector: '.industrycoin-widget',
});
```
