---
title: "Birden çok tesis Azure App Service'te WordPress Dönüştür"
description: "Azure galerisinde aracılığıyla oluşturulan mevcut bir WordPress web uygulaması ele öğrenin ve WordPress çoklu site için Dönüştür"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a>Birden çok tesis Azure App Service'te WordPress Dönüştür
## <a name="overview"></a>Genel Bakış
*Tarafından [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies, Inc.][ms-open-tech]*

Bu öğreticide, Azure galerisinde aracılığıyla oluşturulan mevcut bir WordPress web uygulaması almak ve bir WordPress çoklu site yükleme dönüştürmek öğreneceksiniz. Ayrıca, her yüklemenizi içinde siteler için özel bir etki alanı atama hakkında bilgi edineceksiniz.

WordPress olan bir yüklemesini sahip varsayılır. Bunu yapmazsanız, Lütfen sağlanan yönergeleri izleyin [Azure galerisinden bir WordPress web sitesi oluşturmak][website-from-gallery].

Varolan bir WordPress dönüştürme tek bir site yüklemek için birden çok tesis genellikle oldukça basittir ve ilk adımlar burada çoğunu düz nereden geldiği [A ağ oluştur] [ wordpress-codex-create-a-network] sayfasında [ WordPress Codex](http://codex.wordpress.org).

Haydi başlayalım.

## <a name="allow-multisite"></a>Birden çok tesis izin ver
İlk aracılığıyla çoklu site etkinleştirmeniz gerekiyor `wp-config.php` ile dosya **WP\_izin\_birden çok TESİS** sabit. Web uygulama dosyalarınızı düzenlemek için iki yöntem vardır: FTP ve Git aracılığıyla ikinci ilk aracılığıyladır. Lütfen, bu yöntemlerden birini Kurulum konusunda bilginiz yoksa, aşağıdaki öğreticiler başvurun:

* [PHP web sitesiyle MySQL ve FTP][website-w-mysql-and-ftp-ftp-setup]
* [PHP web sitesiyle MySQL ve Git][website-w-mysql-and-git-git-setup]

Açık `wp-config.php` dosya düzenleyicisiyle ve yukarıdaki aşağıdakileri ekleyin `/* That's all, stop editing! Happy blogging. */` satır.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Dosyayı kaydedin ve sunucuya geri yüklemek emin olun!

## <a name="network-setup"></a>Ağ Kurulumu
Oturum *wp-yönetici* web uygulamanız ve alanının altında yeni bir öğe görmelisiniz **Araçları** adlı menüsü **ağ kurulumu**. Tıklatın **ağ kurulumu** ve ağınızın ayrıntıları doldurun.

![Ağ Kurulum Ekranı][wordpress-network-setup]

Bu öğretici kullanır *alt dizinleri* çünkü her zaman çalışması gerekir ve size özel etki alanları her alt site için daha sonra öğreticide ayarlarını yapacak şema site. Ancak, bir alt etki alanı yüklemek üzerinden bir etki alanına eşlerseniz Kurulum mümkün olmalıdır [Azure Portal](https://portal.azure.com) ve joker DNS düzgün şekilde ayarlayın.

Alt dizin kurulumları alt etki alanı vs hakkında daha fazla bilgi için bkz: [çok siteli ağ türlerini] [ wordpress-codex-types-of-networks] makale üzerinde WordPress Codex.

## <a name="enable-the-network"></a>Ağ etkinleştir
Ağ veritabanında yapılandırılmıştır, ancak ağ işlevselliğini etkinleştirmek için bir geri kalan adımı yok. Sonlandırma `wp-config.php` ayarları ve olun `web.config` her site düzgün bir şekilde yönlendirir.

' I tıklattıktan sonra **yükleme** düğmesini *ağ kurulumu* sayfasında, WordPress güncelleştirmek deneyecek `wp-config.php` ve `web.config` dosyaları. Ancak, güncelleştirmelerinin başarılı sağlamak üzere dosyaları her zaman kontrol etmeniz gerekir. Aksi durumda, bu ekranı ile gerekli güncelleştirmeleri sunacaktır. Düzenle ve dosyaları kaydedebilir.

Yaptıktan sonra oturumu kapatın ve oturum gerekir bu güncelleştirmeler wp-yönetici panoya yedekleyin.

Şimdi olmamalıdır ek bir menü etiketli yönetici çubuğunda **Sitelerim**. Bu menü, yeni ağınız üzerinden denetlemenize olanak tanır **ağ yönetim** Pano.

## <a name="adding-custom-domains"></a>Özel etki alanlarını ekleme
[WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] eklentisi özel etki alanlarını, ağınızdaki herhangi bir siteye eklemek için bir kolay sağlar. Eklenti düzgün çalışması Portal ve etki alanı kayıt şirketinizdeki bazı ek ayar yapmanız gerekir.

## <a name="enable-domain-mapping-to-the-web-app"></a>Web uygulamasının etki alanı eşleştirmeye izin ver
**Serbest** [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) planı modu Web uygulamaları için özel etki alanlarını ekleme desteklemez. Geçiş gerekecek **paylaşılan** veya **standart** modu. Bunu yapmak için:

* Azure portalında oturum açın ve web uygulamanızı bulun. 
* Tıklayın **ölçeği** sekmesinde **ayarları**.
* Altında **genel**, şunlardan birini seçin *paylaşılan* veya *standart*
* Tıklatın **Kaydet**

Kullanım ve ayarladığınız yapılandırmanın bağlı olarak değişiklik doğrulayın ve web uygulamanız şimdi bir maliyet maruz kalabilirsiniz kabul isteyen bir ileti alabilirsiniz.

Yeni ayarları işlemek için birkaç saniye sürer artık etki alanınızı ayarlama başlatmak için uygun bir zamandır.

## <a name="verify-your-domain"></a>Etki alanınızı doğrulayın
Azure Web Apps siteye etki alanını eşlemek sağlayacak önce ilk etki alanını eşlemek için yetkiye sahip doğrulamanız gerekir. Bunu yapmak için yeni bir CNAME kaydı, DNS girdisini eklemeniz gerekir.

* Etki alanınızın DNS Yöneticisi için oturum açın
* Yeni bir CNAME oluşturmanız *awverify*
* Noktası *awverify* için *awverify. YOUR_DOMAIN.azurewebsites.NET*

DNS değişikliklerin tam yürürlüğe gidin, aşağıdaki adımları hemen çalışmazsa kahve, kupaya olun sonra geri dönün ve yeniden deneyin şekilde gitmek biraz zaman alabilir.

## <a name="add-the-domain-to-the-web-app"></a>Web uygulaması için etki alanı ekleme
Web uygulamanız Azure Portalı aracılığıyla dönün, tıklatın **ayarları**ve ardından **özel etki alanları ve SSL**.

Zaman *SSL ayarları* olan görüntülenir, burada girdiğiniz web uygulamanıza atamak istediğiniz tüm etki alanları görürsünüz. Bir etki alanı burada listelenmiyorsa, DNS etki alanı kurulumu nasıl olduğunu bağımsız olarak eşleme WordPress içinde kullanılabilir olmaz.

![Özel etki alanlarını iletişim yönetme][wordpress-manage-domains]

Azure etki alanınızın metin kutusuna yazdıktan sonra daha önce oluşturduğunuz CNAME kaydı doğrular. DNS tam olarak yayılmadan değil varsa, kırmızı bir gösterge gösterir. Başarılı olduysa, yeşil bir onay işareti görürsünüz. 

İletişim kutusunun en altında listelenen IP adresini not alın. Bu kurulum, etki alanınız için A kaydı gerekir.

## <a name="setup-the-domain-a-record"></a>Etki alanı kayıt Kurulumu
Diğer adımlar başarılı olursa, Azure web uygulamanıza bir DNS A kaydı aracılığıyla etki alanı artık atayabilir. 

Burada Azure web uygulamaları CNAME ve A kayıtları ancak kabul olduğunu dikkate almak önemlidir, *gerekir* uygun etki alanı eşleme etkinleştirmek için bir A kaydı kullanın. Nelerin sizin için YOUR_DOMAIN.azurewebsites.net ile oluşturulan Azure olduğu başka bir CNAME için bir CNAME iletilemez.

Önceki adımdaki IP adresini kullanarak, DNS Yöneticisi'ne dönmek ve kurulum için bu IP işaret edecek şekilde A kaydı.

## <a name="install-and-setup-the-plugin"></a>Yükleme ve Kurulum eklentisi
WordPress çoklu site şu anda özel etki alanlarını eşlemek için yerleşik bir yöntem sahip değil. Ancak, adlı bir eklenti yoktur [WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] , sizin için işlevsellik ekler. Sitenizin ağ yönetim bölümünü oturum açın ve yükleme **WordPress MU etki alanı eşleme** eklentisi.

Yükleme ve eklenti etkinleştirdikten sonra ziyaret edin **ayarları** > **etki alanı eşleme** eklentiyi yapılandırmak için. İlk metin kutusuna *sunucusu IP adresi*, etki alanı için bir kayıt kurulumu için kullanılan IP adresi girin. Herhangi ayarlayın *etki alanı seçenekleri* size (varsayılan değerler genellikle ince) istekleri ve tıklayın **kaydetmek**.

## <a name="map-the-domain"></a>Etki alanına Eşle
Ziyaret **Pano** etki alanına Eşle istediğiniz site için. Tıklayın **Araçları** > **etki alanı eşleme** ve yeni etki alanı tıklatın ve metin kutusu yazın **Ekle**.

Varsayılan olarak, yeni etki alanı otomatik olarak oluşturulur site, etki alanı için yazılacaktır. Yeni etki alanına onay gönderilen tüm trafiğin sahip olmak istiyorsanız *bu blog için birincil etki alanı* kutusunu kaydetmeden önce. Etki alanları sınırsız sayıda bir siteye ekleyebilirsiniz, ancak yalnızca bir birincil olabilir.

## <a name="do-it-again"></a>Yeniden yapın
Azure Web uygulamaları bir web uygulaması için etki alanları sınırsız sayıda eklemenize izin verir. Yürütülecek gerekir başka bir etki alanına eklemek için **etki alanınızı doğrulayın** ve **etki alanı kayıt Kurulum** bölümler her etki alanı için.    

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


