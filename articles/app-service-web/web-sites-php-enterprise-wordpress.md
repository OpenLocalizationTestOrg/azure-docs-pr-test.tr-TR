---
title: "Azure üzerinde aaaEnterprise sınıfı WordPress | Microsoft Docs"
description: "Nasıl toohost bir kurumsal sınıf WordPress sitesi Azure App Service hakkında bilgi edinin"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Azure üzerinde WordPress kurumsal sınıf
Azure uygulama hizmeti sağlayan ölçeklenebilir, güvenli ve kullanımı kolay bir ortam için kritik, büyük ölçekli [WordPress] [ wordpress] siteleri. Microsoft kendisini çalıştıran hello gibi kurumsal sınıf siteleri [Office] [ officeblog] ve [Bing] [ bingblog] bloglar. Bu makalede nasıl toouse tooestablish Microsoft Azure App Service Web Apps özelliğini hello ve bakımını bir kurumsal sınıf, büyük hacimli ziyaretçi işleyebilir bulut tabanlı WordPress sitesi gösterilmektedir.

## <a name="architecture-and-planning"></a>Mimari ve planlama
Temel bir WordPress yüklemesi yalnızca iki gereksinimlere sahiptir:

* **MySQL veritabanı**: Bu gereksinim aracılığıyla kullanılabilir [hello Azure Marketi ClearDB][cdbnstore]. Alternatif olarak, kendi MySQL yükleme Azure sanal makineler üzerinde kullanarak yönetebileceğiniz [Windows] [ mysqlwindows] veya [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB birkaç MySQL yapılandırmaları sağlar. Her yapılandırma farklı performans özellikleri vardır. Merhaba bkz [Azure depolama] [ cdbnstore] hello Azure depolama üzerinden veya doğrudan hello üzerinde görülen sağlanan teklifleri hakkında bilgi için [ClearDB Web sitesi](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 veya daha büyük**: Azure uygulama hizmeti şu anda sağlar [PHP sürümleri 5.4, 5.5 ve 5.6][phpwebsite].

  > [!NOTE]
  > Böylece hello en son güvenlik düzeltmelerini sahip bu, her zaman çalışma hello en son sürümünü PHP öneririz.
  >
  >

### <a name="basic-deployment"></a>Temel dağıtımı
Yalnızca hello temel gereksinimleri kullanırsanız, bir Azure bölgesi içinde temel bir çözüm oluşturabilirsiniz.

![Bir Azure web uygulaması ve MySQL veritabanı tek bir Azure bölgesinde barındırılan][basic-diagram]

Bu, uygulamanızın kullanıma hello site tooscale birden çok Web Apps örneği oluşturmanıza izin verir ancak her şeyi belirli bir coğrafi bölgede hello veri merkezleri içinde barındırılır. Bu bölge dışında ziyaretçilerden hello site kullandığınızda yavaş yanıt sürelerini görebilirsiniz. Bu bölgede Hello veri merkezleri devre dışı kalırsa, bu nedenle, uygulamanızın yapar.

### <a name="multi-region-deployment"></a>Çok bölge dağıtımı
Azure kullanarak [trafik Yöneticisi][trafficmanager], birden çok coğrafi bölgeler arasında WordPress sitenizi ölçeklendirin ve sağlayan tüm ziyaretçiler için aynı URL'ye hello. Tüm ziyaretçiler trafik Yöneticisi ile gelir ve dayanır yönlendirilmiş tooa bölge hello sonra Yük Dengeleme yapılandırma değildir.

![Bölgeler arasında CDBR yüksek kullanılabilirlik yönlendirici tooroute tooMySQL kullanarak birden çok bölgede bulunan bir Azure web uygulaması][multi-region-diagram]

Her bir bölge içinde hello WordPress sitesi hala birden çok Web Apps örneklerinde genişletilmiş, ancak bu ölçeklendirme belirli tooa bölgedir. Yüksek trafik bölgeler ve trafiği düşük bölgeleri farklı şekilde genişletilebilir.

kullanabileceğiniz tooreplicate ve rota trafiği toomultiple MySQL veritabanları [ClearDB yüksek kullanılabilirlik yönlendiricileri (CDBRs)] [ cleardbscale] (sol gösterilen) veya [MySQL küme taşıyıcı düzeyde Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Medya depolama ve önbelleğe alma ile bölgeli dağıtımı
Merhaba site yüklemeleri veya hosts medya dosyalarını kabul ederse, Azure Blob Depolama kullanın. Önbelleğe alma gerekiyorsa düşünün [Redis önbelleği][rediscache], [Memcache bulut](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), veya diğer önbelleğe alma tekliflerini hello hello biri [Azure depolama](http://azure.microsoft.com/gallery/store/).

![Yönetilen önbellek, Blob Depolama ve içerik teslim ağı MySQL için CDBR yüksek kullanılabilirlik yönlendirici kullanarak birden çok bölgede bulunan bir Azure web uygulaması][performance-diagram]

Dosyaları tüm siteler arasında çoğaltma hakkında tooworry aktarıp blob depolama bölgelere varsayılan olarak, coğrafi olarak dağıtılmış. Hello Azure etkinleştirebilirsiniz [içerik teslim ağı] [ cdn] Blob Depolama için hangi dağıtır daha yakından tooyour ziyaretçileri dosyaları tooend düğümlerini.

### <a name="planning"></a>Planlama
#### <a name="additional-requirements"></a>Ek gereksinimler
| toodo bu... | Bunu kullanın... |
| --- | --- |
| **Büyük dosyaları depolamak ya da karşıya yükle** |[WordPress eklentisini Blob storage kullanma][storageplugin] |
| **E-posta Gönder** |[SendGrid] [ storesendgrid] ve hello [WordPress eklentisini SendGrid kullanma][sendgridplugin] |
| **Özel etki alanı adları** |[Azure App Service'te özel etki alanı adı yapılandırma][customdomain] |
| **HTTPS** |[Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir][httpscustomdomain] |
| **Üretim öncesi doğrulama** |[Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama][staging] <p>Bir web uygulaması tooproduction hazırlama taşıdığınızda, ayrıca hello WordPress yapılandırma taşıyın. Hazırlanan hello uygulama tooproduction geçmeden önce tüm ayarları üretim uygulamanız için güncelleştirilmiş toohello gereksinimleri olduğundan emin olun.</p> |
| **İzleme ve sorun giderme** |[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme] [ log] ve [Azure App Service'te Web uygulamalarını izleme][monitor] |
| **Sitenizi dağıtma** |[Azure App Service'te bir web uygulaması dağıtma][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Kullanılabilirlik ve olağanüstü durum kurtarma
| toodo bu... | Bunu kullanın... |
| --- | --- |
| **Yük Dengeleme siteleri** veya **coğrafi-siteler dağıtın** |[Azure Traffic Manager ile trafiği yönlendirme][trafficmanager] |
| **Yedekleme ve geri yükleme** |[Azure App Service'te bir web uygulaması yedekleme] [ backup] ve [Azure App Service'in web uygulamasında geri yükleme][restore] |

#### <a name="performance"></a>Performans
Merhaba bulutta performans temelde önbelleğe alma ve ölçeklendirme elde edilir. Ancak, hello bellek, bant genişliği ve Web uygulamalarını barındırma diğer öznitelikleri dikkate alınmalıdır.

| toodo bu... | Bunu kullanın... |
| --- | --- |
| **App Service örneği özelliklerini anlama** |[Uygulama hizmet katmanları yeteneklerini de dahil olmak üzere fiyatlandırma ayrıntıları][websitepricing] |
| **Önbelleği kaynakları** |[Redis önbelleği][rediscache], [Memcache bulut](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), veya diğer önbelleğe alma tekliflerini hello hello biri [Azure depolama](/gallery/store/) |
| **Uygulamanızı ölçeklendirme** |[Bir web uygulamasını Azure App Service'te ölçeklendirme] [ websitescale] ve [ClearDB yüksek kullanılabilirlik yönlendirme][cleardbscale]. Toohost'yı seçerseniz ve kendi MySQL yükleme Yönetimi düşünmelisiniz [MySQL küme CGE] [ cge] genişleme için. |

#### <a name="migration"></a>Geçiş
Varolan bir WordPress sitesi tooAzure uygulama hizmeti iki yöntem toomigrate vardır:

* **[WordPress verme][export]**: Bu yöntem, blog Merhaba içeriğine dışa aktarır. Ardından hello içerik tooa Yeni WordPress sitesi Azure App Service'te hello kullanarak alabileceğiniz [WordPress içeri Aktarıcı eklentisi][import].

  > [!NOTE]
  > Bu işlem, içeriğe geçirmenizi sağlayan olsa da, herhangi bir eklentiniz, temalar veya başka özelleştirmeler geçirmez. Bu bileşenleri yeniden el ile yüklemeniz gerekir.
  >
  >
* **El ile geçiş**: [sitenizi yedekleme] [ wordpressbackup] ve [veritabanı][wordpressdbbackup]ve daha sonra el ile tooa web uygulamasına geri Uygulama hizmeti ve ilişkili MySQL veritabanı. Bu yöntem yararlı toomigrate yüksek oranda özelleştirilmiş siteleri çünkü eklentileri, temalar ve diğer özelleştirmeleri el ile yükleme hello birçoğunu ortadan kaldırır.

## <a name="step-by-step-instructions"></a>Adım adım yönergeler
### <a name="create-a-wordpress-site"></a>WordPress sitesi oluştur
1. Kullanım hello [Azure Marketi] [ cdbnstore] toocreate hello tanımlanan hello boyutta bir MySQL veritabanı [mimari ve planlama](#planning) hello bölge veya bölgelerde bölümü Burada, sitenizi barındırır.
2. Merhaba adımları [Azure App Service'te bir WordPress web uygulaması oluşturma] [ createwordpress] toocreate bir WordPress web uygulaması. Merhaba web uygulaması oluşturduğunuzda seçmeniz **mevcut bir MySQL veritabanını kullan**ve ardından adım 1'de oluşturulan hello veritabanı seçin.

Var olan bir WordPress sitesi geçiriyorsanız, bkz: [var olan bir WordPress sitesi tooAzure geçirmek](#Migrate-an-existing-WordPress-site-to-Azure) yeni bir web uygulaması oluşturduktan sonra.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Varolan bir WordPress sitesi tooAzure geçirme
Hello belirtildiği gibi [mimari ve planlama](#planning) bölümünde, WordPress sitesi iki yolu toomigrate vardır:

* **Dışarı ve içeri aktarma** kadar özelleştirme değilsiniz veya yalnızca istediğiniz toomove hello içeriği siteler için.
* **Kullanım yedekleme ve geri yükleme** istediğiniz toomove her şeyi özelleştirme pek çok siteler için.

Aşağıdaki bölümlerde toomigrate hello sitenizi kullanın.

#### <a name="hello-export-and-import-method"></a>hello dışa ve içe aktarma yöntemi
1. Kullanım [WordPress verme] [ export] tooexport var olan site.
2. Hello hello adımları kullanarak bir web uygulaması oluşturma [bir WordPress sitesi oluşturmak](#Create-a-new-WordPress-site) bölümü.
3. Oturum açma tooyour WordPress hello sitesinde [Azure portal][mgmtportal]ve ardından **eklentileri** > **yeni Ekle**. Arayıp hello Yükle **WordPress içeri Aktarıcı** eklentisi.
4. Merhaba WordPress içeri Aktarıcı eklentisi yüklendikten sonra tıklatın **Araçları** > **alma**ve ardından **WordPress** toouse hello WordPress içeri Aktarıcı eklentisi.
5. Merhaba üzerinde **alma WordPress** sayfasında, **Dosya Seç**. Varolan WordPress sitenizden dışarı aktarılan hello WXR dosyasını bulun ve ardından **karşıya yükleme dosyasını ve içeri aktarma**.
6. Tıklatın **gönderme**. Merhaba alma işleminin başarılı olduğunu istenir.
7. Tüm bu adımları tamamladıktan sonra sitenizden yeniden kendi **uygulama hizmetleri** dikey penceresinde hello [Azure portal][mgmtportal].

Merhaba site içeri aktardıktan sonra hello içeri aktarma dosyasında olmayan adımları tooenable ayarlarını aşağıdaki tooperform hello gerekebilir.

| Bu kullanıyorsanız... | Bunu yapmak... |
| --- | --- |
| **Sabit bağlantıları** |Hello WordPress panodan hello yeni sitenin tıklatın **ayarları** > **sabit bağlantıları**ve ardından hello sabit bağlantıları yapısı güncelleştirin. |
| **Görüntü/medya bağlantılar** |tooupdate bağlantılar toohello yeni konumu, hello kullan [Velvet mavi güncelleştirme URL'leri eklentisi][velvet], bulma ve aracı veya veritabanınızda hello bağlantıları el ile güncelleştirmeniz değiştirme. |
| **Temalar** |Çok Git**Görünüm** > **tema**ve ardından hello sitesi teması gerektiği gibi güncelleştirin. |
| **Menüleri** |Tema menüleri destekliyorsa, bağlantılar tooyour giriş sayfası hello eski alt bunları katıştırılmış sahip olabilirsiniz. Çok Git**Görünüm** > **menüleri**ve bunları güncelleştirin. |

#### <a name="hello-backup-and-restore-method"></a>Merhaba yedekleme ve geri yükleme yöntemi
1. Geri varolan, WordPress sitesi hello bilgileri kullanarak [WordPress yedeklemeleri][wordpressbackup].
2. Merhaba bilgileri kullanarak geri, var olan veritabanını [, veritabanını yedekleme][wordpressdbbackup].
3. Bir veritabanı oluşturun ve hello yedekleme geri yükleyin.

   1. Merhaba yeni bir veritabanından satın [Azure Marketi][cdbnstore], veya üzerinde bir MySQL veritabanı ayarlama bir [Windows] [ mysqlwindows] veya [Linux ] [ mysqllinux] sanal makine.
   2. Bir MySQL istemci gibi kullanın [MySQL çalışma ekranı] [ workbench] tooconnect toohello yeni veritabanı ve WordPress veritabanınızı alın.
   3. Merhaba veritabanı toochange hello etki alanı girişleri tooyour yeni Azure uygulama hizmeti etki alanı, örneğin, mywordpress.azurewebsites.net güncelleştirin. Kullanım hello [arama ve değiştirme için WordPress veritabanları komut] [ searchandreplace] toosafely tüm örneklerini değiştirin.
4. Hello Azure portalında bir web uygulaması oluşturma ve yayımlama hello WordPress yedekleme.

   1. bir veritabanı hello sahip bir web uygulaması toocreate [Azure portal][mgmtportal], tıklatın **yeni** > **Web + mobil**  >  **Azure Market** > **Web uygulamaları** > **Web uygulaması + SQL** (veya **Web uygulaması + MySQL**) > **Oluşturma**. Tüm gerekli hello ayarları toocreate boş web uygulaması yapılandırın.
   2. WordPress yedeklemenize hello bulun **wp-config.php** dosyası ve bir düzenleyicide açın. Yeni MySQL veritabanınız için hello bilgilerle girişleri aşağıdaki hello değiştirin:

      * **DB_NAME**: hello veritabanının hello kullanıcı adı.
      * **DB_USER**: hello kullanıcı kullanılan ad tooaccess hello veritabanı.
      * **DB_PASSWORD**: hello kullanıcı parolası.

        Bu girişler değiştirdikten sonra kaydedin ve kapatın hello **wp-config.php** dosya.
   3. Kullanım hello [Azure App Service'te bir web uygulaması dağıtma] [ deploy] toouse istediğiniz ve Azure App Service'te WordPress yedekleme tooyour web uygulamanızı dağıtmak bilgi tooenable hello dağıtım yöntemi.
5. Merhaba WordPress sitesi dağıtıldıktan sonra mümkün tooaccess hello yeni site (bir App Service web uygulaması) hello kullanarak olmalısınız *. hello sitesinin azurewebsite.net URL'si.

### <a name="configure-your-site"></a>Sitenizi yapılandırmak
Merhaba WordPress sitesi oluşturulan ya da geçirilen sonra bilgi tooimprove performansı izleyerek hello kullanın veya ek işlevsellik etkinleştirin.

| toodo bu... | Bunu kullanın... |
| --- | --- |
| **Uygulama hizmeti planı modu, boyutu ve etkin ölçeklendirme ayarlayın** |[Bir web uygulamasını Azure App Service'te ölçeklendirme][websitescale]. |
| **Kalıcı veritabanı bağlantılarını etkinleştirin** |Varsayılan olarak, WordPress sonra birden çok bağlantı kısıtlanan, bağlantı toohello veritabanı toobecome neden olabilecek kalıcı veritabanı bağlantılarını kullanmaz. tooenable kalıcı bağlantılar, yükleme hello [kalıcı bağlantılar bağdaştırıcısı eklentisi](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Performansı** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Merhaba ARR tanımlama bilgisi devre dışı</a>, hangi performansı arttırabilir WordPress birden çok Web uygulamaları örnekleri üzerinde çalıştığında.</p></li><li><p>Önbelleğe almayı etkinleştir. Kullanabileceğiniz <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">Redis önbelleği</a> (Önizleme) ile Merhaba <a href="https://wordpress.org/plugins/redis-object-cache/">nesne önbelleği WordPress eklentisini Redis</a>, veya hello birini hello önbelleğe alma diğer sunduğu kullanabilirsiniz <a href="/gallery/store/">Azure depolama</a>.</p></li><li><p>[Wincache ile daha hızlı WordPress olun](https://wordpress.org/plugins/w3-total-cache/). Wincache, web uygulamaları için varsayılan olarak etkindir. WinCache ve dinamik önbellek birlikte kullanılırken, WinCache'nin dosya önbelleği devre dışı bırakmak, ancak hello kullanıcı ve oturum önbellek etkin bırakın. dosya önbelleği, sistem düzeyinde .ini dosyası, devre dışı tooturn hello aşağıdaki değeri ayarlayın:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Bir web uygulamasını Azure App Service'te ölçeklendirme] [ websitescale] ve <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB yüksek kullanılabilirlik yönlendirme</a> veya <a href="http://www.mysql.com/products/cluster/">MySQL küme CGE</a>.</p></li></ul> |
| **BLOB depolama alanını kullanın** |<ol><li><p>[Bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md).</p></li><li><p>Nasıl çok öğrenin[kullanım hello içerik dağıtım ağı](../cdn/cdn-create-new-endpoint.md) toogeo-blob'larda depolanan verileri dağıtın.</p></li><li><p>Yükleme ve yapılandırma hello <a href="https://wordpress.org/plugins/windows-azure-storage/">WordPress eklentisini için Azure Storage</a>.</p><p>Ayrıntılı Kurulum ve yapılandırma bilgilerini hello eklentisi için hello bkz <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">Kullanıcı Kılavuzu</a>.</p> </li></ol> |
| **E-posta etkinleştir** |Etkinleştirme <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> hello Azure Store kullanarak. Merhaba yüklemek <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid eklentisi</a> WordPress için. |
| **Bir özel etki alanı adı yapılandırma** |[Azure App Service'te özel etki alanı adı yapılandırma][customdomain]. |
| **Özel etki alanı adı için HTTPS'yi etkinleştir** |[Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir][httpscustomdomain]. |
| **Yük Dengeleme veya coğrafi-sitenizi Dağıt** |[Rota trafiği Azure Traffic Manager ile][trafficmanager]. Özel bir etki alanı kullanıyorsanız, bkz: [Azure App Service'te özel etki alanı adı yapılandırma] [ customdomain] hakkında bilgi için özel etki alanı adları ile toouse trafik Yöneticisi. |
| **Otomatik yedeklemeler etkinleştir** |[Azure App Service'te bir web uygulaması yedekleme][backup]. |
| **Tanılama günlük kaydını etkinleştir** |[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme][log]. |

## <a name="next-steps"></a>Sonraki adımlar
* [WordPress en iyi duruma getirme](http://codex.wordpress.org/WordPress_Optimization)
* [Azure App Service'te WordPress toomultisite Dönüştür](web-sites-php-convert-wordpress-multisite.md)
* [ClearDB Yükseltme Sihirbazı'nı Azure](http://www.cleardb.com/store/azure/upgrade)
* [WordPress web uygulamanızı Azure App Service'te bir alt klasör barındırma](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Adım adım: Azure kullanarak bir WordPress sitesi oluşturma](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Varolan WordPress blogunuz Azure ile ilgili ana bilgisayar](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [WordPress, asıl sabit bağlantıları etkinleştirme](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Nasıl toomigrate ve Azure uygulama hizmeti WordPress blogunuz Çalıştır](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Azure App Service'te WordPress toorun serbest nasıl](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [İki dakika veya daha az Azure üzerinde WordPress](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Bir WordPress blog tooAzure - 1. Bölüm taşıma: Azure üzerinde bir WordPress blog oluşturma](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Taşıma bir WordPress blog tooAzure - 2. parça: içeriğinizi aktarma](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Bir WordPress blog tooAzure - bölümü 3 taşıma: özel etki alanınızı ayarlama](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Bir WordPress blog tooAzure - bölümü 4 taşıma: asıl sabit bağlantıları ve URL yeniden yazma kuralları](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Bir WordPress blog tooAzure - bölümü 5 taşıma: bir alt klasör toohello kökünden taşıma](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Nasıl tooset oluşturan bir WordPress web uygulaması Azure hesabınızda](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Azure üzerinde WordPress propping](http://www.johnpapa.net/wordpress-on-azure/)
* [Azure üzerinde WordPress için ipuçları](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı gerekmez ve hiçbir taahhüt yoktur.
>
>

## <a name="whats-changed"></a>Yapılan değişiklikler
Web siteleri tooApp hizmet gelen bir kılavuzu toohello değişiklik için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
