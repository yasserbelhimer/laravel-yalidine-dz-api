# laravel-yalidine-dz-api
Simple laravel package to use Yalidine dz API
## Installation, and Usage Instructions

This package allows you to consume Yalidine dz Api using laravel.

```cli
composer require yasserbelhimer/laravel-yalidine-dz-api
```
First at all generate your api and token in yalidine website https://www.yalidine.com/

Set  API ID and API TOKEN in the .env  
```env
YALIDINE_API_ID= your yalidine api id
YALIDINE_API_TOKEN= your yalidine api token
```
Once installed you can do stuff like this:

## To know more about arguments and parametres check yalidine API documentation.

## Get your parcels:

To get all your parcels pass an empty array to getParcels([]) function.
```php
    $parcels = Yalidine::getParcels([]);
```

To get some specific parcels pass an array of tracking parcels getParcels($trackings) function.
```php
    $trackings = ['YAL-PAR1','YAL-PAR2'....]; // list of your parcels tracking 
    $parcels = Yalidine::getParcels($trackings);
```

## Create one or many new parcels:

To create new parcels pass an array of parcels to createParcels($parcels) function.
```php
    $parcels = array( // the array that contains all the parcels
        array ( // first parcel
            "order_id"=>"MyFirstOrder",
            "firstname"=>"Brahim",
            "familyname"=>"Mohamed",
            "contact_phone"=>"0123456789,",
            "address"=>"Cité Kaidi",
            "to_commune_name"=>"Bordj El Kiffan",
            "to_wilaya_name"=>"Alger",
            "product_list"=>"Presse à café",
            "price"=>3000,
            "freeshipping"=> true,
            "is_stopdesk"=> false,
            "has_exchange"=> 0,
            "product_to_collect" => null
        ),
        array ( // second parcel
            "order_id" =>"MySecondOrder",
            "firstname"=>"رفيدة",
            "familyname"=>"بن مهيدي",
            "contact_phone"=>"0123456789",
            "address"=>"حي الياسمين",
            "to_commune_name"=>"Ouled Fayet",
            "to_wilaya_name"=>"Alger",
            "product_list"=>"كتب الطبخ",
            "price"=>2400,
            "freeshipping"=>0,
            "is_stopdesk"=>0,
            "has_exchange"=> false,
        ),
        array ( // third parcel
            ...
        ),
        array( // etc
            ...
        )
    );
    $response = Yalidine::createParcels($parcels );
```
This function will return an array of object:
```json
    {
    "MyFirstOrder": {
        "success": true,
        "order_id": "MyFirstOrder",
        "tracking": "yal-12345A",
        "import_id": 234
    },
    "MySecondOrder": {
        "success": true,
        "order_id": "MySecondOrder",
        "tracking": "yal-67891B",
        "import_id": 234
    }
}
```

## Delete one or many parcels

To delete parcels pass an array of tracking parcels to deleteParcels($trackings) function.
```php
    $trackings = ['YAL-PAR1','YAL-PAR2'....]; // list of your parcels tracking 
    $deliveryFees = Yalidine::deleteParcels($trackings);
```

## Get the delivery fees
```php
    $deliveryFees = Yalidine::getDeliveryFees();
```
