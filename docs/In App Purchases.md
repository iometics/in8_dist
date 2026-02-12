
# In-App Purchase (IAP) API User Guide

## Overview

This document provides a comprehensive guide for using the In-App Purchase (IAP) API in your applications. The API offers a platform-agnostic interface for implementing in-app purchases across different platforms.

## Core Methods

The IAP API consists of four primary methods for handling product operations and three callback setters for managing asynchronous events.

### Product Management Methods

#### `loadProducts(productIds)`

Retrieves product information from the platform's store.

**Parameters:**
- `productIds`: A list of product identifier strings that correspond to products configured in your store dashboard.

**Behavior:**
- Initiates an asynchronous request to the platform's store to retrieve information about the specified products.
- Results are delivered through the `productsLoadedCallback`.
- This method should be called during application initialization or before displaying a store UI.

**Example Usage:**
```
// Request product information for three items
loadProducts(["com.myapp.removeads", "com.myapp.extralife", "com.myapp.fullversion"]);
```

#### `purchaseProduct(productId)`

Initiates the purchase flow for a specific product.

**Parameters:**
- `productId`: A string identifier for the product to purchase.

**Behavior:**
- Begins the platform's native purchase flow for the specified product.
- The user may be prompted to authenticate or confirm the purchase.
- Purchase results are delivered through the `purchaseCompletedCallback`.
- This method should be called in response to user interaction, such as tapping a "Buy" button.

**Example Usage:**
```
// When user taps the "Remove Ads" purchase button
purchaseProduct("com.myapp.removeads");
```

#### `restorePurchases()`

Restores previously purchased non-consumable and subscription products.

**Parameters:**
- None

**Behavior:**
- Queries the platform's store for all previously purchased products associated with the current user account.
- The user may be prompted to authenticate with their store account.
- Restored purchases are delivered through the `restoreCompletedCallback`.
- For each restored product, your application should unlock the associated functionality.
- This method should be called when the user taps a "Restore Purchases" button.

**Example Usage:**
```
// When user taps the "Restore Purchases" button
restorePurchases();
```

#### `isProductPurchased(productId)`

Checks if a specific product has been purchased.

**Parameters:**
- `productId`: A string identifier for the product to check.

**Return Value:**
- `true` if the product has been purchased and the purchase is still valid.
- `false` if the product has not been purchased or the purchase is no longer valid.

**Behavior:**
- Performs a synchronous check of the local purchase records.
- This method does not contact the server and only reflects the local state.
- Use this method to determine whether to show purchase UI or unlock features.

**Example Usage:**
```
// Check if ads should be shown
if (!isProductPurchased("com.myapp.removeads")) {
    showAdvertisement();
}
```

### Callback Setters

#### `setProductsLoadedCallback(callback)`

Sets a callback to be invoked when product information has been loaded.

**Parameters:**
- `callback`: A function that takes a boolean success parameter.

**Callback Parameters:**
- `success`: `true` if products were loaded successfully, `false` otherwise.

**Behavior:**
- The callback is invoked after `loadProducts()` completes.
- If successful, your application should update its store UI with the retrieved product information.
- If unsuccessful, your application should display an appropriate error message.

**Example Usage:**
```
setProductsLoadedCallback(function(success) {
    if (success) {
        updateStoreUI();
    } else {
        showErrorMessage("Failed to load store products");
    }
});
```

#### `setPurchaseCompletedCallback(callback)`

Sets a callback to be invoked when a purchase attempt completes.

**Parameters:**
- `callback`: A function that takes a boolean success parameter and a string productId parameter.

**Callback Parameters:**
- `success`: `true` if the purchase was successful, `false` otherwise.
- `productId`: The identifier of the product that was being purchased.

**Behavior:**
- The callback is invoked after a purchase attempt initiated by `purchaseProduct()` completes.
- If successful, your application should unlock the purchased feature and update its UI.
- If unsuccessful, your application should display an appropriate error message.

**Example Usage:**
```
setPurchaseCompletedCallback(function(success, productId) {
    if (success) {
        if (productId === "com.myapp.removeads") {
            disableAds();
        } else if (productId === "com.myapp.extralife") {
            addPlayerLife();
        }
        showSuccessMessage("Purchase successful!");
    } else {
        showErrorMessage("Purchase failed");
    }
});
```

#### `setRestoreCompletedCallback(callback)`

Sets a callback to be invoked when the restore purchases process completes.

**Parameters:**
- `callback`: A function that takes a boolean success parameter.

**Callback Parameters:**
- `success`: `true` if the restore process completed successfully, `false` otherwise.

**Behavior:**
- The callback is invoked after `restorePurchases()` completes.
- If successful, your application should have already processed each restored purchase and updated its state accordingly.
- If unsuccessful, your application should display an appropriate error message.

**Example Usage:**
```
setRestoreCompletedCallback(function(success) {
    if (success) {
        refreshAppUI();
        showSuccessMessage("Purchases restored successfully!");
    } else {
        showErrorMessage("Failed to restore purchases");
    }
});
```

## Best Practices

1. **Initialize Early**: Call `loadProducts()` during application startup to ensure product information is available when needed.

2. **Handle Network Issues**: Implement retry logic for failed network operations, particularly for `loadProducts()`.

3. **Provide Visual Feedback**: Show loading indicators during purchase and restore operations to inform users that an operation is in progress.

4. **Persistence**: Store purchase state locally to avoid unnecessary network requests and provide offline access to purchased content.

5. **Restore Button**: Always provide a clearly visible "Restore Purchases" button in your store UI to allow users to recover their purchases when reinstalling your app or using it on a new device.

6. **Error Handling**: Display user-friendly error messages when operations fail, with specific guidance if possible.

7. **Receipt Validation**: Consider implementing server-side receipt validation for high-value purchases to prevent fraud.

8. **Testing**: Thoroughly test the purchase flow with test accounts before releasing your application.

## Common Issues and Solutions

### Products Not Loading

If `loadProducts()` consistently fails:
- Verify that the product IDs match exactly with those configured in your store dashboard.
- Check that your application has the necessary store permissions.
- Ensure your test account is properly configured for sandbox testing.

### Purchases Not Completing

If `purchaseProduct()` fails:
- Verify that the user is signed in to their store account.
- Check if there are payment issues with the user's account.
- Ensure your application is properly signed and has the necessary store permissions.

### Purchases Not Restoring

If `restorePurchases()` doesn't restore expected purchases:
- Verify that the user is signed in with the same account used for the original purchases.
- Check that the purchases were non-consumable or active subscriptions.
- Ensure your application is correctly identifying and processing the restored purchases.

## Platform-Specific Considerations

While this API provides a consistent interface across platforms, be aware that:

1. The underlying purchase flow and UI will match the platform's native experience.
2. Product availability, pricing, and features may vary by platform and region.
3. Some platforms may require additional initialization steps not covered by this API.

## Security Considerations

1. **Never trust the client**: Implement server-side validation of purchases for high-value or critical content.
2. **Protect purchase state**: Securely store purchase records to prevent tampering.
3. **Monitor for unusual patterns**: Watch for unusual purchase patterns that might indicate fraud or exploitation.


# Complete Guide to Setting Up In-App Purchases on the Apple App Store

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Types of In-App Purchases](#types-of-in-app-purchases)
3. [Step 1: Set Up Your App in App Store Connect](#step-1-set-up-your-app-in-app-store-connect)
4. [Step 2: Create In-App Purchase Products](#step-2-create-in-app-purchase-products)
5. [Step 3: Configure StoreKit in Your Xcode Project](#step-3-configure-storekit-in-your-xcode-project)
6. [Step 4: Implement IAP Code in Your App](#step-4-implement-iap-code-in-your-app)
7. [Step 5: Testing In-App Purchases](#step-5-testing-in-app-purchases)
8. [Step 6: Submit for App Review](#step-6-submit-for-app-review)
9. [Best Practices](#best-practices)
10. [Troubleshooting Common Issues](#troubleshooting-common-issues)

## Prerequisites

Before you begin setting up in-app purchases (IAPs), make sure you have:

- An active Apple Developer Program membership ($99/year)
- A valid App ID configured in your developer account
- Your app created in App Store Connect
- A Paid Applications Agreement in place
- Tax and banking information set up in App Store Connect
- Xcode installed on your Mac

## Types of In-App Purchases

Apple supports four types of in-app purchases:

1. **Consumable**: Can be purchased multiple times (e.g., virtual currency, health points)
2. **Non-Consumable**: Purchased once and do not expire (e.g., premium features, ad removal)
3. **Auto-Renewable Subscriptions**: Recurring billing until canceled (e.g., streaming services, content access)
4. **Non-Renewing Subscriptions**: Fixed duration with no automatic renewal (e.g., season passes)

## Step 1: Set Up Your App in App Store Connect

1. Log in to [App Store Connect](https://appstoreconnect.apple.com)
2. Navigate to "My Apps" and select your app (or create a new one)
3. Go to the "Features" tab
4. Select "In-App Purchases" from the sidebar

## Step 2: Create In-App Purchase Products

1. In the In-App Purchases section, click the "+" button to add a new IAP
2. Select the appropriate IAP type (consumable, non-consumable, etc.)
3. Enter a Reference Name (internal use only)
4. Create a Product ID using reverse-domain notation (e.g., com.yourcompany.app.product1)
5. Set pricing information:
   - Select a price tier
   - For subscriptions, set the duration and renewal settings
6. Fill in the required localization information:
   - Display name (visible to users)
   - Description
   - For subscriptions, provide subscription group details
7. Submit for review (you can save as a draft initially)

## Step 3: Configure StoreKit in Your Xcode Project

1. Open your project in Xcode
2. Select your project in the Navigator
3. Go to the "Capabilities" tab
4. Turn on "In-App Purchase" capability
5. Ensure your app is properly signed with your provisioning profile

## Step 4: Implement IAP Code in Your App

Here's a basic implementation using StoreKit 2 (iOS 15+):

```swift
import StoreKit

class StoreManager: ObservableObject {
    @Published private(set) var products: [Product] = []
    @Published private(set) var purchasedProductIDs = Set<String>()
    
    private var productIDs = [
        "com.yourcompany.app.product1",
        "com.yourcompany.app.product2"
    ]
    
    private var productsLoaded = false
    private var updates: Task<Void, Never>? = nil
    
    init() {
        updates = observeTransactionUpdates()
        Task {
            await loadProducts()
            await updatePurchasedProducts()
        }
    }
    
    deinit {
        updates?.cancel()
    }
    
    @MainActor
    func loadProducts() async {
        guard !productsLoaded else { return }
        
        do {
            products = try await Product.products(for: productIDs)
            productsLoaded = true
        } catch {
            print("Failed to load products: \(error)")
        }
    }
    
    func purchase(_ product: Product) async throws -> Transaction? {
        let result = try await product.purchase()
        
        switch result {
        case .success(let verification):
            let transaction = try checkVerified(verification)
            await updatePurchasedProducts()
            await transaction.finish()
            return transaction
        case .userCancelled:
            return nil
        case .pending:
            return nil
        @unknown default:
            return nil
        }
    }
    
    func checkVerified<T>(_ result: VerificationResult<T>) throws -> T {
        switch result {
        case .unverified:
            throw StoreError.failedVerification
        case .verified(let safe):
            return safe
        }
    }
    
    @MainActor
    func updatePurchasedProducts() async {
        purchasedProductIDs.removeAll()
        
        for await result in Transaction.currentEntitlements {
            do {
                let transaction = try checkVerified(result)
                if transaction.revocationDate == nil {
                    purchasedProductIDs.insert(transaction.productID)
                }
            } catch {
                print("Failed to verify transaction: \(error)")
            }
        }
    }
    
    private func observeTransactionUpdates() -> Task<Void, Never> {
        Task.detached { [weak self] in
            for await verification in Transaction.updates {
                guard let self = self else { return }
                
                do {
                    let transaction = try await self.checkVerified(verification)
                    await self.updatePurchasedProducts()
                    await transaction.finish()
                } catch {
                    print("Failed to verify transaction: \(error)")
                }
            }
        }
    }
    
    enum StoreError: Error {
        case failedVerification
    }
}
```

Usage in SwiftUI:

```swift
struct StoreView: View {
    @StateObject private var storeManager = StoreManager()
    
    var body: some View {
        List {
            ForEach(storeManager.products) { product in
                HStack {
                    VStack(alignment: .leading) {
                        Text(product.displayName)
                            .font(.headline)
                        Text(product.description)
                            .font(.subheadline)
                    }
                    
                    Spacer()
                    
                    Button(action: {
                        Task {
                            do {
                                try await storeManager.purchase(product)
                            } catch {
                                print("Purchase failed: \(error)")
                            }
                        }
                    }) {
                        Text(storeManager.purchasedProductIDs.contains(product.id) ? "Purchased" : product.displayPrice)
                            .bold()
                            .padding(8)
                            .background(storeManager.purchasedProductIDs.contains(product.id) ? Color.gray : Color.blue)
                            .foregroundColor(.white)
                            .cornerRadius(8)
                    }
                    .disabled(storeManager.purchasedProductIDs.contains(product.id))
                }
                .padding(.vertical, 8)
            }
        }
        .navigationTitle("Store")
    }
}
```

## Step 5: Testing In-App Purchases

1. **Create Sandbox Testers**:
   - In App Store Connect, go to "Users and Access" > "Sandbox" > "Testers"
   - Add a new sandbox tester with a unique email and details
   - The email shouldn't be associated with any Apple ID

2. **Use StoreKit Configuration Files (recommended for development)**:
   - In Xcode, create a new StoreKit Configuration File
   - Add your IAP products with prices and details
   - Enable it in your scheme (Edit Scheme > Run > Options > StoreKit Configuration)

3. **Test on Devices**:
   - Sign out of your regular Apple ID on the test device
   - Run your app from Xcode or TestFlight
   - When prompted to purchase, sign in with your sandbox account
   - Complete the purchase (no actual money will be charged)

## Step 6: Submit for App Review

1. Make sure all IAPs are in "Ready to Submit" status in App Store Connect
2. Prepare a demo account for App Review if your IAPs are gated behind login
3. Add special instructions for reviewers if needed (e.g., how to access IAP features)
4. Submit your app for review

## Best Practices

1. **Receipt Validation**: Implement server-side receipt validation for enhanced security
2. **Restore Purchases**: Add a "Restore Purchases" button for non-consumables and subscriptions
3. **Handle Interrupted Purchases**: Account for app crashes or network issues during purchases
4. **Caching**: Cache product information to improve load times
5. **Error Handling**: Provide user-friendly error messages for purchase failures
6. **Subscription Management**: Direct users to settings for subscription management
7. **Localization**: Localize IAP descriptions and prices for global markets
8. **Analytics**: Track purchase patterns and conversion rates

## Troubleshooting Common Issues

1. **Products Not Loading**:
   - Verify Product IDs match exactly between code and App Store Connect
   - Check that your app's bundle ID matches the one in App Store Connect
   - Ensure your Paid Applications Agreement is active
   - Wait a few hours after creating new IAPs for them to propagate

2. **Purchase Failures**:
   - Confirm the sandbox tester has a valid payment method
   - Check for network connectivity issues
   - Verify the user is signed in with a valid Apple ID

3. **Receipt Validation Problems**:
   - Ensure you're using the correct environment URL (sandbox vs. production)
   - Verify your receipt validation logic handles all cases

4. **App Review Rejections**:
   - Make sure your app includes all required restore functionality
   - Ensure IAPs deliver value consistent with their description
   - Verify subscription terms are clearly communicated to users