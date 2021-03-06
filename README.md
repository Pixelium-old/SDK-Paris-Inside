#AzurWay SDK

##How to configure

First, set the SDK public and secret key in the - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions function
```obj-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [[AzurWaySdk sharedInstance] setTokken:@"YOUR_TOKEN" andDepartureLocation:(CLLocation *) departurePosition]];

  return YES;
}
```

## Display the booking interface

- First set the SDK Options, then, use this function to launch the SDK in the selected ViewController
```obj-c
- (void) launchBooking {
  AzurWaySdkOptions *options = [[AzurWaySdkOptions alloc] init];
  
  
   
  [options setType : (AWTypeEnum)(Booking | Activity | Airport)];,
  [options setNow : (Bool)];
  [options setPayment : (Bool)]; // Redirect to payment if necessary
  [options setArrivalDate : (NSDate *)]; // Mandatory if now == false
  [options setDestination : (CLLocation *)]; // Mandatory if activity or airport
  

  // For Airport or activity destination, pass the destination GPS coordinates 
  [options setDestinationLocation:(CLLocation *)destinationCoord];
  

  [[AzurWaySdk sharedInstance] launchBookingFrom:(ViewController *)containerVC withOptions:(AzurWaySdkOptions *)options]];

}
```

## Display the My Order screen

- First set the SDK Options, then, use this function to launch the SDK in the selected ViewController
```obj-c
- (void) launchBooking {
  AzurWaySdkOptions *options = [[AzurWaySdkOptions alloc] init];
  
  [[AzurWaySdk sharedInstance] launchMyOrderFrom:(ViewController *)containerVC withOptions:(AzurWaySdkOptions *)options]];
}
```

## AzurWaySDKOptions parameters lists


| Function  |  Type |  Description |
|---|---|---|
| setType  | AWTypeEnum  |  Order type (Booking / Activity / Airport) |
| setNow  | BOOL  |  Boolean if booking now |
| setPayment  |  BOOL |  if you need redirection to the payment screen |
| setArrivalDate  |  NSDate |  needed arrival date |
| setDestination  |  CLLocation | destination coordinates  |
| setPaymentViewController | UIViewController<AzurWaySdkPaymentDelegate> | PaymentViewController |

## AzurWaySdkPaymentDelegate

``` obj-c
- (void) initWithActivity:(AzurWayActivity *) activityInfos;
- (void) paymentSuccess;
- (void) paymentError;
```

## AzurWayActivity

Feel free to tell us what information you need for the payment

| Name | Type | Description | 
|---|---|---|
| name | NSString | name |
| price | CGFloat | price |
| location | CLLocation | activity location |
