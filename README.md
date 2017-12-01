# Restful

Method to API RESTFUL.

Namespace :

`use KintoUn\libs\Restful;`

All the methods are static.
This 4 methods test the request and return truc or false.

* POST   => Request::POST();
* GET    => Request::GET();
* PUT    => Request::PUT();
* DELETE => Request::DELETE();

To intercept the Request:
* POST   => $_POST
* PUT    => $this->_PUT or Request::$_PUT
* DELETE => Through the uri or $_GET
* GET    => Through the uri or $_GET



```php
# link: mywebsite.com/user/

public function viewAction($id){
  $data = $this->user->findAll();
  
  Request::GET($data); # a condition is not necessary for a GET
  
  # Or if you want to use a condition and return the json use
  
  if(Request::GET()){
    Request::renderJson($data);
  }
  
  if(Request::POST()){
    $this->user->save($_POST);
  }else{ #sinon retourne une page html
    Restful::headerResponse(400);
    exit("Bad Request");
  }
}
```

```php
# lien: mywebsite.com/user/44
# 44 is the $id parameter of the uri

public function viewAction($id){
  $data = $this->user->findById($id);

  Request::GET($data);

  if(Request::PUT()){
    $this->user->save(Request::$_PUT);
  }elseif (Request::DELETE()){
    $this->user->delete($id);
  }else{
    Restful::headerResponse(400);
    exit("Bad Request");			
  }
}
```
