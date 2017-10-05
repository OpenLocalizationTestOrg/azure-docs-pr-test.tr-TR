---
title: "Azure App Service'e Sails.js web uygulaması dağıtma | Microsoft Docs"
description: "Bir Node.js uygulamasını Azure App Service dağıtmayı öğrenin. Bu öğretici Sails.js web uygulamasının nasıl dağıtılacağını gösterir."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a>Azure App Service’e Sails.js web uygulaması dağıtma
Bu öğreticide Azure App Service'e Sails.js uygulama dağıtma gösterilmektedir. Bu süreçte bazı App Service içinde çalıştırmak için Node.js uygulamanızı yapılandırma hakkında genel bilgi glean.

Burada, yararlı becerileri ister öğreneceksiniz:

* App Service içinde çalıştırmak Sails.js uygulama yapılandırın.
* Bir uygulamayı, komut satırından App Service'e dağıtın.
* Dağıtım sorunları gidermek için okuma stderr ve stdout günlükleri.
* Ortam değişkenleri kaynak denetimi dışında depolar.
* Uygulamanızdan Azure ortam değişkenlerine erişim.
* Bir veritabanı (MongoDB) bağlayın.

Sails.js bilgiye sahip olmalıdır. Bu öğretici Sail.js genel çalıştırma ile ilgili sorunları yardımcı olmak için tasarlanmamıştır.

## <a name="cli-versions-to-complete-the-task"></a>Görevi tamamlamak için kullanılacak CLI sürümleri

Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md): Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI’mız
- [Azure CLI 2.0](app-service-web-nodejs-sails.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız

## <a name="prerequisites"></a>Ön koşullar
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Bir Microsoft Azure hesabı. Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)

> [!NOTE]
> Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/). Başlangıç uygulaması oluşturun ve bir saate kadar üzerinde çalışın; kredi kartı veya taahhüt gerekmez.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>1. adım: Oluşturmak ve Sails.js uygulamayı yerel olarak yapılandırma
İlk olarak, hızlı bir şekilde varsayılan Sails.js uygulama geliştirme ortamınızda aşağıdaki adımları izleyerek oluşturun:

1. Tercih ettiğiniz komut satırı Terminalini açın ve `CD` bir çalışma dizini için.
2. Sails.js uygulama oluşturun ve çalıştırın:

        sails new <app_name>
        cd <app_name>
        sails lift

    Http://localhost:1377 varsayılan giriş sayfasına gidebilirsiniz emin olun.

1. Ardından, Azure günlüğünü etkinleştirin. Kök dizininizde adlı bir dosya oluşturun `iisnode.yml` ve aşağıdaki iki satırı ekleyin:

        loggingEnabled: true
        logDirectory: iisnode

    Günlüğe kaydetme için şimdi etkinleştirildiğinde [iisnode](https://github.com/tjanczuk/iisnode) Azure App Service Node.js uygulamalarını çalıştırmak için kullandığı sunucusuna. 
    Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure App Service'te Node.js web uygulamasına hata ayıklama](web-sites-nodejs-debug.md).

2. Ardından, Azure ortam değişkenlerini kullanmak üzere Sails.js uygulamayı yapılandırın. Üretim ortamınıza yapılandırmak ve ayarlamak için config/env/production.js açmak `port` ve `hookTimeout`:

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Bu yapılandırma ayarları için belgeler bulabilirsiniz [Sails.js belgelerine](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Ardından, stillerinizin Node.js sürümünü kullanmak istiyorsunuz. Package.json'da, aşağıdakileri ekleyin `engines` istiyoruz bir Node.js sürümünü ayarlamak için özellik.

        "engines": {
            "node": "6.9.1"
        },

5. Son olarak, bir Git deposunu başlatmak ve dosyalarınızı uygulayın. (Package.json olduğu) uygulama kök aşağıdaki Git komutları çalıştırın:

        git init
        git add .
        git commit -m "<your commit message>"

Kodunuzu dağıtılmaya hazırdır. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>2. adım: Azure bir uygulama oluşturun ve Sails.js dağıtma

Ardından, uygulama hizmeti kaynak oluşturmak ve Sails.js uygulamanızı dağıtma.

1. Azure benzer şekilde oturum açın:

        az login

    Azure aboneliğinizin bulunduğu bir Microsoft hesabıyla tarayıcıda oturum açmaya devam etmek için istemi izleyin.

3. App Service için dağıtım kullanıcısını ayarlayın. Kodu daha sonra bu kimlik bilgilerini kullanarak dağıtacaksınız.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) bir ada sahip. Bu Node.js öğreticisi için gerçekten ne olduğunu bilmeniz gerekmez.

        az group create --location "<location>" --name my-sailsjs-app-group

    `<location>` için hangi olası değerleri kullanabileceğinizi görmek için `az appservice list-locations` CLI komutunu kullanın.

3. "Serbest" oluşturmak [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) bir ada sahip. Bu Node.js öğreticisi için yalnızca, web uygulamaları için bu plan ücret olmaz olduğunu bilirsiniz.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. `<app_name>` içinde benzersiz bir ada sahip yeni bir web uygulaması oluşturun.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Adım 3: Yapılandırma ve Sails.js uygulamanızı dağıtma

1. Şu komutla yeni web uygulamanıza yönelik yerel Git dağıtımını yapılandırın:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Buna benzer bir JSON çıktısı alırsınız ve bu çıktı uzak Git deposunun yapılandırıldığı anlamına gelir:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. JSON'daki URL'yi yerel deponuz (basit olması açısından `azure` diyelim) için bir uzak Git deposu olarak ekleyin.

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Örnek kodunuzu `azure` Git uzak deposuna dağıtın. Kimlik bilgisi istendiğinde daha önce yapılandırdığınız dağıtım kimlik bilgilerini kullanın.

        git push azure master

7. Son olarak, yalnızca dinamik Azure uygulamanızı tarayıcıda başlatın:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Aynı Sails.js giriş sayfası görmelisiniz.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Dağıtımınızın sorunlarını giderme
Sails.js uygulamanızı App Service içinde herhangi bir nedenle başarısız olursa, onu gidermenize yardımcı olması için stderr günlüklerini Bul.
Daha fazla bilgi için bkz: [Azure App Service'te Node.js web uygulamasına hata ayıklama](web-sites-nodejs-debug.md).
Uygulama başarıyla başlatılmış olup olmadığını, stdout günlük tanıdık iletisini göstermelidir:

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

Stdout günlüklerde kesinliği denetleyebilirsiniz [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) dosya.

## <a name="connect-to-a-database-in-azure"></a>Azure veritabanına bağlan
Azure bir veritabanına bağlanmak için Azure, Azure SQL Database, MySQL, MongoDB, Azure (Redis) önbelleği, vb. gibi tercih ettiğiniz veritabanı oluşturun ve karşılık gelen kullanmak [veri deposu bağdaştırıcısı](https://github.com/balderdashy/sails#compatibility) bağlanmak için. Bu bölümdeki adımları kullanarak MongoDB için bağlanma Göster bir [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) MongoDB istemci bağlantılarını desteklemek veritabanı.

1. [MongoDB protokol desteği ile Cosmos DB hesabı oluşturma](../documentdb/documentdb-create-mongodb-account.md).
2. [Cosmos DB koleksiyonu ve veritabanı oluşturma](../documentdb/documentdb-create-collection.md). Koleksiyon adı önemli değildir, ancak Sails.js bağlandığınızda veritabanının adı gerekir.
3. [Cosmos DB veritabanınız için bağlantı bilgilerini bulmak](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Komut satırı, terminal durumundan MongoDB bağdaştırıcısı yükleyin:

        npm install sails-mongo --save

3. Config/Connections.js açın ve aşağıdaki bağlantı nesnesi listeye ekleyin:

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > `ssl: true` Seçeneği önemlidir çünkü [Cosmos DB gerektirir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Her ortam değişkeni için (`process.env.*`), App Service'te ayarlamanız gerekir. Bunu yapmak için terminal durumundan aşağıdaki komutları çalıştırın. Cosmos DB için bağlantı bilgisini kullanın.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Azure uygulama ayarlarında ayarlarınızı koyma, kaynak denetimi (Git) dışında hassas verileri tutar. Ardından, geliştirme ortamınızı aynı bağlantı bilgilerini kullanacak şekilde yapılandırır.
5. Config/Local.js açın ve aşağıdaki bağlantıları nesne ekleyin:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Bu yapılandırma config/connections.js dosyanızda yerel ortamınız için ayarları geçersiz kılar. Git içinde depolanmaz şekilde bu dosyayı varsayılan .gitignore projenizdeki tarafından dışlandı. Şimdi, Azure web uygulamanız ve yerel geliştirme ortamınızı Cosmos DB (MongoDB) veritabanınıza bağlantı kuramaz.
6. Üretim ortamınıza yapılandırmak için config/env/production.js açın ve aşağıdakileri ekleyin `models` nesnesi:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Geliştirme ortamınızı yapılandırmak için config/env/development.js açın ve aşağıdakileri ekleyin `models` nesnesi:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`Veritabanı geçiş özellikleri oluşturmak ve veritabanı koleksiyonları veya tabloları kolayca güncelleştirmek için kullanmanıza olanak sağlar. Ancak, `migrate: 'safe'` Sails.js kullanmanıza izin vermediğinden, Azure (üretim) ortamınız için kullanılan `migrate: 'alter'` bir üretim ortamında (bkz [Sails.js belgelerine](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Gelen terminal [oluşturmak](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) bir Sails.js [API şeması](http://sailsjs.org/documentation/concepts/blueprints) , normalde sonra çalıştırılır gibi `sails lift` Sails.js veritabanı geçiş ile veritabanı oluşturmak için. Örneğin:

         sails generate api mywidget
         sails lift

    `mywidget` Bu komutu tarafından oluşturulan model boşsa, ancak biz veritabanı bağlantısı sahibiz göstermek için kullanabilirsiniz.
    Çalıştırdığınızda `sails lift`, uygulamanızı eksik koleksiyonlar ve tablolar modelleri için oluşturduğu kullanır.
9. Tarayıcıda oluşturduğunuz API şeması erişin. Örneğin:

        http://localhost:1337/mywidget/create

    API geri koleksiyonunuz başarıyla oluşturuldu anlamına gelir tarayıcı penceresinde için oluşturulan girişi döndürmelidir.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Şimdi, değişikliklerinizi Azure'a gönderin ve çalışmaya devam ettiğinden emin olmak için uygulamanızın göz atın.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Azure web uygulamanızın API şeması erişin. Örneğin:

         http://<appname>.azurewebsites.net/mywidget/create

     API başka bir yeni giriş döndürürse, Azure web uygulamanızın Cosmos DB (MongoDB) veritabanınızı Bahsediyor.

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure App Service'te Node.js web uygulamalarını kullanmaya başlama](app-service-web-get-started-nodejs.md)
* [Azure uygulamalarıyla Node.js Modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md)
