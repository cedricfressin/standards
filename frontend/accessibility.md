## UI accessibility best practices

### Standards & Compliance

- **WCAG 2.1 AA Compliance**: Apply WCAG 2.1 AA across web and mobile. Favor semantic elements and platform-native accessibility APIs. Test with real assistive tech
- **Contrast Standards**: Meet at least WCAG 2.1 AA contrast: 4.5:1 text, 3:1 large text/UI

### Semantic HTML & ARIA

- **Semantic HTML**: Use appropriate HTML elements (nav, main, button, etc.) that convey meaning to assistive technologies
- **ARIA When Needed**: Use ARIA attributes to enhance complex components when semantic HTML isn't sufficient
- **Logical Heading Structure**: Use heading levels (h1-h6) in proper order to create a clear document outline

### Keyboard & Navigation

- **Keyboard Navigation**: Ensure all interactive elements are accessible via keyboard with visible focus indicators
- **Focus Management**: Manage focus appropriately in dynamic content, modals, and single-page applications

### Color & Visual Design

- **Color Contrast**: Maintain sufficient contrast ratios (4.5:1 for normal text) and don't rely solely on color to convey information
- **Alternative Text**: Provide descriptive alt text for images and meaningful labels for all form inputs

### Text Alternatives

- Web: `alt` on images; `alt=""` only for decorative images
- React Native: `accessibilityLabel` for informative images; set `accessible={false}` and `importantForAccessibility="no"` for decorative images; use `accessibilityRole="image"`

### Roles, State & Value

- Use native roles (`button`, `link`, `checkbox`, etc.)
- Reflect state with `aria-*` on web and `accessibilityState` / `accessibilityValue` on React Native
- Don't duplicate implicit roles

### Focus & Navigation

- All controls must be reachable and operable via keyboard on web; support screen reader actions on React Native
- Manage focus for modals and overlays; trap focus while open and return focus on close
- Announce important status changes (loading, errors, success)

### Forms

- **Labels and association**: visible labels linked (`htmlFor`/`id`) on web; `accessibilityLabel` or `accessibilityLabelledBy`/`nativeID` on React Native
- **Required fields**: mark in text, not color alone. Provide clear format hints
- **Validation**: expose errors via `role="alert"` or live regions on web; use `AccessibilityInfo.announceForAccessibility` on React Native
- **Autofill**: use proper `type`, `autoComplete` (web) and `keyboardType`, `textContentType` (React Native)

### Dynamic Content & Motion

- Use live regions for status messages: `aria-live="polite|assertive"` (web) or `AccessibilityInfo.announceForAccessibility` (React Native)
- Respect reduced motion. Provide pause/stop controls for animations. Avoid flashing >3 times/second
