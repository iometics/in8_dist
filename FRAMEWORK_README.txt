================================================================================
                          in8 FRAMEWORK
                    Cross-Platform Game Framework
                         Based on SDL3
================================================================================

Version: [version number]
Release Date: [date]
Platform Support: iOS, macOS, Android, Linux

Thank you for obtaining the in8 Framework!

================================================================================
WHAT IS in8?
================================================================================

in8 is a cross-platform game framework built on SDL3, designed to help you 
create games and interactive applications that run on multiple platforms with 
a single codebase.

FEATURES:
- Cross-platform support (iOS, macOS, iPadOS, Android, Linux)
- Built on SDL3 (Simple DirectMedia Layer)
- Single codebase for all platforms
- Easy integration into Xcode, Android Studio, and other IDEs
- Minimal wrapper code required
- Optimized for performance

================================================================================
PACKAGE CONTENTS
================================================================================

This package includes:

📁 Frameworks/
   ├── in8.xcframework              # iOS, macOS, iPadOS support
   └── [platform-specific libraries as applicable]

📄 in8_FRAMEWORK_LICENSE.txt        # Full license agreement
📄 LICENSE_SUMMARY.txt              # Quick license summary
📄 README.txt                       # This file
📄 CHANGELOG.txt                    # Version history
📁 docs/                            # Additional documentation (if included)

================================================================================
QUICK START
================================================================================

1. READ THE LICENSE
   - See in8_FRAMEWORK_LICENSE.txt for complete terms
   - See LICENSE_SUMMARY.txt for a quick overview

2. GET THE DOCUMENTATION
   Visit: [your documentation URL/repository]
   
   The documentation repository includes:
   - Xcode project setup guides (macOS & iOS)
   - Android Studio integration
   - C++, Objective-C, and Swift examples
   - Build configuration tips
   - Troubleshooting guides

3. CREATE YOUR FIRST PROJECT
   
   For iOS/macOS (Xcode):
   - Follow the Xcode Project Setup Guide
   - Add in8.xcframework to your project
   - Write a minimal main file
   - Build and run
   
   For Android (Android Studio):
   - Follow the Android integration guide
   - Add the appropriate library
   - Create a minimal Java/Kotlin wrapper
   - Build and run

4. START BUILDING
   - Your framework exports: int in8_main(int argc, char* argv[])
   - Call this from your platform wrapper
   - The framework handles window creation, rendering, input, etc.

================================================================================
PLATFORM-SPECIFIC NOTES
================================================================================

iOS / macOS / iPadOS (Xcode):
------------------------------
- Use in8.xcframework from the Frameworks folder
- Add to your target: General → Frameworks, Libraries, and Embedded Content
- Set to "Embed & Sign"
- Create a minimal AppDelegate that calls in8_main()
- See documentation for complete examples

Android (Android Studio):
-------------------------
- Use the appropriate .so library for your target architecture
- Create a minimal Java/Kotlin wrapper with JNI
- Call your native main function
- See documentation for complete examples

Linux:
------
- Link against the provided .so library
- Standard makefile or CMake build process
- See documentation for build examples

================================================================================
SYSTEM REQUIREMENTS
================================================================================

DEVELOPMENT:
- Xcode 14.0+ (for iOS/macOS development)
- Android Studio (for Android development)
- C++17 or later compiler
- SDL3 compatible development environment

RUNTIME:
- iOS 13.0+
- macOS 11.0+
- Android API Level 21+ (Android 5.0+)
- Linux (modern distributions)

================================================================================
IMPORTANT: REDISTRIBUTION RULES
================================================================================

⚠️  READ CAREFULLY ⚠️

YOU CAN:
✓ Build applications with in8
✓ Distribute applications that include in8
✓ Sell commercial applications built with in8

YOU CANNOT:
✗ Redistribute in8.xcframework or libraries separately
✗ Share the framework with other developers
✗ Include in8 in public repositories
✗ Bundle in8 in SDKs for others to use

When you distribute your application:
→ The framework should be embedded inside your app bundle
→ Users install your app normally (App Store, Google Play, etc.)
→ Users never see or access the framework separately

For complete legal terms, see in8_FRAMEWORK_LICENSE.txt

================================================================================
DOCUMENTATION & SUPPORT
================================================================================

ONLINE DOCUMENTATION:
[Your documentation URL]
- Complete guides for all platforms
- API reference
- Examples and tutorials
- Troubleshooting guides

GITHUB REPOSITORY (Documentation Only):
[Your GitHub URL]
- Project setup guides
- Code examples
- Community discussions
- Issue reporting

SUPPORT:
Email: [your support email]
Website: [your website]

COMMUNITY:
[Discord/Forum/etc. if applicable]

================================================================================
VERSION INFORMATION
================================================================================

Current Version: [version]
Release Date: [date]
SDL3 Version: [SDL version]

For changelog and version history, see CHANGELOG.txt

================================================================================
GETTING UPDATES
================================================================================

To get updates and new versions:
1. Check [your website] for announcements
2. Contact [your email] to request updates
3. [Other update methods]

Updates are provided at our discretion and may include:
- Bug fixes
- Performance improvements
- New features
- Platform support updates

================================================================================
LICENSING OPTIONS
================================================================================

STANDARD LICENSE (This Package):
- Free for personal and commercial use
- Build unlimited applications
- No royalties or revenue sharing
- Cannot redistribute the framework itself

SPECIAL LICENSING:
Contact us for:
- Team/Enterprise licenses (multiple developers)
- Educational institution licenses
- OEM/Bundling arrangements
- Source code access
- Custom licensing terms

Contact: [your licensing contact]

================================================================================
ATTRIBUTION (OPTIONAL)
================================================================================

While not required, we appreciate attribution in your applications:

Suggested credit text:
"Built with in8 Framework"
or
"Powered by in8"

You may link to: [your website]

================================================================================
LEGAL NOTICES
================================================================================

Copyright (c) 2026 [Your Name/Organization]
All Rights Reserved.

The in8 Framework is proprietary software. Use is governed by the terms of 
the in8 Framework License Agreement (see in8_FRAMEWORK_LICENSE.txt).

SDL3 is licensed under the zlib license.
See https://www.libsdl.org/license.php for SDL3 licensing.

Trademarks:
- "in8" is a trademark of [Your Name/Organization]
- SDL is a trademark of Sam Lantinga
- Other product names mentioned may be trademarks of their respective owners

================================================================================
TROUBLESHOOTING
================================================================================

Framework not found in Xcode:
→ Ensure Framework Search Paths includes the framework location
→ Verify the framework is set to "Embed & Sign"
→ Clean build folder (⌘⇧K) and rebuild

Linker errors:
→ Check that function names match exactly (in8_main)
→ Verify the framework slice matches your target architecture
→ Ensure you're using extern "C" for C++ files

App crashes on launch:
→ Check console logs for specific errors
→ Verify Info.plist is correctly configured
→ Ensure you're calling in8_main on the appropriate thread

For more help:
→ See documentation at [your docs URL]
→ Contact support at [your email]

================================================================================
THANK YOU FOR USING in8!
================================================================================

We're excited to see what you build with in8. If you create something cool, 
we'd love to hear about it!

Share your creations: [your social media/contact]

Good luck with your project!

- The in8 Team

================================================================================

Website: ioMetics.com
Email: support@ioMetics.com

Last Updated: [date]

================================================================================
