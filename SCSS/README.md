#Code Guide for Piggybank SCSS

Written by Adam Bickford

This will be a constant work in progress while striving to write the best code for our team and our product.

Any suggestions should be thoroughly discussed with the team before being added, and complaints should be filed in my complaint box -> :toilet:

---

##Naming structure

**KEY POINT: Meaningful dashes, underscores, or camelCase.**

Don't rely on long strings of one naming scheme like `.RadioToggleTitleActive`
or `.radio-toggle-title-active`. Instead we are using a structure like the
following:

```css
//Component
.ComponentName {}

//Component modifier
.ComponentName--modifier {}

//Component descendant
.__descendant {}

//Component descendant modifier
.__descendant--modifierName {}

//Component state (scoped to component)
.ComponentName.is-state {}

//Descendant state (scoped to descendant)
.__descendant.is-state {}
```

Descendants of components should only be nested **1 level deep** *unless* the
nesting is a psuedo selector or native hover/active styles


###WRONG:
```css
.RadioToggle {
  .__option {
    .__title {} // Don't nest .__element classes two levels deep!
  }
  &.is-active {}
}
```


###RIGHT:
```css
.RadioToggle {
  .__option {}
  .__title {
    &:hover {}
  }
  &.is-active {}
}

//Congratulations! You get to keep your job!
```

This means our longest output should be `.RadioToggle .__title:hover` and

##Rule structure

This keeps a level of uniformity to how our properties are set up.

```
.ComponentName {
  property: value;          // first component properties
  @include prop(value);     // then mixins
  &:hover {}                // then native pseudo or hover styles for the component
  &.is-inActive {}          // then custom state classes for the component

  .__element {              // then descendants
    property: value;           // which in turn follows the same structure
    @include prop(val);        // except there should be no nested elements
    &:first-child {}           // only nested hover/psuedo classes
    &.is-active {}             // or state classes scoped to this element
  }
  .__element--modifier {}   // then modifiers of descendants
}
.ComponentName--modifier {}   // then modifiers of components
```

This keeps our outputted css limited to two elements. `.componentName .__element.is-active` would be the longest selector in our built css and that's the way we want to keep it. This
will help keep specificity simple should rules need to be overridden in the future.
