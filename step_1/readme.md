# Crash Testing

## Step 1

* (walk through) Implement Laravel's [array_get()](https://laravel.com/docs/5.3/helpers#method-array-get)

* Implement Laravel's [array_pull()](https://laravel.com/docs/5.3/helpers#method-array-pull)

* Implement Laravel's [array_except()](https://laravel.com/docs/5.3/helpers#method-array-except)

* Implement Laravel's [array_forget()](https://laravel.com/docs/5.3/helpers#method-array-forget)

## Specs

### array_get()

#### Signature
*array_get(mixed[] $array, string $elements, mixed $default = null)*
* $array is an array of any type
* $elements is a dot-delimited string pointing to a nested element
* $default can be any value

#### Returns
* If **$elements** points to a present nested element within **$array**, return that element
* If **$elements** points to non-present nested element of **$array**, return **$default**

#### Example
```
array_get([ 'foo' => [ 'bar' => 'baz' ] ], 'foo.bar')
// -> 'bar'

array_get([ 'foo' => 'baz' ], 'foo.bar')
// -> null

array_get([ 'foo' => 'baz' ], 'foo.bar', 42)
// -> 42
```

### array_pull()

#### Signature
*array_pull(mixed[] $array, string $elements)*
* $array is an array of any type
* $elements is a dot-delimited string pointing to a nested element

#### Returns
* If **$elements** points to a present nested element within **$array**, return that element and remove the element from **$array**
* If **$elements** points to non-present nested element of **$array**, return null

#### Example
```
$array = ['name' => 'Desk', 'price' => 100];
$name = array_pull($array, 'name');
// $name: Desk
// $array: ['price' => 100]

$name = array_pull($array, 'name');
// $name: null
// $array: ['price' => 100]
```

### array_except()
#### Signature
*array_except(mixed[] $array, string $elements)*
* $array is an array of any type
* $elements is a dot-delimited string pointing to a nested element

#### Returns
* If **$elements** points to a present nested element within **$array**, return **$array** without that element
* If **$elements** points to non-present nested element of **$array**, return **$array** as-is

#### Example
```
$array = ['name' => 'Desk', 'price' => 100];
$array = array_except($array, ['price']);
// ['name' => 'Desk']

$array = ['name' => 'Desk', 'price' => 100];
$array = array_except($array, ['foo']);
// ['name' => 'Desk', 'price' => 100]
```

### array_forget()
#### Signature
*array_forget(mixed[] $array, string $elements)*
* $array is an array of any type
* $elements is a dot-delimited string pointing to a nested element

#### Returns
* *array_except()* is a void function
* If **$elements** points to a present nested element within **$array**, remove element from **$array**
* If **$elements** points to non-present nested element of **$array**, do nothing

#### Example
```
$array = ['products' => ['desk' => ['price' => 100]]];
array_forget($array, 'products.desk');
// ['products' => []]

$array = ['products' => ['desk' => ['price' => 100]]];
array_forget($array, 'foo.bar');
// ['products' => ['desk' => ['price' => 100]]];
```