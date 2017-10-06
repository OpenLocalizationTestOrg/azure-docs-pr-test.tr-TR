---
title: "aaaBuild azure'da Docker Python ve PostgreSQL bir web uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooget Docker Python uygulaması Azure'da çalışan, bağlantı tooa PostgreSQL veritabanı."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Azure'da Docker Python ve PostgreSQL bir web uygulaması oluşturma

Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar. Bu öğretici nasıl toocreate temel Docker Python web uygulaması Azure gösterir. Bu uygulama tooa PostgreSQL veritabanına bağlanırsınız. İşiniz bittiğinde, Docker kapsayıcısı içinde çalışan bir Python Flask uygulaması gerekir [Azure App Service Web Apps](app-service-web-overview.md).

![Docker Python Flask uygulamada Azure uygulama hizmeti](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

MacOS üzerinde hello adımları izleyebilirsiniz. Linux ve Windows'da aynı hello çoğu durumda, ancak bu öğreticide hello farklar ayrıntılı değil yönergelerdir.
 
## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

1. [Git'i yükleyin](https://git-scm.com/)
1. [Python'ı yükleyin](https://www.python.org/downloads/)
1. [Yükleme ve PostgreSQL çalıştırma](https://www.postgresql.org/download/)
1. [Docker Community Edition'ı yükleme](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Yerel PostgreSQL yüklemeyi sınamak ve bir veritabanı oluştur

Merhaba terminal penceresi açın ve çalıştırın `psql postgres` tooconnect tooyour yerel PostgreSQL sunucu.

```bash
psql postgres
```

Bağlantı başarılı olursa, PostgreSQL veritabanınız çalışıyor. Aksi takdirde, yerel PostgresQL veritabanınızı hello adımları izleyerek başlatıldığından emin olun [yüklemeleri - PostgreSQL çekirdek dağıtım](https://www.postgresql.org/download/).

Adlı bir veritabanı oluşturmak *eventregistration* ve adlı bir ayrı veritabanı kullanıcı ayarlama *Yöneticisi* parolayla *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Tür *\q* tooexit hello PostgreSQL istemci. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Yerel Python Flask uygulaması oluşturma

Bu adımda, hello yerel Python Flask projesi ayarlayın.

### <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Açık hello terminal penceresi ve `CD` tooa çalışma dizini.  

Çalışma hello aşağıdaki komutları tooclone hello örnek depo ve Git toohello *0,1 initialapp* serbest bırakın.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Bu örnek depo içeren bir [Flask](http://flask.pocoo.org/) uygulama. 

### <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

> [!NOTE] 
> Bir sonraki adımda Docker kapsayıcısı toouse hello üretim veritabanıyla oluşturarak bu işlemi basitleştirir.

Merhaba gerekli paketleri yüklemek ve hello uygulamasını başlatın.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Merhaba uygulama tam olarak yüklendiğinde iletiden benzeri toohello bakın:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Bir tarayıcıda toohttp://127.0.0.1:5000 gidin. Tıklatın **kaydedin!** ve bir test kullanıcısı oluşturun.

![Yerel olarak çalışan Python Flask uygulama](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

Merhaba Flask örnek uygulamanın kullanıcı verilerini hello veritabanında depolar. Bir kullanıcı kaydetme sırasında başarılı olursa, uygulamanızın veri toohello yerel PostgreSQL veritabanına yazma.

toostop hello Flask sunucuda dilediğiniz zaman, Ctrl + C hello terminal yazın. 

## <a name="create-a-production-postgresql-database"></a>Bir üretim PostgreSQL veritabanı oluşturma

Bu adımda, Azure PostgreSQL veritabanında oluşturun. Uygulamanızı dağıtılan tooAzure olduğunda, bu bulut veritabanı kullanır.

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Devam eden toouse hello Azure CLI 2.0 toocreate hello kaynakları toohost Python uygulamanızı Azure App Service'te gerekli artık size aittir.  Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello ile [az grubu oluşturma](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Merhaba aşağıdaki örnekte bir kaynak grubu hello Batı ABD bölgesi oluşturur:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Kullanım hello [az appservice listesi-konumları](/cli/azure/appservice#list-locations) Azure CLI toolist kullanılabilir konumlarını komutu.

### <a name="create-an-azure-database-for-postgresql-server"></a>PostgreSQL için Azure Veritabanı sunucusu oluşturma

Bir PostgreSQL sunucusu ile Merhaba oluşturmak [az postgres sunucusu oluşturmak](/cli/azure/documentdb#create) komutu.

Hello hello için bir benzersiz sunucu adı yerine komutu, aşağıdaki  *\<postgresql_name >* yer tutucu ve hello için bir kullanıcı adı  *\<admin_username >* yer tutucusu . Merhaba sunucu adı, PostgreSQL uç noktanızı bir parçası olarak kullanılır (`https://<postgresql_name>.postgres.database.azure.com`), hello adı toobe benzersiz Azure içindeki tüm sunucular arasında olmalıdır. Merhaba ilk veritabanı yönetici kullanıcı hesabı Hello kullanıcı adıdır. Bu kullanıcı için bir parola istendiğinde toopick var.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Hello Azure veritabanı PostgreSQL sunucusu oluşturulduğunda, hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Hello Azure veritabanı PostgreSQL sunucusu için bir güvenlik duvarı kuralı oluşturun

Tüm IP adreslerinden Azure CLI komut tooallow erişim toohello veritabanı aşağıdaki hello çalıştırın.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hello Azure CLI hello güvenlik duvarı kuralı oluşturma çıkış benzer toohello aşağıdaki örneğine ile onaylar:

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a>Python Flask uygulama toohello veritabanınız Bağlan

Bu adımda oluşturduğunuz PostgreSQL sunucu, Python Flask örnek uygulama toohello Azure veritabanı bağlayın.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Boş bir veritabanı oluşturun ve yeni bir veritabanı uygulama kullanıcı ayarlama

Bir veritabanı kullanıcısı tooa tek yalnızca access veritabanı ile oluşturun. Merhaba uygulama tam erişim toohello sunucusu vererek bu kimlik bilgileri tooavoid kullanacaksınız.

(Yönetici parolanızı girmeniz istenir) toohello veritabanına bağlanın.

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Merhaba veritabanı ve kullanıcı PostgreSQL CLI hello oluşturun.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Tür *\q* tooexit hello PostgreSQL istemci.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Merhaba uygulamayı yerel olarak hello Azure PostgreSQL veritabanına karşı test etme 

Şimdi toohello geri dönerseniz *uygulama* hello klasörünü klonlanmış Github deposunu, hello veritabanı ortam değişkenleri güncelleştirerek hello Python Flask uygulamayı çalıştırabilirsiniz.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Merhaba uygulama tam olarak yüklendiğinde iletiden benzeri toohello bakın:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Bir tarayıcıda toohttp://127.0.0.1:5000 gidin. Tıklatın **kaydedin!** ve bir test kaydı oluşturun. Şimdi, Azure'da verileri toohello veritabanı yazıyorsanız.

![Yerel olarak çalışan Python Flask uygulama](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Docker kapsayıcısı çalışan hello uygulamadan

Merhaba Docker kapsayıcısı görüntüsünü oluşturabilirsiniz.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker bu başarıyla oluşturuldu BT hello kapsayıcı bir onay görüntüler.

```bash
Successfully built 7548f983a36b
```

Veritabanı ortam değişkenleri tooan ortam değişken dosyası ekleme *db.env*. Merhaba uygulama toohello PostgreSQL üretim Azure veritabanında bağlanır.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Merhaba uygulama hello Docker kapsayıcısı içinde çalıştırın. Merhaba aşağıdaki komutu hello ortam değişken dosyası belirtir ve hello varsayılan Flask bağlantı noktası 5000 toolocal bağlantı noktası 5000 eşler.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

Merhaba çıktı, daha önce gördüğünüzle benzer toowhat şeklindedir. Ancak, hello ilk veritabanı geçiş artık gerçekleştirilen toobe gerekir ve bu nedenle atlanır.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

daha önce oluşturduğunuz hello kayıt Hello veritabanı zaten var.

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Merhaba Docker kapsayıcısı tooa kapsayıcı kayıt defteri karşıya yükle

Bu adımda, hello Docker kapsayıcısı tooa kapsayıcı kayıt defteri karşıya yükleyin. Azure kapsayıcı kayıt defteri kullanırsınız, ancak Docker Hub gibi diğer popüler olanlar da kullanabilirsiniz.

### <a name="create-an-azure-container-registry"></a>Azure Container Registry oluşturma

Komut toocreate bir kapsayıcı kayıt defteri aşağıdaki hello yerine  *\<registry_name >* tercih ettiğiniz bir benzersiz Azure kapsayıcı kayıt defteri adı.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Çıktı
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Docker görüntüleri çekme ve itme hello kayıt defteri kimlik bilgilerini alma

tooshow kayıt defteri kimlik bilgileri, Yönetici modu ilk etkinleştirin.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

İki parola bakın. Merhaba kullanıcı adı ve hello ilk parola not edin.

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Docker kapsayıcısı tooAzure kapsayıcı kayıt defteri karşıya yükle

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Merhaba Docker Python Flask uygulama tooAzure dağıtma

Bu adımda, Docker kapsayıcısı tabanlı Python Flask uygulama tooAzure uygulama hizmeti dağıtın.

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma

Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Merhaba aşağıdaki örnekte oluşturur adlı bir Linux tabanlı uygulama hizmeti planı *myAppServicePlan* fiyatlandırma katmanı hello S1 kullanarak:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Uygulama hizmeti planı Hello oluşturulduğunda, hello Azure CLI bilgi benzer toohello aşağıdaki örneğine gösterir:

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a>Web uygulaması oluşturma

Hello bir web uygulaması oluşturma *myAppServicePlan* hello ile uygulama hizmeti planı [az webapp oluşturmak](/cli/azure/webapp#create) komutu. 

dağıtılan uygulama, bir barındırma kodunuzu toodeploy boşluk ve sizin için bir URL tooview hello sağlar hello web uygulamasını sağlar. Toocreate hello web uygulaması kullanın. 

Hello hello Değiştir komutu, aşağıdaki  *\<app_name >* yer tutucu benzersiz bir uygulama adına sahip. Merhaba adının toobe benzersiz Azure App Service'te tüm uygulamalarında gerekir böylece bu adı hello varsayılan URL hello web uygulaması için bir parçasıdır. 

```azurecli
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

### <a name="configure-hello-database-environment-variables"></a>Merhaba veritabanı ortam değişkenlerini yapılandırın

Öğreticide daha önce Merhaba, ortam değişkenleri tooconnect tooyour PostgreSQL veritabanında tanımlı.

Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ hello kullanarak [az webapp config appsettings kümesi](/cli/azure/webapp/config#set) komutu. 

Merhaba aşağıdaki örnek hello veritabanı bağlantı ayrıntıları uygulama ayarlarını belirtir. Ayrıca hello kullanır *bağlantı noktası* değişken toomap bağlantı noktası 5000 bağlantı noktası 80 üzerinde Docker kapsayıcısı tooreceive HTTP trafiğinden.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Docker kapsayıcısı dağıtımını yapılandırma 

Uygulama hizmeti otomatik olarak karşıdan yükle ve Docker kapsayıcısı çalıştırın.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Her hello Docker kapsayıcısı güncelleştirmek veya hello ayarlarını değiştirme hello uygulamayı yeniden başlatın. Yeniden başlatma, tüm ayarları uygulanır ve hello son kapsayıcı hello kayıt defterinden çekilir sağlar.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure web uygulaması Gözat 

Web tarayıcınız üzerinden dağıtılan toohello web uygulaması göz atın. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> Merhaba kapsayıcı indirilir ve hello kapsayıcısı yapılandırmasını değiştirildikten sonra başlatıldı toobe olduğundan hello web uygulaması uzun tooload alır.

Toohello Azure üretim veritabanını hello önceki adımda kaydedilen önceden kaydedilmiş konuklar bakın.

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Tebrikler!** Azure App Service'te bir Docker kapsayıcısı tabanlı bir Python Flask uygulamanın çalıştırdığınız.

## <a name="update-data-model-and-redeploy"></a>Güncelleştirme veri modeli ve yeniden dağıtın

Bu adımda, hello Konuk modeli güncelleştirerek hello sayıda katılımcı tooeach olay kaydı ekleyin.

Merhaba denetleyin *0.2 geçiş* git komut aşağıdaki hello sürümüyle:

```bash
git checkout tags/0.2-migration
```

Bu sürümü zaten gerekli değişiklikleri tooviews, denetleyicilere ve model hello yaptı. Ayrıca aracılığıyla oluşturulan bir veritabanı geçiş içerir *alembic* (`flask db migrate`). Git komutu aşağıdaki hello yapılan tüm değişiklikleri görebilirsiniz:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Yaptığınız değişiklikler yerel olarak test etme

Aşağıdaki komutları tootest hello değişikliklerinizi çalışan hello flask sunucu tarafından yerel olarak çalıştırın.

Mac / Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Tarayıcı tooview hello değişikliklerinizi toohttp://127.0.0.1:5000 gidin. Bir test kaydı oluşturun.

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Değişiklikleri tooAzure yayımlama

Merhaba yeni docker görüntüsünü oluşturabilirsiniz, toohello kapsayıcı kayıt defteri itme ve hello uygulamayı yeniden başlatın.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Tooyour Azure web uygulamasına gidin ve hello yeni işlevsellik yeniden deneyin. Başka bir olay kaydı oluşturun.

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask uygulamada Azure uygulama hizmeti](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Azure web uygulamanızı yönetme

Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toosee hello web uygulaması.

Merhaba sol menüden **uygulama hizmetleri**, Azure web uygulamanızın hello adını tıklatın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

Varsayılan olarak, web uygulamanızın hello portal gösterir **genel bakış** sayfası. Bu sayfa, uygulamanızın nasıl çalıştığını gösterir. Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. Merhaba sekmeler hello sayfasının sol tarafında hello açabilirsiniz hello farklı yapılandırma sayfaları gösterir.

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Sonraki adımlar

İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad tooyour web uygulaması.

> [!div class="nextstepaction"] 
> [Harita bir var olan özel DNS adı tooAzure Web uygulamaları](app-service-web-tutorial-custom-domain.md)
