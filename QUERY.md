# Querying Data

-   Using the **find()** method:
    -   The **find()** method is the primary method for querying data in CakePHP. It allows you to specify conditions, sorting, pagination, and other options.
    -   Example:
    ```php
    $query = $this->ModelName->find('all');
    $results = $query->toArray();
    ```
-   Using conditions:
    -   You can use the **where()** method to specify conditions in the query.
    -   Example:
    ```php
    $query = $this->ModelName->find('all')
      	->where(['field_name' => 'value']);
    $results = $query->toArray();
    ```
-   Using custom queries:

    -   You can use custom SQL queries using the **query()** method to perform complex queries that are not easily achievable with the built-in methods.
    -   Example:

    ```php
    $results = $this->ModelName->query('SELECT * FROM table_name');
    ```

-   Using query builder methods:
    -   You can chain query builder methods to build complex queries with conditions, sorting, grouping, joins, and other options.
    -   Example:
    ```php
    $query = $this->ModelName->find('all')
    	->where(['field1' => 'value1'])
    	->andWhere(['field2' => 'value2'])
    	->order(['field3' => 'ASC'])
    	->limit(10);
    $results = $query->toArray();
    ```
-   Using associations:
    -   If you have defined associations between models, you can use them to retrieve related data using methods like **contain()** and **matching()**.
    -   Example:
    ```php
    $query = $this->ParentModel->find('all')
    	->contain('ChildModel');
    $results = $query->toArray();
    ```
