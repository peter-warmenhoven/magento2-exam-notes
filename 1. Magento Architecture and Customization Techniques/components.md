### composer
  Magento composer library helps to instantiate Composer application and run composer commands.
### ece-tools 
##### Magento Commerce (Cloud) Deployment Tools
ECE-Tools is a set of scripts and tools designed to manage and deploy Cloud projects. The Cloud tools package is compatible with Magento version 2.1.4 and later to provide a rich set of features you can use to manage your Magento Commerce project.
##### Useful Resources
- [Cloud DevDocs](https://devdocs.magento.com/guides/v2.2/cloud/bk-cloud.html)

### framework 
  contains only PHP code. These are libraries of code plus the application entry point that routes requests to modules (that in turn call the Framework libraries). For example, libraries in the Framework help implement a resource model (base classes and interfaces to inherit from) but not the resource models themselves. Certain libraries also support CSS rendering.
- [coming soon: More details here]()
### framework-amqp 
  AMQP library is designed to provide default implementation for Message Queue Framework.
### framework-bulk 
  This component is designed to provide Bulk Operations Framework.
### framework-foreign-key 
   This component is designed to manage logical foreign keys on the application level for entities that are declared in different databases/database servers.
### framework-message-queue 
   This component is designed to provide Message Queue Framework 
### inventory-composer-installer 
# Magento Inventory Composer Installer

Magento Inventory Composer Installer helps ot install modules that belongs to Magento [Multi Source Inventory](https://github.com/magento-engcom/msi/wiki) community project.

To enable simple **upgrade** for existing Magento installations MSI modules will be disabled by default. To enable them please use `magento module:enable` command. For more information please reference to [Magento Developers Documentation](https://devdocs.magento.com/guides/v2.2/install-gde/install/cli/install-cli-subcommands-enable.html).

For fresh Magento **installation** this plugin won't take effect so MSI modules will preserve default behavior. Thereby, they will be installed and enabled if other not configured explicitly.
### language-de_de
German (Germany) language
### language-en_us 
English (United States) language
### language-es_es 
Spanish (Spain) language
### language-fr_fr 
French (France) language
### language-nl_nl
Dutch (Netherlands) language
### language-pt_br 
Portuguese (Brazil) language
### language-zh_hans_cn 
Chinese (China) language
### magento-composer-installer 
#### Magento Composer Installer
  This is a fork of the [Magento Composer Installer](https://github.com/magento-hackathon/magento-composer-installer) repo that provides support for Magento 2 components (modules, themes, language packages, libraries and components).
##### Usage
In the component's `composer.json`, specify:
*   `type`, type of Magento 2 component.
*   `extra/map`, list of files to move and their paths relative to the Magento root directory.
*   `extra/chmod`, list of permissions that should be set for files.
    **Note**:
    * `extra/map` is required only if your component needs to be moved to a location other than `<Magento root>/vendor`. Otherwise, omit this section.
    * `extra/chmod` is required only if you need to set specific permissions for files.
##### Supported Components
The following list explains the use of `type` in `composer.json`.

##### Magento Module 
`"type": "magento2-module"`

Installation location: Default vendor directory or as defined in `extra/map`

Example:

```json
{
    "name": "magento/module-core",
    "description": "N/A",
    "require": {
        ...
    },
    "type": "magento2-module",
    "extra": {
        "map": [
            [
                "*",
                "Magento/Core"
            ]
        ]
    }
}
```

Final location is `<magento root>/app/code/Magento/Core`

##### Magento Theme 
`"type": "magento2-theme"`

Installation location: `app/design`

Example:
```json
{
    "name": "magento/theme-frontend-luma",
    "description": "N/A",
    "require": {
        ...
    },
    "type": "magento2-theme",
    "extra": {
        "map": [
            [
                "*",
                "frontend/Magento/luma"
            ]
        ]
    }
}
```

Final location is `<magento_root>/app/design/frontend/Magento/luma`

##### Magento Language Package
`"type": "magento2-language"`

Installation location: `app/i18n`

Example:
```json
{
    "name": "magento/language-de_de",
    "description": "German (Germany) language",
    "require": {
        ...
    },
    "type": "magento2-language",
    "extra": {
        "map": [
            [
                "*",
                "Magento/de_DE"
            ]
        ]
    }
}
```

Final location is `<magento_root>/app/i18n/Magento/de_DE`

##### Magento Library
`"type": "magento2-library"`

Support for libraries located in `lib/internal` instead of in the `vendor` directory.

Example:

```json
{
    "name": "magento/framework",
    "description": "N/A",
    "require": {
       ...
    },
    "type": "magento2-library",
    "extra": {
        "map": [
            [
                "*",
                "Magento/Framework"
            ]
        ]
    }
}
```

Final location is `<magento_root>/lib/internal/Magento/Framework`

##### Magento Component
`"type": "magento2-component"`

Installation location: Magento root directory

Example:

```json
{
    "name": "magento/migration-tool",
    "description": "N/A",
    "require": {
        ...
    },
    "type": "magento2-component",
    "extra": {
        "map": [
            [
                "*",
                "dev/tools/Magento/Tools/Migration"
            ]
        ]
    }
}
```

Final location is `<magento_root>/dev/tools/Magento/Tools/Migration`


#### Autoload
After handling all Magento components, `<magento_root>/app/etc/vendor_path.php` specifies the path to your `vendor` directory.

This information allows the Magento application to utilize the Composer autoloader for any libraries installed in the `vendor` directory. The path to `vendor` varies between particular installations and depends on the `magento_root` setting for the Magento Composer installer. That's why it should be generated for each installation.

You must run `composer install` to install dependencies for a new application or `composer update` to update dependencies for an existing application.

#### Deployment Strategy
The Magneto Composer Installer uses the `copy` deployment strategy. It copies each file or directory from the `vendor` directory to its designated location based on the `extra/map` section in the component's `composer.json`.

There are [other deployment strategies](https://github.com/magento/magento-composer-installer/blob/master/doc/Deploy.md) that could be used; however, we don't guarantee that any of them will work.

#### Usage `extra/chmod`

The following example shows how you can set specific permissions for files.

Example:

```json
{
    "name": "magento/module-sample",
    "description": "N/A",
    "require": {
        ...
    },
    "type": "magento2-module",
    "extra": {
         "chmod": [
            {
                "mask": "0755",
                "path": "bin/magento"
            },
            {
                "mask": "0644",
                "path": "some_dir/file.jpg"
            }
        ]
    }
}
```

`mask` is a bit mask for chmod command

`path` is a path to file relative to the Magento root folder

#### Notes
- The extra->magento-root-dir option is no longer supported. It displays only to preseve backward compatibility.
### magento2-b2b-base 
  Magento 2 Base (Enterprise Edition B2B)
### magento2-base 
  This component includes Magento 2 Base (Open Source)
### magento2-ee-base 
  This component includes Magento 2 Base (Commerce)
### module-admin-gws 
  **AdminGws** provides configuration management within the Global, Website, and Store data scopes. Restrictions can be 
imposed on various system elements through configurations that are applied at the desired level.
### module-admin-notification 
  **Admin Notification** provides the ability to alert administrators via
system messages and provides a message inbox for surveys and notifications.
### module-advanced-catalog 
  Magento\AdvancedCatalog module introduces list of optimizations to allow higher concurrency on product management
operations with immediate update of product data on frontend and plays as an extension to indexation logic of
Magento\Catalog module.
### module-advanced-checkout 
  Magento\AdvanceCheckout extends Magento_Checkout with following functions: adding product to cart by entering SKU on
frontend, uploading list of SKUs to add products to cart on frontend and ability for admin to manage customer's shopping
cart.
### module-advanced-pricing-import-export 
  The Magento_AdvancedPricingImportExport module handles the import and export of the advanced pricing.
### module-advanced-rule
  AdvancedRule module enhances the performance of rule processing.
### module-advanced-sales-rule 
  AdvancedSalesRule module enhances the performance of sale rule processing.
### module-advanced-search
  AdvancedSearch module introduces advanced search functionality and provides interfaces that allow to implement this functionality by 3rd party search engines
### module-amqp
  **Amqp** provides functionality to publish/consume messages with Amqp.
### module-analytics 
The Magento_Analytics module integrates your Magento instance with the [Magento Business Intelligence (MBI)](https://magento.com/products/business-intelligence) to use [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html) functionality.

The module implements the following functionality:

* enabling subscription to the MBI and automatic re-subscription
* changing the base URL with the same MBI account remained
* declaring the configuration schemas for report data collection
* collecting the Magento instance data as reports for the MBI
* introducing API that provides the collected data
* extending Magento configuration with the module parameters:
    * subscription status (enabled/disabled)
    * industry (a business area in which the instance website works)
    * time of data collection (time of the day when the module collects data)

##### Structure

Beyond the [usual module file structure](http://devdocs.magento.com/guides/v2.2/architecture/archi_perspectives/components/modules/mod_intro.html) the module contains a directory `ReportXml`.
[Report XML](http://devdocs.magento.com/guides/v2.2/advanced-reporting/report-xml.html) is a markup language used to build reports for Advanced Reporting.
The language declares SQL queries using XML declaration.

##### Subscription Process

The subscription to the MBI service is enabled during the installation process of the Analytics module. Each administrator will be notified of these new features upon their initial login to the Admin Panel.

##### Analytics Settings

Configuration settings for the Analytics module can be modified in the Admin Panel on the Stores > Configuration page under the General > Advanced Reporting tab.

The following options can be adjusted:
* Advanced Reporting Service (Enabled/Disabled)
    * Alters the status of the Advanced Reporting subscription
* Time of day to send data (Hour/Minute/Second in the store's time zone)
    * Defines when the data collection process for the Advanced Reporting service occurs
* Industry
    * Defines the industry of the store in order to create a personalized Advanced Reporting experience

##### Extensibility

We do not recommend to extend the Magento_Analytics module. It introduces an API that is purposed to transfer the collected data. Note that the API cannot be used for other needs.

### module-asynchronous-operations 
 This component is designed  to provide response for client who launched the bulk operation as soon as possible and postpone handling of operations moving them to background handler.
### module-authorization
  **Authorization** enables management of access control list roles and
rules in the application.
### module-authorizenet 
  The Magento_Authorizenet module implements the integration with the Authorize.Net payment gateway and makes the latter available as a payment method in Magento.
### module-b2b
  The Magento_b2b module is the base module for B2B. It must be present on all B2B installations.

This module also provides several B2B branding elements. For example, it adds a link to B2B customer support in Admin, and it displays "B2B Edition" at the bottom of the site. Also, the module adds the configuration page for B2B settings where an admin user can enable or disable a B2B feature. Disabling a B2B feature in store configurations disables this feature for the storefront only, and it is still available in the admin panel.

##### Installation details

This module must be installed to use and to configure the other B2B modules. It can be uninstalled after other B2B modules are uninstalled.

##### Structure
 
[Learn about a typical file structure for a Magento 2 module](http://devdocs.magento.com/guides/v2.2/extension-dev-guide/build/module-file-structure.html).
 
##### Extensibility
 
Extension developers can interact with the Magento_B2b module. For more information about the Magento extension mechanism, see [Magento plug-ins](http://devdocs.magento.com/guides/v2.2/extension-dev-guide/plugins.html).
 
[The Magento dependency injection mechanism](http://devdocs.magento.com/guides/v2.2/extension-dev-guide/depend-inj.html) enables you to override the functionality of the Magento_B2b module.
### module-backend
  The Backend module contains common infrastructure and assets for other modules to be defined and used in their
administration user interface (UI). It does not contain anything specific to other modules. Among many things it
handles the logic of authenticating and authorizing users.
### module-backup
  The Backup module allows administrators to perform backups and rollbacks. Types of backups include system, database and media backups. This module relies on the Cron module to schedule backups.

This module does not affect the storefront.
### module-banner
  The Banner module allows creating and managing dynamic blocks and widgets in Magento application. 
The Dynamic Block content can be specified by Store View.
### module-banner-customer-segment
The Banner Customer Segment module allows creating and managing banners in the customer segment scope.
### module-braintree 
Module Magento\Braintree implements integration with the Braintree payment system.
### module-bundle
Magento_Bundle module introduces new product type in the Magento application named Bundle Product.
This module is designed to extend existing functionality of Magento_Catalog module by adding new product type.
### module-bundle-graph-ql 
**BundleGraphQl** provides type and resolver information for the GraphQl module
to generate bundle product information.
### module-bundle-import-export
Magento_BundleImportExport module implements Bundle products import/export functionality.
This module is designed to extend existing functionality of Magento_CatalogImportExport module by adding new product type.
### module-bundle-import-export-staging
<h2>Magento_BundleImportExportStaging module</h2>
##### Overview
The Magento_BundleImportExportStaging module is a part of the staging functionality in Magento EE. It extends the Magento_BundleImportExport module functionality to be used in staging mode.
##### Implementation Details
The Magento_BundleImportExportStaging module:
 * adds plugin on `\Magento\BundleImportExport\Model\Import\Product\Type\Bundle\RelationsDataSaver` to add sequence information to bundle product relations (options, selections, etc.)
##### Dependencies
You can find the list of modules the Magento_BundleImportExportStaging module depends on in the `require` section of the `composer.json` file located in the same directory as this `README.md` file.
##### Extension Points
The Magento_BundleImportExportStaging module does not provide any specific extension points.

### module-bundle-negotiable-quote
The Magento_BundleNegotiableQuote module enables bundle products to be displayed in a negotiable quote in an B2B environment. This module extends Magento_NegotiableQuote module and Magento_Bundle module.
The Magento_BundleNegotiableQuote module provides the following features:

* Display bundle products in a negotiable quote.
* Order bundle products from a negotiable quote.

### module-bundle-requisition-list
The Magento_BundleRequisitionList module enables bundle products to be displayed in a requisition list in an B2B environment. This module extends Magento_RequisitionList module and Magento_Bundle module.

The Magento_BundleRequisitionList module provides the following features:

* Display bundle products in a requisition list. 

* Add bundle products to cart from a requisition list.
### module-bundle-sample-data
Magento_BundleSampleData module consists of installation scripts and fixtures.
### module-bundle-shared-catalog
The Magento_BundleSharedCatalog module enables bundle products to be added to a shared catalog in an B2B environment. This module extends Magento_SharedCatalog module and Magento_Bundle module.
The Magento_BundleSharedCatalog module provides the following features:

* Display and manage prices for bundle products within a shared catalog.
* Control the visibility of bundle products in quotes and orders. Only those bundle products that have been added to a shared catalog will be available for searches via the "Add by SKU" feature in quotes and orders.
### module-bundle-staging
The Magento_BundleStaging module is a part of the staging functionality in Magento EE. This new functionality enables you to stage a bundle product in the Schedule Update form of the product.
### module-cache-invalidate
The CacheInvalidate module is used to invalidate the Varnish cache if it is configured.
It listens for events that request the cache to be flushed or cause the cache to be invalid, then sends Varnish a purge request using cURL.
### module-captcha
The Captcha module allows applying Turing test in the process of user authentication or similar tasks.
### module-catalog
Magento_Catalog module functionality is represented by the following sub-systems:
 - Products Management. It includes CRUD operation of product, product media, product attributes, etc...
 - Category Management. It includes CRUD operation of category, category attributes

Catalog module provides mechanism for creating new product type in the system.
Catalog module provides API filtering that allows to limit product selection with advanced filters.
### module-catalog-analytics
The Magento_CatalogAnalytics module configures data definitions for a data collection related to the Catalog module entities to be used in [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html).
### module-catalog-event
Magento_CatalogEvent module is designed for creating campaigns that encourage customers to buy products with lower prices.
There are three types of the catalog events: upcoming, open, closed.
### module-catalog-graph-ql
**CatalogGraphQl** provides type and resolver information for the GraphQl module
to generate catalog and product information endpoints.
### module-catalog-import-export 
### module-catalog-import-export-staging
The Magento_CatalogImportExportStaging module is a part of the staging functionality in Magento EE. It extends the Magento_CatalogImportExport module functionality to be used in staging mode.
### module-catalog-inventory
Magento_CatalogInventory module allows retrieve and update stock attributes, such as status and quantity.
### module-catalog-inventory-graph-ql 
**CatalogInventoryGraphQl** provides type information for the GraphQl module
to generate inventory stock fields for product information endpoints.
### module-catalog-inventory-staging 
The Magento_CatalogInventoryStaging module is a part of the staging functionality in Magento EE. It extends the Magento_CatalogInventory module functionality, adding the capability to monitor the "Stock Status" field on the Schedule Update form of a product.
### module-catalog-permissions
Magento_CatalogPermissions feature allows to restrict the following permissions:
- Browse categories
- Display product prices
- Add to cart
- Catalog search
The permissions can be restricted for specific customer groups and guest users.
### module-catalog-rule
Magento_CatalogRule module is responsible for one of the types of price rules in Magento. Catalog Rules are applied to products before they are added to the cart.
### module-catalog-rule-configurable 
Magento_CatalogRuleConfigurable module is an extension of Magento_CatalogRule and Magento_ConfigurableProduct modules that handle catalog rule indexer for configurable product

### module-catalog-rule-sample-data
Magento_CatalogRuleSampleData module consists of installation scripts and fixtures.
### module-catalog-rule-staging
The Magento_CatalogRuleStaging module is a part of the staging functionality in Magento EE. It enables you to create new catalog rule updates or add new changes to the existing store updates. In other words, you can modify the catalog rules in updates. These updates are shown on the content dashboard.
### module-catalog-sample-data
Magento_CatalogSampleData module consists of installation scripts and fixtures.
### module-catalog-search
Magento_CatalogSearch module is an extension of Magento_Catalog module that allows to use search engine for product searching capabilities.
The module implements Magento_Search library interfaces.
### module-catalog-staging
The Magento_CatalogStaging module is a part of the staging functionality in Magento EE. It enables you to create new catalog updates or add new changes to the existing store updates. In other words, you can modify the category and product entity attributes in updates. These updates are shown on the content dashboard.

###### Implementation Details

The Magento_CatalogStaging module extends the Magento_Catalog module functionality. It changes a category and product creation page, and related database tables to make them compatible with the Magento Staging Framework.

The following fields are removed from the Magento_Catalog module forms:

- Category form:
  - Schedule design update from
  - Schedule design update to

- Product form:
  - Set as new from
  - Set as new to
  - Schedule design update from
  - Schedule design update to
  - Special price from
  - Special price to

They are all related to the time period attributes, and now can be set using staging functionality, when you schedule a new update as:

- Special price
- Schedule design update
- Set product as new

###### Category Staging

The Magento_CatalogStaging module enables you to stage the following category attributes:

- Enable/disable Category
- Include in Menu
- Category Name
- Content
    - Category Image
    - Description
    - CMS Blocks
- Display Settings
    - Display Mode
    - Anchor
    - Product Sorting
    - Layered Navigation Price Step
- Search Engine Optimization
    - Meta Title
    - Meta Keywords
    - Meta Description
- Design
    - Layout
    - Layout Update XML
    - New Theme

The following category attributes cannot be staged:

- Assignment of Products to a Category
- URL

###### Product Staging

The Magento_CatalogStaging module enables you to stage the following product attributes:

- Attribute Set
- Product Name
- Price
- Weight attributes
- Visibility
- New(flag)
- Country of Manufacture
- Description
- Websites(assignment)
- Design
  - Layout
  - Display Product Options In
  - Layout Update XML
- Related Products, Up-Sells, and Cross-Sells

Also, you can stage any other attribute added in Admin.

The following product attributes cannot be staged:

- Quantity
- URL Key
- SKU
### module-catalog-url-rewrite 
### module-catalog-url-rewrite-graph-ql
**CatalogUrlRewriteGraphQl** provides type information for the GraphQl module
to generate url rewrite fields for catalog and product information endpoints.
### module-catalog-url-rewrite-staging
The Magento_CatalogUrlRewriteStaging module is a part of the staging functionality in Magento EE. It extends the Magento_CatalogUrlRewrite module.
### module-catalog-widget
**CatalogWidget** contains various widgets that extend Catalog module functionality:
- Product List widget provides widget that contains product list created using rule based filter.
### module-checkout
Magento\Checkout module allows merchant to register sale transaction with the customer. Module implements consumer flow
that includes such actions like adding products to cart, providing shipping and billing information and confirming
the purchase.
### module-checkout-agreements
Magento\CheckoutAgreements module provides the ability add web store agreement that customers must accept before purchasing
products from store. The customer will need to accept the terms and conditions in the Order Review section of the
checkout process to be able to place an order if Terms and Conditions functionality is enabled.
### module-checkout-staging
The Magento_CheckoutStaging module is a part of the staging functionality in Magento EE.
It extends the checkout functionality and enables you to use it in the staging preview mode.

##### Implementation details
The Magento_CheckoutStaging module extends the following Magento_Checkout module functionality to be used in the staging preview mode:
- Disables an order creation
- Creates a demo quote
- Deletes the demo quote using cron
Configuration options:
- The `preview_quota_lifetime` parameter in the `Magento/CheckoutStaging/etc/config.xml` sets the lifetime of the demo quote.
- The `schedule` parameter in the `Magento/CheckoutStaging/etc/crontab.xml` sets a launch schedule of the cron.
### module-cms
The CMS module provides the create, edit, and manage functionality on pages for different content types.
###### Wysiwyg

The Wysiwyg UI component is a customizable and configurable TinyMCE4 editor.

The default implementation has the following customizations:

* Magento Media Library support
### module-cms-graph-ql
**CmsGraphQl** provides type information for the GraphQl module
to generate CMS fields for cms information endpoints.
### module-cms-sample-data
Magento_CmsSampleData module consists of installation scripts and fixtures.
### module-cms-staging
The Magento_CmsStaging module is a part of the staging functionality in Magento EE. It enables you to create new CMS Page and the CMS Block updates or add new changes to the existing store updates. In other words, you can modify the CMS Pages and the CMS Blocks in updates. These updates are shown on the content dashboard.
###### CMS Pages

You can stage the following parameters:

- Enable/Disable CMS Page
- Page Title
- Content 
    - Content Heading
    - Content (WYSIWYG)
- Search Engine Optimization 
    - URL Key
    - Meta Keywords
    - Meta Description
- Design 
    - Layout
    - Layout Update XML
    - Theme

###### CMS Blocks

The following parameters can be staged:

- Enable/Disable CMS Block
- Block Title
- Identifier 
- Store View
- Content (WYSIWYG)
### module-cms-url-rewrite
The Magento_CmsUrlRewrite module adds support for URL rewrite rules for CMS pages. See also Magento_UrlRewrite module. 

The module adds and removes URL rewrite rules as CMS pages are added or removed by a user.
The rules can be edited by an admin user as any other URL rewrite rule. 

### module-cms-url-rewrite-graph-ql
**CmsUrlRewriteGraphQl** provides type information for the GraphQl module
to generate url rewrite fields for cms information endpoints.

### module-company
The Magento_Company module allows a merchant to create a company account and assign multiple members of the company to the account. 

The module also implements roles and permissions for the company members. The company admin builds a hierarchical company structure (which consists of teams and users) in the storefront and assigns roles and permissions to the company members. This hierarchy allows the company admin to control user activity within the account. This hierarchy as well as roles and permissions are currently available in the storefront only. A merchant can only view the list of company members in Admin.
A merchant can view and manage company profiles in Admin. A company's status controls what kind of access the company members have to the website. An admin user can also configure company-level emails and allow or disallow a company registration from the storefront. Also, this module adds a 'customer type' attribute to the customer in Admin: individual user, company member or company admin.
### module-company-credit
The Magento_CompanyCredit module adds the "Payment on Account" payment method for B2B companies. It also allows the credit history to be viewed from both Admin and the storefront. 

With the Magento_Company Credit module
- a customer can pay orders with Payment on Account method (or in credit);
- an admin user can manage credit and credit settings for a company (in the admin panel);
- merchants and customers can track credit history, and specifically: credit allocation, order placement, credit reimbursement, credit change (amount, currency or possibility to exceed credit limit).

The company credit functionality is available for company users only.
 
### module-company-graph-ql
**CompanyGraphQl** provides type information for the GraphQl module
to generate company fields for customer information endpoints.

### module-company-payment
The Magento_CompanyPayment module allows a merchant to configure which payment methods are available for B2B companies.

In Admin, the CompanyPayment module adds an additional panel (on the Company profile page and on the B2B Features page) where a merchant configures payment methods for companies. Payment methods can be configured on the store level or on the company level.
### module-config
The Config module is designed to implement system configuration functionality.
It provides mechanisms to add, edit, store and retrieve the configuration data
for each scope (there can be a default scope as well as scopes for each website and store).

Modules can add items to be configured on the system configuration page by creating 
system.xml files in their etc/adminhtml directories. These system.xml files get merged 
to populate the forms in the config page.

### module-configurable-import-export 
### module-configurable-negotiable-quote
The Magento_ConfigurableNegotiableQuote module enables configurable products to be displayed in a negotiable quote in an B2B environment. This module extends Magento_NegotiableQuote and Magento_Configurable modules.

The Magento_ConfigurableNegotiableQuote module provides the following features:

* Display configurable products in a negotiable quote.
 
* Order configurable products from a negotiable quote.
### module-configurable-product
Magento_ConfigurableProduct module introduces new product type in the Magento application called Configurable Product.
This module is designed to extend existing functionality of Magento_Catalog module by adding new product type.

Configurable Products let the customers select the variant they desire by choosing options.
For example, store owner sells t-shirts in two colors and three sizes.

### module-configurable-product-graph-ql
**ConfigurableProductGraphQl** provides type and resolver information for the GraphQl module
to generate configurable product information.
### module-configurable-product-sales
The Magento_ConfigurableProductSales module checks that the selected options of order item are still presented in
Catalog. Returns true if the previously ordered item configuration is still available.
### module-configurable-product-staging
The Magento_ConfigurableProductStaging module is a part of the staging functionality in Magento EE. It enables you to create new Configurable Product updates or add new changes to the existing store updates. In other words, you can modify the Configurable Products entity attributes in updates. These updates are shown on the content dashboard.
### module-configurable-requisition-list
The Magento_ConfigurableRequisitionList module enables configurable products to be displayed in a requisition list in an B2B environment. This module extends Magento_RequisitionList and Magento_Configurable modules.

The Magento_ConfigurableRequisitionList module provides the following features:

* Display configurable products in a requisition list.

* Add configurable products to cart from a requisition list.
### module-configurable-sample-data
Magento_ConfigurableSampleData module consists of installation scripts and fixtures.
### module-configurable-shared-catalog
The Magento_ConfigurableSharedCatalog module enables configurable products to be added to a shared catalog in an B2B environment. This module extends Magento_SharedCatalog and Magento_Configurable modules.

The Magento_ConfigurableSharedCatalog module provides the following features:

* Display base and custom prices for configurable products within a shared catalog. There is no ability to edit the price of a configurable product.

* Control the visibility of configurable products in quotes and orders. Only those configurable products that have been added to a shared catalog will be available for searches via the "Add by SKU" feature in quotes and orders. 

### module-contact
Magento_Contact module provides an implementation of "Contact Us" feature based on sending email message, allows to configure email recipients, email template, etc...

### module-cookie
Magento_Cookie module allows enabling and configuring HTTP cookie related settings for the store. These settings are available in the store administration.

### module-cron
Cron is a module that enables scheduling of jobs. Other modules can add cron jobs by including crontab.xml in their etc directory. The command "bin/magento cron:run" should be run periodically to trigger the Cron module to run its scheduled jobs.
This module also allows administrators to tune cron options in Magento Admin.
### module-currency-symbol
#### CurrencySymbol

**CurrencySymbol** enables the creation of custom currencies and management of currency conversion rates.

##### Controllers

###### Currency Controllers
***CurrencySymbol\Controller\Adminhtml\System\Currency\FetchRates.php*** gets a specified currency conversion rate.
Supports all defined currencies in the system.
***CurrencySymbol\Controller\Adminhtml\System\Currency\SaveRates.php*** saves rates for defined currencies.

###### Currency Symbol Controllers
***CurrencySymbol\Controller\Adminhtml\System\Currencysymbol\Reset.php*** resets all custom currency symbols.
***CurrencySymbol\Controller\Adminhtml\System\Currencysymbol\Save.php*** creates custom currency symbols.


### module-custom-attribute-management
Magento_CustomAttributeManagement implements user-defined attributes management which provides ability to manage attributes of customers and their address.
Admin user can manage attributes on UI level without assistance of programmer.
Admin user can create new, modify, and remove attributes, control attributes properties and visibility on frontend.
User defined attributes are attributes which are created by admin user and not available out of box.
This attributes can be deleted from the system after their creation.
System attributes are attributes which cannot be deleted from the system in usual way and admin user can edit only their label.
Hidden attribute is an attribute which is hidden from the user on back-end and on front-end.

### module-customer
The Magento_Customer module serves to handle the customer data (Customer, Customer Address and Customer Group entities) both in the admin panel and the storefront. 
For customer passwords, the module implements upgrading hashes. 

### module-customer-analytics
The Magento_CustomerAnalytics module configures data definitions for a data collection related to the Customer module entities to be used in [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html).
### module-customer-balance
The Magento_CustomerBalance module enables customers to have a non-monetary balance in store credits associated to their accounts.
Store credit can be used by customers for shopping in the store and by the store administrator for making refunds.

### module-customer-balance-sample-data
Magento_CustomerBalanceSampleData module consists of installation scripts and fixtures.
### module-customer-custom-attributes
The Magento_CustomerCustomAttributes module handles user-defined customer and customer address attributes.
User-defined attributes are the ones, which are created by a store administrator additionally to the default ones.

### module-customer-finance
The Magento\CustomerFinance module handles the import and export of the store credit and reward customer data.
It extends Magento_CustomerImportExport and joins the basic customer data with reward and customer balance information to enable to import/export of customer data with reward and store credit data.

### module-customer-graph-ql 
**CustomerGraphQl** provides type and resolver information for the GraphQl module
to generate customer information endpoints.

### module-customer-import-export
The Magento_CustomerImportExport module handles the import and export of the customers data and related addresses.

### module-customer-sample-data
Magento_CustomerSampleData module consists of installation scripts and fixtures.
### module-customer-segment
The Magento_CustomerSegment module enables customer segmentation, allowing the creation of customer groups based on characteristics like shopping cart content, orders history, address, and so on.
This allows dynamically targeting different content and promotions for those groups. Various components of a website, such as promotions and banners, can be personalized depending on the customer segment of a customer browsing the store at the moment.

### module-cybersource
The Magento_Cybersource module implements the integration with the Cybersource payment gateway and makes the latter available as a payment method in Magento.

### module-deploy
Deploy is a module that holds collection of services and command line tools to help with Magento application deployment. 
To execute this command, please, run "bin/magento setup:static-content:deploy" from the Magento root directory.
Deploy module contains 2 additional commands that allows switching between application modes (for instance from 
development to
production) and show current application mode. To change the mode run "bin/magento setup:mode:set [mode]".
Where mode can be one of the following:
 - development
 - production
When switching to production mode, you can pass optional parameter skip-compilation to do not compile static files, CSS 
and do not run the compilation process.
### module-developer
The Magento_Developer module provides functionality to make it easier to develop in Magento 2.

### module-dhl
The Magento_Dhl module implements the integration with the DHL shipping carrier.
DHL is available for international shipments only.

### module-directory
**Directory** enables the management of countries and regions recognized by the store and associated data
like the country code and currency rates. Also, enables conversion of prices to a specified currency format.

### module-downloadable
Magento_Downloadable module introduces new product type in the Magento application called Downloadable Product.
This module is designed to extend existing functionality of Magento_Catalog module by adding new product type.

### module-downloadable-graph-ql
**DownloadableGraphQl** provides type and resolver information for the GraphQl module
to generate downloadable product information.

### module-downloadable-import-export
The Magento_DownloadableImportExport module handles the import and export of the downloadable products.

### module-downloadable-sample-data
Magento_DownloadableSampleData module consists of installation scripts and fixtures.

### module-downloadable-staging
The Magento_DownloadableStaging module is a part of the staging functionality in Magento EE. It enables you to create new Downloadable Product updates or add new changes to the existing store updates. In other words, you can modify the Downloadable Products entity attributes in updates. These updates are shown on the content dashboard.

### module-eav
Magento\EAV stands for Entity-Attribute-Value. The purpose of Magento\Eav module is to make entities
configurable/extendable by admin user.

### module-eav-graph-ql
**EavGraphQl** primarily provides the GraphQl module information to generate metadata for Eav attributes.

### module-elasticsearch
Magento\Elasticsearch module allows to use Elastic search engine for product searching capabilities.
The module implements Magento\Search library interfaces.

### module-email
**Email** enables you to manage email templates, which are used when you send email through the
*\Magento\Framework\Mail\TransportInterface* implementations.

### module-encryption-key
The Magento_EncryptionKey module provides an advanced encryption model to protect passwords and other sensitive data.

### module-enterprise 
The Enterprise module switches the store to Enterprise edition by adding a link to Enterprise customer support in Admin Panel, switching notifications from Community to Enterprise-related ones, some small enhancements like displaying "Enterprise Edition" in the bottom of the site, etc.

### module-eway
The Magento_Eway module implements the integration with the Eway payment gateway and makes the latter available as a payment method in Magento.

### module-fedex
The Magento_Fedex implements the integration with the FedEx shipping carrier.

### module-gift-card
Magento_GiftCard module introduces new product type in the Magento application called GiftCard Product.
This module extends existing functionality of Magento_Catalog module by adding new product type.

This product option enables store owner to offers gift cards in Virtual, Physical, or Combination format. 
When a gift card is ordered, a unique code is generated that is emailed to a customer for virtual gift cards, or exported for printing to physical gift cards. 
This unique number can only be redeemed by one customer.


### module-gift-card-account
The Magento_GiftCardAccount module is responsible for gift card balances, for both gift cards created by a store administrator and gift cards sold as gift card products.


### module-gift-card-graph-ql
**GiftCardGraphQl** provides type and resolver information for the GraphQl module
to generate giftcard product information.


### module-gift-card-import-export
Magento_GiftCardImportExport module introduces import and export form GiftCard Product.
This module extends existing functionality of Magento_CatalogImportExport module by adding new product type.

### module-gift-card-negotiable-quote
The Magento_GiftCardNegotiableQuote module enables gift cards to be displayed in a negotiable quote in an B2B environment. This module extends Magento_NegotiableQuote and Magento_GiftCard modules.

The Magento_GiftCardNegotiableQuote module provides the following features:

* Display gift cards in a negotiable quote.

* Order gift cards from a negotiable quote.


### module-gift-card-requisition-list
The Magento_GiftCardRequisitionList module enables gift cards to be displayed in a requisition list in an B2B environment. This module extends Magento_RequisitionList and Magento_GiftCard modules.
The Magento_GiftCardRequisitionList module provides the following features:

* Display gift cards in a requisition list. 
* Add gift cards to cart from a requisition list.

### module-gift-card-sample-data
Magento_GiftCardSampleData module consists of installation scripts and fixtures.

### module-gift-card-shared-catalog
The Magento_GiftCardSharedCatalog module enables gift cards to be added to a shared catalog in an B2B environment. This module extends Magento_SharedCatalog and Magento_GiftCard modules.

The Magento_GiftCardSharedCatalog module provides the following features:

* Display and manage prices for gift cards within a shared catalog.

* Control the visibility of gift cards in quotes and orders. Only those gift card products that have been added to a shared catalog will be available for searches via the "Add by SKU" feature in quotes and orders.

### module-gift-card-staging
The Magento_GiftCardStaging module is a part of the staging functionality in Magento EE. It enables you to create new GiftCard Product updates or add new changes to the existing store updates. In other words, you can modify the GiftCard Product entity attributes in updates. These updates are shown on the content dashboard.
### module-gift-message
Magento\GiftMessage module allows to add a message to order or to each ordered item either on frontend or backend.
### module-gift-message-staging 
The Magento_GiftMessageStaging module is a part of the staging functionality in Magento EE. It extends the Magento_GiftMessage module functionality to be used in the Schedule Update form.
### module-gift-registry
Magento\GiftRegistry module that allows to create sets of gifts specified for specific holiday(Birthday, Wedding, etc).
It resembles wishlist, but there are differences. You can describe Gift Registry as a wishlist of products you would
like to share with other people so they could purchase anything from the list. Customer can even set some shipping
address to a gift registry, thus anyone who follows this list with a purchase would automatically have that shipping
address set by default during checkout. Customer can manage his gift registries in his profile. The gift registry can be
shared or stay private. Every gift registry has system attributes and can have custom attributes.
### module-gift-registry-sample-data
Magento_GiftRegistrySampleData module consists of installation scripts and fixtures.
### module-gift-wrapping
Magento\GiftWrapping module  provides functionality that allows customer to add gift wrapping to the items purchased
from the store as gifts and charge it individually. Magento\GiftWrapping module extends functionality of gift
messages by combining gift messages with gift wrapping functionality
### module-gift-wrapping-staging 
The Magento_GiftWrappingStaging module is a part of the staging functionality in Magento EE. It allows to stage value of 'Allow Gift Wrapping' flag and price of the wrapping for each product update.
### module-google-adwords
GoogleAdwords is a module designed for integration of Google Adwords service.

### module-google-analytics
Magento_GoogleAnalytics is a module for integration with Google Analytics service.

### module-google-optimizer
Magento_GoogleOptimizer module implements functionality of Google Experiment tool that is the part of Google Analytics functionality.

Google Experiment (on Google side) allows to make two variants of the same page and compare their popularity. 
From Magento side, code generated by Google should be saved and displayed on a particular page.
Google Experiment functionality is available on pages of products, categories and cms pages. 
This allows to save different codes for products and categories on different store views.
This functionality can be switched on and off on the configuration page (Stores -> Configuration -> General -> Google Api -> Google Analytics).
Also this functionality depends on Google Analytics module and configuration options.

### module-google-optimizer-staging 
The Magento_GoogleOptimizerStaging module is a part of the staging functionality in Magento EE. It enables you to stage values of the product metadata.

### module-google-tag-manager
Magento_GoogleTagManager is a module for integration with Google Tag Manager service.

### module-graph-ql
**GraphQl** provides the framework for the application to expose GraphQL compliant web services. It exposes an area for
GraphQL services and resolves request data based on the generated schema. It also maps this response to a JSON object 
for the client to read.

### module-grouped-import-export 
### module-grouped-product 
### module-grouped-product-graph-ql 
### module-grouped-product-sample-data 
### module-grouped-product-staging 
### module-grouped-requisition-list 
### module-grouped-shared-catalog 
### module-import-export 
### module-indexer 
### module-instant-purchase 
### module-integration 
### module-inventory 
### module-inventory-admin-ui 
### module-inventory-api 
### module-inventory-bundle-product 
### module-inventory-bundle-product-admin-ui 
### module-inventory-cache 
### module-inventory-catalog 
### module-inventory-catalog-admin-ui 
### module-inventory-catalog-api 
### module-inventory-catalog-search 
### module-inventory-configurable-product 
### module-inventory-configurable-product-admin-ui 
### module-inventory-configurable-product-indexer 
### module-inventory-configuration 
### module-inventory-configuration-api 
### module-inventory-distance-based-source-selection 
### module-inventory-distance-based-source-selection-admin-ui 
### module-inventory-distance-based-source-selection-api 
### module-inventory-elasticsearch 
### module-inventory-grouped-product 
### module-inventory-grouped-product-admin-ui 
### module-inventory-grouped-product-indexer 
### module-inventory-import-export 
### module-inventory-indexer 
### module-inventory-low-quantity-notification 
### module-inventory-low-quantity-notification-admin-ui 
### module-inventory-low-quantity-notification-api 
### module-inventory-multi-dimensional-indexer-api 
### module-inventory-product-alert 
### module-inventory-reservations 
### module-inventory-reservations-api 
### module-inventory-sales 
### module-inventory-sales-admin-ui 
### module-inventory-sales-api 
### module-inventory-sales-frontend-ui 
### module-inventory-setup-fixture-generator 
### module-inventory-shipping 
### module-inventory-shipping-admin-ui 
### module-inventory-source-deduction-api 
### module-inventory-source-selection 
### module-inventory-source-selection-api 
### module-invitation 
### module-layered-navigation 
### module-layered-navigation-staging 
### module-logging 
### module-marketplace 
### module-media-storage 
### module-message-queue 
### module-msrp 
### module-msrp-sample-data 
### module-msrp-staging 
### module-multiple-wishlist 
### module-multiple-wishlist-sample-data 
### module-multishipping 
### module-mysql-mq 
### module-negotiable-quote 
### module-negotiable-quote-shared-catalog 
### module-new-relic-reporting 
### module-newsletter 
### module-offline-payments 
### module-offline-shipping 
### module-offline-shipping-sample-data 
### module-page-cache 
### module-payment 
### module-payment-staging 
### module-paypal 
### module-paypal-on-boarding 
### module-persistent 
### module-persistent-history 
### module-price-permissions 
### module-product-alert 
### module-product-links-sample-data 
### module-product-video 
### module-product-video-staging 
### module-promotion-permissions 
### module-quick-order 
### module-quote 
### module-quote-analytics 
### module-quote-graph-ql 
### module-release-notification 
### module-reminder 
### module-reports 
### module-require-js 
### module-requisition-list 
### module-resource-connections 
### module-review 
### module-review-analytics 
### module-review-sample-data 
### module-review-staging 
### module-reward 
### module-reward-graph-ql 
### module-reward-staging 
### module-rma 
### module-rma-graph-ql 
### module-rma-staging 
### module-robots 
### module-rss 
### module-rule 
### module-sales 
### module-sales-analytics 
### module-sales-archive 
### module-sales-inventory 
### module-sales-rule 
### module-sales-rule-sample-data 
### module-sales-rule-staging 
### module-sales-sample-data 
### module-sales-sequence 
### module-sample-data 
### module-scalable-checkout 
### module-scalable-inventory 
### module-scalable-oms 
### module-scheduled-import-export 
### module-search 
### module-search-staging 
### module-security 
### module-send-friend 
### module-shared-catalog 
### module-shipping 
### module-signifyd 
### module-sitemap 
### module-staging 
### module-store 
### module-store-graph-ql 
### module-support 
### module-swagger 
### module-swagger-webapi 
### module-swagger-webapi-async 
### module-swatches 
### module-swatches-graph-ql 
### module-swatches-layered-navigation 
### module-swatches-sample-data
### module-target-rule 
### module-target-rule-sample-data 
### module-tax 
### module-tax-graph-ql 
### module-tax-import-export 
### module-tax-sample-data 
### module-theme 
### module-theme-sample-data 
### module-tinymce-3 
### module-tinymce-3-banner 
### module-translation 
### module-ui 
### module-ups 
### module-url-rewrite 
### module-url-rewrite-graph-ql 
### module-user 
### module-usps 
### module-variable 
### module-vault 
### module-version 
### module-versions-cms 
### module-visual-merchandiser 
### module-webapi 
### module-webapi-async 
### module-webapi-security 
### module-website-restriction 
### module-weee 
### module-weee-graph-ql 
### module-weee-staging 
### module-widget 
### module-widget-sample-data 
### module-wishlist 
### module-wishlist-analytics 
### module-wishlist-sample-data 
### module-worldpay 
### sample-data-media 
### theme-adminhtml-backend 
### theme-frontend-blank 
### theme-frontend-luma 
### zendframework1
