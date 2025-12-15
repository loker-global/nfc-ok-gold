# NFC by OK GOLD (OK Tap)
## Product Requirements Document (PRD)

---

## 1. Executive Summary

**Product Name:** NFC by OK GOLD (also known as OK Tap)

**Version:** 1.0

**Last Updated:** December 2025

### Product Overview
NFC by OK GOLD (OK Tap) is a mobile-first NFC (Near Field Communication) reader/writer application designed to provide users with a simple, intuitive, and privacy-focused solution for managing NFC tags. The application enables users to read, write, copy, and bulk manage NFC tags directly from their mobile devices with an emphasis on user anonymity through local storage.

### Vision Statement
To become the most user-friendly and privacy-conscious NFC management tool for mobile devices, empowering users to interact with NFC technology seamlessly without compromising their personal data.

---

## 2. Product Goals & Objectives

### Primary Goals
1. **Simplicity First**: Deliver an intuitive interface that requires minimal learning curve
2. **Privacy by Design**: Keep users anonymous by storing all data locally
3. **Mobile Optimization**: Create a mobile-first experience that feels native and responsive
4. **Versatility**: Support multiple use cases through distinct operational modes
5. **Performance**: Ensure fast, reliable NFC operations with minimal latency

### Success Metrics
- User engagement: Average session duration > 2 minutes
- User satisfaction: App store rating > 4.5 stars
- Adoption: 10,000+ active users within 6 months
- Performance: NFC read/write operations complete in < 2 seconds
- Privacy: Zero data transmitted to external servers (local-first architecture)

---

## 3. Target Audience

### Primary User Personas

#### 1. **Tech Enthusiast - "Alex"**
- Age: 25-35
- Tech-savvy, early adopter
- Uses NFC for smart home automation, business cards, and personal projects
- Values privacy and control over their data
- Needs: Quick tag writing, reliable reads, bulk operations

#### 2. **Small Business Owner - "Sam"**
- Age: 30-50
- Runs a small retail or service business
- Uses NFC tags for product information, payments, or customer engagement
- Moderate tech literacy
- Needs: Bulk writing capabilities, simple interface, consistent results

#### 3. **Event Organizer - "Jordan"**
- Age: 28-45
- Manages events, conferences, or exhibitions
- Uses NFC for attendee check-ins, information kiosks, or interactive experiences
- Values efficiency and reliability
- Needs: Quick copy functionality, bulk operations, fast processing

#### 4. **Casual User - "Taylor"**
- Age: 18-60
- Occasional NFC user for personal convenience
- Limited technical knowledge
- Uses NFC for sharing contacts, Wi-Fi credentials, or URLs
- Needs: Simple read/write, clear instructions, no-fuss interface

---

## 4. Core Features & Functionality

### 4.1 Mode 1: Read Mode 🔍

**Purpose:** Scan and view NFC tag content

**Key Features:**
- **Instant Scan**: Tap phone to NFC tag for immediate content display
- **Content Preview**: Display tag data in human-readable format
- **Tag Information**: Show tag type, size, technology (NTAG, MIFARE, etc.)
- **History Log**: Maintain local history of recently scanned tags
- **Data Export**: Copy tag content to clipboard or share via system share sheet
- **Format Detection**: Auto-detect and display URL, text, vCard, Wi-Fi credentials, etc.

**User Flow:**
1. User opens app and selects "Read" mode
2. App displays "Ready to Scan" with visual indicator
3. User taps phone to NFC tag
4. App reads tag and displays content in formatted view
5. User can copy, share, or save the information

**Technical Requirements:**
- Support for common NFC tag types (NTAG203, NTAG213, NTAG215, NTAG216, MIFARE Classic, etc.)
- Parse NDEF (NFC Data Exchange Format) messages
- Graceful error handling for unreadable or corrupted tags
- Read operation timeout: 3 seconds max

---

### 4.2 Mode 2: Write Mode ✍️

**Purpose:** Write custom data to NFC tags

**Key Features:**
- **Content Type Selector**: Choose from predefined formats
  - Plain Text
  - URL/Website
  - Phone Number
  - Email Address
  - Wi-Fi Credentials
  - vCard (Contact)
  - Custom NDEF message
- **Write Verification**: Confirm successful write operations
- **Write Protection**: Option to lock tags after writing
- **Template Library**: Save frequently used content as templates
- **Preview Before Write**: Show exactly what will be written to the tag
- **Overwrite Warning**: Alert users when attempting to overwrite existing data

**User Flow:**
1. User selects "Write" mode
2. User chooses content type from selector
3. User inputs or selects content (with validation)
4. User previews the data to be written
5. User taps phone to blank or writeable NFC tag
6. App writes data and confirms success
7. Optional: Lock tag to prevent future modifications

**Technical Requirements:**
- NDEF message encoding for all supported formats
- Tag capacity validation before write attempt
- Write verification by reading back written data
- Support for tag locking mechanisms
- Clear error messages for write failures

---

### 4.3 Mode 3: Quick Copy 📋

**Purpose:** Clone NFC tag content to other tags rapidly

**Key Features:**
- **One-Tap Cloning**: Read and immediately prepare to write
- **Source Tag Preview**: Display content from original tag
- **Multi-Target Write**: Write to multiple tags in succession without re-reading source
- **Write Counter**: Track number of successful copies
- **Batch Status**: Visual feedback for each copy attempt
- **Quick Reset**: Easy return to read new source tag

**User Flow:**
1. User selects "Quick Copy" mode
2. User taps phone to source NFC tag (original)
3. App reads and displays source tag content
4. User confirms "Ready to Copy"
5. User taps phone to target NFC tag (blank)
6. App writes source data to target tag
7. User can repeat step 5-6 for additional tags
8. User can reset to select new source tag

**Technical Requirements:**
- Cache source tag data in memory during session
- Fast write operation optimization (< 2 seconds per tag)
- Running counter with success/failure tracking
- Session persistence until user explicitly ends or switches modes

---

### 4.4 Mode 4: Bulk Write 📦

**Purpose:** Write the same content to multiple NFC tags in sequence

**Key Features:**
- **Content Definition**: Define content once for all tags
- **Batch Queue**: Set target number of tags to write
- **Progress Tracking**: Visual progress bar and count (e.g., "5/20 completed")
- **Success/Failure Log**: Detailed log of each write attempt
- **Auto-Continue**: Automatic preparation for next tag after successful write
- **Pause/Resume**: Ability to pause and resume batch operations
- **Summary Report**: Final report with statistics and failed writes

**User Flow:**
1. User selects "Bulk Write" mode
2. User defines content to write (same as Write Mode)
3. User sets target quantity (optional)
4. User confirms and starts batch operation
5. User taps phone to first NFC tag
6. App writes and auto-prepares for next tag
7. User continues tapping tags until batch is complete
8. User reviews summary report with statistics

**Technical Requirements:**
- Session state management for batch operations
- Persistent logging of all write attempts
- Progress persistence across app interruptions
- Export batch report to CSV or text file
- Clear visual and haptic feedback for each operation

---

### 4.5 Additional Modes (Future Considerations)

#### Suggested Mode 5: Format Mode 🗑️
- Erase/format NFC tags
- Reset tags to factory state
- Unlock locked tags (if supported)

#### Suggested Mode 6: Analytics Mode 📊
- View usage statistics
- Most read/written tag types
- Operation history and trends
- Success rate metrics

#### Suggested Mode 7: Backup Mode 💾
- Export all saved templates and history
- Import data from backup file
- Sync across devices via local network (privacy-preserving)

---

## 5. Technical Architecture

### 5.1 Technology Stack

**Platform:**
- React Native (container application)
- WebView component for UI rendering
- Native NFC modules via React Native bridges

**Frontend (WebView):**
- HTML5
- CSS3 (with Flexbox/Grid for responsive design)
- JavaScript (ES6+)
- Optional: React.js or Vue.js for component-based architecture

**Storage:**
- LocalStorage API for simple key-value data
- IndexedDB for structured data (templates, history)
- No external database or cloud storage

**Build Tools:**
- Webpack or Vite for bundling
- Babel for JavaScript transpilation
- PostCSS for CSS processing

### 5.2 WebView ↔ React Native Integration

**Communication Protocol:**

The WebView and React Native container communicate via a custom JavaScript bridge API.

**React Native → WebView (Commands):**
```javascript
// Example: NFC tag detected
window.postMessage({
  type: 'NFC_TAG_DETECTED',
  payload: {
    id: 'tag-unique-id',
    techList: ['NDEF', 'NTAG213'],
    ndefMessage: { /* NDEF data */ }
  }
});
```

**WebView → React Native (Requests):**
```javascript
// Example: Request NFC write
window.ReactNativeWebView.postMessage(JSON.stringify({
  type: 'NFC_WRITE_REQUEST',
  payload: {
    ndefMessage: { /* NDEF data to write */ }
  }
}));
```

**API Contract:**

| Event Type | Direction | Purpose |
|------------|-----------|---------|
| `NFC_TAG_DETECTED` | RN → WebView | Notify WebView of NFC tag scan |
| `NFC_READ_SUCCESS` | RN → WebView | Provide tag data after read |
| `NFC_READ_ERROR` | RN → WebView | Report read failure |
| `NFC_WRITE_REQUEST` | WebView → RN | Request tag write operation |
| `NFC_WRITE_SUCCESS` | RN → WebView | Confirm successful write |
| `NFC_WRITE_ERROR` | RN → WebView | Report write failure |
| `NFC_SESSION_START` | WebView → RN | Enable NFC scanning |
| `NFC_SESSION_END` | WebView → RN | Disable NFC scanning |
| `HAPTIC_FEEDBACK` | WebView → RN | Trigger device vibration |
| `SHARE_DATA` | WebView → RN | Open system share sheet |

### 5.3 Data Storage Schema

**LocalStorage Structure:**
```javascript
{
  "settings": {
    "theme": "light|dark|auto",
    "hapticFeedback": true,
    "defaultMode": "read",
    "autoLockTags": false
  },
  "lastMode": "read"
}
```

**IndexedDB Structure:**
```javascript
// Object Store: readHistory
{
  id: "uuid",
  timestamp: 1234567890,
  tagId: "tag-unique-id",
  tagType: "NTAG213",
  content: { /* parsed NDEF data */ },
  rawData: "base64-encoded-raw-data"
}

// Object Store: templates
{
  id: "uuid",
  name: "My WiFi",
  type: "wifi",
  content: { /* NDEF message */ },
  createdAt: 1234567890,
  lastUsed: 1234567890
}

// Object Store: bulkOperations
{
  id: "uuid",
  startTime: 1234567890,
  endTime: 1234567890,
  targetCount: 20,
  successCount: 18,
  failureCount: 2,
  content: { /* NDEF message */ },
  log: [
    { timestamp: 1234567890, success: true },
    { timestamp: 1234567891, success: true, error: "Tag locked" }
  ]
}
```

---

## 6. User Experience (UX) Design

### 6.1 Design Principles

1. **Mobile-First Always**: Every element optimized for touch and small screens
2. **One-Handed Operation**: Critical actions accessible with thumb
3. **Immediate Feedback**: Visual, haptic, and audio cues for all actions
4. **Progressive Disclosure**: Show only what's needed, when it's needed
5. **Error Prevention**: Validate inputs and confirm destructive actions
6. **Consistent Patterns**: Reuse UI components and interaction patterns
7. **Accessibility**: WCAG 2.1 AA compliance minimum

### 6.2 Visual Design Guidelines

**Color Palette:**
- Primary: Gold/Yellow (#FFD700) - Reflects "OK GOLD" brand
- Secondary: Deep Blue (#1E3A8A) - Trust and technology
- Accent: Emerald Green (#10B981) - Success states
- Error: Red (#EF4444) - Error states
- Neutral: Grays (#F9FAFB to #111827) - Backgrounds and text

**Typography:**
- Headings: Bold, sans-serif (e.g., Inter, SF Pro Display)
- Body: Regular, sans-serif with excellent readability
- Minimum size: 16px for body text
- High contrast ratios: 4.5:1 minimum

**Spacing:**
- Use 8px base unit grid system
- Generous touch targets: Minimum 44x44px
- Adequate white space for visual breathing room

**Icons:**
- Clear, simple, and recognizable
- Consistent style (outline or filled, not mixed)
- Accompanied by labels when needed

### 6.3 Navigation Structure

**Primary Navigation (Bottom Tab Bar):**
```
┌─────────────────────────────────────┐
│                                     │
│         [MAIN CONTENT AREA]         │
│                                     │
├─────────────────────────────────────┤
│  📖 Read  │ ✍️ Write │ 📋 Copy │ 📦 Bulk │
└─────────────────────────────────────┘
```

**Alternative: Mode Selector (Card-based Home):**
```
┌─────────────────────────────────────┐
│    NFC by OK GOLD                   │
│    Select a Mode                    │
├─────────────────────────────────────┤
│  ┌───────────────┐ ┌──────────────┐ │
│  │  🔍 READ      │ │ ✍️ WRITE     │ │
│  │  Scan NFC Tag │ │ Write Data   │ │
│  └───────────────┘ └──────────────┘ │
│  ┌───────────────┐ ┌──────────────┐ │
│  │  📋 QUICK COPY│ │ 📦 BULK WRITE│ │
│  │  Clone Tags   │ │ Multi-Write  │ │
│  └───────────────┘ └──────────────┘ │
└─────────────────────────────────────┘
```

**Secondary Navigation:**
- Settings: Gear icon in top-right
- History: Clock icon in top-right
- Help: Question mark icon

### 6.4 Key Screen Flows

**Read Mode Flow:**
```
Home → Read Mode → [Hold Phone Near Tag] → Tag Detected 
→ Content Display → [Copy/Share/Save]
```

**Write Mode Flow:**
```
Home → Write Mode → Select Content Type → Input Data 
→ Preview → [Hold Phone Near Tag] → Write Success → Confirmation
```

**Quick Copy Flow:**
```
Home → Quick Copy → [Hold Phone to Source Tag] → Content Preview 
→ Ready to Copy → [Hold Phone to Target Tag] → Copy Success 
→ [Repeat or Reset]
```

**Bulk Write Flow:**
```
Home → Bulk Write → Define Content → Set Target Count 
→ Start Batch → [Hold Phone to Tag 1] → Success (1/N) 
→ [Hold Phone to Tag 2] → Success (2/N) → ... 
→ Batch Complete → Summary Report
```

### 6.5 Interaction Patterns

**NFC Scanning State:**
- Animated pulsing circle or icon
- Clear instruction text: "Hold phone near NFC tag"
- Visual representation of phone position
- Haptic feedback on successful scan

**Success Feedback:**
- Green checkmark animation
- Success message
- Haptic vibration (short, satisfying)
- Optional sound effect

**Error Feedback:**
- Red X or warning icon
- Clear error message in plain language
- Suggested action to resolve
- Haptic vibration (distinctive error pattern)

**Loading States:**
- Spinner or progress indicator
- Estimated time remaining for longer operations
- Cancellable when appropriate

---

## 7. Privacy & Security

### 7.1 Privacy-First Approach

**Core Principles:**
- **Zero Server Communication**: All data stays on device
- **No User Accounts**: No sign-up, login, or authentication required
- **No Analytics Tracking**: No third-party analytics or tracking SDKs
- **No Ads**: No advertising or monetization through user data
- **Local-Only Storage**: All data stored in device's local storage

### 7.2 Data Handling

**What We Store Locally:**
- NFC tag read history (optional, can be cleared)
- User-created templates
- App settings and preferences
- Bulk operation logs

**What We DO NOT Collect:**
- Personal identifying information
- Device identifiers
- Location data
- Contact lists or other sensitive data
- Usage analytics

**User Control:**
- Clear all history with one tap
- Delete individual records
- Export data for backup
- No data recovery if device is lost (by design for privacy)

### 7.3 Security Considerations

**NFC Security:**
- Validate tag data before display (prevent injection attacks)
- Warn users before writing sensitive information
- Support for tag password protection (when available)
- Option to lock tags after writing

**App Security:**
- Input sanitization for all user inputs
- Content Security Policy (CSP) for WebView
- No execution of untrusted code from NFC tags
- Secure random ID generation for local records

---

## 8. Performance Requirements

### 8.1 Performance Targets

| Operation | Target | Maximum |
|-----------|--------|---------|
| App Launch | < 1 second | 2 seconds |
| Mode Switch | < 200ms | 500ms |
| NFC Read | < 1 second | 3 seconds |
| NFC Write | < 1.5 seconds | 3 seconds |
| UI Interaction Response | < 100ms | 200ms |
| History Load | < 500ms | 1 second |
| Search/Filter | < 300ms | 500ms |

### 8.2 Resource Efficiency

- App size: < 10 MB
- Memory footprint: < 50 MB
- Battery impact: Minimal (NFC session management)
- Storage: Reasonable limits (max 1000 history records)

### 8.3 Offline Capability

- **100% Offline**: App fully functional without internet
- No network requests required for any feature
- All assets bundled with app
- Local storage only

---

## 9. Accessibility

### 9.1 Accessibility Standards

- WCAG 2.1 Level AA compliance
- Support for screen readers (VoiceOver on iOS, TalkBack on Android)
- High contrast mode support
- Adjustable text size (respect system settings)
- Reduced motion support (respect system settings)

### 9.2 Inclusive Design

- Clear, plain language (avoid jargon)
- Visual and non-visual feedback (don't rely on color alone)
- Keyboard navigation support (for devices with keyboards)
- Sufficient touch target sizes (44x44px minimum)
- Descriptive labels for all interactive elements

---

## 10. Supported Platforms

### 10.1 Mobile Platforms

**iOS:**
- Minimum version: iOS 13.0+
- NFC support: iPhone 7 and later (with iOS 13+)
- Optimization for iPhone SE to iPhone 15 Pro Max

**Android:**
- Minimum version: Android 5.0 (API Level 21)+
- NFC support: Devices with NFC hardware
- Optimization for various screen sizes (4" to 7")

### 10.2 NFC Tag Compatibility

**Supported Tag Types:**
- NTAG203, NTAG210, NTAG213, NTAG215, NTAG216
- MIFARE Classic 1K, 4K
- MIFARE Ultralight, Ultralight C
- MIFARE DESFire
- ISO 14443 Type A/B
- FeliCa (limited support)

**NDEF Format Support:**
- Text (RTD Text)
- URI (RTD URI)
- Smart Poster
- External Type
- MIME Type

---

## 11. Development Phases

### 11.1 Phase 1: MVP (Minimum Viable Product)
**Timeline: 8-12 weeks**

**Core Features:**
- Read Mode (basic)
- Write Mode (Text and URL only)
- Quick Copy Mode
- Basic UI/UX implementation
- Local storage for history and templates

**Deliverables:**
- Functional iOS and Android apps
- WebView interface
- React Native bridge implementation
- Basic user testing

### 11.2 Phase 2: Enhanced Features
**Timeline: 6-8 weeks**

**Additional Features:**
- Bulk Write Mode
- Extended Write Mode (Wi-Fi, vCard, Phone, Email)
- Template library
- Settings and customization
- Improved UI/UX polish

**Deliverables:**
- Feature-complete application
- User documentation
- App store assets

### 11.3 Phase 3: Polish & Optimization
**Timeline: 4-6 weeks**

**Focus Areas:**
- Performance optimization
- Accessibility improvements
- Bug fixes and stability
- User feedback incorporation
- Localization (if needed)

**Deliverables:**
- Production-ready app
- App store submission
- Marketing materials

### 11.4 Phase 4: Future Enhancements
**Timeline: Ongoing**

**Potential Features:**
- API integration (to be defined)
- Additional modes (Format, Analytics, Backup)
- Advanced tag features (encryption, signatures)
- Multi-language support
- Dark mode refinements
- Widget support (iOS 14+, Android)

---

## 12. Future API Integration

### 12.1 Current Architecture
- Fully offline, local-only operation
- No server communication
- Privacy-first design

### 12.2 Future API Considerations

**When API is introduced, it should:**
1. Be **optional** - All core features remain available offline
2. Be **privacy-preserving** - User consent required, minimal data transmission
3. Be **additive** - Enhance functionality without replacing local features

**Potential API Use Cases:**
- Cloud backup (encrypted, user-controlled)
- Template sharing (optional, community-driven)
- Advanced analytics (aggregated, anonymized)
- Enterprise features (team management, admin controls)
- Tag verification services (authenticity checking)

**API Integration Principles:**
- Explicit user opt-in required
- Clear data usage disclosure
- End-to-end encryption for transmitted data
- Ability to delete cloud data
- Graceful degradation when offline

---

## 13. Success Criteria

### 13.1 Launch Criteria

**Must Have:**
- [ ] All 4 primary modes functional
- [ ] Reliable NFC read/write operations
- [ ] Intuitive mobile UI
- [ ] Local storage working correctly
- [ ] No critical bugs
- [ ] Basic error handling
- [ ] iOS and Android builds ready

**Should Have:**
- [ ] Template library
- [ ] Read history
- [ ] Settings page
- [ ] Haptic feedback
- [ ] Accessibility features
- [ ] Help/tutorial screens

**Nice to Have:**
- [ ] Onboarding flow
- [ ] Advanced tag information
- [ ] Export/import functionality
- [ ] Multiple language support

### 13.2 Post-Launch Metrics

**User Engagement:**
- Daily Active Users (DAU)
- Weekly Active Users (WAU)
- Monthly Active Users (MAU)
- Session duration
- Feature usage distribution

**Quality Metrics:**
- App crash rate < 0.5%
- NFC operation success rate > 95%
- App store rating > 4.5 stars
- User retention rate (Day 1, Day 7, Day 30)

**Performance Metrics:**
- App launch time
- NFC operation latency
- UI responsiveness
- Battery consumption

---

## 14. Risks & Mitigations

### 14.1 Technical Risks

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| NFC hardware limitations | High | Medium | Extensive device testing, clear compatibility list |
| WebView performance issues | Medium | Low | Performance profiling, optimization, native fallback |
| iOS NFC restrictions | High | Medium | Follow Apple guidelines, Core NFC framework |
| Tag compatibility issues | Medium | Medium | Support common tag types, graceful error handling |
| Storage limitations | Low | Low | Implement storage quotas, user cleanup options |

### 14.2 UX Risks

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Confusing interface | High | Low | User testing, iterative design, clear labeling |
| NFC positioning difficulty | Medium | Medium | Clear visual guides, haptic feedback, tutorials |
| Feature discovery issues | Medium | Low | Onboarding, tooltips, help section |

### 14.3 Market Risks

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Low NFC adoption | High | Low | Focus on early adopters, education content |
| Competition | Medium | Medium | Differentiate with privacy focus and UX quality |
| Platform policy changes | Medium | Low | Stay updated with Apple/Google policies, flexible architecture |

---

## 15. Appendices

### 15.1 Glossary

- **NFC**: Near Field Communication - wireless technology for short-range data exchange
- **NDEF**: NFC Data Exchange Format - standard for NFC data structures
- **Tag**: Physical NFC chip that can store and transmit data
- **Read**: Process of retrieving data from an NFC tag
- **Write**: Process of storing data to an NFC tag
- **WebView**: Component that renders web content within a native app
- **React Native**: Framework for building native apps using JavaScript
- **Local Storage**: Browser API for storing data locally on device

### 15.2 References

- NFC Forum Specifications: https://nfc-forum.org/
- React Native Documentation: https://reactnative.dev/
- WCAG 2.1 Guidelines: https://www.w3.org/WAI/WCAG21/
- iOS Core NFC: https://developer.apple.com/documentation/corenfc
- Android NFC Guide: https://developer.android.com/guide/topics/connectivity/nfc

### 15.3 Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | December 2025 | OK GOLD Team | Initial PRD creation |

---

## 16. Contact & Feedback

For questions, feedback, or contributions to this PRD:

- **Product Team**: [To be defined]
- **Development Team**: [To be defined]
- **Design Team**: [To be defined]

---

**Document Status:** ✅ Final Draft - Ready for Review

**Next Steps:**
1. Review and approval from stakeholders
2. Technical feasibility assessment
3. Design mockup creation
4. Development sprint planning
5. Begin Phase 1 implementation
