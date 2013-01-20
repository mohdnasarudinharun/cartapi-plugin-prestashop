*** The most recent version of this documentation is available through Appixia Dashboard or Appixia Knowledgebase (http://kb.appixia.com) ***


Appixia Cart API Plugin for Prestashop
======================================

* Introduction *

Appixia apps communicate with the Prestashop cart using a custom web service (XML over HTTP). This cart plugin for Prestashop implements the web service from the cart side and should be installed as a Prestashop module on the merchant's store. The plugin is developed by Appixia Prestashop community and used as-is. The plugin is not designed to be changed during your integration process, although you have the full plugin source-code (PHP). If you wish to change the plugin, contact Appixia to learn how to become an active community developer.

* Merchant Cart API Plugin Overrides *

Many merchants require several customizations to the core Appixia Cart API plugin. These customizations have a special folder named "/override" inside the plugin. Integrators should place all customizations in this folder. The overrides mechanism is very similar to the Prestashop overrides mechanism. You can extend the core plugin classes and override functions that you wish to change. This development is done in PHP, since the Prestashop plugin is written in PHP.


Installation
============

* Automatic Installation for Prestashop 1.4.x *

1. Log into the Prestashop admin panel
2. Go to the Modules tab
3. Click on "Add a module from my computer"
4. Under "Module URL" put:
   http://appixia.com/static/appixiacartapi_1.0.1_prestashop_1.4.x.zip
   If your server does not have ZIP installed put:
   http://appixia.com/static/appixiacartapi_1.0.1_prestashop_1.4.x.tar
   Click on the "Download this module" button.
5. The module is installed automatically by Prestashop
6. Enable the module through the Prestashop admin panel by selecting it in the module list and pressing "Install"

* Manual Installation for Prestashop 1.4.x *

1. Download the the plugin package and save it on your computer
2. Unzip the package to a temporary directory on your computer
3. Copy the /appixiacartapi directory to the /modules directory of your Prestashop server, usually using FTP
4. Enable the module through the Prestashop admin panel by selecting it in the module list and pressing "Install"

* Your Connection Details *

If your Prestashop server homepage is on http://prestastore.com

Store Home Url: http://prestastore.com
Your API Endpoint Url: http://prestastore.com/modules/appixiacartapi/api.php


Appixia Cart API Plugin Core Classes For Override
=================================================

The core plugin classes which you can override are found in /modules/appixiacartapi. You can go over their source code to get a sense of what overrides can be done and where. The main responsibility of these classes is to handle various Appixia Cart API requests. The mobile app communicates with the plugin using a custom web service (XML over HTTP). This web service protocol includes several requests, or "operations", like GetSingleItem, which returns an XML description of a single product.

* Items.php *
In charge of everything related to products and product lists.
Handles the following Cart API operations:
  GetSingleItem - returns detailed XML info about a single product using its id.
  GetItemList - returns a paged list of products according to various filters.

* Categories.php *
In charge of everything related to categories and category lists.
Handles the following Cart API operations:
  GetCategoryList - returns a list of categories according to various filters.

* Login.php *
In charge of login and register of new customers.
Handles the following Cart API operations:
  BuyerLogin - logins a customer (either with username+password, or Facebook).
  BuyerRegister - registers a new customer.

* Order.php *
In charge of the entire checkout process (from adding an item to the cart, to address and payment and creating an order on Prestashop itself). Please note that the term "order" under Appixia is closer to the "cart" term in Prestashop. An "order" under Appixia exists from the moment the customer added a product to the cart.
Handles the following Cart API operations:
  GetOrderUpdate - takes a customer cart of items in some stage of the checkout process (an order), updates the internal Prestashop structures accordingly and replies with changes which need to be made to this "order" by the mobile app.
  GetShippingMethods - takes a customer order and returns the possible shipping methods that the customer needs to choose from.
  GetPaymentMethods - takes a customer order and returns the possible payment methods that the customer needs to choose from. 


Appixia Cart API Plugin For Prestashop Structure
================================================

Normally, the integrator would not make any modifications to the core Prestashop plugin (found in /modules/appixiacartapi), except of course for adding overrides under /modules/appixiacartapi/override. Nevertheless, you have the full core plugin source code in order to see which functions you can override. If you want to override something which is not available as a convenient function, please contact Appixia to have this functionality in the core plugin refactored.

* Plugin Folder Structure *

/modules/appixiacartapi/
Root folder, includes implementations for all the core plugin classes (which you can override with your own implementation in the override folder).

/modules/appixiacartapi/override/
The most important folder for the integrator. This folder will hold all the changes you make to the Appixia Cart API plugin. All customizations for your specific store should be here.

/modules/appixiacartapi/modules
Mobile specific modifications for Prestashop modules are found in this folder. The folder is structured like the Prestashop /modules folder. Every Prestashop module which includes an Appixia specific modification will have the modification in here. Most of the modules you can expect to find here are payment modules (like paypal). You should not modify the code in this folder since this is core code.

/modules/appixiacartapi/engine
Core library code used mostly for encoding and decoding the Appixia Cart API web service protocol (XML/JSON over HTTP). This code is not specific to Prestashop and found in Appixia plugins for other carts as well.

* Plugin Overrides Folder Structure *

/modules/appixiacartapi/override/
The root of the overrides. All the core classes which you wish to override will be placed here. The class file names are identical to the plugin core class file names.

/modules/appixiacartapi/override/cms/
Several places in the mobile app display regular HTML content from the Prestashop website. For example, inside the product details additional sections (like product stylist or product look) are plain HTML. The code that renders these HTML files is found in this folder.

/modules/appixiacartapi/override/cms/assets/
Static files required by the templates in the /cms folder. Mostly mobile-specific versions of JS and CSS files.
