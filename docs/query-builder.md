# Documentation: Query builder

Simple PDO includes a helpful query builder which you may choose to utilize.
A query builder is useful to dynamically create queries, 
such as for an API to create a query based on the URL query string.

- [Usage](#usage)
- [Public methods](#public-methods)
- [Examples](#examples)

## Usage

The query builder requires a `PDO` instance to be passed to the constructor.
For more information on creating a `PDO` instance, [see PDO](pdo.md).

```php
use Bayfront\SimplePdo\Query;

$query = new Query($pdo); // $pdo as a PDO instance
```

## Public methods

**Build query**

- [table](#table)
- [distinct](#distinct)
- [innerJoin](#innerjoin)
- [leftjoin](#leftjoin)
- [rightjoin](#rightjoin)
- [select](#select)
- [where](#where)
- [orWhere](#orwhere)
- [startGroup](#startgroup)
- [endGroup](#endgroup)
- [groupBy](#groupby)
- [orderBy](#orderby)
- [orderByRand](#orderbyrand)
- [limit](#limit)
- [offset](#offset)

**Fetch results**

- [get](#get)
- [row](#row)
- [single](#single)
- [getLastQuery](#getlastquery)
- [getLastParameters](#getlastparameters)
- [aggregate](#aggregate)
- [getTotalRows](#gettotalrows)

<hr />

### table

**Description:**

Define the table to query.

**Parameters:**

- `$table` (string)

**Returns:**

- (self)

<hr />

### distinct

**Description:**

Add a `DISTINCT` clause to the query.

**Parameters:**

- (none)

**Returns:**

- (self)

<hr />

### innerJoin

**Description:**

Add `INNER JOIN` clause to the query.

**Parameters:**

- `$table` (string)
- `$col1` (string)
- `$col2` (string)

**Returns:**

- (self)

<hr />

### leftJoin

**Description:**

Add `LEFT JOIN` clause to the query.

**Parameters:**

- `$table` (string)
- `$col1` (string)
- `$col2` (string)

**Returns:**

- (self)

<hr />

### rightJoin

**Description:**

Add `RIGHT JOIN` clause to the query.

**Parameters:**

- `$table` (string)
- `$col1` (string)
- `$col2` (string)

**Returns:**

- (self)

<hr />

### select

**Description:**

Define column(s) to select.

If the column type is `JSON`, keys from within the JSON string can be selected with the format of `COLUMN->KEY`.
The field will be returned as a multidimensional array.
JSON fields which do not exist are returned with a value of `null`.

**Parameters:**

- `$columns` (string|array)

**Returns:**

- (self)

<hr />

### where

**Description:**

Adds a `WHERE/AND WHERE` clause to the query.

If the column type is `JSON`, keys from within the JSON string can be searched with the format of `COLUMN->KEY`.
JSON fields which do not exist are treated as `null`.

Available operators are:

- `eq` (equals)
- `!eq` (does not equal)
- `lt` (less than)
- `gt` (greater than)
- `le` (less than or equal to)
- `ge` (greater than or equal to)
- `sw` (starts with)
- `!sw` (does not start with)
- `isw` (starts with - case-insensitive)
- `!isw` (does not start with - case-insensitive)
- `ew` (ends with)
- `!ew` (does not end with)
- `iew` (ends with - case-insensitive)
- `!iew` (does not end with - case-insensitive)
- `has` (has)
- `!has` (does not have)
- `ihas` (has - case-insensitive)
- `!ihas` (does not have - case-insensitive)
- `in` (in)
- `!in` (not in)
- `null` (is null)
- `!null` (is not null)

The `OPERATOR_*` constants can be used for this purpose.

The `in` and `!in` operators accept multiple comma-separated values.

The `null` and `!null` operators accept one of two values: `true` and `false`.
The `VALUE_*` constants can be used for this purpose.

> **NOTE:** Some native MySQL functions can be used as the `$value`, however, they will be
> injected into the query as strings, so they can be vulnerable to SQL injection. 

**Parameters:**

- `$column` (string)
- `$operator` (string)
- `$value` (mixed)

**Returns:**

- (self)

**Throws:**

- `Bayfront\SimplePdo\Exceptions\QueryException`

<hr />

### orWhere

**Description:**

Adds an `OR/AND OR` clause to the query.

See [where](#where).

**Parameters:**

- `$column` (string)
- `$operator` (string)
- `$value` (mixed)

**Returns:**

- (self)

**Throws:**

- `Bayfront\SimplePdo\Exceptions\QueryException`

<hr />

### startGroup

**Description:**

Start new clause with opening parentheses.

The `$condition` must be one of `AND` or `OR`.
The `CONDITION_AND` and `CONDITION_OR` constants can be used for this purpose.

**Parameters:**

- `$condition` (string)

**Returns:**

- (self)

**Throws:**

- `Bayfront\SimplePdo\Exceptions\QueryException`

<hr />

### endGroup

**Description:**

End clause with closing parentheses.

**Parameters:**

- (none)

**Returns:**

- (self)

<hr />

### groupBy

**Description:**

Adds a `GROUP BY` clause.

**Parameters:**

- `$columns` (array)

**Returns:**

- (self)

<hr />

### orderBy

**Description:**

Adds an `ORDER BY` clause.

Values in the `$columns` array without a prefix or prefixed with a `+` will be ordered ascending.
Values in the `$columns` array prefixed with a `-` will be ordered descending.

If the column type is `JSON`, keys from within the JSON string can be ordered with the format of `COLUMN->KEY`.
JSON fields which do not exist are treated as `null`.

**Parameters:**

- `$columns` (array)

**Returns:**

- (self)

<hr />

### orderByRand

**Description:**

Adds an `ORDER BY RAND()` clause.

**Parameters:**

- (None)

**Returns:**

- (self)

<hr />

### limit

**Description:**

Adds a `LIMIT` clause.

**Parameters:**

- `$limit` (int)

**Returns:**

- (self)

<hr />

### offset

**Description:**

Adds an `OFFSET` clause.

**Parameters:**

- `$offset` (int)

**Returns:**

- (self)

<hr />

### get

**Description:**

Get the result set from a table.

**Parameters:**

- (None)

**Returns:**

- (array)

<hr />

### row

**Description:**

Get a single row from a table, or `false` on failure.

**Parameters:**

- (None)

**Returns:**

- (mixed)

<hr />

### single

**Description:**

Get a single column of a single row of a table, or `false` if not existing.
If more than one field was defined by [select](#select), the first field will be returned.

**Parameters:**

- (None)

**Returns:**

- (mixed)

<hr />

### getLastQuery

**Description:**

Returns last raw query.

**Parameters:**

- (None)

**Returns:**

- (string)

<hr />

### getLastParameters

**Description:**

Returns last query parameters.

**Parameters:**

- None

**Returns:**

- (array)

<hr />

### aggregate

**Description:**

Return calculation of an aggregate function.

Available aggregate functions are:

- `AVG`
- `AVG_DISTINCT`
- `COUNT`
- `COUNT_DISTINCT`
- `MAX`
- `MIN`
- `SUM`
- `SUM_DISTINCT`

The `AGGREGATE_*` constants can be used for this purpose.

**Parameters:**

- `$aggregate` (string): Any valid aggregate function
- `$column = '*'` (string)
- `$decimals = 2` (int)

**Returns:**

- (float)

<hr />

### getTotalRows

**Description:**

Returns total number of rows found for the query without limit restrictions.

NOTE: To get the number of rows affected by a `DELETE`, use the [Bayfront\SimplePdo\Db->rowCount()](README.md#rowcount) method.

This method is depreciated in favor of [aggregate](#aggregate).

**Parameters:**

- (None)

**Returns:**

- (int)

## Examples

Select all records from `items` table:

```php
$results = $query->table('items')
    ->select('*')
    ->get();
```

<hr />

Select all records from `items` table where `price` is greater than `20.00`:

```php
use Bayfront\SimplePdo\Query;

$results = $query->table('items')
    ->select('*')
    ->where('price', Query::OPERATOR_GREATER_THAN, '20.00')
    ->get();
```

<hr />

Select `name`, `color`, `quantity`, `supplier->location` and `supplier->email` as `supplier_email` records from `items` table where `price` is greater than `20.00` and `supplier->name` starts with `a`:

```php
use Bayfront\SimplePdo\Query;

$results = $query->table('items')
    ->select([
        'name',
        'color',
        'quantity',
        'supplier->location',
        'supplier->email AS supplier_email'
    ])
    ->where('price', Query::OPERATOR_GREATER_THAN, '20.00')
    ->where('supplier->name', Query::OPERATOR_STARTS_WITH, 'a')
    ->get();
```

This example represents a column named `supplier` with type of `json`.

<hr />

Select up to 10 results for `name`, `color`, `quantity` from `items` table where `description` contains the word "fluffy", and the price is less than `50.00`, ordered by `name` descending.
Also, get the total number of rows found for the query.

```php
use Bayfront\SimplePdo\Query;

$results = $query->table('items')
    ->select([
        'name',
        'color',
        'quantity'
    ])
    ->where('description', Query::OPERATOR_HAS, 'fluffy')
    ->where('price', Query::OPERATOR_LESS_THAN, '50.00')
    ->orderBy([
        '-name'
    ])
    ->limit(10)
    ->get();

$total_count = $query->aggregate($query::AGGREGATE_COUNT);
```

<hr />

Select the name from `items` where `price` is greater than `20.00` 
or where `price` is less than `5.00` and quantity is less than `10` (using clause groups):

```php
use Bayfront\SimplePdo\Query;

$results = $query->table('items')
    ->select([
        'name'
    ])
    ->where('price', Query::OPERATOR_GREATER_THAN, '20.00')
    ->startGroup(Query::CONDITION_OR)
    ->where('price', Query::OPERATOR_LESS_THAN, '5.00')
    ->where('quantity', Query::OPERATOR_LESS_THAN, 10)
    ->endGroup()
    ->get();
```

<hr />

Example using `LEFT JOIN`:

```php
use Bayfront\SimplePdo\Query;

$results = $query->table('items')
    ->leftJoin('vendors', 'items.vendor_id', 'vendors.id')
    ->select([
        'vendors.name',
        'items.name',
        'items.color',
        'items.quantity'
    ])
    ->where('items.description', Query::OPERATOR_HAS, 'fluffy')
    ->where('items.price', Query::OPERATOR_LESS_THAN, '50.00')
    ->orderBy([
        'vendors.name',
        '-items.name'
    ])
    ->limit(10)
    ->get();

$total_count = $query->aggregate($query::AGGREGATE_COUNT);
```