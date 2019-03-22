### composer
  Magento composer library helps to instantiate Composer application and run composer commands.
### ece-tools 
##### Magento Commerce (Cloud) Deployment Tools
ECE-Tools is a set of scripts and tools designed to manage and deploy Cloud projects. The Cloud tools package is compatible with Magento version 2.1.4 and later to provide a rich set of features you can use to manage your Magento Commerce project.
##### Useful Resources
- [Cloud DevDocs](https://devdocs.magento.com/guides/v2.2/cloud/bk-cloud.html)

### framework 
  contains only PHP code. These are libraries of code plus the application entry point that routes requests to modules (that in turn call the Framework libraries). For example, libraries in the Framework help implement a resource model (base classes and interfaces to inherit from) but not the resource models themselves. Certain libraries also support CSS rendering.
- [More details here](https://devdocs.magento.com/guides/v2.2/architecture/archi_perspectives/framework.html)
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
Magento_GroupedProduct module provides ability to offer several standalone products for sale as a group on the same Product Detail page.
It can offer variations of a product, or group them by season or theme to create a coordinated set.
Products can be purchased separately or as a set.
Each product purchased appears in the Shopping Cart as a separate item.
This module extends the existing functionality of Magento_Catalog module by adding new product type.

### module-grouped-product-graph-ql
**GroupedProductGraphQl** provides type and resolver information for the GraphQl module
to generate grouped product information.

### module-grouped-product-sample-data
Magento_GroupedProductSampleData module consists of installation scripts and fixtures.
### module-grouped-product-staging 
The Magento_GroupedProductStaging module is a part of the staging functionality in Magento EE. It enables you to stage products assigned to grouped product.

##### Implementation details

The Magento_GroupedProductStaging module extends functionality of the Magento_GroupedProduct to be used in staging. It adds Grouped Products field set to the Schedule Update form of a product.
### module-grouped-requisition-list
The Magento_GroupedRequisitionList module enables grouped products to be displayed in a requisition list in an B2B environment. This module extends Magento_RequisitionList and Magento_Grouped modules.

The Magento_GroupedRequisitionList module provides the following features:

* Display grouped products in a requisition list.

* Add grouped products to cart from a requisition list. 

* Disable ability to change quantity of grouped products in a requisition list. 
 
### module-grouped-shared-catalog
The Magento_GroupedSharedCatalog module enables grouped products to be added to a shared catalog in an B2B environment. This module extends Magento_SharedCatalog and Magento_Grouped modules.

The Magento_GroupedSharedCatalog module provides the following features:

* Display base and custom prices for grouped products within a shared catalog. There is no ability to edit the price of a grouped product.

* Control the visibility of grouped products in quotes and orders. Only those grouped products that have been added to a shared catalog will be available for searches via the "Add by SKU" feature in quotes and orders. 

### module-import-export
Magento_ImportExport module provides a framework and basic functionality for importing/exporting various entities in Magento.
It can be disabled and in such case all dependent import/export functionality (products, customers, orders etc.) will be disabled in Magento.

### module-indexer
Magento_Indexer module is a base of Magento Indexing functionality.
It allows:
 - read indexers configuration,
 - represent indexers in admin,
 - regenerate indexes by cron schedule,
 - regenerate indexes from console,
 - view and reset indexer state from console,
 - view and set indexer mode from console

There are 2 modes of the Indexers: "Update on save" and "Update by schedule".
Manual full reindex can be performed via console by running `php -f bin/magento indexer:reindex` console command.
### module-instant-purchase
Instant Purchase feature allows the Customer to place the order in seconds without going through full checkout. Once clicked, system places the order using default shipping and billing addresses and stored payment method. Order is placed and customer gets confirmation message in notification area.

Prerequisites to display the Instant Purchase button:
1. Instant purchase enabled for a store at `Store / Configurations / Sales / Sales / Instant Purchase`
2. Customer is logged in
3. Customer has default shipping and billing address defined
4. Customer has valid stored payment method with instant purchase support
### module-integration
**Integration** enables third-party services to call the Web API by using access tokens.
It provides an admin UI that enables manual creation of integrations. Extensions can also provide a configuration
file so that an integration can be automatically pre-configured. The module also contains the data
model for request and access token management.

### module-inventory 
The `Inventory` module is part of the new inventory infrastructure,
which replaces the legacy `CatalogInventory` module with new and expanded features and APIs for Inventory Management.  
 
The [Inventory Management overview](https://devdocs.magento.com/guides/v2.3/inventory/index.html)
describes the MSI (Multi-Source Inventory) project in more detail.

All Inventory Management modules follow the 
[Single Responsibility Principle](https://en.wikipedia.org/wiki/Single_responsibility_principle).
[Inventory management architecture](https://devdocs.magento.com/guides/v2.3/inventory/architecture.html) 
provides additional insight about the overall structure of these modules.

### module-inventory-admin-ui 
The `InventoryAdminUi` module extends the Magento Admin UI to add Inventory Management functionality.

### module-inventory-api 
The `InventoryApi` module provides Inventory Management service contracts. 

### module-inventory-bundle-product
The `InventoryBundleProduct` module integrates inventory management business logic into Magento's bundle product logic..

### module-inventory-bundle-product-admin-ui
The `InventoryBundleProductAdminUi`extends the Magento Admin UI to add MSI functionality.

### module-inventory-cache
The `InventoryCache` module integrates inventory management business logic into Magento's cache logic.

### module-inventory-catalog 
The `InventoryCatalog` module integrates inventory management business logic into Magento's catalog logic.

### module-inventory-catalog-admin-ui 
The `InventoryCatalogAdminUi` module extends the Magento Admin UI to add MSI functionality.

### module-inventory-catalog-api 
The `InventoryCatalogApi` module provides service contracts for default source and stock providers as well as bulk operations. 

### module-inventory-catalog-search 
The `InventoryCatalogSearch` module integrates inventory management business logic into Magento's search logic.

### module-inventory-configurable-product 
The `InventoryConfigurableProduct` module integrates inventory management business logic into Magento's configurable product logic.

### module-inventory-configurable-product-admin-ui 
The `InventoryConfigurableProductAdminUi`extends the Magento Admin UI to add inventory management functionality.

### module-inventory-configurable-product-indexer 
The `InventoryConfigurableProductIndexer` module integrates inventory management business logic into Magento's indexation logic for configurable products.

### module-inventory-configuration 
The `InventoryConfiguration` module implements logic for inventory management configuration.

### module-inventory-configuration-api 
The `InventoryConfigurationApi` module provides service contracts for inventory management configuration.

### module-inventory-distance-based-source-selection
The `InventoryDistanceBasedSourceSelection` module implements logic for distance based source selection

This module is part of the new inventory infrastructure. The
[Inventory Management overview](https://devdocs.magento.com/guides/v2.3/inventory/index.html)
describes the MSI (Multi-Source Inventory) project in more detail.

### module-inventory-distance-based-source-selection-admin-ui
The `InventoryDistanceBasedSourceSelectionAdminUi` module extends Magento's admin UI with source selection based on distance functionality.

### module-inventory-distance-based-source-selection-api
The `InventoryDistanceBasedSourceSelectionApi` module provides service contracts for distance based source selection algorithm. 

### module-inventory-elasticsearch 
The `InventoryElasticsearch` module provides elastic search support for Inventory Management.

### module-inventory-grouped-product 
The `InventoryGroupedProduct` module integrates inventory management business logic into Magento's grouped product logic.

### module-inventory-grouped-product-admin-ui
The `InventoryGroupedProductAdminUi` module extends Magento's admin UI with inventory management functionality.

This module is part of the new inventory infrastructure. The
[Inventory Management overview](https://devdocs.magento.com/guides/v2.3/inventory/index.html)
describes the MSI (Multi-Source Inventory) project in more detail.

### module-inventory-grouped-product-indexer 
The `InventoryGroupedProductIndexer` module integrates inventory management business logic into Magento's indexation logic for grouped products.

### module-inventory-import-export
The `InventoryImportExport` module provides compatibility between Magento's flat file import/export logic and Inventory Management.

### module-inventory-indexer
The `InventoryIndexer` module provides indexation logic for Inventory Management.

### module-inventory-low-quantity-notification 
The `InventoryLowQuantityNotification` module integrates Inventory Management business logic into Magento's low quantity notification logic.

### module-inventory-low-quantity-notification-admin-ui 
The `InventoryLowQuantityNotificationAdminUi` module extends Magento's admin UI with inventory management functionality.

### module-inventory-low-quantity-notification-api 
The `InventoryLowQuantityNotificationApi` module provides service contracts for managing Inventory Management notifications.

### module-inventory-multi-dimensional-indexer-api 
The `InventoryMultiDimensionalIndexerApi` module  provides functionality for creating and handling multi-dimension indexes.
The library introduces a set of extension points which split a monolithic index by the specified dimension (Scope), creating 
an independent index (i.e. dedicated MySQL table) per dimension. The library also provides a mechanism for resolving 
index names based on the provided scope. The multi-dimension indexes are introduced for the sake of data scalability
and the ability to reindex data in the scope of particular dimension only.

An aliasing mechanism guarantees zero downtime to make Front-End responsive while Full Reindex being processed.

### module-inventory-product-alert 
The `InventoryProductAlert` module integrates Inventory Management business logic into Magento's product alert logic.

### module-inventory-reservations
The `InventoryReservations` module provides logic for handling product reservations.

### module-inventory-reservations-api 
The `InventoryReservationsApi` module provides service contracts for Inventory Management reservations.

### module-inventory-sales
The `InventorySales` module integrates Inventory Management business logic into Magento's sales logic.

### module-inventory-sales-admin-ui
The `InventorySalesAdminUi` module extends Magento's Admin UI with Inventory Management functionality.

### module-inventory-sales-api
The `InventorySalesApi` module provides service contracts for inventory management.

### module-inventory-sales-frontend-ui
The `InventorySalesFrontendUi` module extends Magento's frontend UI with Inventory Management functionality.

### module-inventory-setup-fixture-generator
The `InventorySetupFixtureGenerator` module customizes the process of Inventory Data (Salable Quantity) Generation for [performance testing](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-perf-data.html).

### module-inventory-shipping
The `InventoryShipping` module integrates MSI business logic into Magento's shipping logic.

### module-inventory-shipping-admin-ui
The `InventoryShippingAdminUi` module extends Magento's Admin UI with Inventory Management functionality.

### module-inventory-source-deduction-api 
The `InventorySourceDeductionApi` module provides service contracts for managing source deductuions when products are sold.

### module-inventory-source-selection 
The `InventorySourceSelection` module provides source selection logic for Inventory Management.

### module-inventory-source-selection-api 
The `InventorySourceSelectionApi` module provides service contracts for source selection algorithms (SSA).

### module-invitation
The Magento_Invitation module enables invitation sending, referral tracking and generating invitation reports.

### module-layered-navigation 
Magento_LayeredNavigation module introduces Layered Navigation UI for Catalog (faceted search).
This module can be removed from Magento installation without impact on the application.

### module-layered-navigation-staging 
The Magento_LayeredNavigationStaging module is a part of the staging functionality in Magento EE.
It restricts functionality of the Magento_LayeredNavigationStaging module in the staging preview mode.

### module-logging 
The Logging module is used for logging actions done in the backend by administrators. Information such as time of action, type of action and administrator who performed the action is recorded.
By default all actions are recorded. Rules can be configured only to identify specific kinds of actions.

### module-marketplace 
The Magento_Marketplace module allows to display partners of Magento in the backend.

### module-media-storage 
The Magento_MediaStorage module implements functionality related with upload media files and synchronize it by database.

### module-message-queue 
**MessageQueue** provides support of Advanced Message Queuing Protocol

### module-msrp 
### module-msrp-sample-data 
Magento_MsrpSampleData module consists of installation scripts and fixtures.

### module-msrp-staging 
The Magento_MsrpStaging module is a part of the staging functionality in Magento EE. It enables you to stage the manufacturer's suggested retail price.

The Magento_MsrpStaging module extends the Magento_Msrp module to be used in staging. It adds the following fields in the Advice Pricing form:

- Manufacturer's Suggested Retail Price
- Display Actual Price

### module-multiple-wishlist
The Magento_MultipleWishlist module implements the multiple wishlists functionality.
These are lists of products from a store a customer would like to buy. Customers can save products to multiple wish lists and copy or move items from list to list.

### module-multiple-wishlist-sample-data 
Magento_MultipleWishlistSampleData module consists of installation scripts and fixtures.

### module-multishipping 
Magento\Multishipping module provides functionality that allows customer to request shipping to more than one address
using different carriers. The module provides alternative to standard checkout flow.

### module-mysql-mq 
**MysqlMq** provides message queue implementation based on MySQL.

### module-negotiable-quote 
The Magento_NegotiableQuote module allows a customer and a merchant (admin user) to negotiate product and/or shipping prices before the customer places an order. Its functionality is available for the company members only. 

Currently, B2B quoting is global--the price is given for the quote as a whole. Quoting per item is not supported. The quote lifecycle is managed via quote statuses. The quoting interface allows both a merchant and a customer to manage items in the quote (add, delete, change quantity) as well as make an offer (or request a quote) for items and/or for shipping. The negotiated price set in the negotiable quote is exactly the price that will be applied on a quote during checkout, order generation, and invoice generation. 

The module provides a set of configurations for the quoting feature, such as the ability to request a quote, configure the minimum quote amount, configure the default expiration period, configure attached files, and set email templates for quotes. The module provides web APIs and can be integrated with 3rd party solutions to manage negotiable quote in Magento.
 
The module heavily depends on the Quote and Magento_Company modules, which must be previously installed and enabled. 

Also, the module has dependency on the following Magento’s B2C modules: Tax module, Checkout module and Cart Pricing Rules module. 

When working with the SharedCatalog module, Negotiable Quote will be restricted to the products added to the shared catalog and custom prices set in the shared catalog. 

The module does not create any backward incompatible changes. Can be deactivated and uninstalled at any time.
 
### module-negotiable-quote-shared-catalog 
The Magento_NegotiableQuoteSharedCatalog module enables the NegotiableQuote module to interact with a SharedCatalog in an B2B environment. This module extends the Magento_NegotiableQuote module and Magento_SharedCatalog modules.

The Magento_NegotiableQuoteSharedCatalog module provides the following features:

* Remove items from a negotiable quote if corresponding products were removed from this company's shared catalog.
 
### module-new-relic-reporting
Module Magento\NewRelicReporting implements integration New Relic APM and New Relic Insights with Magento, giving 
real-time visibility into business and performance metrics for data-driven decision making. 

### module-newsletter 
Magento_Newsletter module allows clients to subscribe for information about new promotions and discounts and allows store administrators to send newsletters to clients subscribed for them.

### module-offline-payments 
The Magento_OfflinePayments module implements the payment methods which do not require interaction with a payment gateway (so called offline methods). These methods are the following:
*Bank transfer
*Cash on delivery
*Check / Money Order
*Purchase order

### module-offline-shipping 
The Magento_OfflineShipping module implements the shipping methods which do not involve a direct interaction with shipping carriers, so called offline shipping methods. Namely, the following:
*Free Shipping
*Flat Rate
*Table Rates
*Store Pickup

### module-offline-shipping-sample-data 
Magento_OfflineShippingSampleData module consists of installation scripts and fixtures.

### module-page-cache 
The PageCache module provides functionality of caching full pages content in Magento application. An administrator may switch between built-in caching and Varnish caching. Built-in caching is default and ready to use without the need of any external tools.
Requests and responses are managed by PageCache plugin. It loads data from cache and returns a response. If data is not present in cache, it passes the request to Magento and waits for the response. Response is then saved in cache.
Blocks can be set as private blocks by setting the property '_isScopePrivate' to true. These blocks contain personalized information and are not cached in the server. These blocks are being rendered using AJAX call after the page is loaded. Contents are cached in browser instead.
Blocks can also be set as non-cacheable by setting the 'cacheable' attribute in layout XML files. For example `<block class="Block\Class" name="blockname" cacheable="false" />`. Pages containing such blocks are not cached.

### module-payment 
The Magento_Payment module provides the abstraction level for all payment methods, and all logic that should be used when adding a new payment method. This logic includes configuration models, separate models for payment data verification and so on.
For example, Magento\Payment\Model\Method\AbstractMethod is an abstract model which should be extended by particular payment methods.

### module-payment-staging 
The Magento_PaymentStaging module is a part of the staging functionality in Magento EE. It extends the Magento_Payment module for the staging preview functionality.

### module-paypal
Module Magento\PayPal implements integration with the PayPal payment system. Namely, it enables the following payment methods:
*PayPal Express Checkout
*PayPal Payments Standard
*PayPal Payments Pro
*PayPal Credit
*PayFlow Payment Gateway

### module-paypal-on-boarding
Module Magento\PaypalOnBoarding gives an ability to run PayPal on-boarding flow from Magento PayPal Express Checkout configuration page so merchant can get API credentials configured automatically on merchants store without a need to provide those manually. 

### module-persistent 
Magento\Persistent module enables set customer a long-term cookie containing internal id (random hash - to exclude brute
force) of persistent session. Persistent session data is kept in DB - so it's not deleted in some days and is kept for
as much time as we need. DB session keeps customerId + some data from real customer session that we want to sync (e.g.
num items in shopping cart). For registered customer this info is synced to persistent session if choose "Remember me"
checkbox during first login.

### module-persistent-history 
Magento\PersistentHistory module extends functionality of Magento\Persistent by providing ability to keep track of
products added to  wishlist, recently ordered items, currently compared products, comparison history, recently viewed
products and customer group membership and segmentation.

### module-price-permissions 
Magento_PricePermissions module allows to restrict such admin rights as changing or reading product price, changing product status.

### module-product-alert 
The Magento_ProductAlert module enables product alerts, which allow customers to sign up for emails about product price or stock status change.

### module-product-links-sample-data 
Magento_ProductLinksSampleData module consists of installation scripts and fixtures.

### module-product-video
The Magento_ProductVideo module implements functionality related with linking video files from external resources to product.

### module-product-video-staging
The Magento_ProductVideoStaging module is a part of the staging functionality in Magento EE. It enables you to add or remove a video to a product update.

### module-promotion-permissions 
Magento\PromotionPermission module provides the possibility to an admin user to manage access of promotions and product
prices in the Admin Panel. An admin user can set the following access rights for promotions and product prices: edit,
read, without any permissions.

### module-quick-order 
The Magento_QuickOrder module allows customers to improve their user experience by creating a new order from a list of multiple SKUs.

Multiple items can be sent to the shopping cart from a CSV file, by copy-pasting multiple SKUs from another source, or by manually entering SKUs one-by-one into the Quick Order form. This feature is available for both logged-in users and guests.
 
### module-quote 
### module-quote-analytics 
The Magento_QuoteAnalytics module configures data definitions for a data collection related to the Quote module entities to be used in [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html).

### module-quote-graph-ql 
**QuoteGraphQl** provides type and resolver information for the GraphQl module
to generate quote (cart) information endpoints. Also provides endpoints for modifying a quote.

### module-release-notification 
The **Release Notification Module** serves to provide a notification delivery platform for displaying new features of a Magento installation or upgrade as well as any other required release notifications.
* Provides a method of notifying administrators of changes, features, and functionality being introduced in a Magento release.
* Displays a modal containing a high level overview of the features included in the installed or upgraded release of Magento upon the initial login of each administrator into the Admin Panel for a given Magento version.
* The modal is enabled with pagination functionality to allow for easy navigation between each modal page.
* Each modal page includes detailed information about a highlighted feature of the Magento release or other notification.
* Release Notification modal content is determined and provided by Magento Marketing.
Release notification content is maintained by Magento for each Magento version, edition, and locale. To retrieve the content, a response is returned from a request with the following parameters:
*  **version** = The Magento version that the client has installed (ex. 2.3.0).
*  **edition** = The Magento edition that the client has installed (ex. Community).
*  **locale** = The chosen locale of the admin user (ex. en_US).
The module will make three attempts to retrieve content for the parameters in the order listed:
1. Version/Edition/Locale
2. Version/Edition/en_US (default locale)
3. Version (default file for a Magento version)
If there is no content to be retrieved after these requests, the release notification modal will not be displayed to the admin user.

### module-reminder 
Magento_Reminder module provides functionality for sending reminder emails to customers according to pre-configured rules.

### module-reports 
Magento_Reports module provides ability to collect various reports such as:
 - products reports (bestsellers, low stock, most viewed, products ordered),
 - sales reports (orders, tax, invoiced, shipping, refunds, coupons, and PayPal settlement reports),
 - customer reports (new accounts, customer by order totals, customers by number of orders),
 - shopping cart reports (products in cart, abandoned carts)

### module-require-js 
The Magento\RequireJs module introduces support for RequireJs JavaScript library and provides infrastructure for other modules to have them declared related configuration for RequireJs library.

### module-requisition-list 
The Magento_RequisitionList module allows a customer to create multiple lists of frequently-purchased items and use those lists for order placement. This feature is available for both logged-in users and guests.
 
RequisitionList functionality is similiar to wish lists, but it has the following differences: 

* A requisition list is not purged after sending items to the shopping cart. It can be used to place multiple orders.
* The UI for requisition lists has been modified to a compact view in order to display large number of items. 

The merchant can configure maximum number of requisition lists per customer. 

### module-resource-connections 
Magento\ResourceConnections module adds a mechanism to segregate database connections between master and slave 
database servers based on the request type.

For each master database connection (except the indexer connection) that are configured in db/connection section 
of app/etc/env.php you can add one slave connection that can be configured in db/slave_connection.
Configuration format is the same as db/connection. Slave connection name must be the same as associated master 
connection name. To enable slave connections for specific resources create a slave connection configuration 
by adding slave_connection node as below:

```php
<?php
return array (
    //...
    'db' =>
        array (
            'connection' =>
                array (
                    'default' =>
                        array (
                            'host' => 'default-master-host',
                            'dbname' => 'magento',
                            'username' => 'magento',
                            'password' => 'magento',
                            'active' => '1',
                        ),
                ),
            'slave_connection' =>
                array (
                    'default' =>
                        array (
                            'host' => 'default-slave-host',
                            'dbname' => 'magento',
                            'username' => 'read_only',
                            'password' => 'password',
                            'active' => '1',
                ),
        ),
        'table_prefix' => '',
    ),
    //.......
```
To add slave connection for resources other than 'default' repeat the step and add to db/slave_connection 
new element with same name and slave configuration for specified resource. 
Config structure retains backward compatibility if module is turned off.

WARNING: 'indexer' connection is not designed to have slave configuration.

### module-review 
Magento_Review module functionality allows to write reviews for products.

### module-review-analytics
The Magento_ReviewAnalytics module configures data definitions for a data collection related to the Review module entities to be used in [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html).

### module-review-sample-data
Magento_ReviewSampleData module consists of installation scripts and fixtures.

### module-review-staging 
The Magento_ReviewStaging module is a part of the staging functionality in Magento EE. It displays the Product Reviews grid on the Schedule Update form.

## Implementation details
The Magento_ReviewStaging module extends the following Magento_Review module functionality to be used in staging mode:

- Adds Product Reviews grid on the Schedule Update form. 

NOTE You cannot create an update for a product review.

### module-reward 
Magento\Reward module allows an online merchant to implement unique programs designed to enhance user experience and increase
customer loyalty. Points are awarded based on a wide range of transaction and customer activities, with the ability for
the merchant to control point allotment, balance, and expiration. Customers can redeem points toward purchases based on
a conversion rate between points and currency that is set up by the merchant.

### module-reward-graph-ql
**RewardGraphQl** provides type information for the GraphQl module
to generate reward fields for customer information endpoints.

### module-reward-staging

The Magento_RewardStaging module is a part of the staging functionality in Magento EE. It enables you to create updates for the Add Reward Points attribute of Sales Rules.

The Magento_RewardStaging module extends the following Magento_Reward module functionality to be used in staging mode:

- Adds the ability to be staged for Add Reward Points field of Sales Rules.

### module-rma 
Rma module is responsible for processing Return Merchandise Approvals.

### module-rma-graph-ql 
**RmaGraphQl** provides type information for the GraphQl module
to generate rma fields for catalog and product information endpoints.

### module-rma-staging 
The Magento_RmaStaging module is a part of the staging functionality in Magento EE. It enables you to create updates for the parameters of the Autosettings field set of a product.

RMA stands for a return merchandise authorization.

The Magento_RmaStaging module extends the following Magento_Rma module functionality to be used in staging mode:
- Adds the Autosettings field set to the Schedule update form of a product.

### module-robots 
The Robots module provides the following functionalities: 
* contains a router to match application action class for requests to the `robots.txt` file;
* allows obtaining the content of the `robots.txt` file depending on the settings of the current website.

### module-rss 
Magento_Rss module is responsible for processing all RSS feeds of the application and allows to turn on/off RSS centrally.

### module-rule 
Magento_Rule module provides abstract implementation of rules and rule conditions that are extended by other modules, in particular by: Magento_SalesRule, Magento_CatalogRule, etc...

### module-sales 
Magento\Sales module is responsible for order processing and appearance in system,
Magento\Sales module manages next system entities and flows:
* order management;
* invoice management;
* shipment management (including tracks management);
* credit memos management;
Magento\Sales module is required for Magento\Checkout module to perform checkout operations.

### module-sales-analytics
The Magento_SalesAnalytics module configures data definitions for a data collection related to the Sales module entities to be used in [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html).

### module-sales-archive 
Magento\SalesArchive module responsible for creating logical partitions for storing previews of orders, invoices, credit memos, shipments.
Primary purpose of this module is to increase performance for read operation on orders (shipments, credit memos, shipments) grid.
### module-sales-inventory 
Magento_SalesInventory module allows retrieve and update stock attributes related to Magento_Sales, such as status and quantity.

### module-sales-rule 
SalesRule module is responsible for managing and processing Promotion Shopping Cart Rules.

### module-sales-rule-sample-data 
Magento_SalesRuleSampleData module consists of installation scripts and fixtures.

### module-sales-rule-staging
The Magento_SalesRuleStaging module is a part of the staging functionality in Magento EE. It enables you to create new sales rule updates or add new changes to the existing store updates. In other words, you can modify the sales rules in updates. These updates are shown on the content dashboard.

The Magento_SalesRuleStaging module changes the Cart Price Rules page and the sales rule related database tables to make them compatible with the Magento Staging Framework. 
The Magento_SalesRuleStaging module enables you to stage the following sales rule attributes:

- Rule Name
- Description
- Websites
- Customer Groups
- Priority
- Condition
- Action

This module depends on the Magento_SalesRule module and extends its functionality. It changes database structure of the Magento_SalesRule module and the way in which sales rules are managed.
 
### module-sales-sample-data 
Magento_SalesSampleData module consists of installation scripts and fixtures.

### module-sales-sequence 
Magento\SalesSequence module is responsible for sequences processing in Sales module,
Magento\SalesSequence module manages sequences for next system entities and flows:
* order;
* invoice;
* shipment;
* credit memos;
Magento\SalesSequence module is required for Magento\Sales module.

### module-sample-data 
Magento sample data includes a sample store, complete with more than 250 products (about 200 of them are configurable products), categories, promotional price rules, CMS pages, banners, and so on. Sample data uses the Luma theme on the storefront.

Installing sample data is optional.

Technically, sample data is a set of regular Magento modules, which can be deployed and installed together with the Magento instance, or later in the scope of upgrade.

### module-scalable-checkout 
Magento\ScalableCheckout module provides ability for system extension (Checkout can be configured to work with separate DataBase).
Extraction of Checkout tables to separate database will guarantee better scalability for Magento,
and will allow main server to be optimised for read operations which will reduce latency.

### module-scalable-inventory 
Magento\ScalableInventory module provides ability for system extension (CatalogInventory can be configured to work with separate quantity storage).
Extraction of quantity updates to separate storage will guarantee better scalability for Magento,
and will allow main server to be optimised for read operations which will reduce latency.

### module-scalable-oms 
Magento\ScalableOms (Order Management System) module provides ability for system extension
(Sales can be configured to work with separate database).
Extraction of Sales tables to separate database will guarantee better scalability for Magento,
and will allow main server to be optimised for read operations which will reduce latency.

### module-scheduled-import-export 
Magento_ScheduledImportExport functionality allows to simplify routine of importing and/or exporting data in the store by automating this process.
Admin user can create a rule for importing or exporting new data (which could be Products, Customers and Customer Addresses) and specify date and time of the operation.

### module-search 
Magento_Search module introduces basic search functionality and provides interfaces that allow to implement search for specific module.

### module-search-staging 
The Magento_SearchStaging module is a part of the staging functionality in Magento EE.
It restricts functionality of the Magento_SearchStaging module in the staging preview mode.

### module-security 
**Security** management module
_Main features:_
1. Added support for simultaneous admin user logins with ability to enable/disable the feature, review and disconnect the list of current logged in sessions
2. Added password complexity configuration
3. Enhanced security to prevent account takeover for sessions opened on public computers and similar:
    * Password confirmation for all critical flows (like password, email change)
    * Lockout of the account after a configurable amount of incorrect login/password entries
    * Password Change functionality is enhanced by email and/or ip address by frequency, number and requests per hour limitation
    * Change password link becomes invalid after the first use or after a configurable amount of time
    * Password/email change notifications are sent to both old and new email addresses
4. Fixed: the password is not being reset until the new password is submitted via the form available by a one time link sent to the email address

### module-send-friend 
The Magento_SendFriend implements the functionality behind the "Email to a Friend" link on a product page, which allows to share favorite products with others by clicking the link.

### module-shared-catalog 
The Magento_SharedCatalog modules defines the visibility of products as well as product prices in the catalog and in B2B quotes for different company accounts. 

The module allows a merchant to create multiple shared catalogs, link them to one or more company accounts, and set different product prices. Shared catalogs also control the visibility of products and categories for a company in the storefront. The shared catalog type (public or custom) defines the scope of products and prices available for guest users vs logged-in users. The system can have only one public and any number of custom shared catalogs.

The module relies on the CatalogPermissions module, in that the visibility of categories for a customer group is defined by category permissions for this customer group. Once a shared catalog is enabled in B2B features, the category permissions are automatically enabled. Adding a product or a category to a shared catalog enables appropriate category permissions for the customer groups linked to this shared catalog.

The module provides web APIs and can be integrated with third-party solutions to manage shared catalogs in Magento.
 
### module-shipping 
The Magento_Shipping module provides the abstract models and interfaces for a shipping carrier integration, including the web interface for the Shipment entity.
You need to extend these abstractions if you are adding new shipping carrier integration.

### module-signifyd
The Magento_Signifyd module provides integration with the [Signifyd](https://www.signifyd.com/) fraud protection system. The integration is based on the Signifyd API; see the [Signifyd API docs](https://www.signifyd.com/docs/api/#/introduction/) for technical details.

The module implementation allows to:

 - create a [Signifyd case](https://www.signifyd.com/docs/api/#/reference/cases) for a placed order
 - automatically receive a [Signifyd guarantee](https://www.signifyd.com/docs/api/#/reference/guarantees) for a created case
 - automatically cancel a guarantee when the order is canceled

### module-sitemap 
The Sitemap module allows managing the Magento application sitemap and
[sitemap.xml](http://en.wikipedia.org/wiki/Sitemaps) for searching engines.

### module-staging 
Magento_Staging module is used for setting up, previewing and managing future store updates.
Magento_Staging module have configured timeline view that simplify representation of updates. Configuration of
timeline is present in view/adminhtml/ui_component/staging_update_grid.xml file. Difference between simple grid is
in next components declaration:
 - listingToolbar
    * template - overloaded template to provide switcher between grid and timeline, legend for timeline.
    * updateTypes - path to status column that provide data for legend
 - columns
    * component - timeline component tht extends listing.
    * recordTmpl - overloaded template for timeline records.
    * detailsTmpl - template for tooltip that provide details about updates.
 - status column
    * component - extends selection column, sets class based on value.
    * updateTypesMap - array that contains bounded classes and values.
 - To avoid mixed content and to work properly, Staging Site Preview feature requires both Storefront and Admin area to be under the same protocol (http or https).

### module-store 
The Store module provides one of the basic and major features of a content management system for e-commerce web
sites by creating and managing a store for the customers to conduct online-shopping. Stores can be combined in groups,
and are linked to a specific website. All store related configurations (currency, locale, scope etc.), management and
storage maintenance are covered under this module.

### module-store-graph-ql 
**StoreGraphQl** provides type information for the GraphQl module
to generate store fields information endpoints.

### module-support 
Magento_Support module is used for generation of system reports, which provide detailed information about the system environment and Magento instance configuration.

### module-swagger 
The Magento_Swagger module provides access to a page generated using the swagger-ui package. The swagger-ui can be viewed
[on Github](https://github.com/swagger-api/swagger-ui). It accesses the JSON Schema describing Magento's REST APIs,
and displays it in a user-friendly, navigable format.

### module-swagger-webapi 
The Magento_SwaggerWebapi module provides the implementation of the REST Webapi module with Magento_Swagger.

### module-swagger-webapi-async 
The Magento_SwaggerWebapiAsync module provides the implementation of the Asynchronous WebApi module with Magento_Swagger.

### module-swatches 
Magento_Swatches module is replacing default product attributes text values with swatch images, for more convenient product displaying and selection.

### module-swatches-graph-ql 
**SwatchesGraphQl** provides type information for the GraphQl module
to generate swatches fields for catalog and product information endpoints.

### module-swatches-layered-navigation 
The **Magento_SwatchesLayeredNavigation** module enables LayeredNavigation functionality for Swatch attributes

### module-swatches-sample-data
Magento_SwatchesSampleData module consists of installation scripts.

### module-target-rule 
Magento_TargetRule module allows to configure the rules for showing related products.

### module-target-rule-sample-data 
Magento_TargetRuleSampleData module consists of installation scripts.

### module-tax 
The Magento_Tax module provides the calculations needed to compute the consumption tax on goods and services.

The Magento_Tax module includes the following:
* configuration of the tax rates and rules to apply
* configuration of tax classes that apply to:
** taxation on products
** taxation on shipping charges
** taxation on gift options (example: gift wrapping)
* specification whether the consumption tax is "sales & use" (typically product prices are loaded without any tax) or "VAT" (typically product prices are loaded including tax)
* specification of whether the tax total line can be toggled to display the tax details/subtotals
* display of prices (presented with tax, without tax, or both with and without)

The Magento_Tax module also handles special cases when computing tax, such as:
* determining the tax on an individual item (for example, one that is being returned) when the original tax has been computed on the entire shopping cart
** example country: United States
* being able to handle 2 or more tax rates that are applied separately (examples include a "luxury tax" on exclusive items)
* being able to handle a subsequent tax rate that is applied after a previous one is applied (a "tax on tax" situation, which recently was a part of Canadian tax law)

### module-tax-graph-ql 
**TaxGraphQl** provides type information for the GraphQl module
to generate tax fields for catalog and product information endpoints.

### module-tax-import-export 
### module-tax-sample-data 
Magento_TaxSampleData module consists of installation scripts.
### module-theme 
The Theme module contains common infrastructure that provides an ability to apply and use themes in Magento application.
### module-theme-sample-data 
Magento_ThemeSampleData module consists of installation scripts.
### module-tinymce-3 
We have updated the TinyMCE module to the latest available version, 4.6.4. TinyMCE v4.6.4 provides backwards-compatibility for modified editor modules to prevent the loss of functionality. The TinyMCE3 module is now deprecated and will be removed in a future release.
### module-tinymce-3-banner 
Tinymce3Banner module allows to update banner widget images on Wysiwyg. We have updated the TinyMCE module to the latest available version, 4.6.4. TinyMCE v4.6.4 provides backwards-compatibility for modified editor modules to prevent the loss of functionality. With TinyMCE4 you can update banner widget images using the WYSIWYG. The TinyMCE3 module is now deprecated and will be removed in a future release.
### module-translation
**Translation** enables localization of a store for multiple regions and markets.
Also provides the inline translation tool.

### module-ui 
The Magento\Ui module introduces a set of common UI components, which could be used and configured via layout XML files.

### module-ups 
The Magento_Ups module implements integration with the United Parcel Service shipping carrier.

### module-url-rewrite 
Magento_UrlRewrite module provides ability to customize website URLs by creating custom URL rewrite rules.

### module-url-rewrite-graph-ql 
**UrlRewriteGraphQl** provides type information for the GraphQl module
to generate url rewrites from entities that implement such rewrites,
like categories, products or cms and other 3rd party modules.

### module-user 
**User** enables admin users to manage and assign roles to administrators and other non-customer users,
reset user passwords, and invalidate access tokens.
Different roles can be assigned to different users to define their permissions.
For admin passwords, it enables setting lifetimes and locking them when expired or when a specified numbers of failures have occurred. It allows preventing password brute force attacks for system backend.

### module-usps 
The Magento_Usps module provides integration with the United States Postal Service shipping carrier.

### module-variable 
Magento\Variable Allows to create custom variables and then use them in email templates or in WYSIWYG editor for editing description of system entities.

### module-vault 
The Magento_Vault module implements the integration with the Vault payment gateway and makes the latter available as a payment method in Magento.

### module-version 
Magento\Version Allows to get Magento version and edition by HTTP GET request

### module-versions-cms 
The Versions CMS module adds a hierarchy feature for CMS pages.
The hierarchy feature organizes CMS pages as a hierarchy tree that allows parent/child relationships between pages.

### module-visual-merchandiser 
Create and merchandise categories quickly and easily with Visual Merchandiser for Magento.
Drag-and-drop products into position, or set up 'Smart Categories' based upon attributes.
Saves you hours merchandising your Magento store.

With Visual Merchandiser, products can be re-organised in seconds – visually.
You see the products in place, with images, just like the customer sees them.

### module-webapi 
**Webapi** provides the framework for the application to expose REST and SOAP web services. It exposes an area for REST
and another area for SOAP services and routes requests based on the Webapi configuration. It also handles
deserialization of requests and serialization of responses. 

### module-webapi-async 
**WebapiAsync** Extends Webapi extension and provide functional to process asynchronous requests. It handle asynchronous requests, schedule, publish and consum bulk operations from queue.

### module-webapi-security 
**WebapiSecurity** enables access management of some Web API resources.
If checkbox is enabled in backend through: Stores -> Configuration -> Services -> Magento Web API -> Web Api Security
then the security of all of the services outlined in app/code/Magento/WebapiSecurity/etc/di.xml would be loosened. You may modify this list to customize which services should follow this behavior.
By loosening the security, these services would allow access anonymously (by anyone).

### module-website-restriction 
**Website Restriction** enables administrators to restrict all access to the site or restrict site access
to only logged in customers. You might want to restrict all access when the site is closed for maintenance.
You might want to restrict site access to only logged in customers if the site is a B2B site or if there is
a private sale for registered customers.

### module-weee 
The Magento_Weee module enables the application of fees/fixed product taxes (FPT) on certain types of products, usually related to electronic devices and recycling.
Fixed product taxes can be used to setup a WEEE tax that is a fixed amount, rather than a percentage of the product price. FPT can be configured to be displayed at various places in Magento. Rules, amounts, and display options can be configured in the backend. This module extends the existing functionality of Magento_Tax.

The Magento_Wee module includes the following:

* ability to add different number of fixed product taxes to product. They are treated as a product attribute;
* configuration of where Weee appears (on category, product, sales, invoice, or credit memo pages) and whether FPT should be taxed;
* a new line item in the totals section.

### module-weee-graph-ql 
**WeeeGraphQl** provides type information for the GraphQl module
to generate wee tax fields for catalog and product information endpoints.

### module-weee-staging 
The Magento_WeeeStaging module is a part of the staging functionality in Magento EE. It enables you to stage a value of Fixed Product Tax.

The Magento_WeeeStaging module extends the following Magento_Weee module functionality to be used in staging:
- adds an opportunity to schedule a Fixed Product Tax type attribute using the Schedule Update form of a product

### module-widget 
The Widget module allows Magento application to be extended with custom widget blocks.
### module-widget-sample-data 
Magento_WidgetSampleData module consists of installation scripts and fixtures.

### module-wishlist 
The Magento_Wishlist implements the Wishlist functionality.
This allows customers to create a list of products that they can add to their shopping cart to be purchased at a later date, or share with friends.

### module-wishlist-analytics 
The Magento_WishlistAnalytics module configures data definitions for a data collection related to the Wishlist module entities to be used in [Advanced Reporting](http://devdocs.magento.com/guides/v2.2/advanced-reporting/modules.html).

### module-wishlist-sample-data 
Magento_WishlistSampleData module consists of installation scripts and fixtures.

### module-worldpay 
The Magento_Worldpay module implements the integration with the Worldpay payment gateway and makes the latter available as a payment method in Magento.

### sample-data-media 
Sample Media Data...

### theme-adminhtml-backend 
Magento 2 backend theme

### theme-frontend-blank
Magento Blank theme

### theme-frontend-luma 
Magento Luma child of blank

### zendframework1
Contains Zend Framework 1 plus performance improvements and bug fixes.
