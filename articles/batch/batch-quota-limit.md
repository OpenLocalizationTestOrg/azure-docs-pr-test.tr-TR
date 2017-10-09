---
title: "aaaService Azure Batch için kotalar ve sınırlar | Microsoft Docs"
description: "Varsayılan Azure Batch kotalar, sınırları ve kısıtlamaları ve nasıl toorequest kota artırır hakkında bilgi edinin"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Batch hizmet kotaları ve limitleri

Olarak diğer Azure hizmetleriyle sınırlar vardır hello Batch hizmeti ile ilişkilendirilmiş belirli kaynaklar. Çoğu bu sınırları hello aboneliği veya hesabı düzeyinde Azure tarafından uygulanan varsayılan kotaları bulunur. Bu makalede bu Varsayılanları ele ve kota nasıl istek artırır.

Batch iş yüklerinizi tasarlayıp ölçeğini artırırken kotaları göz önünde bulundurun. Havuzunuzu hello hedef işlem düğümleri, belirttiğiniz sayısına eriştikten değil, örneğin, hello çekirdek kota Batch hesabınıza veya bölgesel VM çekirdek kota için aboneliğiniz için sınırına ulaştınız.

Tek bir Batch hesabında birden fazla toplu iş yüklerini çalıştırmak veya iş yüklerinizi hello Batch hesapları arasında dağıtabilirsiniz aynı abonelik, ancak farklı Azure bölgelerinde.

Toplu toorun üretim iş yükleri planlıyorsanız, bir veya daha fazla hello kotaları hello varsayılan yukarıda tooincrease gerekebilir. Tooraise kota istiyorsanız, çevrimiçi açabilirsiniz [müşteri destek isteği](#increase-a-quota) herhangi bir ücret alınmaz.

> [!NOTE]
> Bir kota kapasitesi garantisi bir kredi sınırı ' dir. Büyük ölçekli kapasite gereksinimlerini varsa, lütfen Azure desteğine başvurun.
> 
> 

## <a name="resource-quotas"></a>Kaynak kotaları
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Kullanıcı abonelik modunda kotaları

Toplu işlem hesabı havuzu ayırma moduyla çok ayarlamak için**kullanıcı aboneliği**, Vm'leri ve depolama hesapları gibi başka kaynaklar toplu işlem, bir havuz oluşturduğunuzda, aboneliğinizde doğrudan oluşturulur. Bu modda oluşturulan tooan hesabı Hello Azure Batch çekirdek kota geçerli değildir. Bunun yerine, bölgesel işlem çekirdek ve diğer kaynakları aboneliğinizin hello kotaları uygulanır. Bu Kotalar hakkında daha fazla bilgi [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).

Kaynak kullanımı kullanıcı abonelik modunda oluşturulan bir hesap için planlama yaparken, toplu işlem kaynaklarında (toplama toocompute çekirdekler) aşağıdaki Not hello her 40 Linux VM'ler veya 20 Windows VM'ler için gerekli şunlardır:

| Kaynak | Kota | Sağlayıcı |
| --- | ---| --- |
| Bir depolama hesabı | Depolama Hesapları | Microsoft.Storage |
| Bir genel IP adresi | Genel IP Adresleri | Microsoft.Network | 
| Bir sanal ağ | Sanal Ağlar | Microsoft.Network | 
| Bir ağ güvenlik grubu | Ağ Güvenlik Grupları | Microsoft.Network | 
| Bir sanal makine ölçek kümesi | Sanal Makine Ölçek Kümeleri | Microsoft.Compute | 
| Bir yük dengeleyici | Yük Dengeleyici | Microsoft.Network | 

Merhaba çekirdek kota bölgesel düzeyinde ya da VM ailesi başına Batch havuzu veya havuzları için gerekli kümesi according toohello VM boyutu olması gerekir:

| Kota | Sağlayıcı |
| --- | ---- |
| Toplam bölgesel çekirdek | Microsoft.Compute |
| … Aile çekirdek | Microsoft.Compute |



## <a name="other-limits"></a>Diğer sınırları
| **Kaynak** | **Üst Sınır** |
| --- | --- |
| [Eş zamanlı görevleri](batch-parallel-node-tasks.md) işlem düğümü başına |düğüm çekirdeği 4 x sayısı |
| [Uygulamaları](batch-application-packages.md) toplu işlem hesabı başına |20 |
| Uygulama başına uygulama paketleri |40 |
| Uygulama paketi boyutu (her) |Yaklaşık 195 GB'den<sup>1</sup> |
| En fazla başlangıç görevi boyutu | 32768 karakter<sup>2</sup> |

<sup>1</sup> en büyük blok blob boyutu için azure depolama sınırı<br />
<sup>2</sup> kaynak dosyaları ve ortam değişkenleri içerir

## <a name="view-batch-quotas"></a>Toplu kotaları görüntüle
Toplu işlem hesabı kotası hello görüntülemek [Azure portal][portal].

1. Seçin **Batch hesapları** hello Portalı'nda, ardından, ilgilendiğiniz hello toplu işlem hesabı seçin.
2. Seçin **özellikleri** hello Batch hesabının menü dikey.
3. Merhaba özellikleri dikey penceresinde hello görüntüler **kotaları** toohello toplu işlem hesabı uygulanmakta
   
    ![Toplu işlem hesabı kotası][account_quotas]

Kullanıcı abonelik modunda oluşturulan bir toplu işlem hesabı için abonelik kotaları hello Azure Portal görünümü hello ilgili.

1. Seçin **abonelikleri**ve hello toplu işlem hesabı için kullandığınız hello abonelik seçin.

2. Merhaba üzerinde **abonelik** dikey penceresinde, select **kullanım + kotaları**.



## <a name="increase-a-quota"></a>Kota artırma
Kota artırma hello kullanarak aboneliğinizi veya toplu iş hesabınız için bu adımları toorequest izleyin [Azure portal][portal]. Kota artışı Hello türü hello havuzu ayırma moduna Batch hesabınızın bağlıdır.

### <a name="increase-a-batch-cores-quota"></a>Toplu işlem çekirdek kota artırma 

Batch hesabınıza oluşturulursa **Batch hizmeti** modu, bu adımları toorequest toplu çekirdek kota artışı izleyin:

1. Select hello **Yardım + Destek** döşeme portal Panonuzda veya hello soru işareti (**?**) hello sağ üst köşesindeki hello portal.
2. Seçin **yeni destek isteği** > **Temelleri**.
3. Merhaba üzerinde **Temelleri** dikey penceresinde:
   
    a. **Sorun türü** > **kota**
   
    b. Aboneliğinizi seçin.
   
    c. **Kota türü** > **toplu işlem**
   
    d. **Destek planınız** > **kota desteği - dahil**
   
    **İleri**’ye tıklayın.
4. Merhaba üzerinde **sorun** dikey penceresinde:
   
    a. Seçin bir **önem** tooyour göre [iş etkisi][support_sev].
   
    b. İçinde **ayrıntıları**, toochange, hello toplu işlem hesabı adı ve hello yeni sınır istediğiniz her kotasını belirtin.
   
    **İleri**’ye tıklayın.
5. Merhaba üzerinde **kişi bilgileri** dikey penceresinde:
   
    a. Seçin bir **tercih edilen iletişim yöntemi**.
   
    b. Doğrulayın ve gerekli hello kişi ayrıntılarını girin.
   
    Tıklatın **oluşturma** toosubmit hello destek isteği.

Destek İsteği gönderdikten sonra Azure destek, sizinle iletişim kuracaktır. Merhaba isteği Tamamlanıyor too2 iş günleri alabileceğine dikkat edin.

### <a name="increase-a-subscription-cores-quota"></a>Abonelik çekirdek kota artırma

Batch hesabınıza oluşturulursa **kullanıcı aboneliği** modu ve gerektiğinde ek bölge veya VM ailesi çekirdek, kota bir istek aboneliğinizde artırın. Adımlar için bkz: [Resource Manager çekirdek Kotayı artırmak istekleri](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>İlgili konular
* [Hello Azure portal kullanarak bir Azure Batch hesabı oluşturma](batch-account-create-portal.md)
* [Azure Batch özelliklerine genel bakış](batch-api-basics.md)
* [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
