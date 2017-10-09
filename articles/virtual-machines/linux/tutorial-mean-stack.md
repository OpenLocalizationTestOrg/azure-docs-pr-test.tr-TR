---
title: "aaaCreate bir ORTALAMASI azure'da bir Linux VM yığında | Microsoft Docs"
description: "Azure'da bir Linux VM üzerinde toocreate bir MongoDB, Express, AngularJS ve Node.js (ortalama) nasıl yığın öğrenin."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>MongoDB, Express, AngularJS ve Node.js (ortalama) yığın azure'da bir Linux VM oluşturma

Bu öğretici azure'da bir Linux VM üzerinde tooimplement bir MongoDB, Express, AngularJS ve Node.js (ortalama) nasıl yığın gösterir. oluşturduğunuz hello ortalama yığın ekleme, silme ve bir veritabanında books listeleme sağlar. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Linux VM oluşturma
> * Node.js yükleme
> * MongoDB yükleme ve başlangıç sunucusunu ayarlama
> * Hızlı yükleme ve yolları toohello sunucusunu ayarlama
> * AngularJS erişim hello yollar
> * Merhaba uygulamayı çalıştırın

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Linux VM oluşturma

Merhaba bir kaynak grubu oluşturmak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komut ve hello ile bir Linux VM oluşturma [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.

Merhaba aşağıdaki örnek kullanan bir kaynak grubu adında hello Azure CLI toocreate *myResourceGroupMEAN* hello içinde *eastus* konumu. Bir VM adlandırılmış oluşturulur *myVM* zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları. toouse belirli bir anahtarları, kullanım hello--ssh-anahtar-değer seçeneği ayarlayın.

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir: 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
Merhaba not edin `publicIpAddress`. Kullanılan tooaccess hello VM adresidir.

Kullanım hello aşağıdaki toocreate hello VM ile SSH oturumu bir komutu. Toouse hello doğru ortak IP adresi emin olun. Örneğimizde yukarıda bizim IP adresi 13.72.77.9 oluştu.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Node.js yükleme

[Node.js](https://nodejs.org/en/) Chrome'nın V8 JavaScript altyapısında oluşturulmuş bir JavaScript Çalışma Zamanı Modülü. Node.js Öğreticisi bu tooset hello Express yönlendirir ve AngularJS denetleyicisi kullanılır.

Merhaba SSH ile açılmış hello bash kabuğunda kullanarak VM, Node.js yükleyin.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>MongoDB yükleme ve başlangıç sunucusunu ayarlama
[MongoDB](http://www.mongodb.com) esnek, JSON benzeri belgelerde verileri depolar. Bir veritabanı alanları belge toodocument değişebilir ve veri yapısı zaman içinde değiştirilebilir. Bizim örnek uygulama için rehberi adı, ISBN numarası, yazar ve sayfa sayısını içeren kitap kayıtları tooMongoDB ekliyoruz. 

1. Merhaba SSH ile açılmış hello bash kabuğunda kullanarak VM hello MongoDB anahtarı ayarlayın.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Merhaba Paket Yöneticisi hello anahtarı ile güncelleştirin.
  
    ```bash
    sudo apt-get update
    ```

3. MongoDB yükleyin.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Merhaba sunucu başlatın.

    ```bash
    sudo service mongodb start
    ```

5. Ayrıca tooinstall hello ihtiyacımız [gövde ayrıştırıcı](https://www.npmjs.com/package/body-parser-json) paket toohelp bize işlem JSON geçirilen istekleri toohello Server'da hello.

    Merhaba npm Paket Yöneticisi'ni yükleyin.

    ```bash
    sudo apt-get install npm
    ```

    Merhaba gövde ayrıştırıcı paketini yükleyin.
    
    ```bash
    sudo npm install body-parser
    ```

6. Adlı bir klasör oluşturun *Books* ve adlı bir dosya tooit ekleyin *server.js* hello web sunucusu hello yapılandırması içerir.

    ```node.js
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
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a>Hızlı yükleme ve yolları toohello sunucusunu ayarlama

[Express](https://expressjs.com) web ve mobil uygulamaları için özellikler sağlayan bir minimal ve esnek Node.js web uygulama çerçevesidir. Bu öğretici toopass defteri bilgi tooand bizim MongoDB veritabanından Express kullanılır. [Mongoose](http://mongoosejs.com) uygulama verilerinizi düz İleri, şema tabanlı çözüm toomodel sağlar. Bu öğretici tooprovide mongoose kullanılan hello veritabanı için bir kitap şema.

1. Express ve Mongoose yükleyin.

    ```bash
    sudo npm install express mongoose
    ```

2. Merhaba, *Books* klasörünü adlı bir klasör oluşturun *uygulamaları* ve adlı bir dosya eklemek *routes.js* tanımlanan yollar ile Merhaba express.

    ```node.js
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
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. Merhaba, *uygulamaları* klasörü, adlı bir klasör oluşturun *modelleri* ve adlı bir dosya eklemek *book.js* tanımlanan hello kitap modeli yapılandırmasına sahip.  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a>AngularJS erişim hello yollar

[AngularJS](https://angularjs.org) dinamik görünümleri, web uygulamaları oluşturmak için bir web çerçevesidir sağlar. Bu öğreticide AngularJS tooconnect web sayfamızı hızlı kullanın ve kitap Veritabanımıza eylemleri gerçekleştirin.

1. Merhaba dizini çok değiştirmek yedekleme*Books* (`cd ../..`) ve ardından adlı bir klasör oluşturun *ortak* ve adlı bir dosya eklemek *script.js* hello denetleyicisiyle tanımlanan yapılandırması.

    ```node.js
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
    ```
    
2. Merhaba, *ortak* klasörü, adlı bir dosya oluşturun *index.html* tanımlanan hello web sayfası.

    ```html
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
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

1. Merhaba dizini çok değiştirmek yedekleme*Books* (`cd ..`) ve şu komutu çalıştırarak hello sunucu başlatın:

    ```bash
    nodejs server.js
    ```

2. VM hello için kaydedilmiş bir web tarayıcısı toohello adresini açın. Örneğin, *http://13.72.77.9:3300*. Sayfa aşağıdaki hello gibi bir şey görmeniz gerekir:

    ![Kayıt defteri](media/tutorial-mean/meanstack-init.png)

3. Veri hello kutularındaki girip tıklatın **Ekle**. Örneğin:

    ![Kitap kaydı ekleme](media/tutorial-mean/meanstack-add.png)

4. Merhaba sayfa yenilendikten sonra bu sayfa şöyle görmeniz gerekir:

    ![Liste defteri kayıtları](media/tutorial-mean/meanstack-list.png)

5. Tıklattığınız **silmek** ve hello kitap kaydı hello veritabanından kaldırın.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir ortalama kullanarak kitap kaydı ve bir web uygulaması oluşturan bir Linux VM yığında. Şunları öğrendiniz:

> [!div class="checklist"]
> * Linux VM oluşturma
> * Node.js yükleme
> * MongoDB yükleme ve başlangıç sunucusunu ayarlama
> * Hızlı yükleme ve yolları toohello sunucusunu ayarlama
> * AngularJS erişim hello yollar
> * Merhaba uygulamayı çalıştırın

Toohello sonraki öğretici toolearn nasıl ilerlemek SSL sertifikaları web sunucularıyla toosecure.

> [!div class="nextstepaction"]
> [SSL ile güvenli web sunucusu](tutorial-secure-web-server.md)
