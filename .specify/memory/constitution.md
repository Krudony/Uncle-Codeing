# Uncle-Codeing Project Constitution

## Core Principles

### I. React-First Frontend
All mobile applications must be built using React Native for cross-platform compatibility. Components must be self-contained, independently testable, and documented. Clear purpose required - no UI-only components without business logic.

### II. Rust Backend Services
All backend services, audio processing, and performance-critical components must be implemented in Rust for maximum performance and memory safety. Services expose functionality via well-defined APIs with clear contracts.

### III. Test-First (NON-NEGOTIABLE)
TDD mandatory: Tests written → User approved → Tests fail → Then implement. Red-Green-Refactor cycle strictly enforced for both React and Rust components.

### IV. Mobile-First Architecture
All features must work seamlessly on mobile devices. Focus areas requiring special attention: Background processing, Audio management, Battery optimization, Cross-device compatibility.

### V. Resource Efficiency
Maximum performance with minimum resource usage. Battery consumption <1% daily, Memory usage <50MB, Startup time <2 seconds. YAGNI principles applied to feature development.

## Technology Stack Requirements

### Frontend (Mobile)
- **Framework**: React Native with Expo for development
- **Language**: TypeScript for type safety
- **State Management**: Context API + useReducer for simplicity
- **Navigation**: React Navigation
- **UI Styling**: Tailwind CSS via NativeWind for modern, responsive design
- **UI Components**: Custom components styled with Tailwind CSS classes

### Backend (Services)
- **Language**: Rust 1.75+
- **Web Framework**: Actix-web or Axum for HTTP services
- **Audio Processing**: Rodio or cpal for audio playback
- **Async Runtime**: Tokio
- **Serialization**: Serde

### Integration & Testing
- **Development**: Expo CLI for rapid iteration
- **Testing**: Jest for React, cargo test for Rust
- **Styling**: NativeWind for Tailwind CSS integration with React Native
- **CI/CD**: GitHub Actions
- **Deployment**: Expo Application Services (EAS)

## Development Workflow

### Feature Development Process
1. **Specification**: Create detailed spec using `/speckit.specify`
2. **Planning**: Generate implementation plan with `/speckit.plan`
3. **Constitution Check**: Verify compliance with technology stack requirements
4. **Implementation**: React Native frontend + Rust backend development
5. **Testing**: Unit tests, integration tests, device testing
6. **Review**: Code review ensures constitution compliance
7. **Deployment**: Expo deployment with Rust backend services

### Quality Gates
- All features must pass automated tests
- Memory usage must be monitored and optimized
- Battery consumption must be measured and validated
- Cross-device testing required for mobile features
- Constitution compliance verified in all PRs

## Governance

This constitution supersedes all other practices and templates. All specifications, plans, and implementations must adhere to these requirements. Amendments require documentation, approval, and migration plan.

**Compliance Rules**:
- All PRs/reviews must verify React + Rust stack compliance
- Mobile performance requirements are non-negotiable
- Resource efficiency must be measured and validated
- Use this constitution for all runtime development guidance

**Version**: 1.0.0 | **Ratified**: 2025-01-24 | **Last Amended**: 2025-01-24
