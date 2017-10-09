---
title: "aaaAzure geçiş ile ilgili SSS | Microsoft Docs"
description: "Azure geçişi hakkında sık sorulan sorular yanıtlar toosome alın."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Azure geçiş SSS

Bu makalede hakkında bazı sık sorulan sorular (SSS) yanıtları [Azure geçiş](https://azure.microsoft.com/services/service-bus/). Genel Azure fiyatlandırma ve destek bilgileri için bkz: [Azure destek SSS](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions"></a>Genel sorular
### <a name="what-is-azure-relay"></a>Azure Geçiş nedir?
Merhaba [Azure geçiş hizmeti](relay-what-is-it.md) kurumsal bir ağ toohello genel bulut içinde sunmaya hizmetlere daha güvenli bir şekilde yardımcı olarak karma uygulamalarınızı kolaylaştırır. Bir güvenlik duvarı bağlantı açmadan ve tooa kurumsal ağ altyapısına müdahale eden değişiklikler gerektirmeden hello Hizmetleri getirebilir.

### <a name="what-is-a-relay-namespace"></a>Bir geçiş ad alanı nedir?
A [ad alanı](relay-create-namespace-portal.md) uygulamanızdaki tooaddress geçiş kaynakları kullanabilirsiniz kapsanan bir kapsayıcıdır. Ad alanı toouse geçiş oluşturmanız gerekir. Bu, Başlarken hello ilk adımlar biridir.

### <a name="what-happened-tooservice-bus-relay-service"></a>Hangi happened tooService Bus geçişi hizmetini?
daha önce Service Bus geçişi hizmetini adlı hello şimdi WCF geçiş adı verilir. Her zamanki gibi bu hizmet toouse devam edebilirsiniz. Merhaba karma bağlantılar Azure BizTalk Services transplanted bir hizmeti güncelleştirilmiş bir sürümünü özelliğidir. WCF geçiş ve karma bağlantılar desteklenen toobe devam eder.

## <a name="pricing"></a>Fiyatlandırma
Sık sorulan bazı hakkında sorular bu bölümde yanıtlar fiyatlandırma yapısına geçiş hello. Ayrıca bkz [Azure desteği ile ilgili SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma bilgileri için. Geçiş fiyatlandırma hakkında tam bilgi için bkz: [Service Bus fiyatlandırma ayrıntıları][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>Karma bağlantılar ve WCF geçiş için nasıl ücret?
Merhaba geçiş fiyatlandırma hakkında tam bilgi için bkz: [karma bağlantılar ve WCF geçişler] [ Pricing overview] hello Service Bus fiyatlandırma ayrıntıları sayfasında tablo. Ayrıca toohello fiyatlar not ettiğiniz bu sayfada ilişkili veri aktarımları, uygulamanızın sağlandı hello datacenter dışında çıkışı için ücretlendirilirsiniz.

### <a name="how-am-i-billed-for-hybrid-connections"></a>Karma bağlantılar için nasıl faturalandırılır?
Karma bağlantılar için üç örnek fatura senaryoları şunlardır:

*   Senaryo 1:
    *   Merhaba karma Bağlantı Yöneticisi yüklü ve hello tüm ay için sürekli olarak çalışan bir örneği gibi tek bir dinleyicisi var.
    *   3 GB veri hello ay hello bağlantısı üzerinden gönder. 
    *   Toplam ücret $5'tir.
*   Senaryo 2:
    *   Merhaba karma Bağlantı Yöneticisi yüklü ve hello tüm ay için sürekli olarak çalışan bir örneği gibi tek bir dinleyicisi var.
    *   10 GB veri hello ay hello bağlantısı üzerinden gönder.
    *   Toplam ücret $7.50 ' dir. 5 hello bağlantısı için ve ilk 5 GB + 2,50 için ek 5 GB veri hello.
*   Senaryo 3:
    *   A ve B, hello karma Bağlantı Yöneticisi yüklü ve hello tüm ay için sürekli çalışan iki örneği vardır.
    *   3 GB veri bağlantısının hello ay boyunca gönderin.
    *   6 GB veri hello Ay B bağlantısı üzerinden gönder.
    *   Toplam ücret $10,50 ' dir. Olan 5 bağlantısının için 5 bağlantı B için + 0,50 (için B bağlantıda hello altıncı gigabayt).

Merhaba örneklerde kullanılan hello fiyatlar yalnızca hello karma bağlantılar Önizleme dönemi boyunca geçerli olduğunu unutmayın. Karma bağlantılar genel kullanılabilirliğini temel konu toochange fiyatlarıdır.

### <a name="how-are-hours-calculated-for-relay"></a>Saat geçiş için nasıl hesaplanır?

WCF geçiş yalnızca standart katmanı ad alanları ile kullanılabilir. Fiyatlandırma ve [bağlantı kotaları](../service-bus-messaging/service-bus-quotas.md) geçişler aksi değişip değişmediğini için. Bu geçişler toobe hello iletileri (olmayan işlemler) sayısına göre ücret devam ve saat relay anlamına gelir. Merhaba daha fazla bilgi için bkz: ["Karma bağlantılar ve WCF geçişler"](https://azure.microsoft.com/pricing/details/service-bus/) fiyatlandırma ayrıntıları sayfası hello tablosunda.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>Birden çok dinleyici bağlı tooa belirli geçiş yoksa ne miyim?
Bazı durumlarda, tek bir geçiş birden fazla bağlı dinleyicileri olabilir. En az bir geçiş dinleyicisi bağlı tooit olduğunda geçiş açık olarak kabul edilir. Ek geçiş saatleri dinleyicileri tooan açık geçiş sonuçları ekleniyor. Merhaba numarası geçişini bağlı tooa geçiş olan (çağırma istemcileri veya gönderme iletileri toorelays) Gönderenler geçiş saatleri hello hesaplanması etkilemez.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>Merhaba iletileri ölçer WCF geçişler için nasıl hesaplanır?
(**Bu yalnızca tooWCF geçişler için geçerlidir. İletileri karma bağlantılar için bir maliyet değildir.** )

Geçişler kullanılarak hesaplanır için genel olarak, Faturalanabilir iletileri aynı hello için kullanılan yöntem aracılı daha önce açıklanan varlıkları (kuyruklar, konular ve abonelikler). Ancak, önemli bazı farklar vardır.

"Tam yoluyla" Merhaba ileti alır toohello geçiş dinleyicisi Gönder, ileti tooa Service Bus geçişi gönderme kabul edilir. Teslim toohello geçiş dinleyicisi tarafından izlenen bir gönderme işlemi toohello Service Bus geçişi olarak işlenmez. İstek-yanıt stili hizmet başlatma (birini yukarı too64 KB) iki Faturalanabilir ileti aktarma dinleyicisi sonuçlarında karşı: hello isteği ve faturalanabilir bir ileti hello yanıt için bir Faturalanabilir ileti (hello yanıt olduğunu da 64 KB varsayarak veya daha küçük). Bu, istemci ve hizmet arasındaki bir sıra toomediate kullanmaktan farklıdır. İstemci ve hizmet arasındaki bir sıra toomediate kullanırsanız, hello aynı istek-yanıt düzeni hello sıra toohello hizmetinden dequeue/teslim tarafından izlenen bir istek Gönder toohello sırası gerektirir. Bu yanıt gönderme tooanother sırası ve dequeue/teslim o sıra toohello istemciden izler. Aynı (yukarı too64 KB) boyunca varsayımlar boyut hello kullanarak hello sıra düzeni 4 Faturalanabilir iletileri sonuçlarında mediated. İki kez hello sayısı aynı geçişi kullanarak gerçekleştirmek desen iletileri tooimplement hello için fatura. Elbette, dayanıklılık ve Yük Dengeleme gibi bu deseni avantajları toousing sıraları tooachieve vardır. Avantajlar hello ek gider justify.

Hello kullanarak açık geçişler **netTCPRelay** WCF bağlama tek bir ileti olarak değil, ancak hello sistemi üzerinden akan bir veri akışı olarak iletileri kabul eder. Bu bağlama kullandığınızda, yalnızca hello gönderen ve dinleyici hello çerçeveleme gönderilen ve alınan hello tek tek iletilerinin görünürlük gerekir. Merhaba kullanan geçişler için **netTCPRelay** bağlama, tüm verileri olarak değerlendirilir Faturalanabilir iletileri hesaplamak için bir akış. Bu durumda, Service Bus hello toplam gönderilen veya alınan 5 dakikalık aralıklarla tek tek her geçiş aracılığıyla veri miktarını hesaplar. Ardından, toplam veri miktarı 64 KB toodetermine hello bu geçiş Faturalanabilir ileti sayısı bu süre içinde böler.

## <a name="quotas"></a>Kotalar
| Kota adı | Kapsam | Tür | Aşıldığında davranışı | Değer |
| --- | --- | --- | --- | --- |
| Bir geçiş üzerinde eşzamanlı dinleyicileri |Varlık |Statik |Sonraki istekleri için ek bağlantıları reddedilir ve kodu çağırma hello tarafından bir özel durum aldı. |25 |
| Eşzamanlı geçiş dinleyicileri |Sistem çapında |Statik |Sonraki istekleri için ek bağlantıları reddedilir ve kodu çağırma hello tarafından bir özel durum aldı. |2,000 |
| Bir hizmet ad alanındaki tüm geçiş uç noktaları başına eşzamanlı geçiş bağlantıları |Sistem çapında |Statik |- |5,000 |
| Hizmet ad alanı başına geçiş uç noktaları |Sistem çapında |Statik |- |10,000 |
| İleti boyutu için [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) ve [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) geçişleri |Sistem çapında |Statik |Bu kotalar aşan gelen iletileri reddedilir ve kodu çağırma hello tarafından bir özel durum aldı. |64 KB |
| İleti boyutu için [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) ve [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) geçişleri |Sistem çapında |Statik |- |Sınırsız |

### <a name="does-relay-have-any-usage-quotas"></a>Geçiş tüm kullanım kotalarını var mı?
Varsayılan olarak, tüm bulut hizmeti için tüm müşteri'nin abonelikler arasında hesaplanan bir toplama aylık kullanım kotası Microsoft ayarlar. Bazen gereksinimlerinizi bu sınırları aşabilir olduğunu anlayın. Biz gereksinimlerinizi anlamak ve bu sınırları uygun şekilde ayarlamak için Müşteri Hizmetleri herhangi bir zamanda başvurabilirsiniz. Hizmet veri yolu için hello toplama kullanım kotalarını aşağıdaki gibidir:

* 5 milyar ileti
* 2 milyon geçiş saati

Biz hello sağ toodisable aylık kullanım kotalarını aşıyor hesabınız rezerve rağmen e-posta bildirimi sağladığımız ve herhangi bir işlem gerçekleştirmeden önce birden çok deneme toocontact hello müşteri vermiyoruz. Bu kotalar aşan müşterileri için aşırı ücretler hala sorumludur.

### <a name="naming-restrictions"></a>Adlandırma kısıtlamaları
Bir geçiş ad alanı adı uzunluğu 6 ile 50 karakter arasında olmalıdır.

## <a name="subscription-and-namespace-management"></a>Abonelik ve ad alanı yönetimi
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Ad alanı tooanother Azure aboneliği nasıl geçişini?

toomove bir Azure aboneliği tooanother aboneliğe ilişkin bir ad alanı, şunları yapabilirsiniz ya da kullanım hello [Azure portal](https://portal.azure.com) veya PowerShell komutlarını kullanın. bir ad alanı tooanother abonelik toomove hello ad alanı zaten etkin olması gerekir. Merhaba komutlarını çalıştırarak hello kullanıcı bir yönetici kullanıcı her iki hello kaynak ve hedef abonelikler üzerinde olmalıdır.

#### <a name="azure-portal"></a>Azure portalına

toouse hello bir abonelik tooanother abonelik, Azure portal toomigrate Azure geçiş ad alanlarını bkz [kaynakları tooa yeni kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove abonelikten bir Azure aboneliği tooanother, komutları bir dizi aşağıdaki kullanım hello bir ad alanı. tooexecute bu işlemi hello ad alanı zaten etkin olmalı ve hello PowerShell komutlarını çalıştırarak hello kullanıcı bir yönetici kullanıcı her iki hello kaynak ve hedef abonelikler üzerinde olmalıdır.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Sorun giderme
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>Bazı hello özel durumların nelerdir Azure geçiş API'leri tarafından oluşturulan ve önerilen gerçekleştirebileceğiniz eylemler?
Genel özel durumlar ve önerilen eylemler gerçekleştirebileceğiniz bir açıklaması için bkz: [geçiş özel durumları][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>Paylaşılan erişim imzası nedir ve hangi dilleri kullanabilirim toogenerate imza?
Paylaşılan erişim imzaları (SAS), SHA-256 güvenli karmaları veya URI dayalı bir kimlik doğrulama mekanizmasıdır. Toogenerate düğüm, PHP, Java, C ve C# ' ta, kendi imzaları nasıl görürüm hakkında bilgi için [paylaşılan erişim imzaları ile Service Bus kimlik doğrulaması][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>Bu, olası toowhitelist geçiş uç noktaları mi?
Evet. Merhaba geçiş istemci bağlantıları tam etki alanı adlarını kullanarak toohello Azure geçiş hizmeti sağlar. Müşteriler için bir giriş ekleyebilirsiniz `*.servicebus.windows.net` duvarlarındaki DNS uygulamaları güvenilir listeye almayı destekler.

## <a name="next-steps"></a>Sonraki adımlar
* [Ad alanı oluşturma](relay-create-namespace-portal.md)
* [.NET kullanmaya başlama](relay-hybrid-connections-dotnet-get-started.md)
* [Node kullanmaya başlama](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md