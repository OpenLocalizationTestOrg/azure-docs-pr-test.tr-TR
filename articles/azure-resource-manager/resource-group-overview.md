---
title: "aaaAzure Resource Manager'a genel bakış | Microsoft Docs"
description: "Açıklar nasıl toouse Azure Resource Manager dağıtım, yönetim ve kaynaklara erişim denetimini Azure üzerinde."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Azure Resource Manager genel bakış
Uygulamanız için Hello altyapısı genellikle birçok bileşenlerinin – belki de bir sanal makine, depolama hesabı ve sanal ağ veya bir web uygulaması, veritabanı, veritabanı sunucusu ve 3 taraf hizmetleri oluşur. Bu bileşenleri ayrı varlıklar olarak değerlendirmez, bunun yerine bunları tek bir varlığın ilgili ve birbirine bağımlı parçaları olarak kabul edersiniz. Toodeploy istediğiniz, yönetmek ve bunları bir grup olarak izleyebilirsiniz. Azure Resource Manager toowork çözümünüzdeki hello kaynaklarla bir grup olarak sağlar. Dağıtma, güncelleştirme veya tek ve eşgüdümlü bir işlemle, çözümünüz için tüm hello kaynakları silin. Dağıtım için bir şablon kullanabilirsiniz. Üstelik bu şablon test, hazırlık ve üretim gibi farklı ortamlarda da çalışabilir. Resource Manager Güvenlik denetimi sağlar ve özellikleri toohelp etiketleme, kaynaklarınızın dağıtımdan sonra yönetin. 

## <a name="terminology"></a>Terminoloji
Yeni tooAzure Resource Manager olup olmadığını bilmiyorsanız olmayabilir bazı terimler vardır.

* **kaynak** - Azure ile kullanılabilen yönetilebilir bir öğe. Sanal makine, depolama hesabı, web uygulaması, veritabanı ve sanal ağ bazı yaygın kaynaklardandır, ancak çok daha fazlası mevcuttur.
* **kaynak grubu** - Bir Azure çözümü için ilgili kaynakları bir arada tutan bir kapsayıcıdır. Merhaba kaynak grubu hello çözüm için tüm hello kaynakları veya yalnızca bir grup olarak toomanage istediğiniz kaynakları içerebilir. Tooallocate kaynakları istediğiniz karar tooresource gruplara göre ne hello en kuruluşunuz için anlamlı üzerinde. Bkz. [Kaynak grupları](#resource-groups).
* **Kaynak sağlayıcısı** -hello kaynakları sağlayan bir hizmet dağıtmak ve Resource Manager aracılığıyla yönetebilirsiniz. Her kaynak sağlayıcısı, dağıtılan hello kaynaklarla çalışmak için işlem sunar. Bazı ortak kaynak sağlayıcıları hello sanal makine kaynağı sağlayan Microsoft.Compute, hello depolama hesabı kaynağı sağlar, Microsoft.Storage ve kaynakları ilgili tooweb uygulamalar sağlayan Microsoft.Web ' dir. Bkz. [Kaynak sağlayıcıları](#resource-providers).
* **Resource Manager şablonu** -bir veya daha fazla kaynakları toodeploy tooa kaynak grubu tanımlayan bir JavaScript nesne gösterimi (JSON) dosyası. Ayrıca, dağıtılan hello kaynakları arasındaki bağımlılıkların hello tanımlar. Merhaba şablon tutarlı ve sürekli olarak kullanılan toodeploy hello kaynakları olabilir. Bkz. [Şablon dağıtımı](#template-deployment).
* **bildirim temelli söz dizimini** -olanak sağlayan sözdizimi durum "İşte ı düşündüğünüz toocreate" komutları toocreate programlama toowrite hello dizisi kalmadan onu. Merhaba Resource Manager şablonu Tanımlayıcı Sözdizimi örneğidir. Merhaba dosyasında hello altyapı toodeploy tooAzure hello özelliklerini tanımlayın. 

## <a name="hello-benefits-of-using-resource-manager"></a>Kaynak Yöneticisi'ni kullanarak hello avantajları
Resource Manager çeşitli avantajlar sunar:

* Dağıtmak, yönetmek ve bir grubu yerine bu kaynakları ayrı ayrı ele çözümünüz için tüm hello kaynakları izle.
* Art arda çözümünüzü hello geliştirme yaşam döngüsü boyunca dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması da size güven verir.
* Altyapınızı betikler yerine bildirim temelli şablonları kullanarak yönetebilirsiniz.
* Merhaba doğru sırayla dağıtılmalarını sağlamak için kaynaklarınız arasındaki hello bağımlılıkları tanımlayabilirsiniz.
* Rol tabanlı erişim denetimi (RBAC) yerel olarak hello yönetim platformuyla doğrudan tümleşik olduğundan, kaynak grubuna erişim denetimi tooall Hizmetleri uygulayabilirsiniz.
* Etiketleri uygulayabilirsiniz tooresources toologically aboneliğinizdeki tüm hello kaynakları düzenleyin.
* Kaynak grubu için maliyetleri görüntüleyerek kuruluşunuzun fatura açıklık getirebilir paylaşımı hello aynı etiketi.  

Resource Manager çözümlerinizi yönetmek ve yeni bir yolu toodeploy sağlar. Kullandıysanız Merhaba önceki dağıtım modelini ve hello değişiklikler hakkında toolearn istediğiniz, bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Tutarlı yönetim katmanı
Resource Manager hello görevleri Azure PowerShell, Azure CLI, Azure portal, REST API ve geliştirme araçları gerçekleştirmek için bir tutarlı yönetim katmanı sağlar. Tüm hello araçları işlemleri ortak bir dizi kullanın. Sizin için en iyi çalışır ve karışıklık birbirinin yerine kullanabilmek için hello araçlarını kullanın. 

Tüm hello araçları etkileşimde nasıl hello aşağıdaki görüntü gösterdiği aynı Azure Kaynak Yöneticisi API'si hello. Merhaba API kimliğini doğrular ve hello isteği yetkilendirir toohello Resource Manager hizmet isteklerini geçirir. Kaynak Yöneticisi'ni, sonra hello istekleri toohello uygun kaynak sağlayıcıları yönlendirir.

![Resource Manager istek modeli](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Rehber
Merhaba aşağıdaki öneriler çözümleriniz üzerinde çalışırken tam anlamıyla Kaynak Yöneticisi'nin yararlanabilmek yardımcı olur.

1. Altyapınızı kesinlik temelli komutlar yerine Resource Manager şablonlarındaki bildirim temelli sözdizimi hello aracılığıyla dağıtmak ve tanımlayın.
2. Tüm dağıtım ve yapılandırma adımları hello şablonunda tanımlayın. Çözümünüzü ayarlarken el ile yapılan hiçbir adım olmaması gerekir.
3. Kesinlik temelli komutlar toomanage toostart gibi kaynaklarınızı çalıştırın veya bir uygulamayı veya makineyi durdurun.
4. Kaynaklar ile Merhaba Yerleştir bir kaynak grubundaki aynı yaşam döngüsü. Diğer tüm düzenleyici kaynaklar için etiketler kullanın.

Şablonlar hakkında öneriler için bkz. [Azure Resource Manager şablonları oluşturmaya yönelik en iyi uygulamalar](resource-manager-template-best-practices.md).

Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Kaynak grupları
Kaynak grubunuzun tanımlarken, bazı önemli faktörler tooconsider vardır:

1. Grubunuzdaki tüm hello kaynakları paylaşmalıdır hello aynı yaşam döngüsü. Bunları birlikte dağıtır, güncelleştirir ve silersiniz. Bir veritabanı sunucusu gibi bir kaynağın farklı dağıtım döngüsünde tooexist gerekirse başka bir kaynak grubunda olması gerekir.
2. Her kaynak yalnızca bir kaynak grubunda yer alabilir.
3. Ekleyebilir veya bir kaynak tooa kaynak grubu dilediğiniz zaman kaldırabilirsiniz.
4. Bir kaynak bir kaynak grubu tooanother grubundan taşıyabilirsiniz. Daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](resource-group-move-resources.md).
5. Bir kaynak grubu farklı bölgelerde bulunan kaynakları içerebilir.
6. Bir kaynak grubu olabilir tooscope erişim denetimi yönetim işlemleri için kullanılır.
7. Bir kaynak diğer kaynak gruplarındaki kaynaklarla etkileşim kurabilir. Bu etkileşimi Hello iki kaynakları ilişkili ancak değil paylaşmak yaygındır hello aynı yaşam döngüsü (tooa veritabanına bağlanma Örneğin, web uygulamaları).

Bir kaynak grubu oluştururken, bu kaynak grubu için bir konum tooprovide gerekir. "Bir kaynak grubu için neden konum gerekli olsun? Ve hello kaynakları hello kaynak grubundan farklı konumlarda varsa neden hello kaynak grubu konumu hiç önemli?" Merhaba kaynak grubu hello kaynaklarla ilgili meta verileri depolar. Bu nedenle, hello kaynak grubu için bir konumu belirttiğinizde, meta verilerin depolandığı belirtiyorsanız. Uyumluluk nedenleriyle tooensure gerekebilir, verileriniz belirli bir bölgedeki depolanır.

## <a name="resource-providers"></a>Kaynak sağlayıcıları
Her kaynak sağlayıcısı bir Azure hizmetiyle çalışmaya yönelik bir dizi kaynak ve işlem sunar. Toostore anahtarları ve gizli anahtarları istiyorsanız, örneğin, hello ile iş **Microsoft.KeyVault** kaynak sağlayıcısı. Adlı bir kaynak türü bu kaynak sağlayıcısı sunar **kasalarını** hello anahtar kasası oluşturmak için. 

Merhaba bir kaynak türü adıdır hello biçiminde: **{kaynak sağlayıcısı} / {kaynak türü}**. Örneğin, hello anahtar kasası türüdür **Microsoft.KeyVault/vaults**.

Kaynaklarınızı dağıtma işlemine başlamadan önce hello kullanılabilir kaynak sağlayıcıları anlamak. Kaynakları tanımlayan sağlayıcıları ve kaynaklar sağlar kaynak Hello adlarını bilme toodeploy tooAzure istiyor. Ayrıca, tooknow hello geçerli konumlar ve API sürümleri her kaynak türü için gerekir. Daha fazla bilgi için bkz. [Kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).

## <a name="template-deployment"></a>Şablon dağıtımı
Resource Manager ile Merhaba altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayan bir şablon (JSON biçiminde) oluşturabilirsiniz. Bir şablon kullanarak çözümünü yaşam döngüsü boyunca defalarca dağıtabilir ve kaynaklarınızın tutarlı bir durumda dağıtıldığından emin olabilirsiniz. Merhaba Portalı'ndan bir çözüm oluşturduğunuzda hello çözüm otomatik olarak bir dağıtım şablonu içerir. Çözümünüz için hello şablonu ile başlayın ve toomeet özelleştirmek için toocreate şablonunuzu sıfırdan elinizde kendi özel gereksinimlerinize göre. Hello kaynak grubunun geçerli durumunu hello dışarı aktarma veya belirli bir dağıtım için kullanılan hello şablonu görüntüleyerek mevcut bir kaynak grubu için bir şablon elde edebilirsiniz. Merhaba görüntüleme [şablonu dışarı](resource-manager-export-template.md) hello şablon söz dizimi hakkında yararlı yolu toolearn değil.

toolearn hello şablon ve onu nasıl oluşturmak hello biçimi hakkında bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md). tooview hello JSON söz dizimi kaynak türleri için bkz: [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/).

Resource Manager işler hello şablonu gibi başka bir istek (Merhaba görüntü için bkz: [tutarlı yönetim katmanı](#consistent-management-layer)). Merhaba şablonu ayrıştırır ve REST API işlemleri hello uygun kaynak sağlayıcıları için sözdizimini dönüştürür. Örneğin, ne zaman Resource Manager şablonu kaynak tanımı aşağıdaki hello ile alır:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Aşağıdaki toohello Microsoft.Storage kaynak sağlayıcısı gönderilen REST API işlemi hello tanımı toohello dönüştürür:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

Şablonlar ve kaynak gruplarına nasıl tanımladığınız tamamen tooyou ve toomanage istediğiniz yedekleme, bir çözümdür. Örneğin, üç katmanı uygulamanız tek şablonu tooa tek bir kaynak grubu aracılığıyla dağıtabilirsiniz.

![üç katmanlı şablon](./media/resource-group-overview/3-tier-template.png)

Ancak, toodefine bütün altyapınızı tek bir şablonda yok. Genellikle, algılama toodivide Dağıtım gereksinimlerinizi hedeflenen, amaca şablonları kümesi sağlar. Bu şablonları farklı çözümler için kolayca yeniden kullanabilirsiniz. toodeploy belirli bir çözüm, tüm gerekli hello şablonları bağlanan bir ana şablon oluşturun. Merhaba aşağıdaki görüntüde nasıl üç katmanı çözümü üç içeren bir ana şablon aracılığıyla toodeploy iç içe geçmiş gösterir şablonları.

![iç içe geçmiş şablon](./media/resource-group-overview/nested-tiers-template.png)

Ayrı yaşam döngüleri sahip, katmanları yararlanmanız üç tooseparate kaynak gruplarınızı dağıtabilirsiniz. Bildirim hello kaynakları hala bağlı tooresources diğer kaynak gruplarında olabilir.

![katman şablonu](./media/resource-group-overview/tier-templates.png)

Şablonlarınızı tasarlama hakkında daha fazla öneri için bkz. [Azure Resource Manager şablonlarını tasarlama düzenleri](best-practices-resource-manager-design-templates.md). İç içe geçmiş şablonlar hakkında daha fazla bilgi için bkz. [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).

Azure Resource Manager tooensure kaynakları hello doğru sırada oluşturulmasını bağımlılıkları analiz eder. Bir kaynak başka bir kaynaktaki değere bağımlıysa (diskler için depolama hesabına ihtiyaç duyan bir sanal makine gibi) bir bağımlılık ayarlayın. Daha fazla bilgi için bkz. [Azure Resource Manager’da bağımlılıkları tanımlama](resource-group-define-dependencies.md).

Merhaba şablon güncelleştirmeleri toohello altyapısı için de kullanabilirsiniz. Örneğin, bir kaynak tooyour çözümü ekleyin ve önceden dağıtılan hello kaynaklar için yapılandırma kuralları ekleyin. Merhaba şablonu kaynak zaten olan bir kaynak oluşturulmasını belirtiyorsa, Azure Resource Manager yeni bir varlık oluşturmak yerine bir güncelleştirme gerçekleştirir. Aynı olarak durum azure Resource Manager güncelleştirmelerini hello varolan varlık toohello olarak yeni olacaktır.  

Merhaba kurulumunda dahil edilmeyen belirli bir yazılımı yükleme gibi ek işlemlere ihtiyaç resource Manager senaryoları için uzantılar sağlar. Zaten DSC, Chef veya Puppet gibi bir yapılandırma yönetim hizmeti kullanıyorsanız, uzantıları kullanarak bu hizmetle çalışmaya devam edebilirsiniz. Sanal makine uzantıları hakkında daha fazla bilgi için bkz. [Sanal makine uzantıları ve özellikleri hakkında](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Son olarak, hello şablon hello kaynak kodu, uygulamanız için bir parçası haline gelir. Tooyour kaynak kodu deposunda denetleyin ve uygulamanız geliştikçe güncelleştirin. Visual Studio üzerinden hello şablonu düzenleyebilirsiniz.

Şablonunuzu tanımladıktan sonra hazır toodeploy hello kaynakları tooAzure demektir. Merhaba komutları toodeploy hello kaynaklar için bkz:

* [Kaynakları Resource Manager şablonları ve Azure PowerShell ile dağıtma](resource-group-template-deploy.md)
* [Kaynakları Resource Manager şablonları ve Azure CLI ile dağıtma](resource-group-template-deploy-cli.md)
* [Kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md)
* [Kaynakları Resource Manager şablonları ve Resource Manager REST API’si ile dağıtma](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Etiketler
Resource Manager yönetme ve fatura tooyour gereksinimlerine göre toocategorize kaynakları sağlayan bir etiketleme özelliği sunar. Kaynak grubu ve kaynak karmaşık koleksiyonu vardır ve bu varlıkları hello çoğu algılama tooyou hello şekilde toovisualize gerekir etiketleri kullanın. Örneğin, kuruluşunuzda benzer bir rolü hizmet veya toohello ait olan kaynakları etiketleyebilirsiniz aynı bölüm. Etiketler, kuruluşunuzdaki kullanıcılar oluşturabilirsiniz olmadan zor toolater olabilir birden çok kaynakları tanımlamak ve yönetmek. Örneğin, belirli bir projenin tüm hello kaynakları toodelete isteyebilir. Bu kaynakları hello projesi için etiketlenir değil, bulmalarını toomanually sahip. Etiketleme, aboneliğinizde tooreduce gereksiz maliyetleri için önemli bir yolu olabilir. 

Kaynakları hello tooreside gerek yoktur aynı kaynak grubu tooshare bir etiket. Kuruluşunuzdaki tüm kullanıcıların yanlışlıkla birbirinden kısmen farklı etiketler (örneğin "departman" yerine"") uygulama kullanıcılar yerine genel etiketler kullanmasını kendi etiket sınıflandırma tooensure oluşturabilirsiniz.

Aşağıdaki örnek hello bir etiket uygulanmış tooa sanal makine gösterir.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

bir etiket değeri tüm hello kaynaklarla tooretrieve kullanmak PowerShell cmdlet'i aşağıdaki hello:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

Veya Azure CLI 2.0 komutu aşağıdaki hello:

```azurecli
az resource list --tag costCenter=Finance
```

Etiketli kaynaklara hello Azure portal aracılığıyla da görüntüleyebilirsiniz.

Merhaba [kullanım raporu](../billing/billing-understand-your-bill.md) aboneliğinizi etiket adları ve değerleri, etiketlere göre toobreak maliyetleri çıkışı sağlayan içerir. Etiketler hakkında daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).

## <a name="access-control"></a>Erişim denetimi
Resource Manager, kuruluşunuz için erişim toospecific eylem yok toocontrol sağlar. Yerel rol tabanlı erişim denetimi (RBAC) hello yönetim platformu ile tümleştirir ve bu erişim denetimi tooall Hizmetleri kaynak grubunuzdaki uygular. 

Rol tabanlı erişim denetimi ile çalışırken, iki ana kavramlar toounderstand vardır:

* Rol tanımları: Bir izin kümesini açıklar ve birden fazla atama için kullanılabilir.
* Rol atamaları: Belirli bir kapsam (abonelik, kaynak grubu veya kaynak) için bir tanımı bir kimlikle (kullanıcı veya grup) ilişkilendirir. Merhaba atama alt kapsamlar tarafından devralınır.

Kullanıcıların toopre tanımlanmış platform ve kaynağa özel rollere ekleyebilirsiniz. Örneğin, kullanıcıların tooview kaynaklara izin veren okuyucu adlı hello önceden tanımlanmış rol yararlanmak ancak değiştiremez. Kuruluşunuzda erişim toohello okuyucu rolüne bu tür gereken kullanıcıları eklemek ve hello rol toohello abonelik, kaynak grubu veya kaynak uygulayın.

Azure dört platform rolleri aşağıdaki hello sağlar:

1. Sahip - erişim dahil her şeyi yönetebilir
2. Katılımcı - erişim dışında her şeyi yönetebilir
3. Okuyucu - her şeyi görüntüleyebilir, ancak değişiklik yapamaz
4. Kullanıcı erişimi Yöneticisi - kullanıcı erişimi tooAzure kaynakları yönetebilir

Azure ayrıca kaynağa özgü birkaç rol sağlar. Yaygın olanlarından bazıları şunlardır:

1. Sanal makine Katılımcısı - sanal makineleri yönetme ancak toothem erişmek ve bunların hello sanal ağ veya depolama hesabı toowhich yönetemez izni yok
2. Ağ katılımcısı - tüm ağ kaynaklarını yönetmek ancak erişim toothem izni yok
3. Depolama hesabı katkıda bulunan - depolama hesaplarını yönetin ancak erişim toothem izni yok
4. SQL Server Katılımcısı - SQL sunucularını ve veritabanlarını yönetebilir, ancak güvenlikle ilgili ilkelerini yönetemez
5. Web sitesi katkıda bulunan - Web sitelerini yönetme ancak bağlı olan web planları toowhich hello değil

Merhaba tam listesi rolleri ve izin verilen eylemleri için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md). Rol tabanlı erişim denetimi hakkında daha fazla bilgi için bkz. [Azure Rol Tabanlı Erişim Denetimi](../active-directory/role-based-access-control-configure.md). 

Bazı durumlarda, toorun kodu veya kaynaklarına erişen betik istediğiniz ancak toorun istemiyorsanız, bir kullanıcının kimlik bilgileri altında. Bunun yerine, toocreate hello uygulama için bir hizmet asıl adı verilen bir kimlik istediğiniz ve hello hello hizmet sorumlusu için uygun rolü atayın. Resource Manager Merhaba uygulaması toocreate kimlik bilgilerini sağlar ve program aracılığıyla hello uygulama kimlik doğrulaması. Hizmet sorumlusu oluşturma hakkında daha fazla toolearn aşağıdaki konulardan birine bakın:

* [Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın](resource-group-authenticate-service-principal.md)
* [Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın](resource-group-authenticate-service-principal-cli.md)
* [Portal toocreate Azure Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanın](resource-group-create-service-principal-portal.md)

Kritik kaynaklara tooprevent kullanıcıların silme veya bunları değiştirme açıkça kilitleyebilirsiniz. Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).

## <a name="activity-logs"></a>Etkinlik günlükleri
Resource Manager bir kaynağı oluşturan, değiştiren veya silen tüm işlemleri günlüğe kaydeder. Merhaba etkinlik günlükleri toofind sorun giderme sırasında bir hata veya toomonitor kullanabilirsiniz, kuruluşunuzdaki bir kullanıcı bir kaynak nasıl değişiklik. toosee hello günlükleri, seçin **etkinlik günlükleri** hello içinde **ayarları** dikey penceresinde bir kaynak grubu için. Merhaba günlükleri hangi kullanıcı tarafından başlatılan hello işlemi de dahil olmak üzere birçok farklı değerlere göre filtreleyebilirsiniz. Merhaba etkinlik günlükleri ile çalışma hakkında daha fazla bilgi için bkz: [etkinliği görüntüle günlüklerini toomanage Azure kaynakları](resource-group-audit.md).

## <a name="customized-policies"></a>Özelleştirilmiş ilkeler
Resource Manager kaynaklarınızı yönetmek için özelleştirilmiş toocreate ilkeleri sağlar. Merhaba, oluşturduğunuz ilke türleri çeşitli senaryolar içerebilir. Kaynaklar üzerinde bir adlandırma kuralı uygulayabilir, hangi kaynak türlerinin ve örneklerinin dağıtılabileceğini sınırlayabilir veya hangi bölgelerin bir kaynak türünü barındırabileceğini sınırlayabilirsiniz. Departmanlara göre kaynakları tooorganize faturalama etiket değeri gerektirebilir. İlke oluşturma toohelp maliyetleri azaltır ve aboneliğinizi tutarlılığını korumak. 

İlkeleri JSON ile tanımlar ve sonra bu ilkeleri aboneliğinize ya da bir kaynak grubuna uygularsınız. Uygulanan tooresource türleri olduğundan rol tabanlı erişim denetimi ilkeleri farklıdır.

Aşağıdaki örnek hello tüm kaynakları costCenter etiketi ekleyin belirterek etiketi tutarlılık sağlayan bir ilke gösterir.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

Oluşturabileceğiniz birçok ilke türü daha vardır. Daha fazla bilgi için bkz: [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](resource-manager-policy.md).

## <a name="sdks"></a>SDK’lar
Azure SDK'ları birden çok dil ve platform için kullanılabilir. Bu dil uygulamalarının her biri ekosistem paket yöneticisi ve GitHub üzerinden kullanılabilir.

Açık Kaynak SDK depolarımız aşağıda verilmiştir. Geri bildirimler, sorunlar ve çekme isteklerini memnuniyetle karşılıyoruz.

* [.NET için Azure SDK](https://github.com/Azure/azure-sdk-for-net)
* [Java için Azure Yönetim Kitaplıkları](https://github.com/Azure/azure-sdk-for-java)
* [Node.js için Azure SDK](https://github.com/Azure/azure-sdk-for-node)
* [PHP için Azure SDK](https://github.com/Azure/azure-sdk-for-php)
* [Python için Azure SDK](https://github.com/Azure/azure-sdk-for-python)
* [Ruby için Azure SDK](https://github.com/Azure/azure-sdk-for-ruby)

Kaynaklarınızla bu dili kullanma hakkında daha fazla bilgi için bkz:

* [.NET geliştiricileri için Azure](/dotnet/azure/?view=azure-dotnet)
* [Java geliştiricileri için Azure](/java/azure/)
* [Node.js geliştiricileri için Azure](/nodejs/azure/)
* [Python geliştiricileri için Azure](/python/azure/)

> [!NOTE]
> Merhaba SDK hello gerekli işlevselliği sağlamıyorsa toohello da çağırabilirsiniz [Azure REST API](https://docs.microsoft.com/rest/api/resources/) doğrudan.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Şablonları ile basit giriş tooworking için bkz: [mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).
* Şablon oluşturmayla ilgili daha kapsamlı bir kılavuz için bkz. [İlk Azure Resource Manager şablonunuzu oluşturma](resource-manager-create-first-template.md).
* bir şablonda kullanabileceğiniz toounderstand hello işlevleri bkz [şablon işlevleri](resource-group-template-functions.md)
* Resource Manager ile Visual Studio’yu kullanma hakkında bilgi edinmek için bkz. [Azure kaynak gruplarını Visual Studio aracılığıyla oluşturma ve dağıtma](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

Bu genel bakışın sunulduğu videoya şuradan ulaşabilirsiniz:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
