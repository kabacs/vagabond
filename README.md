# Vagabond

## About Vagabond

Vagabond is a project that lets you leverage [Nomad](https://github.com/michaeldyrynda/nomad) - Laravel-style database migrations wherever they may roam.

Nomad gives you the power of Laravel's [database migrations](https://laravel.com/docs/5.5/migrations) without the need for a full Laravel installation.

This is particularly useful where you have multiple applications accessing a single database, but you aren't sure which should be responsible for managing the database schema. By extracting your migrations to a separate repository, you can maintain full version control over your database schema, without worrying about different applications trying to run the migrations on the same database.

In addition, you also have the ability to use those centralised migrations within your application test suite much more easily, without having to either duplicate the migrations or run against your own copy of the database.

## Installation

In order to create a new Vagabond project, you can use [Composer](https://getcomposer.org).

```
composer create-project --prefer-dist dyrynda/vagabond wanderer
```

Once installed, you will have access to the `nomad` application, a default configuration to work with an sqlite database, and a `VagabondServiceProvider`. You can extend from this service provider to handle automatically loading configuration for each of your connections. All you need to do is define a protected property - `$connectionName` - on the child provider, that corresponds to the connection you are configuring.

## Usage

Out of the box, Vagabond is configured to use a MySQL database in `config/database.php`. As with Laravel, you can [configure your connections](https://laravel.com/docs/5.6/database#configuration) and database drivers of choice, as well as keeping credentials safe in your `.env` file.

To create a migration, use the `make:migration` Nomad command.

```
php nomad make:migration create_travellers_table
```

You can check the status of your run and pending migrations using the `status` command.

```
php nomad migrate:status
```

Any pending migrations can be run using the `migrate` command.

```
php nomad migrate
```

For further information on the available commands and their functions, be sure to check out Laravel's [migration documentation](https://laravel.com/docs/5.5/migrations).

## Using Vagabond in Laravel applications

You can use Vagabond in your Laravel applications by defining and including service providers centrally in one repository, and include them in any applications that need them.

In doing so, your Laravel application will be able to access the migrations and database configuration, making it very simple to use them in your test environment, whilst still managing your production database in a standalone fashion. This also means that your database could be separately versioned and even managed by database administrators independently of your development process.

**Note:** Be sure not to call the `nomad` console application within your Laravel app as it will not run correctly. When ready, you can use the usual Artisan migrate tools.

You'll first want to update your `composer.json` file to reflect a package name relevant to your project by updating the `name` property.

If you're not using [Packagist](https://packagist.org) to share your migrations, you may need to configure a path or vcs repository as well. You can learn more about this in the Composer [repositories documentation](https://getcomposer.org/doc/05-repositories.md#hosting-your-own).

## Credits

Special thanks to [Nuno Maduro](https://twitter.com/enunomaduro) for the work he has done with [Laravel Zero](http://laravel-zero.com), which helped pave the way for me to finally bring this project to life.

## Support

You can learn more about this project and how it is used [here](https://dyrynda.com.au/blog/sharing-databases-between-laravel-applications).

If you are having general issues with this package, feel free to contact me on [Twitter](https://twitter.com/michaeldyrynda).

If you believe you have found an issue, please report it using the [GitHub issue tracker](https://github.com/michaeldyrynda/vagabond/issues), or better yet, fork the repository and submit a pull request.

If you're using this package, I'd love to hear your thoughts. Thanks!
