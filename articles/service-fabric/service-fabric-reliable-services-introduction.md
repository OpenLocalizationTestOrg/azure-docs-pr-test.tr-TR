---
title: "Merhaba doku güvenilir hizmeti programlama modeli aaaOverview | Microsoft Docs"
description: "Service Fabric'ın güvenilir hizmet programlama modeli hakkında bilgi edinin ve kendi Hizmetleri yazma çalışmaya başlayın."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Reliable Services özelliğine genel bakış
Azure Service Fabric, yazma ve durum bilgisiz ve durum bilgisi olan güvenilir hizmetler yönetme basitleştirir. Bu konu şunları içerir:

* Durum bilgisiz ve durum bilgisi olan hizmeti Hello Reliable Services programlama modeli.
* Merhaba seçeneğiniz toomake, güvenilir bir hizmet yazılırken vardır.
* Bazı senaryolar ve ne zaman örnekler güvenilir toouse Hizmetleri ve bunların nasıl yazılır.

Güvenilir hizmetler biridir hello programlama modelleri Service Fabric üzerinde kullanılabilir. Hello başka bir sanal aktör programlama modeli hello Reliable Services model üzerinde sağlayan hello güvenilir aktör programlama modeli, ' dir. Merhaba Reliable Actors programlama modeli hakkında daha fazla bilgi için bkz: [giriş tooService doku Reliable Actors](service-fabric-reliable-actors-introduction.md).

Service Fabric aracılığıyla Hizmetleri'nden, sağlama ve dağıtım yükseltme ve silme, aracılığıyla hello ömrü yönetir [Service Fabric uygulaması Yönetimi](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>Güvenilir hizmetler nelerdir?
Basit, güçlü, üst düzey programlama modeli toohelp önemli tooyour uygulama nedir express güvenilir hizmetler sağlar. Merhaba güvenilir programlama modeli Hizmetleri ile şunları alırsınız:

* Erişim toohello kalan Service Fabric API'leri programlama hello. Service Fabric olarak Modellenen Hizmetleri aksine [Konuk yürütülebilir dosyalar](service-fabric-deploy-existing-app.md), güvenilir hizmetler toouse hello hello Service Fabric API'leri geri kalanı doğrudan alın. Bu hizmetleri sağlar:
  * Sorgu hello sistemi
  * Merhaba kümesindeki varlıklar hakkında rapor durumu
  * Yapılandırma ve kodun değişiklikler hakkında bildirim almak
  * bulma ve diğer hizmetleri ile iletişim
  * (isteğe bağlı) hello kullan [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md)
  * .. .ve onların erişim toomany diğer özellikleri, çeşitli programlama dillerinde birinci sınıf bir programlama modeli çekmenize.
* Kendi kodunuzu çalıştırmak için basit bir model için kullanılan modellerini programlama gibi görünüyor. Kodunuzu bir iyi tanımlanmış giriş noktası ve kolayca yönetilebilir yaşam döngüsü vardır.
* Takılabilir iletişim modelini. HTTP ile gibi tercih ettiğiniz Hello taşıması kullanan [Web API](service-fabric-reliable-services-communication-webapi.md), WebSockets, özel TCP protokolleri ya da başka bir şey. Güvenilir hizmetler, Giden kutusu seçeneklerini kullanabilirsiniz ya da kendi sağlayabilir bazı harika sağlar.
* Durum bilgisi olan hizmetler için hello güvenilir programlama modeli Hizmetleri tooconsistently sağlar ve durumunuz sağ hizmetinizi iç kullanarak güvenilir bir şekilde depolamak [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md). C# koleksiyonları kullanan bilinen tooanyone olacak yüksek oranda kullanılabilir ve güvenilir koleksiyon sınıfları basit bir dizi güvenilir koleksiyonlarıdır. Geleneksel olarak, dış sistemler güvenilir durum yönetimi için gereken hizmetleri. Güvenilir koleksiyonlarla, durumu sonraki tooyour ile işlem hello depolayabilir aynı yüksek kullanılabilirlik ve güvenilirlik seçtiğiniz gelen tooexpect yüksek oranda kullanılabilir dış depolar. Hello işlem ve toofunction gerekiyor durumunda birlikte bulundurmak çünkü bu modeli gecikme süresi de geliştirir.

Bu genel bir bakış güvenilir hizmetler için Microsoft Virtual Academy videosunu izleyin.<center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>Güvenilir hizmetler farklı ne yapar?
Service Fabric güvenilir Hizmetleri'nde önce yazılmış Hizmetleri'nden farklıdır. Service Fabric, güvenilirlik, kullanılabilirlik, tutarlılık ve ölçeklenebilirlik sağlar.

* **Güvenilirlik** - hizmet kalır yukarı burada makinelerinizi başarısız veya ağ sorunları, isabet bile güvenilir olmayan ortamlarda veya burada hello Hizmetleri kendilerini durumlarda hataları ve kilitlenme karşılaştığınız veya başarısız. Durum bilgisi olan hizmetler için durumu bile hello bulunması ağ veya diğer hataları korunur.
* **Kullanılabilirlik** -, erişilebilir ve esnek bir hizmettir. Service Fabric kopyaları çalışan istenen numaranızı tutar.
* **Ölçeklenebilirlik** - Hizmetleri belirli donanım ayrılmış ve büyütür veya hello eklenmesi veya kaldırılması donanım veya diğer kaynakları aracılığıyla gerektiği gibi küçültür. Hizmetlerdir hello hizmetini ölçeklendirebilirsiniz (özellikle durumda hello durum bilgisi olan) kolayca bölümlenmiş tooensure ve tanıtıcı kısmi hatalar. Hizmetleri oluşturulabilir ve dinamik olarak daha fazla örnekleri toobe gerektiği gibi çalışmaya başlar etkinleştirme kodu aracılığıyla silinmiş yanıt toocustomer isteklerinde söyleyin. Son olarak, Service Fabric Hizmetleri toobe basit önerir. Service Fabric tek bir işlem içinde sağlanan yerine gerektiren veya tüm işletim sistemi örneği veya işlemler tooa tek örnekli bir hizmetin ayrılması Hizmetleri toobe binlerce sağlar.
* **Tutarlılık** -bu hizmetinde depolanan tüm bilgileri toobe tutarlı güvence altına alınabilir. Bu hizmet içinde birden çok güvenilir koleksiyonları arasında bile geçerlidir. İşlemsel olarak atomik bir biçimde bir hizmet kapsamındaki koleksiyonları arasında değişiklik yapılabilir.

## <a name="service-lifecycle"></a>Hizmet yaşam döngüsü
Durum bilgisi olan veya durum bilgisiz hizmetinizi olup olmadığını belirtir, hızlı bir şekilde kodunuzda takın ve çalışmaya başlama sağlayan basit bir yaşam döngüsü güvenilir hizmetler sağlar.  Çalışır hizmetinizi tooimplement tooget gerekir, yalnızca bir veya iki yöntem vardır.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -burada hello hizmetini toouse istediği hello iletişimi stack(s) tanımlar bu yöntemidir. iletişim yığını gibi hello [Web API](service-fabric-reliable-services-communication-webapi.md), dinleme bitiş noktası olan hello ne tanımlar veya uç noktaları için hizmet (nasıl istemcileri hello hizmete erişmek) hello. Ayrıca, görünen hello iletileri hello servis kodu hello kalanı ile nasıl etkileşim tanımlar.
* **RunAsync** -bu yöntem hizmetiniz, iş mantığını çalıştığı ve burada bunu hello hizmet hello ömrü boyunca çalışması gerektiğini herhangi bir arka plan görevi devre dışı kazandırın değildir. sağlanan hello iptal belirteci zaman bu iş durması gerektiğini sinyaldir. Merhaba hizmet toopull iletileri güvenilir bir sıra dışında gerekir ve bunları işlemek, örneğin, bunu burada o iş olur.

Güvenilir hizmetler hello için ilk kez öğrendiğiniz okumaya devam edin! Merhaba yaşam döngüsünü güvenilir hizmetler için ayrıntılı bilgileri arıyorsanız, üzerinden çok head[bu makalede](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Örnek Hizmetleri
Bu programlama modeli bilerek bir hızlı parçaların nasıl bir araya getireceğinizi iki farklı Hizmetleri toosee bakalım.

### <a name="stateless-reliable-services"></a>Durum bilgisiz güvenilir hizmetler
Bir durum bilgisi olmayan bir hizmettir hello Hizmeti'nde çağrıları arasında tutulan bir durum yok. Mevcut herhangi bir durum tamamen atılabilir ve eşitleme, çoğaltma, sürdürme veya yüksek kullanılabilirlik gerektirmez.

Örneğin, belleğe sahip değil ve aynı anda tüm hüküm ve işlemleri tooperform alan bir hesap makinesi göz önünde bulundurun.

Bu durumda, hello `RunAsync()` (C#) veya `runAsync()` (Java) Merhaba hizmet boş olamaz, arka plan yok olduğundan görev işleme hello hizmet toodo gerekiyor. Merhaba hesaplayıcı hizmet oluşturulduğunda döndürür bir `ICommunicationListener` (C#) veya `CommunicationListener` (Java) (örneğin [Web API](service-fabric-reliable-services-communication-webapi.md)), açılan bazı bağlantı noktası üzerinde dinleyen bir uç noktası. Bu dinleme bitiş toohello farklı hesaplama yöntemlerini kanca oluşturur (örnek: "Ekle (n1, n2)") hello hesaplayıcı'nın genel API'si tanımlayın.

Bir istemciden bir çağrısı yapıldığında hello uygun yöntemi çağrılır ve hello hesap makinesi hizmetinin sağlanan verileri ve hello sonucunu döndürür hello hello işlemleri gerçekleştirir. Herhangi bir durum depolamak değil.

Herhangi bir iç durum depolamayın Bu örnek hesaplayıcı kolaylaştırır. Ancak çoğu Hizmetleri gerçekten durum bilgisiz değil. Bunun yerine, bunlar kendi durumu toosome diğer deposu hale getirmesini sağlayarak. (Örneğin, bir yedekleme deposu veya önbelleği oturum durumu tutmayı güvenen herhangi bir web uygulamasına durum bilgisiz değildir.)

Nasıl durum bilgisi olmayan hizmetler için yaygın bir örnek, Service Fabric kullanılır düzenlemenizi sağlayan bir web uygulaması için genel kullanıma yönelik API hello bir ön uç değil. Merhaba ön uç hizmeti ardından toostateful Hizmetleri toocomplete Kullanıcı isteği alınmaktadır. Bu durumda, istemcilerden gelen çağrıları 80 gibi hello durum bilgisiz hizmet burada dinleme yaptığı bağlantı bilinen yönlendirilmiş tooa aynıdır. Bu durum bilgisiz hizmet hello araması aldığı ve hello çağrısı güvenilir bir tarafın olup olmadığını ve hangi hizmet belirler için hedeflenen.  Ardından, hello durum bilgisiz hizmet hello çağrısı toohello doğru bölüm hello durum bilgisi olan hizmet iletir ve yanıt bekler. Merhaba durum bilgisiz hizmeti bir yanıtı aldığında toohello özgün istemci yanıt verir. Bu tür bir hizmet, bizim örneklerimizi örneğidir [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Bu yalnızca bir örneği hello örnekleri bu modelinde, vardır başkalarının diğer örneklerinde.

### <a name="stateful-reliable-services"></a>Durum bilgisi olan güvenilir hizmetler
Durum bilgisi olan hizmet durumu tutarlı ve hello hizmet toofunction sırada mevcut tutulan kısmı olmalıdır biridir. Sürekli olarak çalışırken ortalama aldığı güncelleştirmelerine göre belirli bir değerin hesaplar bir hizmeti kullanmayı düşünün. toodo bunu hello geçerli tooprocess gerekli gelen istekleri kümesine sahip ve hello geçerli ortalama gerekir. Alır, işler ve (örneğin, bir Azure blob veya tablo deposu Bugün) bir dış deposunda bilgileri depolayan herhangi durum bilgisi olan hizmetidir. Yalnızca durumuna hello dış durum deposunda saklar.

Merhaba dış deposu için bu duruma güvenilirlik, kullanılabilirlik, ölçeklenebilirlik ve tutarlılık sağladıkları olduğundan çoğu Hizmetleri bugün durumlarına harici olarak depolar. Service Fabric içinde Hizmetleri durumlarına dışarıdan gerekli toostore değil. Service Fabric hello servis kodu ve hello hizmeti durumu için bu gereksinimleri ilgilenir.

> [!NOTE]
> Durum bilgisi olan güvenilir hizmetler için destek henüz (C# veya Java) için Linux üzerinde kullanılabilir değil.
>

Toowrite resimlerini işleyen bir hizmet istiyoruz varsayalım. toodo bu dönüşümleri tooperform, görüntü üzerindeki görüntü ve hello bir dizi hello hizmet alır. (Şimdi onu bir Webapı olduğunu varsayın) bu hizmeti iletişimi dinleyici düzenlemenizi sağlayan bir API ister döndürür `ConvertImage(Image i, IList<Conversion> conversions)`. Bir istek aldığında, hello hizmet depolar bir `IReliableQueue`ve böylece hello isteği izleyebilirsiniz bazı kimliği toohello istemci döndürür.

Bu hizmette `RunAsync()` daha karmaşık olabilir. Merhaba hizmetine sahip bir döngü içinde kendi `RunAsync()` dışı istekleri çeker `IReliableQueue` ve istenen hello dönüşümleri gerçekleştirir. Hello sonuçları depolanan bir `IReliableDictionary` zaman hello istemci geri gelir böylece dönüştürülen resimlerinin elde edebilirsiniz. tooensure başka bir şey hello görüntü başarısız olsa bile kaybı olmadığından, bu güvenilir hizmet hello sıra dışında çekme, hello dönüşümlerini gerçekleştirmek ve tümünü tek bir işlemde hello sonucu depolamak. Bu durumda, selamlama iletisine hello sıradan kaldırılır ve yalnızca hello dönüşümleri tamamlandığında hello sonuçları hello sonuç sözlükte depolanır. Alternatif olarak, hello hizmeti hello görüntü hello sıra dışında çekme ve hemen bir uzak depolama alanında depolar. Bu hello azaltır durum hello hizmeti miktarını toomanage var, ancak hello hizmet tookeep hello gerekli meta veri toomanage hello uzak deposu olduğundan karmaşıklığını artırır. Bir şey de başarısız olursa ya da bir yaklaşım ile Merhaba Orta hello isteği hello sıra bekleme toobe işlenen kalır.

Bu hizmet hakkında bir şey toonote gibi normal bir .NET hizmetine sesleri değil! Merhaba yalnızca kullanılan hello veri yapıları farktır (`IReliableQueue` ve `IReliableDictionary`) Service Fabric tarafından sağlanan ve yüksek oranda güvenilir, kullanılabilir ve tutarlı.

## <a name="when-toouse-reliable-services-apis"></a>Zaman toouse güvenilir hizmetler API'leri
Merhaba aşağıdakilerden herhangi birini uygulama hizmeti gereksinimlerinizi niteleyen bile güvenilir hizmetler API'leri düşünmeniz gerekir:

* Hizmetinizin kodunu istediğiniz (ve isteğe bağlı olarak durumu) yüksek oranda kullanılabilir ve güvenilir toobe
* İşlem garanti durumu (örneğin, siparişler ve satır öğeleri sipariş) birden çok birimi arasında gerekir.
* Uygulamanızın durumu doğal olarak güvenilir sözlükler ve Kuyruklar modellenebilir.
* Uygulamaların kod ya da durum toobe düşük gecikme süresi okuma ve yazma işlemleri ile yüksek oranda kullanılabilir gerekir.
* Uygulamanızı bir veya daha fazla güvenilir koleksiyonlarındaki toocontrol hello eşzamanlılık veya uygulaması yapılan işlemler kesinliği gerekiyor.
* Toomanage hello iletişimleri ya da hizmetiniz için bölümleme denetim hello istiyor.
* Kodunuzu bir ücretsiz iş parçacıklı çalışma zamanı ortamı gerekir.
* Toodynamically uygulamanız gereken oluşturun veya güvenilir sözlükler veya sıralar veya çalışma zamanında tüm hizmetleri yok.
* Tooprogrammatically denetimi Service Fabric tarafından sağlanan yedekleme ve geri yükleme özellikleri için Hizmetinizin durumunu gerekir.
* Uygulamanızı toomaintain değişiklik geçmişini kendi durumu birimleri için gerekir.
* Toodevelop istediğiniz veya üçüncü taraf geliştirilmiş, özel durum sağlayıcılarının kullanabilir.

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
* [Kullanım Gelişmiş güvenilir hizmetler](service-fabric-reliable-services-advanced-usage.md)
* [Merhaba Reliable Actors programlama modeli](service-fabric-reliable-actors-introduction.md)
