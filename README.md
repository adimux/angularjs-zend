AngularJS services/providers/factories useful with a Zend PHP back-end

## 1. zendUrl provider

**Build urls** (like $this->url) to **request** a **zend based back-end** in AngularJS using the zendUrl provider

The module to inject as a dependency is **"zend"**
So add it in your list of dependencies :

    var myApp = angular.module("myApp", [..., "zend"] );

Then configure it :

    myApp.config(function(zendUrl) {
        zendUrl.setBaseUrl("http://mybackend.com/zendApplication/"); // Base url of the zend app
        // Set the hierarchy of your zend app. Modules > controllers > actions
        zendUrl.setHierarchy(
        {
            "default": { 
                "index":[],
    	        "public": [],
            }
            "ecommerce", {
                "products":["get", "remove", edit"],
                "games":["get", "add"],
            }
        });
    }

Then use it !
Example :

    myApp.controller(function productsController($scope, zendUrl) {
        $scope.fetchProducts = function() {
            $http.get(zendUrl({module:"ecommerce", controller:"products", action:"get"})).then(
                function(response) {
                     var list = response.data;
                     $scope.listProducts = list;
                });
            }
        });
        
