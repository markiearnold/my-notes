# CSS Animation Keyframes


## Example

```css
div {
  width: 50px;
  height: 40px;
  background: blue;
  position: relative;
  left: 500px;
  -webkit-animation: slideIn 2s forwards;
  -moz-animation: slideIn 2s forwards;
  animation: slideIn 2s forwards;
}
```

```css
@-webkit-keyframes slideIn {
  0% {
    transform: translateX(-900px);
  }
  100% {
    transform: translateX(0);
  }
}
@-moz-keyframes slideIn {
  0% {
    transform: translateX(-900px);
  }
  100% {
    transform: translateX(0);
  }
}
@keyframes slideIn {
  0% {
    transform: translateX(-900px);
  }
  100% {
    transform: translateX(0);
  }
}
```

## Properties
* @keyframes
* animation-name
* animation-duration
* animation-delay
* animation-iteration-count
* animation-direction
* animation-timing-function
* animation-fill-mode
* animation

