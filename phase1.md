# CulinAiry iOS - Phase 1 Implementation Guide 📱

Panduan lengkap untuk mengimplementasikan Phase 1 secara manual di Xcode.

## 🚀 Getting Started

### Step 1: Create New Xcode Project
1. **Buka Xcode** → Create a new Xcode project
2. **Platform**: iOS
3. **Template**: App
4. **Project Details**:
   - Product Name: `CulinAiry`
   - Interface: SwiftUI
   - Language: Swift
   - Bundle Identifier: `com.culinairy.ios`
   - Team: (Your development team)
   - Use Core Data: ❌ (kita akan pakai SwiftData)
   - Include Tests: ✅

5. **Save Location**: `/Users/dmzmzmd/CulinAiry-ios/`

---

## 📁 Step 2: Organize Project Structure

### Create Folder Groups in Xcode Navigator:
```
CulinAiry/
├── App/
├── Features/
├── Shared/
│   ├── Models/
│   ├── Services/
│   ├── Utilities/
│   └── Extensions/
└── Resources/
```

**Cara membuat groups:**
1. Right-click project name → New Group
2. Buat struktur folder sesuai diagram di atas
3. Drag files ke group yang sesuai

---

## 🎨 Step 3: Configure App Settings

### Update Info.plist
Tambahkan permissions berikut ke `Info.plist`:

```xml
<!-- Background Modes -->
<key>UIBackgroundModes</key>
<array>
    <string>background-app-refresh</string>
    <string>background-processing</string>
    <string>remote-notification</string>
</array>

<!-- Background Task Identifiers -->
<key>BGTaskSchedulerPermittedIdentifiers</key>
<array>
    <string>com.culinairy.sync</string>
    <string>com.culinairy.process</string>
    <string>com.culinairy.nutrition-sync</string>
    <string>com.culinairy.worker-coordination</string>
</array>

<!-- Permissions -->
<key>NSCameraUsageDescription</key>
<string>CulinAiry uses the camera to recognize food ingredients and track your nutrition through photo analysis.</string>

<key>NSPhotoLibraryUsageDescription</key>
<string>CulinAiry needs access to your photo library to save and analyze food photos for nutrition tracking.</string>

<key>NSHealthShareUsageDescription</key>
<string>CulinAiry integrates with HealthKit to provide comprehensive nutrition tracking and health insights.</string>

<key>NSHealthUpdateUsageDescription</key>
<string>CulinAiry logs nutrition data to HealthKit to help you track your dietary goals and health progress.</string>

<key>NSSiriUsageDescription</key>
<string>CulinAiry works with Siri to generate recipes and manage your cooking through voice commands.</string>

<key>NSUserNotificationsUsageDescription</key>
<string>CulinAiry sends notifications for cooking timers, meal reminders, and recipe generation updates.</string>

<key>ITSAppUsesNonExemptEncryption</key>
<false/>
```

### Update Project Settings
1. **Project Navigator** → Select project name
2. **TARGETS** → CulinAiry
3. **General Tab**:
   - Display Name: `CulinAiry`
   - Bundle Identifier: `com.culinairy.ios`
   - Version: `1.0`
   - Build: `1`
   - Deployment Target: `iOS 17.0`

4. **Signing & Capabilities**:
   - Add Capability: Background Modes
     - ✅ Background app refresh
     - ✅ Background processing
     - ✅ Background fetch
   - Add Capability: Push Notifications
   - Add Capability: HealthKit
   - Add Capability: Siri

---

## 🎨 Step 4: Create Color Assets

### Add Custom Colors to Assets.xcassets
1. **Assets.xcassets** → Right-click → New Color Set
2. Buat 4 color sets berikut:

#### PrimaryGreen
- **Name**: `PrimaryGreen`
- **RGB**: R: 51, G: 179, B: 102 (atau #33B366)

#### SecondaryOrange
- **Name**: `SecondaryOrange`
- **RGB**: R: 255, G: 153, B: 51 (atau #FF9933)

#### BackgroundCream
- **Name**: `BackgroundCream`
- **RGB**: R: 250, G: 245, B: 240 (atau #FAF5F0)

#### TextCharcoal
- **Name**: `TextCharcoal`
- **RGB**: R: 51, G: 51, B: 51 (atau #333333)

---

## 💻 Step 5: Implement Core Files

### 5.1 Update ContentView.swift
Ganti isi `ContentView.swift` dengan:

```swift
import SwiftUI

struct ContentView: View {
    @EnvironmentObject private var appStateManager: AppStateManager
    @State private var selectedTab: Tab = .recipes

    enum Tab: String, CaseIterable {
        case recipes = "Recipes"
        case aiChef = "AI Chef"
        case nutrition = "Nutrition"
        case profile = "Profile"

        var icon: String {
            switch self {
            case .recipes: return "book.fill"
            case .aiChef: return "wand.and.stars"
            case .nutrition: return "heart.fill"
            case .profile: return "person.fill"
            }
        }
    }

    var body: some View {
        Group {
            if appStateManager.hasCompletedOnboarding {
                mainTabView
            } else {
                OnboardingView()
            }
        }
    }

    private var mainTabView: some View {
        TabView(selection: $selectedTab) {
            RecipesView()
                .tabItem { Label(Tab.recipes.rawValue, systemImage: Tab.recipes.icon) }
                .tag(Tab.recipes)

            AIChefView()
                .tabItem { Label(Tab.aiChef.rawValue, systemImage: Tab.aiChef.icon) }
                .tag(Tab.aiChef)

            NutritionView()
                .tabItem { Label(Tab.nutrition.rawValue, systemImage: Tab.nutrition.icon) }
                .tag(Tab.nutrition)

            ProfileView()
                .tabItem { Label(Tab.profile.rawValue, systemImage: Tab.profile.icon) }
                .tag(Tab.profile)
        }
        .accentColor(.culinAiryPrimary)
    }
}

// MARK: - Onboarding View
struct OnboardingView: View {
    @EnvironmentObject private var appStateManager: AppStateManager

    var body: some View {
        VStack(spacing: 32) {
            Spacer()

            VStack(spacing: 16) {
                Image(systemName: "wand.and.stars")
                    .font(.system(size: 80))
                    .foregroundColor(.culinAirySecondary)

                Text("Welcome to CulinAiry")
                    .font(.largeTitle)
                    .fontWeight(.bold)
                    .multilineTextAlignment(.center)

                Text("Your AI-powered cooking companion")
                    .font(.title2)
                    .foregroundColor(.secondary)
                    .multilineTextAlignment(.center)
            }

            VStack(spacing: 24) {
                FeatureCard(
                    icon: "brain.head.profile",
                    title: "AI Recipe Generation",
                    description: "Create personalized recipes from your ingredients"
                )

                FeatureCard(
                    icon: "heart.text.square",
                    title: "Nutrition Tracking",
                    description: "Track your health goals with HealthKit integration"
                )

                FeatureCard(
                    icon: "camera.fill",
                    title: "Smart Food Recognition",
                    description: "Scan ingredients and analyze nutrition automatically"
                )
            }

            Spacer()

            Button(action: {
                appStateManager.completeOnboarding()
            }) {
                Text("Get Started")
                    .font(.headline)
                    .foregroundColor(.white)
                    .frame(maxWidth: .infinity)
                    .padding()
                    .background(Color.culinAiryPrimary)
                    .cornerRadius(12)
            }
            .padding(.horizontal)
        }
        .padding()
    }
}

// MARK: - Feature Card
struct FeatureCard: View {
    let icon: String
    let title: String
    let description: String

    var body: some View {
        HStack(spacing: 16) {
            Image(systemName: icon)
                .font(.title2)
                .foregroundColor(.culinAirySecondary)
                .frame(width: 40)

            VStack(alignment: .leading, spacing: 4) {
                Text(title)
                    .font(.headline)
                    .fontWeight(.semibold)

                Text(description)
                    .font(.subheadline)
                    .foregroundColor(.secondary)
                    .multilineTextAlignment(.leading)
            }

            Spacer()
        }
        .padding()
        .background(Color(.systemGray6))
        .cornerRadius(12)
    }
}

// MARK: - Placeholder Views
struct RecipesView: View {
    var body: some View {
        NavigationStack {
            Text("Recipes View")
                .navigationTitle("Recipes")
        }
    }
}

struct AIChefView: View {
    var body: some View {
        NavigationStack {
            Text("AI Chef View")
                .navigationTitle("AI Chef")
        }
    }
}

struct NutritionView: View {
    var body: some View {
        NavigationStack {
            Text("Nutrition View")
                .navigationTitle("Nutrition")
        }
    }
}

struct ProfileView: View {
    var body: some View {
        NavigationStack {
            Text("Profile View")
                .navigationTitle("Profile")
        }
    }
}

#Preview {
    ContentView()
        .environmentObject(AppStateManager())
        .environmentObject(BackgroundTaskCoordinator())
        .environmentObject(WebPlatformSyncManager())
}
```

### 5.2 Update Main App File
Ganti nama file `CulinAiryApp.swift` dan isi dengan:

```swift
import SwiftUI
import SwiftData
import BackgroundTasks

@main
struct CulinAiryApp: App {

    @StateObject private var appStateManager = AppStateManager()
    @StateObject private var backgroundTaskCoordinator = BackgroundTaskCoordinator()
    @StateObject private var webPlatformSyncManager = WebPlatformSyncManager()

    var body: some Scene {
        WindowGroup {
            ContentView()
                .environmentObject(appStateManager)
                .environmentObject(backgroundTaskCoordinator)
                .environmentObject(webPlatformSyncManager)
                .onAppear {
                    setupApp()
                }
                .onReceive(NotificationCenter.default.publisher(for: UIApplication.didFinishLaunchingNotification)) { _ in
                    registerBackgroundTasks()
                }
                .onReceive(NotificationCenter.default.publisher(for: UIApplication.didEnterBackgroundNotification)) { _ in
                    scheduleBackgroundTasks()
                }
        }
        .modelContainer(DataController.shared.container)
    }

    private func setupApp() {
        configureAppearance()
        requestPermissions()
    }

    private func configureAppearance() {
        let appearance = UINavigationBarAppearance()
        appearance.configureWithOpaqueBackground()
        appearance.backgroundColor = UIColor.systemBackground
        UINavigationBar.appearance().standardAppearance = appearance
        UINavigationBar.appearance().scrollEdgeAppearance = appearance
    }

    private func requestPermissions() {
        Task {
            await requestNotificationPermissions()
            await requestHealthKitPermissions()
        }
    }

    private func requestNotificationPermissions() async {
        let center = UNUserNotificationCenter.current()
        try? await center.requestAuthorization(options: [.alert, .badge, .sound])
    }

    private func requestHealthKitPermissions() async {
        // HealthKit permissions will be requested when first needed
    }

    private func registerBackgroundTasks() {
        backgroundTaskCoordinator.registerBackgroundTasks()
    }

    private func scheduleBackgroundTasks() {
        backgroundTaskCoordinator.scheduleBackgroundSync()
        backgroundTaskCoordinator.scheduleBackgroundProcessing()
    }
}

// MARK: - App State Manager
@MainActor
class AppStateManager: ObservableObject {
    @Published var isFirstLaunch: Bool = true
    @Published var hasCompletedOnboarding: Bool = false
    @Published var currentUser: User?
    @Published var isAuthenticated: Bool = false

    init() {
        loadAppState()
    }

    private func loadAppState() {
        isFirstLaunch = UserDefaults.standard.bool(forKey: "hasLaunchedBefore") == false
        hasCompletedOnboarding = UserDefaults.standard.bool(forKey: "hasCompletedOnboarding")

        if isFirstLaunch {
            UserDefaults.standard.set(true, forKey: "hasLaunchedBefore")
        }
    }

    func completeOnboarding() {
        hasCompletedOnboarding = true
        UserDefaults.standard.set(true, forKey: "hasCompletedOnboarding")
    }

    func setUser(_ user: User) {
        currentUser = user
        isAuthenticated = true
    }

    func logout() {
        currentUser = nil
        isAuthenticated = false
    }
}
```

---

## 📁 Step 6: Add Required Swift Files

### 6.1 Create Extensions/Color+Extensions.swift

```swift
import SwiftUI

extension Color {
    static let culinAiryPrimary = Color("PrimaryGreen")
    static let culinAirySecondary = Color("SecondaryOrange")
    static let culinAiryBackground = Color("BackgroundCream")
    static let culinAiryText = Color("TextCharcoal")

    static var culinAiryGradient: LinearGradient {
        LinearGradient(
            colors: [.culinAiryPrimary, .culinAirySecondary],
            startPoint: .topLeading,
            endPoint: .bottomTrailing
        )
    }
}

// Color palette fallbacks for when custom colors are not available
extension Color {
    static var primaryGreen: Color {
        Color(red: 0.2, green: 0.7, blue: 0.4)
    }

    static var secondaryOrange: Color {
        Color(red: 1.0, green: 0.6, blue: 0.2)
    }

    static var backgroundCream: Color {
        Color(red: 0.98, green: 0.96, blue: 0.94)
    }

    static var textCharcoal: Color {
        Color(red: 0.2, green: 0.2, blue: 0.2)
    }
}
```

### 6.2 Create Placeholder Classes
Buat file-file berikut sebagai placeholder yang akan diimplementasi nanti:

#### Services/BackgroundTaskCoordinator.swift
```swift
import Foundation
import BackgroundTasks

@MainActor
class BackgroundTaskCoordinator: ObservableObject {

    func registerBackgroundTasks() {
        print("🔄 Background tasks registered")
    }

    func scheduleBackgroundSync() {
        print("📅 Background sync scheduled")
    }

    func scheduleBackgroundProcessing() {
        print("⚙️ Background processing scheduled")
    }
}
```

#### Services/WebPlatformSyncManager.swift
```swift
import Foundation

@MainActor
class WebPlatformSyncManager: ObservableObject {

    init() {
        print("🌐 Web Platform Sync Manager initialized")
    }
}
```

#### Services/DataController.swift
```swift
import Foundation
import SwiftData

@MainActor
class DataController: ObservableObject {

    static let shared = DataController()

    let container: ModelContainer

    private init() {
        // Temporary simple container - akan diupdate nanti
        do {
            container = try ModelContainer(for: User.self)
        } catch {
            fatalError("Failed to create ModelContainer: \(error)")
        }
    }
}
```

#### Models/User.swift
```swift
import Foundation
import SwiftData

@Model
class User {
    var id: String
    var email: String
    var displayName: String

    init(id: String, email: String, displayName: String) {
        self.id = id
        self.email = email
        self.displayName = displayName
    }
}
```

---

## 🧪 Step 7: Test Build

1. **Build Project**: `Cmd + B`
2. **Run Simulator**: `Cmd + R`
3. **Verify**:
   - App launches successfully
   - Onboarding screen appears
   - Can tap "Get Started" button
   - Tab navigation works

---

## ✅ Phase 1 Completion Checklist

- [ ] ✅ Xcode project created
- [ ] ✅ Project structure organized
- [ ] ✅ Info.plist configured
- [ ] ✅ Custom colors added
- [ ] ✅ Basic UI implemented
- [ ] ✅ Placeholder services created
- [ ] ✅ App builds successfully
- [ ] ✅ Basic navigation works

---

## 🎯 Next Steps (Phase 2)

Setelah Phase 1 selesai, lanjut ke:
1. **UI/UX Implementation** - Design system lengkap
2. **Navigation Architecture** - Advanced routing
3. **Component Library** - Reusable SwiftUI components

**File ini akan menjadi foundation untuk implementasi feature-feature lanjutan di phase berikutnya!** 🚀

---

> 💡 **Tips**: Simpan file ini sebagai referensi dan update setiap kali ada perubahan pada struktur project.