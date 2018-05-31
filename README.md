# paginator
A Codeigniter library to add pagination easily

## Usage:

Download and copy the Paginator.php file to your Codeigniter libraries folder

In your controller use it like the following :

```php
$this->load->library('paginator'); // load paginator library
$data['posts'] = $this->paginator->paginate('posts'); // per page equal 10 by default
```

You can customize 3 optional options (per_page, query_string (true/false), base_url) by passing them as an array for the second parameter:

```php
$data['posts'] = $this->paginator->paginate('posts', ['per_page' => 15, 'query_string' => true, 'base_url' => 'posts']);
```

you can read more about Codeigniter pagination options here : https://www.codeigniter.com/userguide3/libraries/pagination.html


Finally in your view to add the pagination links :

```php
<?php echo $this->paginator->get_links('posts', 'bootstrap4'); ?>
```

The second parameter is optional, if you are using bootstrap 3 or 4 just pass 'bootstrap3' or 'bootstrap4' as a second parameter.
