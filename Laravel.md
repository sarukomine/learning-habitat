
### Contents

- [New Collection Helper](#new-collection-helper)
- [8 Images of Laravel Eloquent Relationships](#8-images-of-laravel-eloquent-relationships)
- [Enhancement of Password Attribute in Laravel Eloquent](#enhancement-of-password-attribute-in-laravel-eloquent)

---

### New Collection Helper

```php
use Illuminate\Support\Collection;

function collect($value = null): Collection
{
    return Collection::make($value)->map(function ($row) {
        return is_array($row) ? collect($row) : $row;
    })
}
```

---

### 8 Images of Laravel Eloquent Relationships

one-to-one

![one-to-one](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/one-to-one.png?raw=true)

one-to-many

![one-to-many](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/one-to-many.png?raw=true)

many-to-many

![many-to-many](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/many-to-many.png?raw=true)

has-one-through

![has-one-through](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/has-one-through.png?raw=true)

has-many-through

![has-many-through](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/has-many-through.png?raw=true)

one-to-one (polymorphism)

![one-to-one-polymorphism](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/one-to-one-polymorphism.png?raw=true)

one-to-many (polymorphism)

![one-to-many-polymorphism](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/one-to-many-polymorphism.png?raw=true)

many-to-many (polymorphism)

![many-to-many-polymorphism](https://github.com/sarukomine/learning-habitat/blob/main/assets/laravel/eloquent/many-to-many-polymorphism.png?raw=true)

---

### Enhancement of Password Attribute in Laravel Eloquent

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Casts\Attribute;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;

class User extends Authenticatable
{
    // ...

    /**
     * Set the user's password with the hashed value.
     *
     * @return \Illuminate\Database\Eloquent\Casts\Attribute
     */
    protected function password(): Attribute
    {
        return Attribute::make(
            set: fn ($value) => $this->hashPasswordIfNecessary($value),
        );
    }

    /**
     * Hash the password if necessary.
     *
     * @param  string  $value
     * @return string
     */
    protected function hashPasswordIfNecessary($value): string
    {
        return strlen($value) === 60 && Str::startsWith($value, '$2y$')
            ? $value
            : Hash::make($value);
    }
}
```
