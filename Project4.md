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
    
    
 
 

   



  



    



