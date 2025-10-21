## Expo best practices

### Core Principles

- **Mobile-First Development**: Design for mobile constraints first, then adapt for web/desktop
- **Cross-Platform Excellence**: Write once, run everywhere with platform-specific optimizations
- **Keep it Simple**: Implement solutions in fewest lines with straightforward approaches
- **Performance First**: Leverage native optimizations and avoid unnecessary re-renders
- **Platform-Native Feel**: Use platform-specific UI patterns when appropriate
- **Managed Workflow**: Rely on Expo's managed workflow for streamlined development and deployment
- **Mobile Web Vitals**: Prioritize Mobile Web Vitals (Load Time, Jank, and Responsiveness)

### Configuration & Environment

- **Environment Variables**: Use `expo-constants` for managing environment variables and configuration
- **Permission Modules**: Use individual permission modules (e.g., `expo-camera`, `expo-location`) as `expo-permissions` is deprecated
- **OTA Updates**: Implement `expo-updates` for over-the-air (OTA) updates

### Navigation

- **Layouts Definition**: Define layouts that wrap child routes with shared UI and navigation structure (`_layout.tsx`)
- **Declarative Navigation**: Use `Link` for declarative navigation with proper TypeScript typing
- **Programmatic Navigation**: Use `router` hook for programmatic navigation
- **Immediate Redirects**: Use `Redirect` for immediate redirects without rendering

### Lists & Performance

- **Efficient List Rendering**: Use `FlatList`, `SectionList` or `VirtualizedList` instead of `map()` for long lists
- **Advanced List Performance**: Use `@legendapp/list` for long lists and heavy rendering to improve performance
- **Key Extraction**: Provide a stable and unique `keyExtractor`
- **Item Layout Optimization**: Implement `getItemLayout` for fixed-height items

### Keyboard

- **Keyboard Handling**: Use `react-native-keyboard-controller` to handle keyboard behavior identically on both platforms
- **Keyboard Events**: Handle keyboard events for better user experience

### Animations

- **Reanimated Animations**: Use `react-native-reanimated` for smooth, performant animations

### Images & Assets

- **Image Formats**: Use appropriate image formats: WebP for photos, SVG for icons
- **Image Performance**: Use `expo-image` for better performance and caching
- **Lazy Loading Images**: Implement lazy loading for images not immediately visible
- **Blurhash Transitions**: Use blurhash for smooth loading transitions and better perceived performance
- **Density Optimization**: Optimize image sizes for different screen densities
- **Remote Images**: Use remote images with CDN when possible
- **Scalable Icons**: Use SVG for scalable icons and illustrations
- **Custom Vectors**: Leverage `react-native-svg` for custom vector graphics
- **SVG Optimization**: Optimize SVG files before bundling (remove unnecessary metadata)

### Internationalization & Accessibility

- **Language Support**: Support multiple languages and RTL layouts
- **Text Accessibility**: Ensure text scaling and font adjustments for accessibility

### Security

- **Secure Storage**: Use `expo-secure-store` for sensitive data storage
- **Biometric Protection**: Enable `requireAuthentication` for biometric-protected storage
- **OAuth Flows**: Use `expo-auth-session` for OAuth flows
