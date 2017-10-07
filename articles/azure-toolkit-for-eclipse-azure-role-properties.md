---
title: "aaaAzure rolü özellikleri"
description: "Nasıl toouse hello Azure araç setini Eclipse tooconfigure Azure rol ayarlarını öğrenin."
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
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Azure rol özellikleri
Azure rolünüz için çeşitli yapılandırma ayarlarını hello Eclipse için Azure Araç Seti içinde ayarlanabilir.

## <a name="configuring-azure-role-properties"></a>Azure rol özellikleri yapılandırma
Azure rol özellikleri yapılandırma hello özellik iletişim kutuları, çalışan rolü için aracılığıyla gerçekleştirilir. Eclipse'nın Proje Gezgini bölmesinde ve select hello hello rol için açık hello bağlam menüsünde **Azure** alt menüsünde. (Merhaba Eclipse Proje Gezgini hello rolünde görmüyorsanız, proje Gezgini'nde Azure projenizi genişletin.)

![][ic789599]

hello ayarlanabilir çeşitli özellikleri hello **özellikleri** iletişim kutuları, bu konudaki açıklanmıştır. Yeni bir Azure dağıtım projesi oluşturduğunuzda, birçok özelliği otomatik olarak doldurulur olduğunu unutmayın.

özellik sayfaları aşağıdaki hello Azure rolleri için kullanılabilir.

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
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **özellikleri**, ve hello özelliği toochange hello sanal makine boyutuna sahip ve aynı zamanda değiştirmeniz Hello hello görüntü aşağıdaki gösterildiği gibi örnek sayısı.

![][ic719499]

> [!NOTE]
> Yalnızca Windows: hello örneklerinin sayısını tooa değeri 1'den büyük ayarlayın ve uygulama sunucusu ayrıca yapılandırdığınızda hello Araç Seti yalnızca 1 rol örneği toorun bu ayardan bağımsız olarak hello öykünücüsü de izin verir. Tooavoid bağlantı noktası bağlama çakışmaları hello farklı sunucu örnekleri (örneğin, tüm çalışırken toobind tooport 8080) arasında budur üzerinde hello çalıştırdıklarında aynı bilgisayar. İstenen örnek sayınız ayarı korunur, ancak yalnızca toohello bulut dağıttığınızda yürürlüğe girer.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Özellikleri önbelleğe alma
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **önbelleğe alma**. Bu iletişim kutusu içinde adlandırılmış birlikte bulunan memcache uyumlu önbellekler, web uygulamalarınızı toohelp hızı izin vererek etkinleştirebilirsiniz.

![][ic719483]

Merhaba içinde **önbelleğe alma** özellik sayfasında, aşağıdaki hello için genel ayarları belirtebilirsiniz:

* birlikte bulunan önbellek etkinleştirilip etkinleştirilmediği.
* Merhaba önbellek boyutu bellek yüzdesi.
* Uygulamanızı bir bulut hizmeti veya none çalıştığında toosave hello önbellek durumu istemiyorsanız hello önbellek durumu kaydetmek için hello depolama hesabı adı. (Merhaba işlem öykünücüsü uygulamanızı çalıştırdığınızda hello depolama hesabı adı kullanılmaz.) Merhaba depolama hesabı adı çok ayarlarsanız**(otomatik)** (Merhaba varsayılan olduğu), önbelleğe alma yapılandırmanızı otomatik olarak kullanacak bir hello Seçtiğiniz hello gibi aynı depolama hesabındaki hello **tooAzureYayımlama**iletişim.

> [!NOTE]
> Merhaba **(otomatik)** ayarı Yayımlama Sihirbazı yalnızca hello Eclipse Toolkit'in kullanarak dağıtımınızı yayımlarsanız istenen hello etkili olacaktır. Bunun yerine el ile hello gibi bir dış mekanizmayı kullanarak hello .cspkg dosya yayımlarsanız [Azure Yönetim Portalı][Azure Management Portal], hello dağıtım düzgün çalışmaz.
> 
> 

iletişim kutusu aşağıdaki hello önbelleği için hello özellikleri gösterir.

![][ic719501]

* **Ad:** birlikte bulunan önbellek hello hello adı.
* **Bağlantı noktası numarası:** hello önbelleği için bağlantı noktası numarası toouse hello.
* **Süre sonu ilkesi:** hello önbellek anahtarında sona erdiğinde belirtir değerleri aşağıdaki hello biri.
  * **Mutlak:** hello anahtar süresi başlangıç zamanı olarak belirtildiğinde **dakika toolive** ulaşıldı.
  * **NeverExpires:** hello anahtar sona erme süresi yok.
  * **SlidingWindow:** hello anahtar süresi, tarafından belirtilen süre için hello erişildikten değil, **dakika toolive**; her seferinde tarafından erişildiğini, hello sona erme saati sıfırlanır.
* **Dakika toolive:** toolive, memcached anahtarı için dakika sayısı üst sınırı toohello süre sonu ilkesine tabidir.
* **Farklı rol örneklerinde çoğaltılan yedeklemeler ile yüksek kullanılabilirlik:** etkinleştirilirse, yüksek kullanılabilirlik kullanılarak çoğaltılan yedeklemeler farklı rol örneklerinde yardımcı sağlayın. Bu özellik toowork için dağıtımınız için en az iki rol örnekleri etkin olması gerektiğini unutmayın.

tooadd yeni bir önbellek tıklatın hello **Ekle** hello düğmesini **önbelleğe alma** özellik sayfası ve bir **adlandırılmış önbelleği Yapılandır** iletişim kutusu açılabilir. Yukarıda açıklanan hello özellikleri için değerleri girin.

toomodify adlandırılmış önbellek hello önbellek tıklatıp hello **Düzenle** hello düğmesini **önbelleğe alma** özellik sayfası. İzin verme, toomodify hello önbellek Özellikleri iletişim kutusu açılır. Tuşuna **Tamam** toosave hello önbellek değerleri.

toodelete bir önbellek hello önbellek tıklatıp hello **kaldırmak** hello düğmesini **önbelleğe alma** özellik sayfası ve ardından **Evet** tooconfirm hello silme.

Hakkında daha fazla bilgi için önbelleğe alma, toouse bkz [nasıl tooUse birlikte bulunan önbellek][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Sertifika Özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **Sertifikalar**.

![][ic710964]

Bu iletişim kutusu içinde ekleyebilir veya Eclipse projenizin tarafından başvurulan sertifikaları kaldırın. Burada listelenen hello sertifikaları otomatik olarak tüm Java keystore'un içinde depolanmaz ve bu nedenle bir Java uygulaması içinde kullanım için otomatik olarak kullanılabilir değildir unutmayın. Bunlar sertifika dağıtımınızı çalışan hello sanal makineler üzerinde depolamak ve daha sonra kullanılan Windows hello başka bir Windows yazılım tarafından yüklenmiş böylece bunlar yalnızca Azure ile kaydedilir. Bu şekilde hello özelliği hello sertifikaları kullanır hello araç seti, başvurulan yalnızca şu anda hello **sertifikaları** iletişim [SSL boşaltma][SSL Offloading], son tooits bağımlılık gerektiren Internet Information Services (IIS) ve uygulama isteği yönlendirme (ARR), bu şekilde kullanıma uygun sertifika toobe hello.

Merhaba Yayımlama Sihirbazı'nı kullanarak, proje tooAzure dağıttığınızda, istendiğinde toopoint hello kişisel bilgi değişimi (PFX) birlikte kullanıcıların parolalarını toothese sertifikaları karşılık gelen dosyaları sırayla tooautomatically karşıya bunları toohello adresindeki olacaktır Ancak bunlar var. daha önce yüklenmiş değil, yalnızca Azure hizmeti.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Bileşenlerin özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **bileşenleri**. Bu iletişim kutusu içinde hello özelliği tooadd sahip, değiştirebilir veya rolünüze hello bileşenlerini kaldırmak yanı işlenen hello sırasını değiştirme.

![][ic719502]

Merhaba bileşenleri özellik tooadd bağımlılıkları tooyour Azure dağıtım projesi, Java uygulama projeleri, özel dosyaları ve dağıtımınızda gerekli yürütülebilir komut satırı deyimleri gibi sağlar.

Her bileşen için şunları belirtebilirsiniz:

* Merhaba adım toobe onu yapılandırıldığında hello bileşen Azure dağıtım projesine içeri aktarırken gerçekleştirilecek.
* Merhaba adım toobe hello Azure bulut bu bileşende dağıtırken gerçekleştirilecek.

> [!NOTE]
> Bileşen dosyaları veya komut satırlarını belirtirken, özel adımlar Windows tabanlı bir işletim sistemi için geçerli olmalıdır dağıtımınızı yayımlanan tooa Windows sanal makine olacağını göz önünde bulundurun. 
> 
> 

Bileşenleri hello aşağıdaki özelliklere sahiptir:

* **İçeri Aktar:** hello proje yapılandırıldığında nasıl hello bileşen hello projesine içeri aktarılacak gösterir yöntemi. Bu değerleri aşağıdaki hello biri olabilir:
  * **kopyalama:** hello bileşen hello yerel yolundan hello tarafından belirtilen kopyalanır **gelen** hello rolün özellikte **approot** dizin.
  * **KULAK:** hello bileşenidir hello yerel yolundaki hello tarafından belirtilen bir kuruluş uygulaması projesini içe aktarıldığı bir Java enterprise arşiv (kulak) **gelen** özelliği. (Bu otomatik olarak bu konumda hello proje hello yapısını göre hello araç tarafından algılanan).
  * **JAR:** hello bileşen Java arşiv (JAR) ve bir Java projesi hello tarafından belirtilen hello yerel yolundaki içeri **gelen** özelliği. (Bu otomatik olarak bu konumda hello proje hello yapısını göre hello araç tarafından algılanan).
  * **Hiçbiri:** tooimport hello bileşen hiçbir işlem yapılmadı. Hello bileşen varsayılır Bu uygulanabilir olduğunda tooalready hello rolün içinde mevcut **approot** dizin veya hello bileşeni yalnızca bir yürütülebilir komut satırı deyimi, belirtilen hello olarak olduğunda **olarak**özelliği hello zaman **dağıtma** yöntemi **exec**.
  * **WAR:** hello bileşen bir Java web uygulaması Arşivi (WAR) ve dinamik Web projesi tarafından hello belirtilen hello yerel yolundaki üzerinden içe aktarılan **gelen** özelliği. (Bu otomatik olarak bu konumda hello proje hello yapısını göre hello araç tarafından algılanan).
  * **zip:** hello bileşen bir zip dosyası ve hello tarafından belirtilen sıkıştırma hello dizin veya dosya olarak içeri **gelen** özelliği.
* **Kimden:** yerel makine toohello klasörü veya hello öğeleri tooimport tooyour dağıtımını dosya kaynak yolu. Windows ortam değişkenleri, bu özellik kullanılabilir. Tüm alınabilir bileşenleri hello rolün içeri aktarılacak **approot** hello proje yapılandırıldığında dizin.
  
    Toohello bulut (Merhaba işlem öykünücüsü değil) dağıtırken bir indirme bileşeninden hello özelliği toodeploy sahip gerektiğini unutmayın. Bir bileşeni ekleme hakkında ilgili bilgiler aşağıda bakın.    
* **AS:** altında hangi hello bileşen hello rolün aktarılacak dosya adı **approot** dizin ve sonuç olarak dağıtılan hello Azure bulut içinde. Bu özellik boş tookeep hello hello yerel makinede haliyle aynıdır adı hello bırakın. (Yürütülebilir bileşenlerin, diğer bir deyişle, bu özelliği **dağıtma** yöntemi olarak ayarlanmış çok**exec**, bu rastgele bir Windows komut satırı bildirimi olabilir.)
  
  > [!IMPORTANT]
  > Bu değer için boşluk karakterleri kullanırsanız, bunlar farklı hello bağlı olarak işleneceğini yöntemi dağıtın. Merhaba yöntemi dağıtmak ise **exec**, alanları hello dosya adının bir parçası olarak değil de komut satırı bağımsız değişkeni ayırıcı olarak yorumlanır. İçin diğer tüm yöntemler dağıtabilir, alanları hello dosya adının bir parçası olarak yorumlanır.
  > 
  > 
* **Dağıtın:** hello eylemi gösterir yöntemi uygulandığında toohello bileşen hello dağıtımı başladı. Bu değerleri aşağıdaki hello biri olabilir:
  
  * **kopyalama:** hello bileşenidir hello tarafından belirtilen kopyalanan toohello hedef yolu **için** özelliği.
  * **Exec:** hello bileşenidir hello tarafından belirtilen hello yolu Merhaba içeriğine yürütülme yürütülebilir bir Windows komut satırı deyimi **için** özelliği hello zaman hello dağıtımı başlatır.
  * **Hiçbiri:** hello dağıtım başladığında, hiçbir eylem uygulanan toohello bileşendir.
  * **zip:** hello bileşenidir hello tarafından belirtilen sıkıştırması açılmış toohello hedef yolu **için** özelliği. Bu yöntem yalnızca hello zaman kullanılabilir **alma** özelliği **zip**.
* **Kime:** hello sanal makineye hello bileşen dağıtılacağı hedef yolu. Bu özellik Windows ortam değişkenlerini kullanılabilir ve dosya yollarını göreli çok**approot**.

tooadd yeni bir bileşeni tıklatın hello **Ekle** hello düğmesini **bileşenleri** özellik sayfası ve bir **Azure rolü bileşeni** iletişim kutusu açılabilir. Yukarıda açıklanan hello özellikleri için değerleri girin. 

Merhaba aşağıdaki yeni bir WAR bileşen eklemek için bir örneği gösterir.

![][ic719503]

Ne zaman toohello bulut (değil hello işlem öykünücüsü), bir yükleme toodeploy hello bileşeninden istiyorsanız dağıtma emin **bulutta hello pakete dahil etme yerine olduğunda, dağıtım** denetlenir. Azure storage hesabınızdan toodownload istiyorsanız, hello hello depolama hesabı seçin **depolama hesabı** aşağı açılan liste (Merhaba tıklayabilirsiniz **hesapları** hello listesinde nedir toomodify bağlantı), hangi kısmen doldurur hello **URL** alan ve hello URL'sinin kalan hello doldurun. Toouse Azure depolama istemiyorsanız seçin **(hiçbiri)** hello gelen **depolama hesabı** aşağı açılan listesinde ve hello URL tooyour bileşen hello girmek **URL** alan. Hello yöntemler aşağıdaki birini belirtin:

* **kopyalama:** hello indirme bileşenidir hello tarafından belirtilen kopyalanan toohello hedef yolu **tooDirectory** yolu.
* **aynı:** hello için kullanılan aynı yöntemi **dağıtma indirme alanından** olarak **paketinden dağıtma**.
* **zip:** hello indirme bileşenidir hello tarafından belirtilen sıkıştırması açılmış toohello hedef yolu **tooDirectory** yolu.

Bileşen, select hello bileşeni ve tıklatın hello toomodify **Düzenle** hello düğmesini **bileşenleri** özellik sayfası. İzin verme, toomodify hello Bileşen Özellikleri iletişim kutusu açılır. Tuşuna **Tamam** toosave hello bileşen değerleri.

toodelete bileşen, select hello bileşeni ve tıklatın hello **kaldırmak** hello düğmesini **bileşenleri** özellik sayfası ve ardından **Evet** tooconfirm hello silme.

Bileşenleri listelenen hello sırada işlenir. Kullanım hello **Yukarı Taşı** ve **Aşağı Taşı** tooarrange hello sipariş düğmeler.

> [!NOTE]
> Merhaba sunucu yapılandırması özellik bileşenler de kullanır. Bu bileşenler kaldırılır veya hello karşılık gelen sunucu yapılandırması kaldırmadan düzenlenemiyor. Toomake değişiklikleri toosuch bileşenleri çalışırken istenir.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Uç noktalarının özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **uç noktaları**. Bu iletişim kutusu içinde bir uç nokta hello özelliği toocreate sahip yanı sıra düzenleyin veya bir uç nokta hello görüntü aşağıdaki gösterildiği gibi kaldırın.

![][ic719505]

uç noktası, bir tooadd tıklatın hello **Ekle** hello düğmesini **uç noktaları** özellik sayfası ve bir **uç nokta Ekle** iletişim kutusu açılabilir.

![][ic710897]

Merhaba uç noktası için bir ad girin, hello türünü seçin (ya da **giriş**, **dahili**, veya **InstanceInput**) ve hello ortak ve özel bağlantı noktasını belirtin. Tuşuna **Tamam** toosave hello yeni uç nokta değerleri.

Uç nokta Hello türüne bağlı olarak, bağlantı noktası aralıkları gibi kullanabilirsiniz:

* Bir giriş örneğinin uç noktası için bağlantı noktası aralığını hello genel bağlantı noktası olabilir (örneğin **2000 2010**) ve özel bağlantı noktası hello sabit bir değerdir.
* Bir iç uç nokta için hello genel bağlantı noktası kullanılmaz ve hello özel bağlantı noktası aralığı, ya da boş veya kümesi tooan yıldız tooindicate Azure tarafından otomatik olarak ayarlanır olabilir.
* Giriş uç noktaları için hello genel bağlantı noktası yalnızca sabit bir değer olabilir ve hello özel bağlantı noktası bir sabit değer boş veya kümesi tooan yıldız tooindicate Azure tarafından otomatik olarak ayarlanmış olabilir.

Toouse aralığı yerine bir tek bağlantı noktası numarası istiyorsanız hello End hello aralığının hello metin kutusunu boş bırakın.

Toodetermine gerekiyorsa olan kümesi tooautomatic hangi bağlantı noktası gerçekten çalışma zamanı sırasında kullanılan bağlantı noktaları için uygulamanız hello hello belgelenen Azure hizmeti çalışma zamanı API'si kullanabilir [com.microsoft.windowsazure.serviceruntime paketi Özet][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify uç noktası, bir hello endpoint tıklatıp hello **Düzenle** hello düğmesini **uç noktaları** özellik sayfası. Bir iletişim kutusu toomodify hello uç nokta adı, türü ve genel ve özel bağlantı noktaları izin vererek açılır. Tuşuna **Tamam** toosave hello uç nokta değerleri değiştirdi.

toodelete uç noktası, bir hello endpoint tıklatıp hello **kaldırmak** hello düğmesini **uç noktaları** özellik sayfası ve ardından **Evet** tooconfirm hello silme.

Merhaba Araç Seti otomatik olarak kullanıcı tanımlı uç noktaları ile birlikte listelenir özel uç noktaları yapılandırabilir, sipariş tooproperly (örneğin, önbelleğe alma, oturum benzeşimi ya da SSL boşaltma) hello özelliklerden bazıları rol hello kullanıcı tarafından etkinleştirilmiş yapılandırın. Merhaba Araç Seti hello kullanıcı düzenlemesini engeller veya hello özelliği ilişkili olduğu sürece bu otomatik olarak oluşturulan uç noktaları siliniyor etkinleştirilir.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Ortam değişkenlerinin özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **ortam değişkenleri**. Bu iletişim kutusu içinde bir ortam değişkeni hello özelliği toocreate sahip yanı sıra değiştirmek veya bir ortam değişkeni hello görüntü aşağıdaki gösterildiği gibi kaldırın.

![][ic719506]

Merhaba rol başladığında ortamı değişkenleri kullanılabilir tooyour başlangıç betiği kullanılabilir.

> [!NOTE]
> Ortam değişkenleri belirtirken, ortam değişkenlerini Windows tabanlı bir işletim sistemi için geçerli olması gerekir, dağıtımınızı yayımlanan tooa Windows sanal makine, olacağını göz önünde bulundurun.
> 
> 

Merhaba tıklayarak hello rol başladığında kullanılabilir olan bir ortam değişkeni bir örnek, yeni bir ortam değişkeni oluşturma **Ekle** düğmesi. Merhaba aşağıdaki gösterir adlı bir ortam değişkeni **MyRoleVersion** oluşturulur ve hello değeri atanan **1.0**.

![][ic659268]

Jsp kodunuzu içinde hello kullanarak hello değerini görüntüleyebilir `System.getenv` yöntemi:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Uygulamanızı çalıştığında bu çıktıda sonuçlanır:

![][ic552233]

toomodify bir ortam değişkeni hello ortam değişkeni tıklatıp hello **Düzenle** hello düğmesini **ortam değişkenleri** özellik sayfası. İzin verme, toomodify hello ortam değişkeni Özellikleri iletişim kutusu açılır. Tuşuna **Tamam** toosave hello ortam değişkeni değerlerini.

toodelete bir ortam değişkeni hello ortam değişkeni tıklatıp hello **kaldırmak** hello düğmesini **ortam değişkenleri** özellik sayfası ve ardından **Evet**tooconfirm hello silme.

Sipariş tooproperly hello özelliklerden bazıları (örneğin, sunucu yapılandırması, uzaktan hata ayıklama veya yerel depolama) bir rolü hello kullanıcı tarafından etkinleştirilmiş yapılandırmak, hello araç seti ile birlikte listelenen özel ortam değişkenleri otomatik olarak yapılandırabilirsiniz Kullanıcı tanımlı ortam değişkenleri. Merhaba Araç Seti hello kullanıcı düzenlemesini engeller veya hello özelliği ilişkili olduğu sürece bu otomatik olarak oluşturulan ortam değişkenleri silme etkinleştirilir.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Yük Dengeleme / oturum benzeşimi (a.k.a "Yapışkan oturumları") özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **Yük Dengeleme**. Bu iletişim kutusu içinde hello özelliği tooenable sahip veya oturum benzeşimi hello görüntü aşağıdaki gösterildiği gibi devre dışı bırakın.

![][ic719492]

İlgili bilgi için bkz: [oturum benzeşimi][Session Affinity]. Ayrıca, bu özelliğin davranışı SSL boşaltma, hello bağlamda konusunda açıklandığı gibi unutmayın [SSL boşaltma][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Yerel depolama özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **yerel depolama**. Bu iletişim kutusu içinde hello özelliği toocreate sahip, değiştirme veya yerel geçici depolama uygulamanızı çalıştıran hello sanal makine için kaldırın. Belirli değerler için hello boyutu hello yerel depolama yanı sıra hello rol hello görüntü aşağıdaki gösterildiği gibi geri dönüştürüldüğünde hello içeriği olup korunur ayarlanabilir.

![][ic719508]

Ayrıca isteğe bağlı olarak toohello yerel depolama karşılık gelen bir ortam değişkeni belirtebilirsiniz.

Varsayılan olarak, Azure'a dağıttığınız her şeyi yerleştirilen (sıkıştırması açılmış hello ve) **approot** hello rol örneğinin klasör. Çoğu basit dağıtım var. sonra bile Merhaba ayrılmış hello alanı olan sığacak sırada **approot** dizindir sınırlı ve iyi tanımlanmış (1 GB bir makul udur daha azını). Bu nedenle, hello uygun değildir daha büyük dağıtımlar için yeterli disk alanı tooensure Azure ayırır **approot** klasörünü hello kullanarak yerel depolama kaynağı ayarlamalıdır **yerel depolama** iletişim kutusu. Kolay bir yolu toodo için bkz: [dağıtma büyük dağıtımlar][Deploying Large Deployments].

Merhaba depolama kaynağı başlangıç komut dosyalarından kolayca başvurusu yapabilir (örneğin, **startup.cmd**) hello gösterildiğigibiotomatikolarakhelloEclipsearaçtarafındanhellokaynaklailişkilihelloortamdeğişkenikullanarak **Yerel depolama** iletişim. Bu ortam değişkeni, başlangıç komut dosyanızı yürütülen hello zamanında yapılandırdığınız hello yerel kaynak hello tam yolunu içerir. 

toomodify yerel depolama kaynağı hello yerel depolama kaynağı tıklatıp hello **Düzenle** hello düğmesini **yerel depolama** özellik sayfası. İzin verme, toomodify hello yerel depolama kaynağı özellikleri iletişim kutusu açılır. Tuşuna **Tamam** toosave hello yerel depolama kaynağı değerleri.

toodelete yerel depolama kaynağı hello yerel depolama kaynağı tıklatıp hello **kaldırmak** hello düğmesini **yerel depolama** özellik sayfası ve ardından **Evet** tooconfirm hello silme.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Sunucu Yapılandırma Özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **sunucu yapılandırması**. Bu iletişim kutusu içinde hello özelliği tooadd kaldırmak ve hello JDK ve Java uygulama sunucusu dağıtımınızı tarafından kullanılan değiştirmek yanı sıra eklemek veya kaldırmak Dağıtımınızda kullanılan hello uygulamaları (WAR, JAR veya kulak dosyaları gibi) sahip.

### <a name="jdk-configuration"></a>JDK yapılandırma
Bu iletişim kutusu toospecify hello JDK paket toouse dağıtımınız için sağlar. Windows üzerinde Eclipse kullanıyorsanız, hello JDK paketi yerel olarak hello Azure öykünücüsü çalışan toouse ve bu yerel yükleme tooAzure hello seçeneği toodeploy sahip belirtebilirsiniz. Windows olmayan işletim sistemlerinde hello öykünücüsü JDK ayarı uygulanabilir değildir ve dağıtamazsınız hello yerel olarak yüklü JDK Windows ile uyumlu olmadığından. Ancak, hello işletim kullanmakta olduğunuz sisteminden bağımsız olarak, bunun her zaman arasında 3 taraf JDK paketleri toodeploy tooAzure hello ya da kendi Windows uyumlu JDK paketin bir diğer yükleme konumundan noktası seçebilirsiniz.

Merhaba, Windows'da bir JDK nasıl belirtebilirsiniz örneği aşağıdadır:

![][ic780647]

Windows üzerinde Eclipse kullanıyorsanız, JDK toouse hello ile işlem öykünücüsü belirtebilirsiniz; Bu nedenle, toodo emin olun **yerel olarak test etmek için bu dosya yolundan kullanım hello JDK** hello denetlenir **öykünücüsü dağıtım** bölüm. Ardından, hello yerel yol tooyour JDK belirtin; Merhaba bir toouse otomatik olarak seçilmez istiyorsanız toodifferent JDK göz atabilirsiniz. Ayrıca, JDK tooyour Azure bulut hizmeti hello seçeneği toodeploy vardır; toodo, bu nedenle, hello seçin **my yerel JDK (otomatik karşıya yükleme toocloud depolama) dağıtmak** hello seçeneğinde **bulut dağıtımı** bölümü.

Not: Windows olmayan işletim sistemlerinde hello **öykünücüsü dağıtım** ayarları ve hello **my yerel JDK dağıtımı** seçeneği kullanılamaz. Merhaba aşağıdaki örnek bir Mac üzerinde bir JDK belirtme gösterilmektedir veya diğer Windows olmayan işletim sistemi desteklenmiyor:

![][ic789643]

İki aşağıdaki hello sahip olduğunuz üzerinde Hello işletim sisteminden bağımsız olarak **bulut dağıtımı** hello kaynak ve JDK paketinizi türü için seçenekleri:

* **Azure üzerinde kullanılabilir 3 taraf JDK paketi dağıtma** 
* **Özel bir Merkezi'nden dağıtma** 

Merhaba kullanıyorsanız **3 taraf JDK kullanılabilir bir paketi Azure'dan dağıtmak** seçeneği:

1. Adlı hello onay **3 taraf JDK kullanılabilir bir paketi Azure'dan dağıtmak**.
2. Merhaba aşağı açılan listeden, Azure üzerinde kullanılabilir hello 3 taraf JDK paketi seçin.
3. **JDK** sekmesi Windows toohello aşağıdakilere benzer görünür: ![][ic780648] ve Mac OS benzer toohello aşağıda görüneceğini veya diğer Windows olmayan işletim sistemleri desteklenir:![][ic789643]
4. Tıklatın **Tamam** toosave değişikliklerinizi.
5. İstendiğinde tooaccept hello Lisans Sözleşmesi'nden hello 3. taraf JDK paket sağlayıcısı hello Lisans Koşulları'nı inceleyin. Merhaba koşullarını kabul varsayılarak tıklatın **Evet** tooclose hello **lisans sözleşmesini kabul** iletişim.
    Merhaba aşağı açılan listesinde hello öğeler için görünür mantığı temel bu hello Not **3 taraf JDK kullanılabilir bir paketi Azure'dan dağıtmak** seçeneği özelleştirilebilir. Merhaba de toocustomize hello öğelerde **JDK** iletişim kutusunda, hello tıklatın **Özelleştir** bağlantı. Bu hello kapatacak **JDK** özellik sayfası ve açık hello **componentsets.xml** sonra gerektiği gibi değiştirebilirsiniz Eclipse dosyasında. Belgelerine **componentsets.xml** hello dahil **componentsets.xml** kendisini dosya.

Merhaba kullanıyorsanız **özel indirme alanından bir JDK dağıtımı** seçeneği:

1. ZIP JDK yükleme dizininizin oluşturmak, o hello dizin düğüm sağlamaya hello alt hello ZIP yapısı ve içeriğini değil. Daha sonra ihtiyacınız ve bu JDK göz önünde bulundurmanız hello dizininin hello adını not edin yükleme dağıtılan tooa Windows sanal makine olacaktır.
2. Merhaba ZIP Azure depolama hesabınızda blob olarak yükleyin. BLOB'ları tooAzure depolama yüklemek için dışarıdan kullanılabilir olan bir aracı kullanarak bunu yapabilirsiniz. Bu özel bir blob toouse önerilir. Merhaba blob hello ZIP içeriği URL'sini not edin.
3. Adlı hello onay **özel indirme alanından bir JDK dağıtımı**.
    Azure storage hesabınızdan toodownload istiyorsanız, hello hello depolama hesabı seçin **depolama hesabı** aşağı açılan liste (Merhaba tıklayabilirsiniz **hesapları** hello listesinde nedir toomodify bağlantı), hangi kısmen doldurur hello **URL** alan ve hello URL'sinin kalan hello doldurun. Azure depolama toouse istemiyorsanız seçin **(hiçbiri)** hello gelen **depolama hesabı** aşağı açılan listesinde ve JDK karşıdan hello URL tooyour hello girin **URL** alan. Azure storage kullanıyorsanız, hello URL'sindeki blob adları küçük harf olmalıdır.
4. Bu hello olun **JAVA_HOME** textbox toohello doğru dizin adı başvuruyor. Varsayılan olarak, bu başvurur hello hello değer yerel kullanımınız için seçtiğiniz aynı JDK dizin adı. Ancak hello ZIP hello diziniyle farklı bir ada sahip olması gerekir (örneğin, son toousing farklı bir sürüm), güncelleştirme hello dizin adı hello **JAVA_HOME** textbox buna uygun olarak, bu ayar hello kullanılacağından bulut () değil hello işlem öykünücüsü).
5. Tıklatın **Tamam** toosave değişikliklerinizi.

Bu kadar. Şimdi, hello bulut için yapılandırdığınızda, başlangıç paket boyutu çok daha küçük olur, hello oluşturma işlemi genellikle daha az zaman ve hello dağıtım kendisini toohello bulut yayımladığınızda, daha az zaman gerçekleştirmesi gereken fark edeceksiniz. Bu hello Not **my yerel JDK (otomatik karşıya yükleme toocloud depolama) dağıtmak** veya **JDK özel indirme alanından dağıtmak** seçeneklerdir yürürlükte yalnızca hello bulutta uygulamanızı dağıtıldığında. Bunlar, işlem öykünücüsü deneyiminizi üzerinde hiçbir etkisi yoktur; Merhaba bileşenlerin yerel sürümü hello hala toohello işlem öykünücüsü dağıttığınızda kullanılır. 

### <a name="server-configuration"></a>Sunucu Yapılandırması
Merhaba, bir uygulama sunucusu nasıl belirteceğinizi örneği aşağıdadır.

![][ic796926]

Bu hello doğrulayın **bu tür bir sunucu dağıtımı** onay kutusu seçilidir ve hello türü seçin toouse istediğiniz uygulama sunucusu.

Bulut dağıtım için bir sunucu toouse belirtmek için aşağıdaki seçenekleri şu hello yararlanabilirsiniz:

1. **Bir 3. taraf sunucusuna Azure üzerinde kullanılabilir dağıtmak** -bu burada dağıtım verimliliği ve Basitlik, öncelik ve hello sunucu özel bir yapılandırma gerektirmez geliştirme ve test senaryolarında özellikle geçerlidir. Veya hello başlangıç noktası bu sunuculardan biri toouse istiyor ancak dahil uygun sunucu özelleştirme dağıtımınızın başlangıç mantığı adımları.
2. **Özel bir Merkezi'nden dağıtmak** -toouse hello bulutta istediğiniz özel olarak hazırlanmış ve yapılandırılmış bir sunucunuz varsa bu üretim senaryolarında özellikle geçerlidir.
3. **Yerel sunucu yükleme dağıtmak** -Bu, yerel sunucu yüklemesi zaten kullanımınız için özel olarak yapılandırılmış ise özellikle geçerlidir. Bu seçeneği seçerseniz, ayrıca, yerel sunucunuzun yolu hello belirtmeniz gerekir **yerel sunucu yolu** aşağıdaki metin kutusu.

Merhaba kullanıyorsanız **bir 3. taraf sunucusuna Azure üzerinde kullanılabilir dağıtmak** seçeneği:

1. Adlı hello onay **bir 3. taraf sunucusuna Azure üzerinde kullanılabilir dağıtmak**.
2. Merhaba açılan menüden istenen hello sunucu yazılım toouse dağıtımınız ile Merhaba bulutta seçin. Not: sunucu toouse daha önce bir tür zaten belirttiyseniz, sınırlı toochoosing hello olan bir bulut sunucusu olacaktır, sunucu türü olarak aynı aile. Ancak sunucu türü istemediyseniz, Azure üzerinde şu anda kullanılabilir hello sunuculardan herhangi biri arasından seçim yapabilirsiniz ve hello sunucu türünü otomatik olarak sizin için seçilir.
3. Tıklatın **Tamam** toosave değişikliklerinizi.

Merhaba kullanıyorsanız **dağıtma özel indirme alanından** seçeneği:

1. Önceki adımları toohello göre bir sunucu türü zaten seçtiğinizden emin olun. Bu şekilde, özel yükleme toodeploy hello sunucusundan hello nasıl olmalıdır hello eklentisi bildirir, seçilen sunucu türü olarak aynı aile.
2. Adlı hello onay **dağıtma özel indirme alanından**.
    Azure storage hesabınızdan toodownload istiyorsanız, hello hello depolama hesabı seçin **depolama hesabı** aşağı açılan liste (Merhaba tıklayabilirsiniz **hesapları** hello listesinde nedir toomodify bağlantı), hangi kısmen doldurur hello **URL** alan ve hello URL tooyour server kısmını kalan hello doldurun (Azure depolama, hello URL'sindeki blob adları kullanarak küçük harfli olması gerektiğini olduğunda) ZIP indirin. Toouse Azure depolama istemiyorsanız seçin **(hiçbiri)** hello gelen **depolama hesabı** aşağı açılan listesinde ve hello URL tooyour sunucu indirme ZIP hello girin **URL** alan. Merhaba ZIP, uygulama sunucusu yükleme dizinini temsil eden bir alt klasör içerir. Apache Tomcat 7.0.35 zip kullanıyorsanız, örneğin, içinde hello zip Merhaba alt klasörünü temsil eden hello yükleme dizini, gibi olur **apache tomcat 7.0.35**. 
3. Merhaba giriş dizini ortam değişkeni Hello değerini belirtin. Toohello değeri varsa, yerel uygulama sunucusu için kullanılan varsayılan olur, ancak bulut uygulama sunucunuzu yerel uygulama sunucunuzdan farklıysa, farklı bir değer belirtebilirsiniz. Ancak, bulut uygulama sunucunuzu hello emin toomake gerekir ailesini daha önce seçtiğiniz hello sunucu türü.
    Merhaba gelecekteki içinde bulut uygulama sunucusu zip güncelleştirirseniz, hello giriş dizini ayarı veya yeniden eşleşen (yerel uygulama sunucunuza çok değiştirdiyseniz), yerel ayar toohave el ile değiştirebilirsiniz.
4. Tıklatın **Tamam** toosave değişikliklerinizi.

öğeler görünür hello mantığı temel hello **Server** hello sekmesinde **sunucu yapılandırması** özellik sayfası özelleştirilebilir. Gereksinimlerinize hello varsayılan değerleri genişletirseniz ya da diğer sunucuları tooadd istiyorsanız gerekebilecek Gelişmiş bir özelliktir. Merhaba de toocustomize hello mantığında **Server** iletişim kutusunda, hello tıklatın **Özelleştir** bağlantı. Bu hello kapatacak **sunucu yapılandırması** özellik sayfası ve açık hello **componentsets.xml** gerekli tooextend hello sunucu yapılandırması şablon olarak değiştirebileceği Eclipse dosyasında. Belgelerine **componentsets.xml** hello dahil **componentsets.xml** kendisini dosya.

Merhaba kullanıyorsanız **yerel (otomatik karşıya yükleme toocloud depolama) dağıtmak** seçeneği:

1. Adlı hello onay **yerel (otomatik karşıya yükleme toocloud depolama) dağıtmak**.
2. Hello kullanarak **depolama hesabı** aşağı açılan listesinden, **(otomatik)**. Belirtirseniz **(otomatik)** burada hello Araç Seti kullanacağınız Eclipse hello sunucunuz için aynı depolama hesabı hello bir hello dağıtımınızda için seçtiğiniz **tooAzure yayımlama** iletişim.
3. Tıklatın **Tamam** toosave değişikliklerinizi.

Bir sunucu yükleme yolunu, bilgisayarınızdaki hello seçin **yerel sunucu yolu** herhangi hello aşağıdaki koşullar doğruysa, metin kutusunda:

* (Yalnızca tooWindows geçerlidir) hello öykünücüsü dağıtımınızda tootest istiyor.
* Yerel olarak yüklü sunucu toohello bulutunuzu toodeploy istiyor.
* Toouse; bu durumda kendi hello buluta özel sunucu yüklenmesini istediğiniz, ayrıca hello olun **yerel (otomatik karşıya yükleme toocloud depolama) dağıtmak** yukarıda seçili seçeneği.

Seçenekleri önceki hello hiçbiri tooyour durum uygularsanız, hello yerel sunucu isteğe bağlı bir ayardır.

### <a name="applications-configuration"></a>Uygulamaları yapılandırma
Merhaba, bir uygulamanın nasıl belirteceğinizi örneği aşağıdadır.

![][ic719512]

Tıklatın **Ekle** tooadd başka bir uygulama veya **kaldırmak** tooremove bir uygulama. Toouse bir yükleme için bir uygulamanın hello kaynak toohello bulut dağıtırken istiyorsanız, verimliliği amacıyla, hello kullanın [bileşenlerin özellikleri](#components_properties) toospecify bir URL, depolama hesabı, vs. 

Merhaba Nisan 2014 sürümü ile başlayarak, uygulamalarınızı otomatik olarak hello yüklenir aynı depolama hesabındaki (Merhaba altında **eclipsedeploy** kapsayıcı) bir dağıtım için seçtiğiniz hello gibi. Merhaba başlangıç mantığı, dağıtımınızın önce bu uygulamaları bu depolama hesabından indirmeleri bir adım içerir. Bu, toorebuild gerek kalmadan, dağıtımınızdaki uygulamalarınızı yükseltme hello uygulamasına doğrudan (örneğin hello Azure portal kullanarak) bu depolama hesabı'nın daha yeni sürümleri el ile karşıya yükleyerek hello tüm paketi yeniden anlamına gelir , hello WAR dosyaları değiştirme başlangıçta karşıya var. hello araç takımı tarafından. Ardından, yeniden veya komut satırı yardımcı programları üzerinden Azure yönetim portalını kullanarak bu rol örneklerinin hello geri dönüştürme yalnızca başlatın. (Rol geri dönüştürme hello Eclipse toolkit içinde doğrudan tetikleme şu anda desteklenmiyor.)

### <a name="notes-about-server-configuration"></a>Sunucu yapılandırması ile ilgili notlar
Merhaba yapılan değişiklikler **sunucu yapılandırması** özellik sayfası hello yansıtılır `<component>` hello package.xml dosyasının öğeleri.

Merhaba kullandığınızda **otomatik olarak karşıya yükleme...**  veya **indirme alanından Dağıt...**  hello JDK veya uygulama sunucusu ve sizin için seçenekler hello bulut (değil hello işlem öykünücüsü), oluşturma ve bağlı toohello ağı olan, hello konsol çıktısı, hello aşağıdaki gibi iletileri Ant hello gibi yapı karşılaşabilirsiniz Oluşturucu hello indirme'nin kullanılabilirlik doğrular:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Merhaba seçtiyseniz **indirme alanından Dağıt...**  seçeneği, uyarı aşağıdaki hello gösterilmesi ancak hello yapı devam edecek:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Bu uyarı, indirme'nin kullanılabilirlik hello hello tek belirti doğrulandı kurmadı ' dir. Bu nedenle bir dağıtım hello bulutta herhangi bir nedenden dolayı başarısız olursa, bu uyarıyı alırsanız toosee denetleyin.

(Örneğin, bunu gereksiz yere yavaşlatır hello yapı düşünüyorsanız) toodisable hello indirme doğrulama istiyorsanız ayarlayın hello `verifydownloads` çok öznitelik`false` hello içinde `<windowsazurepackage>` package.xml öğesidir: 

`<windowsazurepackage verifydownloads="false" ...>` 

Merhaba seçtiyseniz **otomatik olarak karşıya yükleme...**  seçeneği hello konsol penceresinde yapı iletileri hello karşıya yükleme her 5 karşıya yükleme gerekli olduğunda saniyede raporlama hello ilerlemesini görürsünüz.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL boşaltma özellikleri
Eclipse'nın Proje Gezgini bölmesinde hello rol hello bağlam menüsünü açın, **Azure**ve ardından **SSL boşaltma**. 

![][ic719481]

Bu iletişim kutusu içinde boşaltma, Java uygulama sunucusundaki SSL tooconfigure gerek kalmadan, azure'da Java dağıtımınızdaki Köprü Metni Aktarım Protokolü güvenli (HTTPS) destekleyen tooeasily etkinleştir izin vererek SSL etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [SSL boşaltma] [ SSL Offloading] ve [nasıl tooUse SSL boşaltma][How tooUse SSL Offloading].

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Azure proje özellikleri][Azure Project Properties]

[Azure depolama hesabı listesi][Azure Storage Account List]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

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
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
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
