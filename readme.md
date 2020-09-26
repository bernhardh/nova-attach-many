# Nova Attach Many - Changes to Original

### Allow to use same table for multiple "flag" fields

Zum Beispiel:  `adresse` joint über Tabelle `adresse_2_art` mit der Tabelle `adresse_art`, wobei `adresse_art` aber `adresse_art_gruppe_id` in meherere Gruppen aufgeteilt ist. Im Model `\App\Models\Adresse` hat man dann mehrere `belongsToMany` Relations, wie zB.

- `paymentFlags`
- `kitchenFlags`
- ...

Dazu muss man in der Nova Resource folgendes machen:

```php
// app/Nova/Adresse
class Adresse extends Resource {

    /**
     * For AttachMany Fields
     * 
     * @var \string[][]
     */
    public static $attachManyGroups = [
        ["paymentFlags", "kitchenFlags"]
    ];
    
    public function fields() {
        return [
            AttachMany::make('Zahlart', 'paymentFlags', AdresseArt\ZahlungsArt::class),
            AttachMany::make('Küchenart', 'kitchenFlags', AdresseArt\KuechenArt::class),
            ...
        ];
    }
}
```


# Original Nova Attach Many

[![Latest Version on Github](https://img.shields.io/github/release/dillingham/nova-attach-many.svg?style=flat-square)](https://packagist.org/packages/dillingham/nova-attach-many)
[![Total Downloads](https://img.shields.io/packagist/dt/dillingham/nova-attach-many.svg?style=flat-square)](https://packagist.org/packages/dillingham/nova-attach-many) [![Twitter Follow](https://img.shields.io/twitter/follow/dillinghammm?color=%231da1f1&label=Twitter&logo=%231da1f1&logoColor=%231da1f1&style=flat-square)](https://twitter.com/im_brian_d)

Belongs To Many create & edit form UI for Nova. Enables attaching relationships easily and includes validation.

![attach-many](https://user-images.githubusercontent.com/29180903/52160651-be7fd580-2687-11e9-9ece-27332b3ce6bf.png)

### Installation

```bash
composer require dillingham/nova-attach-many
```

### Usage

```php
use NovaAttachMany\AttachMany;
```
```php
public function fields(Request $request)
{
    return [
        AttachMany::make('Permissions'),
    ];
}
```

### Validation

You can set min, max, size or custom rule objects

```php
->rules('min:5', 'max:10', 'size:10', new CustomRule)
```

<img src="https://user-images.githubusercontent.com/29180903/52160802-9ee9ac80-2689-11e9-9657-80e3c0d83b27.png" width="75%" />


### Options

Here are a few customization options

- `->showCounts()` Shows "selected/total"
- `->showPreview()` Shows only selected
- `->hideToolbar()` Removes search & select all
- `->height('500px')` Set custom height
- `->fullWidth()` Set to full width
- `->help('<b>Tip:</b> help text')` Set the help text

### All Options Demo
<img src="https://user-images.githubusercontent.com/29180903/53781117-6978ee80-3ed5-11e9-8da4-d2f2408f1ffb.png" width="75%"/>

### Relatable
The attachable resources will be filtered by relatableQuery()
So you can filter which resources are able to be attached

### Authorization
This field also respects policies: ie Role / Permission
- RolePolicy: attachAnyPermission($user, $role)
- RolePolicy: attachPermission($user, $role, $permission)
- PermissionPolicy: viewAny($user)

---

# Author

Hi 👋, Im Brian D. I created this Nova package [and others](https://novapackages.com/collaborators/dillingham)

Hope you find it useful. Feel free to reach out with feedback.

Follow me on twitter: [@im_brian_d](https://twitter.com/im_brian_d) 
