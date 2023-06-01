# Controller's Lifecycles

-   **initialize()**: This method is called when the controller is instantiated. It is often used to set up any initial configuration, such as loading components, helpers, or other dependencies.

-   **beforeFilter()**: This method is called before each action method is executed. It is commonly used for tasks such as authentication, authorization, or setting up data that is required by multiple actions.
    -   This event is triggered before any controller action is executed.
    ```php
    // Example callback method for beforeFilter event
    public function beforeFilter(Event $event)
    {
    	// Perform pre-action operations or apply authentication/authorization rules
    }
    ```
-   **afterFilter()**: This method is called after the view has been rendered and the response has been sent to the client. It is typically used for cleanup tasks or logging.

    -   This event is triggered after a controller action is executed.

    ```php
    // Example callback method for afterFilter event
    public function afterFilter(Event $event)
    {
    	// Perform post-action operations or cleanup tasks
    }
    ```

-   **beforeRender()**: This method is called just before the view is rendered. It allows you to modify the data that will be passed to the view or perform any other necessary operations.
    -   This event is triggered before the view is rendered.
    ```php
    // Example callback method for beforeRender event
    public function beforeRender(Event $event)
    {
    	// Perform pre-render operations or modify view variables
    }
    ```
-   **afterRender()**:

    ```php
    // Example callback method for afterRender event
    public function afterRender(Event $event)
    {
    	// Perform post-render operations or additional view modifications
    }
    ```

-   **beforeRedirect()**: This method is called before a redirect response is sent back to the client. It can be used to modify the redirect URL or perform any other necessary operations before the redirect occurs.

-   **shutdown**: This event is triggered at the end of the request lifecycle, after the response has been sent.
    ```php
    // Example callback method for shutdown event
    public function shutdown(Event $event)
    {
    	// Perform cleanup tasks or logging
    }
    ```

---

# View Events:

-   **beforeRender**: This event is triggered before the view is rendered.
    ```php
    // Example callback method for beforeRender event
    public function beforeRender(Event $event)
    {
    	// Perform pre-render operations or modify view variables
    }
    ```
-   **afterRender**: This event is triggered after the view is rendered.
    ```php
    // Example callback method for afterRender event
    public function afterRender(Event $event)
    {
    	// Perform post-render operations or additional view modifications
    }
    ```
-   **beforeLayout**: This event is triggered before the layout is applied to the view.
    ```php
    // Example callback method for beforeLayout event
    public function beforeLayout(Event $event)
    {
    	// Perform pre-layout operations or modify layout variables
    }
    ```
-   **afterLayout**: This event is triggered after the layout is applied to the view.
    ```php
    // Example callback method for afterLayout event
    public function afterLayout(Event $event)
    {
    	// Perform post-layout operations or additional layout modifications
    }
    ```

---

# Component Events:

-   initialize: This event is triggered during the initialization of a component.

```php
// Example callback method for initialize event
public function initialize(Event $event)
{
	// Perform initialization tasks or configuration settings
}
```

-   startup: This event is triggered after the component has been initialized.

```php
// Example callback method for startup event
public function startup(Event $event)
{
    // Perform startup tasks or checks before the component is used
}
```

-   beforeRender: This event is triggered before the component's associated view is rendered.

```php
// Example callback method for beforeRender event
public function beforeRender(Event $event)
{
    // Perform pre-render operations or modify view variables
}
```

-   shutdown: This event is triggered at the end of the request lifecycle, after the response has been sent.

```php
// Example callback method for shutdown event
public function shutdown(Event $event)
{
    // Perform cleanup tasks or logging
}
```

---

# Model Callback Method

-   **beforeFind**/**afterFind**:
    -   beforeFind: This event is triggered before a database query is executed.
    -   afterFind: This event is triggered after a database query is executed.

```php
// Example callback method for beforeFind event
public function beforeFind(Event $event, Query $query, \ArrayObject $options, $primary)
{
    // Perform pre-query operations or modify the query
}

// Example callback method for afterFind event
public function afterFind(Event $event, EntityInterface $entity, \ArrayObject $options)
{
    // Perform post-query operations or modify the retrieved entity
}
```

-   **beforeValidate**/**afterValidate**:
    -   beforeValidate: This event is triggered before the validation process.
    -   afterValidate: This event is triggered after the validation process.

```php
// Example callback method for beforeValidate event
public function beforeValidate(Event $event, EntityInterface $entity, \ArrayObject $options)
{
    // Perform pre-validation operations or modify the entity data
}

// Example callback method for afterValidate event
public function afterValidate(Event $event, EntityInterface $entity, \ArrayObject $options, $result)
{
    // Perform post-validation operations or modify the validation result
}
```

-   **beforeSave**/**afterSave**:
    -   beforeSave:This event is triggered before saving data to the database.
    -   afterSave: This event is triggered after data is saved to the database.

```php
// Example callback method for beforeSave event
public function beforeSave(Event $event, EntityInterface $entity, \ArrayObject $options)
{
    // Perform pre-save operations or modify the entity data
}

// Example callback method for afterSave event
public function afterSave(Event $event, EntityInterface $entity, \ArrayObject $options)
{
    // Perform post-save operations or access the saved entity
}
```

-   **beforeDelete**/**afterDelete**:
    -   beforeDelete: This event is triggered before a record is deleted from the database.
    -   afterDelete: This event is triggered after a record is deleted from the database.

```php
// Example callback method for beforeDelete event
public function beforeDelete(Event $event, EntityInterface $entity, \ArrayObject $options)
{
    // Perform pre-deletion operations or validation checks
}

// Example callback method for afterDelete event
public function afterDelete(Event $event, EntityInterface $entity, \ArrayObject $options)
{
    // Perform post-deletion operations or cleanup tasks
}
```

-   **beforeMarshal(array $data, array $options)**: This method is called before data is marshaled for saving or patching. It allows you to modify the data array before it is processed further.

-   **beforeValidate(array $options)**: This method is called before data validation occurs. You can use this method to perform any data manipulation or additional validation checks before the validation process.

-   **afterValidate(array $options)**: This method is called after data validation has been performed successfully. It is typically used for any post-validation processing or data cleanup tasks.

-   **beforeSave($event, $entity, $options)**: This method is called before a model entity is saved to the database. It provides an opportunity to perform any additional data manipulation or validation before saving.

-   **afterSave($event, $entity, $options)**: This method is called after a model entity has been successfully saved. It can be used for any post-save processing or updating related data.

-   **beforeDelete($event, $entity, $options)**: This method is called before a model entity is deleted from the database. You can use this method to perform any necessary checks or additional actions before deletion.

-   **afterDelete($event, $entity, $options)**: This method is called after a model entity has been deleted. It can be used for any post-deletion processing or cleanup tasks.

#### These callback methods allow you to intervene and add custom logic at specific points in the model's lifecycle. By overriding these methods in your model class, you can extend the default behavior of the model and implement custom business rules or data manipulation.

---

# Request Events

-   beforeDispatch: This event is triggered before the request is dispatched to the corresponding controller action.

```php
// Example callback method for beforeDispatch event
public function beforeDispatch(Event $event)
{
    // Perform pre-dispatch operations or modify the request
}
```

-   afterDispatch: This event is triggered after the request has been dispatched and the controller action has been executed.

```php
// Example callback method for afterDispatch event
public function afterDispatch(Event $event)
{
    // Perform post-dispatch operations or additional request processing
}
```
