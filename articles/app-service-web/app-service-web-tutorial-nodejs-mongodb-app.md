---
title: "aaaBuild azure'da Node.js ve MongoDB bir web uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooget Azure'da çalışan bir Node.js uygulaması ile bağlantı tooa Cosmos DB veritabanı ile MongoDB bağlantı dizesi."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Azure'da Node.js ve MongoDB bir web uygulaması oluşturma

Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar. Bu öğretici nasıl toocreate bir Node.js web uygulaması Azure ve tooa MongoDB veritabanı bağlantı gösterir. İşiniz bittiğinde, ortalama uygulama (MongoDB, Express, AngularJS ve Node.js) çalışan bir gerekir, [Azure App Service](app-service-web-overview.md). Kolaylık olması için hello örnek uygulama hello kullanır [MEAN.js web çerçevesi](http://meanjs.org/).

![Azure App Service’te çalışan MEAN.js uygulaması](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Öğrenecekleriniz:

> [!div class="checklist"]
> * MongoDB veritabanı oluşturma
> * Bir Node.js uygulaması tooMongoDB Bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın
> * Azure Stream tanılama günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

1. [Git'i yükleyin](https://git-scm.com/)
1. [Node.js ve NPM'yi yükleyin](https://nodejs.org/)
1. [Gulp.js yükleme](http://gulpjs.com/) (gerektirdiği [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Yükleyip çalıştırabilirsiniz MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Test yerel MongoDB

Açık hello terminal penceresi ve `cd` toohello `bin` MongoDB yüklemenizin dizin. Bu bir terminal penceresi toorun Bu öğreticide tüm hello komutlarını kullanabilirsiniz.

Çalıştırma `mongo` hello terminal tooconnect tooyour yerel MongoDB Server.

```bash
mongo
```

Bağlantı başarılı olursa, MongoDB veritabanı zaten çalışıyor. Aksi takdirde, yerel MongoDB veritabanı hello adımları izleyerek başlatıldığından emin olun [MongoDB Community Edition yüklemek](https://docs.mongodb.com/manual/administration/install-community/). Genellikle, MongoDB yüklenir, ancak yine de toostart gerekir çalıştırarak `mongod`. 

Bitirdiğinizde, MongoDB veritabanı sınama, yazın `Ctrl+C` hello terminal içinde. 

## <a name="create-local-nodejs-app"></a>Yerel Node.js uygulaması oluşturma

Bu adımda, hello yerel Node.js projesi ayarlayın.

### <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Merhaba terminal penceresinde `cd` tooa çalışma dizini.  

Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Bu örnek depo hello bir kopyasını içeren [MEAN.js depo](https://github.com/meanjs/mean). Uygulama hizmeti üzerinde değiştirilmiş toorun olduğu (Merhaba MEAN.js depo daha fazla bilgi için bkz: [Benioku dosyasını](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Aşağıdaki komutları tooinstall hello gerekli paketleri hello çalıştırın ve hello uygulamasını başlatın.

```bash
cd meanjs
npm install
npm start
```

Merhaba uygulama tam olarak yüklendiğinde iletiden benzeri toohello bakın:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Bir tarayıcıda toohttp://localhost:3000 gidin. Tıklatın **kaydolun** hello üst menü ve test kullanıcısı oluşturma. 

Merhaba MEAN.js örnek uygulamanın kullanıcı verilerini hello veritabanında depolar. Kullanıcı oluşturma ve oturum açma başarılı olursa, uygulamanızın veri toohello yerel MongoDB veritabanı yazıyor.

![MEAN.js tooMongoDB başarıyla bağlanır.](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Seçin **yönetici > yönetmek makaleleri** tooadd bazı makaleler.

herhangi bir zamanda Node.js toostop basın `Ctrl+C` hello terminal içinde. 

## <a name="create-production-mongodb"></a>Üretim MongoDB oluşturma

Bu adımda, Azure MongoDB veritabanı oluşturun. Uygulamanızı dağıtılan tooAzure olduğunda, bu bulut veritabanını kullanır.

MongoDB için Bu öğretici kullanır [Azure Cosmos DB](/azure/documentdb/). Cosmos DB MongoDB istemci bağlantılarını destekler.

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Uygulamanızı Azure'da hello Azure CLI 2.0 toocreate hello gerekli kaynakları toohost kullanacaksınız. Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Merhaba aşağıdaki örnekte bir kaynak grubu hello Batı Avrupa bölgede oluşturur.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Kullanım hello [az appservice listesi-konumları](/cli/azure/appservice#list-locations) Azure CLI toolist kullanılabilir konumlarını komutu. 

### <a name="create-a-cosmos-db-account"></a>Cosmos DB hesabı oluşturma

Cosmos DB hesabı ile Merhaba oluşturma [az cosmosdb oluşturma](/cli/azure/cosmosdb#create) komutu.

Hello hello için benzersiz bir Cosmos DB ad yerine komutu, aşağıdaki  *\<cosmosdb_name >* yer tutucu. Bu ad hello Cosmos DB endpoint hello parçası olarak kullanılır `https://<cosmosdb_name>.documents.azure.com/`, hello adı toobe benzersiz Azure içindeki tüm Cosmos DB hesaplar arasında olmalıdır. Merhaba adı yalnızca küçük harf, sayı ve hello tire (-) karakterini içermelidir ve 3-50 karakter uzunluğunda olmalıdır.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Merhaba *--tür MongoDB* parametresi MongoDB istemci bağlantıları sağlar.

Merhaba Cosmos DB hesabı oluşturulduğunda, hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>Uygulama tooproduction MongoDB Bağlan

Bu adımda, MongoDB bağlantı dizesi kullanarak oluşturduğunuz MEAN.js örnek uygulama toohello Cosmos DB veritabanınız bağlayın. 

### <a name="retrieve-hello-database-key"></a>Merhaba veritabanı anahtarı alma

tooconnect toohello Cosmos DB veritabanı hello veritabanı anahtarı gerekir. Kullanım hello [az cosmosdb listesi anahtarlar](/cli/azure/cosmosdb#list-keys) komutu tooretrieve hello birincil anahtar.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Merhaba değerini kopyalayın `primaryMasterKey`. Bu bilgiler sonraki adımda hello gerekir.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Node.js uygulamanızda Hello bağlantı dizesini yapılandırma

MEAN.js deponuz açmak _config/env/production.js_.

Merhaba, `db` nesne, güncelleştirme hello değerini `uri`:

* Merhaba iki Değiştir  *\<cosmosdb_name >* Cosmos DB veritabanı adınız yer tutucularını.
* Hello yerine  *\<primary_master_key >* hello önceki adımda kopyaladığınız hello anahtarla yer tutucu.

Merhaba aşağıdaki kod gösterir hello `db` nesnesi:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Merhaba `ssl=true` seçeneği, çünkü gereklidir [Cosmos DB SSL gerekir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Yaptığınız değişiklikleri kaydedin.

### <a name="test-hello-application-in-production-mode"></a>Üretim modunda Hello uygulamayı test etme 

Toominify ve paket komut hello üretim ortamı için aşağıdaki hello çalıştırın. Bu işlem hello üretim ortamı tarafından gerek hello dosyaları oluşturur.

```bash
gulp prod
```

Komut toouse hello bağlantı dizesi, yapılandırdığınız aşağıdaki çalışma hello _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Node.js toorun hello üretim ortamında söyler hello ortam değişkenini ayarlar.  `node server.js`başlatır hello Node.js sunucusuyla `server.js` depo kök. Azure'da Node.js uygulamanızı nasıl yüklenir budur. 

Merhaba uygulama yüklendiğinde toomake hello üretim ortamında çalıştığından emin denetleyin:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Bir tarayıcıda toohttp://localhost:8443 gidin. Tıklatın **kaydolun** hello üst menü ve test kullanıcısı oluşturma. Başarılı bir kullanıcı oluşturma ve oturum açma, uygulamanızı Azure'da veri toohello Cosmos DB veritabanı yazıyor. 

Yazarak Hello terminal, Node.js durdurun `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Uygulama tooAzure dağıtma

Bu adımda, MongoDB bağlı Node.js uygulaması tooAzure uygulama hizmeti dağıtın.

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma

Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Merhaba aşağıdaki örnekte oluşturur adlı bir uygulama hizmeti planı _myAppServicePlan_ hello kullanarak **serbest** fiyatlandırma katmanı:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Uygulama hizmeti planı Hello oluşturulduğunda, hello Azure CLI bilgi benzer toohello aşağıdaki örneğine gösterir:

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Web uygulaması oluşturma

Hello bir web uygulaması oluşturma `myAppServicePlan` hello ile uygulama hizmeti planı [az webapp oluşturmak](/cli/azure/webapp#create) komutu. 

dağıtılan uygulama, bir barındırma kodunuzu toodeploy boşluk ve sizin için bir URL tooview hello sağlar hello web uygulamasını sağlar. Toocreate hello web uygulaması kullanın. 

Hello hello Değiştir komutu, aşağıdaki  *\<app_name >* yer tutucu benzersiz bir uygulama adına sahip. Merhaba adının toobe benzersiz Azure App Service'te tüm uygulamalarında gerekir böylece bu adı hello web uygulaması için hello varsayılan URL hello parçası olarak kullanılır. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a>Bir ortam değişkeni yapılandırın

Başlangıç Öğreticisi, sabit kodlanmış hello veritabanı bağlantı dizesinde önceki _config/env/production.js_. Mantığıyla en iyi güvenlik uygulaması, tookeep Git deponuzu dışında bu hassas verileri istiyor. Uygulamanız için Azure'da çalışan, bir ortam değişkeni kullanmanız.

Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ hello kullanarak [az webapp config appsettings güncelleştirme](/cli/azure/webapp/config/appsettings#update) komutu. 

Merhaba aşağıdaki örnek yapılandırır bir `MONGODB_URI` , Azure web uygulaması uygulama ayarı. Hello yerine  *\<app_name >*,  *\<cosmosdb_name >*, ve  *\<primary_master_key >* yer tutucuları.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

Bu uygulama ayarı ile erişim node.js kodu `process.env.MONGODB_URI`herhangi bir ortam değişkeni erişim gibi. 

Şimdi, değişiklikleri too_config/env/production.js_ komutu aşağıdaki hello ile geri:

```bash
git checkout -- .
```

Açık _config/env/production.js_ yeniden. Bu hello varsayılan MEAN.js uygulama zaten yapılandırılmış toouse hello Not `MONGODB_URI` oluşturduğunuz ortam değişkeni.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Yerel git dağıtımını yapılandırma 

Kullanım hello [az webapp dağıtım kullanıcısı ayarlanmadı](/cli/azure/webapp/deployment/user#set) toocreate kimlik bilgileri dağıtımı için komutu.

Uygulama tooAzure uygulama hizmeti FTP, yerel Git, GitHub, Visual Studio Team Services ve BitBucket dahil olmak üzere çeşitli yollarla dağıtabilirsiniz. FTP ve yerel Git için gerekli toohave dağıtım kullanıcı dağıtımınızı hello sunucu tooauthenticate üzerinde yapılandırılmış. Bu dağıtım kullanıcı hesabı düzeyi ve Azure abonelik hesabınızdan farklıdır. Yalnızca tooconfigure bu dağıtım kullanıcı kez gerekir.

Komut, aşağıdaki Hello yerine  *\<kullanıcı adı >* ve  *\<parola >* yeni bir kullanıcı adı ve parola ile. Merhaba kullanıcı adının benzersiz olması gerekir. Merhaba parola en az sekiz karakter uzunluğunda, iki üç öğeleri aşağıdaki hello olmalıdır: harf, sayı, simge. Alırsanız bir ` 'Conflict'. Details: 409` hata, değişiklik hello kullanıcı adı. ` 'Bad Request'. Details: 400` hatası alırsanız daha güçlü bir parola kullanın.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Kayıt hello kullanıcı adı ve parola hello uygulamayı dağıttığınızda daha sonraki adımlarda kullanılacak.

Kullanım hello [az webapp dağıtım kaynağı config-yerel-git](/cli/azure/webapp/deployment/source#config-local-git) komutu tooconfigure yerel Git erişim toohello Azure web uygulaması. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Merhaba dağıtım kullanıcı yapılandırıldığında, hello Azure CLI Azure web uygulamanız için hello dağıtım URL biçimi aşağıdaki hello gösterir:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Merhaba sonraki adımda kullanılacak şekilde hello terminal durumundan çıktı hello kopyalayın. 

### <a name="push-tooazure-from-git"></a>Anında iletme tooAzure Git

Bir Azure uzak tooyour yerel Git deposu ekleyin. 

```bash
git remote add azure <paste_copied_url_here> 
```

Toohello Azure uzak toodeploy Node.js uygulamanızı iletin. Merhaba dağıtım kullanıcının hello oluşturmanın bir parçası daha önce sağlanan hello parolası istenir. 

```bash
git push azure master
```

Dağıtım sırasında Azure App Service, ilerleme durumunu Git ile iletişim kurar.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

Merhaba dağıtım işleminin çalıştığını fark edebilirsiniz [Gulp](http://gulpjs.com/) sonra `npm install`. Uygulama hizmeti Gulp veya Grunt görevleri dağıtımı sırasında çalışmaz, bu örnek depo iki nedenle ek kendi kök dizin tooenable, dosyalarını: 

- _.Deployment_ -uygulama hizmeti toorun bu dosya söyler `bash deploy.sh` hello özel dağıtım komut dosyası olarak.
- _Deploy.sh_ -hello özel dağıtım komut dosyası. Merhaba dosya gözden geçirirseniz, çalıştığını görürsünüz `gulp prod` sonra `npm install` ve `bower install`. 

Bu yaklaşım tooadd herhangi adım tooyour Git tabanlı bir dağıtım kullanabilirsiniz. Uygulama hizmeti, herhangi bir noktada, Azure web uygulamanızın yeniden başlatırsanız, bu otomasyon görevleri yeniden değil.

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure web uygulaması Gözat 

Web tarayıcınız üzerinden dağıtılan toohello web uygulaması göz atın. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Tıklatın **kaydolun** hello üst menü ve sahte bir kullanıcı oluşturun. 

Başarılı ve hello uygulama otomatik olarak oturum açtığında kullanıcı sonra MEAN.js uygulamanızı Azure içinde oluşturulan toohello bağlantı toohello MongoDB (Cosmos DB) veritabanı yoktur. 

![Azure App Service’te çalışan MEAN.js uygulaması](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Seçin **yönetici > yönetmek makaleleri** tooadd bazı makaleler. 

**Tebrikler!** Azure App Service'te veri güdümlü bir Node.js uygulaması kullanıyorsunuz.

## <a name="update-data-model-and-redeploy"></a>Güncelleştirme veri modeli ve yeniden dağıtın

Bu adımda, hello değiştirmek `article` veri modeli ve değişiklik tooAzure yayımlayın.

### <a name="update-hello-data-model"></a>Güncelleştirme hello veri modeli

Açık _modules/articles/server/models/article.server.model.js_.

İçinde `ArticleSchema`, ekleme bir `String` adlı türü `comment`. İşiniz bittiğinde, şema kodunuzu aşağıdaki gibi görünmelidir:

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>Merhaba makaleleri kodunu güncelleştirin

Merhaba geri kalanı güncelleştirmek, `articles` toouse kod `comment`.

Beş dosyaları toomodify ihtiyacınız vardır: hello server denetleyicisi ve hello dört istemci görünümleri. 

Açık _modules/articles/server/controllers/articles.server.controller.js_.

Merhaba, `update` işlev, atama için ekleme `article.comment`. Merhaba aşağıdaki kod gösterir tamamlandı hello `update` işlevi:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Açık _modules/articles/client/views/view-article.client.view.html_.

Merhaba kapanış hemen `</section>` etiket, satır toodisplay aşağıdaki hello eklemek `comment` hello kalan hello makale verileri birlikte:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Açık _modules/articles/client/views/list-articles.client.view.html_.

Merhaba kapanış hemen `</a>` etiket, satır toodisplay aşağıdaki hello eklemek `comment` hello kalan hello makale verileri birlikte:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Açık _modules/articles/client/views/admin/list-articles.client.view.html_.

İç hello `<div class="list-group">` öğesi ve hemen önce hello kapanış `</a>` etiket, satır toodisplay aşağıdaki hello eklemek `comment` hello kalan hello makale verileri birlikte:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Açık _modules/articles/client/views/admin/form-article.client.view.html_.

Hello bulur `<div class="form-group">` hello Gönder düğmesi, bu gibi görünen içeren öğe:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Bu etiketi yalnızca başka bir tane eklemek `<div class="form-group">` hello Düzenle kişiler olanak sağlayan öğe `comment` alan. Yeni öğe aşağıdaki gibi görünmelidir:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Yaptığınız değişiklikler yerel olarak test etme

Yaptığınız tüm değişiklikleri kaydedin.

Değişikliklerinizi üretim modunda yeniden sınayın.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Unutmayın, _config/env/production.js_ döndürüldü ve hello `MONGODB_URI` ortam değişkeni, Azure web uygulamanızda ve yerel makinenizde değil yalnızca ayarlayın. Merhaba yapılandırma dosyasını bakarsanız, o hello bulur üretim yapılandırma Varsayılanları toouse yerel bir MongoDB veritabanı. Bu kod değişiklikleri yerel olarak test ettiğinizde üretim verileri touch yok emin olur.

Çok gidin`http://localhost:8443` bir tarayıcıda ve oturum açtınız olduğundan emin olun.

Seçin **yönetici > yönetmek makaleleri**, ardından bir makale hello seçerek eklemek  **+**  düğmesi.

Merhaba yeni gördüğünüz `Comment` şimdi metin kutusu.

![Ek Açıklama alanı tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

Yazarak Hello terminal, Node.js durdurun `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Değişiklikleri tooAzure yayımlama

Git yaptığınız değişiklikleri kaydetmek ve ardından hello kod değişiklikleri tooAzure gönderme.

```bash
git commit -am "added article comment"
git push azure master
```

Bir kez hello `git push` tamamlamak, tooyour Azure web uygulamasına gidin ve hello yeni işlevselliği deneyin.

![Model ve veritabanı değişikliklerini tooAzure yayımlanan](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Tüm makaleleri daha önce eklediyseniz, bunları yine görebilirsiniz. Cosmos veritabanında var olan veri kaybı olmadığından. Ayrıca, güncelleştirmelerinin toohello veri şemanızı ve varolan verilerinizi dokunmaz.

## <a name="stream-diagnostic-logs"></a>Akış tanılama günlükleri 

Node.js uygulamanızı Azure App Service'te çalışırken hello konsol günlükleri yöneltilen tooyour terminal elde edebilirsiniz. Bu şekilde hello aynı tanılama iletileri alabilirsiniz uygulama hatalarını hata ayıklama toohelp.

Akış, kullanım hello toostart günlük [az webapp günlük tail](/cli/azure/webapp/log#tail) komutu.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Günlük akış başladıktan sonra Azure web uygulamanızda hello tarayıcı tooget bazı web trafiği yenileyin. Şimdi, konsol günlükleri tooyour terminal yöneltilen bakın.

Herhangi bir zamanda yazarak akış günlük durdurma `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Azure web uygulamanızı yönetme

Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toosee hello web uygulaması.

Merhaba sol menüden **uygulama hizmetleri**, Azure web uygulamanızın hello adını tıklatın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Varsayılan olarak, web uygulamanızın hello portal gösterir **genel bakış** sayfası. Bu sayfa, uygulamanızın nasıl çalıştığını gösterir. Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. Merhaba sekmeler hello sayfasının sol tarafında hello açabilirsiniz hello farklı yapılandırma sayfaları gösterir.

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Sonraki adımlar

Öğrendiklerinizi:

> [!div class="checklist"]
> * MongoDB veritabanı oluşturma
> * Bir Node.js uygulaması tooMongoDB Bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın
> * Azure tooyour terminal akış günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad tooyour web uygulaması.

> [!div class="nextstepaction"] 
> [Harita bir var olan özel DNS adı tooAzure Web uygulamaları](app-service-web-tutorial-custom-domain.md)
