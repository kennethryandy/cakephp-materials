# Updating Data

-   Here's an example of how you can use the **where()** method with the **IN** operator to query data:

```php
$ids = [1, 2, 3]; // An array of IDs to match

$query = $this->ModelName->find()
    ->where(['id IN' => $ids]);

$results = $query->all();
```

-   Using the **patchEntity()** Method:
    The **patchEntity()** method allows you to update an existing entity with new data before saving. You can retrieve the entity you want to update from the database, patch it with the new data, and then save it using the model's save() method. For example:

```php
// Retrieve the entity to update
$author = $this->Authors->get($id);

// Patch the entity with new data
$author = $this->Authors->patchEntity($author, $this->request->getData());

// Save the updated entity
$this->Authors->save($author);
```

The **patchEntity()** method automatically maps the request data to the entity's properties based on their names.

-   Using the **save()** Method with Data Array:
    If you already have an array of data to update, you can directly pass it to the model's **save()** method. This method will create or update the record based on the provided data. For example:

```php
// Update the author record using data array
$data = [
    'id' => $id,
    'name' => 'New Author Name',
    // Other fields to update
];

$author = $this->Authors->newEntity($data);
$this->Authors->save($author);
```

In this example, the **save()** method updates the author record with the new data based on the specified **id**.

-   Using the **query()->update()** Method:
    If you prefer to work with raw SQL queries, you can use the **query()** method along with the **update()** method to create and execute custom SQL update queries. For example:

```php
$query = $this->Authors->query();
$query->update()
    ->set(['name' => 'New Author Name'])
    ->where(['id' => $id])
    ->execute();
```

This approach allows you to have more control over the update query and can be useful for complex update operations.

# Updating with relationship

-   Using the **saveAssociated()** method:
    -   If you have defined the associations between parent and child models correctly, you can use the **saveAssociated()** method to update both parent and child models in a single call.
    -   This method automatically handles saving associated data and manages the necessary foreign key relationships.
    -   Example:
    ```php
    $this->ParentModel->patchEntity($parentEntity, $parentData, ['associated' => ['ChildModel']]);
    $this->ParentModel->saveAssociated($parentEntity);
    ```
-   Using the **save()** method for the parent and **saveMany()** or **saveAssociated()** for the child:

    -   You can update the parent model using the **save()** method, and then update the child model separately.
    -   Example:

    ```php
    $this->ParentModel->patchEntity($parentEntity, $parentData);
    $this->ParentModel->save($parentEntity);

    $this->ChildModel->saveMany($childDataArray);
    ```

-   Updating child models and parent associations separately:

    -   You can update child models individually and then update the parent model's associations using the **link()** or **unlink()** methods.
    -   Example:

    ```php
    // Update child models
    $this->ChildModel->save($childEntity1);
    $this->ChildModel->save($childEntity2);

    // Update parent associations
    $this->ParentModel->link($childEntity1, ['associated' => ['ChildModel']]);
    $this->ParentModel->link($childEntity2, ['associated' => ['ChildModel']]);
    ```

-   Using transactions:

    -   If you want to ensure atomicity, you can use transactions to update both parent and child models.
    -   Example:

    ```php
    $connection = ConnectionManager::get('default');
    $connection->begin();
    try {
    	// Update parent and child models

    	$connection->commit();
    } catch (\Exception $e) {
    	$connection->rollback();
    }
    ```
