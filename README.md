Angular JS: an overview
=================================================
This example is upgrade of <b>angular js</b> tutorial from <b>[Tableless](http://tableless.com.br/criando-uma-aplicacao-simples-com-angularjs/#.UlnWzGSLIpQ)</b> by <b>[Davi Ferreira](http://tableless.com.br/?author=7)</b>. Features added in the code: Filter, Delete and Edit Products, complete crud.

Brunch.io
-----------------------------

<code>npm install -g brunch</code>

<code>ng-controller (ng-controller="myController")</code>

<code>ng-model (ng-model="item.name")</code>

<code>ng-view (ng-view)</code>

<code>ng-click (ng-click="myFunction()")</code>

<code>ng-repeat (ng-repeat="item in itens")</code>

<code>ng-hide|show (ng-hide="boolean")</code>
<code>ng-href (ng-href="link")</code>

<code>ng-init (ng-init="expression")</code>

<code>ng-readonly (ng-readonly="expression")</code>

<code>ng-disabled (ng-disabled="expression")</code>

See [Angular JS Cheat Sheet](http://www.cheatography.com/proloser/cheat-sheets/angularjs/).

Hello World
-----------------------------------
Below the basic example with angular js:

<pre>
	&lt;html ng-app&gt;
		&lt;head&gt;
			&lt;title&gtBasic Example with Angular JS &lt;/title&gt;
			&lt;script src="js/libs/angular-1.0.1.min.js"&gt;&lt;/script&gt;
		&lt;/head&gt;
		&lt;body&gt;
			&lt;input type="text" ng-model="name" placeholder="Type your name"&gt;
        	&lt;p&gt;Hello {{ name }} !&lt;/p&gt;
		&lt;/body&gt;
	&lt;html&gt;
</pre>

See [JSFiddle](http://jsfiddle.net/jM2TL/3/).

List Products in Controller
-----------------------------------
Store products in items model defined by <b>controller</b>:

<pre>
	function ListProductsController($scope) {
    	$scope.items = [
        	{product: 'Milk', amount: 2, purchased: false},
        	{product: 'Beer', amount: 12, purchased: false}
    	];
	}
</pre>

Now, list products with http request to return items json:

<pre>
	function ListProductsController($scope) {
		$scope.fetchProductsList = function() {
    		$http.get('http://www.url.com/products').success(function(products){
        		$scope.items = products;
    		});
		}
	}
</pre>

List Products in View
-----------------------------------
Show products in <b>view</b>:

![List Products](https://github.com/tiagobarreto/simple-crud-angular-js/blob/master/img/docs/list-products.png)

<pre>
	&lt;div ng-controller="ListaComprasController"&gt;
		&lt;table&gt;
  			&lt;thead&gt;
    			&lt;tr&gt;
      				&lt;th&gt;Produto&lt;/th&gt;
      				&lt;th&gt;Quantidade&lt;/th&gt;
    			&lt;/tr&gt;
  			&lt;/thead&gt;
  			&lt;tbody&gt;
    			&lt;tr ng-repeat="item in itens"&gt;
      				&lt;td&gt;&lt;strong&gt;{{ item.produto }}&lt;/strong&gt;&lt;/td&gt;
      				&lt;td&gt;{{ item.quantidade }}&lt;/td&gt;
    			&lt;/tr&gt;
  			&lt;/tbody&gt;
		&lt;/table&gt;
	&lt;/div&gt;
</pre>

Filter Products in View
-----------------------------------
Added the filter attr in the ng-repeat to enabled filter:

![Filter Product](https://github.com/tiagobarreto/simple-crud-angular-js/blob/master/img/docs/filter-products.png)

<code>&lt;tr ng-repeat="item in items | filter:search"&gt;</code>

Also added a input text to search products:

<code>&lt;input type="search" ng-model="search" placeholder="Search by…"&gt;</code>


Add Products
-----------------------------------
Add products in <b>view</b>:

<pre>
	&lt;form name="products"&gt;
    	&lt;input type="text" ng-model="item.product"&gt;
    	&lt;input type="number" ng-model="item.amount"&gt;
    	&lt;button ng-click="addItem()">add item&lt;/button&gt;
	&lt;/form&gt;
</pre>

Functions in <b>controller</b>:

<code>Add item in the items array</code>
<pre>
	$scope.addItem = function () {
    	$scope.items.push({product: $scope.item.product, amount: $scope.item.amount, purchase: false});
	};
</pre>

<code>Add item with HTTP Request</code>

<pre>
	$scope.addItem = function(product) {
    	$http.post('/products/', product).success(function(product) {
        	toastr.success("Item added.");
        	$scope.items.push(product);
     	}).error(function(data) {
        	toastr.error("Fail on adding product.");
    	});
 	};
</pre>

Remove Products
-----------------------------------
Remove products in <b>view</b>:

<pre>
	&lt;button class="btn btn-danger btn-small" ng-click="deleteItem($index)"&gt;
    	&lt;i class="icon-trash icon-white"&gt;&lt;/i&gt; remove
	&lt;/button&gt;
</pre>

Function to delete item in <b>Controller</b>

<pre>
	$scope.deleteItem = function(index){
    	$scope.items.splice(index, 1);
	};
</pre>


Edit Products
-----------------------------------
![Edit Product](https://github.com/tiagobarreto/simple-crud-angular-js/blob/master/img/docs/edit-products.png)

Edit products used the main button from form to change the product with the <code>ng-hide</code> and <code>ng-show</code> in view:

<pre>
	$scope.editItem = function(index){
    	$scope.item = $scope.items[index];
	};
</pre>

Routes Application
-----------------------------------
<pre>
	var application = {};

	var App = angular.module('application');

	App.config(['$routeProvider', function ($routeProvider) {
    	$routeProvider
        	.when('/products', { templateUrl: 'views/products/list.html', controller: ProductsControllers })
        	.when(<code>'…'</code>, { templateUrl: <code>'…'</code>, controller: <code>...</code> });
	}]);
</pre>

Libs used by example
--------------------------------------------
   * <b>Bootstrap</b>
      * Version: [3.0.0](https://github.com/twbs/bootstrap/archive/v3.0.0.zip)
 
   * <b>Toastr</b>
      * Version: [2.0.0](https://github.com/CodeSeven/toastr/blob/master/toastr.js)
      
   * <b>jQuery</b>
      * Version: [2.2.0](http://code.jquery.com/jquery-2.2.0.js)

More Details
--------------------------------------------
   * <b>Blog</b>
      * [http://www.tiagobarreto.com/simples-aplicacao-em-angularjs/](http://www.tiagobarreto.com/simples-aplicacao-em-angularjs/)
      
Other projects
--------------------------------------------
   * [Simple Crud with Elixir / Phoenix / Angular JS](https://github.com/tiagobarreto/simple-crud-phoenix)
   * [Simple Crud with Spring MVC / Angular JS](https://github.com/tiagobarreto/simple-app-spring-mvc-angularjs)
