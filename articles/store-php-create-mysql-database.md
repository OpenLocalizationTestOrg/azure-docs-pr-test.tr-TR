---
title: "aaaCreate ve azure'da tooa MySQL veritabanına bağlanın"
description: "Nasıl toouse Azure portal toocreate bir MySQL veritabanı hello ve Azure bir PHP web uygulamasından tooit bağlanmak öğrenin."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Oluştur ve Azure tooa MySQL veritabanına bağlan
Bu öğretici nasıl toocreate bir MySQL veritabanı hello gösterir [Azure portal](https://portal.azure.com) (sağlayıcısı [ClearDB](http://www.cleardb.com/)) ve nasıl tooconnect tooit bir php'den web uygulaması çalışır durumda [Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Ayrıca bir MySQL veritabanı parçası olarak oluşturabileceğiniz bir [Market uygulaması şablonu](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Azure portalında bir MySQL veritabanı oluşturma
toocreate hello Azure portal, MySQL veritabanında hello aşağıdaki:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüden **yeni** > **veri + depolama** > **MySQL veritabanı**.

    ![Azure - başlangıç MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-1-start.png)
3. Merhaba yeni MySQL veritabanı içinde [dikey](azure-portal-overview.md), yeni MySQL veritabanınız şu şekilde yapılandırın (*dikey*: yatay açılır bir portal sayfası):

   * **Veritabanı adı**: benzersiz olarak tanımlanabilen bir ad yazın
   * **Abonelik**: hello abonelik toouse seçin
   * **Veritabanı türü**: seçin **paylaşılan** için düşük maliyetli veya ücretsiz katman veya **adanmış** tooget ayrılmış kaynakları.
   * **Kaynak grubu**: hello MySQL veritabanı tooan varolan eklemek [kaynak grubu](azure-resource-manager/resource-group-overview.md) veya yeni bir yerleştirin. Aynı grup birlikte kolayca yönetilebilir hello kaynakları.
   * **Konum**: konum Kapat tooyou seçin. Kaynak grubu mevcut tooan eklerken kilitli toohello kaynak grubu konumu demektir.
   * **Fiyatlandırma katmanı**: tıklatın **fiyatlandırma katmanı**, ardından fiyatlandırma seçeneğini belirleyin (**Mercury** katman ücretsiz) ve ardından **seçin**.
   * **Yasal koşullar**: tıklatın **yasal koşulları**hello satın alma ayrıntılarını gözden geçirin ve'ı tıklatın **satın**.
   * **PIN toodashboard**: tooaccess istiyorsanız seçin, doğrudan hello panosundan. Henüz portal gezinme alışık değilseniz bu özellikle yararlıdır.

     Aşağıdaki ekran görüntüsü hello MySQL veritabanınızı nasıl yapılandırabileceğiniz yalnızca bir örnektir.  
     ![Azure üzerinde MySQL veritabanı oluşturma - yapılandırma](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Bitirdiğinizde yapılandırma, tıklatın **oluşturma**.

    ![Azure üzerinde MySQL veritabanı oluşturma - oluşturma](./media/store-php-create-mysql-database/create-db-3-create.png)

    Dağıtım başladı bildiğiniz bir açılır bildirim veren görürsünüz.

    ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Dağıtım başarılı olduktan sonra başka bir açılır alırsınız. Merhaba portal MySQL veritabanı dikey pencerenizde aynı zamanda otomatik olarak açar.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Bağlantı tooyour MySQL veritabanı
Yeni MySQL veritabanınızı toosee hello bağlantı bilgilerini tıklatmanız **özellikleri** web uygulamanızın dikey penceresinde.

![Azure - MySQL veritabanı dikey bir MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Bu gibi durumlarda, bu bağlantı bilgisini artık herhangi bir web uygulamasına kullanabilirsiniz. Nasıl toouse hello bağlantı bilgilerini basit bir PHP uygulamasından ulaşılabilir gösteren bir örnek [burada](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Bir Laravel web uygulamasından (Merhaba PHP get Başlarken Öğreticisi) bağlanma
Yalnızca tamamlanan hello öğretici varsayalım [oluşturma, yapılandırma ve PHP web uygulaması tooAzure dağıtma](app-service-web/app-service-web-php-get-started.md) ve bir [Laravel](https://www.laravel.com/) Azure'da çalışan web uygulaması. Veritabanı özellikleri tooyour Laravel uygulama kolayca ekleyebilirsiniz. Yalnızca hello adımları izleyin:

> [!NOTE]
> Merhaba aşağıdaki adımlarda hello öğreticiyi bitirdikten varsayılmaktadır [oluşturma, yapılandırma ve PHP web uygulaması tooAzure dağıtma](app-service-web/app-service-web-php-get-started.md).
>
>

1. Merhaba Laravel uygulama, yerel geliştirme ortamı toopoint toohello MySQL veritabanınızı yapılandırın. toodo Bu, açık `.env` Laravel uygulamanızın kök dizini ve hello MySQL veritabanı seçeneklerini yapılandırın.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > Merhaba, **özellikleri** dikey penceresinde, MySQL veritabanınızı hello adını olabilir veya bir hello hello görüntülenmeyebilir **veritabanı adı** alan. Daha iyi toocheck hello veritabanı parametresinde hello olan **bağlantı DİZESİ** alan.    
   >
   > ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Merhaba hızlı şekilde tooverify MySQL erişim şimdi sahip olduğu toouse [Laravel'ın varsayılan kimlik doğrulama iskele](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   Merhaba komut satırı terminale komutları Laravel uygulamanızın kök dizininden aşağıdaki hello çalıştırın:

         php artisan migrate
         php artisan make:auth

    Merhaba ilk komut hello önceden tanımlanmış geçişleri göre azure'da hello tablolar oluşturur `database/migrations` dizin ve iskelesini kurar hello temel görünümleri ve kullanıcı kaydı ve kimlik doğrulaması için rota hello ikinci komutu.
3. Merhaba geliştirme sunucusu şimdi çalıştır:

        php artisan serve
4. Merhaba tarayıcıda toohttp://localhost:8000 gidin ve gösterildiği gibi yeni bir kullanıcı kaydı:

    ![Azure tooMySQL veritabanında connect - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Merhaba UI komut istemi tam hello kayıt izleyin. Kayıt işlemi tamamlandıktan sonra oturum açmanız.

    ![Azure tooMySQL veritabanında connect - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Uygulamanızı azure'da hello MySQL veritabanında şimdi geliştirmektedir.
5. Şimdi, tooreplicate yeterlidir, `.env` ayarları tooyour Azure web uygulaması. Azure CLI komutları aşağıdaki hello çalıştırın:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Ardından, kaydetmek ve anında önceki çalıştırılırken tooAzure hello yerel değişikliklerinin `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Toohello Azure web uygulaması göz atın.

        azure site browse
8. Daha önce oluşturduğunuz hello kullanıcı kimlik bilgilerini kullanarak oturum açın.

    ![Azure tooMySQL veritabanında connect - tooAzure web uygulaması Gözat](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Oturum açtıktan sonra hello kolay sonrası oturum açma ekranı görmeniz gerekir.

    ![Azure - oturum tooMySQL veritabanına bağlan](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Tebrikler, azure'da PHP web uygulamanız şimdi MySQL veritabanından veri erişiyor.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).
