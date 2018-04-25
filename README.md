# React-Number-Format
React component to format number in an input or as a text

### Features
1. Prefix, suffix and thousand separator.
2. Custom format pattern.
3. Masking.
4. Custom formatting handler.
5. Formatting a input or a simple text.


### Usage
ES6
```js
import NumberFormat from 'react-number-format';
```

ES5
```js
const NumberFormat = require('react-number-format');
```

Typescript
```js
import * as NumberFormat from 'react-number-format';
```

#### Format with pattern : Format credit card in an input
```jsx
<NumberFormat format="#### #### #### ####" />
```
![Screencast example](https://i.imgur.com/KEiYp4o.gif)

#### Format with mask : Format credit card in an input
```jsx
<NumberFormat format="#### #### #### ####" mask="_"/>
```
![Screencast example](https://i.imgur.com/qvmydpH.gif)


#### Format with mask as array
Mask can also be a array of string. Each item corresponds to the same index #.
```jsx
<NumberFormat format="##/##" placeholder="MM/YY" mask={['M', 'M', 'Y', 'Y']}/>
```
![Screencast example](https://media.giphy.com/media/xT9IgojmLf6x3jX0nS/giphy.gif)

#### Custom format method  : Format credit card expiry time
```jsx
function limit(val, max) {
  if (val.length === 1 && val[0] > max[0]) {
    val = '0' + val;
  }

  if (val.length === 2) {
    if (Number(val) === 0) {
      val = '01';

    //this can happen when user paste number
  } else if (val > max) {
      val = max;
    }
  }

  return val;
}

function cardExpiry(val) {
  let month = limit(val.substring(0, 2), '12');
  let year = val.substring(2, 4);

  return month + (year.length ? '/' + year : '');
}

<NumberFormat format={cardExpiry}/>
```
![Screencast example](https://i.imgur.com/9wwdyFF.gif)

### Format phone number
```jsx
<NumberFormat format="+1 (###) ###-####" mask="_"/>
```
![Screencast example](https://media.giphy.com/media/l1J9wJ6ZSONO7cXkI/giphy.gif)

### Custom Inputs
You can easily extend your custom input with number format. But custom input should have all input props.
```jsx
  import TextField from 'material-ui/TextField';
```

```jsx
  <NumberFormat customInput={TextField} format="#### #### #### ####"/>
```
![Screencast example](https://media.giphy.com/media/3og0IH0LJhIQWFxztC/giphy.gif)

**Passing custom input props**
All custom input props and number input props are passed together.
```jsx
  <NumberFormat hintText="Some placeholder" value={this.state.card} customInput={TextField} format="#### #### #### ####"/>
```

### Live Demo
[http://codepen.io/s-yadav/pen/bpKNMa](http://codepen.io/s-yadav/pen/bpKNMa)

### Show your support
[:star: this repo](https://github.com/s-yadav/react-number-format)

### Development
- Download the zip
- `npm install`
- `npm start` to run example server
- `npm run test` to test changes
- `npm run bundle` to bundle files

#### Testing
Test cases are written in jasmine and run by karma
Test file : /test/test_input.js
To run test : `npm run test`
