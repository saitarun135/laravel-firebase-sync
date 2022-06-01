# Laravel Firebase Sync
## Synchronize your Eloquent models with the [Firebase Realtime Database](https://firebase.google.com/docs/database/)


## Contents

- [Installation](#installation)
- [Usage](#usage)

<a name="installation" />

## Installation
laravel-version is **5**

In order to add Laravel Firebase Sync to your project, just add

    "repositories": [
        {
            "type":"package",
            "package": {
              "name": "saitarun135/laravel-firebase-sync",
              "version":"master",
              "source": {
                  "url": "https://github.com/saitarun135/laravel-firebase-sync",
                  "type": "git",
                  "reference":"master"
                }
            }
        }
    ],
    "require": {
        "saitarun135/laravel-firebase-sync": "master"
    },

to your composer.json. Then run `composer install` or `composer update` or `composer update --prefer-source`.

<a name="usage" />

## Usage
Note:- it will not support `insert` for example **Model::insert([$data])**
```
$data = $request->all();
Model::create([$data]);
```
### Configuration

This package requires you to add the following section to your `config/services.php` file:

```php
'firebase' => [
    'api_key' => 'API_KEY', // Only used for JS integration
    'auth_domain' => 'AUTH_DOMAIN', // Only used for JS integration
    'database_url' => 'https://your-database-at.firebaseio.com',
    'secret' => 'DATABASE_SECRET',
    'storage_bucket' => 'STORAGE_BUCKET', // Only used for JS integration
]
```

**Note**: This package only requires the configuration keys `database_url` and `secret`. The other keys are only necessary if you want to also use the firebase JS API. 

### Synchronizing models

To synchronize your Eloquent models with the Firebase realtime database, simply let the models that you want to synchronize with Firebase use the `Mpociot\Firebase\SyncsWithFirebase` trait.

```php
use Mpociot\Firebase\SyncsWithFirebase;

class User extends Model {

    use SyncsWithFirebase;

}
```

The data that will be synchronized is the array representation of your model. That means that you can modify the data using the existing Eloquent model attributes like `visible`, `hidden` or `appends`.

If you need more control over the data that gets synchronized with Firebase, you can override the `getFirebaseSyncData` of the `SyncsWithFirebase` trait and let it return the array data you want to send to Firebase.


<a name="license" />

