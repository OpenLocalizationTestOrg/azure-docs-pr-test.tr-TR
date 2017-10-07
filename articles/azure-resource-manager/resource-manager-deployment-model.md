---
title: "aaaResource Manager ve klasik dağıtımı | Microsoft Docs"
description: "Merhaba hello Resource Manager dağıtım modeli ve klasik hello (veya Hizmet Yönetimi) arasındaki farklar dağıtım modelini açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Azure Resource Manager ve klasik dağıtım: Merhaba kaynaklarınızın durumunu ve dağıtım modellerini anlama
Bu konuda, Azure Resource Manager ve klasik dağıtım modeli, kaynaklarınızın hello durumu hakkında bilgi edinin ve kaynaklarınızı biri veya hello diğer dağıtılan neden. Merhaba Resource Manager ve klasik dağıtım modellerine dağıtma ve yönetme Azure çözümlerinizi iki farklı şekilde temsil eder. İki farklı API kümesi bunlarla çalışmak ve dağıtılan hello kaynakları önemli farklılıklar içerebilir. Merhaba iki modeli birbirleri ile tamamen uyumlu değildir. Bu konu bu farkları açıklamaktadır.

toosimplify hello dağıtımı ve kaynak yönetimi, Microsoft tüm yeni kaynaklar için Kaynak Yöneticisi'ni kullanmanızı önerir. Mümkünse, Microsoft, var olan kaynakların Resource Manager aracılığıyla dağıtmanız önerir.

Yeni tooResource Yöneticisi iseniz, hello tanımlanan toofirst gözden geçirme hello terminolojisi isteyebilirsiniz [Azure Resource Manager'a genel bakış](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Merhaba dağıtım modellerinin geçmişi
Azure başlangıçta yalnızca hello Klasik dağıtım modeli sağlanan. Bu modelde, bağımsız olarak her bir kaynağın var; hiçbir yolu yoktu toogroup ilgili kaynakları birlikte. Bunun yerine, çözüm ya da uygulama yapılan hangi kaynaklara izlemek ve toomanage unutmayın toomanually vardı koordineli bir yaklaşım bunları. toodeploy bir çözüm, hello Klasik portal üzerinden ayrı ayrı her bir kaynağın veya tüm hello kaynakları hello doğru sırayla dağıtılan bir komut dosyası oluşturmak tooeither vardı. toodelete bir çözüm, sizin toodelete her bir kaynağın ayrı ayrı vardı. Kolayca uygulanır ve ilgili kaynaklar için erişim denetimi ilkeleri güncelleştirin. Son olarak, bunları yardımcı koşullarla kaynaklarınızı izlemek ve faturalama yönetmek etiketleri tooresources toolabel uygulanamadı.

2014'te Azure Kaynak Yöneticisi, bir kaynak grubu hello kavramı eklenen kullanıma sunuldu. Bir kaynak grubu, ortak bir yaşam döngüsü paylaşmak kaynaklar için bir kapsayıcıdır. Merhaba Resource Manager dağıtım modeli çeşitli avantajlar sunar:

* Dağıtmak, yönetmek ve bir Grup yerine bu hizmetleri ayrı ayrı ele çözümünüz için tüm hello hizmetlerini izleyin.
* Art arda çözümünüzü yaşam döngüsü dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması da size güven verir.
* Erişim denetimi tooall kaynakları kaynak grubunuzdaki uygulayabilirsiniz ve yeni kaynaklar toohello kaynak grubuna eklendiğinde bu ilkeleri otomatik olarak uygulanır.
* Etiketleri uygulayabilirsiniz tooresources toologically aboneliğinizdeki tüm hello kaynakları düzenleyin.
* JavaScript nesne gösterimi (JSON) toodefine hello altyapısı çözümünüz için kullanabilirsiniz. Merhaba JSON dosyası Resource Manager şablonu olarak bilinir.
* Merhaba doğru sırayla dağıtılmalarını sağlamak için kaynaklarınız arasındaki hello bağımlılıkları tanımlayabilirsiniz.

Resource Manager eklendiğinde tüm kaynakları firmalarda geriye dönük toodefault kaynak grupları eklendi. Bir kaynak şimdi Klasik dağıtım aracılığıyla oluşturursanız, bu kaynak grubu dağıtım sırasında belirtmedi olsa bile hello kaynak bu hizmet için varsayılan bir kaynak grubu içinde otomatik olarak oluşturulur. Ancak, yalnızca bir kaynak grubu içinde varolan hello kaynak dönüştürülmüş toohello Resource Manager modeli bırakıldı anlamına gelmez. Biz, her hizmetin hello iki dağıtım modeli hello sonraki bölümde nasıl işlediğini adresindeki göreceğiz. 

## <a name="understand-support-for-hello-models"></a>Merhaba modelleri için destek anlama
Hangi dağıtım modeli toouse kaynaklarınız için karar verirken, üç senaryoları toobe farkında vardır:

1. Merhaba hizmeti Kaynak Yöneticisi'ni destekler ve yalnızca tek bir türü sağlar.
2. Merhaba hizmeti Kaynak Yöneticisi'ni destekler, ancak iki tür - sağlar bir Resource Manager ve klasik için. Bu senaryo yalnızca toovirtual makineler, depolama hesapları ve sanal ağlar için geçerlidir.
3. Merhaba hizmeti Resource Manager desteklemiyor.

toodiscover Kaynak Yöneticisi, bir hizmet destekleyip desteklemediğini görmek [kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).

Merhaba hizmet toouse istediğiniz Resource Manager desteklemiyorsa, Klasik dağıtım kullanarak devam etmeniz gerekir.

Merhaba hizmet Resource Manager destekliyorsa ve **değil** bir sanal makine, depolama hesabı ya da sanal ağ herhangi zorluklar Kaynak Yöneticisi'ni kullanabilirsiniz.

Merhaba kaynak Klasik dağıtım oluşturduysanız, sanal makineler, depolama hesapları ve sanal ağlar için toooperate üzerinde Klasik işlemleri aracılığıyla devam etmeniz gerekir. Merhaba sanal makine, depolama hesabı ya da sanal ağ Resource Manager dağıtım oluşturulmuşsa, Resource Manager işlemleri kullanarak devam etmeniz gerekir. Aboneliğinizi Resource Manager ve klasik dağıtımı oluşturulan kaynakları bir karışımını içeriyorsa bu ayrım kafa karıştırıcı elde edebilirsiniz. Hello kaynakları desteklemez çünkü bu kaynakların bileşimini beklenmeyen sonuçlar oluşturabilirsiniz hello aynı işlemleri.

Bazı durumlarda, bir Kaynak Yöneticisi komut Klasik dağıtım oluşturulan bir kaynak hakkında bilgi alabilir veya bir Klasik kaynak tooanother kaynak grubu taşıma gibi bir yönetim görevi gerçekleştirebilirsiniz. Ancak, bu gibi durumlarda hello türü Resource Manager işlemlerini destekleyen hello izlenim vermemelisiniz. Örneğin, Klasik dağıtım ile oluşturulmuş bir sanal makine içeren bir kaynak grubu olduğunu varsayalım. Resource Manager PowerShell komutunu aşağıdaki hello çalıştırırsanız:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Merhaba sanal makine döndürür:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Ancak, Resource Manager cmdlet'i hello **Get-AzureRmVM** yalnızca Resource Manager aracılığıyla dağıtılan sanal makineleri döndürür. Merhaba aşağıdaki komutu Klasik dağıtım oluşturulan hello sanal makinenin döndürmez.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Yalnızca Kaynak Yöneticisi desteği etiketleri oluşturulan kaynakları. Etiketler tooclassic kaynakları uygulanamıyor.

## <a name="resource-manager-characteristics"></a>Kaynak Yöneticisi özellikleri
Merhaba iki anlamak toohelp modeller, şimdi Resource Manager türleri hello özelliklerini gözden geçirin:

* Merhaba oluşturulan [Azure portal](https://portal.azure.com/).
  
     ![Azure portalına](./media/resource-manager-deployment-model/portal.png)
  
     İşlem, depolama ve ağ kaynakları için Resource Manager veya Klasik dağıtım kullanarak hello seçeneğiniz vardır. Seçin **Resource Manager**.
  
     ![Resource Manager dağıtımı](./media/resource-manager-deployment-model/select-resource-manager.png)
* Merhaba Resource Manager sürümü hello Azure PowerShell cmdlet'leri ile oluşturulur. Bu komutlar hello biçimine sahip *fiili AzureRmNoun*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Merhaba oluşturulan [Azure Resource Manager REST API'si](https://docs.microsoft.com/rest/api/resources/) REST işlemleri için.
* Azure CLI komutlarını hello Çalıştır aracılığıyla oluşturulan **arm** modu.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* Merhaba kaynak türü içermez **(Klasik)** hello adı. Merhaba aşağıdaki resimde gösterilmiştir hello türü olarak **depolama hesabı**.
  
    ![web uygulamasına](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Klasik dağıtım özellikleri
Merhaba hizmet yönetimi modeli olarak hello Klasik dağıtım modeli de biliyorsunuz.

Merhaba Klasik dağıtım modeli paylaşımı hello özellikleri aşağıdaki oluşturulan kaynakları:

* Merhaba oluşturulan [Klasik portal](https://manage.windowsazure.com)
  
     ![Klasik portal](./media/resource-manager-deployment-model/classic-portal.png)
  
     Veya, Azure portal hello ve belirttiğiniz **Klasik** dağıtımı (için işlem, depolama ve ağ).
  
     ![Klasik dağıtım](./media/resource-manager-deployment-model/select-classic.png)
* Hello Service Management sürümünü hello Azure PowerShell cmdlet'leri oluşturulur. Bu komut adları hello biçimine sahip *fiili AzureNoun*.

  ```powershell
  New-AzureVM
  ```

* Merhaba oluşturulan [Hizmet Yönetimi REST API'si](https://msdn.microsoft.com/library/azure/ee460799.aspx) REST işlemleri için.
* Azure CLI komutları çalıştırmak aracılığıyla oluşturulan **asm** modu.

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* Merhaba kaynak türünü içeren **(Klasik)** hello adı. Merhaba aşağıdaki resimde gösterilmiştir hello türü olarak **depolama hesabı (Klasik)**.
  
    ![Klasik türü](./media/resource-manager-deployment-model/classic-type.png)

Klasik dağıtım oluşturulan hello Azure portal toomanage kaynakları kullanabilir.

## <a name="changes-for-compute-network-and-storage"></a>İşlem, ağ ve depolama için değişiklikleri
Merhaba Aşağıdaki diyagramda Resource Manager aracılığıyla dağıtılan işlem, ağ ve depolama kaynakları görüntüler.

![Resource Manager mimarisi](./media/resource-manager-deployment-model/arm_arch3.png)

Merhaba kaynakları ilişkileri aşağıdaki hello dikkat edin:

* Bir kaynak grubu içindeki tüm hello kaynağı yok.
* Merhaba sanal makinesi, disklerini blob depolama (gerekli) hello depolama kaynak sağlayıcısı toostore içinde tanımlanan bir belirli bir depolama hesabına bağlıdır.
* Merhaba sanal makine (gerekli) hello ağ kaynak sağlayıcısı ve kullanılabilirlik hello işlem kaynak Sağlayıcısı'nda tanımlanan (isteğe bağlı) kümesi içinde tanımlanan belirli bir NIC başvurur.
* Merhaba NIC başvuruları hello sanal makinenin IP adresi hello sanal makine (gerekli) ve tooa ağ güvenlik grubu (isteğe bağlı) için sanal ağ hello hello alt ağdan (gerekli) atanır.
* Merhaba alt ağ bir sanal ağ içinde ağ güvenlik grubu (isteğe bağlı) başvuruyor.
* Merhaba yük dengeleyici örneği hello arka uç havuzu hello (isteğe bağlı) bir sanal makinenin NIC içeren IP adreslerinin başvuruyor ve bir yük dengeleyici genel veya özel IP adresi (isteğe bağlı) başvuruyor.

Merhaba bileşenleri ve klasik dağıtımı için ilişkilerini şunlardır:

![Klasik mimarisi](./media/resource-manager-deployment-model/arm_arch1.png)

bir sanal makineyi barındırmak için Klasik çözüm hello içerir:

* Sanal makineleri (işlem) barındırmak için bir kapsayıcı olarak davranır gerekli bulut hizmeti. Sanal makineleri otomatik olarak bir ağ arabirimi kartı (NIC) ile sağlanan ve Azure tarafından bir IP adresi atanır. Ayrıca, bir dış yük dengeleyici örneği, bir ortak IP adresi ve varsayılan uç noktaları tooallow Uzak Masaüstü ile uzaktan PowerShell Windows tabanlı sanal makineleri için hem de güvenli Kabuk (SSH) trafiği için hello bulut hizmeti içeren Linux tabanlı sanal makineler.
* Depoları hello işletim sistemi, geçici ve ek veri diskleri (Depolama) dahil olmak üzere sanal makine için VHD'ler hello gerekli depolama hesabı.
* Görevi gören bir alt ağlı yapısı oluşturun ve hello alt ağ üzerinde hangi hello sanal makinenin bulunduğu atamak ek bir kapsayıcı, isteğe bağlı bir sanal ağ (ağ).

Aşağıdaki tablonun hello işlem, ağ ve depolama kaynak sağlayıcıları nasıl etkileşim içinde değişiklikleri açıklar:

| Öğe | Klasik | Resource Manager |
| --- | --- | --- |
| Virtual Machines için Bulut Hizmeti |Bulut hizmeti kullanılabilirlik hello platform ve Yük Dengeleme gerekli hello sanal makineleri barındırmak için bir kapsayıcıydı. |Bulut hizmeti artık hello yeni modeli kullanarak bir sanal makine oluşturmak için gereken nesne değildir. |
| Sanal Ağlar |Bir sanal ağ hello sanal makine için isteğe bağlıdır. Dahil edilmişse, Resource Manager ile Merhaba sanal ağ dağıtılamıyor. |Sanal makine Resource Manager ile dağıtılan bir sanal ağ gerektirir. |
| Depolama Hesapları |Merhaba sanal makine hello VHD'ler hello işletim sistemi, geçici ve ek veri disklerinin depolayan bir depolama hesabı gerektirir. |Merhaba sanal makine, disklerini blob depolamada bir depolama hesabı toostore gerektirir. |
| Kullanılabilirlik Kümeleri |Kullanılabilirlik toohello platformu belirtilen yapılandırarak hello sanal makineler üzerinde aynı "AvailabilitySetName" Merhaba. Merhaba en fazla hata etki alanlarının sayısı 2 '. |Kullanılabilirlik kümesi, Microsoft.Compute Sağlayıcısı tarafından sağlanan bir kaynaktır. Yüksek kullanılabilirlik gerektiren sanal makinelerde hello kullanılabilirlik kümesi eklenmesi gerekir. Merhaba hata etki alanlarının en yüksek sayısı artık 3'tür. |
| Benzeşim Grupları |Benzeşim Grupları Sanal Ağlar oluşturmak için gerekliydi. Ancak, bölgesel sanal ağlar hello sunulmasıyla, artık gerekli değil. |toosimplify, hello benzeşim grupları kavramı Azure Resource Manager aracılığıyla sunulan API'leri hello mevcut değildir. |
| Yük Dengeleme |Bir bulut hizmeti oluşturulması dağıtılan sanal makineleri hello için örtük yük dengeleyici sağlar. |Merhaba yük dengeleyici hello Microsoft.Network sağlayıcısı tarafından sunulan bir kaynaktır. Merhaba toobe yükü dengelenmiş gereken sanal makineleri Hello birincil ağ arabirimi hello yük dengeleyiciye baş vurmalıdır. Yük Dengeleyiciler dahili ve harici olabilir. Bir yük dengeleyici örneği hello arka uç havuzu hello (isteğe bağlı) bir sanal makinenin NIC içeren IP adreslerinin başvuruyor ve bir yük dengeleyici genel veya özel IP adresi (isteğe bağlı) başvuruyor. [Daha fazla bilgi edinin.](../virtual-network/resource-groups-networking.md) |
| Sanal IP Adresi |Tooa bulut hizmeti bir VM eklendiğinde, cloud Services varsayılan VIP'i (sanal IP adresi) alın. Merhaba sanal IP adresi hello örtük yük dengeleyici ile ilişkili hello adresidir. |Genel IP adresi hello Microsoft.Network sağlayıcısı tarafından sunulan bir kaynaktır. Genel IP Adresi Statik (Ayrılmış) veya Dinamik olabilir. Dinamik genel IP'ler tooa yük dengeleyici atanabilir. Genel IP’ler Güvenlik Grupları kullanılarak güvenli hale getirilebilir. |
| Ayrılmış IP Adresi |Azure ve IP adresi hello bir bulut hizmeti tooensure ile Yapışkan ilişkilendirme bir IP adresi ayırabilirsiniz. |Genel IP adresi oluşturulabilir "Statik" modunda ve bunu bir "ayrılmış IP adresi" aynı özelliği sunar hello. Statik genel IP'ler yalnızca tooa yük dengeleyici şu anda atanabilir. |
| Genel IP Adresi (PIP) / VM |Genel IP adresleri de doğrudan ilişkili tooa VM olabilir. |Genel IP adresi hello Microsoft.Network sağlayıcısı tarafından sunulan bir kaynaktır. Genel IP Adresi Statik (Ayrılmış) veya Dinamik olabilir. Ancak, yalnızca dinamik genel IP'ler şu anda atanmış tooa ağ arabirimi tooget bir genel IP VM başına olabilir. |
| Uç Noktalar |Bir sanal makine toobe yapılandırılmış giriş uç noktaları gerekli toobe belirli bağlantı noktaları bağlantısının açık. Giriş uç noktaları ayarlanarak yapılır toovirtual makinelere bağlanmanın yaygın modlarında hello biri. |Yük Dengeleyici gelen NAT kuralları yapılandırılabilir tooachieve hello toohello sanal makinelerini bağlamak için belirli bağlantı noktalarındaki uç noktaları etkinleştirme aynı özellik. |
| DNS Adı |Bulut hizmeti örtük bir genel benzersiz DNS Adı almalıdır. Örneğin: `mycoffeeshop.cloudapp.net`. |DNS Adları, Genel IP Adresi kaynağında belirtilebilen isteğe bağlı parametrelerdir. Merhaba hello aşağıdakileri FQDN'sidir biçimi - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Ağ Arabirimleri |Birincil ve İkincil Ağ Arabirimi ve özellikleri Sanal makinenin ağ yapılandırması olarak tanımlanmıştı. |Ağ Arabirimi, Microsoft.Network Sağlayıcısı tarafından sunulan bir kaynaktır. Ağ arabirimi değil hello Hello yaşam döngüsü tooa sanal makine bağlıdır. (Gerekli) hello sanal makinenin atanan IP adresi hello alt ağı hello sanal ağın hello sanal makine (gerekli) ve tooa ağ güvenlik grubu (isteğe bağlı) başvuruyor. |

sanal ağlar farklı dağıtım modelinden bağlanma hakkında toolearn bkz [hello Portalı'nda farklı dağıtım modelinden sanal ağlara bağlanabilir](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Klasik tooResource Yöneticisi geçirme
Hazır toomigrate olup olmadığını Klasik dağıtım tooResource Yöneticisi dağıtım kaynaklarınızdan bakın:

1. [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Klasik tooAzure Resource Manager Iaas kaynaklardan desteklenen platform geçişi](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Iaas kaynaklarına Klasik tooAzure Resource Manager Azure PowerShell kullanarak geçirme](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Azure CLI kullanarak Klasik tooAzure Resource Manager Iaas kaynaklarını geçirme](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Sık Sorulan Sorular
**Klasik dağıtım kullanılarak oluşturulan bir sanal ağ içinde Azure Resource Manager toodeploy kullanarak bir sanal makine oluşturabilir miyim?**

Bu işlem desteklenmiyor. Klasik dağıtım kullanılarak oluşturulmuş bir sanal ağa, Azure Resource Manager toodeploy bir sanal makine kullanamazsınız.

**Hello Azure Hizmet Yönetim API'leri kullanılarak oluşturulmuş kullanıcı görüntüsünden hello kullanarak bir sanal makine Azure Resource Manager oluşturabilirim?**

Bu işlem desteklenmiyor. Ancak, hello Hizmet Yönetim API'leri kullanılarak oluşturulmuş bir depolama hesabından hello VHD dosyaları kopyalayın ve Azure Resource Manager aracılığıyla oluşturulan tooa yeni hesabı ekleyin.

**Aboneliğimi hello kotasının hello etkisini nedir?**

Merhaba kotaları hello sanal makineler, sanal ağlar ve Azure Resource Manager hello oluşturulan depolama hesapları için diğer kota ayrıdır. Yeni API'leri kullanarak her abonelik alır kotaları toocreate hello kaynakları hello. Daha fazla bilgiyi hello ek Kotalar hakkında [burada](../azure-subscription-service-limits.md).

**Sanal makineler, sanal ağlar ve depolama hesaplarını hello Resource Manager API'leri aracılığıyla sağlama için otomatik betiklerimi toouse devam edebilir mi?**

Tüm hello otomasyon ve derlediğiniz betikleri hello mevcut sanal makineler, sanal ağlar hello Azure hizmet yönetimi modu altında oluşturulan toowork devam eder. Ancak, hello betikleri hello hello Resource Manager moduna aracılığıyla aynı kaynakların oluşturulmasında toobe güncelleştirilmiş toouse hello yeni sahiptir.

**Azure Resource Manager şablonları örneklerini nerede bulabilirim?**

Başlangıç şablonu kapsamlı bir kümesini bulunabilir [Azure Resource Manager hızlı başlangıç şablonları](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Sonraki adımlar
* bir sanal makine, depolama hesabı ve sanal ağ, bkz: tanımlayan şablonu hello oluşturulmasını aracılığıyla toowalk [Resource Manager şablonu Kılavuzu](resource-manager-template-walkthrough.md).
* bir şablonu dağıtmak için toosee hello komutlarını görmek [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

