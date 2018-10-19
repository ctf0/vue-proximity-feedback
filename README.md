<h1 align="center" style="border: none">
    Vue Proximity Feedback
    <br>
    <a href="https://www.npmjs.com/package/vue-proximity-feedback"><img src="https://img.shields.io/npm/v/vue-proximity-feedback.svg?style=for-the-badge" alt="npm" /></a> <a href="https://www.npmjs.com/package/vue-proximity-feedback"><img src="https://img.shields.io/npm/dt/vue-proximity-feedback.svg?style=for-the-badge" alt="npm" /></a>
</h1>

## Installation

```bash
npm install vue-proximity-feedback --save
```

<br>

## Usage

- register the component.

    ```js
    window.Vue = require('vue')

    Vue(ProximityFeedback, require('vue-proximity-feedback'))
    ```

- create a css animation
    ```css
    @keyframes pulse {
        to {
            transform: scale(1.4);
        }
    }

    .pulse {
        animation: pulse 0.25s ease infinite alternate;
    }
    ```

- usage
    ```vue
    <proximity-feedback
        ref="pfb"
        tag="div"
        animation-class="pulse"
        :distance="{min: 10, max: 400}"
        :divide-by="125"
        @click.native="doSomthing()">

        <i class="fa-search"></i>
    </proximity-feedback>
    ```

    - you can conditionaly start / stop the mouse tracking through
        ```vue
        this.$refs.pfb.stop()
        this.$refs.pfb.start()
        ```

    |      prop      |      required      |  type  |      default       |              description               |
    |----------------|--------------------|--------|--------------------|----------------------------------------|
    | tag            | :x:                | string | span               |                                        |
    | animationClass | :white_check_mark: | string |                    |                                        |
    | distance       | :x:                | object | {min: 0, max: 100} |                                        |
    | divideBy       | :x:                | number | 100                | proximity / divideBy = animation speed |

<br>

## TODO
- fix frame stutter when animation speed change.
