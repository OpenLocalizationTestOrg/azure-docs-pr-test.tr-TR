---
title: "aaaMove, Azure kaynaklarını toonew abonelik veya kaynak grubu | Microsoft Docs"
description: "Azure Resource Manager toomove kaynakları tooa yeni kaynak grubu veya abonelik kullanın."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Kaynakları toonew kaynak grubuna veya aboneliğe taşıma
Bu konu, nasıl toomove kaynakları tooeither yeni bir abonelik veya yeni bir kaynak grubunda hello gösterir. aynı abonelik. Merhaba portal, PowerShell, Azure CLI veya hello REST API toomove kaynak kullanabilirsiniz. Merhaba taşıma bu konudaki tüm Yardım Azure desteği olmadan kullanılabilir tooyou işlemleridir.

Kaynaklar taşınırken hello kaynak grubu ve hello hedef grubu hello işlemi sırasında kilitlenir. Yazma ve silme işlemleri hello taşıma işlemi tamamlanana kadar hello kaynak gruplarında engellenir. Bu kilit ekleyemez, güncelleştirme veya hello kaynak gruplarındaki kaynakları silin, ancak hello kaynakları dondurulmuş gelmez anlamına gelir. Örneğin, bir SQL Server ve kendi veritabanı tooa yeni kaynak grubu taşırsanız, hello veritabanı kullanan bir uygulama kapalı kalma süresi karşılaşır. Bunu hala okuyabilir ve toohello veritabanı yazma.

Merhaba kaynak hello konumunu değiştiremezsiniz. Bir kaynak taşıma yalnızca bu tooa yeni kaynak grubu taşınır. Merhaba yeni kaynak grubu farklı bir konum olabilir, ancak hello kaynak hello konumunu değiştirmez.

> [!NOTE]
> Bu makalede, mevcut Azure içindeki toomove kaynakların nasıl önerme hesap açıklanmaktadır. Azure hesabınızda (Kullandıkça Öde toopre-ödeme yükseltme gibi), mevcut kaynaklarla toowork devam ederken sunumu gerçekten toochange istiyorsanız bkz [Azure aboneliği tooanother teklifiniz geçiş](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Kaynakları geçmeden önce denetim listesi
Bir kaynak taşımadan önce bazı önemli adımlar tooperform vardır. Bu koşulları doğrulayarak hataları önleyebilirsiniz.

1. Merhaba kaynak ve hedef abonelikler hello içinde aynı bulunmalıdır [Azure Active Directory Kiracı](../active-directory/active-directory-howto-tenant.md). Her iki aboneliğin sahip Merhaba, aynı toocheck Kiracı kimliği, Azure PowerShell veya Azure CLI kullanın.

  Azure PowerShell için kullanın:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Azure CLI 2.0 için kullanın:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Merhaba kimlikleri için Kiracı varsa hello kaynak ve hedef abonelikler olmayan aynı hello toochange hello dizin hello abonelik için deneyebilirsiniz. Ancak, bu seçenek yalnızca kullanılabilir tooService bir Microsoft hesabıyla (Kurumsal bir hesap değil) oturum açmış yöneticileri içindir. Başlangıç dizini, toohello günlüğünde değiştirme tooattempt [Klasik portal](https://manage.windowsazure.com/)seçip **ayarları**ve hello abonelik seçin. Merhaba, **dizini Düzenle** simge mevcut ise, toochange seçin hello ilişkili Azure Active Directory.

  ![dizini Düzenle](./media/resource-group-move-resources/edit-directory.png)

  Bu simge kullanılabilir durumda değilse, desteği toomove hello kaynakları tooa yeni Kiracı başvurmanız gerekir.

2. Merhaba hizmetini hello özelliği toomove kaynakları etkinleştirmeniz gerekir. Bu konu, taşıma kaynakları hangi hizmetlerin etkinleştirmek ve hangi hizmetlerin taşıma kaynakları etkinleştirmeyin listeler.
3. Merhaba hedef abonelik taşınan hello kaynağının hello kaynak sağlayıcısı için kayıtlı olması gerekir. Bu hello bildiren bir hata alırsanız, **kaynak türü için abonelik kayıtlı değil**. Kaynak tooa yeni bir abonelik taşırken bu sorunla karşılaşabilir, ancak bu abonelik hiçbir zaman bu kaynak türü ile kullanıldı. toolearn nasıl toocheck hello kayıt durumunu ve kaynak sağlayıcıları kaydetme bkz [kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Toocall desteği
Bu konuda gösterilen hello Self Servis işlemleri üzerinden en fazla kaynak taşıyabilirsiniz. Merhaba Self Servis işlemleri için kullanın:

* Resource Manager kaynaklarını taşıma
* Toohello göre Klasik kaynakları taşımak [Klasik dağıtım kısıtlamaları](#classic-deployment-limitations).

Gerektiğinde desteğini arayın:

* Kaynakları tooa yeni Azure hesabı (ve Azure Active Directory kiracısı) taşıyın.
* Klasik kaynakları taşımak ancak hello kısıtlamalarla sorunu yaşıyor.

## <a name="services-that-enable-move"></a>Taşıma Etkinleştirme Hizmetleri
Şimdilik, taşıma tooboth yeni bir kaynak grubu ve abonelik etkinleştirmek hello hizmetler şunlardır:

* API Management
* App Service uygulamalarının (web uygulamaları) - bkz [App Service sınırlamalar](#app-service-limitations)
* Application Insights
* Otomasyon
* Batch
* Bing Haritalar
* CDN
* Bulut Hizmetleri - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)
* Bilişsel hizmetler
* Content Moderator
* Veri Kataloğu
* Data Factory
* Data Lake Analytics
* Data Lake Store
* DNS
* Azure Cosmos DB
* Event Hubs
* Bkz: Hdınsight kümeleri - [Hdınsight sınırlamaları](#hdinsight-limitations)
* IOT hub'ları
* Anahtar Kasası
* Yük Dengeleyici
* Logic Apps
* Machine Learning
* Media Services
* Mobile Engagement
* Notification Hubs
* Operasyonel Öngörüler
* Operations Management
* Power BI
* Redis Önbelleği
* Scheduler
* Arama
* Sunucu Yönetimi
* Service Bus
* Service Fabric
* Depolama
* Depolama (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)
* Akış analizi - Stream Analytics işleri de çalıştırırken taşınamaz durumu.
* SQL veritabanı sunucusuna - hello veritabanı ve sunucu bulunmalıdır hello aynı kaynak grubu. Bir SQL server taşıdığınızda, tüm veritabanlarını da taşınır.
* Traffic Manager
* Virtual Machines
* Anahtar kasası - taşıma toonew kaynak grubu aynı abonelik içinde depolanan sertifika sanal makinelerle etkindir, ancak çapraz abonelik taşıma etkin değil.
* Sanal makineler (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)
* Sanal Makine Ölçek Kümeleri
* VNet eşlemesi devre dışı bırakılmış kadar sanal ağlar - şu anda, eşlenmiş bir sanal ağ taşınamaz. Bir kez devre dışı, sanal ağ başarıyla taşınabilmesi hello ve hello VNet eşlemesi etkinleştirilebilir. Ayrıca, kaynak Gezinti bağlantıları olan herhangi bir alt ağ Hello sanal ağ içeriyorsa, bir sanal ağ taşınan tooa farklı bir abonelik olamaz. Örneğin, bu alt ağ Microsoft.Cache redis kaynak dağıtıldığında bir sanal ağ alt kaynak Gezinti bağlantısı vardır.
* VPN Gateway


## <a name="services-that-do-not-enable-move"></a>Taşıma etkinleştirmeyin Hizmetleri
şu anda bir kaynak taşıma etkinleştirmeyin hello hizmetler şunlardır:

* AD etki alanı Hizmetleri
* AD karma sistem durumu hizmeti
* Application Gateway
* Yönetilen bir diske sahip sanal makinelerle kullanılabilirlik kümeleri
* BizTalk Services
* Kapsayıcı Hizmeti
* Express Route
* DevTest Labs - taşıma toonew kaynak grubu aynı abonelikte etkindir, ancak abonelik taşıma etkin değil.
* Dynamics LCS
* Yönetilen disklerden oluşturulan görüntüler
* Yönetilen Diskler
* Yönetilen uygulamalar
* Kurtarma Hizmetleri kasası - ile ilişkili değil hello işlem, ağ ve depolama kaynakları taşıma kurtarma hizmetleri de hello yapmak kasa için bkz: [kurtarma Hizmetleri sınırlamaları](#recovery-services-limitations).
* Güvenlik
* Yönetilen disklerden oluşturulan anlık görüntüler
* StorSimple cihaz Yöneticisi
* Yönetilen bir diske sahip sanal makineler
* Bkz: Sanal ağları (Klasik) - [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)
* Market kaynaklardan - oluşturulan sanal makineleri abonelikler arasında taşınamaz. Merhaba geçerli abonelikte sağlaması kaldırılıyor. sağlaması ve yeniden hello yeni abonelikte dağıtılmış toobe kaynak gerekiyor

## <a name="app-service-limitations"></a>App Service sınırlamalar
Uygulama hizmeti uygulamaları ile çalışırken, yalnızca bir uygulama hizmeti planı taşınamıyor. toomove App Service uygulamalarının Seçenekleriniz şunlardır:

* Merhaba uygulama hizmeti planı ve diğer tüm uygulama hizmeti kaynakları App Service kaynakları zaten sahip olmayan bu kaynak grubu tooa yeni kaynak grubu içinde taşıyın. Uygulama hizmeti kaynakları bile taşımalısınız anlamına gelir hello bu gereksinim, uygulama hizmeti planı hello ile ilişkili değildir.
* Hello uygulamaları tooa farklı bir kaynak grubu taşıma, ancak hello özgün kaynak grubundaki tüm uygulama hizmeti planları tutun.

Merhaba uygulama hizmeti planı içinde tooreside gerekmez hello hello app hello uygulama toofunction için aynı kaynak grubunda doğru.

Örneğin, kaynak grubunuz varsa:

* **Web-a** ile ilişkili **planı-a**
* **Web b** ile ilişkili **planı b**

Seçenekleriniz şunlardır:

* Taşıma **web-a**, **planı-a**, **web-b**, ve **planı b**
* Taşıma **web-a** ve **web-b**
* Taşıma **web-a**
* Taşıma **web-b**

Diğer tüm birleşimler, bir uygulama hizmeti planı (uygulama hizmeti kaynak türlü) taşırken bırakılamaz arkasındaki bir kaynak türü bırakarak içerir.

Web uygulamanızın farklı bir kaynak grubu, uygulama hizmeti planı daha bulunur, ancak her iki tooa yeni kaynak grubu toomove istediğiniz iki adımda hello taşıma gerçekleştirmeniz gerekir. Örneğin:

* **Web-a** bulunan **web grubu**
* **planı bir** bulunan **planı Grup**
* İstediğiniz **web-a** ve **planı-a** tooreside içinde **birleştirilmiş Grup**

Bu taşıma hello dizisi aşağıdaki iki ayrı taşıma işlemleri tooaccomplish:

1. Merhaba taşıma **web-a** çok**planı Grup**
2. Taşıma **web-a** ve **planı-a** çok**Birleştirilmiş grup**.

Bir uygulama hizmet sertifikası tooa yeni kaynak grubu veya abonelik sorunları olmadan taşıyabilirsiniz. Ancak, web uygulamanızı harici olarak satın alınan ve toohello uygulamanın karşıya bir SSL sertifikası içeriyorsa, taşıma hello web uygulaması önce hello sertifika silmeniz gerekir. Örneğin, aşağıdaki adımları hello gerçekleştirebilirsiniz:

1. Merhaba karşıya sertifika hello web uygulamasından silme
2. Taşıma hello web uygulaması
3. Merhaba sertifika toohello web uygulamasını yükleme

## <a name="recovery-services-limitations"></a>Kurtarma Hizmetleri kısıtlamaları
Taşıma ağ, depolama için etkin değil veya işlem kaynakları Azure Site Recovery ile olağanüstü durum kurtarma yukarı tooset kullanılır.

Örneğin, şirket içi makineler tooa depolama hesabınız (Storage1) çoğaltmayı ayarlama ayarladığınız düşünün ve sonra Yük devretme tooAzure tooa sanal ağ (Network1) bir sanal makineye (VM1) bağlı olarak yukarı korumalı hello makine toocome istiyor. Bu Azure kaynakları - Storage1, VM1, hiçbirini taşıyamazsınız ve Network1 - arasında kaynak grupları hello aynı abonelik veya abonelikler arasında.

## <a name="hdinsight-limitations"></a>Hdınsight sınırlamaları

Hdınsight kümeleri tooa yeni abonelik veya kaynak grubu taşıyabilirsiniz. Ancak, abonelikleri hello kaynakları bağlantılı toohello Hdınsight kümesi (örneğin, hello sanal ağ, NIC veya yük dengeleyici) ağ üzerinden taşınamıyor. Ayrıca, tooa yeni kaynak grubu ekli tooa sanal makine hello küme için bir NIC taşınamıyor.

Bir Hdınsight kümesi tooa yeni abonelik taşırken, diğer kaynakları (gibi hello depolama hesabı) taşıyın. Ardından, hello Hdınsight kümesi tek başına taşıyın.

## <a name="classic-deployment-limitations"></a>Klasik dağıtım sınırlamaları
Merhaba hello Klasik modeli aracılığıyla dağıtılan kaynakları taşıma için seçenekler taşıdığınız bir abonelik veya tooa yeni abonelik içindeki hello kaynaklara göre değişir.

### <a name="same-subscription"></a>Aynı abonelik
Bir kaynak grubu tooanother kaynak grubundaki aynı abonelik, kısıtlamaları aşağıdaki hello uygulamak hello içindeki kaynaklar taşınırken:

* Sanal ağları (Klasik) taşınamaz.
* Sanal makineler (Klasik) hello bulut hizmetiyle taşınması gerekir.
* Merhaba taşıma tüm sanal makineleri içerdiğinde bulut hizmeti yalnızca taşınabilir.
* Aynı anda yalnızca bir bulut hizmeti taşınabilir.
* Aynı anda yalnızca bir depolama hesabı (Klasik) taşınabilir.
* Depolama hesabı (Klasik) hello taşınamaz bir sanal makine ya da bir bulut hizmeti ile aynı işlemi.

toomove Klasik kaynakları tooa yeni kaynak grubu içinde Merhaba aynı abonelik, hello aracılığıyla hello standart taşıma işlemlerini kullanmak [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), veya [REST API](#use-rest-api). Kullandığınız hello aynı işlemleri Resource Manager kaynaklarını taşımak için kullanın.

### <a name="new-subscription"></a>Yeni abonelik
Kaynakları tooa yeni abonelik taşırken kısıtlamaları aşağıdaki hello Uygula:

* Hello hello Abonelikteki tüm Klasik kaynaklar taşınmalıdır aynı işlemi.
* Merhaba hedef abonelik diğer Klasik kaynakları içermemesi gerekir.
* Merhaba taşıma yalnızca klasik taşıma için ayrı bir REST API aracılığıyla istenebilir. Klasik kaynaklar tooa yeni abonelik taşırken Hello standart Resource Manager taşıma komutlar çalışmaz.

toomove Klasik kaynakları tooa yeni abonelik, belirli tooclassic kaynakları hello REST işlemlerini kullanın. toouse REST, hello aşağıdaki adımları gerçekleştirin:

1. Çapraz abonelik hello kaynak abonelik katılabilir onay taşıyın. Merhaba aşağıdaki işlemi kullanın:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Merhaba istek gövdesinde şunları içerir:

  ```json
  {
    "role": "source"
  }
  ```

     Merhaba doğrulama işlemi için Hello yanıt biçimi aşağıdaki hello şöyledir:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Çapraz abonelik hello hedef abonelik katılabilir onay taşıyın. Merhaba aşağıdaki işlemi kullanın:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Merhaba istek gövdesinde şunları içerir:

  ```json
  {
    "role": "target"
  }
  ```

     Merhaba yanıt aynı hello kaynak abonelik doğrulama biçimi hello kullanılıyor.
3. Her iki aboneliğin doğrulama başarılı olursa, tüm Klasik kaynaklar ile aşağıdaki işlemi hello bir abonelik tooanother abonelikten Taşı:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    Merhaba istek gövdesinde şunları içerir:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

Merhaba işlemi birkaç dakika çalışabilir.

## <a name="use-portal"></a>Portal kullanma
toomove kaynaklar, bu kaynakları içeren hello kaynak grubu seçin ve ardından hello seçin **taşıma** düğmesi.

![Kaynakları taşıma](./media/resource-group-move-resources/select-move.png)

Merhaba kaynakları tooa yeni kaynak grubu veya yeni bir abonelik taşıma olup olmadığını seçin.

Merhaba kaynakları toomove ve hello hedef kaynak grubu seçin. Bu kaynaklar ve seçim için tooupdate betikleri gereksinim kabul **Tamam**. Merhaba önceki adımda hello Düzenle abonelik simgesini seçtiyseniz hello hedef aboneliği seçmeniz gerekir.

![hedef seçin](./media/resource-group-move-resources/select-destination.png)

İçinde **bildirimleri**, taşıma işlemi çalıştıran bu hello bakın.

![taşıma durumunu göster](./media/resource-group-move-resources/show-status.png)

Tamamlandığında, hello sonucunu bildirilir.

![taşıma sonucu göster](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>PowerShell kullanma
toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, `Move-AzureRmResource` komutu.

ilk örnekteki Hello nasıl toomove bir kaynak tooa yeni kaynak grubu.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Merhaba ikinci örnekteki nasıl toomove birden çok kaynak tooa yeni kaynak grubu.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa yeni abonelik, hello için bir değer dahil `DestinationSubscriptionId` parametresi.

Bunu Sorduğunuza toomove hello istediğiniz tooconfirm belirtilen kaynaklar.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Azure CLI 2.0 kullanın
toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, `az resource move` komutu. Merhaba kaynak hello kaynakları toomove kimliklerini sağlar. Kaynak kimlikleri komutu aşağıdaki hello ile alabilirsiniz:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Aşağıdaki örnek hello nasıl toomove bir depolama hesabı tooa yeni kaynak grubu gösterir. Merhaba, `--ids` parametresi hello kaynak kimlikleri toomove boşlukla ayrılmış bir listesini sağlayın.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa yeni abonelik, hello sağlamak `--destination-subscription-id` parametresi.

## <a name="use-azure-cli-10"></a>Azure CLI 1.0 kullanın
toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, `azure resource move` komutu. Merhaba kaynak hello kaynakları toomove kimliklerini sağlar. Kaynak kimlikleri komutu aşağıdaki hello ile alabilirsiniz:

```azurecli
azure resource list -g sourceGroup --json
```

Biçim aşağıdaki hello döndürür:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Aşağıdaki örnek hello nasıl toomove bir depolama hesabı tooa yeni kaynak grubu gösterir. Merhaba, `-i` parametresi hello kaynak kimlikleri toomove virgülle ayrılmış bir listesini sağlayın.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Bunu Sorduğunuza toomove hello istediğiniz tooconfirm belirtilen kaynak.

## <a name="use-rest-api"></a>REST API’yi kullanma
toomove mevcut kaynakları tooanother kaynak grubuna veya aboneliğe, çalıştırın:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

Merhaba istek gövdesinde hello hedef kaynak grubu ve hello kaynakları toomove belirtin. Merhaba taşıma REST işlemi hakkında daha fazla bilgi için bkz: [taşıma kaynakları](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Sonraki adımlar
* Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında toolearn bkz [Resource Manager ile Azure PowerShell'i kullanarak](powershell-azure-resource-manager.md).
* Aboneliğinizi yönetmek için Azure CLI komutları hakkında toolearn bkz [kullanma hello Azure CLI Resource Manager ile](xplat-cli-azure-resource-manager.md).
* Aboneliğinizi yönetmek için portal özellikleri hakkında toolearn bkz [hello Azure portal toomanage kaynakları kullanarak](resource-group-portal.md).
* bir mantıksal kuruluş tooyour kaynakları uygulama hakkında toolearn bkz [kullanarak kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).
