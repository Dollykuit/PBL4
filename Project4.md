# Project 4
## Step 1 - Install NodeJs

The below cmdlet updates Ubuntu

    sudo apt update
    
 <img width="960" alt="Screenshot 2022-03-22 010003" src="https://user-images.githubusercontent.com/98477745/159386935-97eb0eae-6141-4fa0-b585-24d0402bf53f.png">

Upgraded Ubuntu with the below cmdlet
 
    sudo apt upgrade
  
  <img width="945" alt="Screenshot 2022-03-22 011008" src="https://user-images.githubusercontent.com/98477745/159387705-ba6f9465-6964-44b5-b70a-525ade7b71ca.png">

 Installed NodeJs
 
    sudo apt install -y nodejs
   <img width="960" alt="Screenshot 2022-03-22 011532" src="https://user-images.githubusercontent.com/98477745/159388122-bf3e2519-e338-46cb-9a40-4c15d5d815e8.png">

**Step 2** : Install MongoDB
          
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    
    
<img width="960" alt="Screenshot 2022-03-22 013005" src="https://user-images.githubusercontent.com/98477745/159389475-ffec2b48-d58a-4fdb-bfee-edd3d6bacabf.png">


echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

Installed Mongodb using the below:

    sudo apt install -y mongodb
<img width="955" alt="Screenshot 2022-03-22 014048" src="https://user-images.githubusercontent.com/98477745/159390427-c6e56284-0674-4c71-badb-3ad748c2cee5.png">

Started mongodb server using the below:

    sudo service mongodb start
    
Verified the service was up and running using the below

    Sudo systemctl status mongodb
    
  <img width="914" alt="Screenshot 2022-03-22 014752" src="https://user-images.githubusercontent.com/98477745/159391037-19b0c6e1-1113-48f8-b087-2dd8089c437f.png">

Installed a node package manager

    sudo apt install -y npm
    
 <img width="958" alt="Screenshot 2022-03-22 020006" src="https://user-images.githubusercontent.com/98477745/159392299-03b15540-6489-473a-a689-543c94a5fd48.png">
 
  Installed a body-parser package to help process JSON files passed in requests to server
  
    sudo npm install body-parser
 
 <img width="934" alt="Screenshot 2022-03-22 020327" src="https://user-images.githubusercontent.com/98477745/159392586-3a0ca9be-fff8-4acd-b57f-29e3a6e5ab99.png">
 
Created a folder named 'Books' and changed directory to 'Books'

     mkdir Books && cd Books 

<img width="890" alt="Screenshot 2022-03-22 020924" src="https://user-images.githubusercontent.com/98477745/159393953-6007a3b2-4056-4c37-9c37-2a738efcb307.png">

In the Books directory, an npm project was initialized

     npm init
    
 <img width="960" alt="Screenshot 2022-03-22 021405" src="https://user-images.githubusercontent.com/98477745/159394436-38a4885f-7764-48dc-b56f-de0caf8c85f5.png">
 
 Added a file to the directory 'server.js' with the cmdlet below
 
    vi server.js
    
  var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});


<img width="960" alt="Screenshot 2022-03-22 022429" src="https://user-images.githubusercontent.com/98477745/159395510-8d69eb27-36e2-4576-a813-f2e87686dc4f.png">

**Step 3** Install Express and set up Routes to the server

Installed the mongoose package for express framework

    sudo npm install express mongoose
    
 
  <img width="833" alt="Screenshot 2022-03-22 024633" src="https://user-images.githubusercontent.com/98477745/159397770-5ed6a501-1d14-4df7-b55d-ecdb63f5aaa0.png">

Created a folder 'apps' and in the folder, we created a file 'routes.js'

    mkdir apps && cd apps
    
    vi routes.js
    
  We added the below code to the 'routes.js' file 
  
  var Book = require('./models/book');
module.exports = function(app) {
  app.get('/book', function(req, res) {
    Book.find({}, function(err, result) {
      if ( err ) throw err;
      res.json(result);
    });
  }); 
  app.post('/book', function(req, res) {
    var book = new Book( {
      name:req.body.name,
      isbn:req.body.isbn,
      author:req.body.author,
      pages:req.body.pages
    });
    book.save(function(err, result) {
      if ( err ) throw err;
      res.json( {
        message:"Successfully added book",
        book:result
      });
    });
  });
  app.delete("/book/:isbn", function(req, res) {
    Book.findOneAndRemove(req.query, function(err, result) {
      if ( err ) throw err;
      res.json( {
        message: "Successfully deleted the book",
        book: result
      });
    });
  });
  var path = require('path');
  app.get('*', function(req, res) {
    res.sendfile(path.join(__dirname + '/public', 'index.html'));
  });
};
   
   
<img width="960" alt="Screenshot 2022-03-22 025829" src="https://user-images.githubusercontent.com/98477745/159399296-92ea0ce4-575a-491f-8dcc-3287a3e463d2.png">

**Step 4** Access the routes with AngularJS

We changed to the 'Books' directory

    cd ../..
    
Then created a folder 'public'

    mkdir public && cd public
    
Created a file 'script.js'

    vi script.js
    
  then pasted the below codes in the 'script.js'
  
 var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
  $scope.add_book = function() {
    var body = '{ "name": "' + $scope.Name + 
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author + 
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});



 <img width="960" alt="Screenshot 2022-03-22 031316" src="https://user-images.githubusercontent.com/98477745/159400942-e0b27a4d-9df0-4524-aecb-175efed5d73d.png">
 
  created an 'index.html' in the 'public' directory
 
    vi index.html
    
  Then pasted the below code:
  
  <!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>

        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>

          <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>


<img width="960" alt="Screenshot 2022-03-22 032509" src="https://user-images.githubusercontent.com/98477745/159402129-849cb99e-838d-4bde-bccc-f6a50c5e95cd.png">

Changed the directory back to the 'books' directory    

      cd..
      
      
 Started the node server 
 

    node server.js
    
   Created a custom TCP port 3300 in the security group of the AWS EC2 instance
    
    
    
<img width="960" alt="Screenshot 2022-03-22 154531" src="https://user-images.githubusercontent.com/98477745/159526081-7fa286c2-b19e-4131-a45c-8b3e8e04c57a.png">

Did a test to see what the server return locally:

    curl -s http://localhost:3300



  <img width="960" alt="Screenshot 2022-03-22 160526" src="https://user-images.githubusercontent.com/98477745/159526548-0f1cc710-80f0-44e9-ad19-519f4a175bad.png">
  
  Accessed the app on the browser which works perfectly.
  
  

 
<img width="960" alt="Screenshot 2022-03-22 153709" src="https://user-images.githubusercontent.com/98477745/159527403-aa5fd3a7-fb99-473a-95c1-7b02a6f8f2d6.png">



