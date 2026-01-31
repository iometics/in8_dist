# in8 Framework - Quick Reference & FAQ

## 🚀 Quick Start Checklist

- [ ] Read the [LICENSE](LICENSE) file
- [ ] Obtain the in8.xcframework from [contact information]
- [ ] Follow the [Xcode Project Setup Guide](xcode_project_setup_guide.md)
- [ ] Review the [C++ Main Files](cpp_main_files.md) for code examples
- [ ] Build and test your project
- [ ] **DO NOT** commit in8.xcframework to public repositories

## 📋 Licensing Quick Reference

### What You CAN Do ✅

| Action | Allowed? | Notes |
|--------|----------|-------|
| Build apps with in8 | ✅ Yes | Commercial or non-commercial |
| Distribute your apps | ✅ Yes | App Store, Steam, direct download, etc. |
| Bundle in8 in your app | ✅ Yes | Must be embedded in your app bundle |
| Use multiple copies | ✅ Yes | Each of your apps can include in8 |
| Modify example code | ✅ Yes | Documentation examples are MIT licensed |
| Share documentation | ✅ Yes | This documentation is freely shareable |

### What You CANNOT Do ❌

| Action | Allowed? | Why Not? |
|--------|----------|----------|
| Redistribute in8 framework | ❌ No | Proprietary license |
| Put in8 in public GitHub | ❌ No | Violates redistribution terms |
| Include in8 in your SDK | ❌ No | Would allow others to use without permission |
| Share in8 with other devs | ❌ No | They must obtain it directly |
| Extract in8 as library | ❌ No | Must stay bundled in apps |
| Post in8 on CDN/npm/etc. | ❌ No | Unauthorized distribution |

## 🤔 Frequently Asked Questions

### Q: Can I sell applications I build with in8?
**A:** Yes! You can build and sell commercial applications using in8. The framework can be bundled within your distributed apps.

### Q: Can I put my project on GitHub?
**A:** Yes, but **do not include the in8.xcframework** in your repository. Use the provided `.gitignore` file to prevent accidental commits. Document in your README how to obtain the framework.

### Q: How do my users get in8 if it's not in my repo?
**A:** Your users don't need the framework separately. When you build and distribute your app, the framework is embedded within it. Your users just install your app normally.

### Q: Can I share in8 with my team members?
**A:** Each developer on your team should obtain the framework through official channels. Contact [your contact information] for team/commercial licensing options.

### Q: What if I'm building an open-source project?
**A:** You can open-source your application code, but the in8.xcframework itself cannot be included. Provide instructions in your README on how to obtain the framework to build the project.

### Q: Can I use in8 in a game engine or framework I'm building?
**A:** No. The framework cannot be redistributed as part of other SDKs, engines, or frameworks. It's for building end-user applications only.

### Q: What about app updates?
**A:** You can include updated versions of in8 in your app updates. Each version of your app can bundle the framework.

### Q: Can I use in8 in multiple projects?
**A:** Yes! You can use in8 in as many of your own projects as you want. Each project can include the framework when distributed.

### Q: What if I violate the license accidentally?
**A:** If you've unintentionally violated the terms (e.g., committed the framework to GitHub), remove it immediately and contact [your contact information] to discuss the situation.

### Q: Do I need to credit in8 in my app?
**A:** Check the full license terms, but generally you should include appropriate attribution. A simple "Built with in8 framework" in your credits is appreciated.

## 📁 Repository Structure Best Practices

### ✅ Recommended Structure
```
your-game/
├── README.md                    # Your project documentation
├── .gitignore                   # Include framework exclusions
├── src/                         # Your game code
├── assets/                      # Your game assets
├── docs/                        # Your documentation
│   └── BUILD.md                 # Build instructions
└── xcode/                       # Xcode project files
    └── YourGame.xcodeproj
    
# Framework is obtained separately and placed here:
# xcode/Frameworks/in8.xcframework  (gitignored)
```

### ❌ Avoid This Structure
```
your-game/
├── lib/
│   └── in8.xcframework/         # ❌ Don't commit this!
└── ...
```

## 🔒 Security & Privacy

### Protecting Your Framework Copy

1. **Keep it out of version control**
   - Use the provided `.gitignore`
   - Don't commit to git, svn, or other VCS

2. **Store it securely**
   - Keep your framework copy in a secure location
   - Don't share via public file services

3. **Update responsibly**
   - Download updates only from official sources
   - Verify checksums if provided

## 📞 Getting Help

### For Framework Access
- **Contact:** [your email/website]
- **Subject Line:** "in8 Framework Access Request"
- **Include:** Your name, organization, intended use

### For Documentation Issues
- **GitHub Issues:** [your repo URL]/issues
- **Pull Requests:** Documentation improvements welcome

### For Technical Support
- **Framework bugs:** Contact [your support channel]
- **Documentation errors:** Open a GitHub issue
- **Integration help:** See the guides or contact support

## 🎯 Common Scenarios

### Scenario 1: Solo Indie Developer
```
1. Contact [contact] to get in8.xcframework
2. Create Xcode project following the guide
3. Add framework to project (not to git)
4. Build and test your game
5. Distribute your game (framework included in bundle)
6. Open source your game code (without framework)
```

### Scenario 2: Small Team
```
1. One person obtains framework
2. Share via secure internal method (not public repo)
3. Each dev places framework in their local project
4. Use .gitignore to prevent commits
5. Build and distribute apps normally
6. For larger teams, contact about licensing options
```

### Scenario 3: Educational Use
```
1. Obtain framework for educational purposes
2. Teach using the documentation (freely shareable)
3. Students build projects with framework
4. Students can showcase projects (with framework bundled)
5. Do not redistribute framework itself
```

## 📊 Quick Comparison: Similar Licenses

| Aspect | in8 | Unity | Unreal | SDL3 |
|--------|-----|-------|--------|------|
| Use in apps | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| Redistribute engine | ❌ No | ❌ No | ❌ No | ✅ Yes* |
| Commercial use | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| Source access | ❌ No | ⚠️ Some | ✅ Yes | ✅ Yes |

*SDL3 is zlib licensed, different from in8's proprietary license

## 🎓 Best Practices Summary

1. **Never** commit the framework to public repos
2. **Always** use the provided .gitignore
3. **Do** bundle the framework in your distributed apps
4. **Don't** redistribute the framework separately
5. **Do** share this documentation freely
6. **Don't** share the framework binaries
7. **Do** contact for commercial licensing if needed
8. **Do** read the full LICENSE file

---

**Remember:** When in doubt, ask! Contact [your contact information]

Last Updated: [Date]
