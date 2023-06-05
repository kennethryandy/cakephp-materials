# Inserting Data

-   Creating and Saving Entities:
    You can create an entity using the model's **newEntity()** method and populate its properties with the data you want to insert. Then, save the entity using the model's **save()** method. For example:

```php
// Create a new entity
$author = $this->Authors->newEntity();
$author->name = 'John Doe';

// Save the entity
$this->Authors->save($author);
```

-   Creating and Saving Associated Data:
    If you have associated models, you can include associated data while saving. For example, if an **Author** has many **Books**, you can save the author and associated books using the **newEntity()** method with associated data and the **save()** method with the **'associated'** option:

```php
// Create a new entity with associated data
$author = $this->Authors->newEntity([
    'name' => 'John Doe',
    'books' => [
        ['title' => 'Book 1'],
        ['title' => 'Book 2'],
    ]
], ['associated' => ['Books']]);

// Save the entity and associated data
$this->Authors->save($author, ['associated' => ['Books']]);
```

-   Using Table's **query()** Method:
    You can also use the **query()** method of the model's table to create and execute custom SQL queries. This provides more flexibility for complex insert operations. For example:

```php
$query = $this->Authors->query();
$query->insert(['name'])
    ->values(['name' => 'John Doe'])
    ->execute();
```

-   Batch Inserts:
    If you need to insert multiple records at once, you can use the **newEntities()** method to create multiple entities and then save them in a batch using the **saveMany()** method. For example:

```php
$authors = $this->Authors->newEntities([
    ['name' => 'Author 1'],
    ['name' => 'Author 2'],
    ['name' => 'Author 3'],
]);

$this->Authors->saveMany($authors);
```

-   Using the **patchEntity()** Method:
    The **patchEntity()** method allows you to create an entity and patch it with request data before saving. This method is commonly used when you have form data to populate the entity. For example:

```php
// Create an entity and patch it with request data
$author = $this->Authors->newEntity();
$author = $this->Authors->patchEntity($author, $this->request->getData());

// Save the entity
$this->Authors->save($author);
```

-   Using the **saveMany()** Method with Association:
    If you have a one-to-many or many-to-many association and want to save multiple records along with associated data, you can use the **saveMany()** method with the **'associated'** option. This method allows you to save multiple entities and their associated entities in a single operation. For example:

```php
// Create an array of entities with associated data
$authors = [
    ['name' => 'Author 1', 'books' => [['title' => 'Book 1']]],
    ['name' => 'Author 2', 'books' => [['title' => 'Book 2']]],
    ['name' => 'Author 3', 'books' => [['title' => 'Book 3']]],
];

// Save the entities and associated data
$this->Authors->saveMany($authors, ['associated' => ['Books']]);
```

#### These are some of the common methods used for inserting data in CakePHP version 3. Adjust the code according to your specific application's requirements and naming conventions.

# Inserting with relationship

-   BelongsTo Relationship:
    For a **BelongsTo** relationship, where one model belongs to another, you can associate the parent model with the child model using the foreign key. Here's an example:

```php
// Create a new Author entity and associate it with a User
$author = $this->Authors->newEntity();
$author->name = 'John Doe';
$author->user_id = $user->id; // Assuming you have the user ID

$this->Authors->save($author);
```

-   HasOne and HasMany Relationships:
    For **HasOne** and **HasMany** relationships, where one model has one or multiple associated models, you can include the associated data when creating the entity. Here's an example:

```php
// Create a new User entity and associate it with a Profile
$user = $this->Users->newEntity([
    'username' => 'john_doe',
    'email' => 'john@example.com',
    'profile' => [
        'first_name' => 'John',
        'last_name' => 'Doe',
    ],
], ['associated' => ['Profile']]);

$this->Users->save($user, ['associated' => ['Profile']]);
```

In this example, the **Users** table has a **HasOne** relationship with the Profiles table, where each user has one associated profile.

\*BelongsToMany Relationship:
For a **BelongsToMany** relationship, where two models are associated through a join table, you can include the associated data when creating the entity. Here's an example:

```php
// Create a new Book entity and associate it with multiple Authors
$book = $this->Books->newEntity([
    'title' => 'Book Title',
    'authors' => [
        ['name' => 'Author 1'],
        ['name' => 'Author 2'],
    ],
], ['associated' => ['Authors']]);

$this->Books->save($book, ['associated' => ['Authors']]);
```

In this example, the **Books** table has a **BelongsToMany** relationship with the Authors table, where multiple authors can be associated with a book through a join table.


-   Transactional Saving: If you have multiple operations that need to be performed within a single transaction (such as saving the parent and child records), you can wrap the save operation in a transaction. This ensures that either all the records are saved successfully or none of them are saved.
```php
$connection = ConnectionManager::get('default');
$connection->begin();
try {
    if ($this->Parent->save($parent, ['associated' => ['Child']])) {
        $connection->commit();
        // Success handling
    } else {
        $connection->rollback();
        // Error handling
    }
} catch (\Exception $e) {
    $connection->rollback();
    // Exception handling
}
```

