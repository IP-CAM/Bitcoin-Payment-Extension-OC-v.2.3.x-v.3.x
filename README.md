# SpectroCoin OpenCart Crypto Payment Plugin

Integrate cryptocurrency payments seamlessly into your OpenCart store with the [SpectroCoin Crypto Payment Plugin](https://spectrocoin.com/plugins/accept-bitcoin-opencart.html). This extension facilitates the acceptance of a variety of cryptocurrencies, enhancing payment options for your customers. Easily configure and implement secure transactions for a streamlined payment process on your OpenCart website.

## Installation

1. Download latest release from github.
2. From OpenCart admin dashboard navigate to **"Extensions"** -> **"Installer"**.
3. Upload the plugin zip "spectrocoin.ocmod.zip" file (zip file name is strict).
4. Go to **"Extensions"** -> **"Extensions"**. Choose **"Payments"** from the dropdown. Find **"SpectroCoin"** and click **"Install"**.
5. Click **"Edit"** to configure the plugin settings.
6. Move to [Setting up](#setting-up) section.

## Setting up

1. **[Sign up](https://auth.spectrocoin.com/signup)** for a SpectroCoin Account.
2. **[Log in](https://auth.spectrocoin.com/login)** to your SpectroCoin account.
3. On the dashboard, locate the **[Business](https://spectrocoin.com/en/merchants/projects)** tab and click on it.
4. Click on **[New project](https://spectrocoin.com/en/merchants/projects/new)**.
5. Fill in the project details and select desired settings (settings can be changed).
6. Click **"Submit"**.
7. Copy and paste the "Project id".
8. Click on the user icon in the top right and navigate to **[Settings](https://test.spectrocoin.com/en/settings/)**. Then click on **[API](https://test.spectrocoin.com/en/settings/api)** and choose **[Create New API](https://test.spectrocoin.com/en/settings/api/create)**.
9. Add "API name", in scope groups select **"View merchant preorders"**, **"Create merchant preorders"**, **"View merchant orders"**, **"Create merchant orders"**, **"Cancel merchant orders"** and click **"Create API"**.
10. Copy and store "Client id" and "Client secret". Save the settings.

**Note:** Keep in mind that if you want to use the business services of SpectroCoin, your account has to be verified.

## Test order creation on localhost

We gently suggest trying out the plugin in a server environment, as it will not be capable of receiving callbacks from SpectroCoin if it will be hosted on localhost. To successfully create an order on localhost for testing purposes, change these 3 lines in **_CreateOrderRequest.php_**:

`$this->callbackUrl = isset($data['callbackUrl']) ? Utils::sanitizeUrl($data['callbackUrl']) : null;`, <br>
`$this->successUrl = isset($data['successUrl']) ? Utils::sanitizeUrl($data['successUrl']) : null;`, <br>
`$this->failureUrl = isset($data['failureUrl']) ? Utils::sanitizeUrl($data['failureUrl']) : null;`

__To__

`$this->callbackUrl = "https://localhost.com/";`, <br>
`$this->successUrl = "https://localhost.com/";`, <br>
`$this->failureUrl = "https://localhost.com/";`

Don't forget to change it back when migrating website to public.

## Testing Callbacks

Order callbacks in the SpectroCoin plugin allow your WordPress site to automatically process order status changes sent from SpectroCoin. These callbacks notify your server when an order’s status transitions to PAID, EXPIRED, or FAILED. Understanding and testing this functionality ensures your store handles payments accurately and updates order statuses accordingly.
 
1. Go to your SpectroCoin project settings and enable **Test Mode**.
2. Simulate a payment status:
   - **PAID**: Sends a callback to mark the order as **Completed** in WordPress.
   - **EXPIRED**: Sends a callback to mark the order as **Failed** in WordPress.
3. Ensure your `callbackUrl` is publicly accessible (local servers like `localhost` will not work).
4. Check the **Order History** in SpectroCoin for callback details. If a callback fails, use the **Retry** button to resend it.
5. Verify that:
   - The **order status** in WordPress has been updated accordingly.
   - The **callback status** in the SpectroCoin dashboard is `200 OK`.

## Changelog

### 1.1.0 (16/07/2025)

_Added_ support for new JSON and old URL-encoded form data callbacks format. New callbacks will be automatically enabled with new SpectroCoin merchant projects created. With old projects, old callback format will be used. In the future versions old callback format will be removed.

### 1.0.0 (02/17/2025)

This major update introduces several improvements, including enhanced security, updated coding standards, and a streamlined integration process. **Important:** Users must generate new API credentials (Client ID and Client Secret) in their SpectroCoin account settings to continue using the extension. The previous private key and merchant ID functionality have been deprecated.

_Updated_: Order creation API endpoint has been updated for enhanced performance and security.

_Removed_: Private key functionality and merchant ID requirement have been removed to streamline integration.

_Added_: OAuth functionality introduced for authentication, requiring Client ID and Client Secret for secure API access.

_Added_: API error logging and message displaying in order creation process.

_Migrated_: Since HTTPful is no longer maintained, we migrated to GuzzleHttp. In this case /vendor directory was added which contains GuzzleHttp dependencies.

_Reworked_: SpectroCoin callback handling was reworked. Added appropriate callback routing for success, fail and callback.

_Updated_: Instead of using outdated addOrderHistory for changing the order status, we now use the new addHistory method.

_Updated_ Class and some method names have been updated based on PSR-12 standards.

_Updated_ Composer class autoloading has been implemented.

_Added_ _Config.php_ file has been added to store plugin configuration.

_Added_ _Utils.php_ file has been added to store utility functions.

_Added_ _GenericError.php_ file has been added to handle generic errors.

_Added_ Strict types have been added to all classes.

_Updated_ Order creation API endpoint has been updated for enhanced performance and security.

_Removed_ Private key functionality and merchant ID requirement have been removed to streamline integration.

_Added_ OAuth functionality introduced for authentication, requiring Client ID and Client Secret for secure API access.

_Added_ Enhanced the style of the admin's payment settings window to match the design of SpectroCoin.com, providing a more cohesive user experience.

_Migrated_ Since HTTPful is no longer maintained, we migrated to GuzzleHttp. In this case /vendor directory was added which contains GuzzleHttp dependencies.

_Added_ Settings field sanitization.

Added Settings field validation. In this case we minimized possible error count during checkout, SpectroCoin won't appear in checkout until settings validation is passed.

_Added_ "spectrocoin\_" prefix to functiton names.

_Added_ "SpectroCoin\_" prefix to class names.

_Added_ Validation and Sanitization when request payload is created.

_Added_ Validation and Sanitization when callback is received.

_Added_ Components class "SpectroCoin_FormattingUtil" changed to "SpectroCoin_Utilities".

_Added_ Appropriate error logging to OpenCart admin.

_Added_ API error form.

_Optimised_: Removed the The whole $\_REQUEST stack processing. Now only needed callback keys is being processed.

## Information

This client has been developed by SpectroCoin.com If you need any further support regarding our services you can contact us via:

E-mail: merchant@spectrocoin.com </br>
Skype: spectrocoin_merchant </br>
[Web](https://spectrocoin.com) </br>
[X (formerly Twitter)](https://twitter.com/spectrocoin) </br>
[Facebook](https://www.facebook.com/spectrocoin/)
