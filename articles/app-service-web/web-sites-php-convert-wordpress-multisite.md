---
title: Azure App Service'te WordPress tooMultisite aaaConvert
description: "Nasıl tootake var olan bir WordPress web uygulaması Azure hello Galerisi'nde aracılığıyla oluşturulan ve tooWordPress birden çok tesis Dönüştür öğrenin"
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
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Azure App Service'te WordPress tooMultisite Dönüştür
## <a name="overview"></a>Genel Bakış
*Tarafından [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies, Inc.][ms-open-tech]*

Bu öğreticide, var olan bir WordPress web uygulaması tootake hello Galerisi'nde Azure ve WordPress birden çok tesis içine yüklemek dönüştürme aracılığıyla nasıl oluşturulacağını öğreneceksiniz. Ayrıca, nasıl tooassign Merhaba, özel etki alanı tooeach yüklemenizi içinde alt site öğreneceksiniz.

WordPress olan bir yüklemesini sahip varsayılır. Bunu yapmazsanız, Lütfen sağlanan hello yönergeleri izleyin [azure'da hello Galeriden bir WordPress web sitesi oluşturmak][website-from-gallery].

Varolan bir WordPress dönüştürme tek bir site yükleme tooMultisite genellikle oldukça basittir ve burada başlangıç adımları hello çoğunu düz hello gelen [A ağ oluştur] [ wordpress-codex-create-a-network] hello sayfasında[WordPress Codex](http://codex.wordpress.org).

Haydi başlayalım.

## <a name="allow-multisite"></a>Birden çok tesis izin ver
İlk tooenable birden çok tesis hello aracılığıyla ihtiyacınız `wp-config.php` hello dosyasıyla **WP\_izin\_birden çok TESİS** sabit. Web uygulama dosyalarınızı iki yöntem tooedit vardır: hello ilk olduğu FTP ve Git aracılığıyla ikinci hello aracılığıyla. Konusunda bilginiz yoksa toosetup bu yöntemlerden birini başvurun öğreticileri aşağıdaki toohello:

* [PHP web sitesiyle MySQL ve FTP][website-w-mysql-and-ftp-ftp-setup]
* [PHP web sitesiyle MySQL ve Git][website-w-mysql-and-git-git-setup]

Açık hello `wp-config.php` dosya seçtiğiniz hello düzenleyicisiyle ve hello yukarıda hello aşağıdakileri ekleyin `/* That's all, stop editing! Happy blogging. */` satır.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Emin toosave hello dosyası olması ve geri toohello sunucu karşıya!

## <a name="network-setup"></a>Ağ Kurulumu
İçinde toohello oturum *wp-yönetici* web uygulamanız ve alan hello altında yeni bir öğe görmeniz gerekir **Araçları** adlı menüsü **ağ kurulumu**. Tıklatın **ağ kurulumu** ve ağınızın hello ayrıntıları doldurun.

![Ağ Kurulum Ekranı][wordpress-network-setup]

Bu öğretici hello kullanır *alt dizinleri* çünkü her zaman çalışması gerekir ve size özel etki alanları her alt site için daha sonra hello öğreticide ayarlarını yapacak şema site. Ancak, bir alt etki alanı yüklemek hello üzerinden bir etki alanına eşlerseniz olası toosetup olmalıdır [Azure Portal](https://portal.azure.com) ve joker DNS düzgün şekilde ayarlayın.

Alt etki alanı vs hakkında daha fazla bilgi için alt dizin kurulumları hello bkz [çok siteli ağ türlerini] [ wordpress-codex-types-of-networks] makale hello WordPress Codex üzerinde.

## <a name="enable-hello-network"></a>Merhaba ağ etkinleştir
Merhaba ağ hello veritabanında yapılandırılmıştır, ancak bir kalan adım tooenable hello ağ işlevi yoktur. Merhaba Sonlandır `wp-config.php` ayarları ve olun `web.config` her site düzgün bir şekilde yönlendirir.

Merhaba tıkladıktan sonra **yükleme** hello düğmesinde *ağ kurulumu* sayfasında, WordPress tooupdate hello deneyecek `wp-config.php` ve `web.config` dosyaları. Ancak, hello dosyaları tooensure hello güncelleştirmeleri başarılı her zaman kontrol etmeniz gerekir. Aksi durumda, bu ekranı hello gerekli güncelleştirmeleri sunacaktır. Düzenle ve hello dosyalarını kaydedin.

Yaptıktan sonra bu güncelleştirmeleri toolog çıkışı ve günlük gerekir hello wp-yönetici panoya yedekleyin.

Şimdi olmamalıdır ek bir menü etiketli hello yönetici çubuğunda **Sitelerim**. Bu menü toocontrol sağlayan yeni ağınızdan hello **ağ yönetim** Pano.

## <a name="adding-custom-domains"></a>Özel etki alanlarını ekleme
Merhaba [WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] eklentisi yapar kolay tooadd özel etki alanlarını tooany site ağınızda. Merhaba eklentisi toooperate sırada düzgün toodo hello Portal ve ayrıca etki alanı kayıt şirketinizdeki bazı ek kurulum gerekir.

## <a name="enable-domain-mapping-toohello-web-app"></a>Etki alanı eşleme toohello web uygulaması etkinleştir
Merhaba **serbest** [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) plan modunda özel etki alanlarını tooWeb uygulamalar ekleme desteklemez. Tooswitch çok gerekir**paylaşılan** veya **standart** modu. toodo bu:

* Toohello Azure portalında oturum açın ve web uygulamanızı bulun. 
* Tıklatın hello üzerinde **ölçeği** sekmesinde **ayarları**.
* Altında **genel**, şunlardan birini seçin *paylaşılan* veya *standart*
* Tıklatın **Kaydet**

Tooverify hello değişiklik soran bir ileti alırsınız ve web uygulamanız şimdi kullanım bağlı olarak bir maliyet doğurur ve belirlediğiniz başka bir yapılandırma hello kabul.

Tooprocess hello yeni ayarları, birkaç saniye sürer etki alanınızın iyi zaman toostart ayarlama böylece sunulmuştur.

## <a name="verify-your-domain"></a>Etki alanınızı doğrulayın
Azure Web Apps toomap bir etki alanı toohello site sağlayacak. önce ilk hello yetkilendirme toomap hello etki alanınız olduğunu tooverify gerekir. toodo bu nedenle, yeni bir CNAME kaydı tooyour DNS girişi eklemeniz gerekir.

* Tooyour etki alanının DNS Yöneticisi'nde oturum
* Yeni bir CNAME oluşturmanız *awverify*
* Noktası *awverify* çok*awverify. YOUR_DOMAIN.azurewebsites.NET*

Bunu süre hello DNS değişiklikleri toogo için tam etkili, aşağıdaki adımları hello hemen çalışmazsa kahve, kupaya olun sonra geri dönün ve yeniden deneyin böylece gidin.

## <a name="add-hello-domain-toohello-web-app"></a>Merhaba etki alanı toohello web uygulaması Ekle
Dönüş tooyour web uygulaması'hello Azure Portal aracılığıyla tıklatın **ayarları**ve ardından **özel etki alanları ve SSL**.

Ne zaman hello *SSL ayarları* olan görüntülenir, burada girdiğiniz tooassign tooyour web uygulaması istediğiniz tüm hello etki alanlarının hello alanların görürsünüz. Bir etki alanı burada listelenmiyorsa, WordPress içinde nasıl hello etki alanı DNS kurulması bağımsız olarak eşleme için kullanılabilir olmaz.

![Özel etki alanlarını iletişim yönetme][wordpress-manage-domains]

Etki alanınızı hello metin kutusuna yazdıktan sonra Azure hello CNAME kaydı daha önce oluşturduğunuz doğrulayın. Merhaba DNS tam olarak yayılmadan değil varsa, kırmızı bir gösterge gösterir. Başarılı olduysa, yeşil bir onay işareti görürsünüz. 

IP adresi hello iletişim hello alt kısmında listelenen hello not edin. Bu toosetup hello kayıt etki alanınız için gerekir.

## <a name="setup-hello-domain-a-record"></a>Kurulum Hello etki alanı A kaydı
Merhaba diğer adımlar başarılı olursa, DNS A kaydına hello etki alanı tooyour Azure web uygulaması şimdi atayabilir. 

Azure web uygulamaları CNAME ve A kayıtları ancak kabul etmiş önemli toonote burada olduğundan, *gerekir* bir A kaydı tooenable uygun etki alanı eşlemesi kullanın. CNAME tooanother CNAME, Azure sizin yerinize YOUR_DOMAIN.azurewebsites.net ile oluşturulan olduğu iletilemez.

Başlangıç IP adresi hello önceki adımdaki kullanarak, tooyour DNS Yöneticisi'ni ve Kurulum hello kayıt toopoint toothat IP döndürür.

## <a name="install-and-setup-hello-plugin"></a>Yükleme ve Kurulum hello eklentisi
WordPress çoklu site şu anda bir yerleşik bir yöntem toomap özel etki alanlarına sahip değil. Ancak adlı bir eklenti yoktur [WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] hello işlevsellik sizin için ekler. Toohello Ağ Yönetim bölümünde, sitenizin günlüğüne bakın ve hello **WordPress MU etki alanı eşleme** eklentisi.

Yükleme ve hello eklentisi etkinleştirme ziyaret sonra **ayarları** > **etki alanı eşleme** tooconfigure hello eklentisi. Merhaba ilk metin kutusuna, *sunucusu IP adresi*, giriş hello toosetup kullanılan IP adresi hello hello etki alanı için bir kaydı. Herhangi ayarlayın *etki alanı seçenekleri* istediğiniz (Merhaba varsayılan değerler genellikle ince) tıklatıp **kaydetmek**.

## <a name="map-hello-domain"></a>Harita hello etki alanı
Merhaba ziyaret **Pano** hello site için toomap hello etki alanına istiyor. Tıklayın **Araçları** > **etki alanı eşleme** ve türü hello yeni etki alanına tıklayın ve hello textbox **Ekle**.

Varsayılan olarak, yeni bir etki alanı hello yeniden toohello otomatik olarak oluşturulur site, etki alanı olacaktır. Tüm gönderilen trafiğin toohello yeni etki alanı toohave istiyorsanız hello denetleyin *bu blog için birincil etki alanı* kutusunu kaydetmeden önce. Etki alanları tooa site sınırsız sayıda ekleyebilirsiniz, ancak yalnızca bir birincil olabilir.

## <a name="do-it-again"></a>Yeniden yapın
Azure Web uygulamaları tooadd etki alanları tooa web uygulaması sınırsız sayıda olanak sağlar. tooadd tooexecute hello gerekir başka bir etki alanı **etki alanınızı doğrulayın** ve **Kurulum hello etki alanı A kaydı** bölümler her etki alanı için.    

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

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


