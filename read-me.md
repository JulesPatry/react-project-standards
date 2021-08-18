# React Project Standards

In this read-me will contain the standards for writing react components. The goal in creating these standards is to define a writing style that a team can agree with. Once achieved it will improve the ability for an engineer to understand brand new react projects and empower them to contribue at a faster rate without surprises.

1. All React components should be written as a function to leverage hooks. Class components do not support hooks.
2. Higher Order Components, also known as HoCs should be replaced with hooks.
3. All React Components should be written with typescript.

```tsx
interface Props {
  // NOTE: name the react component's interface is always named as Props
  a: number;
  b: number;
}

export default function Sum({ a, b }: Props) {
  return <div>{a + b}</div>;
}
```

4. File imports should be organized, starting with react import if it exists and components should be separated from the helper functions

```tsx
// NOTE: react starts first
import { useState } from 'react';
// NOTE: helper/hook functions after
import helperFunction from 'helpers/helperFunction';

// Components (this is always last)
import HelloWorld from 'components/HelloWorld;';

interface Props {
  a: number;
  b: number;
}

export default function Sum({ a, b }: Props) {
  return <HelloWorld>{a + b}</HelloWorld>;
}
```

5. The ts-config should support file paths for all the root folders in src.

```json
{
  "compilerOptions": {
    // ....
    "baseUrl": "./",
    "paths": {
      "src": ["./*"],
      "components": ["components/*"],
      "helpers": ["helpers/*"],
      "hooks": ["hooks/*"],
      "pages": ["pages/*"],
      "styles": ["styles/*"],
      "types": ["types/*"]
    }
  }
}
```

6. The src folders should be like the following

```json
/components -- All components go here
/helpers -- All helpers such as models and misc functions go here. And it should be one file per function
/hooks -- Same as helpers expect it's hooks
/pages -- Next.js Page components go here. These components should be bare and rely on components to display logic
/styles -- The theme should live in here
/types -- Global types should belong here.
```

7. JSS over CSS. JSS fixes the problem of css global variables and can override theming with javascript.

8. An example of the styles folder

global.css - useful for overriding browser default css styles

```ts
// example
*,
*:before,
*:after {
  box-sizing: border-box;
}
```

height.ts - defines all the heights on the application (like navbar height)
width.ts - same as heights

```ts
// example
export interface Heights {
  navBar: number;
  page: string;
}

export default {
  navBar: 70,
  page: '80vh',
};
```

media.ts - defines the media sizes

```ts
// example
export interface Media {
  md: any;
  sm: any;
  xs: any;
}

export default {
  md: '@media (max-width: 800px)',
  sm: '@media (max-width: 630px)',
  xs: '@media (max-width: 480px)',
};
```

palette.ts - defines the theme (more on this later)

shape.ts - defined borders like border radius and border color

```ts
// example
export interface Shape {
  borderRadius: number;
}

export default {
  borderRadius: 5,
};
```

spacing.ts - defines the unit of spacing every component should use for padding / margin. I stick with 8px

```ts
export interface Spacing {
  unit: 8;
}

export const unit = 8;
export default {
  unit: 8,
};
```

theme.ts - the combination of all these files exists in the theme

```ts
export interface Theme {
  palette: Palette;
  spacing: Spacing;
  widths: Widths;
  heights: Heights;
  media: Media;
  transitions: Transitions;
  shape: Shape;
}

export default {
  palette,
  spacing,
  widths,
  heights,
  media,
  transitions,
  shape,
} as Theme;
```

transitions.ts - defines the animations for all the components like button hover and tooltip fade away. I stick with slow, default, fast

```ts
export interface Transitions {
  norm: string;
  fast: string;
  slow: string;
}

const transitionSpeeds = {
  norm: 0.4,
  fast: 0.2,
  slow: 0.8,
};

export default {
  norm: `${transitionSpeeds.norm}s`,
  fast: `${transitionSpeeds.fast}s`,
  slow: `${transitionSpeeds.slow}s`,
  speeds: transitionSpeeds,
} as Transitions;
```
