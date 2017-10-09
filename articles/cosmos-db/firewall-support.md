---
title: "aaaAzure Cosmos DB güvenlik duvarı desteği & IP erişim denetimi | Microsoft Docs"
description: "Azure Cosmos DB veritabanı hesaplarında toouse IP erişim denetimi İlkeleri Güvenlik Duvarı için nasıl destek bilgi edinin."
keywords: "IP erişim denetimi, güvenlik duvarı desteği"
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Azure Cosmos DB güvenlik duvarı desteği
bir Azure Cosmos DB veritabanı hesapta depolanan toosecure verileri Azure Cosmos DB sağlanan destek dayalı bir gizlilik için [yetkilendirme modelini](https://msdn.microsoft.com/library/azure/dn783368.aspx) güçlü karma tabanlı ileti kimlik doğrulama kodu (HMAC) kullanır. Şimdi, ayrıca yetkilendirme modelini toohello gizli alan, gelen güvenlik duvarı desteği için IP tabanlı erişim denetimlerini güdümlü İlkesi Azure Cosmos DB destekler. Bu model geleneksel veritabanı sisteminin çok benzer toohello güvenlik duvarı kuralları ve güvenlik toohello Azure Cosmos DB veritabanı hesabı, ek bir düzeyi sağlar. Bu modelde, şimdi bir Azure Cosmos DB veritabanı hesabı toobe yalnızca onaylanan bir makineler kümesinden erişilebilir yapılandırmak ve/veya Bulut Hizmetleri. Bu makineler ve hizmetler onaylanan kümeleri tooAzure Cosmos DB kaynaklarına erişim hala hello arayan toopresent geçerli bir yetkilendirme belirteci gerektirir.

## <a name="ip-access-control-overview"></a>IP erişim denetimine genel bakış
Varsayılan olarak, bir Azure Cosmos DB veritabanı hesabı Hello isteği tarafından geçerli bir yetkilendirme belirteci eşlik sürece, genel internet'ten erişilebilir. tooconfigure IP ilke tabanlı erişim denetimi, hello kullanıcı IP adreslerini veya CIDR form toobe izin verilen veritabanı hesabı için istemci IP listesi hello olarak eklenen IP adres aralıklarını hello kümesi sağlamanız gerekir. Bu yapılandırma uygulandıktan sonra bu izin verilenler dışında makinelerden kaynaklanan tüm istekler hello sunucu tarafından engellenir.  Merhaba IP tabanlı erişim denetimi için akışı işleme hello bağlantı diyagramı aşağıdaki hello tanımlanır.

![IP tabanlı erişim denetimi için Hello bağlantı işlemini gösteren diyagram](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Bulut hizmetleri gelen bağlantıları
Azure'da, bulut Hizmetleri Azure Cosmos DB kullanan Orta katman hizmet mantığı barındırmak için bir çok yaygın bir yöntemdir. tooenable erişim tooan bir bulut hizmetinden Azure Cosmos DB veritabanı hesabı, hello genel IP adresi hello bulut hizmeti tarafından Azure Cosmos DB veritabanı hesabınızla ilişkili IP adreslerinin listesi izin eklenen toohello olmalıdır [yapılandırma Merhaba IP erişim denetimi ilkesini](#configure-ip-policy).  Bu, bulut Hizmetleri tüm rol örneklerini erişim tooyour Azure Cosmos DB veritabanı hesabı sahip olmasını sağlar. Hello ekran aşağıdaki gösterildiği gibi hello Azure portalında, bulut hizmetlerinizde için IP adreslerini alabilir.

![Hello Azure portalında görüntülenen bir bulut hizmeti için genel IP adresi Hello gösteren ekran görüntüsü](./media/firewall-support/public-ip-addresses.png)

Ek rol örnekleri ekleyerek, bulut hizmetinin ölçeğini olduğunda, bu yeni örnekleri otomatik olarak erişim toohello Azure Cosmos DB veritabanı hesabı sahip hello parçası olduğu aynı bulut hizmeti.

## <a name="connections-from-virtual-machines"></a>Sanal makinelerden bağlantıları
[Sanal makineler](https://azure.microsoft.com/services/virtual-machines/) veya [sanal makine ölçek kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) kullanılan toohost Azure Cosmos DB kullanarak orta katman hizmetleri de olabilir.  tooconfigure hello Azure Cosmos DB veritabanı hesabı tooallow erişimi sanal makineler, sanal makine ve/veya sanal makine ölçek kümesi genel IP adreslerine izin verilen IP adreslerini Azure Cosmos DB veritabanı hesabınızın hello biri olarak yapılandırılması gerekir [hello IP erişim denetimi ilkesini yapılandırma](#configure-ip-policy). Hello ekran aşağıdaki gösterildiği gibi hello Azure portal, sanal makineler için IP adresleri geri alabilirsiniz.

![Hello Azure portalında görüntülenen bir sanal makine için genel bir IP adresi gösteren ekran görüntüsü](./media/firewall-support/public-ip-addresses-dns.png)

Ek sanal makine örnekleri toohello grup eklediğinizde, bunlar otomatik olarak erişim tooyour Azure Cosmos DB veritabanı hesabı sağlanır.

## <a name="connections-from-hello-internet"></a>Internet bağlantılarını hello
Bir Azure Cosmos DB üzerinde bir bilgisayar hesabını veritabanı erişimi Merhaba, Internet hello istemci IP adresi veya IP adresi aralığı hello makinenin izin verilen hello Azure Cosmos DB veritabanı hesabı için bir IP adresi listesine eklenen toohello olması gerekir. 

## <a id="configure-ip-policy"></a>Merhaba IP erişim denetimi ilkesini yapılandırma
Merhaba IP erişim denetimi ilkesini hello Azure portal ayarlanabilir veya üzerinden programlı olarak [Azure CLI](cli-samples.md), [Azure Powershell](powershell-samples.md), veya hello [REST API](/rest/api/documentdb/) hello güncelleştirerek`ipRangeFilter` özelliği. IP adresleri/aralıklarına virgülle ayrılmış ve boşluk içermemelidir olması gerekir. Örnek: "13.91.6.132,13.91.6.1/24". Veritabanı hesabınızı bu yöntemlerle güncelleştirirken emin toopopulate olması tüm hello özellikleri tooprevent toodefault ayarları sıfırlanıyor.

> [!NOTE]
> Tüm erişim tooyour yapılandırılmış hello dışında makinelerden Azure Cosmos DB veritabanı hesabı, Azure Cosmos DB veritabanı hesabınız için bir IP erişim denetimi İlkesi etkinleştirerek, IP adresi aralıkları listesi engellendi izin verilen. Bu model, hello veri düzlemi işlemi hello portalından gözatma de engellenen tooensure hello bütünlüğü erişim denetimi.

toosimplify geliştirme hello Azure portal belirleyip makinenizde çalışan uygulamalar hello Azure Cosmos DB hesap erişebilmesi için listesi, izin verilen, istemci makine toohello hello IP'sini ekleyin yardımcı olur. Merhaba istemci IP adresi burada hello portal tarafından görülen algılandığını unutmayın. Makinenizin hello istemci IP adresi olabilir, ancak ağ geçidinizin hello IP adresi olabilir. Tooremove unutmadığınızdan giderek tooproduction önce.

tooset hello IP erişim denetimi ilkesini hello Azure portal'ı tıklatın, toohello Azure Cosmos DB hesabı dikey gidin **Güvenlik Duvarı** hello Gezinti menüsünde ardından **ON** 

![Nasıl tooopen hello güvenlik duvarı dikey penceresinde hello Azure portal gösteren ekran görüntüsü](./media/firewall-support/azure-portal-firewall.png)

Merhaba yeni bölmesinde hello Azure portal erişim hello hesabı ve diğer adresleri ve aralıkları uygun şekilde ekleyin, sonra tıklatın olup olmadığını belirtin **kaydetmek**.  

> [!NOTE]
> Bir IP erişim denetimi İlkesi etkinleştirdiğinizde, Azure portal toomaintain erişim hello için tooadd başlangıç IP adresi gerekir. Merhaba portal IP adresleri şunlardır:
> |Bölge|IP adresi|
> |------|----------|
> |Tüm bölgeler aşağıda belirtilen hariç| 104.42.195.92|
> |Almanya|51.4.229.218|
> |Çin|139.217.8.252|
> |ABD Devleti Arizona|52.244.48.71|
>

![Bir nasıl gösteren ekran görüntüsü tooconfigure Güvenlik Duvarı ayarlarında hello Azure portalı](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Merhaba IP erişim denetimi İlkesi sorun giderme
### <a name="portal-operations"></a>Portal işlemleri
Tüm erişim tooyour yapılandırılmış hello dışında makinelerden Azure Cosmos DB veritabanı hesabı, Azure Cosmos DB veritabanı hesabınız için bir IP erişim denetimi İlkesi etkinleştirerek, IP adresi aralıkları listesi engellendi izin verilen. Koleksiyonlar ve sorgu belgeleri gözatma gibi tooenable portal veri düzlemi işlemler istiyorsanız, bu nedenle tooexplicitly gerekir hello kullanarak Azure portal erişime izin **Güvenlik Duvarı** dikey penceresinde hello portal. 

![Bir nasıl gösteren ekran görüntüsü tooenable erişim toohello Azure portalı](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK & Rest API'si
Güvenlik nedeniyle, SDK veya REST API aracılığıyla erişime izin verilen listesine hello makinelerde karşı genel 404 bulunamadı yanıtta başka ek ayrıntı döndürülecek için. Merhaba IP Azure Cosmos DB veritabanı hesap tooensure hello doğru ilke yapılandırmanızı için yapılandırılan listesinden uygulanan tooyour Azure Cosmos DB veritabanı hesabı izin verilen doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar
Ağ hakkında bilgi için ilgili performans ipuçları, bkz: [performans ipuçları](performance-tips.md).

