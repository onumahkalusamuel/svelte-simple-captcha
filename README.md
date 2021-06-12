# svelte-simple-captcha

A simple HTML5 Captcha for Svelte.

## Installation

```bash
$ npm i svelte-simple-captcha
```

or

```bash
$ yarn add svelte-simple-captcha
```

## Usage

There is one export: `Captcha`
Import `Captcha` into any page / component you need it. Then add it as markup, anywhere in the markup section.

```svelte
<script>
...
import { Captcha } from 'svelte-simple-captcha'
...
</script>
...
<Captcha />
...
```

### Attributes

You can bind the following attributes:

| Attribute  | Description                                 |
| :--------- | :------------------------------------------ |
| `answer`   | The answer provided by the user. (required) |
| `width`    | Box width. Default=`160`                    |
| `height`   | Box height. Default=`60`                    |
| `fontSize` | Size of display font. Default=`40`          |

### Actions

Listen to the `verified` action to know when the input `answer` is correct.
## Example

```svelte
<script>
import { Captcha } from 'svelte-simple-captcha';
let answer = '';
let verified = false;
</script>

<input bind:value={answer} type='number' placeholder='Enter Captcha Answer'/>
<Captcha {answer} on:verified={(ctx) => verified = ctx.detail} />

<!-- You can bind `verified` to the submit button or handler -->
```

## License

**[MIT](LICENSE)** Licensed

---

Got something interesting to share with me? Hit me up on [Twitter](https://twitter.com/@SKOnumah)
