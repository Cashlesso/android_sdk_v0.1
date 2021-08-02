# android_sdk_v0.1
Android SDK


  **Step 1: SDK Installation and Setup**

![1_d8A4Q6W-OSKObTcVGqX_xg](https://user-images.githubusercontent.com/81406245/127822858-05e61ebe-ce1d-42dd-a4a6-a016ddccb150.png)

```html
              •	Add .aar file in your project 
                  File -> New module -> Select import .aar package -> Click on next button

              •	Add below line to ‘Dependencies’ section of your App build.gradle

                  implementation project(':cashlesso_sdk-release')


              •	Add the following code to your AndroidManifest.xml to get static permission

                  <uses-permission android:name="android.permission.INTERNET"/>
                  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

```



  **Step 2: Initialization**

```java
              •	To initialize the Cashlesso SDK, use below class:
                      Intent intent = new Intent(“YourActivity”, CashlessoPayment.class);

              •	Object: Order
                      Stores all order related information which are required to be passed by you to Cashlesso. Order object is created by following code snippet –

                      Intent intent = new Intent(“YourActivity”, CashlessoPayment.class);
                      HashMap<String, String> paramMap = new HashMap<>();

                      **************Mandate params Start**********************

                      paramMap.put("PAY_ID", “PAY_ID”);
                      paramMap.put("ORDER_ID", “ORDER_ID”);
                      paramMap.put("AMOUNT", “100”);
                      paramMap.put("CURRENCY_CODE",” CURRENCY_CODE”);
                      paramMap.put("SALT", “SALT”);
                      //key in your Production or UAT value should be true(production) or false(UAT)
                      paramMap.put("IS_UAT", “TRUE”);

                      **************Mandate params End**********************

                      //send mapObject through intent with same key
                      intent.putExtra("cashlessoRequest", merchantMap);
                      startActivityForResult(intent, 2);
              
```



  **Step 3: Receive response**
  
```java
              •	Receive output parameters in onActivityResult


                  @Override
                  protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
                      super.onActivityResult(requestCode, resultCode, data);
                      String payment_status_to_merchant = "";

                      if (resultCode == 200) {

                  /* This callback indicates only about completion of UI flow. Inform your server to make the transaction
                              status call to get the status. Update your app with the success/failure status.*/

                          Toast.makeText(this,data.getStringExtra("PaymentResponse"),Toast.LENGTH_LONG).show();
                      }

                  }

```

