---
title: "Azure kaynakları için yeni abonelik veya kaynak grubu taşıma | Microsoft Docs"
description: "Yeni kaynak grubu ya da abonelik kaynaklarını taşımak için Azure Resource Manager kullanın."
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
ms.date: 10/05/2017
ms.author: tomfitz
ms.openlocfilehash: 7d500d20dcce3e472e3e1e15b9ce307874caf22a
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2018
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a>Kaynakları yeni kaynak grubuna veya aboneliğe taşıyın.

Bu makalede yeni bir abonelik veya yeni bir kaynak grubu aynı abonelik kaynaklarını taşıma gösterilmektedir. Kaynak taşıma için portal, PowerShell, Azure CLI veya REST API'sini kullanabilirsiniz. Taşıma işlemleri bu makalede Azure Destek'ten herhangi bir Yardım için kullanılabilir.

Kaynaklar taşınırken işlemi sırasında kaynak grubu ve hedef grubu kilitlenir. Yazma ve silme işlemleri taşıma işlemi tamamlanana kadar kaynak gruplarında engellenir. Bu kilit ekleyemez, güncelleştirme veya kaynak gruplarındaki kaynakları silin, ancak kaynaklar dondurulmuş gelmez anlamına gelir. Örneğin, bir SQL Server ve veritabanının yeni bir kaynak grubuna taşırsanız, veritabanı kullanan bir uygulama kapalı kalma süresi karşılaşır. Bunu hala okuyabilir ve veritabanına yazma.

Kaynağın konumu değiştirilemez. Bir kaynak taşıma yalnızca bu yeni bir kaynak grubuna taşınır. Yeni kaynak grubu farklı bir konum olabilir, ancak kaynak konumunu değiştirmez.

> [!NOTE]
> Bu makalede, mevcut Azure içindeki kaynaklara önerme hesap taşımayı açıklar. Gerçekte (önceden ödenecek Kullandıkça Öde yükseltme gibi) sunan Azure hesabınızda değiştirmek mevcut kaynakları ile çalışmak için bkz: devam ederken istiyorsanız [Azure aboneliğinizi başka bir teklife geç](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Kaynakları geçmeden önce denetim listesi

Bir kaynağı taşımadan önce gerçekleştirmeniz gereken bazı önemli adımlar vardır. Bu koşulları doğrulayarak hataları önleyebilirsiniz.

1. Kaynak ve hedef abonelikler aynı içinde bulunmalıdır [Azure Active Directory Kiracı](../active-directory/active-directory-howto-tenant.md). Her iki aboneliğin aynı Kiracı kimliği olduğunu denetlemek için Azure PowerShell veya Azure CLI kullanın.

  Azure PowerShell için kullanın:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName <your-source-subscription>).TenantId
  (Get-AzureRmSubscription -SubscriptionName <your-destination-subscription>).TenantId
  ```

  Azure CLI için şunu kullanın:

  ```azurecli-interactive
  az account show --subscription <your-source-subscription> --query tenantId
  az account show --subscription <your-destination-subscription> --query tenantId
  ```

  Kaynak ve hedef abonelikler için Kiracı kimlikleri aynı değilse, başvurmalıdır [Destek](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) kaynakları için yeni bir kiracı taşımak için.

2. Hizmet, kaynakları taşıma olanağını sağlamalıdır. Bu makalede, hangi hizmetlerin taşıma kaynakları etkinleştirmek ve hangi hizmetlerin taşıma kaynakları etkinleştirmeyin listelenmektedir.
3. Hedef abonelik, taşınan kaynağın kaynak sağlayıcısına kayıtlı olmalıdır. Belirten bir hata alırsanız, **kaynak türü için abonelik kayıtlı değil**. Kaynağı taşıdığınız yeni abonelik, ilgili kaynak türüyle daha önce kullanılmamışsa bu sorunla karşılaşabilirsiniz.

  PowerShell için kayıt durumunu almak için aşağıdaki komutları kullanın:

  ```powershell
  Set-AzureRmContext -Subscription <destination-subscription-name-or-id>
  Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
  ```

  Bir kaynak sağlayıcısını kaydetmek için kullanın:

  ```powershell
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
  ```

  Azure CLI için kayıt durumunu almak için aşağıdaki komutları kullanın:

  ```azurecli-interactive
  az account set -s <destination-subscription-name-or-id>
  az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
  ```

  Bir kaynak sağlayıcısını kaydetmek için kullanın:

  ```azurecli-interactive
  az provider register --namespace Microsoft.Batch
  ```

## <a name="when-to-call-support"></a>Destek çağrısı yapıldığında

Bu makalede gösterilen Self Servis işlemleri üzerinden en fazla kaynak taşıyabilirsiniz. Self Servis işlemleri için kullanın:

* Resource Manager kaynaklarını taşıma
* Klasik kaynakları göre taşımak [Klasik dağıtım kısıtlamaları](#classic-deployment-limitations).

Kişi [Destek](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) için gerektiğinde:

* Kaynaklarınızın bir yeni bir Azure hesabı (ve Azure Active Directory kiracısı) taşıyın.
* Klasik kaynakları taşımak ancak kısıtlamalarla sorunu yaşıyor.

## <a name="services-that-enable-move"></a>Taşıma Etkinleştirme Hizmetleri

Bir yeni kaynak grubu ve abonelik için taşıma etkinleştirmek hizmetler şunlardır:

* API Management
* App Service uygulamalarının (web uygulamaları) - bkz [App Service sınırlamalar](#app-service-limitations)
* Application Insights
* Otomasyon
* Azure Cosmos DB
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
* Event Hubs
* Bkz: Hdınsight kümeleri - [Hdınsight sınırlamaları](#hdinsight-limitations)
* IoT Hub
* Anahtar Kasası
* Yük Dengeleyiciler
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
* SQL veritabanı sunucusu - veritabanı ve sunucu, aynı kaynak grubunda bulunmaları gerekir. Bir SQL server taşıdığınızda, tüm veritabanlarını da taşınır.
* Traffic Manager
* Sanal makineler - VMs yönetilen disklerle taşınamaz. Bkz: [sanal makineleri sınırlamaları](#virtual-machines-limitations)
* Sanal makineler (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)
* Sanal makine ölçek kümeleri - bkz [sanal makineleri sınırlamaları](#virtual-machines-limitations)
* Sanal ağlar - bkz [sanal ağlar sınırlamaları](#virtual-networks-limitations)
* VPN Gateway

## <a name="services-that-do-not-enable-move"></a>Taşıma etkinleştirmeyin Hizmetleri

Şu anda bir kaynak taşıma etkinleştirmeyin hizmetler şunlardır:

* AD Domain Services
* AD karma sistem durumu hizmeti
* Application Gateway
* BizTalk Services
* Kapsayıcı Hizmeti
* Express Route
* DevTest Labs - taşıma aynı Abonelikteki yeni kaynak grubu için etkinleştirildi, ancak çapraz abonelik taşıma etkin değil.
* Dynamics LCS
* Yönetilen Uygulamalar
* Yönetilen diskleri - bkz [sanal makineleri sınırlamaları](#virtual-machines-limitations)
* Kurtarma Hizmetleri kasası - ayrıca yapın kurtarma Hizmetleri kasası ile ilişkili işlem, ağ ve depolama kaynaklarını taşıyamazsınız bkz [kurtarma Hizmetleri sınırlamaları](#recovery-services-limitations).
* Güvenlik
* StorSimple Cihaz Yöneticisi
* Bkz: Sanal ağları (Klasik) - [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)

## <a name="virtual-machines-limitations"></a>Sanal makineler sınırlamaları

Yönetilen diskleri taşıma desteklemez. Bu kısıtlama, bazı ilgili kaynaklar çok taşınamaması anlamına gelir. Taşınamıyor:

* Yönetilen diskler
* Yönetilen diske sahip sanal makineler
* Yönetilen disklerden oluşturulan görüntüler
* Yönetilen disklerden oluşturulan anlık görüntüler
* Yönetilen bir diske sahip sanal makinelerle kullanılabilirlik kümeleri

Market kaynaklardan oluşturulan sanal makineleri abonelikler arasında taşınamaz. Sanal makine geçerli abonelikte yetkisini kaldırma ve yeni abonelikte yeniden dağıtın.

Sanal makineler anahtar kasasında depolanan sertifika ile aynı abonelikte ancak abonelikleri boyunca değil yeni bir kaynak grubu için taşınabilir.

## <a name="virtual-networks-limitations"></a>Sanal ağlar sınırlamaları

Eşlenmiş bir sanal ağ taşımak için öncelikle sanal ağ eşlemesi devre dışı bırakmalısınız. Devre dışı sonra sanal ağ taşıyabilirsiniz. Taşıma sonrasında sanal ağ eşlemesi yeniden etkinleştirin.

Sanal ağ alt ağı kaynak Gezinti bağlantılarıyla içeriyorsa, bir sanal ağ farklı bir aboneliğe taşınamıyor. Örneğin, bir alt ağ bir Redis önbelleği kaynak dağıtılırsa, bu alt ağdaki kaynak Gezinti bağlantısı vardır.

## <a name="app-service-limitations"></a>App Service sınırlamalar

Uygulama hizmeti uygulamaları ile çalışırken, yalnızca bir uygulama hizmeti planı taşınamıyor. App Service uygulamalarının taşımak için seçenekleriniz şunlardır:

* Uygulama hizmeti planı ve diğer tüm uygulama hizmeti kaynakları bu kaynak grubunda zaten App Service kaynakları yok yeni bir kaynak grubuna taşıyın. Bu gereksinim, hatta uygulama hizmeti plan ile ilişkili olmayan uygulama hizmeti kaynakları taşımalısınız anlamına gelir.
* Uygulamalar farklı bir kaynak grubuna taşımak, ancak tüm uygulama hizmeti planları özgün kaynak grubunda tutun.

Uygulama hizmeti planı düzgün çalışabilmesi için aynı kaynak grubunda için uygulaması olarak bulunmaları gerekmez.

Örneğin, kaynak grubunuz varsa:

* **Web-a** ile ilişkili **planı-a**
* **Web b** ile ilişkili **planı b**

Seçenekleriniz şunlardır:

* Taşıma **web-a**, **planı-a**, **web-b**, ve **planı b**
* Taşıma **web-a** ve **web-b**
* Taşıma **web-a**
* Taşıma **web-b**

Diğer tüm birleşimler, bir uygulama hizmeti planı (uygulama hizmeti kaynak türlü) taşırken bırakılamaz arkasındaki bir kaynak türü bırakarak içerir.

Web uygulamanızın farklı bir kaynak grubu, uygulama hizmeti planı daha bulunur, ancak her ikisi de yeni bir kaynak grubuna taşımak istediğiniz iki adımda taşıma gerçekleştirmeniz gerekir. Örneğin:

* **Web-a** bulunan **web grubu**
* **planı bir** bulunan **planı Grup**
* İstediğiniz **web-a** ve **planı-a** bulunması için **birleştirilmiş Grup**

Bu taşıma gerçekleştirmek için iki ayrı taşıma işlemi aşağıdaki sırayla gerçekleştirin:

1. Taşıma **web-a** için **planı Grup**
2. Taşıma **web-a** ve **planı-a** için **Birleştirilmiş grup**.

Yeni kaynak grubu veya abonelik sorunları olmadan, bir uygulama hizmet sertifikası taşıyabilirsiniz. Ancak, web uygulamanızı dışarıdan satın ve uygulamaya karşıya bir SSL sertifikası içeriyorsa, web uygulaması taşımadan önce sertifika silmeniz gerekir. Örneğin, aşağıdaki adımları gerçekleştirebilirsiniz:

1. Karşıya yüklenen sertifikanın web uygulamasından silme
2. Web uygulaması taşıma
3. Web uygulaması'na ve sertifikayı karşıya yüklemek

## <a name="classic-deployment-limitations"></a>Klasik dağıtım sınırlamaları

Klasik modeli aracılığıyla dağıtılan kaynakları taşıma seçeneklerini taşıdığınız bir abonelik içindeki veya yeni bir abonelik için kaynaklara göre farklılık gösterir.

### <a name="same-subscription"></a>Aynı abonelik

Kaynaklar aynı abonelik içindeki başka bir kaynak grubu için bir kaynak grubundan taşırken, aşağıdaki kısıtlamalar geçerlidir:

* Sanal ağları (Klasik) taşınamaz.
* Sanal makineler (Klasik) bulut hizmetiyle taşınması gerekir.
* Tüm sanal makineleri taşıma içerdiği durumlarda bulut hizmeti yalnızca taşınabilir.
* Aynı anda yalnızca bir bulut hizmeti taşınabilir.
* Aynı anda yalnızca bir depolama hesabı (Klasik) taşınabilir.
* Depolama hesabı (Klasik), sanal makine ya da bir bulut hizmeti ile aynı işlemde taşınamaz.

Klasik kaynaklar aynı abonelik içindeki yeni bir kaynak grubuna taşımak için standart taşıma işlemleri aracılığıyla kullanmak [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), veya [REST API](#use-rest-api). Resource Manager kaynaklarını taşımak için kullandığınız gibi işlemlerin aynısını kullanın.

### <a name="new-subscription"></a>Yeni abonelik

Kaynaklar için yeni bir abonelik taşırken, aşağıdaki kısıtlamalar geçerlidir:

* Abonelikteki tüm Klasik kaynaklar aynı işlem içinde taşınması gerekir.
* Hedef abonelik diğer Klasik kaynakları içermemesi gerekir.
* Taşıma yalnızca klasik taşıma için ayrı bir REST API aracılığıyla istenebilir. Klasik kaynaklar için yeni bir abonelik taşırken standart Resource Manager taşıma komutlar çalışmaz.

Klasik kaynaklar için yeni bir aboneliği taşımak için Klasik kaynakları için belirli REST işlemlerini kullanın. REST kullanmak için aşağıdaki adımları gerçekleştirin:

1. Kaynak abonelik bir çapraz abonelik taşıma katılabilmesi için denetleyin. Aşağıdaki işlemi kullanın:

  ```HTTP
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     İstek gövdesinde şunları içerir:

  ```json
  {
    "role": "source"
  }
  ```

     Yanıt için doğrulama işlemi aşağıdaki biçimdedir:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Hedef abonelik bir çapraz abonelik taşıma katılabilmesi için denetleyin. Aşağıdaki işlemi kullanın:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     İstek gövdesinde şunları içerir:

  ```json
  {
    "role": "target"
  }
  ```

     Kaynak abonelik doğrulama ile aynı biçimi yanıt kullanılıyor.
3. Her iki aboneliğin doğrulama başarılı olursa, tüm Klasik kaynaklar bir abonelikten şu işlemi başka bir aboneliğe taşıyın:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    İstek gövdesinde şunları içerir:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

İşlemi birkaç dakika çalışabilir.

## <a name="recovery-services-limitations"></a>Kurtarma Hizmetleri kısıtlamaları

Ağ, depolama için etkin değil taşıyın veya işlem kaynaklarını Azure Site Recovery ile olağanüstü durum kurtarma ayarlamak için kullanılır.

Örneğin, şirket içi makinelerinizi bir depolama hesabına (Storage1) çoğaltmasını ayarladıktan ve bir sanal ağa (Network1) bağlı sanal makine (VM1) olarak Azure için yük devretme sonrasında gündeme için korumalı makine istediğinizi varsayalım. Bu Azure kaynakları - Storage1, VM1 ve Network1 - hiçbirini aynı abonelik içindeki kaynak grupları arasında veya abonelikler arasında taşınamıyor.

Kayıtlı bir VM taşımak için **Azure yedekleme** kaynak grupları arasında:
 1. Geçici olarak yedeklemeyi durdurma ve yedekleme verileri tut
 2. VM hedef kaynak grubuna taşıma
 3. Kullanıcıların taşıma işlemi önce oluşturulan kullanılabilir geri yükleme noktaları geri yükleyebilirsiniz aynı/yeni kasa altında yeniden koruyun.
Kullanıcı abonelikleri yedeklenen VM geçerse, adım 1 ve 2. adım aynı kalır. 3. adımda, mevcut / hedef abonelik içinde oluşturulan yeni bir kasa altında VM korumak kullanıcı gerekir. Kurtarma Hizmetleri kasası bilgilerine desteği çapraz abonelik yedekler.

## <a name="hdinsight-limitations"></a>Hdınsight sınırlamaları

Yeni Abonelik veya kaynak grubu için Hdınsight kümeleri taşıyabilirsiniz. Ancak, ağ kaynaklarını (örneğin, sanal ağ, NIC veya yük dengeleyici) bir Hdınsight kümesine bağlı abonelikler arasında taşınamaz. Ayrıca, küme için bir sanal makineye bağlı bir NIC yeni bir kaynak grubuna taşıyamazsınız.

Hdınsight kümesi için yeni bir abonelik taşırken, diğer kaynakları (örneğin, depolama hesabı) taşıyın. Ardından, Hdınsight kümesi tek başına taşıyın.

## <a name="search-limitations"></a>Arama sınırlamaları

Birden çok arama kaynakları farklı bölgelerde tümünü bir defada yerleştirilen taşınamıyor.
Böyle bir durumda, ayrı ayrı taşımanız gerekir.

## <a name="use-portal"></a>Portal kullanma

Kaynakları taşımak için bu kaynakları içeren kaynak grubunu seçin ve ardından **taşıma** düğmesi.

![Kaynakları taşıma](./media/resource-group-move-resources/select-move.png)

Yeni bir kaynak grubu veya yeni bir abonelik için kaynakları taşıma olup olmadığını seçin.

Taşıma için kaynak ve hedef kaynak grubu seçin. Bu kaynaklar için komut dosyaları güncelleştirmek ve seçmek gereken kabul **Tamam**. Önceki adımda Düzenle abonelik simgesini seçtiyseniz, hedef abonelik seçmeniz gerekir.

![hedef seçin](./media/resource-group-move-resources/select-destination.png)

İçinde **bildirimleri**, taşıma işleminin çalıştığını görürsünüz.

![taşıma durumunu göster](./media/resource-group-move-resources/show-status.png)

Tamamlandığında, sonucu bildirilir.

![taşıma sonucu göster](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>PowerShell kullanma

Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için kullanmak [taşıma AzureRmResource](/powershell/module/azurerm.resources/move-azurermresource) komutu. Aşağıdaki örnek, birden çok kaynakları yeni bir kaynak grubuna taşımak gösterilmiştir.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

Yeni bir aboneliği taşımak için bir değer dahil `DestinationSubscriptionId` parametresi.

## <a name="use-azure-cli"></a>Azure CLI kullanma

Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için kullanmak [az kaynak taşıma](/cli/azure/resource?view=azure-cli-latest#az_resource_move) komutu. Kaynak taşımak için kimlikleri kaynakları sağlar. Aşağıdaki örnek, birden çok kaynakları yeni bir kaynak grubuna taşımak gösterilmiştir. İçinde `--ids` parametresi, kaynak taşımak için kimlikleri boşlukla ayrılmış bir listesini sağlayın.

```azurecli
webapp=$(az resource show -g OldRG -n ExampleSite --resource-type "Microsoft.Web/sites" --query id --output tsv)
plan=$(az resource show -g OldRG -n ExamplePlan --resource-type "Microsoft.Web/serverfarms" --query id --output tsv)
az resource move --destination-group newgroup --ids $webapp $plan
```

Yeni bir abonelik taşımanızı sağlayan `--destination-subscription-id` parametresi.

## <a name="use-rest-api"></a>REST API’yi kullanma

Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için çalıştırın:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

İstek gövdesinde hedef kaynak grubu ve kaynakları taşımak için belirtin. Taşıma REST işlemi hakkında daha fazla bilgi için bkz: [taşıma kaynakları](/rest/api/resources/Resources/MoveResources).

## <a name="next-steps"></a>Sonraki adımlar

* Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında bilgi edinmek için [Resource Manager ile Azure PowerShell'i kullanarak](powershell-azure-resource-manager.md).
* Aboneliğinizi yönetmek için Azure CLI komutları hakkında bilgi edinmek için [Resource Manager ile Azure CLI kullanarak](xplat-cli-azure-resource-manager.md).
* Aboneliğinizi yönetmeye yönelik portal özellikleri hakkında bilgi edinmek için [kaynakları yönetmek için Azure portalını kullanarak](resource-group-portal.md).
* Kaynaklarınız için bir mantıksal kuruluş uygulama hakkında bilgi edinmek için [etiketleri kullanarak kaynaklarınızı düzenleme](resource-group-using-tags.md).
