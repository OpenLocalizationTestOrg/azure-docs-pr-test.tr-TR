---
title: bir bulut hizmeti aaaHow tooupdate | Microsoft Docs
description: "Tooupdate bulut Azure hizmetleri nasıl öğrenin. Bir bulut hizmeti üzerinde güncelleştirme tooensure kullanılabilirlik nasıl geçer öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>Nasıl tooupdate bir bulut hizmeti

Kendi rolleri ve konuk işletim sistemi, dahil olmak üzere bir bulut hizmeti güncelleştirme üç adım bir işlemdir. İlk olarak, hello ikili dosyaları ve yapılandırma dosyalarını hello yeni bulut hizmeti veya işletim sistemi sürümü yüklenmelidir. Ardından, Azure hello gereksinimlerine göre hello yeni bulut hizmeti sürümü hello bulut hizmeti için işlem ve ağ kaynakları ayırır. Son olarak, Azure çalışırken yükseltme tooincrementally güncelleştirme hello Kiracı toohello yeni sürümü ya da konuk işletim sistemi, kullanılabilirliği koruyarak gerçekleştirir. Bu makalede bu son adım – yükseltmesinde hello hello ayrıntılarını anlatılmaktadır.

## <a name="update-an-azure-service"></a>Bir Azure hizmetini güncelleştirme
Azure rolü örneklerinizi yükseltme etki alanları (UD) adı verilen mantıksal gruplar düzenler. Yükseltme etki alanları (UD) bir grup olarak güncelleştirilen rol örnekleri mantıksal kümeleridir.  Bulut bir Azure güncelleştirmeleri bir UD, her seferinde diğer UDs toocontinue trafiği hizmet örnekleri sağlayan hizmet.

Merhaba varsayılan yükseltme etki alanlarının sayısı 5'tir. Merhaba hizmetin tanım dosyası (.csdef) hello upgradeDomainCount özniteliği dahil olmak üzere farklı bir yükseltme etki alanlarının sayısını belirtebilirsiniz. Merhaba upgradeDomainCount özniteliği hakkında daha fazla bilgi için bkz: [WebRole şema](https://msdn.microsoft.com/library/azure/gg557553.aspx) veya [örn şema](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Bir veya daha fazla rolün bir yerinde güncelleştirme hizmetinizi gerçekleştirdiğinizde, ait oldukları yükseltme etki alanı toowhich toohello göre rol örnekleri kümesi Azure güncelleştirir. Tüm bunları getirilmesi güncelleştirme onları durdurma belirli bir yükseltme etki alanındaki – hello örneklerinin çevrimiçi – geri azure güncelleştirmeleri sonra hello sonraki etki alanında oturum taşır. Etki alanı yükseltme Hello geçerli çalışan yalnızca hello örnekleri durdurarak, Azure bir güncelleştirme hizmetini çalıştıran hello olabildiğince az etkisi toohello olduğunda emin olur. Daha fazla bilgi için bkz: [nasıl hello güncelleştirme işlemi devam eder](#howanupgradeproceeds) bu makalenin ilerisinde yer.

> [!NOTE]
> While hello koşulları **güncelleştirme** ve **yükseltme** Azure hello bağlamda biraz farklı bir anlama sahip, hello işlemleri ve bu belgedeki hello özelliklerin açıklamaları için birbirinin yerine kullanılabilir.
>
>

Hizmetiniz bir rol, rol güncelleştirilmiş toobe yerinde kapalı kalma süresi olmadan için en az iki örnek tanımlamanız gerekir. Merhaba hizmeti bir rolü yalnızca bir örneği oluşuyorsa, hello yerinde güncelleştirme tamamlanana kadar hizmet kullanılamaz.

Bu konu Azure güncelleştirmeler hakkında bilgi aşağıdaki hello şunları içerir:

* [Hizmet değişikliklerini güncelleştirme sırasında izin verilen](#AllowedChanges)
* [Nasıl bir yükseltme işlemi devam eder](#howanupgradeproceeds)
* [Bir güncelleştirme geri alma](#RollbackofanUpdate)
* [Devam eden bir dağıtımda birden çok mutating işlemleri başlatma](#multiplemutatingoperations)
* [Yükseltme etki alanları arasında rollerin dağıtım](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Hizmet değişikliklerini güncelleştirme sırasında izin verilen
Merhaba aşağıdaki tabloda hello değişiklikleri tooa hizmet güncelleştirme sırasında izin verilen gösterilmektedir:

| Toohosting, hizmetler ve roller izin değişiklikleri | Yerinde güncelleştirme | Hazırlanmış (VIP takas) | Silme ve yeniden Dağıt |
| --- | --- | --- | --- |
| İşletim sistemi sürümü |Evet |Evet |Evet |
| .NET güven düzeyi |Evet |Evet |Evet |
| Sanal makine boyutu<sup>1</sup> |Evet<sup>2</sup> |Evet |Evet |
| Yerel depolama ayarları |Yalnızca artırmak<sup>2</sup> |Evet |Evet |
| Rolleri bir hizmet olarak ekleyip |Evet |Evet |Evet |
| Belirli bir rol örneklerinin sayısını |Evet |Evet |Evet |
| Sayı veya bir hizmet için uç nokta türü |Evet<sup>2</sup> |Hayır |Evet |
| Adları ve yapılandırma ayarlarının değerleri |Evet |Evet |Evet |
| Değerleri (ancak değil adları) yapılandırma ayarları |Evet |Evet |Evet |
| Yeni sertifika Ekle |Evet |Evet |Evet |
| Mevcut sertifikalarını değiştirme |Evet |Evet |Evet |
| Yeni kod dağıtın |Evet |Evet |Evet |

<sup>1</sup> boyutu değişikliği sınırlı toohello alt boyutlarının hello bulut hizmeti için kullanılabilir.

<sup>2</sup> Azure SDK 1.5 gerektirir veya sonraki sürümler.

> [!WARNING]
> Merhaba sanal makine boyutunu değiştirme yerel verileri silecektir.
>
>

Aşağıdaki öğelerindeki hello güncelleştirme sırasında desteklenmez:

* Bir rolü Hello adının değiştirilmesi. Kaldırın ve ardından hello Yeni adla hello rolünü ekleyin.
* Merhaba yükseltme etki alanı sayısı değiştirme.
* Merhaba yerel kaynaklar Hello boyutunu azaltma.

Yerel kaynak hello boyutunu azaltmak gibi tooyour hizmetin tanımı, diğer güncelleştirmeleri yapıyorsanız bir VIP takas güncelleştirmesi yerine gerçekleştirmeniz gerekir. Daha fazla bilgi için bkz: [takas dağıtım](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Nasıl bir yükseltme işlemi devam eder
Tooupdate isteyip istemediğinize karar verebilirsiniz tüm hizmetiniz hello rollerinde veya hello hizmetindeki tek bir rol. Her iki durumda da, yükseltilmekte olan ve toohello ilk yükseltme etki alanına ait her bir rol tüm örneklerini durduruldu, yükseltme ve tekrar çevrimiçi. Yeniden çevrimiçi olduktan sonra hello hello ikinci yükseltme etki alanındaki örnekleri durduruldu, yükseltme ve çevrimiçi duruma geri. Bir bulut hizmeti en çok bir yükseltme aynı anda etkin olabilir. Merhaba yükseltme her zaman hello en son sürümünü hello bulut hizmeti karşı gerçekleştirilir.

Merhaba Aşağıdaki diyagramda tüm hello hizmetindeki hello rollerin yükseltiyorsanız nasıl hello yükseltme işlemi devam eder gösterilmektedir:

![Hizmet yükseltme](media/cloud-services-update-azure-service/IC345879.png "yükseltme hizmeti")

Sonraki Bu diyagramda, yalnızca tek bir rol yükseltiyorsanız nasıl hello güncelleştirme işlemi devam eder gösterilir:

![Yükseltme rol](media/cloud-services-update-azure-service/IC345880.png "yükseltme rolü")  

Cihazın güvenli toowalk hello olduğunda sonraki UD bir otomatik güncelleştirme sırasında hello Azure yapı denetleyicisi hello bulut hizmeti toodetermine hello durumunu düzenli aralıklarla değerlendirir. Bu sistem durumu değerlendirmesi bir rol başına temelinde gerçekleştirilir ve hello en son sürüm (yani zaten gitti UDs örneklerinden) yalnızca örnekleri göz önünde bulundurur. Olduğunu doğrular en az sayıda her rol için rol örneği elde tatmin edici terminal durumuna.

### <a name="role-instance-start-timeout"></a>Rol örneği başlangıç zaman aşımı
Merhaba doku denetleyicisi her rol örneği tooreach Başlatıldı durumuna 30 dakika bekler. Merhaba zaman aşımı süresi aşılırsa, hello doku denetleyicisi toohello sonraki rol örneği taramasını devam eder.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Bulut hizmeti yükseltme sırasında etkisi toodrive verileri

Bir hizmet hello yükseltme toohello şekilde Azure Hizmetleri yükseltme gerçekleştirilirken hizmetinizi gidersiniz aşağı tek örnek toomultiple örnekleri yükseltirken. Merhaba hizmet düzeyi sözleşmesi güvence altına almak hizmet kullanılabilirliği, yalnızca birden fazla örneği ile dağıtılan tooservices geçerlidir. Merhaba aşağıdaki listede her sürücüde hello veri her Azure hizmet yükseltme senaryosu tarafından nasıl etkilendiğini açıklanmaktadır:

|Senaryo|C sürücüsü|D sürücüsü|E sürücüsü|
|--------|-------|-------|-------|
|VM yeniden başlatma|Korunur|Korunur|Korunur|
|Portal yeniden başlatma|Korunur|Korunur|Yok|
|Portal yeniden görüntü oluşturma|Korunur|Yok|Yok|
|Yerinde yükseltme|Korunur|Korunur|Yok|
|Düğüm geçiş|Yok|Yok|Yok|

Merhaba listesinin hello E: sürücü hello rolün kök sürücüsünde temsil eder ve sabit kodlanmış olmamalıdır, unutmayın. Bunun yerine, hello kullanın **RoleRoot %** ortam değişkeni toorepresent hello sürücü.

Tek Örnekli bir hizmeti yükseltirken toominimize hello kapalı kalma süresi, yeni bir çok örnekli hizmet toohello Hazırlama sunucusu dağıtmak ve bir VIP takası gerçekleştirin.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Bir güncelleştirme geri alma
Azure Hizmetleri hello ilk güncelleştirme isteği hello Azure yapı denetleyicisi tarafından kabul edildikten sonra bir hizmete ek işlemleri başlatmak izin vererek güncelleştirme sırasında yönetme esneklik sağlar. Bir geri alma, yalnızca bir güncelleştirme olduğunda (yapılandırma değişikliği) gerçekleştirilebilir veya yükseltmedir hello **devam eden** hello dağıtımda durum. En az bir örnek henüz güncelleştirilmiş toohello yeni sürüm edilmemiş hello hizmetinin var olduğu sürece toobe süren bir güncelleştirme veya yükseltme olarak kabul edilir. tootest geri almaya izin verilip verilmeyeceğini hello değeri tarafından döndürülen hello RollbackAllowed bayrağı denetleyin [alma dağıtım](https://msdn.microsoft.com/library/azure/ee460804.aspx) ve [bulut hizmeti özellik alma](https://msdn.microsoft.com/library/azure/ee460806.aspx) işlemleri tootrue ayarlanır.

> [!NOTE]
> Yalnızca anlamlı toocall geri alma üzerinde kolaylaştırır bir **yerinde** güncelleştirmek veya bir çalışan örneğinin tamamını hizmetinizi diğeriyle VIP takas yükseltmeler içerdiğinden dolayı yükseltin.
>
>

Geri alma devam eden güncelleştirme hello dağıtım etkileri aşağıdaki hello sahiptir:

* Güncelleştirilmiş veya yükseltilmiş toohello yeni sürüm henüz yüklenmiş değil tüm rol örneklerinin güncelleştirilmez veya bu örneklerde hello hedef hello hizmetinin sürümü zaten çalıştığından, yükseltme.
* Hangi zaten güncelleştirilmişse veya yükseltilmiş toohello yeni hello hizmet paketi sürümünü herhangi bir rol örnekleri (\*.cspkg) dosyası ya da hello hizmet yapılandırması (\*.cscfg) dosya (veya her iki dosya) olan döndürülen toohello yükseltme öncesi sürümü Bu dosyalar.

Bu, işlevsel olarak özellikler aşağıdaki hello tarafından sağlanır:

* Merhaba [geri alma güncelleştirme veya yükseltme](https://msdn.microsoft.com/library/azure/hh403977.aspx) bir yapılandırma güncelleştirme çağrılabilir işlemi (çağırarak tetiklenen [dağıtım yapılandırmasını değiştirme](https://msdn.microsoft.com/library/azure/ee460809.aspx)) veya yükseltme (çağırarak tetiklenen [ Yükseltme dağıtımı](https://msdn.microsoft.com/library/azure/ee460793.aspx)) var olduğu sürece en az bir örnek hello hizmetinde toohello yeni sürüm henüz değiştirilmediğinden güncelleştirildi.
* Merhaba hello yanıt gövdesi bir parçası olarak döndürülen kilitli öğe ve hello RollbackAllowed öğenin hello [alma dağıtım](https://msdn.microsoft.com/library/azure/ee460804.aspx) ve [bulut hizmeti özellik alma](https://msdn.microsoft.com/library/azure/ee460806.aspx) işlemleri:

  1. mutating işlemi üzerinde belirli bir dağıtım çağrılabilir olduğunda hello kilitli öğesi toodetect izin verir.
  2. Merhaba RollbackAllowed öğesi toodetect hello olduğunda sağlar [geri alma güncelleştirme veya yükseltme](https://msdn.microsoft.com/library/azure/hh403977.aspx) işlemi üzerinde belirli bir dağıtım çağrılabilir.

  Sipariş tooperform bir geri alma, kilitli hello hem RollbackAllowed öğeleri hello toocheck gerekmez. RollbackAllowed tootrue ayarlandığını tooconfirm soneklerini. Bu yöntemler hello istek üstbilgisi çok ayarlamak kullanarak çağrılan bu öğeleri yalnızca döndürülür "x-ms-version: 2011-10-01" veya sonraki bir sürümü. Sürüm oluşturma üstbilgileri hakkında daha fazla bilgi için bkz: [Hizmet Yönetimi sürüm](https://msdn.microsoft.com/library/azure/gg592580.aspx).

Bazı durumlar vardır geri alma bir güncelleştirme olduğunda veya yükseltme desteklenmiyor, bunlar şu şekildedir:

* Yerel kaynaklar - azalma hello güncelleştirme artar hello yerel kaynakları bir rol için Azure platformu hello durumunda izin vermiyor geri alınıyor.
* Kota sınırlamaları - hello güncelleştirme işlemi artık olabilecek bir ölçek ise yeterli işlem kota toocomplete hello geri alma işlemi vardır. Her Azure aboneliği hello en yüksek toothat abonelik ait tüm barındırılan hizmetler tarafından kullanılan çekirdek sayısı belirtir kendisiyle ilişkili bir kota sahiptir. Verilen güncelleştirmesi işlemin geri alınmasının aboneliğinizi kota sonra koyabilirsiniz, bir geri alma etkin değil.
* Yarış durumu - Hello ilk güncelleştirme tamamladıysa, bir geri alma mümkün değildir.

Ne zaman bir güncelleştirme hello geri alma yararlı olabilecek bir hello kullanıyorsanız örnektir [yükseltme dağıtımı](https://msdn.microsoft.com/library/azure/ee460793.aspx) en önemli bir yerinde yükseltme tooyour Azure barındırılan hizmeti el ile moduna toocontrol hello oranı işlem toplama.

Merhaba yükseltme Hello piyasaya sürme sırasında çağırmanız [yükseltme dağıtımı](https://msdn.microsoft.com/library/azure/ee460793.aspx) el ile modunda ve toowalk yükseltme etki alanlarının başlayın. Merhaba yükseltme izlerken bir noktada, bazı rol örnekleri, inceleyin hello ilk yükseltme etki alanlarında vermiyordu unutmayın, hello çağırabilirsiniz [geri alma güncelleştirme veya yükseltme](https://msdn.microsoft.com/library/azure/hh403977.aspx) hello dağıtım işlemi, henüz yükseltme dokunulmadan hello örnekleri bırakır ve toohello önceki hizmet paketi ve yapılandırma olsaydı geri alma örneklerini yükseltilecektir.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Devam eden bir dağıtımda birden çok mutating işlemleri başlatma
Bazı durumlarda, devam eden bir dağıtım birden çok eşzamanlı mutating işlemleri tooinitiate isteyebilirsiniz. Örneğin, bir hizmet güncelleştirmesi gerçekleştirebilir ve bu güncelleştirmeyi hizmetiniz arasında alınmakta olsa da, toomake bazı değiştirmek istediğiniz, örneğin tooroll geri güncelleştirme Merhaba, farklı bir güncelleştirme uygulamak veya bile hello dağıtımı silin. Hizmet yükseltmesi bir yükseltilen rol örneği toorepeatedly çökmesine neden olan buggy kodu içeriyorsa, bu gerekli olabilir durumu gösterir. Bu durumda, hello Azure yapı denetleyicisi hello yükseltilmiş etki alanındaki örnekleri sayısı yetersiz sağlıklı olduğundan, yükseltme uygulanırken mümkün toomake sürüyor olmaz. Bu durumda başvurulan tooas bir *takılmış dağıtım*. Merhaba güncelleştirme geri veya yeni bir güncelleştirme biri başarısız hello üst uygulama tarafından hello dağıtım sürüklemeniz.

Merhaba ilk istek tooupdate veya yükseltme hello hizmeti hello Azure yapı denetleyicisi tarafından alınan sonra sonraki diziyi işlemleri başlatabilirsiniz. Diğer bir deyişle, başka bir mutating işlemi başlamadan önce hello ilk işlemi toocomplete toowait gerekmez.

Merhaba ilk güncelleştirme devam eden durumdayken ikinci bir güncelleştirme işlemi başlatma benzer toohello geri alma işlemi gerçekleştirir. Merhaba ikinci güncelleştirmeyi otomatik modda ise, hello ilk yükseltme etki alanı hemen yükseltilir, büyük olasılıkla hello çevrimdışı olmasından birden fazla yükseltme etki alanlarından tooinstances baştaki aynı zamanda noktası.

Merhaba diziyi işlem aşağıdaki gibidir: [dağıtım yapılandırmasını değiştirme](https://msdn.microsoft.com/library/azure/ee460809.aspx), [yükseltme dağıtımı](https://msdn.microsoft.com/library/azure/ee460793.aspx), [güncelleştirme dağıtım durumunu](https://msdn.microsoft.com/library/azure/ee460808.aspx), [Sil Dağıtım](https://msdn.microsoft.com/library/azure/ee460815.aspx), ve [geri alma güncelleştirme veya yükseltme](https://msdn.microsoft.com/library/azure/hh403977.aspx).

İki işlem [alma dağıtım](https://msdn.microsoft.com/library/azure/ee460804.aspx) ve [bulut hizmeti özellik alma](https://msdn.microsoft.com/library/azure/ee460806.aspx), incelenmesi toodetermine mutating işlemi üzerinde belirli bir dağıtım çağrılabilir olup olmadığını olabilen hello kilitli bayrağı döndürür.

Merhaba kilitli bayrağı döndüren sipariş toocall hello sürümünde bu yöntemler, istek üstbilgisi çok ayarlamanız gerekir "x-ms-version: 2011-10-01" ya da daha sonra. Sürüm oluşturma üstbilgileri hakkında daha fazla bilgi için bkz: [Hizmet Yönetimi sürüm](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Yükseltme etki alanları arasında rollerin dağıtım
Azure rol örneklerini hello hizmet açıklaması (.csdef) dosyasının bir parçası olarak yapılandırılmış yükseltme etki alanlarının sayısı kümesini arasında eşit olarak dağıtır. Yükseltme etki alanlarının en büyük sayı Hello 20'dir ve hello varsayılan 5'tir. Nasıl toomodify hello hizmet tanımı dosyası hakkında daha fazla bilgi için bkz: [Azure Hizmet tanım Şeması (.csdef dosyası)](cloud-services-model-and-package.md#csdef).

Örneğin, rolünüze on örneği varsa, varsayılan olarak her bir yükseltme etki alanı iki örneklerini içerir. Rolünüze 14 örneği varsa, dört hello yükseltme etki alanlarının üç örneklerini içerir ve iki beşinci bir etki alanı içerir.

Yükseltme etki alanları, sıfır tabanlı bir dizin ile tanımlanır: hello ilk yükseltme etki alanı kimliği 0 ve hello ikinci yükseltme etki alanı varsa bir kimliği 1 ve benzeri.

Merhaba Aşağıdaki diyagramda nasıl iki rolü içeren bir hizmet dağıtılır hello hizmet iki yükseltme etki alanlarının tanımladığında gösterilmektedir. Merhaba hizmeti sekiz hello web rolü örneklerini ve hello çalışan rolü dokuz örneklerini çalışıyor.

![Yükseltme etki alanlarının dağıtım](media/cloud-services-update-azure-service/IC345533.png "yükseltme etki alanlarının dağılımı")

> [!NOTE]
> Azure örnekleri yükseltme etki alanları arasında nasıl ayrıldığını denetleyen unutmayın. Hangi örnekleri toowhich etki alanı ayrılacağını olası toospecify değil.
>
>

## <a name="next-steps"></a>Sonraki adımlar
[TooManage Cloud Services nasıl](cloud-services-how-to-manage.md)  
[TooMonitor Cloud Services nasıl](cloud-services-how-to-monitor.md)  
[TooConfigure Cloud Services nasıl](cloud-services-how-to-configure.md)  
