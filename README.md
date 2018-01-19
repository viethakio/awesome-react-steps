# React Steps

A set of steppers components for you to use in your react projects.

## Examples

### Arrows

![default](./docs/screenshots/arrows/default.png)
![custom blue](./docs/screenshots/arrows/blue.png)
![custom gold/pink](./docs/screenshots/arrows/gold-pink.png)
![custom dark](./docs/screenshots/arrows/dark.png)
![custom dark](./docs/screenshots/arrows/red.png)

> It's only implemented Arrows stepper until now, but more steppers will be available soon. :)

## Quick usage

The quickest way for you to use a stepper component in your project is by using a package manager to install it, and a ES6 ready environment.

```shell
npm install awesome-react-steps
# or
yarn add awesome-react-steps
```

```js
import "./node_module/awesome-react-steps/lib/css/arrows.css";
import { Arrows } from "awesome-react-steps";

//...

<Arrows
  model={{
    steps: [
      { label: "Step one" },
      { label: "Step two" },
      { label: "Step three" }
    ],
    current: 0
  }}
/>;
```

## Within a container

In a real project you won't actually use the quick example as shown above, you will probably use it inside a container component, for managing its state.

In this situation you better choose `StepsModel` object instead of plain Javascript object, because it provides some API for you to mutate your state easily.

```js
import React from "react";
import { Arrows, StepsModel } from "awesome-react-steps";

class MyContainer extends Component {
  constructor(props) {
    super(props);
    this.state = {
      stepsModel: new StepsModel([
        { label: "Step one" },
        { label: "Second step" },
        { label: "Another step" },
        { label: "Last step" }
      ])
    };
  }

  render() {
    return (
      <div>
        <Arrows model={this.state.stepsModel} />
        <button onClick={this.back.bind(this)}>Back</button>
        <button onClick={this.advance.bind(this)}>Advance</button>
      </div>
    );
  }

  advance() {
    this.setState(prevState => ({
      stepsModel: prevState.stepsModel.next()
    }));
  }

  back() {
    this.setState(prevState => ({
      stepsModel: prevState.stepsModel.previous()
    }));
  }
}
```

## Coming features

* New steppers types

## API

### StepsModel class

```js
import { StepsModel } from "awesome-react-steps";
```

#### Constructing

Without arguments:

```js
let model = new StepsModel();
model = model.addStep({ label: "First step" });
```

With an array of steps:

```js
const model = new StepsModel([{ label: "First step" }, { label: "Last step" }]);
```

With an object:

```js
const model = new StepsModel({
  steps: [{ label: "One step" }, { label: "Other step" }],
  current: 1
});
```

#### Setting step states

```js
// You can set the current step state using these functions
model = model.skip();
model = model.done();
model = model.invalidate();

// You can also set it directly
model = model.setStepState(myNewState);
```

#### Moving throw steps

```js
/// You can move around using these functions
model = model.next();
model = model.previous();

// You can also set the current step directly
model = model.setCurrent(2);
```

### StepState type

```js
import { StepState } from "awesome-react-steps";
```

```js
// The following states are available
StepState.UNTOUCHED;
StepState.DONE;
StepState.SKIPPED;
StepState.INVALID;
```

> These states are used by each stepper for rendering. Not all steppers will use all these states when rendering. But in your custom styles you can render steps using their states.

## Customizing styles

### Arrows

The classes used for each part of the stepper:

```css
/* The root element of the Arrows stepper. The background should be customized in this class.  */
.Arrows {
}

/* The element which holds a step */
.Arrows--step {
}

/* The SVG element used to draw the arrow in the background of each step */
.Arrows--step--arrow {
}

/* The elements for the number and the label of each step */
.Arrows--step--number {
}
.Arrows--step--label {
}
```

The classes for the states of the stepper. You can combine these one with the classes of the stepper parts to custom the rendering style for different states of the stepper.

```css
/* Current step */
.Arrows--step__current {
}

/* Steps before the current step */
.Arrows--step__passed {
}

/* Steps after the current step */
.Arrows--step__coming {
}

/* Invalid step */
.Arrows--step__invalid {
}

/* Step is done */
.Arrows--step__done {
}

/* Step was skipped */
.Arrows--step__skipped {
}
```

## Contributing

Open an issue if you encounter a bug or want some new feature. We will appreciate if you write us some pull requests too.

## License

MIT License
