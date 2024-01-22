<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

You may also try the [Laravel Bootcamp](https://bootcamp.laravel.com), where you will be guided through building a modern Laravel application from scratch.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 2000 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the [Laravel Partners program](https://partners.laravel.com).

### Premium Partners

- **[Vehikl](https://vehikl.com/)**
- **[Tighten Co.](https://tighten.co)**
- **[WebReinvent](https://webreinvent.com/)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel/)**
- **[Cyber-Duck](https://cyber-duck.co.uk)**
- **[DevSquad](https://devsquad.com/hire-laravel-developers)**
- **[Jump24](https://jump24.co.uk)**
- **[Redberry](https://redberry.international/laravel/)**
- **[Active Logic](https://activelogic.com)**
- **[byte5](https://byte5.de)**
- **[OP.GG](https://op.gg)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).


## php artisan make:model nom_du_model --all

- Elle crée un nouveau modèle Eloquent avec le nom nom_du_model
- L'option --all indique de également générer un controller, Seeder, migration, factory, policy une fabrique et une ressource pour ce model.

![Texte alternatif](./others/img1.png)

## Factory

Les factories dans Laravel jouent un rôle important pour générer des données de test pour les modèles

- Générer facilement des enregistrements factices en base de données pour les tests. Au lieu d'insérer manuellement des données
- Tester le modèle avec des données aléatoires à chaque exécution des tests. La factory permet de ne pas réutiliser les mêmes données statiques.

```php
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\Customer>
 */
class CustomerFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    public function definition(): array
    {
        $type = $this->faker->randomElement(['I', 'B']);
        $name = $type == 'I' ? $this->faker->name() : $this->faker->company();


        return [
            'name'=> $name,
            'type'=> $type,
            'email'=> $this->faker->email(),
            'address'=> $this->faker->streetAddress(),
            'city'=> $this->faker->city(),
            'state'=> $this->faker->state(),
            'postal_code'=> $this->faker->postcode(),
            //
        ];
    }
}

```

### Customer

Le modèle `Customer` représente un client dans le système. Il peut être de type individuel (I) ou professionnel (B). Il a des attributs tels que le nom, l'email, l'adresse, la ville, l'État, et le code postal.

```php
class Customer extends Model
{
    use HasFactory;

    public function invoices(){
        return $this->hasMany(Invoice::class);
    }
}
```

## Factories

### InvoiceFactory

La factory `InvoiceFactory` est utilisée pour générer des données de test pour le modèle `Invoice`. Elle utilise le Faker intégré à Laravel pour créer des valeurs réalistes pour les attributs.

```php
class InvoiceFactory extends Factory
{
    // ... (voir le code complet dans le message précédent)
}
```

### CustomerFactory

La factory `CustomerFactory` est utilisée pour générer des données de test pour le modèle `Customer`. Elle utilise le Faker intégré à Laravel pour créer des valeurs réalistes en fonction du type de client (individuel ou professionnel).

```php
class CustomerFactory extends Factory
{
    // ... (voir le code complet dans le message précédent)
}
```

## Seeders

### CustomerSeeder

Le seeder `CustomerSeeder` peuple la base de données avec des clients et leurs factures associées en utilisant les factories. Il simule différents scénarios en générant des quantités variables de clients et de factures pour chaque client.

```php
class CustomerSeeder extends Seeder
{
    // ... (voir le code complet dans le message précédent)
}
```

## DatabaseSeeder

La classe `DatabaseSeeder` est le point d'entrée principal pour exécuter les seeders. Dans cet exemple, elle appelle uniquement le seeder `CustomerSeeder`, mais dans un projet plus complexe, elle pourrait appeler plusieurs seeders pour générer différentes parties de la base de données.

```php
class DatabaseSeeder extends Seeder
{
    public function run(): void
    {
        $this->call(CustomerSeeder::class);
    }
}
```

N'oubliez pas d'adapter ce README en fonction des détails spécifiques de votre projet et d'ajouter d'autres sections au besoin.
