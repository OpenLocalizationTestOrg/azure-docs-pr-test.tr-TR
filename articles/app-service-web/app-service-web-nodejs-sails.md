---
title: "aaaDeploy Sails.js web uygulaması tooAzure App Service | Microsoft Docs"
description: "Bilgi nasıl toodeploy bir Node.js uygulamasını Azure App Service. Bu öğretici nasıl toodeploy bir Sails.js web uygulaması gösterir."
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
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Sails.js web uygulaması tooAzure uygulama hizmeti dağıtma
Bu öğretici şunların nasıl yapıldığını gösterir toodeploy Sails.js uygulama tooAzure uygulama hizmeti. Merhaba işleminde bazı genel bilgi nasıl glean tooconfigure, App Service'te Node.js uygulaması toorun.

Burada, yararlı becerileri ister öğreneceksiniz:

* App Service içinde çalıştırmak Sails.js uygulama yapılandırın.
* Merhaba komut satırından uygulama tooApp hizmet dağıtın.
* Stderr ve stdout günlükleri tootroubleshoot dağıtım sorunları okuyun.
* Ortam değişkenleri kaynak denetimi dışında depolar.
* Uygulamanızdan Azure ortam değişkenlerine erişim.
* Tooa veritabanı (MongoDB) bağlayın.

Sails.js bilgiye sahip olmalıdır. Bu öğretici hedeflenen toohelp toorunning Sail.js genel sorunları ile ilgili değildir.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="prerequisites"></a>Ön koşullar
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Bir Microsoft Azure hesabı. Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)

> [!NOTE]
> Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/). Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>1. adım: Oluşturmak ve Sails.js uygulamayı yerel olarak yapılandırma
İlk olarak, hızlı bir şekilde varsayılan Sails.js uygulama geliştirme ortamınızda aşağıdaki adımları izleyerek oluşturun:

1. Tercih ettiğiniz komut satırı Terminalini açın hello ve `CD` tooa çalışma dizini.
2. Sails.js uygulama oluşturun ve çalıştırın:

        sails new <app_name>
        cd <app_name>
        sails lift

    Http://localhost:1377 toohello varsayılan giriş sayfasına gidebilirsiniz emin olun.

1. Ardından, Azure günlüğünü etkinleştirin. Kök dizininizde adlı bir dosya oluşturun `iisnode.yml` ve hello aşağıdaki iki satırı ekleyin:

        loggingEnabled: true
        logDirectory: iisnode

    Günlüğü Merhaba şimdi etkin [iisnode](https://github.com/tjanczuk/iisnode) server Azure App Service Node.js uygulamalarını toorun kullanır. 
    Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz: [nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md).

2. Ardından, hello Sails.js uygulama toouse Azure ortam değişkenlerini yapılandırın. Üretim ortamınıza config/env/Production.js tooconfigure açıp ayarlamak `port` ve `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Bu yapılandırma ayarları için belgeler bulabilirsiniz [Sails.js belgelerine](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Toouse istediğiniz İleri stillerinizin hello Node.js sürümü. Package.json'da, hello aşağıdakileri ekleyin `engines` istediğimiz özelliği tooset hello Node.js sürüm tooone.

        "engines": {
            "node": "6.9.1"
        },

5. Son olarak, bir Git deposunu başlatmak ve dosyalarınızı uygulayın. İçinde uygulama kökü (package.json olduğu) Merhaba, Git komutlarını aşağıdaki hello çalıştırın:

        git init
        git add .
        git commit -m "<your commit message>"

Kodunuzu dağıtılan hazır toobe ' dir. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>2. adım: Azure bir uygulama oluşturun ve Sails.js dağıtma

Ardından, Azure'da hello uygulama hizmeti kaynak oluşturup Sails.js uygulama tooit dağıtabilirsiniz.

1. tooAzure günlüğüne şu şekilde:

        az login

    Merhaba komut istemi toocontinue hello tarayıcı Azure aboneliğiniz olan bir Microsoft hesabı ile oturum açma izleyin.

3. Merhaba dağıtım kullanıcı için uygulama hizmeti ayarlayın. Kodu daha sonra bu kimlik bilgilerini kullanarak dağıtacaksınız.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) bir ada sahip. Bu Node.js öğreticisi için nedir gerçekten tooknow gerekmez.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee hangi olası değerler için kullanabilmeniz için `<location>`, hello kullan `az appservice list-locations` CLI komutu.

3. "Serbest" oluşturmak [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) bir ada sahip. Bu Node.js öğreticisi için yalnızca, web uygulamaları için bu plan ücret olmaz olduğunu bilirsiniz.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. `<app_name>` içinde benzersiz bir ada sahip yeni bir web uygulaması oluşturun.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Adım 3: Yapılandırma ve Sails.js uygulamanızı dağıtma

1. Yerel Git dağıtımı yeni web uygulamanız için komutu aşağıdaki hello ile yapılandırın:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Bu hello uzak Git deposu yapılandırılmış anlamına gelir bunun gibi bir JSON çıktısını alırsınız:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Yerel deposu için uzak bir Git olarak hello JSON Hello URL'si ekleyin (adlı `azure` basitleştirmek için).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Örnek kod toohello dağıtmak `azure` Git uzaktan. İstendiğinde, daha önce yapılandırılmış hello dağıtım kimlik bilgileri kullanın.

        git push azure master

7. Son olarak, yalnızca dinamik Azure uygulamanızı hello tarayıcıda başlatın:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Artık görmelisiniz aynı Sails.js giriş sayfası hello.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Dağıtımınızın sorunlarını giderme
Sails.js uygulamanızı App Service içinde herhangi bir nedenle başarısız olursa, hello stderr günlüklerini bulmak toohelp giderme.
Daha fazla bilgi için bkz: [nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md).
Merhaba uygulama başarıyla başlatılmış olup olmadığını hello stdout günlük göstermelidir hello tanıdık ileti:

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
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

Merhaba stdout hello günlüklerinde kesinliği denetleyebilirsiniz [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) dosya.

## <a name="connect-tooa-database-in-azure"></a>Azure tooa veritabanına bağlan
tooconnect tooa veritabanı Azure, Azure, Azure SQL Database, MySQL, MongoDB, Azure (Redis) önbelleği, vb. gibi tercih ettiğiniz hello veritabanı oluşturun ve hello karşılık gelen kullanmak [veri deposu bağdaştırıcısı](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Merhaba bu bölümdeki adımları şunları nasıl yapacağınızı kullanarak tooconnect tooMongoDB bir [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) MongoDB istemci bağlantılarını desteklemek veritabanı.

1. [MongoDB protokol desteği ile Cosmos DB hesabı oluşturma](../documentdb/documentdb-create-mongodb-account.md).
2. [Cosmos DB koleksiyonu ve veritabanı oluşturma](../documentdb/documentdb-create-collection.md). Merhaba koleksiyonunun Hello adı önemli değildir, ancak Sails.js bağlandığınızda hello veritabanının hello adı gerekir.
3. [Cosmos DB veritabanınızı Hello bağlantı bilgilerini bulmak](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Komut satırı, terminal durumundan hello MongoDB bağdaştırıcısı yükleyin:

        npm install sails-mongo --save

3. Config/Connections.js açın ve bağlantı nesnesi toohello listesi aşağıdaki hello ekleyin:

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
    > Merhaba `ssl: true` seçeneği önemlidir çünkü [Cosmos DB gerektirir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Her ortam değişkeni için (`process.env.*`), tooset ihtiyacınız App Service içinde. toodo terminal durumundan komutları aşağıdaki Bu, çalışma hello. Merhaba bağlantı bilgilerini Cosmos DB için kullanın.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Azure uygulama ayarlarında ayarlarınızı koyma, kaynak denetimi (Git) dışında hassas verileri tutar. Ardından, geliştirme yapılandıracağınız ortamı toouse hello aynı bağlantı bilgileri.
5. Config/Local.js açın ve bağlantıları nesne aşağıdaki hello ekleyin:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Bu yapılandırma hello yerel ortamınıza config/connections.js dosyanızdaki hello ayarları geçersiz kılar. Git içinde depolanmaz şekilde bu dosyayı hello varsayılan .gitignore projenizdeki tarafından dışlandı. Şimdi, Azure web uygulamanız ve yerel geliştirme ortamınızı mümkün tooconnect tooyour Cosmos DB (MongoDB) veritabanı misiniz.
6. Üretim ortamınıza config/env/Production.js tooconfigure açın ve hello aşağıdakileri ekleyin `models` nesnesi:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Geliştirme ortamınızı config/env/Development.js tooconfigure açın ve hello aşağıdakileri ekleyin `models` nesnesi:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`Veritabanı geçiş özellikleri toocreate kullanın ve veritabanı koleksiyonları veya tabloları kolayca güncelleştirmenize olanak sağlar. Ancak, `migrate: 'safe'` Sails.js, toouse izin vermediğinden, Azure (üretim) ortamınız için kullanılan `migrate: 'alter'` bir üretim ortamında (bkz [Sails.js belgelerine](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Merhaba terminal, gelen [oluşturmak](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) bir Sails.js [API şeması](http://sailsjs.org/documentation/concepts/blueprints) , normalde sonra çalıştırılır gibi `sails lift` ile Sails.js veritabanı geçiş hello veritabanı oluşturmak için. Örneğin:

         sails generate api mywidget
         sails lift

    Merhaba `mywidget` bu komutu tarafından oluşturulan model boşsa, ancak biz veritabanı bağlantısı sahibiz tooshow kullanabilirsiniz.
    Çalıştırdığınızda `sails lift`hello eksik koleksiyonları oluşturur ve tablolar hello için modeller, uygulama kullanır.
9. Merhaba tarayıcıda oluşturduğunuz erişim hello şeması API. Örneğin:

        http://localhost:1337/mywidget/create

    Merhaba API koleksiyonunuz başarıyla oluşturuldu anlamı hello tarayıcı penceresinde hello oluşturulan girişi geri tooyou döndürmelidir.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Şimdi, değişiklikleri tooAzure anında ve tooyour uygulama toomake çalışmaya devam ettiğinden emin göz atın.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Azure web uygulamanızın erişim hello şeması API. Örneğin:

         http://<appname>.azurewebsites.net/mywidget/create

     Merhaba API başka bir yeni giriş döndürürse, Azure web uygulamanızın tooyour Cosmos DB (MongoDB) veritabanı Bahsediyor.

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure App Service'te Node.js web uygulamalarını kullanmaya başlama](app-service-web-get-started-nodejs.md)
* [Azure uygulamalarıyla Node.js Modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md)
