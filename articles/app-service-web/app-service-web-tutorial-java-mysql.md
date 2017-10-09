---
title: "aaaBuild Azure içinde Java ve MySQL bir web uygulaması"
description: "Bilgi nasıl tooget bir Java uygulaması bağlanan Azure uygulama hizmeti çalışan toohello Azure MySQL veritabanı hizmeti."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Azure'da Java ve MySQL bir web uygulaması oluşturma

Bu öğretici nasıl toocreate bir Java web uygulaması Azure ve tooa MySQL veritabanına bağlanmak gösterir. İşiniz bittiğinde, olacaktır bir [yay önyükleme](https://projects.spring.io/spring-boot/) veri depolarken uygulama [Azure veritabanı için MySQL](https://docs.microsoft.com/azure/mysql/overview) üzerinde çalışan [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Azure uygulama hizmeti çalışan Java uygulaması](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Azure üzerinde MySQL veritabanı oluşturma
> * Örnek uygulama toohello veritabanına bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Güncelleştirme ve hello uygulama yeniden dağıtın
> * Azure Stream tanılama günlükleri
> * Hello Azure portal'ın Hello uygulamayı izleme


## <a name="prerequisites"></a>Ön koşullar

1. [Git yükleyip](https://git-scm.com/)
1. [Merhaba Java 7 JDK yükleyip veya üstü](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [İndirme, yükleme ve MySQL Başlat](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Yerel MySQL hazırlama 

Bu adımda, bir veritabanı kullanmak için yerel bir MySQL Server test hello uygulamada yerel olarak makinenizde oluşturun.

### <a name="connect-toomysql-server"></a>TooMySQL sunucuya bağlanın

Bir terminal penceresi tooyour yerel MySQL sunucusuna bağlanın. Bu bir terminal penceresi toorun Bu öğreticide tüm hello komutlarını kullanabilirsiniz.

```bash
mysql -u root -p
```

İçin bir parola istenirse Merhaba hello parolayı girin `root` hesabı. Kök hesap parolanızı hatırlamıyorsanız bkz [MySQL: nasıl tooReset hello kök parola](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Komutunuzu başarıyla çalışırsa, MySQL sunucunuzu zaten çalışıyor. Aksi takdirde, yerel MySQL sunucunuz tarafından aşağıdaki hello başlatıldığından emin olun [MySQL yükleme sonrası adımları](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Veritabanı oluşturma 

Merhaba, `mysql` isteminde, bir veritabanı ve tablo hello için yapılacaklar öğelerini oluşturun.

```sql
CREATE DATABASE tododb;
```

Sunucu bağlantısı yazarak çıkmak `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Oluşturma ve hello örnek uygulamayı çalıştırma 

Bu adımda, örnek yay önyükleme uygulama kopyalama, toouse hello yerel MySQL veritabanını yapılandırın ve bilgisayarınızda çalıştırın. 

### <a name="clone-hello-sample"></a>Kopya hello örnek

Merhaba terminal penceresinde dizin ve kopya hello örnek depo çalışma tooa gidin. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Merhaba uygulama toouse hello MySQL veritabanını yapılandırın

Güncelleştirme hello `spring.datasource.password` ve değer *spring-boot-mysql-todo/src/main/resources/application.properties* hello ile aynı kök parola tooopen hello MySQL istemi kullanılır:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Derleme ve hello örnek çalıştırma

Derleme ve hello bağlantıların bulunması dahil hello Maven sarmalayıcı kullanarak hello örnek çalıştırın:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Tarayıcı toohttp://localhost:8080 toosee eylemin hello örneği açın. Görevleri toohello listesinde eklediğinizde, aşağıdaki SQL komut istemi tooview hello veri MySQL içinde depolanan hello MySQL komutları hello kullanın.

```SQL
use testdb;
select * from todo_item;
```

Devreyi tarafından Hello uygulamayı durdurun `Ctrl` + `C` hello terminal içinde. 

## <a name="create-an-azure-mysql-database"></a>Bir Azure MySQL veritabanı oluşturma

Bu adımda, oluşturduğunuz bir [Azure veritabanı için MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) hello kullanarak örneğini [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli). Hello örnek uygulama toouse bu veritabanını daha sonra hello öğreticide yapılandırın.

Bir terminal penceresi toocreate hello kaynakları kullanım hello Azure CLI 2.0 toohost Java uygulamanızı Azure uygulama hizmeti gerekli. Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello ile [az grubu oluşturma](/cli/azure/group#create) komutu. Bir Azure kaynak grubu web uygulamaları, veritabanları ve depolama hesapları gibi ilgili kaynaklar burada dağıtılan ve yönetilen mantıksal bir kapsayıcısıdır. 

Merhaba aşağıdaki örnekte bir kaynak grubu hello Kuzey Avrupa bölgede oluşturur:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

toosee hello olası değerler için kullanabileceğiniz `--location`, hello kullan [az appservice listesi-konumları](/cli/azure/appservice#list-locations) komutu.

### <a name="create-a-mysql-server"></a>MySQL sunucusu oluşturun

Bir sunucu Azure veritabanı'nda MySQL (Önizleme) ile Merhaba oluşturmak [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) komutu.    
Merhaba gördüğünüz kendi benzersiz MySQL sunucu adı yerine `<mysql_server_name>` yer tutucu. Bu ad, MySQL sunucunuzun ana bilgisayar adı, bir parçasıdır `<mysql_server_name>.mysql.database.azure.com`, toobe genel olarak benzersiz olmalıdır. Ayrıca yerine `<admin_user>` ve `<admin_password>` kendi değerlere sahip.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Merhaba MySQL server oluşturulduğunda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Sunucu Güvenlik Duvarı'nı yapılandırma

Bağlantılar için MySQL server tooallow istemcinizi hello kullanarak bir güvenlik duvarı kuralı oluşturun [az mysql server güvenlik duvarı kuralı oluşturmak](/cli/azure/mysql/server/firewall-rule#create) komutu. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure veritabanı için MySQL (Önizleme) Azure Hizmetleri bağlantılarından şu anda otomatik olarak etkinleştirmez. Dinamik olarak atanmış IP adresleri Azure gibi tüm IP adresleri için daha iyi tooenable olan şimdi. Merhaba hizmet önizlemesini devam ettikçe, veritabanınızın güvenliğini sağlamak için daha iyi yöntemleri etkinleştirilecek.

## <a name="configure-hello-azure-mysql-database"></a>Hello Azure MySQL veritabanını yapılandırın

Merhaba terminal penceresinde, bilgisayarınızda, azure'da toohello MySQL sunucusuna bağlanın. Daha önce için belirttiğiniz başlangıç değeri kullanın `<admin_user>` ve `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Veritabanı oluşturma 

Merhaba, `mysql` isteminde, bir veritabanı ve tablo hello için yapılacaklar öğelerini oluşturun.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>İzinleri olan bir kullanıcı oluşturun

Bir veritabanı kullanıcısı oluşturmak ve hello tüm ayrıcalıkları vermek `tododb` veritabanı. Merhaba yer tutucuları değiştirmek `<Javaapp_user>` ve `<Javaapp_password>` kendi benzersiz uygulama adıyla.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Sunucu bağlantısı yazarak çıkmak `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Merhaba örnek tooAzure uygulama hizmeti dağıtma

Merhaba ile bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı hello kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu. Merhaba uygulama hizmeti planı hello kullanılan fiziksel kaynakları toohost uygulamalarınızı tanımlar. Tooan uygulama hizmeti planı atanan tüm uygulamaların birden fazla uygulama barındırdığında toosave maliyet izin vererek, bu kaynakları paylaşır. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Hello planı hazır olduğunda, Azure CLI benzer gösterir hello aşağıdaki örneğine toohello çıktı:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Bir Azure Web uygulaması oluşturma

 Kullanım hello [az webapp oluşturma](/cli/azure/appservice/web#create) CLI komutu toocreate bir web uygulaması tanımı'nda hello `myAppServicePlan` uygulama hizmeti planı. Merhaba web uygulaması tanımı URL tooaccess uygulamanızla sağlar ve çeşitli seçenekler toodeploy kod tooAzure yapılandırır. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Yedek hello `<app_name>` kendi benzersiz uygulama adıyla yer tutucu. Merhaba adının toobe benzersiz azure'da tüm uygulamalarında gerekir böylece bu benzersiz bir ad hello varsayılan etki alanı adı hello web uygulaması için bir parçasıdır. Tooyour kullanıcılar kullanıma önce bir özel etki alanı adı girişi toohello web uygulaması eşleyebilirsiniz.

Merhaba web uygulaması tanımı hazır olduğunda, aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir: 

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

### <a name="configure-java"></a>Java yapılandırın 

Uygulamanızın ile Merhaba gerektiğini hello Java Çalışma zamanı yapılandırma ayarlama [az appservice web yapılandırma güncelleştirmesi](/cli/azure/appservice/web/config#update) komutu.

Merhaba aşağıdaki komutu hello web uygulama toorun üzerinde yeni bir Java 8 JDK yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Merhaba uygulama toouse hello Azure SQL veritabanını Yapılandır

Merhaba örnek uygulamayı çalıştırmadan önce uygulama ayarları hello web uygulama toouse hello Azure MySQL veritabanı Azure içinde oluşturulan ayarlayın. Bu özellikler ortam değişkenleri olarak sunulan toohello web uygulaması ve hello application.properties hello paketlenmiş web app içinde kümesindeki hello değerlerini geçersiz kılar. 

Uygulama ayarlarını kullanarak [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) hello CLI içinde:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>FTP dağıtımı kimlik bilgileri alma 
Uygulama tooAzure appservice FTP, yerel Git, GitHub, Visual Studio Team Services ve BitBucket dahil olmak üzere çeşitli yollarla dağıtabilirsiniz. Bu örneğin, FTP toodeploy hello. WAR dosyası daha önce yerel makine tooAzure uygulama hizmeti oluşturuldu.

toodetermine ne kimlik bilgileri bir ftp komutu toohello Web uygulaması, kullanım içinde boyunca toopass [az appservice web dağıtım listesi-yayımlama-profilleri](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) komutu: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>FTP kullanarak hello uygulamayı karşıya yüklemek

Sık kullandığınız FTP aracı toodeploy hello kullanın. WAR dosyası toohello */site/wwwroot/webapps* hello alınan hello sunucu adresi klasöründe `URL` alanındaki hello önceki komutu. Merhaba var olan varsayılan (kök) uygulama dizini kaldırın ve ROOT.war ile Merhaba varolan hello değiştirin. WAR dosyası Hello hello öğreticide daha önce oluşturulmuş.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Test hello web uygulaması

Çok Gözat`http://<app_name>.azurewebsites.net/` ve birkaç görevleri toohello listesine ekleyin. 

![Azure uygulama hizmeti çalışan Java uygulaması](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Tebrikler!** Azure App Service'te bir veri güdümlü Java uygulaması kullanıyorsunuz.

## <a name="update-hello-app-and-redeploy"></a>Güncelleştirme hello uygulama ve yeniden dağıtın

Merhaba uygulama tooinclude hello Yapılacaklar listesinde hangi gün hello öğesinin oluşturulduğu için ek bir sütun güncelleştirin. Yay önyükleme güncelleştirme hello veritabanı şeması hello veri modeli değişikliklerini, var olan veritabanı kayıtlarını değiştirmeden işler.

1. Yerel sisteminizde açık *src/main/java/com/example/fabrikam/TodoItem.java* ve hello aşağıdaki alır toohello sınıfı ekleyin:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Ekleme bir `String` özelliği `timeCreated` çok*src/main/java/com/example/fabrikam/TodoItem.java*, nesne oluşturma sırasında bir zaman damgasına sahip başlatılıyor. Alıcıları/ayarlayıcılar hello yeni için ekleme `timeCreated` bu dosyayı düzenlerken özelliği.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Güncelleştirme *src/main/java/com/example/fabrikam/TodoDemoController.java* hello bir satır ile `updateTodo` yöntemi tooset hello zaman damgası:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Merhaba yeni alan için destek hello Thymeleaf şablonunda ekleyin. Güncelleştirme *src/main/resources/templates/index.html* hello zaman damgası ve her bir tablo veri satırının hello timestamp yeni alan toodisplay hello değeri için yeni bir tablo üstbilgiyle.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Merhaba uygulaması yeniden oluşturun:

    ```bash
    mvnw clean package 
    ```

6. FTP hello güncelleştirildi. Hello varolan kaldırma WAR olarak önce *site/wwwroot/webapps/ROOT* dizin ve *ROOT.war*, sonra da güncelleştirilmiş hello karşıya yükleme. WAR dosyası olarak ROOT.war. 

Merhaba uygulama yenilediğinizde bir **saat oluşturulan** sütundur artık görünür. Yeni bir görev eklediğinizde, hello uygulama hello zaman damgası otomatik olarak doldurur. Veri modelini temel hello değişti olsa bile varolan görevlerinizi değişmeden ve hello uygulama ile çalışmak kalır. 

![Java uygulaması olan yeni bir sütun güncelleştirildi](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Akış tanılama günlükleri 

Java uygulamanızı Azure App Service'te çalışırken hello konsol alabilirsiniz günlükleri yöneltilen doğrudan tooyour terminal. Bu şekilde hello aynı tanılama iletileri alabilirsiniz uygulama hatalarını hata ayıklama toohelp.

Akış, kullanım hello toostart günlük [az webapp günlük tail](/cli/azure/appservice/web/log#tail) komutu.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Azure web uygulamanızı yönetme

Oluşturduğunuz toohello Azure portal toosee hello web uygulamasına gidin.

toodo Bu, çok oturum[https://portal.azure.com](https://portal.azure.com).

Merhaba sol menüden **uygulama hizmeti**, Azure web uygulamanızın hello adını tıklatın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-java-mysql/access-portal.png)

Varsayılan olarak, web uygulamanızın dikey penceresinde hello gösterir **genel bakış** sayfası. Bu sayfa, uygulamanızın nasıl çalıştığını gösterir. Burada, Durdur, Başlat, yeniden başlatma ve silme gibi yönetim görevlerini gerçekleştirebilirsiniz. hello sol tarafındaki hello dikey penceresinde Hello sekmeleri açabilir hello farklı yapılandırma sayfalarında gösterilir.

![Azure portalında App Service dikey penceresi](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Bu sekme hello dikey penceresinde hello tooyour web uygulama eklemek için birçok harika özellikler gösterir. liste aşağıdaki hello birkaçı hello olasılıklar sunar:
* Özel bir DNS adı eşleme
* Özel bir SSL sertifikası bağlama
* Sürekli dağıtımı yapılandırma
* Ölçeği artırma ve genişletme
* Kullanıcı kimlik doğrulaması ekleme

## <a name="clean-up-resources"></a>Kaynakları temizleme

Başka bir öğretici için bu kaynakları gerekmiyorsa (bkz [sonraki adımlar](#next)), bunları hello aşağıdaki komutu çalıştırarak silin: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="checklist"]
> * Azure üzerinde MySQL veritabanı oluşturma
> * Bir örnek Java uygulama toohello MySQL Bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Güncelleştirme ve hello uygulama yeniden dağıtın
> * Azure Stream tanılama günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad toohello uygulama.

> [!div class="nextstepaction"] 
> [Harita bir var olan özel DNS adı tooAzure Web uygulamaları](app-service-web-tutorial-custom-domain.md)
