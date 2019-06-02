# paginator
A Codeigniter library to add pagination easily

## Simple Usage:

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

The second parameter is optional, the available options currently are: 'bootstrap3' or 'bootstrap4' or 'bulma'. 

## Customize the Result:

Paginator allows you to specify **where**, **like** and **order_by** options to customize your query result like the following:

```php
$data['posts'] = $this->paginator->paginate('posts', ['base_url' => "posts", 'where' => array('published' => '1'), 'order_by' => 'id asc' , 'per_page' => 15]);
```
or with like :

```php
$data['posts'] = $this->paginator->paginate('posts', ['base_url' => "posts", 'like' => array('title' => 'some term here'), 'order_by' => 'id asc' , 'per_page' => 15]);
```

And that's fine for most situations, but what if you need more complex request ? 

In this case :

1- get rid of **where**, **like** and **order_by** options

2- replace the very first parameter of `paginate()` method with custom query builder result, for example :

```php
$this->load->model('YourModel');
$custom_object = $this->YourModel->get_custom_db_obj();
$data['posts'] = $this->paginator->paginate($custom_object, ['base_url' => "posts", 'per_page' => 15]);
```
In your model you might have a method that returns the db object, for example

```php
function get_custom_db_obj()
{
  # you can have any complex query here:
  $this->db->select('*');
  $this->db->from('posts');
  $this->db->where(array('published'=>'1'));
  $this->db->order_by('created_at', 'DESC');
  return $this->db; // make sure to return $this->db without calling ->get() on it
}
```
**It's very important to note that you should never call or return $this->db->get() but only return $this->db, also avoid using limit() on your request building because it's the role of paginator to use it internally**

## Feedback

Please use the [Issues](https://github.com/scratchoo/paginator/issues) for any bugs, feature requests, etc.

## License

MIT License
