# PHP Didit

PHP SDK for Didit's identity verification (KYC) and authentication (CIAM) solutions.

## Features

- Verification
- Auth (coming soon)
- Data (coming soon)

## Installation

Install the package via composer:

```bash
composer require alexstewartja/php-didit
```

## Usage

### Get Access Token

Supply the Client ID and Client Secret of your application from the Didit console:

```php
$client_id = 'your-client-id';
$client_secret = 'your-client-secret';

$token_info = Didit::getAccessToken($client_id, $client_secret);
$access_token = $token_info->getAccessToken();
```

### Create a Verification Session

After obtaining a valid client access token, create a new verification session:

```php
$access_token = 'your-access-token';
$vendor_data = 'user-unique-id';
$callback = 'https://verify.didit.me/';
$features = VerificationFeatures::OCR_FACE;

$session = Didit::createVerificationSession($access_token, $vendor_data, $callback);
$session_id = $session->getSessionId();
$session_url = $session->getSessionUrl();
```

### Retrieve a Verification Session

Retrieve the results of a verification session:

```php
$access_token = 'your-access-token';
$session_id = 'session-id';

$session = Didit::getVerificationSession($access_token, $session_id);
```

### Update a Verification Session Status

Approve or decline a verification:

```php
$access_token = 'your-access-token';
$session_id = 'session-id';
$new_status = VerificationStatus::DECLINED;
$comment = 'Optional comment for review';

$declined = Didit::updateVerificationSessionStatus($access_token, $session_id, $new_status, $comment);
```

### Generate a Verification PDF Report

Generate a PDF for sessions:

```php
$access_token = 'your-access-token';
$session_id = 'session-id';
$save_to = './session_pdf_downloads/session.pdf';

$generated = Didit::generateVerificationSessionPdf($access_token, $session_id, $save_to);
```

## Testing

1. Copy credentials template:
   ```bash
   cp tests/assets/credentials.json.example tests/assets/credentials.json
   ```
2. Add your Client ID and Client Secret to `tests/assets/credentials.json`
3. Run tests:
   ```bash
   composer test
   ```

## Project Structure

- `src/` - Source code
- `tests/` - Test files
- `composer.json` - Dependencies and package configuration
- `CHANGELOG.md` - Version history
- `CONTRIBUTING.md` - Contribution guidelines
- `LICENSE.md` - License information
- `README.md` - Documentation 