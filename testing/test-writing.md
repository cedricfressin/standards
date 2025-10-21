## Test coverage best practices

### Test Design Principles

- **Test Behavior, Not Implementation**: Focus tests on what the code does, not how it does it, to reduce brittleness
- **Clear Test Names**: Use descriptive names that explain what's being tested and the expected outcome
- **Independent Tests**: Each test should run independently without relying on execution order or shared state
- **Follow Arrange-Act-Assert (AAA)**: Structure tests as Arrange, Act, then Assert
- **One Concept Per Test**: Test one behavior or scenario per test to make failures easy to diagnose
- **Test Real User Workflows**: Validate behavior from the user's perspective, especially for integration tests

### Test Implementation

- **Use Testing Library Render APIs**: Use `render` or `renderHook` to implement tests
- **Fast Execution**: Keep unit tests fast (milliseconds) so developers run them frequently during development
- **Maintain Test Code Quality**: Apply the same code quality standards to tests as to production code

## Coverage

- **Set Minimum Thresholds**: Establish baseline coverage requirements (e.g., 80% overall) but prioritize meaningful tests over percentages
- **Prioritize Critical Paths**: Aim for higher coverage (90%+) on business logic, authentication, and payment flows
- **Quality Over Quantity**: 100% coverage doesn't guarantee bug-free code; focus on testing behavior and edge cases
- **Track Coverage Trends**: Monitor coverage over time to catch regressions and ensure new code is tested
- **Exclude Appropriately**: Don't count generated code, test files, or configuration files against coverage metrics

### Query & Interaction

- **Use Proper Query Priority**: `getByRole` → `getByLabelText` → `getByText` → `getByTestId` (last resort)
- **Prefer userEvent Over fireEvent**: Use `userEvent` for realistic user interactions
- **Assert Visibility for Displayed UI**: Use `toBeVisible()` when components should be shown

### Scope & Mocking Strategy

- **Test Edge Cases**: Include boundary conditions, empty inputs, null values, and error scenarios
- **Mock External Dependencies**: For unit tests, isolate units by mocking databases, APIs, file systems, and other external services
- **Avoid Mocking Internals**: For integration tests, do not mock sub-components or internal dependencies unless necessary

<example>

```tsx
// Unit Test: Test for a hook loading session data
import { renderHook } from "@testing-library/react-native";
import { SessionProvider } from "~/lib/providers/session-provider";

describe("useSession", async () => {
  it("load sucessfully load session data", () => {
    // Arrange
    const { result } = renderHook(<useSession />, { wrapper: SessionProvider });

    // Act
    await waitFor(() => expect(result.current.loading).toBe(false));

    // Assert
    expect(result.current.session).toMatchSnapshot();
  });
});
```

```tsx
// Integration Test: Test for a title being visible with a simple greeting message
import { render, screen } from "@testing-library/react-native";
import { Providers } from "~/lib/providers";

describe("HomeScreen", () => {
  it("should has greeting message visible", () => {
    // Arrange & Act
    render(<HomeScreen />, { wrapper: Providers });
    // Assert
    expect(screen.getByRole("heading", { name: /^Welcome/i })).toBeVisible();
  });
});
```

```tsx
// Integration Test: Test for a back button navigation
import { render, screen } from "@testing-library/react-native";
import { router } from "expo-router";

jest.mock("expo-router");

describe("Header", () => {
  it("should navigate back when press back button", async () => {
    // Arrange
    render(<Header />);
    // Act
    fireEvent.press(screen.getByRole("button", { name: "Back" }));
    // Assert
    await waitFor(() => expect(router.back).toHaveBeenCalled());
  });
});
```

</example>
