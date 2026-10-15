https://master.dev/courses/frontend-system-design/introduction/

## Box model
 - composition:
	 - content
	 - padding
	 - border
	 - margin
 - types: 
	 - block element
		 - intrinsic height, width 100% of the parent
	 - anonymous box - elements not wrapped, such as text without a wrapper
 - mathematics of block elements
	 - border box: includes all the layers into the width
 - inline elements
	 - does not respond to widh and height (ignores it)
	 - height determined by line height or by intrinsic height (the overflow will be ignored by the browser)

## Browser Formatting Context
- whenever you create a new display property (block or inline) it creates a new formatting context

## Positioning
- relative
	- when we apply `position: relative` we create a new stacking context (z-index)
	- **containing element** - if element has `position: relative` its containing block is the parent block
- absolute
	- removed from the normal flow

## Reflow
- whenever javascript modifies DOM
- to calculate the layout the pc uses CPU
- to paint the layout the pc uses GPU
	- GPU is much faster, so something like animation is much faster than moving the element down with calculating the margin

