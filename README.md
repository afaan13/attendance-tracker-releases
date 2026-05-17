# 📱 Attendence — The Elite School Management Ecosystem 🚀

<div align="center">
  <p>
    <img src="https://img.shields.io/badge/Kotlin-0095D5?style=for-the-badge&logo=kotlin&logoColor=white" alt="Kotlin" />
    <img src="https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Android" />
    <img src="https://img.shields.io/badge/Jetpack_Compose-4285F4?style=for-the-badge&logo=android&logoColor=white" alt="Jetpack Compose" />
    <img src="https://img.shields.io/badge/SQLite_Room-3DDC84?style=for-the-badge&logo=sqlite&logoColor=white" alt="Room SQLite" />
    <img src="https://img.shields.io/badge/Firebase_Firestore-FFCA28?style=for-the-badge&logo=firebase&logoColor=black" alt="Firebase" />
  </p>
  <p>
    <img src="https://img.shields.io/badge/Architecture-MVVM_Clean_Code-orange?style=flat-square&logo=clean-code" alt="MVVM Architecture" />
    <img src="https://img.shields.io/badge/Database-Offline_First-blue?style=flat-square&logo=sqlite" alt="Offline-First" />
    <img src="https://img.shields.io/badge/Automation-WhatsApp_Accessibility-green?style=flat-square&logo=whatsapp" alt="WhatsApp Automation" />
  </p>
</div>

---

## 📖 Introduction: What is Attendence & How It Works 🏫✨

### 💡 In Simple Words
**Attendence** is a high-performance Android application built to bridge the gap between school administration, teachers, and parents. It completely digitizes the process of taking attendance, scheduling holidays, managing school rosters, and distributing reports. 

Instead of manual registers, sheets, or tedious copy-pasting, **Attendence** works as an automated ecosystem:
1. **`[👑 Admin]` The Principal Sets Up the School:** The Principal registers the school in the app, generating a secure **Invite Code**.
2. **`[🧑‍🏫 Staff]` Teachers Join the Network:** Teachers register using this Invite Code. Once the Principal approves them, they gain instant access to class rosters based on administrative policies.
3. **`[⚡ Fast]` Attendance is Marked in Seconds:** Teachers open their customized dashboard, select a class, and mark attendance (Present, Absent, Late, or on Leave) with one-tap efficiency.
4. **`[💾 Offline]` Data Syncs Silently:** The app is **offline-first**. It works perfectly inside classrooms with poor cell reception. As soon as the device connects to the internet, it silently syncs the data to the cloud.
5. **`[🤖 Robot]` Parents Get Instant Automated Updates:** The app generates gorgeous, professional PDF reports on-device and dispatches them directly to parents' WhatsApp or WhatsApp Business numbers automatically, removing all manual effort from the teacher's day.

---

## 💎 Features & Capabilities (Start-to-End Walkthrough) 🌟🛠️

### 🎭 Unified Role-Based Portals
* **`[⚡ Instant]` Welcome Gate:** An elegant, single-step onboarding gateway featuring high-fidelity animations that transition users instantly into the application, completely removing long multi-step tutorials.
* **`[👑 Admin]` Principal Dashboard:** The administrative hub allowing management of teacher access, school subscription tiers, holiday schedules, database status, and school-wide analytics.
* **`[🧑‍🏫 Staff]` Teacher Dashboard:** A high-speed, uncluttered environment designed strictly for class coordination, student roster lookup, quick attendance marking, and automated report dispatching.

### 👥 Robust Class & Student Registry
* **`[🏫 Streamlined]` Dynamic Class Allocation:** Create classrooms, assign division streams, and populate them with detailed student profiles (including Roll Number, Name, Parent Name, and Phone Number).
* **`[🎓 Leadership]` Class Representative (CR) System:** Designate specific students as Class Representatives to assist teachers in organizing daily class operations.
* **`[👁️ Privacy]` Granular Class Visibility:** Principals can set class rosters as viewable by *"All Teachers"*, *"None"*, or manually allocate classes to *"Selected Teachers"* to secure student privacy.

### 🔒 Smart Attendance Gating & Locks
* **`[⏱️ Rapid]` Interactive Day View:** Rapid single-tap toggling to mark students as **Present**, **Absent**, **Late**, or **Leave**.
* **`[🔒 Immutable]` Global Attendance Edit Lock:** Principals can toggle an administrative lock on historical attendance logs, preventing teachers from editing past records.
* **`[📅 Intelligent]` Smart Holiday Management:** 
  * Principals can schedule school-wide holidays on the central calendar.
  * Teachers are instantly shown a prominent warning banner on holiday dates.
  * Interactive attendance marking is automatically disabled during holidays to enforce data integrity.

### 🔄 Advanced Cloud-Caching & Synchronization
* **`[💾 Offline-First]` SQLite (Room DB) Caching:** Local SQLite storage guarantees flawless operations even in completely offline environments.
* **`[📡 Demand-Sync]` Adaptive Data Dispatch:** Replaced heavy, continuous listeners with smart, manual, and delta-based sync actions to conserve battery, reduce data consumption, and minimize Firebase Firestore read/write quota usage.
* **`[⚔️ Safe-Merge]` Conflict Resolution Engine:** Robust transaction management prevents offline changes from overriding administrative locks or newer server-side edits.

### 📄 Automated PDF Report Generation & Batch Dispatch
* **`[📄 Vector-PDF]` High-Resolution Report Compilation:** Generate weekly, monthly, or customized range-based attendance reports directly on the device as beautifully styled PDFs.
* **`[🤖 Auto-Click]` Intelligent WhatsApp Dispatcher:** Load queues of parent phone numbers and automatically deliver the corresponding PDF files via WhatsApp or WhatsApp Business.

### 💎 Tiered Subscription Ecosystem (Elite Plans)
* **`[🆓 Free]` Core Attendance Utilities:** Core features, basic class sizes, and manual backup utilities.
* **`[💎 Premium]` Scale-Up Package:** Dynamic allocation of up to 30 classes and 200 students per class, and custom teacher restriction overrides.
* **`[👑 Elite]` Advanced Calendars & Restrictions:** 2x capacity of Premium, advanced administrative rules, and school-wide holiday management.
* **`[🌌 Ultimate]` Absolute Limits & Priority Sync:** Complete school scaling with unlimited rosters, priority Firestore syncing, and granular teacher policy enforcement.

---

## 🛡️ Professional Permissions Architecture & Rationale 🔒🧩

From an enterprise Android engineering perspective, maintaining device stability, user privacy, and strict permission compliance is paramount. Below is the technical breakdown of the permissions requested by the **Attendence** app, their implementation architecture, and why they are vital to the ecosystem.

### 1. `android.permission.INTERNET` 🌐
* **Purpose:** Network Socket Creation and API Access.
* **Developer POV Rationale:** 
  To achieve seamless cloud synchronization, the application establishes secure outbound TLS connections to the Firebase Authentication servers (for user sign-in and session retention) and Google Cloud Firestore (for database read/write actions, subscription verification, and holiday updates).
* **Security Implementation:** All web traffic is strictly gated over HTTPS and TLS 1.3, enforced by the app's `networkSecurityConfig` declarations in the manifest.

### 2. `android.permission.ACCESS_NETWORK_STATE` 📶
* **Purpose:** Network Connectivity Monitoring.
* **Developer POV Rationale:** 
  To implement a reliable offline-first database pattern, the app uses a dynamic `NetworkMonitor` observer. By checking the device's transport capabilities (Wi-Fi, Cellular, Ethernet) before launching network requests, the app:
  * Intelligently buffers cloud writes inside the local Room SQLite DB when offline.
  * Avoids wasting CPU and radio power attempting failed connections over high-latency or dead networks, heavily optimizing battery consumption.
  * Automates the background syncing routine immediately upon transition to an active network state.

### 3. `android.permission.BIND_ACCESSIBILITY_SERVICE` 🤖 (The "Attendance Auto-Sender" Service)
* **Purpose:** Automation of Batch PDF Delivery on WhatsApp & WhatsApp Business.
* **Developer POV Rationale & Mechanics:**
  Sending daily or monthly attendance reports to 200+ parents manually is an operational bottleneck for teachers. To solve this, the application registers an Android Accessibility Service (`WhatsAppAutomatorService`).
  
  * **How it Operates:** 
    When the teacher triggers a batch send, the app programmatically parses parent phone numbers and executes implicit `ACTION_SEND` intents containing the student’s custom PDF file URI. The intent targets WhatsApp (`com.whatsapp`) or WhatsApp Business (`com.whatsapp.w4b`).
  * **Event Sniffing & Automation:** 
    The `WhatsAppAutomatorService` listens exclusively to `TYPE_WINDOW_STATE_CHANGED` and `TYPE_WINDOW_CONTENT_CHANGED` accessibility events emanating *only* from the WhatsApp packages.
  * **Node Inspection & Programmatic Clicks:** 
    The service scans the active window's visual tree (`rootInActiveWindow`) to resolve the "Send" button. It utilizes a failsafe hierarchy:
    1. Looks up the button's layout resource IDs directly using `flagReportViewIds` (targeting specific IDs across current WhatsApp updates such as `com.whatsapp:id/send` or `com.whatsapp.w4b:id/send`).
    2. If WhatsApp layout updates obfuscate or modify the ID, the engine performs a recursive node-tree traversal matching nodes by content descriptions or texts containing the localized keyword `"Send"`.
    3. Once resolved, it triggers an `ACTION_CLICK` action on the node, simulating a tap on the user's behalf.
    4. Instantly after dispatch, it issues a `GLOBAL_ACTION_BACK` command to return to the app's queue, proceeding to the next student immediately.

#### 🔒 Security, Trust, and Privacy Safeguards (Accessibility API)
Because the Accessibility API is highly sensitive, the `WhatsAppAutomatorService` has been engineered with strict privacy safeguards:
* **Zero Telemetry / Data Logging:** The service is entirely local. It does **not** write to storage, log chat content, or transmit any analytical data to external servers.
* **Read-Only / Action-Specific:** It never reads user contact lists, message histories, status updates, or incoming chat packets. It is programmed to do exactly **one** thing: locate the Send button of the active package and tap it.
* **Targeted Filtering:** It is tightly scoped via `accessibility_service_config.xml` to ignore all system events other than those originating from `com.whatsapp` and `com.whatsapp.w4b`.
* **Android 13+ Restrictive Sandbox Compliance:** On modern Android versions (Android 13, 14+), the OS implements a "Restricted Settings" sandbox for side-loaded apps utilizing accessibility services. The app includes built-in guidance, directing the administrator/teacher to open App Info, click the top-right options menu, and select **"Allow Restricted Settings"** to authorize the accessibility daemon securely.

---

## 🛠️ Technology Stack & Architecture 📐🧱

* **UI Engine:** Jetpack Compose (Modern declarative UI with a custom HSL palette, dark mode toggles, and animated glassmorphic surfaces).
* **State Management:** MVVM Architecture with Clean Architecture principles (Repositories, Use Cases, ViewModels, and unidirectional State/Event Flows).
* **Database & Persistence:** Room Persistence Library (SQLite local cache) & Firebase Firestore Cloud DB.
* **Asynchronous Concurrency:** Kotlin Coroutines & Flow (for reactive, resource-efficient UI updates).
* **Report Engine:** Android PDF Graphics Canvas.
* **Language:** Kotlin 1.9+ with full Proguard configuration.

---
*Developed with ❤️ to empower modern educators and administrations by Afaan.*
