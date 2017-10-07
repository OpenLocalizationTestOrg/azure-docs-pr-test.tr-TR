---
title: "aaaHow tooConfigure bir uygulama hizmeti ortamı v1"
description: "Yapılandırma, yönetim ve uygulama hizmeti ortamı v1 Merhaba izleme"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Bir uygulama hizmeti ortamı v1

> [!NOTE]
> Uygulama hizmeti ortamı v1 hello hakkında makaledir.  Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Genel Bakış
Yüksek bir düzeyde bir Azure uygulama hizmeti ortamı birkaç önemli bileşenlerden oluşur:

* Uygulama hizmeti ortamı hello çalışan işlem kaynakları barındıran hizmet
* Depolama
* Bir veritabanı
* Classic(V1) veya kaynak Manager(V2) Azure sanal ağ (VNet) 
* Bir alt ağ içinde çalışan hello uygulama hizmeti ortamı'nın barındırılan hizmeti ile

### <a name="compute-resources"></a>İşlem kaynaklarını
Merhaba işlem kaynakları, dört kaynak havuzları için kullanın.  Her uygulama hizmeti ortamı'nın (ana) ön uçlar ve üç olası çalışan havuzu kümesi vardır. Tüm üç alt havuzları--toouse gerekmeyen isterseniz, yalnızca bir veya iki kullanabilirsiniz.

Merhaba konakları hello kaynak havuzlarında (ön uçlar ve çalışanlar) doğrudan erişilebilir tootenants değildir. Uzak Masaüstü Protokolü (RDP) tooconnect toothem kullanmak, kendi sağlama değiştiremez veya bunları bir yönetim görevi görür.

Kaynak havuzu miktarı ve boyutu ayarlayabilirsiniz. ASE'de, P1 P4 aracılığıyla etiketli dört boyutu seçeneğiniz vardır. Bu boyutları ve bunların fiyatlandırma hakkında daha fazla ayrıntı için bkz: [uygulama hizmeti fiyatlandırma](../app-service/app-service-value-prop-what-is.md).
Merhaba miktarı veya boyutunu değiştirme bir ölçeklendirme işlemi adı verilir.  Yalnızca bir ölçeklendirme işlemi aynı anda ediyor olabilir.

**Ön Uçları**: hello ön uçlar olan hello HTTP/HTTPS uç noktaları, ana tutulan uygulamalarınız için. Ön Uçları hello iş yükleri çalıştırmayın.

* Bir ana geliştirme ve test iş yükleri ve alt düzey üretim iş yükleri için yeterli olan iki P2s ile başlar. Kesinlikle P3s üretim iş yükleri için Orta tooheavy öneririz.
* Orta tooheavy üretim iş yükleri için en az dört P3s tooensure zamanlanmış bakım oluştuğunda çalıştıran yeterli ön uçlar vardır sahip olmasını öneririz. Zamanlanmış bakım etkinlikler aynı anda bir ön uç çıkarır. Bu genel azaltır bakım etkinlikleri sırasında kullanılabilir ön uç kapasitesi.
* Ön Uçları tooan saat tooprovision alabilir. 
* Daha fazla ölçek ince ayar için hello CPU yüzdesi ve bellek yüzdesi etkin istek ölçümleri hello ön uç havuzu için izlemeniz gerekir. Merhaba CPU veya bellek yüzdelerini P3s çalıştırırken yüzde 70 varsa, daha fazla ön uçlar ekleyin. Merhaba etkin istek değeri ortalama, too15, 000 too20, ön uç başına 000 istekleri çıkışı daha fazla ön uçlar eklemeniz gerekir. Merhaba genel tookeep CPU ve bellek yüzdelerini % 70 ve etkin P3s çalıştırırken toobelow 15.000 istekleri ön uç başına ortalama istek aşağıda hedeftir.  

**Çalışanlar**: hello çalışanlardır uygulamalarınızı gerçekte çalıştırdığı. App Service planlarına ölçeklendirdiğinizde hello çalışanlarına temizleme işleminde çalışan havuzunda ilişkilendirilmiş.

* Çalışanlar anında ekleyemezsiniz. Bunlar tooan saat tooprovision sürebilir.
* Herhangi bir havuz için bir işlem kaynağı Hello boyutunu ölçeklendirme güncelleştirme etki alanı başına < 1 saat sürer. ASE'de 20 güncelleştirme etki alanı yoktur. Merhaba işlem boyutu 10 örneğiyle çalışan havuzunda ölçeği, too10 saatleri toocomplete ele geçirebilir.
* Çalışan havuzunda kullanılan hello işlem kaynakları hello boyutunu değiştirirseniz, çalışan havuzunda çalışan hello uygulamaların soğuk başlatır neden olur.

toochange hello işlem uygulamalardan çalıştırmayan bir çalışan havuzu kaynak boyutu hello en hızlı yolu şudur:

* Çalışanlar too2 Hello miktarını ölçeklendirin.  Merhaba minimum ölçek hello portal boyutunda aşağı 2'dir. Bu işlem birkaç dakika toodeallocate örneklerinizi olur. 
* Merhaba yeni işlem boyutu ve örneklerinin sayısını seçin. Buradan, too2 saatleri toocomplete olur.

Uygulamalarınızı daha büyük bir işlem kaynak boyutu gerektiriyorsa, hello önceki kılavuzunun yararlanamaz. Bu uygulamaları barındıran hello çalışan havuzunda Hello boyutunu değiştirme yerine başka bir çalışan havuzu hello istenen boyutta arkadaşlarınızla doldurmak ve uygulamalarınızı toothat havuzunda taşıyın.

* Başka bir çalışan havuzu boyutu işlem gerekli hello ek örneklerini Hello oluşturun. Bu tooan saat toocomplete sürecek.
* Daha büyük boyutu yeni yapılandırılmış toohello çalışan havuzunda gereken hello uygulamaları barındırma, uygulama hizmeti planları yeniden atayın. Bu dakika toocomplete değerinden yapması gereken hızlı bir işlemdir.  
* Artık kullanılmayan Bu örneklerde gerekmiyorsa hello ilk çalışan havuzunda ölçeklendirin. Bu işlem birkaç dakika toocomplete alır.

**Otomatik ölçeklendirmeyi**: bir toomanage yardımcı olabilecek hello araçlarının işlem kaynak tüketimini otomatik ölçeklendirme yapıyor. Otomatik ölçeklendirme için kullanabileceğiniz ön uç veya çalışan havuzlarında. Merhaba sabah örneklerinizi herhangi bir havuz türde bu artış gibi şeyler ve hello Akşam azaltır. Veya bir çalışan havuzunda kullanılabilir çalışan hello sayısı belirli bir eşiğin altına düştüğünde örnekleri belki de ekleyebilirsiniz.

İşlem kaynak havuzu ölçümleri geçici tooset otomatik ölçeklendirme kurallarını istediğiniz sonra bu sağlama göz hello süre tutmak gerektirir. Otomatik ölçeklendirmeyi App Service ortamları hakkında daha fazla ayrıntı için bkz: [nasıl tooconfigure otomatik ölçeklendirme uygulama hizmeti ortamı'nda][ASEAutoscale].

### <a name="storage"></a>Depolama
Her ana 500 GB depolama yapılandırılır. Bu alanı hello ana tüm hello uygulamaları arasında kullanılır. Bu depolama alanı hello ana bir parçasıdır ve anahtarlı toouse depolama alanınızı şu anda olamaz. Ayarlamaları tooyour sanal ağ yönlendirme veya güvenlik yapıyorsanız, toostill gereken erişim tooAzure depolama--izin vermek veya hello ana çalışamaz.

### <a name="database"></a>Database
Merhaba veritabanı içinde çalıştırılan hello uygulamaları hello ayrıntılarını yanı sıra hello ortamı tanımlar hello bilgileri tutar. Bu çok bir hello Azure tutulan abonelik parçasıdır. Bir şey doğrudan özelliği toomanipulate sahip değil. Ayarlamaları tooyour sanal ağ yönlendirme veya güvenlik yapıyorsanız, toostill gereken erişim tooSQL Azure--izin vermek veya hello ana çalışamaz.

### <a name="network"></a>Ağ
Merhaba, ana ile kullanılan VNet hello ana oluşturduğunuzda yaptığınız veya önceden yapılan olabilir. Ana oluşturma sırasında hello alt ağ oluşturduğunuzda, hello ana toobe hello içinde zorlar hello sanal ağ ile aynı kaynak grubunda. Daha sonra sanal ağınızı farklı, ana toobe tarafından kullanılan hello kaynak grubu gerekiyorsa, resource manager şablonu kullanarak, ana toocreate gerekir.

Bir ana için kullanılan sanal ağda hello bazı sınırlamalar vardır:

* Merhaba sanal ağı bölgesel bir sanal ağ olmalıdır.
* Toobe hello ana dağıtıldığı 8 veya daha fazla adresleri olan bir alt ağ gerekir.
* Bir alt ağ kullanılan toohost bir ana sonra hello adres aralığı hello alt ağ değiştirilemez. Bu nedenle, gelecekteki ana büyümesine en az 64 adresleri tooaccommodate hello alt içeren öneririz.
* Olabilir hello alt ancak hello ana başka bir şey.

Merhaba ana içeren hello barındırılan hizmet hello [sanal ağ] [ virtualnetwork] ve alt ağ kullanıcı denetimi altında.  Sanal ağınızı hello sanal ağ kullanıcı Arabirimi veya PowerShell ile yönetebilirsiniz.  Bir ana Klasik veya Resource Manager Vnet'i dağıtılabilir.  Merhaba portal ve API deneyimleri Klasik ve Resource Manager sanal ağlar arasında biraz farklılık gösterir ancak hello ana deneyimi aynı hello değil.

Merhaba, kullanılan toohost bir ana sanal ağ ya da özel RFC1918 IP adresleri kullanabilirsiniz veya genel IP adresleri kullanabilirsiniz.  RFC1918 tarafından kapsanmayan bir IP aralığı toouse isterseniz (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) ana oluşturma öncesinde, ana tarafından kullanılan, VNet ve alt ağ toobe toocreate yüklemeniz gerekir.

Bu özellik hello Azure App Service sanal ağınızda yerleştirir olduğundan, ana barındırılan uygulamalarınızı şimdi doğrudan ExpressRoute veya siteden siteye sanal özel ağlar (VPN) kullanılabilir hale getirilir kaynaklara erişebilir anlamına gelir. Uygulama hizmeti ortamınızı içinde hello uygulamalar, uygulama hizmeti ortamınızı barındıran ek ağ özellikleri tooaccess kaynakları kullanılabilir toohello sanal ağ gerekmez. Başka bir deyişle, toouse VNET tümleştirme ya da karma bağlantılar tooget tooresources içinde veya bağlı tooyour sanal ağ gerekmez. Tooaccess kaynakları olmayan ağlarda tooyour sanal ağa bağlı olsa bu özelliklerin her ikisi de kullanmaya devam edebilirsiniz.

Örneğin, aboneliğinizde olmakla birlikte, ana içinde bağlı toohello sanal ağı olmayan bir sanal ağ ile VNET tümleştirme toointegrate kullanabilirsiniz. Normalde yapabildiğiniz gibi diğer ağlarda, karma bağlantılar tooaccess kaynakları yine de kullanabilirsiniz.  

Bir ExpressRoute VPN ile yapılandırılmış sanal ağınız varsa, bir ana sahip hello yönlendirme gereksinimlerini bazıları farkında olmalıdır. Bir ana ile uyumlu olmayan bazı kullanıcı tanımlı yönlendirme (UDR) yapılandırmaları vardır. ExpressRoute ile bir sanal ağ içinde bir ana çalıştırma hakkında daha fazla ayrıntı için bkz: [bir sanal ağ ExpressRoute ile bir uygulama hizmeti ortamı çalışan][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Gelen trafiğinin güvenliğini sağlama
İki birincil yöntemleri toocontrol vardır gelen trafiği tooyour ana.  Hangi IP ağ güvenlik Groups(NSGs) toocontrol kullanabilirsiniz adresleri burada açıklandığı şekilde, ana erişim [nasıl toocontrol gelen bir uygulama hizmeti ortamı trafiği](app-service-app-service-environment-control-inbound-traffic.md) ve bir iç yük ile ana de yapılandırabilirsiniz Balancer(ILB).  Nsg'ler tooyour ILB ana kullanarak toorestrict erişmek istiyorsanız bu özellikleri de birlikte kullanılabilir.

Bir ana oluşturduğunuzda, sanal ağınızda bir VIP oluşturur.  İki VIP türleri, iç ve dış vardır.  Bir dış VIP ile bir ana oluşturduğunuzda, ana uygulamalarınızda bir Internet yönlendirilebilir IP adresi erişilebilir olacaktır. İç, ana seçtiğinizde, bir ILB ile yapılandırılmış ve doğrudan internet erişilebilir olmaz.  Bir ILB ana hala bir dış VIP gerektiriyor, ancak yalnızca Azure yönetim ve Bakım erişimi için kullanılır.  

ILB ana oluşturma sırasında ILB ana hello tarafından kullanılan hello alt etki alanı sağlayın ve toomanage kendi DNS hello alt belirtmeniz gerekir.  Hello alt etki alanı adı ayarlamak için de HTTPS erişimi için kullanılan toomanage hello sertifika gerekiyor.  Sonra ana olduğunuz oluşturma tooprovide hello sertifika istenir.  oluşturma ve bir ILB ana kullanma hakkında daha fazla toolearn okuma [bir uygulama hizmeti ortamı ile bir iç yük dengeleyici kullanarak][ILBASE]. 

## <a name="portal"></a>Portal
Yönetebilir ve uygulama hizmeti ortamınızı hello UI hello Azure portal kullanarak izleyebilirsiniz. Ardından bir ana varsa, büyük olasılıkla toosee hello uygulama hizmeti simgesi Kenar çubuğunda olur. Bu simgenin kullanılan toorepresent App Service ortamları hello Azure portal'ın şöyledir:

![Uygulama hizmeti ortamı simgesi][1]

tooopen tüm App Service ortamları listeler UI Merhaba, hello simgesine veya select hello Köşeli Çift Ayraca kullanabilirsiniz (">" simgesi) hello kenar tooselect App Service ortamları hello sonundaki. Listelenen hello ASEs birini seçerek hello kullanılan toomonitor olan kullanıcı arabirimini açın ve yönetebilirsiniz.

![İzleme ve uygulama hizmeti ortamınızı yönetmek için kullanıcı Arabirimi][2]

Bu ilk Kama kaynak havuzu başına ölçüm grafik yanı sıra, ana bazı özelliklerini gösterir. Hello gösterilen hello özelliklerden bazıları **Essentials** blok olan de onunla ilişkilendirilen hello dikey yukarı açılır köprüler. Örneğin, hello seçebilirsiniz **sanal ağ** adı tooopen hello UI yukarı, ana çalıştığı hello sanal ağ ile ilişkili. **Uygulama hizmeti planları** ve **uygulamaları** , ana bu öğeleri listesinde Kanatlar her açın.  

### <a name="monitoring"></a>İzleme
Merhaba grafikleri toosee çeşitli performans ölçümleri her kaynak havuzundaki izin verin. Merhaba ön uç havuzu için hello ortalama CPU ve bellek izleyebilirsiniz. Çalışan havuzlarında kullanılan hello ve kullanılabilir olan hello miktar izleyebilirsiniz.

Birden çok uygulama hizmeti planları yapabilirsiniz hello çalışanı çalışan havuzunda kullanın. Merhaba iş yükü yok hello CPU ve bellek kullanımı sağlamak için çok yararlı bilgiler hello yolu hello ön uç sunucuları gibi aynı deneyerek hello dağıtılmaz. Daha önemli tootrack olan kaç kullandığınızı çalışanları ve özellikle, bu sistem başkaları için yönetiyorsanız kullanılabilir--toouse.  

Ayrıca, tüm uyarıları hello grafikleri tooset izlenebilir hello ölçümleri de kullanabilirsiniz. Ayarlama, burada works aynı olarak başka bir yere App Service'te hello uyarır. Bir uyarı ya da hello ayarlayabilirsiniz **uyarıları** UI parçası ya da kullanıcı Arabirimi ve seçerek herhangi ölçümleri inmelerini **eklemek uyarı**.

![Ölçümleri kullanıcı Arabirimi][3]

yalnızca bahsedilen hello ölçümleri hello uygulama hizmeti ortamı ölçümleridir. Uygulama hizmeti planı düzeyi hello kullanılabilir ölçümleri de vardır. Bu, CPU ve bellek izleme algılama çok kılan unsurdur.

ASE'de, App Service planlarına hello ayrılmış uygulama hizmeti planları tümü. Merhaba ayrılan konakları toothat uygulama hizmeti planı üzerinde çalışan hello yalnızca uygulamaların bu uygulama hizmeti planında hello uygulamaları olmasını anlamına gelir. Uygulama hizmeti planınızı toosee ayrıntıları herhangi birinden hello listeleri hello ana UI veya gelen uygulama hizmeti planınızı Getir **Gözat App Service planlarına** (listelerinin bunların tümünün).   

### <a name="settings"></a>Ayarlar
Hello ana Dikey içinde var olan bir **ayarları** çeşitli önemli özellikleri içeren bölümü:

**Ayarları** > **özellikleri**: Merhaba **ayarları** dikey penceresi otomatik olarak açılır, ana dikey getirdiğinizde. Hello üstünde olduğu **özellikleri**. İçinde gördüğünüz yedekli toowhat olan öğelerin burada birkaç vardır **Essentials**, ancak çok kullanışlı nedir **sanal IP adresi**, yanı **giden IP adreslerini**.

![Ayarlar dikey ve özellikleri][4]

**Ayarları** > **IP adreslerini**: bir IP Güvenli Yuva Katmanı (SSL) uygulama, ana oluşturduğunuzda, bir IP SSL adresi gerekir. Sipariş tooobtain içinde biri, ana ayrılabilen sahibi IP SSL adres olması gerekir. Bir ana oluşturulduğunda, bu amaç için bir IP SSL adresi vardır, ancak daha ekleyebilirsiniz. Var olan bir ücret ek IP SSL adresleri için gösterildiği gibi [uygulama hizmeti fiyatlandırma] [ AppServicePricing] (bölümünde hello SSL bağlantılarını). Merhaba ek hello IP SSL fiyat fiyatıdır.

**Ayarları** > **ön uç havuzu** / **çalışan havuzlarında**: her bu kaynak havuzu dikey hello özelliği toosee bilgi yalnızca bu kaynak havuzu sunar , ayrıca tooproviding toofully ölçek bu kaynak havuzu denetler.  

Hello temel dikey pencere her kaynak havuzu için bu kaynak havuzu için bir grafik ölçümlerle sağlar. Gibi hello grafiklerle hello ana dikey penceresinden, hello şemasına gidin ve istediğiniz gibi uyarıları ayarlama. Belirli bir kaynak havuzu için hello ana dikey penceresinden bir uyarı ayarını hello kaynak havuzundan yapmakta olarak aynı anlama hello. Merhaba çalışan havuzundan **ayarları** dikey penceresinde, App Service planlarına bu çalışan havuzunda çalışmakta olan veya erişim tooall hello uygulamaları yüklü.

![Çalışan havuzu ayarları kullanıcı Arabirimi][5]

### <a name="portal-scale-capabilities"></a>Portal ölçeği özellikleri
Üç ölçeklendirme işlemleri şunlardır:

* IP SSL kullanımı için uygun olan hello ana IP adresleri Hello sayısını değiştirme.
* Bir kaynak havuzunda kullanılan hello işlem kaynak Hello boyutunu değiştirme.
* Bir kaynak havuzu el ile veya otomatik ölçeklendirmeyi aracılığıyla kullanılan işlem kaynakları Hello sayısını değiştirme.

Merhaba Portalı'nda, kaynak havuzlarında sahip kaç tane sunucuya üç yolu toocontrol vardır:

* Merhaba ana ana dikey penceresinde hello üstünde bir ölçeklendirme işlemi. Birden fazla ölçek yaptığınız yapılandırma değişiklikleri toohello ön uç ve çalışan havuzlarında. Tek bir işlem olarak tüm uygulanır.
* El ile ölçeklendirme işlemi hello tek başına bir kaynak havuzundan **ölçek** altındaki dikey **ayarları**.
* Merhaba tek tek kaynak havuzundan ayarladığınız otomatik ölçeklendirmeyi **ölçek** dikey.

toouse hello ölçeklendirme işlemi hello ana dikey penceresinde, istediğiniz ve kaydetme hello kaydırıcı toohello miktarı sürükleyin. Bu UI, değişen hello boyutu da destekler.  

![Ölçek kullanıcı Arabirimi][6]

belirli kaynak havuzundaki toouse hello el ile veya otomatik ölçeklendirme özelliği Git çok**ayarları** > **ön uç havuzu** / **çalışan havuzlarında** olarak uygun. Ardından hello kuyruğunu toochange istediğiniz açın. Çok Git**ayarları** > **ölçeği Genişlet** veya **ayarları** > **ölçeği Artır**. Merhaba **ölçeği Genişlet** dikey toocontrol örneği miktar sağlar. **Ölçeği Artır** toocontrol kaynak boyutu sağlar.  

![Ölçek ayarları kullanıcı Arabirimi][7]

## <a name="fault-tolerance-considerations"></a>Hataya dayanıklılık konuları
Bir uygulama hizmeti ortamı toouse too55 toplam işlem kaynakları yapılandırabilirsiniz. Bu 55 işlem kaynakları yalnızca 50 kullanılan toohost iş yükleri olabilir. Bunun nedeni Hello yönlüdür. En az 2 ön uç işlem kaynakları yoktur.  Too53 toosupport hello çalışan havuzu ayırma bırakır. Sipariş tooprovide hata toleransı içinde toohave toohello kurallara göre ayrılmış bir ek hesaplama kaynağı gerekir:

* Her bir çalışan havuzu, bir iş yükü atanan kullanılabilir toobe olmayan en az 1 ek hesaplama kaynağa gerekir.
* Merhaba miktar çalışan havuzunda işlem kaynakları üzerinde belirli bir değere gittiğinde, başka bir işlem kaynağı hataya dayanıklılık için gerekli değildir. Bu hello ön uç havuzu hello durumda değil.

Herhangi bir tek çalışan havuzunda içinde belirli bir X değeri için kaynakları tooa çalışan havuzuna atanmış hello hataya dayanıklılık gereksinimleri şunlardır:

* X 2 ile 20 arasında hello tutar iş yükleri için kullanabileceğiniz kullanılabilir işlem kaynakları X-1 ise.
* X 21 ile 40 arasında hello tutar iş yükleri için kullanabileceğiniz kullanılabilir işlem kaynakları X-2 ise.
* X 41 ve 53 arasındaysa hello iş yükleri için kullanabileceğiniz kullanılabilir işlem kaynakları X-3 miktarıdır.

Merhaba minimum ayak izini 2 ön uç sunucuları ve 2 çalışan vardır.  Ardından deyimleri yukarıda Hello ile birkaç örnek tooclarify şunlardır:  

* Tek bir havuzda 30 çalışanları varsa, bunların 28 kullanılan toohost iş yükleri olabilir.
* Tek bir havuzda 2 çalışan varsa, 1 kullanılan toohost iş yükleri olabilir.
* Tek bir havuzda 20 çalışanları varsa, 19 kullanılan toohost iş yükleri olabilir.  
* Tek bir havuzda 21 çalışanları varsa, kullanılan toohost iş yükleri 19 yalnızca sonra hala.  

Merhaba hataya dayanıklılık en boy önemlidir, ancak bunu aklınızda ölçeklendirme belirli eşikleri tookeep gerekir. 21 herhangi daha fazla Kapasite eklemek değil çünkü tooadd fazla Kapasite 20 örnekleri sonra gidin too22 geçiyor ya da daha yüksek istiyorsanız. Merhaba aynı kapasite ekler hello sonraki sayıyı 42 olduğu 40 giderek geçerlidir.  

## <a name="deleting-an-app-service-environment"></a>Bir uygulama hizmeti ortamı siliniyor
Bir uygulama hizmeti ortamı toodelete istiyorsanız, hello yalnızca kullanın **silmek** eylemin hello uygulama hizmeti ortamı dikey penceresinde hello üstünde. Bunu yaptığınızda, gerçekten toodo bu istediğinizi, uygulama hizmeti ortamı tooconfirm istendiğinde tooenter hello adı olması. Bir uygulama hizmeti ortamı sildiğinizde, tüm içeriğini hello içindeki de Sil unutmayın.  

![Bir uygulama hizmeti ortamı UI silin.][9]  

## <a name="getting-started"></a>Başlarken
Uygulama hizmeti ortamları ile çalışmaya tooget bkz [nasıl toocreate bir uygulama hizmeti ortamı](app-service-web-how-to-create-an-app-service-environment.md).

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
