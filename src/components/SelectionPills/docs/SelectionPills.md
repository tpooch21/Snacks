
### Self controlled state

Initial state for all pills is set through properties of individual pills in the `pills` array prop.
All changes in pill state through user interaction is stored and updated within the
`SelectionPills` internal state unless the `parentControlledState` state prop is passed in.
The parent component of `SelectionPills` does not need to maintain state for pills once mounted.

The `pills` array accept all properties of a `SelectionPill` and can be used to
to override the underlying pill behavior or style.

```jsx
import { SelectionPills } from 'ic-snacks'

const initialState = { activePill: 'carrots' }
const pills = [
  { text: 'bananas', id: 'filterby-1', isSelected: true },
  { text: 'carrots', id: 'filterby-2' },
  { text: 'watermelon', id: 'filterby-3' },
  { text: 'snacks', id: 'filterby-4' },
  { text: 'kale', id: 'filterby-5' },
  { text: 'endives', id: 'filterby-6', isDisabled: true },
  { text: 'arugula', id: 'filterby-7' },
  { text: 'spinach', id: 'filterby-8' },
  { text: 'potatoes', id: 'filterby-9' },
]

;<div>
  <SelectionPills
    pills={pills}
    onSelectPill={(e, pill) => {
      console.log('SelectionPills SelectionPill clicked!', pill)
    }}
    label="Filter by"
  />
  </div>
```

#### With select all pill

Optional parameter to include a "select all" button. It deselects all other options when clicked.

```jsx
import { SelectionPills } from 'ic-snacks'

const pills = [
  { text: 'bananas', id: 'selection-1', isSelected: true },
  { text: 'carrots', id: 'selection-2' },
  { text: 'watermelon', id: 'selection-3' },
  { text: 'snacks', id: 'selection-4' },
  { text: 'kale', id: 'selection-5' },
  { text: 'endives', id: 'selection-6', isDisabled: true },
  { text: 'arugula', id: 'selection-7' },
  { text: 'spinach', id: 'selection-8' },
  { text: 'potatoes', id: 'selection-9' },
]
;<div>
  <SelectionPills
    includeSelectAll
    selectAllLabel="Select all"
    pills={pills}
    onSelectPill={(e, pill) => {
      console.log('SelectionPills SelectionPill clicked!', pill)
    }}
    label="Filter by"
  />
  </div>
```

#### With maximum number of selections

Optional parameter to restrict the number of selections that can be chosen

```jsx
import { SelectionPills } from 'ic-snacks'

const pills = [
  { text: 'bananas', id: 'maxSelection-1' },
  { text: 'carrots', id: 'maxSelection-2' },
  { text: 'watermelon', id: 'maxSelection-3' },
  { text: 'snacks', id: 'maxSelection-4' },
  { text: 'kale', id: 'maxSelection-5' },
  { text: 'endives', id: 'maxSelection-6' },
  { text: 'arugula', id: 'maxSelection-7' },
  { text: 'spinach', id: 'maxSelection-8' },
  { text: 'potatoes', id: 'maxSelection-9' },
]
;<div>
  <SelectionPills
    maxSelectionCount={3}
    pills={pills}
    onSelectPill={(e, pill) => {
      console.log('SelectionPills SelectionPill clicked!', pill)
    }}
    label="Select up to 3:"
  />
  </div>
```

#### Without ScrollTrack wrapper

Optional parameter to layout in grid format without `ScrollTrack` wrapper

```jsx
import { SelectionPills } from 'ic-snacks'

const pills = [
  { text: 'bananas', id: 'gridSelection-1' },
  { text: 'carrots', id: 'gridSelection-2' },
  { text: 'watermelon', id: 'gridSelection-3' },
  { text: 'snacks', id: 'gridSelection-4' },
  { text: 'kale', id: 'gridSelection-5' },
  { text: 'endives', id: 'gridSelection-6' },
  { text: 'arugula', id: 'gridSelection-7' },
  { text: 'spinach', id: 'gridSelection-8' },
  { text: 'potatoes', id: 'gridSelection-9' },
]
;<div>
  <SelectionPills
    excludeScrollTrack
    pills={pills}
    onSelectPill={(e, pill) => {
      console.log('SelectionPills SelectionPill clicked!', pill)
    }}
  />
  </div>
```

### Parent controlled state

State of each `SelectionPill` can be controlled by a parent component by passing a
in the `parentControlledState` prop. When this prop is present, the `pills`
array prop controls the state of each pill through the `isSelected` property.



```jsx
import { SelectionPills } from 'ic-snacks'

const initialState = {
  pills: [
    { text: 'bananas', id: 'parentControlled-1' },
    { text: 'carrots', id: 'parentControlled-2' },
    { text: 'watermelon', id: 'parentControlled-3' },
    { text: 'snacks', id: 'parentControlled-4' },
    { text: 'kale', id: 'parentControlled-5' },
    { text: 'endives', id: 'parentControlled-6' },
    { text: 'arugula', id: 'parentControlled-7' },
    { text: 'spinach', id: 'parentControlled-8' },
    { text: 'potatoes', id: 'parentControlled-9' },
  ]
}
;<div>
  <SelectionPills
    parentControlledState
    pills={state.pills}
    onSelectPill={(e, pill) => {
      console.log('SelectionPills SelectionPill clicked!', pill)
      const updatedPills = state.pills.map(p => {
        if (p.id === pill.id) {
          return {
            ...p,
            isSelected: !p.isSelected
          }
        }
        return p
      })
      setState({
        pills: updatedPills
      })
    }}
    label="Filter by"
  />
  </div>
```
