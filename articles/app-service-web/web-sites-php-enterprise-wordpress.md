---
title: "Azure üzerinde kurumsal sınıf WordPress | Microsoft Docs"
description: "Azure App Service'te bir kurumsal sınıf WordPress sitesini barındırmak öğrenin"
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
ms.openlocfilehash: 21281955458a2632d96a91d884cab13803f4d296
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Azure üzerinde WordPress kurumsal sınıf
Azure uygulama hizmeti sağlayan ölçeklenebilir, güvenli ve kullanımı kolay bir ortam için kritik, büyük ölçekli [WordPress] [ wordpress] siteleri. Microsoft kendisini çalıştıran kurumsal sınıf siteleri gibi [Office] [ officeblog] ve [Bing] [ bingblog] bloglar. Bu makalede kurmak ve bakımını bir kurumsal sınıf, büyük hacimli ziyaretçi işleyebilir WordPress sitesi bulut tabanlı Microsoft Azure App Service Web Apps özelliğini kullanmayı gösterir.

## <a name="architecture-and-planning"></a>Mimari ve planlama
Temel bir WordPress yüklemesi yalnızca iki gereksinimlere sahiptir:

* **MySQL veritabanı**: Bu gereksinim aracılığıyla kullanılabilir [Azure Marketi ClearDB][cdbnstore]. Alternatif olarak, kendi MySQL yükleme Azure sanal makineler üzerinde kullanarak yönetebileceğiniz [Windows] [ mysqlwindows] veya [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB birkaç MySQL yapılandırmaları sağlar. Her yapılandırma farklı performans özellikleri vardır. Bkz: [Azure depolama] [ cdbnstore] Azure depolama üzerinden veya doğrudan üzerinde görülen sağlanan teklifleri hakkında bilgi için [ClearDB Web sitesi](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 veya daha büyük**: Azure uygulama hizmeti şu anda sağlar [PHP sürümleri 5.4, 5.5 ve 5.6][phpwebsite].

  > [!NOTE]
  > Böylece en son güvenlik düzeltmelerini sahip, her zaman en son sürümünü PHP çalıştırmanızı öneririz.
  >
  >

### <a name="basic-deployment"></a>Temel dağıtımı
Yalnızca temel gereksinimleri kullanırsanız, bir Azure bölgesi içinde temel bir çözüm oluşturabilirsiniz.

![Bir Azure web uygulaması ve MySQL veritabanı tek bir Azure bölgesinde barındırılan][basic-diagram]

Bu, uygulamanın ölçeğini genişletmek için site birden çok Web Apps örneği oluşturmanıza izin verir ancak her şeyi veri merkezlerinde belirli bir coğrafi bölge içinde barındırılır. Bu bölge dışında ziyaretçilerden site kullandığınızda yavaş yanıt sürelerini görebilirsiniz. Bu bölgede veri merkezleri devre dışı kalırsa, bu nedenle, uygulamanızın yapar.

### <a name="multi-region-deployment"></a>Çok bölge dağıtımı
Azure kullanarak [trafik Yöneticisi][trafficmanager], birden çok coğrafi bölgeler arasında WordPress sitenizi ölçeklendirin ve tüm ziyaretçiler için aynı URL'yi girin. Tüm ziyaretçiler trafik Yöneticisi ile gelir ve ardından Yük Dengeleyici yapılandırmasını temel alarak bir bölgeye yönlendirilir.

![MySQL için bölgeler arasında yönlendirmek için CDBR yüksek kullanılabilirlik yönlendiricisi kullanan birden çok bölgede bulunan bir Azure web uygulaması][multi-region-diagram]

Her bir bölge içinde WordPress sitesi hala birden çok Web Apps örneklerinde genişletilmiş, ancak bu bir bölgeye özeldir. Yüksek trafik bölgeler ve trafiği düşük bölgeleri farklı şekilde genişletilebilir.

Çoğaltma ve birden çok MySQL veritabanları için trafiği yönlendirmek için kullanabileceğiniz [ClearDB yüksek kullanılabilirlik yönlendiricileri (CDBRs)] [ cleardbscale] (sol gösterilen) veya [MySQL küme taşıyıcı düzeyde Edition (CGE)][cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Medya depolama ve önbelleğe alma ile bölgeli dağıtımı
Site yüklemeleri veya hosts medya dosyalarını kabul ederse, Azure Blob Depolama kullanın. Önbelleğe alma gerekiyorsa düşünün [Redis önbelleği][rediscache], [Memcache bulut](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), veya diğer önbelleğe alma tekliflerini [Azure depolama](http://azure.microsoft.com/gallery/store/).

![Yönetilen önbellek, Blob Depolama ve içerik teslim ağı MySQL için CDBR yüksek kullanılabilirlik yönlendirici kullanarak birden çok bölgede bulunan bir Azure web uygulaması][performance-diagram]

Böylece dosyaları tüm siteler arasında çoğaltma hakkında endişelenmeniz gerekmez blob depolama bölgelere varsayılan olarak, coğrafi olarak dağıtılmış. Azure etkinleştirebilirsiniz [içerik teslim ağı] [ cdn] Blob Depolama için hangi dağıtır, ziyaretçiye daha yakın olan düğümleri sonuna dosyaları.

### <a name="planning"></a>Planlama
#### <a name="additional-requirements"></a>Ek gereksinimler
| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **Büyük dosyaları depolamak ya da karşıya yükle** |[WordPress eklentisini Blob storage kullanma][storageplugin] |
| **E-posta Gönder** |[SendGrid] [ storesendgrid] ve [WordPress eklentisini SendGrid kullanma][sendgridplugin] |
| **Özel etki alanı adları** |[Azure App Service'te özel etki alanı adı yapılandırma][customdomain] |
| **HTTPS** |[Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir][httpscustomdomain] |
| **Üretim öncesi doğrulama** |[Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama][staging] <p>Bir web uygulaması hazırlamadan üretime taşıdığınızda, ayrıca WordPress yapılandırma taşıyın. Hazırlanan uygulama üretime geçmeden önce tüm ayarlar için üretim uygulamanız gereksinimlere güncelleştirildiğinden emin olun.</p> |
| **İzleme ve sorun giderme** |[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme] [ log] ve [Azure App Service'te Web uygulamalarını izleme][monitor] |
| **Sitenizi dağıtma** |[Azure App Service'te bir web uygulaması dağıtma][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Kullanılabilirlik ve olağanüstü durum kurtarma
| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **Yük Dengeleme siteleri** veya **coğrafi-siteler dağıtın** |[Azure Traffic Manager ile trafiği yönlendirme][trafficmanager] |
| **Yedekleme ve geri yükleme** |[Azure App Service'te bir web uygulaması yedekleme] [ backup] ve [Azure App Service'in web uygulamasında geri yükleme][restore] |

#### <a name="performance"></a>Performans
Bulutta performans temelde önbelleğe alma ve ölçeklendirme elde edilir. Ancak, bellek, bant genişliği ve Web uygulamalarını barındırma diğer öznitelikleri dikkate alınmalıdır.

| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **App Service örneği özelliklerini anlama** |[Uygulama hizmet katmanları yeteneklerini de dahil olmak üzere fiyatlandırma ayrıntıları][websitepricing] |
| **Önbelleği kaynakları** |[Redis önbelleği][rediscache], [Memcache bulut](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), veya diğer önbelleğe alma tekliflerini [Azure depolama](/gallery/store/) |
| **Uygulamanızı ölçeklendirme** |[Bir web uygulamasını Azure App Service'te ölçeklendirme] [ websitescale] ve [ClearDB yüksek kullanılabilirlik yönlendirme][cleardbscale]. Ana bilgisayar ve dikkate almanız gereken kendi MySQL yüklemesini yönetmek isterseniz [MySQL küme CGE] [ cge] genişleme için. |

#### <a name="migration"></a>Geçiş
Azure App Service'e var olan bir WordPress sitesi geçirmek için iki yöntem vardır:

* **[WordPress verme][export]**: Bu yöntem, blog içerik dışa aktarır. Daha sonra içeriği Azure App Service üzerinde yeni bir WordPress siteye kullanarak alabilirsiniz [WordPress içeri Aktarıcı eklentisi][import].

  > [!NOTE]
  > Bu işlem, içeriğe geçirmenizi sağlayan olsa da, herhangi bir eklentiniz, temalar veya başka özelleştirmeler geçirmez. Bu bileşenleri yeniden el ile yüklemeniz gerekir.
  >
  >
* **El ile geçiş**: [sitenizi yedekleme] [ wordpressbackup] ve [veritabanı][wordpressdbbackup]ve daha sonra el ile bir web uygulamasını Azure App Service ve ilişkili MySQL veritabanı için geri yükleyin. Eklenti, temalar ve diğer özelleştirmelerin el ile yükleme birçoğunu ortadan kaldırır olduğundan üst düzeyde özelleştirilmiş siteleri geçirmek bu yöntem kullanışlıdır.

## <a name="step-by-step-instructions"></a>Adım adım yönergeler
### <a name="create-a-wordpress-site"></a>WordPress sitesi oluştur
1. Kullanım [Azure Marketi] [ cdbnstore] içinde tanımlanan boyutta bir MySQL veritabanı oluşturmak için [mimari ve planlama](#planning) bölge veya barındırdığınız sitenizi bölgeler bölümünde.
2. Adımları [Azure App Service'te bir WordPress web uygulaması oluşturma] [ createwordpress] bir WordPress web uygulaması oluşturma. Web uygulaması oluşturduğunuzda seçmeniz **mevcut bir MySQL veritabanını kullan**ve ardından adım 1'de oluşturulan veritabanı seçin.

Var olan bir WordPress sitesi geçiriyorsanız, bkz: [var olan bir WordPress sitesi Azure'a geçirmek](#Migrate-an-existing-WordPress-site-to-Azure) yeni bir web uygulaması oluşturduktan sonra.

### <a name="migrate-an-existing-wordpress-site-to-azure"></a>Var olan bir WordPress sitesi Azure'a geçirme
Bölümünde belirtildiği gibi [mimari ve planlama](#planning) bölümünde, WordPress sitesi geçirmek için iki yolu vardır:

* **Dışarı ve içeri aktarma** kadar özelleştirme değilsiniz veya yalnızca istediğiniz içerik taşıma siteler için.
* **Kullanım yedekleme ve geri yükleme** istediğiniz her şeyi taşımak için çok sayıda özelleştirme sahip siteler için.

Aşağıdaki bölümlerde biri sitenizin geçirmek için kullanın.

#### <a name="the-export-and-import-method"></a>Dışarı ve içeri aktarma yöntemi
1. Kullanım [WordPress verme] [ export] var olan sitenize vermek için.
2. ' Ndaki adımları kullanarak bir web uygulaması oluşturma [bir WordPress sitesi oluşturmak](#Create-a-new-WordPress-site) bölümü.
3. Oturum WordPress sitenize [Azure portal][mgmtportal]ve ardından **eklentileri** > **yeni Ekle**. Arayın ve yükleyin **WordPress içeri Aktarıcı** eklentisi.
4. WordPress içeri Aktarıcı eklentisi yüklendikten sonra tıklatın **Araçları** > **alma**ve ardından **WordPress** WordPress içeri Aktarıcı eklentisini kullanmak için.
5. Üzerinde **alma WordPress** sayfasında, **Dosya Seç**. Varolan WordPress sitenizden dışarı aktarılan WXR dosyasını bulun ve ardından **karşıya yükleme dosyasını ve içeri aktarma**.
6. Tıklatın **gönderme**. Alma işleminin başarılı olduğunu istenir.
7. Tüm bu adımları tamamladıktan sonra sitenizden yeniden kendi **uygulama hizmetleri** dikey penceresinde [Azure portal][mgmtportal].

Site içe aktardıktan sonra içeri aktarma dosyasında olmayan ayarlarını etkinleştirmek için aşağıdaki adımları gerçekleştirmeniz gerekebilir.

| Bu kullanıyorsanız... | Bunu yapmak... |
| --- | --- |
| **Sabit bağlantıları** |Yeni site WordPress panodan tıklatın **ayarları** > **sabit bağlantıları**ve sabit bağlantıları yapısı güncelleştirin. |
| **Görüntü/medya bağlantılar** |Yeni bir konuma bağlantıları güncelleştirmek için kullanmak [Velvet mavi güncelleştirme URL'leri eklentisi][velvet], bulma ve aracı veya veritabanınızı bağlantıları el ile güncelleştirmeniz değiştirme. |
| **Temalar** |Git **Görünüm** > **tema**ve ardından sitenin temasını gerektiği gibi güncelleştirin. |
| **Menüleri** |Tema menüleri destekliyorsa, giriş sayfanızın bağlantılar hala bunları katıştırılmış eski alt olabilir. Git **Görünüm** > **menüleri**ve bunları güncelleştirin. |

#### <a name="the-backup-and-restore-method"></a>Yedekleme ve geri yükleme yöntemi
1. Geri varolan, WordPress sitesi bölümündeki bilgileri kullanarak [WordPress yedeklemeleri][wordpressbackup].
2. Bilgileri kullanarak geri, var olan veritabanını [, veritabanını yedekleme][wordpressdbbackup].
3. Bir veritabanı oluşturun ve yedekleme geri yükleyin.

   1. Yeni bir veritabanından satın [Azure Marketi][cdbnstore], veya üzerinde bir MySQL veritabanı ayarlama bir [Windows] [ mysqlwindows] veya [Linux] [ mysqllinux] sanal makine.
   2. Bir MySQL istemci gibi kullanın [MySQL çalışma ekranı] [ workbench] yeni veritabanına bağlanıp WordPress veritabanınızı içeri aktarın.
   3. Yeni Azure App Service etki alanınıza, örneğin, mywordpress.azurewebsites.net etki alanının girişlerini değiştirmek için veritabanı güncelleştirin. Kullanım [arama ve değiştirme için WordPress veritabanları komut] [ searchandreplace] güvenle tüm örnekleri değiştirmek için.
4. Azure portalında bir web uygulaması oluşturma ve WordPress yedekleme yayımlayın.

   1. Bir veritabanı içinde sahip bir web uygulaması oluşturmak için [Azure portal][mgmtportal], tıklatın **yeni** > **Web + mobil** > **Azure Marketi** > **Web Apps** > **Web uygulaması + SQL** (veya **Web uygulaması + MySQL**) > **oluşturma**. Boş web uygulaması oluşturmak için gerekli tüm ayarları yapılandırın.
   2. WordPress yedeklemenize bulun **wp-config.php** dosyası ve bir düzenleyicide açın. Yeni MySQL veritabanınız için bilgilerle aşağıdaki girdileri değiştirin:

      * **DB_NAME**: veritabanı kullanıcı adı.
      * **DB_USER**: veritabanına erişmek için kullanılan kullanıcı adı.
      * **DB_PASSWORD**: kullanıcı parolası.

        Bu girişler değiştirdikten sonra kaydedin ve kapatın **wp-config.php** dosya.
   3. Kullanmak [Azure App Service'te bir web uygulaması dağıtma] [ deploy] kullanın ve ardından web uygulamanızı Azure App Service'te WordPress yedekleme dağıtmak istediğiniz dağıtım yöntemini etkinleştirmek için bilgi.
5. WordPress sitesi dağıtıldıktan sonra yeni site (olarak App Service web uygulaması) kullanarak erişebiliyor olmalısınız *. site için azurewebsite.net URL.

### <a name="configure-your-site"></a>Sitenizi yapılandırmak
WordPress sitesi geçişi veya oluşturulduktan sonra performansı artırmak veya ek işlevlerini etkinleştirmek için aşağıdaki bilgileri kullanın.

| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **Uygulama hizmeti planı modu, boyutu ve etkin ölçeklendirme ayarlayın** |[Bir web uygulamasını Azure App Service'te ölçeklendirme][websitescale]. |
| **Kalıcı veritabanı bağlantılarını etkinleştirin** |Varsayılan olarak, WordPress sonra birden çok bağlantı kısıtlanan hale veritabanına bağlantınızı neden olabilecek kalıcı veritabanı bağlantılarını kullanmaz. Kalıcı bağlantılar etkinleştirmek için yükleme [kalıcı bağlantılar bağdaştırıcısı eklentisi](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Performansı** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">ARR tanımlama bilgisi devre dışı</a>, hangi performansı arttırabilir WordPress birden çok Web uygulamaları örnekleri üzerinde çalıştığında.</p></li><li><p>Önbelleğe almayı etkinleştir. Kullanabileceğiniz <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">Redis önbelleği</a> ile (Önizleme) <a href="https://wordpress.org/plugins/redis-object-cache/">nesne önbelleği WordPress eklentisini Redis</a>, veya diğer önbelleğe alma tekliflerinin dışında birini kullanabilirsiniz <a href="/gallery/store/">Azure depolama</a>.</p></li><li><p>[Wincache ile daha hızlı WordPress olun](https://wordpress.org/plugins/w3-total-cache/). Wincache, web uygulamaları için varsayılan olarak etkindir. WinCache ve dinamik önbellek birlikte kullanılırken, WinCache'nin dosya önbelleği devre dışı bırakmak, ancak kullanıcı ve oturum önbellek etkin bırakın. Dosya önbelleği, sistem düzeyinde .ini dosyası, devre dışı bırakmak için aşağıdaki değeri ayarlayın:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Bir web uygulamasını Azure App Service'te ölçeklendirme] [ websitescale] ve <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB yüksek kullanılabilirlik yönlendirme</a> veya <a href="http://www.mysql.com/products/cluster/">MySQL küme CGE</a>.</p></li></ul> |
| **BLOB depolama alanını kullanın** |<ol><li><p>[Bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md).</p></li><li><p>Bilgi nasıl [içerik dağıtım ağı kullanmak](../cdn/cdn-create-new-endpoint.md) coğrafi için-blob'larda depolanan verileri dağıtın.</p></li><li><p>Yükleme ve yapılandırma <a href="https://wordpress.org/plugins/windows-azure-storage/">WordPress eklentisini için Azure Storage</a>.</p><p>Ayrıntılı Kurulum ve eklenti için yapılandırma bilgileri için bkz: <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">Kullanıcı Kılavuzu</a>.</p> </li></ol> |
| **E-posta etkinleştir** |Etkinleştirme <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> Azure Store kullanarak. Yükleme <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid eklentisi</a> WordPress için. |
| **Bir özel etki alanı adı yapılandırma** |[Azure App Service'te özel etki alanı adı yapılandırma][customdomain]. |
| **Özel etki alanı adı için HTTPS'yi etkinleştir** |[Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir][httpscustomdomain]. |
| **Yük Dengeleme veya coğrafi-sitenizi Dağıt** |[Rota trafiği Azure Traffic Manager ile][trafficmanager]. Özel bir etki alanı kullanıyorsanız, bkz: [Azure App Service'te özel etki alanı adı yapılandırma] [ customdomain] Traffic Manager ile özel etki alanları kullanma hakkında bilgi için. |
| **Otomatik yedeklemeler etkinleştir** |[Azure App Service'te bir web uygulaması yedekleme][backup]. |
| **Tanılama günlük kaydını etkinleştir** |[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme][log]. |

## <a name="next-steps"></a>Sonraki adımlar
* [WordPress en iyi duruma getirme](http://codex.wordpress.org/WordPress_Optimization)
* [Çok siteli Azure App Service'te WordPress dönüştürün](web-sites-php-convert-wordpress-multisite.md)
* [ClearDB Yükseltme Sihirbazı'nı Azure](http://www.cleardb.com/store/azure/upgrade)
* [WordPress web uygulamanızı Azure App Service'te bir alt klasör barındırma](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Adım adım: Azure kullanarak bir WordPress sitesi oluşturma](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Varolan WordPress blogunuz Azure ile ilgili ana bilgisayar](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [WordPress, asıl sabit bağlantıları etkinleştirme](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Geçiş ve Azure App Service üzerinde WordPress blogunuz çalıştırma](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [WordPress ücretsiz Azure uygulama hizmeti çalıştırma](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [İki dakika veya daha az Azure üzerinde WordPress](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Azure - 1. bölüm bir WordPress blog taşıma: Azure üzerinde bir WordPress blog oluşturma](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Azure - 2. parça bir WordPress blog taşıma: içeriğinizi aktarma](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Azure - bölümü 3 bir WordPress blog taşıma: özel etki alanınızı ayarlama](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Azure - bölümü 4 bir WordPress blog taşıma: asıl sabit bağlantıları ve URL yeniden yazma kuralları](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Azure - bölümü 5 bir WordPress blog taşıma: kök alt klasöründen taşıma](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Azure hesabınızda bir WordPress web uygulaması kurma](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Azure üzerinde WordPress propping](http://www.johnpapa.net/wordpress-on-azure/)
* [Azure üzerinde WordPress için ipuçları](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service'i kullanmaya başlamak istiyorsanız, Git [App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı gerekmez ve hiçbir taahhüt yoktur.
>
>

## <a name="whats-changed"></a>Yapılan değişiklikler
Sitelerinden App Service'e değiştirme kılavuzu için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714).

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
