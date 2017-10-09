---
title: "aaaService doku güvenilir aktörler genel bakış | Microsoft Docs"
description: "Giriş toohello Service Fabric Reliable Actors programlama modeli."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Giriş tooService doku Reliable Actors
Güvenilir aktörler üzerinde hello dayalı bir çerçevedir Service Fabric uygulaması [sanal aktör](http://research.microsoft.com/en-us/projects/orleans/) düzeni. Merhaba güvenilir aktörler API Service Fabric tarafından sağlanan hello ölçeklenebilirlik ve güvenilirlik garantileri üzerine kurulu bir tek iş parçacıklı programlama modeli sağlar.

## <a name="what-are-actors"></a>Aktör nelerdir?
Bir oyuncu hesaplama ve tek iş parçacıklı yürütme durumuyla yalıtılmış, bağımsız bir birimdir. Merhaba [aktör düzeni](https://en.wikipedia.org/wiki/Actor_model) eşzamanlı veya dağıtılmış sistemleri, aynı anda çok sayıda bu aktörler yürütün ve birbirlerine bağımsız olarak bir hesaplama modelidir. Aktör birbirleri ile iletişim kurabilir ve daha fazla aktörler oluşturabilirsiniz.

### <a name="when-toouse-reliable-actors"></a>Zaman toouse Reliable Actors
Service Fabric Reliable Actors hello aktör tasarım deseni uygulamasıdır. Tüm yazılım tasarım deseni gibi hello düzeni toouse belirli bir desene olup yapılan olsun veya olmasın bir yazılım tasarım üzerinde sorun dayalı hello karar sığar.

Merhaba aktör tasarım deseni dağıtılmış sistemlerin sorunları ve senaryoları, dikkat hello düzeni ve hello framework hale getirilmesi gereken uygulama hello kısıtlamaları iyi uygun tooa sayısı olabilse de. Genel bir yönerge olarak hello aktör düzeni toomodel sorun veya senaryoyu göz önünde bulundurun:

* Çok sayıda sorunu alanınızı içerir (binlerce veya daha fazla) küçük, bağımsız ve yalıtılmış birim durumu ve mantığı sayısı.
* Dış bileşenlerinden aktörler kümesi boyunca durumu sorgulama dahil olmak üzere önemli etkileşim gerektirmeyen tek iş parçacıklı nesnelerle toowork istiyor.
* Aktör örneklerinizi g/ç işlemleri vererek beklenmeyen gecikme ile arayanlar engellemez.

## <a name="actors-in-service-fabric"></a>Service Fabric aktör
Service Fabric içinde aktörler hello Reliable Actors framework uygulanır: üstünde bir aktör desen tabanlı uygulama altyapısıdır [Service Fabric Reliable Services](service-fabric-reliable-services-introduction.md). Yazdığınız her güvenilir aktör hizmeti aslında bir bölümlenmiş, durum bilgisi olan güvenilir hizmetidir.

Her aktör aktör türünün bir örneği tanımlanır, aynı toohello .NET nesnesi .NET türünün bir örneği yoludur. Örneğin, bir hesap makinesi hello işlevselliğini uygulayan bir aktör türü olabilir ve çeşitli düğümlerde küme genelinde dağıtılan birçok aktörler türü olabilir. Her tür aktör aktör kimliği ile benzersiz olarak tanımlanır

### <a name="actor-lifetime"></a>Aktör yaşam süresi
Service Fabric aktör sanal, kendi ömürleri bağlı tootheir bellek içi temsili olmadığından emin anlamına gelir. Sonuç olarak, açıkça oluşturulan veya tahrip toobe gerekmez. Merhaba Reliable Actors çalışma zamanı aktör hello bu aktör kimliği için bir istek alırsa ilk kez otomatik olarak etkinleştirir. Bir oyuncu bir süre kullanılmazsa hello Reliable Actors çalışma zamanı çöp-hello bellekteki nesne toplar. Daha sonra yeniden toobe ihtiyacınız olursa, hello aktör'ın varlığı bilgisi de korur. Daha fazla ayrıntı için bkz: [aktör yaşam döngüsü ve atık toplama](service-fabric-reliable-actors-lifecycle.md).

Bu sanal aktör ömrü soyutlama hello sanal aktör modeli sonucunda bazı uyarılar gerçekleştirir ve hatta hello Reliable Actors uygulama bazen bu modelden farklılık göstermesi.

* Bir oyuncu (bir aktör oluşturulan nesne toobe neden) otomatik olarak etkinleştirilir hello tooits aktör kimliği gönderilen bir ileti ilk kez Belirli bir süre sonra toplanacak hello aktör nesnesidir. Hello hello aktör kimliği kullanarak yeniden, gelecekteki yeni aktör oluşturulan nesne toobe neden olur. Bir aktör'in durumunu hello nesnesinin ömrü outlives hello durum Yöneticisi'nde depolanan olduğunda.
* Aktör kimliği için herhangi bir aktör yöntemini çağırmadan bu aktör etkinleştirir. Bu nedenle, aktör türlerini örtük olarak hello çalışma zamanı tarafından adlı kendi oluşturucuya sahip. Bu nedenle, istemci kodu parametreleri toohello aktör'ın Oluşturucusu hello hizmeti tarafından kendisine geçirilen ancak parametreleri toohello aktör türünün Oluşturucusu geçiremezsiniz. Merhaba hello aktör başlatma parametreleri hello istemciden gerektiriyorsa aktörler kısmen başlatılmış bir durumda diğer yöntemleri, üzerine denir hello zamana göre oluşturulması, sonucudur. Bir oyuncu hello istemciden hello etkinleştirilmesi için tek giriş noktası yok.
* Reliable Actors örtülü olarak aktör nesneleri oluştursanız da; hello özelliği tooexplicitly bir aktör silip durumuna sahip.

### <a name="distribution-and-failover"></a>Dağıtım ve yük devretme
tooprovide ölçeklenebilirlik ve güvenilirlik, Service Fabric aktör hello küme boyunca ve otomatik olarak dağıtır bunları gerektiği gibi başarısız düğümlerin toohealthy olanları gelen geçirir. Bu bir üzerinden soyutlamadır bir [bölümlenmiş, durum bilgisi olan güvenilir hizmet](service-fabric-concepts-partitioning.md). Dağıtım, ölçeklenebilirlik, güvenilirlik ve otomatik yük devretme tüm sağlanan aktörler bir durum bilgisi olan güvenilir hello adlı hizmeti içinde çalışan hello olgu, *aktör hizmeti*.

Aktör hello aktör hizmeti hello bölümleri arasında dağıtılır ve bu bölümler bir Service Fabric kümesindeki hello düğümler arasında dağıtılır. Her bir hizmet bölümü aktörler kümesini içerir. Service Fabric, dağıtım ve yük devretme hello hizmet bölümlerinin yönetir.

Örneğin, bir aktör hizmeti dokuz bölümleri olan hello varsayılan aktör bölüm yerleştirme kullanarak düğümler thusly dağıtılmış toothree dağıtılan:

![Güvenilir aktörler dağıtım][2]

Merhaba aktör Framework sizin için bölüm düzeni ve anahtar aralığı ayarlarını yönetir. Bu, bazı seçenekleri basitleştirir ancak ayrıca bazı önem taşır:

* Bölüm sayısı ve güvenilir hizmetler toochoose bölümleme düzeni (bölümleme aralığı kullanırken) anahtar aralığı sağlar. Güvenilir aktörler kısıtlı toohello aralığı bölümleme düzeni (Merhaba Tekdüzen Int64 düzeni) ve hello tam Int64 anahtar aralığını kullanmanız gerekir.
* Varsayılan olarak, aktörler rastgele Tekdüzen dağıtımlarında kaynaklanan bölümlere yerleştirilir.
* Aktör rastgele yerleştirildiğinden aktör işlemleri ağ iletişimi, seri hale getirme ve seri durumundan çıkarma gecikme süresi ve ek yükü yansıtılmasını yöntemi çağrısı verileri de dahil olmak üzere her zaman gerektirecektir beklenmelidir.
* Gelişmiş senaryolar, olası toocontrol aktör bölüm yerleştirme Int64 aktör toospecific bölümleri eşleme kimlikleri kullanmaktır. Ancak, bunun bölümler böylece aktörler dengesiz bir dağıtım sonuçlanabilir.

Aktör hizmetleri nasıl bölümlenir daha fazla bilgi için çok başvuran[kavramları aktörleri bölümleme](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Aktör iletişimi
Aktör etkileşimleri hello arabirimini uygulayan hello aktör ve bir proxy tooan aktör hello aracılığıyla alır hello istemci tarafından paylaşılan bir arabirim tanımlanmış aynı arabirimi. Bu arabirim kullanılan tooinvoke aktör yöntemleri zaman uyumsuz olarak olduğundan, hello arabirimdeki her yöntem görev döndürme olması gerekir.

Sonuçta yöntem çağrılarını ve yanıtlarını hello küme, bunu hello bağımsız değişkenleri ve dönüş hello platformu tarafından seri hale getirilebilir olmaları gerekir, hello görevlerin hello sonuç türleri arasında ağ isteklerine neden. Özellikle, olmalıdır [veri sözleşmesi seri hale getirilebilir](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>Merhaba aktör proxy
Merhaba Reliable Actors istemci API aktör örneği aktör istemci arasında iletişimi sağlar. toocommunicate bir aktör ile bir istemci hello aktör arabirimini uygulayan bir aktör proxy nesnesi oluşturur. Merhaba istemci hello proxy nesnesi üzerinde bildirilecekse yöntemlerle hello aktör ile etkileşime girer. Merhaba aktör proxy istemci aktör ve aktör aktör iletişimi için kullanılabilir.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Merhaba iki parça bilgi toocreate hello aktör proxy nesnesi kullanılan Not: hello aktör kimliği ve hello uygulama adı. Merhaba aktör kimliği hello uygulama adı hello tanımlayan sırada hello aktör benzersiz olarak tanımlayan [Service Fabric uygulaması](service-fabric-reliable-actors-platform.md#application-model) hello aktör dağıtıldığı.

Merhaba `ActorProxy`(C#) / `ActorProxyBase`(Java) sınıfı hello istemci tarafında hello gerekli çözümleme toolocate hello aktör Kimliğine göre gerçekleştirir ve bir iletişim kanalı ile açın. İletişim hataları ve yük devretme işlemlerini hello durumlarda toolocate hello aktör yeniden dener. Sonuç olarak, ileti teslimi hello aşağıdaki özelliklere sahiptir:

* İleti teslimi en iyi çaba olur.
* Aktör hello yinelenen iletileri alabilirsiniz aynı istemci.

### <a name="concurrency"></a>Eşzamanlılık
Merhaba Reliable Actors çalışma zamanı aktör yöntemleri erişmek için bir basit Aç tabanlı erişim modeli sağlar. Başka bir deyişle, birden fazla iş parçacığı dilediğiniz zaman içinde aktör nesnenin kod etkin olabilir. Veri erişimi için eşitleme mekanizmaları için gerekli olduğu Aç tabanlı erişim eşzamanlı sistemleri büyük ölçüde basitleştirir. Ayrıca, sistemleri için özel hususlar her aktör örneğinin ile Merhaba tek iş parçacıklı erişim yapısı tasarlanmalıdır anlamına gelir.

* Bir tek aktör örneği aynı anda birden fazla isteği işleyemiyor. Beklenen toohandle eşzamanlı istek ise aktör örneği bir işleme performans sorunu neden olabilir.
* Bir dış istek hello aktör tooone aynı anda yapılan sırada iki aktörler arasında döngüsel bir istek varsa aktörler birbirine kilitlenme. Merhaba aktör çalışma zamanı otomatik olarak zaman aşımına aktör çağırır ve olası kilitlenme durumlarda bir özel durum toohello arayan toointerrupt atar.

![Güvenilir aktörler iletişim][3]

#### <a name="turn-based-access"></a>Bırakma tabanlı erişim
Bir dönüş hello tam olarak yürütülmesini diğer aktörler veya istemciler yanıt tooa isteği aktör yönteminde veya hello tam olarak yürütülmesini oluşur bir [Zamanlayıcı/anımsatıcı](service-fabric-reliable-actors-timers-reminders.md) geri çağırma. Bu yöntem ve geri aramalar zaman uyumsuz olmasına karşın, hello aktörler çalışma zamanı bunları Interleave değil. Yeni bir dönüş izin verilmeden önce bir dönüş tam olarak tamamlanmış olmalıdır. Diğer bir deyişle, şu anda yürütülen bir aktör yöntemi veya Zamanlayıcı/anımsatıcı geri önce yeni bir çağrı tooa yöntemi tam olarak tamamlanmış olmalıdır veya geri çağırma izin verilir. Bir yöntem veya geri çağırma toohave tamamlanmış hello yürütme hello yönteminden döndürülen veya hello yöntemi veya geri çağırma tarafından döndürülen geri çağırma ve hello görevi tamamlandı olarak kabul edilir. Bu o Aç tabanlı eşzamanlılık bile farklı yöntemler, zamanlayıcılar ve geri aramalar arasında dikkate değer vurgulayan olur.

Aktör başına kilit bir dönüş hello başında alınırken tarafından Hello aktörler çalışma zamanı Aç tabanlı eşzamanlılık zorunlu kılan ve hello hello sonunda hello kilidi serbest bırakma. Bu nedenle, dönüş tabanlı eşzamanlılık aktör başına temelinde arasında değil aktörler zorlanır. Aynı anda aktör yöntemleri ve Zamanlayıcı/anımsatıcı geri aramalar adına farklı aktörler yürütebilir.

Aşağıdaki örneğine hello kavramları yukarıda hello gösterilmektedir. İki zaman uyumsuz yöntemleri uygulayan bir aktör türü göz önünde bulundurun (örneğin, *Method1* ve *Method2*), bir Zamanlayıcı ve bir anımsatıcı. Merhaba diyagrama iki aktörler adına bu yöntemleri ve geri aramalar hello yürütme için bir zaman çizelgesi örneği gösterir (*ActorId1* ve *ActorId2*) toothis aktör türü ait.

![Güvenilir aktörler çalışma zamanı Aç tabanlı eşzamanlılık ve erişim][1]

Bu diyagramda, bu kuralları aşağıdaki gibidir:

* Her dikey çizgi hello mantıksal akışını bir yöntem ya da bir geri çağırma belirli aktör adına gösterir.
* Merhaba olaylar dikey her satırda işaretlenmiş kronolojik sırada eskiler yeni olayların ile oluşur.
* Farklı renk zaman çizelgelerini karşılık gelen toodifferent aktörler için kullanılır.
* Vurgulama hangi hello için yöntemi veya geri çağırma adına aktör başına kilit tutulur kullanılan tooindicate hello süresi geçen süredir.

Bazı önemli noktalar tooconsider:

* Sırada *Method1* adına yürütüyor *ActorId2* yanıt tooclient isteğinde *xyz789*, başka bir istemci isteği (*abc123*) ulaşan de gerektirir *Method1* tarafından yürütülen toobe *ActorId2*. Ancak, ikinci yürütülmesi hello *Method1* hello önceki yürütme tamamlanana kadar başlamaz. Benzer şekilde, bir anımsatıcı kayıtlı tarafından *ActorId2* sırasında ateşlenir *Method1* yanıt tooclient istekte yürütülen *xyz789*. Merhaba anımsatıcı geri çağırma yalnızca her iki yürütmeleri sonra yürütülür *Method1* tamamlandığından. Tüm bu olduğu için zorlanan tooturn tabanlı eşzamanlılık son *ActorId2*.
* Benzer şekilde, bırakma tabanlı eşzamanlılık ayrıca için zorunlu *ActorId1*tarafından hello yürütülmesi gösterildiği gibi *Method1*, *Method2*, ve Zamanlayıcı geri adına hello *ActorId1* seri biçimde olmuyor.
* Yürütülmesi *Method1* adına *ActorId1* adına yürütülmesinin ile çakışıyor *ActorId2*. Bırakma tabanlı eşzamanlılık yalnızca bir aktör içinde arasında değil aktörler zorlanır olmasıdır.
* Bazı hello yöntemi/geri çağırma yürütmeleri hello `Task`(C#) / `CompletableFuture`(Java) hello metodu döndükten sonra hello yöntemi/geri araması bitirdiğinde tarafından döndürülen. Bazı bazılarında hello zaman uyumsuz işlem zaten hello yöntemi/geri döndürür hello zamanına göre bitirdi. Her iki durumda da, yalnızca iki hello yöntemi/geri döndürür ve hello zaman uyumsuz işlemi tamamlandıktan sonra hello aktör başına kilit yayımlanır.

#### <a name="reentrancy"></a>Yeniden giriş
Merhaba aktörler çalışma zamanı yeniden giriş varsayılan olarak izin verir. Bu olması durumunda bir aktör yöntemi anlamına gelir *aktör A* bir yöntemi çağırır *aktör B*, sırayla çağıran başka bir yöntem üzerinde *aktör A*, yöntem toorun izin verilir. Merhaba parçası olduğundan bu olduğu aynı mantıksal çağrı zincirine bağlamı. Tüm Zamanlayıcı ve anımsatıcı çağrıları hello yeni mantıksal çağrı içeriği ile başlatın. Merhaba bkz [Reliable Actors yeniden giriş](service-fabric-reliable-actors-reentrancy.md) daha fazla ayrıntı için.

#### <a name="scope-of-concurrency-guarantees"></a>Eşzamanlılık garanti kapsamı
Merhaba aktörler çalışma zamanı bu eşzamanlılık garantiler burada bu yöntemlerin hello çağırma denetimleri durumlarda sağlar. Örneğin, Zamanlayıcı ve anımsatıcı geri aramalar yanı sıra, yanıt tooa istemci isteğinde bitti hello yöntem çağrılarına için bu garantileri sağlar. Ancak, Hello aktör kodu doğrudan hello mekanizmaları hello aktörler çalışma zamanı tarafından sağlanan dışında bu yöntemleri çağırırsa, hello çalışma zamanı eşzamanlılık garanti sağlayamaz. Örneğin, hello aktör yöntemleri tarafından döndürülen hello görev ile ilişkili değil bazı görev hello bağlamında Hello yöntemi çağrıldıysa hello çalışma zamanı eşzamanlılık garanti sağlayamaz. Bir iş parçacığından Hello yöntemi çağrıldıysa bu hello aktör, kendi oluşturur, ardından hello çalışma zamanı da eşzamanlılık garanti sağlayamaz. Aktörler tooperform arka plan işlemleri, bu nedenle, kullanmalısınız [aktör zamanlayıcılar ve aktör anımsatıcıları](service-fabric-reliable-actors-timers-reminders.md) Aç tabanlı eşzamanlılık saygılı olun.

## <a name="next-steps"></a>Sonraki adımlar
* İlk Reliable Actors hizmetiniz oluşturarak başlayın:
   * [.NET üzerinde Reliable Actors ile çalışmaya başlama](service-fabric-reliable-actors-get-started.md)
   * [Üzerinde Java Reliable Actors ile çalışmaya başlama](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
