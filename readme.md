# Send Welcome Email Notification with Event and Listener

## Step 1

Create `SendWelcomeEmailNotification` notification

```
php artisan make:notification SendWelcomeEmailNotification
```

## Step 2

Create `SendWelcomeEmail` listener on user registration

```
php artisan make:listener SendWelcomeEmail --event=Illuminate\\Auth\\Events\\Registered
```

## Step 3

Open up `App\Listeners\SenWelcomeEmail.php`, add the following lines:

```php
$event->user->notify(
    new SendWelcomeEmailNotification()
);
```

## Step 4

Then register `App\Listeners\SenWelcomeEmail` to  `Illuminate\Auth\Events\Registered` in `app\Providers\EventServiceProvider.php`.

```php
protected $listen = [
    'Illuminate\Auth\Events\Registered' => [
        'App\Listeners\SendWelcomeEmail',
    ],
];
```

## Step 5

Please ensured to setup your database and emails connection, and migrate the existing migration scripts.

```
php artisan migrate
```

## Step 6

Then you're ready to register. You should receive email once registered.