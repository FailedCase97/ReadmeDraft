# IAPHelper Framework

## Installation:

## Integration Steps:

### Step - 1 
### Step - 2


## Manager Documentation:
There are 6 trypes of notification under the hood which will eventually be posted when the corresponding event will occure. To catch them from the app-end we have to register the notification. To register we can simply call the following function:
```
SubscriptionManager.shared.notificationHandler.addObserver(self)
```
The following class have to conform the "SubManagerNotificationObserver" protocol and implement the following function
```
func updateRequiredThingsFor(
    notificationType: IAPHelper.IAPurchaseState,
    notification: Notification?
)
```
<br></br>
In the above function, we get the notificationType as parameter which will of type **IAPHelper.IAPurchaseState**. Based on notificationType, we can decide the next workflow. In the IAPurchaseState enum, we have few states among which following 6 are most used:
* #### ***.purchaseSuccessful:*** When purchase is successful
* #### ***.purchaseSuccessfulNotification:*** When purchase is successful
* #### ***.purchaseFailureNotification:*** When purchase is failed
* #### ***.restoreSuccessfulNotification:*** When restoration is successful
* #### ***.restoreFailureNotification:*** When restoration is failed
* #### ***.promotionPurchaseStartNotification:*** 
* #### ***.duplicatePurchasedNotification:*** When user tries to purchase an already purchased product 
