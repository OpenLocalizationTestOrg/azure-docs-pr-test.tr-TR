---
title: "Azure rol özellikleri"
description: "Azure rol ayarlarını yapılandırmak için Eclipse için Azure Araç Seti kullanmayı öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a>Azure rol özellikleri
Eclipse için Azure Araç Seti içinde çeşitli yapılandırma ayarlarını Azure rolünüz için ayarlanabilir.

## <a name="configuring-azure-role-properties"></a>Azure rol özellikleri yapılandırma
Azure rol özellikleri yapılandırma, çalışan rolü için özellik iletişim kutuları aracılığıyla gerçekleştirilir. Eclipse'nın Proje Gezgini bölmesinde rolün bağlam menüsünü açın ve seçin **Azure** alt menüsünde. (Eclipse Proje Gezgini rolünde görmüyorsanız, proje Gezgini'nde Azure projenizi genişletin.)

![][ic789599]

Arasında ayarlanabilir çeşitli özellikleri **özellikleri** iletişim kutuları, bu konudaki açıklanmıştır. Yeni bir Azure dağıtım projesi oluşturduğunuzda, birçok özelliği otomatik olarak doldurulur olduğunu unutmayın.

Aşağıdaki özellik sayfaları Azure rolleri için kullanılabilir.

* [Sanal makine özellikleri](#virtual_machine_properties)
* [Özellikleri önbelleğe alma](#caching_properties)
* [Sertifika Özellikleri](#certificates_properties)
* [Bileşenlerin özellikleri](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Uç noktalarının özellikleri](#endpoints_properties)
* [Ortam değişkenlerinin özellikleri](#environment_variables_properties)
* [Yük Dengeleme / oturum benzeşimi (a.k.a "Yapışkan oturumları") özellikleri](#session_affinity_properties)
* [Yerel depolama özellikleri](#local_storage_properties)
* [Sunucu Yapılandırma Özellikleri](#server_configuration_properties)
* [SSL boşaltma özellikleri](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Sanal makine özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **özellikleri**, ve sanal makine boyutunu değiştirme olanağına sahip ve aynı zamanda sayısını değiştirme örnekleri aşağıdaki görüntüde gösterildiği gibi.

![][ic719499]

> [!NOTE]
> Yalnızca Windows: örnek sayısı için bir değer 1'den büyük ayarlama ve uygulama sunucusu ayrıca yapılandırdığınızda Araç Seti öykünücüsü, bu ayardan bağımsız olarak çalıştırmak yalnızca 1 rol örneği izin verir. Aynı bilgisayarda çalıştırdığınızda, bağlantı noktası bağlama farklı bir sunucu örnekleri arasında (örneğin, tüm bağlantı noktası 8080 bağlamak çalışıyor) çakışmaları budur. İstenen örnek sayınız ayarı korunur, ancak yalnızca buluta dağıttığınızda yürürlüğe girer.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Özellikleri önbelleğe alma
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **önbelleğe alma**. Bu iletişim kutusu içinde adlandırılmış birlikte bulunan memcache uyumlu önbellekler, web uygulamalarınızı hızlandırmak sağlayarak etkinleştirebilirsiniz.

![][ic719483]

İçinde **önbelleğe alma** özellik sayfası, aşağıdakiler için genel ayarları belirtin:

* birlikte bulunan önbellek etkinleştirilip etkinleştirilmediği.
* Önbellek boyutu bellek yüzdesi.
* Uygulamanızı bir bulut hizmeti veya none çalıştığında önbellek durumu kaydetmeyi istemiyorsanız önbellek durumu kaydetmek için depolama hesabı adı. (Uygulamanızın işlem öykünücüsü çalıştırdığınızda, depolama hesabı adı kullanılmaz.) Depolama hesabı adı ayarlamak, **(otomatik)** (varsayılan değer olan), önbelleğe alma yapılandırmanızı seçin, bir otomatik olarak aynı depolama hesabını kullanacak **Azure Yayımla** iletişim.

> [!NOTE]
> **(Otomatik)** ayarı Yayımlama Sihirbazı yalnızca Eclipse Toolkit'in kullanarak dağıtımınızı yayımlarsanız istenen etkisi olacaktır. Bunun yerine bir dış mekanizması gibi kullanarak el ile .cspkg dosya yayımlarsanız [Azure Yönetim Portalı][Azure Management Portal], dağıtım düzgün çalışmaz.
> 
> 

Aşağıdaki iletişim kutusu için bir önbellek özellikleri gösterir.

![][ic719501]

* **Ad:** birlikte bulunan önbellek adı.
* **Bağlantı noktası numarası:** önbelleği için kullanılacak bağlantı noktası numarası.
* **Süre sonu ilkesi:** önbellek anahtarında sona erdiğinde belirtir şu değerlerden biri.
  * **Mutlak:** zaman tarafından belirtilen anahtar sona erme **Canlı dakika** ulaşıldı.
  * **NeverExpires:** anahtarı sona erme süresi yok.
  * **SlidingWindow:** onu tarafından belirtilen süre miktarı erişildikten değil anahtar süresi **Canlı dakika**; her seferinde erişilmeden, sona erme saati sıfırlanır.
* **Canlı dakika:** süre sonu ilkesine Live'a memcached anahtarı için dakika sayısı üst sınırı.
* **Farklı rol örneklerinde çoğaltılan yedeklemeler ile yüksek kullanılabilirlik:** etkinleştirilirse, yüksek kullanılabilirlik kullanılarak çoğaltılan yedeklemeler farklı rol örneklerinde yardımcı sağlayın. Bu özelliğin çalışması, dağıtımınız için en az iki rol örnekleri etkin olması gerektiğini unutmayın.

Yeni bir önbellek eklemek için tıklatın **Ekle** düğmesini **önbelleğe alma** özellik sayfası ve bir **adlandırılmış önbelleği Yapılandır** iletişim kutusu açılabilir. Yukarıda açıklanan özellikleri için değerleri girin.

Adlandırılmış önbellek değiştirmek için önbellek seçin ve tıklatın **Düzenle** düğmesini **önbelleğe alma** özellik sayfası. Bir iletişim kutusu, önbellek özellikleri değiştirmenize izin verecek açılır. Tuşuna **Tamam** önbellek değerlerini kaydetmek için.

Bir önbellek silmek için önbellek seçip tıklatın **kaldırmak** düğmesini **önbelleğe alma** özellik sayfası ve ardından **Evet** silme işlemini onaylamak için.

Önbelleğe almayı kullanma hakkında daha fazla bilgi için bkz: [Co-located önbelleğe alma kullan nasıl][How to Use Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Sertifika Özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **Sertifikalar**.

![][ic710964]

Bu iletişim kutusu içinde ekleyebilir veya Eclipse projenizin tarafından başvurulan sertifikaları kaldırın. Burada listelenen sertifikalar otomatik olarak tüm Java keystore'un içinde depolanmaz ve bu nedenle bir Java uygulaması içinde kullanım için otomatik olarak kullanılabilir değildir unutmayın. Bunlar sertifika dağıtımınızı çalışan sanal makineleri depolamak ve daha sonra kullanılan Windows başka bir Windows yazılım tarafından yüklenmiş böylece bunlar yalnızca Azure ile kaydedilir. Şu anda, sertifikaları kullanan araç setini yalnızca özellik bu şekilde başvurulan **sertifikaları** iletişim [SSL boşaltma][SSL Offloading], kendi bağımlılık nedeniyle Internet Information Services (IIS) ve uygulama isteği yönlendirme (ARR), bu şekilde kullanılabilir duruma getirilmek üzere doğru sertifikayı gerektiren.

Projeniz için Azure Yayımlama Sihirbazı'nı kullanarak dağıttığınızda, kullanıcıların parolalarını yanı sıra bu sertifikaları otomatik olarak Azure hizmetine karşıya yüklemek için ilgili kişisel bilgi değişimi (PFX) dosyalarını işaret edecek şekilde istenir , ancak yalnızca bunlar var. önceden yüklenmemiş olması gerekir.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Bileşenlerin özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **bileşenleri**. Bu iletişim kutusu içinde eklemek, değiştirmek veya rolünüze bileşenlerini kaldırmak, yanı sıra bunların işlenme sırasını değiştirme olanağına sahip.

![][ic719502]

Bileşenleri özellik Java uygulama projeleri, özel dosyaları ve dağıtımınızda gerekli yürütülebilir komut satırı deyimleri gibi Azure dağıtım projesi bağımlılıkları eklemenize olanak sağlar.

Her bileşen için şunları belirtebilirsiniz:

* Bunu yapılandırıldığında bileşen Azure dağıtım projesine içeri aktarırken gerçekleştirilecek adımı.
* Bu bileşen Azure bulutta dağıtırken gerçekleştirilecek adımı.

> [!NOTE]
> Bileşen dosyaları veya komut satırlarını belirtirken, bir Windows sanal makineye özel adımlar Windows tabanlı bir işletim sistemi için geçerli olmalıdır dağıtımınızı yayımlanacağını aklınızda bulundurun. 
> 
> 

Bileşenleri aşağıdaki özelliklere sahiptir:

* **İçeri Aktar:** proje yapılandırıldığında nasıl bileşen projeye içeri aktarılacak gösterir yöntemi. Bu aşağıdaki değerlerden biri olabilir:
  * **kopyalama:** bileşen tarafından belirtilen yerel yolu kopyalanır **gelen** rolün özellikte **approot** dizin.
  * **KULAK:** bir kurumsal uygulama projesi tarafından belirtilen yerel yolundaki içe aktarıldığı bir Java enterprise arşiv (kulak) bileşenidir **gelen** özelliği. (Bu otomatik olarak bu konumda proje yapısını göre araç takımı tarafından algılanan).
  * **JAR:** bileşen Java arşiv (JAR) ve bir Java projesi tarafından belirtilen yerel yolundaki içeri **gelen** özelliği. (Bu otomatik olarak bu konumda proje yapısını göre araç takımı tarafından algılanan).
  * **Hiçbiri:** bileşeni almak için hiçbir işlem yapılmadı. Bileşen zaten rolün içinde mevcut olduğu varsayılarak bu uygulanabilir olduğunda **approot** dizini veya bileşeni yalnızca bir yürütülebilir komut satırı deyimi, belirtildiği gibi olduğunda **olarak** özelliği zaman **dağıtma** yöntemi **exec**.
  * **WAR:** bileşen bir Java web uygulaması Arşivi (WAR) ve dinamik Web projesi tarafından belirtilen yerel yolundaki üzerinden içe aktarılan **gelen** özelliği. (Bu otomatik olarak bu konumda proje yapısını göre araç takımı tarafından algılanan).
  * **zip:** bileşen bir zip dosyası ve dizin veya dosya tarafından belirtilen sıkıştırma içeri **gelen** özelliği.
* **Kimden:** dağıtımınıza almak için öğeleri temsil eden dosyayı veya klasörü için yerel makinenizde kaynak yolu. Windows ortam değişkenleri, bu özellik kullanılabilir. Tüm alınabilir bileşenleri rolün içeri aktarılacak **approot** proje yapılandırıldığında dizin.
  
    Bir yükleme bileşeninden buluta (işlem öykünücüsü değil) dağıtırken dağıtma yeteneği gerektiğini unutmayın. Bir bileşeni ekleme hakkında ilgili bilgiler aşağıda bakın.    
* **AS:** altında bileşen içeri aktarılacak rolün dosya adı **approot** dizin ve sonuç olarak dağıtılan Azure bulutta. Bu özellik yerel makinede olduğu gibi aynı adı kullanmak için boş bırakın. (Yürütülebilir bileşenlerin, diğer bir deyişle, bu özelliği **dağıtma** yöntemi ayarlanmış **exec**, bu rastgele bir Windows komut satırı bildirimi olabilir.)
  
  > [!IMPORTANT]
  > Bu değer için boşluk karakterleri kullanırsanız, dağıtım yöntemine bağlı olarak farklı işlenecek. Dağıtma yöntemi ise **exec**, boşluk, dosya adının bir parçası olarak değil de komut satırı bağımsız değişkeni ayırıcı olarak yorumlanır. İçin diğer tüm yöntemler dağıtabilir, boşluk, dosya adının bir parçası olarak yorumlanır.
  > 
  > 
* **Dağıtın:** dağıtım başlatıldığında bileşenine uygulanmış eylemi gösterir yöntemi. Bu aşağıdaki değerlerden biri olabilir:
  
  * **kopyalama:** bileşen tarafından belirtilen hedef yolu kopyalanır **için** özelliği.
  * **Exec:** tarafından belirtilen yol bağlamında yürütülen yürütülebilir bir Windows komut satırı deyimi bileşenidir **için** dağıtımı başlatır zaman özelliği.
  * **Hiçbiri:** dağıtım başladığında, hiçbir eylem bileşenine uygulanır.
  * **zip:** tarafından belirtilen hedef yolu sıkıştırması açılmış bir bileşenidir **için** özelliği. Bu yöntem yalnızca olduğu **alma** özelliği **zip**.
* **Kime:** bileşen dağıtılacağı sanal makinede hedef yolu. Bu özellik Windows ortam değişkenlerini kullanılabilir ve dosya yollardır göreli **approot**.

Yeni bir bileşen eklemek için tıklatın **Ekle** düğmesini **bileşenleri** özellik sayfası ve bir **Azure rolü bileşeni** iletişim kutusu açılabilir. Yukarıda açıklanan özellikleri için değerleri girin. 

Yeni bir WAR bileşen eklemek için bir örnek gösterilmektedir.

![][ic719503]

Ne zaman bir indirme bileşeninden dağıtmak istiyorsanız (işlem öykünücüsü değil) buluta dağıtma emin **bulutta pakete dahil etme yerine olduğunda, dağıtım** denetlenir. Azure storage hesabınızdan karşıdan yüklemek isterseniz, depolama hesabından seçin **depolama hesabı** aşağı açılan liste (tıklayabilirsiniz **hesapları** listede nedir değiştirmek için bağlantı), hangi olur kısmen doldurmak **URL** alan ve URL'nin kalan bölümünde doldurun. Azure storage kullanmayı istemiyorsanız seçin **(hiçbiri)** gelen **depolama hesabı** aşağı açılan listesinde ve, bileşeni için URL'yi girin **URL** alan. Aşağıdaki yöntemlerden birini belirtin:

* **kopyalama:** yüklenecek bir bileşen tarafından belirtilen hedef yolu kopyalanır **dizin** yolu.
* **aynı:** için kullanılan aynı yöntemi **dağıtma indirme alanından** olarak **paketinden dağıtma**.
* **zip:** yüklenecek bir bileşen tarafından belirtilen hedef yolu sıkıştırması açılmış **dizin** yolu.

Bir bileşen değiştirmek için bileşeni seçin ve **Düzenle** düğmesini **bileşenleri** özellik sayfası. Bir iletişim kutusu bileşeni özellikleri değiştirmenize izin verecek açılır. Tuşuna **Tamam** bileşen değerlerini kaydetmek için.

Bir bileşeni silmek için bileşeni seçin ve **kaldırmak** düğmesini **bileşenleri** özellik sayfası ve ardından **Evet** silme işlemini onaylamak için.

Bileşenleri listelenen sırada işlenir. Kullanım **Yukarı Taşı** ve **Aşağı Taşı** sırasını düzenlemek için düğmeler.

> [!NOTE]
> Sunucu yapılandırması özellik bileşenler de kullanır. Bu bileşenler kaldırılır veya karşılık gelen sunucu yapılandırmasını kaldırmadan düzenlenemiyor. Bu tür bileşenleri için değişiklik çalışılırken istenir.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Uç noktalarının özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **uç noktaları**. Bu iletişim kutusu içinde aşağıdaki görüntüde gösterildiği gibi bir uç nokta oluşturma yanı sıra düzenleme veya bir uç nokta kaldırmak olanağına sahip.

![][ic719505]

Bir uç nokta eklemek için tıklatın **Ekle** düğmesini **uç noktaları** özellik sayfası ve bir **uç nokta Ekle** iletişim kutusu açılabilir.

![][ic710897]

Uç nokta için bir ad girin, türünü seçin (ya da **giriş**, **dahili**, veya **InstanceInput**) ve ortak ve özel bağlantı noktasını belirtin. Tuşuna **Tamam** yeni uç nokta değerlerini kaydetmek için.

Uç nokta türüne bağlı olarak, bağlantı noktası aralıkları gibi kullanabilirsiniz:

* Bir giriş örneğinin uç noktası için bağlantı noktası aralığını genel bağlantı noktası olabilir (örneğin **2000 2010**) ve özel bağlantı noktası sabit bir değer.
* Bir iç uç nokta için genel bağlantı noktası kullanılmaz ve özel bağlantı noktası aralığı olabilir veya sol boş veya belirtmek için bir yıldız işareti kümesine Azure tarafından otomatik olarak ayarlanır.
* Giriş uç noktaları için genel bağlantı noktası yalnızca sabit bir değer olabilir ve özel bağlantı noktası bir sabit değer ya da sol boş olabilir veya Azure tarafından otomatik olarak ayarlanır belirtmek için bir yıldız işareti ayarlayın.

Bir tek bağlantı noktası numarası yerine bir aralık kullanmak istiyorsanız, metin kutusunu End aralığı boş bırakın.

Otomatik, eğer ayarladığınız bağlantı noktalarını hangi bağlantı noktası gerçekten çalışma zamanı sırasında kullanılan karar vermeniz için uygulamanız belgelenen Azure hizmeti çalışma zamanı API'si kullanabilir [com.microsoft.windowsazure.serviceruntime paket özeti ][com.microsoft.windowsazure.serviceruntime package summary].

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

Bir uç nokta değiştirmek için uç nokta seçin ve tıklatın **Düzenle** düğmesini **uç noktaları** özellik sayfası. Bir iletişim kutusu, uç nokta adı, türü ve genel ve özel bağlantı noktaları değiştirmenize izin verecek açılır. Tuşuna **Tamam** değiştirilmiş uç nokta değerleri kaydetmek için.

Bir uç nokta silmek için uç nokta seçin ve tıklatın **kaldırmak** düğmesini **uç noktaları** özellik sayfası ve ardından **Evet** silme işlemini onaylamak için.

Bir rol üzerinde bir kullanıcı tarafından etkinleştirilmiş (örneğin, önbelleğe alma, oturum benzeşimi ya da SSL boşaltma) özelliklerinden bazıları düzgün bir şekilde yapılandırmak için Araç Seti Kullanıcı tanımlı uç noktaları ile birlikte listelenir özel uç noktaları otomatik olarak yapılandırabilirsiniz. Araç Seti Kullanıcı düzenlemesini engeller veya ilişkili özelliğin etkin olduğu sürece uç noktaları gibi otomatik olarak silineceği oluşturulabilir.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Ortam değişkenlerinin özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **ortam değişkenleri**. Bu iletişim kutusu içinde bir ortam değişkeni oluşturma yanı sıra değiştirmek veya bir ortam değişkeni kaldırmak için aşağıdaki resimde gösterildiği gibi sahipsiniz.

![][ic719506]

Rol başladığında, ortam değişkenleri başlangıç komut dosyanıza kullanılabilir.

> [!NOTE]
> Ortam değişkenleri belirtirken, bir Windows sanal makine için ortam değişkenlerini Windows tabanlı bir işletim sistemi için geçerli olmalıdır dağıtımınızı yayımlanacağını aklınızda bulundurun.
> 
> 

Bir rolü başladığında kullanılabilir olan bir ortam değişkeni örnek, yeni bir ortam değişkeni oluşturun **Ekle** düğmesi. Adlı bir ortam değişkeni aşağıdaki gösterir **MyRoleVersion** oluşturulur ve değer atanmışsa **1.0**.

![][ic659268]

Jsp kodunuzu içinde değerini kullanarak görüntüleyebilir `System.getenv` yöntemi:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Uygulamanızı çalıştığında bu çıktıda sonuçlanır:

![][ic552233]

Bir ortam değişkeni değiştirmek için ortam değişkeni seçin ve **Düzenle** düğmesini **ortam değişkenleri** özellik sayfası. Ortam değişkeni özellikleri değiştirmenize izin verecek bir iletişim kutusu açılacak. Tuşuna **Tamam** ortam değişkeni değerlerini kaydetmek için.

Bir ortam değişkeni silmek için ortam değişkeni seçip tıklatın **kaldırmak** düğmesini **ortam değişkenleri** özellik sayfası ve ardından **Evet** için silme işlemini onaylayın.

Özelliklerinden bazıları (örneğin, sunucu yapılandırması, uzaktan hata ayıklama veya yerel depolama) bir rol üzerinde bir kullanıcı tarafından etkinleştirilmiş düzgün bir şekilde yapılandırmak için Araç Seti Kullanıcı tanımlı birlikte listelenen özel ortam değişkenleri otomatik olarak yapılandırabilirsiniz ortam değişkenleri. Araç Seti Kullanıcı düzenlemesini engeller veya ilişkili özelliğin etkin olduğu sürece gibi otomatik olarak silineceği ortam değişkenleri oluşturulabilir.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Yük Dengeleme / oturum benzeşimi (a.k.a "Yapışkan oturumları") özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **Yük Dengeleme**. Bu iletişim kutusu içinde aşağıdaki görüntüde gösterildiği gibi etkinleştirmek veya devre dışı oturum benzeşimi olanağına sahip.

![][ic719492]

İlgili bilgi için bkz: [oturum benzeşimi][Session Affinity]. Ayrıca, bu özelliğin davranışı SSL boşaltma, bağlamda konusunda açıklandığı gibi unutmayın [SSL boşaltma][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Yerel depolama özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **yerel depolama**. Bu iletişim kutusu içinde oluşturma, değiştirme veya yerel geçici depolama uygulamanızı çalıştıran sanal makine için kaldırma olanağına sahip. Belirli değerler için yerel depolama boyutu yanı sıra rolü aşağıdaki resimde gösterildiği gibi geri dönüştürüldüğünde içeriği olup korunur ayarlanabilir.

![][ic719508]

Ayrıca isteğe bağlı olarak, yerel depolama alanına karşılık gelen bir ortam değişkeni belirtebilirsiniz.

Varsayılan olarak, Azure'a dağıttığınız her şeyi yerleştirilen (sıkıştırması açılmış ve) **approot** rol örneğinin klasör. Çoğu basit dağıtım var. sonra bile olan uygun olsa da, alan için ayrılan **approot** dizindir sınırlı ve iyi tanımlanmış (1 GB bir makul udur daha azını). Bu nedenle, Azure emin olmak için ayırır yeterli disk alanı uygun, değildir daha büyük dağıtımlar için **approot** klasör, yerel depolama bir kullanarak kaynak ayarlamalıdır **yerel depolama** iletişim. Bunu yapmak için kolay bir yol için bkz: [dağıtma büyük dağıtımlar][Deploying Large Deployments].

Depolama kaynağı başlangıç komut dosyalarından kolayca başvurusu yapabilir (örneğin, **startup.cmd**) gösterildiği gibi otomatik olarak Eclipse araç takımı tarafından kaynakla ilişkili ortam değişkeni kullanarak  **Yerel depolama** iletişim. Bu ortam değişkenini, başlatma komut yürütüldüğünde yapılandırdığınız yerel kaynak tam yolunu içerir. 

Yerel depolama kaynağı değiştirmek için yerel depolama kaynağı seçin ve **Düzenle** düğmesini **yerel depolama** özellik sayfası. Bir iletişim kutusu, yerel depolama kaynak özellikleri değiştirmenize izin verecek açılır. Tuşuna **Tamam** yerel depolama kaynak değerlerini kaydetmek için.

Yerel depolama kaynağı silmek için yerel depolama kaynağı seçin ve **kaldırmak** düğmesini **yerel depolama** özellik sayfası ve ardından **Evet** onaylamak için silme.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Sunucu Yapılandırma Özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **sunucu yapılandırması**. Bu iletişim kutusu içinde eklemek, kaldırmak ve dağıtımınız tarafından kullanılan JDK ve Java uygulama sunucusunu değiştirme olanağına sahip yanı sıra ekleyip Dağıtımınızda kullanılan uygulamaları (WAR, JAR veya kulak dosyaları gibi).

### <a name="jdk-configuration"></a>JDK yapılandırma
Bu iletişim kutusu, dağıtımınız için kullanılacak JDK paketi belirtmenize olanak sağlar. Windows üzerinde Eclipse kullanıyorsanız, Azure öykünücüsünde çalıştırırken yerel olarak kullanılacak JDK paket belirtebilirsiniz ve bu yerel yükleme Azure'a dağıtmak için seçeneğiniz vardır. Windows olmayan işletim sistemlerinde öykünücüsü JDK ayarı uygulanabilir değildir ve Windows ile uyumlu olmadığından yerel olarak yüklü JDK dağıtamazsınız. Ancak, kullanmakta olduğunuz işletim sistemi'ne ne olursa olsun, her zaman Azure'a dağıtma veya kendi Windows uyumlu JDK paketin bir diğer yükleme konumundan noktası için 3 taraf JDK paketler arasında seçebilirsiniz.

Bir JDK Windows'da nasıl belirleyebileceğiniz bir örnek verilmiştir:

![][ic780647]

Windows üzerinde Eclipse kullanıyorsanız, işlem öykünücüsü ile kullanmak için bir JDK belirtebilirsiniz; Bunu yapmak için olun **yerel olarak test etmek için bu dosya yolundan JDK kullanmak** iade **öykünücüsü dağıtım** bölümü. Ardından, JDK yerel yolu belirtin; kullanmak istediğiniz bir otomatik olarak seçili değilse farklı JDK göz atabilirsiniz. Azure bulut hizmetinize, JDK dağıtma seçeneği de; Bunu yapmak için seçin **my yerel JDK (otomatik karşıya yükleme bulut depolama için) dağıtmak** seçeneğini **bulut dağıtımı** bölümü.

Not: Windows olmayan işletim sistemlerinde, **öykünücüsü dağıtım** ayarları ve **my yerel JDK dağıtımı** seçeneği kullanılamaz. Aşağıdaki örnek, bir Mac veya diğer desteklenen Windows olmayan işletim sisteminin bir JDK belirtme gösterilmektedir:

![][ic789643]

Aşağıdaki iki sahip olduğunuz üzerinde olan işletim sisteminden bağımsız olarak **bulut dağıtımı** kaynak ve JDK paketinizi türü için seçenekleri:

* **Azure üzerinde kullanılabilir 3 taraf JDK paketi dağıtma** 
* **Özel bir Merkezi'nden dağıtma** 

Kullanıyorsanız **3 taraf JDK kullanılabilir bir paketi Azure'dan dağıtmak** seçeneği:

1. Adlı onay **3 taraf JDK kullanılabilir bir paketi Azure'dan dağıtmak**.
2. Aşağı açılan listeden, Azure üzerinde kullanılabilir 3 taraf JDK paketi seçin.
3. **JDK** sekmesi Windows aşağıdakine benzer görünür: ![][ic780648] ve Mac OS aşağıdakine benzer görünecektir veya diğer Windows olmayan işletim sistemleri desteklenir:![][ic789643]
4. Değişikliklerinizi kaydetmek için **Tamam**’a tıklayın.
5. 3 taraf JDK paket sağlayıcısından lisans sözleşmesini kabul etmek isteyip istemediğiniz sorulduğunda, lisans koşullarını gözden geçirin. Koşulları kabul varsayılarak tıklatın **Evet** kapatmak için **lisans sözleşmesini kabul** iletişim.
    Hangi öğeleri için temel mantığını görünür için aşağı açılan listesinde Not **3 taraf JDK kullanılabilir bir paketi Azure'dan dağıtmak** seçeneği özelleştirilebilir. İçinde öğelerini özelleştirmek için **JDK** iletişim kutusunda, tıklatın **Özelleştir** bağlantı. Bu kapatacak **JDK** özellik sayfası ve açık **componentsets.xml** sonra gerektiği gibi değiştirebilirsiniz Eclipse dosyasında. Belgelerine **componentsets.xml** dahil **componentsets.xml** kendisini dosya.

Kullanıyorsanız **özel indirme alanından bir JDK dağıtımı** seçeneği:

1. Dizin düğümü ZIP yapısı ve içeriğini değil alt olduğundan emin olmanın ZIP JDK yükleme dizininizin oluşturun. Daha sonra ihtiyacınız ve bu JDK yükleme için Windows sanal makine dağıtılacak göz önünde bulundurmanız dizinin adını not edin.
2. ZIP Azure depolama hesabınızda blob olarak yükleyin. Azure depolama alanına karşıya yükleme BLOB'lar için bu dışarıdan kullanılabilir olan bir aracı kullanarak yapabilirsiniz. Özel bir blob kullanılması önerilir. ZIP içeriği blob URL'sini not edin.
3. Adlı onay **özel indirme alanından bir JDK dağıtımı**.
    Azure storage hesabınızdan karşıdan yüklemek isterseniz, depolama hesabından seçin **depolama hesabı** aşağı açılan liste (tıklayabilirsiniz **hesapları** listede nedir değiştirmek için bağlantı), hangi olur kısmen doldurmak **URL** alan ve URL'nin kalan bölümünde doldurun. Azure storage kullanmayı istemiyorsanız seçin **(hiçbiri)** gelen **depolama hesabı** aşağı açılan listesinde ve, JDK indirmesi için URL'yi girin **URL** alan. Azure storage kullanıyorsanız, URL'deki blob adları küçük harf olmalıdır.
4. Emin **JAVA_HOME** textbox doğru dizin adına başvuruyor. Varsayılan olarak, yerel kullanımınız için seçtiğiniz değer aynı JDK dizin adı başvurur. Ancak ZIP diziniyle (örneğin, farklı bir sürüm kullanma nedeniyle), farklı bir ad varsa güncelleştirmesi dizin adı **JAVA_HOME** textbox buna uygun olarak, bu yana ayarı bulutta kullanılabilir (değil öykünücü işlem).
5. Değişikliklerinizi kaydetmek için **Tamam**’a tıklayın.

Bu kadar. Şimdi, bulut için yapılandırdığınızda, paket boyutu çok daha küçük olur, oluşturma işlemi genellikle daha az zaman ve dağıtım kendisini buluta yayımladığınızda, aynı zamanda daha az zaman fark edeceksiniz. Unutmayın **my yerel JDK (otomatik karşıya yükleme bulut depolama için) dağıtmak** veya **özel indirme alanından bir JDK dağıtımı** seçeneklerdir yürürlükte yalnızca bulutta uygulamanızı dağıtıldığında. Bunlar, işlem öykünücüsü deneyiminizi üzerinde hiçbir etkisi yoktur; işlem öykünücüsü dağıttığınızda bileşenlerinin yerel sürümünü hala kullanılır. 

### <a name="server-configuration"></a>Sunucu Yapılandırması
Bir uygulama sunucusu nasıl belirteceğinizi bir örnek verilmiştir.

![][ic796926]

Doğrulayın **bu tür bir sunucu dağıtımı** onay kutusu seçilidir ve ardından kullanmak istediğiniz uygulama sunucusu seçin.

Bulut dağıtım için kullanılacak bir sunucu belirtmek için aşağıdaki seçeneklerden birini yararlanabilirsiniz:

1. **Bir 3. taraf sunucusuna Azure üzerinde kullanılabilir dağıtmak** -bu burada dağıtım verimliliği ve Basitlik, öncelik ve sunucu özel bir yapılandırma gerektirmez geliştirme ve test senaryolarında özellikle geçerlidir. Veya bu sunuculardan birinde başlangıç noktası olarak kullanmak istediğiniz ancak dahil uygun sunucu özelleştirme dağıtımınızın başlangıç mantığı adımları.
2. **Özel bir Merkezi'nden dağıtmak** -bulutta kullanmak istediğiniz özel olarak hazırlanmış ve yapılandırılmış bir sunucunuz varsa bu üretim senaryolarında özellikle geçerlidir.
3. **Yerel sunucu yükleme dağıtmak** -Bu, yerel sunucu yüklemesi zaten kullanımınız için özel olarak yapılandırılmış ise özellikle geçerlidir. Bu seçeneği seçerseniz, yerel sunucunuzun yolunda de belirtmeniz gerekir **yerel sunucu yolu** aşağıdaki metin kutusu.

Kullanıyorsanız **bir 3. taraf sunucusuna Azure üzerinde kullanılabilir dağıtmak** seçeneği:

1. Adlı onay **bir 3. taraf sunucusuna Azure üzerinde kullanılabilir dağıtmak**.
2. Açılan menüden bulutta dağıtımınız ile kullanmak için istenen sunucu yazılımı seçin. Not, eski sunucu türünü zaten belirtilmişse, bu sunucu türü ile aynı ailesindeki olan bir bulut sunucuyu seçmek için sınırlı olacaktır. Ancak sunucu türü istemediyseniz, Azure üzerinde şu anda kullanılabilir sunuculardan herhangi biri arasından seçim yapabilirsiniz ve sunucu türünü otomatik olarak sizin için seçilir.
3. Değişikliklerinizi kaydetmek için **Tamam**’a tıklayın.

Kullanıyorsanız **dağıtma özel indirme alanından** seçeneği:

1. Yukarıdaki adımları göre sunucu türü zaten seçtiğinizden emin olun. Seçilen sunucu türü olarak aynı aile olmalıdır olarak bu, özel yükleme sunucudan dağıtma eklentisi bildirir.
2. Adlı onay **dağıtma özel indirme alanından**.
    Azure storage hesabınızdan karşıdan yüklemek isterseniz, depolama hesabından seçin **depolama hesabı** aşağı açılan liste (tıklayabilirsiniz **hesapları** listede nedir değiştirmek için bağlantı), hangi olur kısmen doldurmak **URL** alan ve sunucunuzun URL'sini geri kalan bölümü doldurun (Azure depolama, URL'deki blob adları kullanarak küçük harfli olması gerektiğini olduğunda) ZIP indirin. Azure storage kullanmayı istemiyorsanız seçin **(hiçbiri)** gelen **depolama hesabı** aşağı açılan listesinde ve sunucunuz için URL'yi girin içinde ZIP karşıdan **URL** alan. ZIP, uygulama sunucusu yükleme dizinini temsil eden bir alt klasör içerir. Örneğin, bir zip Apache Tomcat 7.0.35 kullanıyorsanız, içinde zip olacaktır yükleme dizini gibi temsil eden alt klasör **apache tomcat 7.0.35**. 
3. Giriş dizini ortam değişkeninin değerini belirtin. Varsa, yerel uygulama sunucusu için kullanılan değeri varsayılan olur, ancak bulut uygulama sunucunuzu yerel uygulama sunucunuzdan farklıysa, farklı bir değer belirtebilirsiniz. Ancak, bulut uygulama sunucunuzu sunucusu olarak aynı ailesinin olduğundan emin olmanız gerekir daha önce seçilen türü.
    Bulut uygulama sunucusu zip gelecekte güncelleştirirseniz, giriş dizini ayarını el ile değiştirebilirsiniz veya yeniden (yerel uygulama sunucunuza çok değiştirdiyseniz), yerel ayar eşleştirmek için.
4. Değişikliklerinizi kaydetmek için **Tamam**’a tıklayın.

Kendisi için öğeler görünür temel mantığını **Server** sekmesinde **sunucu yapılandırması** özellik sayfası özelleştirilebilir. Varsayılan değerler gereksinimlerinizi genişlettiğinizde ya da diğer sunucuları eklemek istiyorsanız gerekebilecek Gelişmiş bir özelliktir. İçinde mantığını özelleştirmek için **Server** iletişim kutusunda, tıklatın **Özelleştir** bağlantı. Bu kapatacak **sunucu yapılandırması** özellik sayfası ve açık **componentsets.xml** sonra sunucu yapılandırma şablonu genişletmek için gerektiği şekilde değiştirebilirsiniz Eclipse dosyasında. Belgelerine **componentsets.xml** dahil **componentsets.xml** kendisini dosya.

Kullanıyorsanız **yerel (otomatik karşıya yükleme bulut depolama için) dağıtmak** seçeneği:

1. Adlı onay **yerel (otomatik karşıya yükleme bulut depolama için) dağıtmak**.
2. Kullanarak **depolama hesabı** aşağı açılan listesinden, **(otomatik)**. Belirtirseniz **(otomatik)** Eclipse araç seti, dağıtımınız için seçtiğiniz bir sunucunuz için aynı depolama hesabındaki burada kullanacağı **Azure Yayımla** iletişim.
3. Değişikliklerinizi kaydetmek için **Tamam**’a tıklayın.

Bilgisayarınızdaki sunucu yükleme yolunu seçin **yerel sunucu yolu** aşağıdaki koşullardan herhangi biri doğruysa, metin kutusunda:

* (Yalnızca Windows için geçerlidir) öykünücüsünde dağıtımınızı test etmek istediğiniz.
* Yerel olarak yüklü sunucunuzu buluta dağıtmak istediğiniz.
* İstediğiniz özel sunucu indirme bulutta, kendi durumunun kullanmak için ayrıca olun **yerel (otomatik karşıya yükleme bulut depolama için) dağıtmak** yukarıda seçili seçeneği.

Yukarıdaki seçeneklerden hiçbiri durumunuza uygularsanız, yerel sunucu ayarını isteğe bağlıdır.

### <a name="applications-configuration"></a>Uygulamaları yapılandırma
Bir uygulamanın nasıl belirleyebileceğiniz bir örnek verilmiştir.

![][ic719512]

Tıklatın **Ekle** başka bir uygulama eklemek için veya **kaldırmak** bir uygulamayı kaldırmak için. Verimlilik amacıyla bir indirme buluta, kullanım dağıtırken Uygulama kaynağı için kullanmak istiyorsanız, [bileşenlerin özellikleri](#components_properties) depolama hesabı, bir URL belirtmek için vb.. 

Nisan 2014 sürümünden itibaren uygulamalarınızı otomatik olarak aynı depolama hesabındaki yüklenir (altında **eclipsedeploy** kapsayıcısı), dağıtım için seçtiğiniz bir. Dağıtımınızın başlangıç mantığı önce bu uygulamaları bu depolama hesabından indirmeleri bir adım içerir. Bu, uygulamalarınız, dağıtımınızdaki yeniden oluşturun ve doğrudan (örneğin Azure Portalı'nı kullanarak), bu depolama hesabı uygulamasına daha yeni sürümlerini el ile karşıya yükleyerek tüm paketi yeniden dağıtmak zorunda kalmadan yükseltmeniz anlamına gelir. WAR dosyaları değiştirme başlangıçta var. araç takımı tarafından karşıya yüklendi. Ardından, yeniden veya komut satırı yardımcı programları üzerinden Azure yönetim portalını kullanarak bu rol örnekleri geri dönüştürme yalnızca başlatın. (Rol doğrudan Eclipse Araç Seti içinde geri dönüştürme tetikleme şu anda desteklenmiyor.)

### <a name="notes-about-server-configuration"></a>Sunucu yapılandırması ile ilgili notlar
Üzerinden yapılan değişiklikler **sunucu yapılandırması** özellik sayfası yansıtılır `<component>` package.xml dosyasının öğeleri.

Kullandığınızda **otomatik olarak karşıya yükleme...**  veya **indirme alanından Dağıt...**  JDK veya uygulama sunucusu ve sizin için Seçenekler (işlem öykünücüsü değil) Bulutu oluşturma ve ağa bağlı, Ant Oluşturucu doğrular gibi konsol çıktısı aşağıdaki gibi iletileri yapı karşılaşabilirsiniz indirme ait kullanılabilirlik:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Seçtiyseniz **indirme alanından Dağıt...**  seçeneği, aşağıdaki uyarıyı gösterilen, ancak derleme devam eder:

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Bu uyarı, indirme ait kullanılabilirlik doğrulanmış kurmadı yalnızca göstergesidir. Bir dağıtım bulutta herhangi bir nedenden dolayı başarısız olursa, bu nedenle, bu uyarı aldığınız denetleyin.

(Örneğin, gereksiz yere yavaşlatır yapı düşünüyorsanız) indirme doğrulamayı devre dışı bırakmak istiyorsanız ayarlamak `verifydownloads` özniteliğini `false` içinde `<windowsazurepackage>` package.xml öğesidir: 

`<windowsazurepackage verifydownloads="false" ...>` 

Seçtiyseniz **otomatik olarak karşıya yükleme...**  seçenek görürsünüz: sonra konsol penceresinde yapı her 5 karşıya yükleme gerekli olduğunda saniyede karşıya yükleme ilerlemesini raporlama iletileri.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL boşaltma özellikleri
Eclipse'nın Proje Gezgini bölmesinde, rol için bağlam menüsünde Aç'ı tıklatın **Azure**ve ardından **SSL boşaltma**. 

![][ic719481]

Bu iletişim kutusu içinde SSL boşaltma, kolayca SSL Java uygulama sunucunuzu yapılandırmak gerek kalmadan, azure'da Java dağıtımınızdaki Köprü Metni Aktarım Protokolü güvenli (HTTPS) desteğini etkinleştirmek sağlayarak etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [SSL boşaltma] [ SSL Offloading] ve [kullanım SSL boşaltma nasıl][How to Use SSL Offloading].

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Azure proje özellikleri][Azure Project Properties]

[Azure depolama hesabı listesi][Azure Storage Account List]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
