# Nova Notes Field

This package is based on the original Nova Notes Field package by [Tarvo Reinpalu](https://github.com/Tarpsvo).

All credit goes to Tarvo Reinpalu for creating a fantastic addition to Nova. The core features of the original package are the same however there are some layout tweaks and I hope to add additional features such as stuck/important notes, latest note cards, etc.

## Features

- Notes field on Detail view
- Differentiation between user-added and system-added notes
- Ability to add notes through the UI or programmatically
- Ability to delete user-made notes (w/ confirmation modal)
- Customizable placeholder support

## Installation

```bash
# Install the package via Composer
composer require jam0r85/nova-notes-field

# Run automatically loaded migration(s)
php artisan migrate
```

## Usage

Add `HasNotes` trait to the model that has the notes:

```php
use Jam0r85\NovaNotesField\Traits\HasNotes;

class ExampleModel extends Model
{
    use HasNotes;
}
```

Add `NotesField` to the matching resource:

```php
use Jam0r85\NovaNotesField\NotesField;

class SomeResource extends Resource
{
  // ...

  public function fields(Request $request)
  {
    return [
      // ...
      NotesField::make('Notes')
        ->placeholder('Add note'), // Optional
    ]
  }
}
```

## Adding notes programmatically

To add notes programmatically, use the method provided by the `HasNotes` trait:

```php
/**
 * Creates a new note and attaches it to the model.
 *
 * @param string $note The note text which can contain raw HTML.
 * @param bool $user Enables or disables the use of `Auth::user()` to set as the creator.
 * @param bool $system Defines whether the note is system created and can be deleted or not.
 * @return \Jam0r85\NovaNotesField\Models\Note
 **/
public function addNote($note, $user = true, $system = true)
```

## Credits

- [Tarvo Reinpalu](https://github.com/Tarpsvo)

## License

This project is open-sourced software licensed under the [MIT license](LICENSE.md).
# nova-notes-field
