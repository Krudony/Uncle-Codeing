---

description: "Task list for React Native + Rust Bell Notification App implementation"
---

# Tasks: React Native + Rust Bell Notification App

**Input**: Design documents from `/specs/001-bell-notification-v2/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Tests are OPTIONAL - only include test tasks if explicitly requested during implementation.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Frontend**: `frontend/src/`, `frontend/`
- **Backend**: `backend/src/`, `backend/`
- **Contracts**: Shared between frontend and backend
- Paths follow the mobile + backend service architecture from plan.md

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure
**วัตถุประสงค์**: การสร้างโครงสร้างโปรเจคและการตั้งค่าเบื้องต้น

- [ ] T001 Create project structure with frontend/ and backend/ directories per implementation plan
- [ ] T002 Initialize React Native Expo project with TypeScript dependencies in frontend/
- [ ] T003 Initialize Rust project with Actix-web and required dependencies in backend/
- [ ] T004 [P] Configure ESLint and Prettier for frontend TypeScript code
- [ ] T005 [P] Configure Rust formatting and clippy for backend code
- [ ] T006 [P] Setup Git repository with .gitignore for mobile and Rust projects
- [ ] T007 Create environment configuration files (.env.example) for both frontend and backend

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented
**วัตถุประสงค์**: โครงสร้างพื้นฐานที่ต้องเสร็จสมบูรณ์ก่อนการทำงาน User Story ใดๆ

**⚠️ CRITICAL**: No user story work can begin until this phase is complete
**⚠️ ข้อควรทราบ**: ไม่สามารถเริ่มทำงาน User Story ใดๆ ได้จนกว่า Phase นี้จะเสร็จสิ้น

- [ ] T008 Setup SQLite database schema with migrations in backend/src/database/migrations/
- [ ] T009 [P] Implement database connection and pool management in backend/src/database/mod.rs
- [ ] T010 [P] Create shared type definitions from contracts/types.json in frontend/src/types/ and backend/src/types/
- [ ] T011 [P] Setup API routing structure in backend/src/api/mod.rs with health check endpoint
- [ ] T012 [P] Configure error handling middleware for backend API responses
- [ ] T013 [P] Setup logging infrastructure for both frontend and backend
- [ ] T014 Create base data models (User, BellSchedule, BellType) in backend/src/database/models/
- [ ] T015 [P] Setup HTTP client service in frontend/src/services/ApiService.ts
- [ ] T016 [P] Configure Tailwind CSS and NativeWind in frontend/
- [ ] T017 Setup React Navigation structure in frontend/src/navigation/

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel
**จุดตรวจสอบ**: โครงสร้างพื้นฐานพร้อม - สามารถเริ่มทำงาน User Story ได้พร้อมกัน

---

## Phase 3: User Story 1 - Instant Bell Access (Priority: P1) 🎯 MVP

**Goal**: Users can trigger bell audio immediately through React Native interface with <100ms latency
**เป้าหมาย**: ผู้ใช้สามารถกดเล่นเสียงระฆังทันทีผ่าน React Native interface ด้วยความหน่วง <100ms

**Independent Test**: Install app, tap bell button, confirm audio plays within 100ms with smooth UI animations
**การทดสอบอิสระ**: ติดตั้งแอป กดปุ่มระฆัง และยืนยันว่าเสียงเล่นภายใน 100ms พร้อม animation ที่ลื่นไหล

### Tests for User Story 1 (OPTIONAL - only if tests requested) ⚠️

> **NOTE: Write these tests FIRST, ensure they FAIL before implementation**
> **หมายเหตุ**: เขียน test ก่อนเสมอ และตรวจสอบว่า FAIL ก่อนการ implement

- [ ] T018 [P] [US1] Contract test for /audio/play endpoint in backend/src/tests/api/audio_test.rs
- [ ] T019 [P] [US1] Integration test for bell button journey in frontend/src/__tests__/BellButton.test.tsx

### Implementation for User Story 1

- [ ] T020 [P] [US1] Create BellType entity model in backend/src/database/models/bell_type.rs
- [ ] T021 [P] [US1] Create AudioSession entity model in backend/src/database/models/audio_session.rs
- [ ] T022 [US1] Implement audio processing with CPAL in backend/src/audio/player.rs
- [ ] T023 [US1] Implement play bell API endpoint in backend/src/api/handlers/audio.rs
- [ ] T024 [US1] Create BellButton component with Tailwind styling in frontend/src/components/BellButton/BellButton.tsx
- [ ] T025 [US1] Implement AudioService for backend communication in frontend/src/services/AudioService.ts
- [ ] T026 [US1] Create HomeScreen with bell button interface in frontend/src/screens/HomeScreen.tsx
- [ ] T027 [US1] Add bell animation styles with NativeWind in frontend/src/components/BellButton/BellButton.styles.ts
- [ ] T028 [US1] Add audio playback error handling and user feedback
- [ ] T029 [US1] Add logging for audio operations in both frontend and backend

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently
**จุดตรวจสอบ**: ณ จุดนี้ User Story 1 ควรทำงานได้เต็มรูปแบบและทดสอบได้โดยอิสระ

---

## Phase 4: User Story 2 - High-Performance Background Operation (Priority: P1)

**Goal**: Background notifications work efficiently with <1% battery consumption using Rust optimization
**เป้าหมาย**: การแจ้งเตือนเบื้องหลังทำงานอย่างมีประสิทธิภาพด้วยการใช้แบตเตอรี่ <1% ต่อวัน ผ่านการปรับแต่งของ Rust

**Independent Test**: Run background bell notifications for 24 hours and measure <1% battery consumption
**การทดสอบอิสระ**: ทดสอบการแจ้งเตือนเบื้องหลังเป็นเวลา 24 ชั่วโมงและวัดการใช้แบตเตอรี่ <1%

### Tests for User Story 2 (OPTIONAL - only if tests requested) ⚠️

- [ ] T030 [P] [US2] Background task integration test in backend/src/tests/background/scheduler_test.rs
- [ ] T031 [P] [US2] Battery usage measurement test in backend/src/tests/performance/battery_test.rs

### Implementation for User Story 2

- [ ] T032 [P] [US2] Create BellSchedule entity model in backend/src/database/models/bell_schedule.rs
- [ ] T033 [P] [US2] Create NotificationHistory entity model in backend/src/database/models/notification_history.rs
- [ ] T034 [US2] Implement background task scheduler with Tokio in backend/src/audio/scheduler.rs
- [ ] T035 [US2] Implement battery-efficient audio processing in backend/src/audio/power_optimizer.rs
- [ ] T036 [US2] Create background job configuration for React Native in frontend/src/services/BackgroundService.ts
- [ ] T037 [US2] Implement schedule management API endpoints in backend/src/api/handlers/schedules.rs
- [ ] T038 [US2] Add Android background permissions and configuration in frontend/app.json
- [ ] T039 [US2] Optimize memory usage for long-running background service
- [ ] T040 [US2] Integrate background scheduler with audio player in backend/src/audio/mod.rs

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently
**จุดตรวจสอบ**: ณ จุดนี้ User Story 1 และ 2 ควรทำงานได้โดยอิสระทั้งสองเรื่อง

---

## Phase 5: User Story 3 - Cross-Platform Resource Efficiency (Priority: P1)

**Goal**: App maintains <50MB memory usage and works across all Android 6.0+ devices
**เป้าหมาย**: แอปรักษาการใช้หน่วยความจำ <50MB และทำงานได้บนอุปกรณ์ Android 6.0+ ทุกรุ่น

**Independent Test**: Test across different Android devices and confirm <50MB memory usage consistently
**การทดสอบอิสระ**: ทดสอบบนอุปกรณ์ Android ต่างๆ และยืนยันการใช้หน่วยความจำ <50MB อย่างสม่ำเสมอ

### Tests for User Story 3 (OPTIONAL - only if tests requested) ⚠️

- [ ] T041 [P] [US3] Memory usage test across devices in backend/src/tests/performance/memory_test.rs
- [ ] T042 [P] [US3] Cross-device compatibility test in frontend/src/__tests__/compatibility/DeviceTest.tsx

### Implementation for User Story 3

- [ ] T043 [P] [US3] Create SystemStatus API endpoint for monitoring in backend/src/api/handlers/system.rs
- [ ] T044 [US3] Implement memory monitoring and optimization in backend/src/utils/memory_monitor.rs
- [ ] T045 [US3] Add device-specific audio optimizations in backend/src/audio/device_optimizer.rs
- [ ] T046 [US3] Configure React Native for Android 6.0+ compatibility in frontend/app.json
- [ ] T047 [US3] Implement resource usage tracking in frontend/src/services/ResourceMonitor.ts
- [ ] T048 [US3] Add memory-efficient image and asset loading in frontend/src/utils/AssetLoader.ts
- [ ] T049 [US3] Optimize Tailwind CSS bundle size for mobile in frontend/tailwind.config.js
- [ ] T050 [US3] Add device capability detection and adaptive behavior

**Checkpoint**: All user stories should now be independently functional
**จุดตรวจสอบ**: User Stories ทั้งหมดควรทำงานได้โดยอิสระในขณะนี้

---

## Phase 6: User Story 4 - Expo Development Workflow (Priority: P2)

**Goal**: Enable rapid development through Expo QR code with production-equivalent performance
**เป้าหมาย**: ให้การพัฒนารวดเร็วผ่าน Expo QR code ด้วยประสิทธิภาพเทียบเท่า production

**Independent Test**: Successfully test changes through Expo QR code and confirm equivalent performance
**การทดสอบอิสระ**: ทดสอบการเปลี่ยนแปลงผ่าน Expo QR code สำเร็จและยืนยันประสิทธิภาพเทียบเท่า

### Implementation for User Story 4

- [ ] T051 [P] [US4] Configure Expo development server settings in frontend/eas.json
- [ ] T052 [US4] Setup Metro bundler optimization for development in frontend/metro.config.js
- [ ] T054 [US4] Create development build configuration for testing
- [ ] T055 [US4] Add development vs production environment handling in frontend/src/utils/Environment.ts
- [ ] T056 [US4] Optimize backend for local development connections
- [ ] T057 [US4] Create development documentation and QR code testing guide

---

## Phase 7: User Story 5 - Modern UI/UX with Tailwind CSS (Priority: P2)

**Goal**: Beautiful, responsive interface with smooth animations across all screen sizes
**เป้าหมาย**: ส่วนติดต่อที่สวยงาม ตอบสนองได้ดี พร้อม animation ที่ลื่นไหลบนหน้าจอขนาดต่างๆ

**Independent Test**: Test UI responsiveness and animations across different screen sizes and Android versions
**การทดสอบอิสระ**: ทดสอบการตอบสนองของ UI และ animation บนหน้าจอขนาดต่างๆ และ Android version ต่างๆ

### Implementation for User Story 5

- [ ] T058 [P] [US5] Create SettingsScreen component with Tailwind styling in frontend/src/screens/SettingsScreen.tsx
- [ ] T059 [P] [US5] Design responsive layout components in frontend/src/components/Layout/
- [ ] T060 [US5] Add custom bell animation keyframes in frontend/tailwind.config.js
- [ ] T061 [US5] Implement dark/light theme switching with NativeWind in frontend/src/context/ThemeContext.tsx
- [ ] T062 [US5] Create schedule card components with Tailwind in frontend/src/components/ScheduleCard/
- [ ] T063 [US5] Add touch feedback and haptic responses in frontend/src/utils/HapticFeedback.ts
- [ ] T064 [US5] Optimize animations for 60fps performance using React Native Reanimated

---

## Phase 8: User Story 6 - User Preference Management (Priority: P2)

**Goal**: Flexible control over silent/vibrate mode behavior through intuitive settings
**เป้าหมาย**: การควบคุมโหมดเงียบ/สั่นสะเทือนอย่างยืดหยุ่นผ่านการตั้งค่าที่ใช้งานง่าย

**Independent Test**: Test different preference settings and confirm backend responds correctly to each configuration
**การทดสอบอิสระ**: ทดสอบการตั้งค่าต่างๆ และยืนยันว่า backend ตอบสนองถูกต้องกับแต่ละการตั้งค่า

### Implementation for User Story 6

- [ ] T065 [P] [US6] Create UserPreferences entity model in backend/src/database/models/user_preferences.rs
- [ ] T066 [US6] Implement user preferences API endpoints in backend/src/api/handlers/preferences.rs
- [ ] T067 [US6] Create preference management components in frontend/src/components/Preferences/
- [ ] T068 [US6] Implement silent mode behavior logic in backend/src/audio/silent_mode_handler.rs
- [ ] T069 [US6] Add preferences storage service in frontend/src/services/PreferencesService.ts
- [ ] T070 [US6] Create settings screens with Tailwind styling and validation

---

## Phase 9: User Story 7 - Type Safety and Reliability (Priority: P2)

**Goal**: Robust codebase with TypeScript type safety and Rust memory safety
**เป้าหมาย**: โค้ดที่แข็งแกร่งด้วย TypeScript type safety และ Rust memory safety

**Independent Test**: Verify absence of type-related runtime errors through comprehensive test coverage
**การทดสอบอิสระ**: ตรวจสอบว่าไม่มี runtime errors ที่เกี่ยวข้องกับ type ผ่านการทดสอบอย่างครอบคลุม

### Implementation for User Story 7

- [ ] T071 [P] [US7] Add comprehensive TypeScript interfaces in frontend/src/types/
- [ ] T072 [P] [US7] Add Rust error types and proper error handling in backend/src/error/
- [ ] T073 [US7] Implement API response validation with TypeScript in frontend/src/utils/Validation.ts
- [ ] T074 [US7] Add Rust compile-time guarantees for audio thread safety
- [ ] T075 [US7] Create shared type definitions from contracts for both frontend and backend
- [ ] T076 [US7] Add runtime type checking for API communications

---

## Phase 10: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories
**วัตถุประสงค์**: การปรับปรุงที่ส่งผลกระทบต่อ User Stories หลายๆ เรื่อง

- [ ] T077 [P] Add comprehensive error logging and monitoring
- [ ] T078 [P] Implement performance monitoring dashboard
- [ ] T079 Add audio file validation and management
- [ ] T080 Create comprehensive README and setup documentation
- [ ] T081 Add security best practices and input sanitization
- [ ] T082 [P] Run quickstart.md validation and fix any issues
- [ ] T083 Optimize bundle sizes and loading times
- [ ] T084 Add backup and restore functionality for user data
- [ ] T085 Create production build configurations and deployment scripts

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3-9)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2)
- **Polish (Phase 10)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational - No dependencies on other stories
- **User Story 2 (P1)**: Can start after Foundational - May integrate with US1 but should be independently testable
- **User Story 3 (P1)**: Can start after Foundational - Works across all stories
- **User Story 4 (P2)**: Can start after Foundational - Development workflow enhancement
- **User Story 5 (P2)**: Can start after Foundational - UI improvements for all stories
- **User Story 6 (P2)**: Can start after Foundational - Integrates with audio playback
- **User Story 7 (P2)**: Can start after Foundational - Type safety across all components

### Within Each User Story

- Tests (if included) MUST be written and FAIL before implementation
- Models before services
- Services before endpoints
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- All tests for a user story marked [P] can run in parallel
- Models within a story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# Launch all tests for User Story 1 together (if tests requested):
Task: "Contract test for /audio/play endpoint in backend/src/tests/api/audio_test.rs"
Task: "Integration test for bell button journey in frontend/src/__tests__/BellButton.test.tsx"

# Launch all models for User Story 1 together:
Task: "Create BellType entity model in backend/src/database/models/bell_type.rs"
Task: "Create AudioSession entity model in backend/src/database/models/audio_session.rs"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Add User Stories 4-7 → Test and deploy
6. Complete Polish phase → Full production ready

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1 + 4 (Frontend focus)
   - Developer B: User Story 2 + 3 (Backend/Audio focus)
   - Developer C: User Story 5 + 6 (UI/Preferences focus)
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Verify tests fail before implementing (if tests are included)
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Focus on performance requirements: <100ms latency, <50MB memory, <1% battery daily
- Ensure TypeScript and Rust type safety throughout implementation

## หมายเหตุ

- [P] tasks = ไฟล์ต่างกัน ไม่มี dependencies
- [Story] label ใช้ระบุ task กับ user story ที่เกี่ยวข้อง
- แต่ละ user story ควรสามารถทำสำเร็จและทดสอบได้โดยอิสระ
- ตรวจสอบว่า tests fail ก่อนการ implement (ถ้ามี tests)
- Commit หลังจากแต่ละ task หรือกลุ่มที่เป็นเรื่องเดียวกัน
- หยุดที่จุดตรวจสอบเพื่อตรวจสอบ story อย่างอิสระ
- เน้นความต้องการด้านประสิทธิภาพ: latency <100ms, memory <50MB, แบตเตอรี่ <1% ต่อวัน
- มั่นใจว่ามี TypeScript และ Rust type safety ตลอดการ implement