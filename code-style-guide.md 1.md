# Code Style Guidelines


- [Template](#Template)
- [Component](#Component)
- [ES Imports](#ES-Imports)
- [Naming](#Naming)
- [Style CSS](#Style-CSS)

## Template

HTML tag writing rules:

- When an element has two or more attributes, we should write **each attribute on a separate line**.
- Attributes must be written in a **specific order**:
  - Structural directives
  - Animations
  - Attribute directive
  - Static properties
  - Dynamic properties
  - Events
- The closing tag must be **written on the last line**.


Let's take a look at the example:
```html
<input
	*ngIf="canSearch"
	@fadeIn
	padInput
	class="text-sm font-medium"
	type="text"
	[formControl]="autoSearchControl"
	(keyup.enter)="onKeywordEnter()" />
```



## Component

Use the following order of groups to organize Angular components:

1. Dependencies injection.
2. Data binding properties.
3. Private properties.
4. View and content properties.
5. UI properties.
6. Component API properties.
7. Constructor.
8. Lifecycle hooks.
9. Event handlers.
10. Component API methods.
11. Private methods.

| Group                       | Description                                                                                                                                                          |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Component API methods       | Public methods intended to be used by other components, directives, or services.                                                                                     |
| Component API properties    | Public properties intended to be used by other components, directives, or services.                                                                                  |
| Data binding properties     | Properties decorated by `Input` or `Output`.                                                                                                                         |
| Event handlers.             | Methods used by the component template.                                                                                                                              |
| Lifecycle hooks             | Methods implementing the `AfterContentChecked`, `AfterContentInit`, `AfterViewChecked`, `AfterViewInit`, `DoCheck` `OnChanges`, `OnDestroy`, or `OnInit` interfaces. |
| Private properties          | Properties marked by `private` or `#`.                                                                                                                               |
| UI properties               | Public properties used by the component template.                                                                                                                    |
| View and content properties | Properties decorated by `ContentChild`, `ContentChildren`, `ViewChild`, or `ViewChildren`.                                                                           |



## ES Imports
The imports should be grouped as follows:
- Angular import
- Rx imports
- Third parties import
- Local/Project imports

```typescript
// Angular
import { NgFor, NgTemplateOutlet } from '@angular/common';
import { OnDestroy, OnInit, inject } from '@angular/core';

// Rx
import { Subscription, filter } from 'rxjs';

// Third parties
import { CompareWith, PadSafeAny } from 'pad-ui-lib/core/type';
import { PadMenuModule } from 'pad-ui-lib/menu';

// Project
import { OptionComponent, OptionSelectionChange,} from './option.component';
import { WrapperOptionsComponent } from './wrapper-option.component';
```


## Naming

- Use meaningful and descriptive names for variables, functions, and classes.
- Class and enum are PascalCase.
- Everything else (function, variables, etc.) is camel-case.
- Prefix private with a capital `_`  (e.g., `_cdr`, `).
- Variable and property names with type observable must have `$` at the end (e.g.,  `user$`, `loading$`).
- Variable and property names with type signal must be starting with `$` (e.g.,  `$products`, `$status`).

## Style CSS
- Class names with BEM type.
