Bokun REST Client
================

Kohana REST client for Bokun API by extending Kohana's Request class.


Installation
----------------

In your web root path, do:

`git clone git://github.com/birkir/kohana-api-bokun.git modules/bokun-api`

Then add the module to your bootstrap file:

`'bokun-api' => MODPATH.'bokun-api',`


How to use
----------------

Simple search using startDate and endDate.

```php
$search = Bokun::factory(Bokun::ACCOMMADATION)
->method(Bokun::POST)
->operation('search')
->params(array(
  'startDate' => new DateTime('2013-11-01'),
  'endDate'   => new DateTime('2013-12-01')
))
->execute();

echo Debug::vars($search);
```

Simply attach users browser session to API session. Display users cart.

```php
$session = Session::instance();

$cart = Bokun::factory(Bokun::SHOPPING_CART)
->operation('session')
->operation($session->id())
->execute();

echo Debug::vars($cart);
```


Create customer from $_POST values.

```php
$customer = Bokun::factory(Bokun::CUSTOMER)
->method(Bokun::POST)
->operation('new')
->params($this->request->post())
->execute();

if ( ! $customer->success)
  throw new Kohana_Exception('Customer not created successfully. Try again later.');
```

Note: chainable methods are do not have to be in order, except *operation* method. Also, the execution method has to be the last one.
