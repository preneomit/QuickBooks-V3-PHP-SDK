# QuickBooks V3 PHP SDK - Codebase Index

## Overview
The QuickBooks V3 PHP SDK is a PHP client library for connecting to the QuickBooks Online V3 REST API. This is a non-official fork maintained by preneomit.

**License:** Apache-2.0  
**PHP Version:** >=7.2.5  
**Main Namespace:** `QuickBooksOnline\API\`

## Project Structure

### Root Files
- `README.md` - Project documentation and links
- `composer.json` - Composer dependencies and autoloading configuration
- `composer.lock` - Locked dependency versions
- `phpunit.xml` - PHPUnit testing configuration
- `.travis.yml` - Travis CI continuous integration configuration
- `bootstrap.php` - Application bootstrap file
- `LICENSE` - Apache 2.0 license

### Dependencies
**Required:**
- PHP >=7.2.5
- ext-mbstring
- ext-dom
- guzzlehttp/guzzle ^7.9

**Development:**
- phpunit/phpunit ^5.0 || ^6.0 || ^7.0 || ^8
- php-mock/php-mock-phpunit ^2.6
- php-mock/php-mock ^2.3

**Optional:**
- ext-curl - For cURL HTTP requests
- guzzlehttp/guzzle - For Guzzle HTTP requests

---

## Core Components

### src/Core/
**Core framework components**

#### Core Files
- `ServiceContext.php` - Main service context class containing settings for REST calls, authentication, and configuration
- `CoreHelper.php` - Helper functions for core operations
- `CoreConstants.php` - Constants used throughout the SDK

#### Subdirectories

**Core/Configuration/**
- Configuration management classes

**Core/Http/**
- HTTP communication layer

**Core/HttpClients/**
- HTTP client implementations (cURL, Guzzle)

**Core/OAuth/**
- OAuth authentication layer
  - `OAuth1/` - OAuth 1.0a authentication
  - `OAuth2/` - OAuth 2.0 authentication
    - `OAuth2AccessToken.php` - OAuth 2.0 access token management
    - `OAuth2LoginHelper.php` - OAuth 2.0 login helper for token operations
    - `certs/` - SSL certificates for OAuth 2.0

---

## Data Services

### src/DataService/
**Main data service for CRUD operations**

- `DataService.php` - Primary service class for Create, Read, Update, Delete (CRUD) operations on QBO entities
- `Batch.php` - Batch operation support for multiple requests
- `IntuitBatchResponse.php` - Response handler for batch operations
- `IntuitCDCResponse.php` - Change Data Capture response handling
- `IntuitRecurringTransactionResponse.php` - Recurring transaction response handling
- `IntuitResponseStatus.php` - Response status management
- `RecurringTransactionAdapter.php` - Adapter for recurring transactions

**Key Methods in DataService:**
- `Configure($settings)` - Static factory method to configure from array or file
- `Add($entity)` - Create new entity
- `Update($entity)` - Update existing entity
- `Delete($entity)` - Delete entity
- `Void($entity)` - Void transaction
- `FindById($entity)` - Find entity by ID
- `Query($queryString)` - Execute query
- `Upload($imgBits, $fileName, $mimeType, $objAttachable)` - Upload attachments
- `DownloadPDF($entity, $dir)` - Download PDF for entities
- `SendEmail($entity)` - Send email notifications

---

## Data Models

### src/Data/
**IPP (Intuit Platform Protocol) data models**

Contains 200+ PHP classes representing QuickBooks entities. Key entities include:

#### Financial Entities
- `IPPAccount.php` - Chart of accounts
- `IPPBill.php` - Bills
- `IPPBillPayment.php` - Bill payments
- `IPPCheckPurchase.php` - Check purchases
- `IPPCreditCardPurchase.php` - Credit card purchases
- `IPPDeposit.php` - Deposits
- `IPPInvoice.php` - Invoices
- `IPPCreditMemo.php` - Credit memos
- `IPPPayment.php` - Payments
- `IPPPurchaseOrder.php` - Purchase orders
- `IPPEstimate.php` - Estimates
- `IPPSalesReceipt.php` - Sales receipts
- `IPPJournalEntry.php` - Journal entries

#### Customer/Vendor Entities
- `IPPCustomer.php` - Customers
- `IPPCustomerType.php` - Customer types
- `IPPEmployee.php` - Employees
- `IPPPurchase.php` - Purchases
- `IPPVendor.php` - Vendors (implied)

#### Item/Product Entities
- `IPPItem.php` - Products and services
- `IPPItemGroupDetail.php` - Item groups
- `IPPInventoryAdjustment.php` - Inventory adjustments
- `IPPFixedAsset.php` - Fixed assets

#### Transaction Details
- `IPPLine.php` - Transaction line items
- `IPPLineDetailTypeEnum.php` - Line detail type enums
- `IPPDiscountLineDetail.php` - Discount line details
- `IPPItemLineDetail.php` - Item line details

#### Configuration
- `IPPCompanyInfo.php` - Company information
- `IPPPreferences.php` - Company preferences
- `IPPTaxService.php` - Tax service configuration
- `IPPCurrency.php` - Currency settings

#### Attachments
- `IPPAttachable.php` - File attachments
- `IPPAttachableResponse.php` - Attachment responses

#### Enums and Types
- `IPPAccountTypeEnum.php` - Account type enumerations
- `IPPPostingTypeEnum.php` - Posting type enumerations
- `IPPPaymentStatusEnum.php` - Payment status enumerations
- `IPPEntityStatusEnum.php` - Entity status enumerations

#### Batch Operations
- `IPPBatchItemRequest.php` - Batch request items
- `IPPBatchItemResponse.php` - Batch response items
- `IPPIntuitBatchRequest.php` - Batch request wrapper

#### CDC Support
- `IPPCDCQuery.php` - Change Data Capture query
- `IPPCDCResponse.php` - Change Data Capture response

#### Core Classes
- `IPPIntuitEntity.php` - Base entity class
- `IPPIntuitObject.php` - Base object class
- `IPPIntuitResponse.php` - Base response class
- `IPPid.php` - Entity ID representation
- `IPPMoney.php` - Monetary amounts
- `IPPDateMacro.php` - Date macros for queries

---

## Security & Authentication

### src/Security/
**Authentication and security components**

- `OAuthRequestValidator.php` - OAuth 1.0a request validator
- `RequestValidator.php` - Base request validator interface

### src/Core/OAuth/
**OAuth authentication implementation**

**OAuth1/**
- OAuth 1.0a authentication (legacy)

**OAuth2/**
- `OAuth2AccessToken.php` - OAuth 2.0 access token management
- `OAuth2LoginHelper.php` - OAuth 2.0 login helper
  - Generate OAuth authorization URL
  - Exchange authorization code for tokens
  - Refresh access tokens
  - Revoke tokens
- `certs/` - SSL certificates for token validation

---

## Platform Services

### src/PlatformService/
- `PlatformService.php` - Platform-level services for company info and app tokens

---

## Report Services

### src/ReportService/
**QuickBooks reporting functionality**

- `ReportService.php` - Main report service for generating financial reports
- `ReportName.php` - Report name constants and types

---

## Webhooks Services

### src/WebhooksService/
**Webhook event handling**

- `WebhooksService.php` - Main webhook service for processing webhook notifications
- `WebhooksEvent.php` - Webhook event data structure
- `WebhooksCloudEvent.php` - Cloud event format support
- `DataChangeEvent.php` - Data change event handling
- `Entity.php` - Entity change representation
- `EventNotification.php` - Event notification structure
- `TokenVerifier.php` - Webhook signature verification
- `Readme.txt` - Webhooks documentation

---

## Utilities

### src/Utility/
**Helper utilities and tools**

- `ArrayUtil.php` - Array manipulation utilities
- `ClassNamingUtil.php` - Class naming conventions
- `DomainEntityBuilder.php` - Domain entity builder
- `IntuitErrorHandler.php` - Error handling utilities
- `JsonValidator.php` - JSON validation
- `MetadataExtractor.php` - Metadata extraction
- `ReflectionUtil.php` - PHP reflection utilities
- `UtilityConstants.php` - Utility constants

**Utility/Configuration/**
- Configuration utilities

---

## HTTP Client Layer

### src/Core/HttpClients/
**HTTP client abstraction layer**

- Client factory and implementations
- Request/response handling
- Error handling and fault management
- Support for both cURL and Guzzle HTTP clients

### src/Core/Http/
**HTTP protocol implementation**

- Serialization formats (XML, JSON)
- Compression handling
- Request/response processing

---

## Exception Handling

### src/Exception/
**Exception hierarchy**

- `IdsException.php` - Base IDS exception
- `IdsError.php` - Error representation
- `IdsExceptionManager.php` - Exception management
- `SdkException.php` - SDK-specific exceptions
- `SecurityException.php` - Security-related exceptions
- `ServiceException.php` - Service-level exceptions
- `ValidationException.php` - Validation exceptions

**Exception/SdkExceptions/**
- Specific SDK exception implementations

---

## Diagnostics & Logging

### src/Diagnostics/
**Logging and diagnostics**

- `Logger.php` - Main logger interface
- `LoggerBase.php` - Base logger implementation
- `LogRequestsToDisk.php` - File-based logging
- `TraceLevel.php` - Trace level constants
- `TraceLogger.php` - Trace logging
- `ContentWriter.php` - Content writing utilities

**Logging Features:**
- Request/response logging to disk
- Configurable log levels
- Custom log directory support
- OAuth call logging with debug mode

---

## Query & Filtering

### src/QueryFilter/
**Query construction and filtering**

- `QueryMessage.php` - Query message handling
- `README.txt` - Query documentation

**Query Capabilities:**
- SQL-like query language
- Entity filtering
- Complex query construction
- Batch query support

---

## Interceptors & Middleware

### src/Interceptors/
**Request/response interceptors**

- Request interceptors
- Response interceptors
- Middleware support

---

## Retry Logic

### src/Retry/
**Retry mechanism for failed requests**

- Automatic retry on transient failures
- Configurable retry policies
- Backoff strategies

---

## Facades

### src/Facades/
**Facade patterns for simplified API access**

- Simplified interfaces to complex subsystems
- Helper facades for common operations

---

## XSD2PHP

### src/XSD2PHP/
**XSD to PHP converter tool**

- **buildDocs.sh** - Documentation build script
- **src/** - Source code for XSD converter
- **lib/** - Library files
- **resources/** - Resource files
- **test/** - Test files
- **docs/** - Documentation
- **website/** - Website files
- **README** - Tool documentation
- **LICENSE** - License for the tool

---

## Testing

### test/
**PHPUnit test suite**

- `DependencyTest.test.php` - Dependency testing
- `ServiceContextTest.test.php` - Service context testing
- `test/Core/` - Core component tests
  - `test/Core/HttpClients/` - HTTP client tests
  - `test/Core/OAuth/` - OAuth authentication tests

### src/test/
**Additional source tests**

### src/Utility.Test/
**Utility component tests**

---

## Samples

### src/_Samples/
**Sample code and examples**

- Usage examples for various SDK features
- Authentication examples
- CRUD operation examples
- Query examples

---

## Configuration Files

### src/config.php
**SDK configuration file**

### src/sdk.config
**Default SDK configuration**

### src/xsd2php.php
**XSD to PHP conversion script**

---

## Documentation

### docs/
**Generated documentation**

- `index.html` - Documentation index
- `overview.html` - SDK overview
- `quickstart.html` - Quick start guide
- `authorization.html` - Authorization documentation
- `configuration.html` - Configuration guide
- `handle-error.html` - Error handling guide
- `genindex.html` - Generated index
- `search.html` - Search interface
- `searchindex.js` - Search index
- `.nojekyll` - GitHub Pages configuration
- `docs/_images/` - Documentation images
- `docs/_sources/` - Source documentation
- `docs/_static/` - Static documentation assets

---

## Views

### views/
**UI assets**

- `RateSDK.png` - SDK rating image
- `Thumbup.png` - Thumbs up image
- `Thumbdown.png` - Thumbs down image

---

## Key Features

### Authentication
- OAuth 1.0a support (legacy)
- OAuth 2.0 support (recommended)
- Token refresh and management
- Multiple authentication methods

### Data Operations
- CRUD operations on all QBO entities
- Batch operations for efficiency
- Query support with SQL-like syntax
- Change Data Capture (CDC) support
- Recurring transactions

### Reporting
- Financial reports generation
- Custom report parameters
- Export capabilities

### Webhooks
- Webhook event handling
- Signature verification
- Data change notifications
- Cloud events support

### Error Handling
- Comprehensive exception hierarchy
- Detailed error messages
- Fault handling
- Logging and diagnostics

### HTTP Client Support
- cURL client (default)
- Guzzle HTTP client
- Configurable client selection
- Request/response logging

### Serialization
- XML serialization
- JSON serialization (limited support)
- Object mapping
- Type conversion

---

## Configuration Methods

### 1. Configuration from Array
```php
$settings = [
    'auth_mode' => 'oauth2',
    'ClientID' => 'your_client_id',
    'ClientSecret' => 'your_client_secret',
    'accessTokenKey' => 'access_token',
    'refreshTokenKey' => 'refresh_token',
    'QBORealmID' => 'realm_id',
    'baseUrl' => 'production'
];
$dataService = DataService::Configure($settings);
```

### 2. Configuration from File
```php
$dataService = DataService::Configure('path/to/config/file');
```

---

## Common Use Cases

### 1. Create Entity
```php
$invoice = new IPPInvoice();
// Set invoice properties
$resultingInvoice = $dataService->Add($invoice);
```

### 2. Read Entity
```php
$invoice = $dataService->FindById("invoice", $invoiceId);
```

### 3. Update Entity
```php
$updatedInvoice = $dataService->Update($invoice);
```

### 4. Delete Entity
```php
$dataService->Delete($invoice);
```

### 5. Query Entities
```php
$invoices = $dataService->Query("SELECT * FROM Invoice");
```

### 6. Generate Report
```php
$reportService = new ReportService($serviceContext);
$report = $reportService->executeReport("ProfitAndLoss");
```

---

## API Versioning

- Current API version: v3
- Minor version support: Configurable via `setMinorVersion()`
- Base URL support: Production and Sandbox environments

---

## Best Practices

1. **Use OAuth 2.0** for new integrations (OAuth 1.0a is deprecated)
2. **Enable logging** during development for debugging
3. **Handle exceptions** properly using the exception hierarchy
4. **Use batch operations** for multiple entity operations
5. **Implement token refresh** for OAuth 2.0 access tokens
6. **Validate input data** before creating/updating entities
7. **Use proper error handling** with `throwExceptionOnError()`
8. **Configure appropriate timeout settings** for production use

---

## Maintenance & Support

- **Documentation:** https://intuit.github.io/QuickBooks-V3-PHP-SDK/
- **Wiki:** https://github.com/intuit/QuickBooks-V3-PHP-SDK/wiki
- **Examples:** https://github.com/IntuitDeveloper/SampleApp-CRUD-PHP
- **CI/CD:** Travis CI integration
- **Packagist:** https://packagist.org/packages/quickbooks/v3-php-sdk

---

## Notes

- This is a fork of the official Intuit QuickBooks V3 PHP SDK
- Maintained by preneomit
- Non-official version
- PHP 7.2.5+ required
- PSR-4 autoloading support
- Comprehensive test suite included