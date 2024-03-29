# IAPHelper Framework

## Installation:

To install the **GenericIAPHelper** Framework using CocoaPods, follow these steps:

1. Open your terminal.

2. Navigate to your Xcode project directory using the cd command:
``` bash
cd /path/to/your/project
```
3. Create a Podfile if you don't have one already:
``` bash
pod init
```
4. Open the Podfile with your preferred text editor:
``` bash
nano Podfile
```
5. Add the **GenericIAPHelper** pod to your Podfile:
``` bash
target 'YourTargetName' do
  # Other pods if any
  pod 'GenericIAPHelper'
end
```
Make sure to replace 'YourTargetName' with the actual name of your Xcode target.

6. Save the Podfile and exit the text editor.

7. Install the pods by running the following command in the terminal:
``` bash
pod install
```
8. After the installation is complete, open your Xcode workspace using the generated .xcworkspace file:
``` bash
open YourProject.xcworkspace
```
Now, you should be able to use the **GenericIAPHelper** framework in your Swift project. Remember to import the framework in your Swift files where you need to use it:

``` bash
import GenericIAPHelper
```
Make sure to replace 'YourProject' and 'YourTargetName' with the appropriate names used in your Xcode project.
<br></br>

## Integration:


 Initializes the **SubscriptionManager** singleton instance with the specified parameters.

 **Parameters:**
 
  * `sharedSecret`: The shared secret used for in-app purchase validation.
  * `subscriptionProductIDs`: An array of product identifiers for subscription products.
  * `nonConsumableProductIDs`: An array of product identifiers for non-consumable products.
  * `consumableProductIDs`: An array of product identifiers for consumable products.

 Call this method to set up the **SubscriptionManager** with the necessary information for in-app purchases. This initialization should be performed once, typically during the application's launch.

 **Example usage:**
 ```swift
 SubscriptionManager.shared.initWithProductIDsWithIapSharedSecret(
     sharedSecret: "YOUR_SHARED_SECRET",
     subscriptionProductIDs: ["subscriptionProductID1", "subscriptionProductID2"],
     nonConsumableProductIDs: ["nonConsumableProductID1", "nonConsumableProductID2"],
     consumableProductIDs: ["consumableProductID1", "consumableProductID2"]
 )
```
<br></br>
There are 6 types of notifications underlying the system, which are posted when the corresponding events occur. To capture these notifications from the application end, registration is required, and it can be achieved by calling the following function:
``` swift
SubscriptionManager.shared.notificationHandler.addObserver(self)
```
The following class have to conform the **SubManagerNotificationObserver** protocol and implement the following function:
``` swift
func updateRequiredThingsFor(
    notificationType: IAPHelper.IAPurchaseState,
    notification: Notification?
)
```
<br>

## Enums

In the above function, we get the notificationType as parameter which will of type **IAPHelper.IAPurchaseState**. Based on notificationType, we can decide the next workflow. In the IAPurchaseState enum, we have few states among which following 6 are most used:

* ***.purchaseSuccessfulNotification:*** a notification triggered when the purchase is successful.

* ***.purchaseFailureNotification:*** a notification triggered upon the failure of a purchase transaction.

* ***.restoreSuccessfulNotification:*** a notification triggered when the restoration is successful.

* ***.restoreFailureNotification:*** a notification triggered when the restoration process fails.

* ***.promotionPurchaseStartNotification:*** a notification triggered when the process of a promotional purchase is initiated.

* ***.duplicatePurchasedNotification:*** a notification triggered when a user attempts to purchase a product that has already been acquired.
<br></br>

## Functions

The following public functions within the **SubscriptionManager** can be invoked to perform specific actions:<br></br>

* ***`getProductIDsInfo():`*** 
Returns Array of productIDs.<br></br>

* ***`getProduct(for productId:):`*** 
Returns necessary product info against a product ID.<br></br>

* ***`getFreeTrialPeriod(for:, inDays:):`***
Returns number of trial days against a product ID.<br></br>

* ***`isCurrentSubscription(_ productId:):`*** 
Returns true against a product ID if that subscription is currently on.<br></br>

* ***`isTrialPeriodOngoing():`*** 
Returns true if current subscription's trial days are still remaining.<br></br>

* ***`initWithProductIDs(iapSharedSecret:, subscriptionProductIDs:, nonConsumableProductIDs:, consumableProductIDs:):`*** 
This initialization function is used for setting up notification observers and loading information related to product IDs.<br></br>

* ***`isNonComsumableTypeProduct(productID:):`***
Returns true if the product is non-consumable product.<br></br>

* ***`isComsumableTypeProduct(productID:):`***
Returns true if the product is consumable product.<br></br>

* ***`isSubscriptionTypeProduct(productID:):`***
Returns true if product is of subscription type.<br></br>

* ***`isSubscribedOrUnlockedAll():`*** 
Returns true if any subscription is currentlt running. For debugging purpose may return **DEBUG_FOR_ISSUBSCRIBED** to test premium features.<br></br>

* ***`isIndividuallyPurchased(for productID:):`*** 
Returns true against a product ID if some individual content available on the product is purchased.<br></br>

* ***`purchaseRequest(for: productID) { isPurchaseInitiated in }:`*** 
Tries to purchase product against a product ID.<br></br>

* ***`requestPrice(for:) :`*** 
Returns price against a price Id as string.<br></br>

* ***`requestPriceInDecimal(for:):`*** 
Returns price against a price Id in decimal.<br></br>

* ***`refreshPurchaseableProducts() { skProducts in }:`***
Reloads offline saved receipts and provides an optional completion handler for fetching associated InAppProduct instances.<br></br>

* ***`restorePurchase(afterProductLoading:,andShouldShowSuccessAlert:):`*** 
Tries to restore purchase, if successful shows success alert, else shows failure alert.
<br></br>
## InAppProduct

***InAppProduct*** is a public class serving as a wrapper for SKProduct, encapsulating in-app purchase details and functionality for streamlined integration into Swift applications.