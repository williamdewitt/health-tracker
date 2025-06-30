[<< Back](./../design.md)

# Frontend Design Specification

## 🗺️ **User Flow → Use Case Mapping (Template)**

### **CRITICAL: Mapping Protocol for GAIA**

**PURPOSE**: This section serves as the central registry for all user flows and their corresponding use cases. GAIA must maintain this mapping to ensure complete traceability from user journey to implementation requirements.

**TEMPLATE STRUCTURE**:

```markdown
### 📋 **User Flow Registry**

#### **Flow ID**: `UF-[NUMBER]-[SHORT-NAME]`
- **Flow Name**: [Descriptive name of the user flow]
- **Primary Use Case(s)**: [UC-001, UC-002] (Reference to 1-use-cases.md)
- **Secondary Use Cases**: [UC-003] (Supporting or related use cases)
- **User Type**: [Primary user persona for this flow]
- **Flow Complexity**: [Simple/Medium/Complex]
- **Implementation Priority**: [High/Medium/Low]

**Flow Steps**:
1. **[Step Name]**: [Description of user action and system response]
2. **[Step Name]**: [Description of user action and system response]
3. **[Step Name]**: [Description of user action and system response]

**UI Components Required**:
- [Component Name] - [Brief purpose]
- [Component Name] - [Brief purpose]

**Success Criteria**:
- [Measurable outcome 1]
- [Measurable outcome 2]

**Error Scenarios**:
- [Error condition] → [User feedback/recovery path]
- [Error condition] → [User feedback/recovery path]

---
```

### 📊 **Example Implementation**

#### **Flow ID**: `UF-001-USER-REGISTRATION`
- **Flow Name**: New User Account Registration
- **Primary Use Case(s)**: UC-001 (User Registration)
- **Secondary Use Cases**: UC-002 (Email Verification), UC-003 (Profile Setup)
- **User Type**: First-time visitor
- **Flow Complexity**: Medium
- **Implementation Priority**: High

**Flow Steps**:
1. **Landing**: User arrives at registration page from marketing site or login redirect
2. **Form Input**: User fills registration form (email, password, basic info)
3. **Validation**: Real-time field validation with immediate feedback
4. **Submission**: Form submission with loading state and API call
5. **Verification**: Email verification prompt with resend option
6. **Confirmation**: Success message with next steps (profile completion)

**UI Components Required**:
- RegistrationForm - Input fields with validation
- LoadingSpinner - Submission feedback
- EmailVerificationModal - Post-registration verification
- SuccessToast - Confirmation messaging

**Success Criteria**:
- User completes registration within 2 minutes
- 95% form validation accuracy
- Clear guidance for next steps

**Error Scenarios**:
- Email already exists → Clear error message with login option
- Network failure → Retry mechanism with saved form data
- Validation errors → Inline field errors with correction guidance

---

### 🎯 **GAIA Implementation Guidelines**

**When Adding New User Flows**:
1. **Flow Discovery**: Identify user flows from use case analysis
2. **Component Mapping**: Link flows to required UI components
3. **Priority Assessment**: Evaluate implementation complexity and business value
4. **Cross-Reference**: Ensure flows align with use cases in 1-use-cases.md
5. **Update Registry**: Add complete flow documentation using template above

**Maintenance Protocol**:
- **Review Frequency**: Update flows when use cases change
- **Traceability Check**: Ensure every use case has corresponding user flows
- **Component Validation**: Verify all required components are documented
- **Testing Alignment**: Ensure flows match Playwright test scenarios

**Quality Standards**:
- **Completeness**: Every user journey from entry to exit documented
- **Clarity**: Each step clearly describes user action and system response
- **Consistency**: Uniform flow documentation across all features
- **Actionability**: Sufficient detail for implementation and testing

---

## Overview

This document captures the complete frontend application specification, design system, and architecture. It serves as the single source of truth for all UI/UX decisions and implementation details. This specification ensures the frontend is not just functional, but truly beautiful and modern.

**MANDATORY DEFAULTS**: All frontends must include responsive design supporting desktop and mobile devices, unless explicitly specified otherwise by the user.

## 📱 **MANDATORY RESPONSIVE DESIGN REQUIREMENTS**

**CRITICAL**: Every frontend application MUST support responsive design across desktop and mobile devices unless the user explicitly specifies otherwise.

### **Default Responsive Standards**:

**Required Device Support**:

- **Desktop**: 1024px+ (Primary development and business use)
- **Tablet**: 768px - 1023px (Intermediate layouts)
- **Mobile**: 375px - 767px (Essential mobile experience)

**Implementation Requirements**:

- **Mobile-First Development**: Build for mobile first, enhance for desktop
- **Flexible Grid Systems**: CSS Grid/Flexbox or Ant Design's responsive grid
- **Responsive Typography**: Scalable text sizes across all breakpoints
- **Touch Optimization**: 44px minimum touch targets for mobile
- **Navigation Adaptation**: Collapsible menus and mobile-friendly navigation

**Quality Assurance**:

- **Playwright Testing**: Mandatory screenshot tests at all breakpoints
- **Cross-Device Validation**: Test on actual mobile devices when possible
- **Performance Optimization**: Fast loading on mobile networks
- **Accessibility**: Keyboard navigation and screen reader compatibility

**When Responsive Design is NOT Required**:

- User explicitly requests desktop-only application
- Specialized hardware/kiosk applications
- Technical constraints preventing responsive implementation
- User specifies single-device targeting

## 🎨 **GAIA's UI/UX EXPERTISE** (When No Inspiration Provided)

### **Automatic Design Intelligence**

When users don't provide visual inspiration or UI/UX directives, GAIA automatically becomes the expert UI/UX designer, analyzing the target audience and crafting the perfect interface.

### **Audience-Driven Design Matrix**

#### **Business/Enterprise Applications**

**Characteristics**: Professional, trustworthy, efficient
**Color Palette**:

- Primary: Deep blues (#1E40AF, #3B82F6) or sophisticated grays (#374151, #6B7280)
- Accent: Professional greens (#059669, #10B981) or warm oranges (#EA580C, #F97316)
  **Typography**: Clean sans-serif (Inter, Roboto, Open Sans)
  **Layout**: Grid-based, data-dense, clear hierarchy
  **Examples**: Stripe, Linear, Notion, Salesforce Lightning

#### **Consumer/General Applications**

**Characteristics**: Friendly, approachable, intuitive
**Color Palette**:

- Primary: Warm blues (#2563EB, #3B82F6) or friendly purples (#7C3AED, #8B5CF6)
- Accent: Energetic colors (#EF4444, #F59E0B, #10B981)
  **Typography**: Rounded, friendly fonts (Inter, Poppins, Nunito)
  **Layout**: Card-based, whitespace-heavy, mobile-first
  **Examples**: Airbnb, Spotify, Instagram, Apple

#### **Creative/Portfolio Applications**

**Characteristics**: Bold, expressive, showcase-focused
**Color Palette**:

- Primary: Bold, artistic colors (#DC2626, #7C2D12, #1F2937)
- Accent: Vibrant, creative colors (#F59E0B, #8B5CF6, #EC4899)
  **Typography**: Distinctive fonts (Outfit, Playfair Display, custom)
  **Layout**: Asymmetrical, image-heavy, creative grids
  **Examples**: Behance, Dribbble, Awwwards, Adobe

#### **Technical/Developer Applications**

**Characteristics**: Functional, customizable, information-dense
**Color Palette**:

- Primary: Dark themes (#111827, #1F2937) with accent colors (#3B82F6, #10B981)
- Light: Clean grays (#F9FAFB, #F3F4F6) with technical blues
  **Typography**: Monospace options (JetBrains Mono, Fira Code) + sans-serif
  **Layout**: Dashboard-style, customizable panels, terminal-inspired
  **Examples**: GitHub, VS Code, Vercel, Figma

### **GAIA's Creative Process**

1. **Audience Analysis**: Extract target user type from project description
2. **Industry Research**: Apply industry-specific design patterns and expectations
3. **Color Psychology**: Select colors that evoke appropriate emotions and trust
4. **Information Architecture**: Design user flows that match user mental models
5. **Accessibility Integration**: Ensure inclusive design from the ground up
6. **Modern Trends Integration**: Apply current design trends appropriately

### **Default Design Decisions** (When Creating Original UI)

#### **Color Strategy**:

- **Primary Color**: Choose based on industry (blue for trust, green for growth, purple for creativity)
- **Accent Colors**: Complementary colors that enhance, not compete
- **Neutral Palette**: Modern grays with proper contrast ratios (4.5:1 minimum)
- **Semantic Colors**: Green for success, red for errors, amber for warnings, blue for info

#### **Typography Hierarchy**:

- **Display/Hero**: 3.5rem (56px) - Landing page headlines
- **H1**: 2.5rem (40px) - Page titles
- **H2**: 2rem (32px) - Section headers
- **H3**: 1.5rem (24px) - Subsection headers
- **Body Large**: 1.125rem (18px) - Important content
- **Body**: 1rem (16px) - Standard content
- **Small**: 0.875rem (14px) - Meta information
- **Caption**: 0.75rem (12px) - Fine print

#### **Spacing System** (8px base):

- **XS**: 4px - Icon spacing, small gaps
- **SM**: 8px - Element padding, tight spacing
- **MD**: 16px - Standard spacing between elements
- **LG**: 24px - Section spacing
- **XL**: 32px - Large section breaks
- **2XL**: 48px - Major layout divisions
- **3XL**: 64px - Hero section spacing

#### **Component Defaults**:

- **Buttons**: Rounded corners (8px), hover states, focus rings
- **Cards**: Subtle shadows, rounded corners (12px), proper padding
- **Forms**: Clear labels, proper spacing, validation states
- **Navigation**: Intuitive hierarchy, clear active states
- **Loading States**: Skeleton screens, progressive loading
- **Empty States**: Helpful illustrations, clear next steps

## 🎨 Visual Inspiration & Design Direction

### Design References

- **Primary Inspiration**: `[LINKS_TO_SPECIFIC_APPS/WEBSITES]`
- **Secondary References**: `[ADDITIONAL_INSPIRATION_SOURCES]`
- **Target Aesthetic**: `[MODERN_MINIMALIST/RICH_DETAILED/CREATIVE_BOLD/ENTERPRISE_PROFESSIONAL/ETC]`

### Design Philosophy

- **Core Principle**: `[BEAUTY_THROUGH_SIMPLICITY/SOPHISTICATED_DETAIL/BOLD_CREATIVITY/ETC]`
- **User Experience Goals**: `[INTUITIVE_NAVIGATION/DELIGHTFUL_INTERACTIONS/EFFICIENT_WORKFLOWS/ETC]`
- **Brand Personality**: `[TRUSTWORTHY/INNOVATIVE/PLAYFUL/PROFESSIONAL/ETC]`

## Design System

### Color Palette

**Primary Colors** (Based on inspiration/brand):

- Primary: `#[HEX_CODE]` - Main brand color for CTAs and primary actions
- Primary Light: `#[HEX_CODE]` - Hover states and backgrounds
- Primary Dark: `#[HEX_CODE]` - Active states and emphasis
- Secondary: `#[HEX_CODE]` - Accent color for highlights and secondary actions
- Tertiary: `#[HEX_CODE]` - Supporting color for variety and interest

**Neutral Palette** (Modern, sophisticated neutrals):

- White: `#FFFFFF` - Pure white for backgrounds
- Gray 50: `#[HEX_CODE]` - Lightest gray for subtle backgrounds
- Gray 100: `#[HEX_CODE]` - Very light gray for disabled states
- Gray 200: `#[HEX_CODE]` - Light gray for borders
- Gray 300: `#[HEX_CODE]` - Medium-light gray for secondary text
- Gray 400: `#[HEX_CODE]` - Medium gray for placeholders
- Gray 500: `#[HEX_CODE]` - True gray for secondary text
- Gray 600: `#[HEX_CODE]` - Dark gray for primary text
- Gray 700: `#[HEX_CODE]` - Very dark gray for headings
- Gray 800: `#[HEX_CODE]` - Almost black for emphasis
- Gray 900: `#[HEX_CODE]` - Pure black for maximum contrast

**Semantic Colors** (Modern, accessible):

- Success: `#10B981` - Green for success states
- Success Light: `#D1FAE5` - Light green for success backgrounds
- Warning: `#F59E0B` - Amber for warning states
- Warning Light: `#FEF3C7` - Light amber for warning backgrounds
- Error: `#EF4444` - Red for error states
- Error Light: `#FEE2E2` - Light red for error backgrounds
- Info: `#3B82F6` - Blue for informational states
- Info Light: `#DBEAFE` - Light blue for info backgrounds

## 🔔 **MANDATORY NOTIFICATION SYSTEM**

### **Default User Feedback Requirements**

**CRITICAL**: Every frontend application MUST implement a comprehensive notification system for user feedback, especially for API interactions and critical user actions.

#### **Required Notification Scenarios**

**API Interaction Notifications**:

- **API Call Failures**: Network errors, server errors (5xx), timeout errors
- **API Call Success**: Form submissions, data saves, record updates, deletions
- **Authentication Events**: Login/logout success, session expiration warnings
- **Validation Errors**: Client-side and server-side validation failures
- **Loading States**: Long-running operations, data fetching, file uploads

**System Event Notifications**:

- **Connection Status**: Network connectivity changes, offline mode
- **Data Sync**: Background synchronization status, conflict resolution
- **Feature Updates**: New features, maintenance notifications
- **Critical Alerts**: Security warnings, system maintenance

#### **Notification Types & Implementation**

**Using Ant Design Notification System**:
- **Error Notifications**: API failures with actionable error messages (6-8s duration)
- **Success Notifications**: Operation confirmations (3-4s duration)
- **Loading States**: Auto-clearing progress indicators
- **Warning Notifications**: Session expiration, important notices (5-6s duration)

**Notification Standards**:
- **Error (API Failures)**: Red theme, longer duration, actionable message
- **Success**: Green theme, brief duration, confirmation message
- **Warning**: Orange theme, medium duration, cautionary message
- **Info**: Blue theme, standard duration, informational message
- **Loading**: Auto-dismiss when operation completes

#### **Error Message Categories**

**Network & Server Errors**:

- **Network Error**: "Connection failed. Please check your internet connection and try again."
- **Server Error (5xx)**: "Something went wrong on our end. Please try again in a few moments."
- **Timeout Error**: "Request timed out. Please try again."
- **Rate Limit**: "Too many requests. Please wait a moment before trying again."

**Authentication & Authorization**:

- **Session Expired**: "Your session has expired. Please log in again to continue."
- **Unauthorized**: "You don't have permission to perform this action."
- **Invalid Credentials**: "Invalid username or password. Please try again."

**Validation & Data Errors**:

- **Validation Error**: "Please check the highlighted fields and correct any errors."
- **Duplicate Data**: "This record already exists. Please use a different value."
- **Missing Required Data**: "Please fill in all required fields before submitting."
- **Invalid Format**: "Please enter a valid [email/phone/date] format."

#### **Notification Positioning & Behavior**

**Desktop Layout**:

- **Primary Position**: Top-right corner for standard notifications
- **Critical Alerts**: Center modal overlay for important messages
- **Loading States**: Inline or center overlay depending on context

**Mobile Layout**:

- **Primary Position**: Top of screen, full width
- **Critical Alerts**: Full-screen overlay for important messages
- **Loading States**: Inline with touch-friendly dismiss options

**Accessibility Features**:

- **Screen Reader**: Proper ARIA labels and live regions
- **Keyboard Navigation**: Focus management and dismiss shortcuts
- **High Contrast**: Sufficient color contrast for all notification types
- **Reduced Motion**: Respect user motion preferences

#### **Implementation Pattern**

**HTTP Client with Automatic Notifications**:
- **Request Interceptors**: Show loading states for API calls
- **Response Interceptors**: Handle success/error notifications automatically
- **Error Classification**: Network, authentication, server, and validation errors
- **Form Integration**: Seamless notification integration with form submissions

**Key Implementation Features**:
- **Auto-loading States**: Show/hide loading indicators automatically
- **Error Categorization**: Different notification styles for different error types
- **Success Feedback**: Configurable success messages with form resets
- **Retry Mechanisms**: Built-in retry functionality for failed operations

#### **Notification System Exceptions**

**When NOT to Use Default Notifications**:

- User explicitly requests silent mode or custom notification system
- Specialized applications where notifications interfere with workflow
- Real-time applications where notifications would be overwhelming
- Custom notification systems already implemented with equivalent functionality

## ✨ Modern Animations & Micro-interactions

### Timing & Easing (Smooth, Natural Feel)

**Transition Durations**:
- **Instant**: `0ms` (Immediate feedback)
- **Fast**: `150ms` (Quick hover states, small UI changes)
- **Medium**: `250ms` (Default for most interactions)
- **Slow**: `400ms` (Page transitions, complex animations)
- **Very Slow**: `600ms` (Special emphasis animations)

**Easing Functions** (Natural, physics-based):
- **Default**: `cubic-bezier(0.4, 0, 0.2, 1)` (Material Design standard)
- **Entrance**: `cubic-bezier(0, 0, 0.2, 1)` (Ease out - elements coming in)
- **Exit**: `cubic-bezier(0.4, 0, 1, 1)` (Ease in - elements going out)
- **Sharp**: `cubic-bezier(0.4, 0, 0.6, 1)` (Quick, snappy movements)
- **Bounce**: `cubic-bezier(0.68, -0.55, 0.265, 1.55)` (Playful bounce effect)

### Component Animations

**Button Interactions**:
- Hover: `transform: translateY(-1px)` + shadow increase over `150ms`
- Active: `transform: translateY(0px)` + shadow decrease over `100ms`
- Loading: Spinner or pulse animation
- Success: Brief scale animation `scale(1.05)` then back to `1.0`

**Card Animations**:
- Hover: `transform: translateY(-4px)` + shadow elevation over `250ms`
- Load-in: Fade in with `translateY(20px)` to `translateY(0)` over `400ms`
- Stagger: Cards animate in sequence with `100ms` delays

**Modal Animations**:
- Entrance: Backdrop fade in over `250ms`, Modal scale from `0.95` to `1.0` + fade in over `300ms`
- Exit: Reverse of entrance over `200ms`

**Page Transitions**:
- Route changes: Fade + slight slide (`translateX(20px)`) over `400ms`
- Loading states: Skeleton screens with subtle shimmer animations

### Micro-interactions (Delightful Details)

**Interactive Feedback**:
- **Form Focus**: Smooth border color transition + subtle scale of focus ring
- **Checkbox/Radio**: Checkmark draw-in animation over `200ms`
- **Toggle Switches**: Smooth slide animation with bounce easing
- **Dropdown Expand**: Height expansion with opacity fade-in
- **Progress Indicators**: Smooth bar fill or circular progress
- **Success Actions**: Subtle confetti or checkmark animation

**Hover States**:
- **Links**: Underline animation from left to right
- **Images**: Subtle scale (`scale(1.05)`) with overflow hidden
- **Icons**: Color transition + optional rotation/bounce
- **Navigation Items**: Background slide-in animation

### Loading & State Animations

**Loading States**:
- **Skeleton Screens**: Shimmer animation across placeholder content
- **Spinners**: Smooth rotation with appropriate sizing
- **Progress Bars**: Smooth fill animation with optional pulse
- **Lazy Loading**: Fade-in as content loads

**Data Animations**:
- **Chart Transitions**: Smooth data updates with eased transitions
- **Number Counters**: Count-up animations for statistics
- **Sort/Filter**: Smooth reordering with translate animations

## 📱 Modern Responsive Design

### Mobile-First Strategy

**Mobile Layout Patterns** (320px+):
- Single column layouts
- Collapsible navigation (hamburger menu)
- Touch-friendly 44px+ button heights
- Swipe gestures for carousels/navigation
- Bottom-aligned primary actions

**Tablet Adaptations** (768px+):
- Two-column layouts where appropriate
- Expanded navigation (visible menu items)
- Side-by-side forms
- Larger touch targets maintained

**Desktop Enhancements** (1024px+):
- Multi-column layouts (up to 3-4 columns)
- Hover states and micro-interactions
- Larger imagery and more whitespace
- Advanced navigation patterns
- Keyboard shortcuts and accessibility

### Touch & Interaction Targets

**Minimum Sizes** (Accessibility compliant):
- Touch targets: `44px × 44px` minimum
- Spacing between targets: `8px` minimum
- Text links: `44px` height clickable area
- Form inputs: `44px` height minimum

## ♿ Accessibility & Inclusion

### Color & Contrast (WCAG AA+)

**Contrast Ratios**:
- Normal text: `4.5:1` minimum (WCAG AA)
- Large text (18px+): `3:1` minimum
- UI components: `3:1` minimum
- Focus indicators: `3:1` minimum

**Color Independence**:
- Never rely solely on color to convey information
- Use icons, text, or patterns as alternatives
- Support colorblind users with distinct patterns

### Keyboard & Screen Reader Support

**Focus Management**:
- Visible focus indicators with `2px` outline + `2px` offset
- Logical tab order following content flow
- Focus trapping in modals and dropdowns
- Skip links for main content areas

**ARIA & Semantic HTML**:
- Proper heading hierarchy (h1 → h2 → h3)
- ARIA labels for icon buttons and complex components
- Live regions for dynamic content updates
- Semantic landmarks (nav, main, aside, footer)

**Screen Reader Optimization**:
- Descriptive alt text for images
- Form labels explicitly associated with inputs
- Error messages linked to form fields
- Loading states announced to screen readers

## 🚀 Modern Technology Stack

### Core Framework & Build Tools

**Frontend Framework**:
- **Next.js**: `14.x` (App Router) for React applications with SSR/SSG
- **React**: `18.x` with modern hooks and concurrent features
- **TypeScript**: `5.x` for type safety and developer experience

**Build & Development**:
- **Vite**: Fast development and building (alternative to Next.js)
- **ESLint**: Code linting with React and TypeScript rules
- **Prettier**: Code formatting for consistency

### Styling & Design Implementation

**CSS Strategy**:
- **Tailwind CSS**: `3.x` for utility-first styling with custom design system
- **CSS Modules**: For component-specific styles when needed
- **PostCSS**: For CSS processing and autoprefixing

**Component Libraries**:
- **Ant Design (Default)**: Primary component library with comprehensive React components, built-in theming, and professional design system
- **Alternative Options** (when specifically requested):
  - **Headless UI**: For accessible, unstyled components
  - **Radix UI**: For complex, accessible components
  - **Custom Components**: Built with design system specifications

### 🐜 **ANT DESIGN IMPLEMENTATION (DEFAULT)**

**CRITICAL**: Use Ant Design as the default component library for all frontends unless explicitly specified otherwise by the user.

#### **Core Ant Design Setup**:
- **Package**: `antd` latest stable version
- **Icons**: `@ant-design/icons` for comprehensive icon library
- **Styling**: `@ant-design/cssinjs` for CSS-in-JS theming
- **Date Handling**: Integrate with Day.js (Ant Design's preferred date library)

#### **Ant Design Component Usage**:

**Form Components** (Default choices):
- **Form**: `Form` component with built-in validation
- **Input**: `Input`, `Input.TextArea`, `Input.Password`
- **Select**: `Select` with search and multi-select capabilities
- **DatePicker**: `DatePicker`, `RangePicker` for date selections
- **Upload**: `Upload` with drag-and-drop support
- **Button**: `Button` with various types and sizes

**Layout Components**:
- **Layout**: `Layout`, `Header`, `Content`, `Footer`, `Sider`
- **Grid**: `Row` and `Col` for responsive layouts
- **Space**: `Space` for consistent spacing between elements
- **Divider**: `Divider` for visual separation

**Navigation Components**:
- **Menu**: `Menu` for navigation with nested items
- **Breadcrumb**: `Breadcrumb` for navigation hierarchy
- **Pagination**: `Pagination` for data navigation
- **Steps**: `Steps` for multi-step processes

**Data Display Components**:
- **Table**: `Table` with sorting, filtering, and pagination
- **List**: `List` for structured data display
- **Card**: `Card` for content containers
- **Descriptions**: `Descriptions` for detailed information display
- **Tag**: `Tag` for labels and categories

**Feedback Components**:
- **Alert**: `Alert` for important messages
- **Message**: `message` for global feedback
- **Notification**: `notification` for system notifications
- **Modal**: `Modal` for dialogs and confirmations
- **Popconfirm**: `Popconfirm` for action confirmations

#### **Ant Design Theming Configuration**:

**Custom Theme Setup**:
- **Primary Colors**: Customize based on project branding requirements
- **Component Styling**: Control height, border radius, and spacing for accessibility
- **Typography**: Set font families and sizing for consistency
- **Layout Tokens**: Configure spacing, shadows, and component behavior

**Responsive Design with Ant Design**:
- Use Ant Design's built-in responsive grid system
- Leverage breakpoint utilities: `xs`, `sm`, `md`, `lg`, `xl`, `xxl`
- Implement responsive props for components (e.g., `Table` responsive scrolling)

#### **Ant Design Best Practices**:

**Performance Optimization**:
- Use tree-shaking to include only used components
- Implement proper `import` statements: `import { Button } from 'antd'`
- Configure babel-plugin-import for automatic tree-shaking

**Accessibility Compliance**:
- Leverage Ant Design's built-in accessibility features
- Test with keyboard navigation and screen readers
- Customize ARIA labels when needed

**Customization Guidelines**:
- Use CSS-in-JS theming rather than global CSS overrides
- Implement custom components that extend Ant Design components
- Maintain consistency with Ant Design's design language

#### **Tutorial System Integration**:
- **Tutorial Tooltips**: Use Ant Design's `Tooltip` and `Popover` components
- **Tour Component**: Utilize Ant Design's `Tour` component for guided tours
- **Progress Indicator**: Use `Progress` component for tutorial completion
- **Navigation**: Implement with `Button` components and consistent styling

#### **Common Component Patterns**:

**Form Implementation**:
- **Form.Item**: Use for consistent spacing and validation
- **Validation Rules**: Leverage built-in validation with custom rules
- **Error Handling**: Implement proper error display and recovery

**Data Table Implementation**:
- **Column Configuration**: Define sortable, filterable columns
- **Pagination**: Implement for large datasets with customizable page sizes
- **Action Buttons**: Use Space component for consistent button grouping

### State Management & Data Fetching

**State Management**:
- **Zustand**: Lightweight, modern state management for simple-medium projects
- **Redux Toolkit**: For complex state management needs
- **React Context**: For simple shared state

**Data Fetching**:
- **TanStack Query**: For server state management and caching
- **SWR**: Alternative for data fetching
- **Axios**: For HTTP client with interceptors

### Additional Libraries

**UI Enhancement**:
- **React Hook Form**: For performant, flexible forms
- **Framer Motion**: For beautiful animations and page transitions
- **React Hot Toast**: For elegant notification system
- **React Icons**: Comprehensive icon library
- **Date-fns**: For date manipulation and formatting

## 🎓 **MANDATORY TUTORIAL/ONBOARDING SYSTEM**

**CRITICAL**: Every frontend MUST include a comprehensive, built-in tutorial/onboarding system. This is a core requirement, not optional.

#### **Tutorial System Libraries**:
- **Primary**: Intro.js, Shepherd.js, or Reactour for React applications
- **Custom Implementation**: Overlay divs with z-index management for specific needs
- **State Management**: Tutorial progress tracking with localStorage persistence
- **Analytics**: Tutorial completion and drop-off tracking

#### **Tutorial System Components**:

**Core Tutorial Components**:
- **Tutorial Overlay**: Semi-transparent backdrop (rgba(0,0,0,0.7)) with spotlight effect
- **Tutorial Tooltip**: Positioned tooltip with arrow, description, and navigation controls
- **Progress Indicator**: Visual progress bar showing tutorial completion (e.g., "3 of 8")
- **Navigation Controls**: Previous, Next, Skip, and Exit buttons
- **Tutorial Menu**: Always-accessible help menu for re-starting tutorials

**Tutorial Content Structure**:
1. **Welcome Screen**: Brief app introduction with key value propositions
2. **Navigation Tour**: How to move around the application (menu, breadcrumbs, etc.)
3. **Core Features**: 3-5 most important features with interactive demonstrations
4. **Primary Actions**: Key actions users will perform regularly
5. **Help & Support**: Where to find documentation, contact support, or get help

#### **Implementation Specifications**:

**Visual Design**:
- **Spotlight Effect**: Highlighted element with 8px border-radius, white border
- **Backdrop**: Semi-transparent overlay (rgba(0,0,0,0.7)) covering entire viewport
- **Tooltip Design**: White background, Level 4 shadow, 12px border-radius
- **Typography**: Body M for descriptions, Label for buttons
- **Colors**: Primary color for action buttons, Gray-600 for secondary text
- **Animation**: 300ms smooth transitions between steps

**Responsive Behavior**:
- **Mobile**: Tooltip positioning adapts to avoid viewport edges
- **Tablet**: Larger tooltip sizes with more comfortable spacing
- **Desktop**: Full-featured tooltips with detailed descriptions

**Accessibility**:
- **Keyboard Navigation**: Arrow keys, Enter, and Esc key support
- **Screen Reader**: ARIA labels and announcements for tutorial steps
- **Focus Management**: Proper focus trapping and restoration
- **Skip Options**: Easy skip/exit options for experienced users

#### **Audience-Specific Tutorial Adaptations**:

**Business/Enterprise Applications**:
- Focus on efficiency, workflow optimization, and data insights
- Highlight reporting features, collaboration tools, and integrations
- Emphasize security features and admin controls

**Consumer/General Applications**:
- Emphasize fun, discovery, and social features
- Show personalization options and customization
- Highlight sharing and social interaction features

**Creative/Portfolio Applications**:
- Showcase creation tools and artistic features
- Highlight customization options and themes
- Show portfolio organization and presentation features

**Technical/Developer Applications**:
- Show advanced features, integrations, and API access
- Highlight customization options and developer tools
- Demonstrate automation features and workflow optimization

#### **Quality Requirements**:
- Track completion rates and identify drop-off points
- Update tutorials when UI changes
- Test tutorials on all supported devices and browsers
- Automated tests for tutorial functionality

## 📁 Modern File Structure

```
src/
├── app/                    # Next.js app directory (if using App Router)
│   ├── globals.css        # Global styles and Tailwind imports
│   ├── layout.tsx         # Root layout component
│   └── page.tsx           # Home page
├── components/
│   ├── ui/                # Base design system components
│   │   ├── Button.tsx     # Button variants
│   │   ├── Input.tsx      # Form inputs
│   │   ├── Card.tsx       # Card component
│   │   ├── Modal.tsx      # Modal/dialog system
│   │   └── index.ts       # Component exports
│   ├── forms/             # Form-specific components
│   │   ├── LoginForm.tsx
│   │   ├── ContactForm.tsx
│   │   └── index.ts
│   ├── layout/            # Layout components
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   ├── Sidebar.tsx
│   │   └── Navigation.tsx
│   └── features/          # Feature-specific components
│       ├── auth/
│       ├── dashboard/
│       └── settings/
├── hooks/                 # Custom React hooks
│   ├── useAuth.ts
│   ├── useApi.ts
│   └── useLocalStorage.ts
├── lib/                   # Utility libraries
│   ├── api.ts            # API client configuration
│   ├── auth.ts           # Authentication utilities
│   ├── utils.ts          # General utilities
│   └── validations.ts    # Form validation schemas
├── store/                 # State management
│   ├── authStore.ts      # Authentication state
│   ├── uiStore.ts        # UI state (modals, loading)
│   └── index.ts          # Store configuration
├── styles/               # Styling files
│   ├── globals.css       # Global styles
│   ├── components.css    # Component-specific styles
│   └── tailwind.css      # Tailwind customizations
├── types/                # TypeScript type definitions
│   ├── api.ts           # API response types
│   ├── auth.ts          # Authentication types
│   └── common.ts        # Shared types
└── utils/               # Pure utility functions
    ├── formatting.ts    # Date, number formatting
    ├── validation.ts    # Validation helpers
    └── constants.ts     # Application constants
```

## 🎯 Implementation Best Practices

### Performance Optimization

**Bundle Optimization**:
- Code splitting at route and component levels
- Dynamic imports for heavy components
- Tree shaking for unused code elimination
- Asset optimization (images, fonts, CSS)

**Runtime Performance**:
- React.memo for expensive components
- useMemo and useCallback for expensive calculations
- Virtual scrolling for large data sets
- Image optimization with Next.js Image component

**Loading Strategies**:
- Skeleton screens for better perceived performance
- Progressive loading for images and content
- Lazy loading for below-the-fold content
- Service workers for caching (when appropriate)

### Developer Experience

**Type Safety**:
- Strict TypeScript configuration
- API response typing with Zod or similar
- Component prop interfaces
- Custom hook typing

**Code Quality**:
- ESLint with React and TypeScript rules
- Prettier for consistent formatting
- Husky for pre-commit hooks
- Conventional commits for better git history

### Testing Strategy

**Testing Framework**:
- **Vitest**: Fast unit testing for components and utilities
- **React Testing Library**: Component testing with user-centric approach
- **Playwright**: End-to-end testing with visual regression
- **MSW**: API mocking for consistent testing

**Testing Patterns**:
- Unit tests for utility functions and custom hooks
- Component tests for user interactions and rendering
- Integration tests for complete user flows
- Visual regression tests for UI consistency

## 🎨 Design System Implementation

### Tailwind Configuration

**Custom Design System Setup**:
- **Color Extensions**: Primary brand colors with proper contrast ratios
- **Typography**: Custom font families (Inter, Outfit) for modern appearance
- **Spacing**: Extended spacing scale for consistent layouts
- **Shadows**: Multi-level shadow system for depth and hierarchy
- **Plugins**: Forms and typography plugins for enhanced styling

### Component Implementation Standards

**TypeScript Component Patterns**:
- **Props Interface**: Extend native HTML element props for flexibility
- **Variant System**: Support multiple visual styles (primary/secondary/ghost)
- **Size System**: Responsive sizing (sm/md/lg) with proper touch targets
- **State Management**: Handle loading, disabled, and interactive states
- **Accessibility**: Built-in focus management and ARIA support

## 📊 Success Metrics & Quality Gates

### Performance Targets

- **First Contentful Paint**: < 1.5s
- **Largest Contentful Paint**: < 2.5s
- **Cumulative Layout Shift**: < 0.1
- **First Input Delay**: < 100ms
- **Lighthouse Score**: 90+ for all categories

### Accessibility Goals

- **WCAG AA Compliance**: 100% for all interactive elements
- **Keyboard Navigation**: Full functionality without mouse
- **Screen Reader Support**: Comprehensive ARIA implementation
- **Color Contrast**: Minimum 4.5:1 for all text

## 🎨 CRITICAL: Visual Quality Assurance & Testing Protocol

### ⚠️ MANDATORY Visual Testing Requirements

**NEVER ASSUME BEAUTY** - Don't assume the frontend is beautifully implemented. ALWAYS rely on Playwright screenshot tests to ensure visual quality and design conformity.

### Visual Testing Implementation Strategy

#### 1. Screenshot Test Coverage

**Required Screenshot Tests**:
- **Homepage/Landing**: Desktop (1920x1080), Tablet (768x1024), Mobile (375x667)
- **All Major Pages**: Dashboard, Profile, Settings, etc. at all breakpoints
- **Component States**: Hover, focus, loading, error, empty states
- **Form Interactions**: Focus states, validation errors, success states
- **Navigation**: Open/closed states, responsive menu behavior
- **Modals & Overlays**: Proper positioning and backdrop rendering

#### 2. Visual Quality Checklist

**Contrast & Color Analysis**:
- [ ] All text meets WCAG AA contrast ratios (4.5:1 minimum)
- [ ] No jarring color combinations (e.g., black text on purple backgrounds)
- [ ] Consistent color palette application across all components
- [ ] Proper semantic color usage (success=green, error=red, etc.)
- [ ] Brand colors applied consistently

**Typography & Spacing**:
- [ ] Consistent font sizes and weights throughout
- [ ] Proper line heights for readability
- [ ] Consistent spacing between elements
- [ ] Proper heading hierarchy (h1→h2→h3)
- [ ] Text doesn't break or overflow containers

**Layout & Responsive Design**:
- [ ] No horizontal scrolling on mobile devices
- [ ] Touch targets are minimum 44px on mobile
- [ ] Elements stack properly at different screen sizes
- [ ] No overlapping or cut-off content
- [ ] Consistent alignment and grid structure

**Interactive Elements**:
- [ ] Clear hover states for all interactive elements
- [ ] Focus indicators visible and well-designed
- [ ] Loading states are visually appealing
- [ ] Error states are clear but not aggressive
- [ ] Success states provide positive feedback

#### 3. Playwright Visual Testing Implementation

**Test Structure Requirements**:
- **Multi-Breakpoint Testing**: Desktop (1920x1080), Tablet (768x1024), Mobile (375x667)
- **Interactive State Testing**: Hover, focus, and active states for all interactive elements
- **Error State Testing**: API failure scenarios with proper error display
- **Loading State Testing**: Async operations with loading indicators
- **Navigation Testing**: Menu states, responsive behavior, and transitions
- **Form Testing**: Validation states, focus management, and submission flows

#### 4. Visual Quality Police Protocol

**Review Process**:
1. **Take Screenshots**: Capture all major pages and components
2. **Analyze Contrast**: Use browser dev tools to check color contrast ratios
3. **Compare to Design**: Reference the visual inspiration and design specs
4. **Identify Issues**: Document any visual problems or inconsistencies
5. **Fix and Re-test**: Implement fixes and re-run visual tests
6. **Iterate Until Perfect**: Continue until all visual tests pass

**Common Issues to Watch For**:
- Text that's too light on backgrounds (poor contrast)
- Elements that are cut off or overflow
- Inconsistent spacing or alignment
- Buttons or links that don't look clickable
- Missing hover or focus states
- Broken responsive layouts
- Colors that clash or look unprofessional
- Typography that's too small or hard to read
- Loading states that look broken or confusing

#### 5. Automated Visual Regression Testing

**CI/CD Integration**:
- Run visual tests on every pull request
- Compare screenshots against baseline images
- Flag any visual changes for manual review
- Block deployments if critical visual tests fail

**Baseline Management**:
- Update baselines when intentional design changes are made
- Maintain separate baselines for different environments
- Regular baseline audits to ensure quality standards

This comprehensive component catalog ensures that all UI components referenced in use cases have detailed implementation specifications for consistent, reliable frontend development.
