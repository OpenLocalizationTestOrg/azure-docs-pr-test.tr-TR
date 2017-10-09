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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="d27aa-103">MongoDB, Express, AngularJS ve Node.js (ortalama) yığın azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d27aa-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="d27aa-104">Bu öğretici azure'da bir Linux VM üzerinde tooimplement bir MongoDB, Express, AngularJS ve Node.js (ortalama) nasıl yığın gösterir.</span><span class="sxs-lookup"><span data-stu-id="d27aa-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="d27aa-105">oluşturduğunuz hello ortalama yığın ekleme, silme ve bir veritabanında books listeleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="d27aa-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="d27aa-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d27aa-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d27aa-107">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d27aa-107">Create a Linux VM</span></span>
> * <span data-ttu-id="d27aa-108">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="d27aa-108">Install Node.js</span></span>
> * <span data-ttu-id="d27aa-109">MongoDB yükleme ve başlangıç sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d27aa-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="d27aa-110">Hızlı yükleme ve yolları toohello sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d27aa-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="d27aa-111">AngularJS erişim hello yollar</span><span class="sxs-lookup"><span data-stu-id="d27aa-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="d27aa-112">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d27aa-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d27aa-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="d27aa-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d27aa-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="d27aa-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d27aa-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d27aa-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="d27aa-116">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d27aa-116">Create a Linux VM</span></span>

<span data-ttu-id="d27aa-117">Merhaba bir kaynak grubu oluşturmak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komut ve hello ile bir Linux VM oluşturma [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d27aa-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="d27aa-118">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d27aa-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d27aa-119">Merhaba aşağıdaki örnek kullanan bir kaynak grubu adında hello Azure CLI toocreate *myResourceGroupMEAN* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="d27aa-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="d27aa-120">Bir VM adlandırılmış oluşturulur *myVM* zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları.</span><span class="sxs-lookup"><span data-stu-id="d27aa-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="d27aa-121">toouse belirli bir anahtarları, kullanım hello--ssh-anahtar-değer seçeneği ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d27aa-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

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

<span data-ttu-id="d27aa-122">Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:</span><span class="sxs-lookup"><span data-stu-id="d27aa-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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
<span data-ttu-id="d27aa-123">Merhaba not edin `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="d27aa-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="d27aa-124">Kullanılan tooaccess hello VM adresidir.</span><span class="sxs-lookup"><span data-stu-id="d27aa-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="d27aa-125">Kullanım hello aşağıdaki toocreate hello VM ile SSH oturumu bir komutu.</span><span class="sxs-lookup"><span data-stu-id="d27aa-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="d27aa-126">Toouse hello doğru ortak IP adresi emin olun.</span><span class="sxs-lookup"><span data-stu-id="d27aa-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="d27aa-127">Örneğimizde yukarıda bizim IP adresi 13.72.77.9 oluştu.</span><span class="sxs-lookup"><span data-stu-id="d27aa-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="d27aa-128">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="d27aa-128">Install Node.js</span></span>

<span data-ttu-id="d27aa-129">[Node.js](https://nodejs.org/en/) Chrome'nın V8 JavaScript altyapısında oluşturulmuş bir JavaScript Çalışma Zamanı Modülü.</span><span class="sxs-lookup"><span data-stu-id="d27aa-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="d27aa-130">Node.js Öğreticisi bu tooset hello Express yönlendirir ve AngularJS denetleyicisi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d27aa-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="d27aa-131">Merhaba SSH ile açılmış hello bash kabuğunda kullanarak VM, Node.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="d27aa-132">MongoDB yükleme ve başlangıç sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d27aa-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="d27aa-133">[MongoDB](http://www.mongodb.com) esnek, JSON benzeri belgelerde verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="d27aa-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="d27aa-134">Bir veritabanı alanları belge toodocument değişebilir ve veri yapısı zaman içinde değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d27aa-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="d27aa-135">Bizim örnek uygulama için rehberi adı, ISBN numarası, yazar ve sayfa sayısını içeren kitap kayıtları tooMongoDB ekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="d27aa-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="d27aa-136">Merhaba SSH ile açılmış hello bash kabuğunda kullanarak VM hello MongoDB anahtarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d27aa-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="d27aa-137">Merhaba Paket Yöneticisi hello anahtarı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="d27aa-138">MongoDB yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="d27aa-139">Merhaba sunucu başlatın.</span><span class="sxs-lookup"><span data-stu-id="d27aa-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="d27aa-140">Ayrıca tooinstall hello ihtiyacımız [gövde ayrıştırıcı](https://www.npmjs.com/package/body-parser-json) paket toohelp bize işlem JSON geçirilen istekleri toohello Server'da hello.</span><span class="sxs-lookup"><span data-stu-id="d27aa-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="d27aa-141">Merhaba npm Paket Yöneticisi'ni yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="d27aa-142">Merhaba gövde ayrıştırıcı paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="d27aa-143">Adlı bir klasör oluşturun *Books* ve adlı bir dosya tooit ekleyin *server.js* hello web sunucusu hello yapılandırması içerir.</span><span class="sxs-lookup"><span data-stu-id="d27aa-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

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

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="d27aa-144">Hızlı yükleme ve yolları toohello sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d27aa-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="d27aa-145">[Express](https://expressjs.com) web ve mobil uygulamaları için özellikler sağlayan bir minimal ve esnek Node.js web uygulama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="d27aa-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="d27aa-146">Bu öğretici toopass defteri bilgi tooand bizim MongoDB veritabanından Express kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d27aa-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="d27aa-147">[Mongoose](http://mongoosejs.com) uygulama verilerinizi düz İleri, şema tabanlı çözüm toomodel sağlar.</span><span class="sxs-lookup"><span data-stu-id="d27aa-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="d27aa-148">Bu öğretici tooprovide mongoose kullanılan hello veritabanı için bir kitap şema.</span><span class="sxs-lookup"><span data-stu-id="d27aa-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="d27aa-149">Express ve Mongoose yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="d27aa-150">Merhaba, *Books* klasörünü adlı bir klasör oluşturun *uygulamaları* ve adlı bir dosya eklemek *routes.js* tanımlanan yollar ile Merhaba express.</span><span class="sxs-lookup"><span data-stu-id="d27aa-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

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

3. <span data-ttu-id="d27aa-151">Merhaba, *uygulamaları* klasörü, adlı bir klasör oluşturun *modelleri* ve adlı bir dosya eklemek *book.js* tanımlanan hello kitap modeli yapılandırmasına sahip.</span><span class="sxs-lookup"><span data-stu-id="d27aa-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

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

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="d27aa-152">AngularJS erişim hello yollar</span><span class="sxs-lookup"><span data-stu-id="d27aa-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="d27aa-153">[AngularJS](https://angularjs.org) dinamik görünümleri, web uygulamaları oluşturmak için bir web çerçevesidir sağlar.</span><span class="sxs-lookup"><span data-stu-id="d27aa-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="d27aa-154">Bu öğreticide AngularJS tooconnect web sayfamızı hızlı kullanın ve kitap Veritabanımıza eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d27aa-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="d27aa-155">Merhaba dizini çok değiştirmek yedekleme*Books* (`cd ../..`) ve ardından adlı bir klasör oluşturun *ortak* ve adlı bir dosya eklemek *script.js* hello denetleyicisiyle tanımlanan yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="d27aa-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="d27aa-156">Merhaba, *ortak* klasörü, adlı bir dosya oluşturun *index.html* tanımlanan hello web sayfası.</span><span class="sxs-lookup"><span data-stu-id="d27aa-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

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

##  <a name="run-hello-application"></a><span data-ttu-id="d27aa-157">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d27aa-157">Run hello application</span></span>

1. <span data-ttu-id="d27aa-158">Merhaba dizini çok değiştirmek yedekleme*Books* (`cd ..`) ve şu komutu çalıştırarak hello sunucu başlatın:</span><span class="sxs-lookup"><span data-stu-id="d27aa-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="d27aa-159">VM hello için kaydedilmiş bir web tarayıcısı toohello adresini açın.</span><span class="sxs-lookup"><span data-stu-id="d27aa-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="d27aa-160">Örneğin, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="d27aa-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="d27aa-161">Sayfa aşağıdaki hello gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d27aa-161">You should see something like hello following page:</span></span>

    ![Kayıt defteri](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="d27aa-163">Veri hello kutularındaki girip tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d27aa-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="d27aa-164">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d27aa-164">For example:</span></span>

    ![Kitap kaydı ekleme](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="d27aa-166">Merhaba sayfa yenilendikten sonra bu sayfa şöyle görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d27aa-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Liste defteri kayıtları](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="d27aa-168">Tıklattığınız **silmek** ve hello kitap kaydı hello veritabanından kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d27aa-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d27aa-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d27aa-169">Next steps</span></span>

<span data-ttu-id="d27aa-170">Bu öğreticide, bir ortalama kullanarak kitap kaydı ve bir web uygulaması oluşturan bir Linux VM yığında.</span><span class="sxs-lookup"><span data-stu-id="d27aa-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="d27aa-171">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="d27aa-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d27aa-172">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d27aa-172">Create a Linux VM</span></span>
> * <span data-ttu-id="d27aa-173">Node.js yükleme</span><span class="sxs-lookup"><span data-stu-id="d27aa-173">Install Node.js</span></span>
> * <span data-ttu-id="d27aa-174">MongoDB yükleme ve başlangıç sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d27aa-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="d27aa-175">Hızlı yükleme ve yolları toohello sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d27aa-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="d27aa-176">AngularJS erişim hello yollar</span><span class="sxs-lookup"><span data-stu-id="d27aa-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="d27aa-177">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d27aa-177">Run hello application</span></span>

<span data-ttu-id="d27aa-178">Toohello sonraki öğretici toolearn nasıl ilerlemek SSL sertifikaları web sunucularıyla toosecure.</span><span class="sxs-lookup"><span data-stu-id="d27aa-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d27aa-179">SSL ile güvenli web sunucusu</span><span class="sxs-lookup"><span data-stu-id="d27aa-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
