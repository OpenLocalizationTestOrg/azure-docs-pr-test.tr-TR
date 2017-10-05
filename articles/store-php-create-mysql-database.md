---
title: "Azure’da MySQL veritabanı oluşturma ve ona bağlanma"
description: "Bir MySQL veritabanı oluşturun ve bir PHP web uygulamasını Azure buna bağlanmak için Azure portalını kullanmayı öğrenin."
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
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a>Azure’da MySQL veritabanı oluşturma ve ona bağlanma
Bu öğretici bir MySQL veritabanının oluşturulacağı gösterilmektedir [Azure portal](https://portal.azure.com) (sağlayıcısı [ClearDB](http://www.cleardb.com/)) ve çalışır durumda bir PHP web uygulamasından bağlanmak nasıl [Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Ayrıca bir MySQL veritabanı parçası olarak oluşturabileceğiniz bir [Market uygulaması şablonu](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Azure portalında bir MySQL veritabanı oluşturma
Azure portalında bir MySQL veritabanı oluşturmak için aşağıdakileri yapın:

1. [Azure Portal](https://portal.azure.com)’da oturum açın.
2. Sol menüden **yeni** > **veri + depolama** > **MySQL veritabanı**.

    ![Azure - başlangıç MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-1-start.png)
3. Yeni MySQL veritabanı [dikey](azure-portal-overview.md), yeni MySQL veritabanınız şu şekilde yapılandırın (*dikey*: yatay açılır bir portal sayfası):

   * **Veritabanı adı**: benzersiz olarak tanımlanabilen bir ad yazın
   * **Abonelik**: kullanılacak aboneliği seçin
   * **Veritabanı türü**: seçin **paylaşılan** için düşük maliyetli veya ücretsiz katman veya **adanmış** özel kaynakları alınamadı.
   * **Kaynak grubu**: mevcut bir MySQL veritabanı Ekle [kaynak grubu](azure-resource-manager/resource-group-overview.md) veya yeni bir yerleştirin. Aynı gruptaki kaynakların birlikte kolayca yönetilebilir.
   * **Konum**: yakın bir konum seçin. Varolan bir kaynak grubuna eklerken, kaynak grubunun konuma kilitli.
   * **Fiyatlandırma katmanı**: tıklatın **fiyatlandırma katmanı**, ardından fiyatlandırma seçeneğini belirleyin (**Mercury** katman ücretsiz) ve ardından **seçin**.
   * **Yasal koşullar**: tıklatın **yasal koşulları**, satın alma ayrıntılarını gözden geçirin ve'ı tıklatın **satın**.
   * **Panoya Sabitle**: doğrudan panodan erişim isteyip istemediğinizi seçin. Henüz portal gezinme alışık değilseniz bu özellikle yararlıdır.

     Aşağıdaki ekran görüntüsünde, MySQL veritabanınızı nasıl yapılandırabileceğiniz yalnızca bir örnektir.  
     ![Azure üzerinde MySQL veritabanı oluşturma - yapılandırma](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Bitirdiğinizde yapılandırma, tıklatın **oluşturma**.

    ![Azure üzerinde MySQL veritabanı oluşturma - oluşturma](./media/store-php-create-mysql-database/create-db-3-create.png)

    Dağıtım başladı bildiğiniz bir açılır bildirim veren görürsünüz.

    ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Dağıtım başarılı olduktan sonra başka bir açılır alırsınız. Portal, MySQL veritabanı dikey aynı zamanda otomatik olarak açar.

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a>MySQL veritabanına bağlan
Yeni MySQL veritabanınız için bağlantı bilgilerini görmek için tıklatmanız **özellikleri** web uygulamanızın dikey penceresinde.

![Azure - MySQL veritabanı dikey bir MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Bu gibi durumlarda, bu bağlantı bilgisini artık herhangi bir web uygulamasına kullanabilirsiniz. Basit bir PHP uygulaması'ndan bağlantı bilgisinin nasıl kullanılacağını gösteren bir örnek kullanılabilir [burada](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a>Bir Laravel web uygulamasından (PHP get Başlarken Öğreticisi) bağlanma
Öğretici yalnızca tamamlandı varsayalım [oluşturma, yapılandırma ve Azure'a bir PHP web uygulaması dağıtma](app-service-web/app-service-web-php-get-started.md) ve bir [Laravel](https://www.laravel.com/) Azure'da çalışan web uygulaması. Veritabanı özellikleri Laravel uygulamanıza kolayca ekleyebilirsiniz. Yalnızca aşağıdaki adımları izleyin:

> [!NOTE]
> Aşağıdaki adımlarda öğreticiyi bitirdikten varsayılmaktadır [oluşturma, yapılandırma ve Azure'a bir PHP web uygulaması dağıtma](app-service-web/app-service-web-php-get-started.md).
>
>

1. Laravel uygulama yerel geliştirme ortamınızı MySQL veritabanına işaret edecek şekilde yapılandırın. Bunu yapmak için açın `.env` Laravel uygulamanızın kök dizini ve MySQL veritabanı seçeneklerini yapılandırın.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > İçinde **özellikleri** dikey penceresinde, MySQL veritabanınızın adını olabilir veya bir içinde görüntülenmeyebilir **veritabanı adı** alan. Veritabanı parametresi iade daha iyidir **bağlantı DİZESİ** alan.    
   >
   > ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. MySQL erişim artık yüklü olduğunu doğrulamak için en hızlı yoludur kullanmaktır [Laravel'ın varsayılan kimlik doğrulama iskele](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   Komut satırı terminale Laravel uygulamanızın kök dizininden aşağıdaki komutları çalıştırın:

         php artisan migrate
         php artisan make:auth

    İlk komut, önceden tanımlanmış geçişleri temel Azure tabloları oluşturur `database/migrations` dizin ve ikinci komut scaffolds temel görünümleri ve kullanıcı kaydı ve kimlik doğrulaması için rota.
3. Geliştirme Sunucusu şimdi çalıştır:

        php artisan serve
4. Tarayıcı için 8000 gidin ve gösterildiği gibi yeni bir kullanıcı kaydı:

    ![Azure'da MySQL veritabanına bağlanma - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Tam UI istemi kayıt izleyin. Kayıt işlemi tamamlandıktan sonra oturum açmanız.

    ![Azure'da MySQL veritabanına bağlanma - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Artık uygulamanızı Azure MySQL veritabanında karşı geliştirmektedir.
5. Şimdi, çoğaltmak yeterlidir, `.env` Azure web uygulamanızın ayarlar. Aşağıdaki Azure CLI komutları çalıştırın:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Ardından, kaydetmek ve daha önce çalıştırılırken yapılan yerel değişiklikleri Azure'a gönderin `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Azure web uygulaması'na göz atın.

        azure site browse
8. Daha önce oluşturduğunuz kullanıcı kimlik bilgilerini kullanarak oturum açın.

    ![Connect Azure - MySQL veritabanında Azure web uygulaması'na göz atın](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Oturum açtıktan sonra kolay sonrası oturum açma ekranı görmeniz gerekir.

    ![Oturum açmış Azure - MySQL veritabanına bağlan](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Tebrikler, azure'da PHP web uygulamanız şimdi MySQL veritabanından veri erişiyor.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: [PHP Geliştirici Merkezi](/develop/php/).
