---
title: "Azure aaaOverview yönetilen uygulamalar | Microsoft Docs"
description: "Azure için Hello kavramlarını açıklar yönetilen uygulamalar"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Azure yönetilen uygulamaların genel bakış

Azure kullanmak satıcılar Merhaba Dünya çözümleri toocustomers sunabilir. Azure Market birinci taraf ve üçüncü taraf satıcılar karmaşık, multiresource şablonlardan yüzlerce oluşan bir galeri ' dir. Dakika içinde müşteriler dağıtabilir ve platform hizmet (PaaS) ve yazılım hizmet (SaaS) uygulaması olarak kullanmaya başlayın. 

Merhaba Market harika bir yoldur rağmen bir sunum için müşteriler tooquickly dağıtmak, koruma ve hello çözümünü güncelleme hello müşteri sorumludur. Merhaba sanal makine görüntüsü faturalama ötesinde satıcılar müşteriler uygulama hello kullanımı için ücret olamaz. Ayrıca, satıcılar, kritik uygulama kaynakları değiştirmesini müşteriler engelleyemez. Satıcılar da uygulama yapar erişimi toointellectual özelliğini durduramazsınız. Azure yönetilen uygulamalar için bu sorunları çözümler sağlar. 

Merhaba Market, temel farklardan biri ile benzer tooa çözüm şablonunda bir yönetilen uygulamasıdır. Yönetilen bir uygulamada hello hello satıcısı tarafından yönetilen sağlanan tooa kaynak grubu kaynaklardır. Hello kaynak grubu hello müşterinin aboneliğini var, ancak erişim toohello kaynak grubu hello satıcının Kiracı içinde bir kimliğe sahip.

## <a name="advantages-of-managed-applications"></a>Yönetilen uygulamaların avantajları

Hizmet sağlayıcıları (MSP'ler) ISV'ler, yönetilen ve kurumsal merkezi BT ekiplerinin hello Market aracılığıyla yönetilen uygulamaların toodeliver çözümlerini kullanabilir veya hizmet Kataloğu hello. Müşteriler bu aboneliği yönetilen uygulamaların dağıtmak rağmen güncelleştirme ya da bunları hizmet toomaintain sahip değilsiniz. Satıcılar yönetmek ve hello uygulamalarını desteklemek için müşteriler bu uygulamaları toodevelop uygulamaya özgü etki alanı bilgi toomanage yok. Müşteriler, otomatik olarak uygulama güncelleştirmeleri hello uygulamalarla sorunlarını tanılama ve sorun giderme hakkında hello gerek tooworry olmadan elde edebilirsiniz.

Satıcılar ve sağlayıcıları için bir kanal toosell altyapı ve yazılım hello Market aracılığıyla yönetilen uygulamalar oluşturun. Yönetilen uygulamalar ayrıca bir şekilde tooattach sağlamak Hizmetleri ve tooAzure müşteriler işlemsel desteği. Satıcılar hello Azure faturalama sistemi kullanarak müşteriler faturalandırmak. Dağıtılmış uygulama şablonları toomanage hello yaşam döngüsü kullanabilirler. Satıcılar yüksek kaliteli bir hizmet sağlayabilmesi için bu çözümleri bağımsızdır ve korumalı toohello Müşteri ' dir. Bu yaklaşım PaaS ve SaaS satıcıları fayda sağlar. Ayrıca Şirket merkezi platformu ekipleri ve sistem tümleştiricileri (SIS) yardımcı olan toopackage istediğiniz ve bunların çözümleri satmak.

## <a name="managed-application-types"></a>Yönetilen uygulama türleri
Azure yönetilen uygulamaların gelen iki türlerinde: hizmet kataloğu ve Market.
 
### <a name="service-catalog"></a>Service Catalog  

Merhaba hizmet Kataloğu müşteriler kendi kuruluşunuzdaki kişiler tarafından kullanılan Azure toobe onaylanan çözümleri katalog oluşturabilirsiniz. Gibi koruma çözümleri kataloğunu kuruluşlarda merkezi BT ekipleri için yararlıdır. Kuruluşları için çözümleri sunarken hello katalog tooensure uyumluluk belirli kuruluş standartlarıyla kullanabilirler. Denetleme, güncelleştirme ve bu uygulamaları korumak. Çalışanlar hello katalog tooeasily hello zengin önerilen ve kendi BT departmanları tarafından onaylanan uygulamaların keşfedin. Müşteriler, oluşturuldukları hello hizmet Kataloğu yönetilen uygulamaları konusuna bakın. Bunlar hello yönetilen uygulamalarının kendi kuruluş paylaşımda onlarla diğer kişilerin de görebilirsiniz.
 
Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).
 
Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).
 
### <a name="marketplace"></a>Market

Yönetilen uygulamaların hello Market hello Azure portal aracılığıyla kullanılabilir. Bu uygulamalar Hello satıcı yayımlar sonra içinden veya bir kuruluş tooconsume dışından herkes için kullanılabilir. Bu yaklaşımda, MSP'ler, ISV ve SIS bunların çözümleri tooall Azure müşterilerine sunabilir. Müşteriler hello gerek tooinvest anlaşılması ve hello çözümleri koruma olmadan karmaşık bu çözümleri kullanmanın hello yararlanır. 

Şu anda, yayımcılar kendi teklifleri bir yönetilen uygulamayı veya bir çözüm şablonu olarak, koyabileceğiniz yönetilmeyen. Merhaba ana bileşenleri, yönetilen bir uygulama yayımlama hello şablon dosyası ve hello UI tanım dosyası içerir. Merhaba şablon dosyası, sağlanan hello kaynaklar açıklanır. Merhaba UI tanım dosyası, bu kaynakları sağlama girişleri hello Portalı'nda görüntülenen hello nasıl gerekli açıklar. Merhaba, dosyaları bir .zip dosyasında paketlenir ve yayımlama hello Portalı aracılığıyla karşıya gereklidir.
 
Yönetilen uygulama toohello Market yayımlama hakkında daha fazla bilgi için bkz: [Azure hello Market uygulamalarda yönetilen](managed-application-author-marketplace.md).

Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Önemli kavramlar

### <a name="managed-resource-group"></a>Yönetilen kaynak grubu
Merhaba yönetilen kaynak burada tüm Azure hello grubudur hello şablonunda sağlanan kaynakları oluşturulur. Örneğin, Hello Gereci kullanılan toocreate bir depolama hesabı ise, bu kaynak grubu hello depolama hesabı kaynağı içeriyor. Merhaba Gereci kaynak içermiyor.

### <a name="appliance-package"></a>Uygulama paketi
Merhaba publisher hello şablon dosyalarını ve hello createUIDefinition dosya içeren bir paket oluşturur. Özellikle, aşağıdaki dosyaları hello içerir:

- **applianceMainTemplate.json**: Bu şablon dosyası hello Gereci tarafından sağlanan tüm hello kaynakları tanımlar. Bu dosya toocreate kaynakları kullandığı Normal şablon dosyasıdır.

- **MainTemplate.json**: Bu şablon dosyası hello Gereci kaynak (Microsoft.Solutions/appliances) tanımlar. Bu kaynak içinde tanımlanmış bir anahtar özellik ManagedResourceGroupId ' dir. Bu özellik, hangi kaynak grubu içinde applianceMainTemplate.json tanımlanan kullanılan toohost hello gerçek olan kaynakları gösterir.

- **applianceCreateUIDefinition.json**: Bu dosya hello hello şablonda tanımlanan hello parametreler için gerekli kullanıcı Arabirimi nasıl işleneceğini tanımlar.

### <a name="authorization"></a>Yetkilendirme
Merhaba yayımcı hello müşteri adına hello satıcı toomanage hello kaynaklar tarafından gereken hello izinleri belirtmeniz gerekir. Bu izin toohello yönetilen kaynak grubu uygulanır. Hello aşağıdaki değerleri ayarlayın:

- **Principalıd**: Azure Active Directory (Azure AD) tanıtıcısı hello kullanıcı, Grup veya toogrant erişim toohello yönetilen kaynak grubu kullandı uygulama hello. Bu tanımlayıcı toohello publisher'ın Kiracı aittir.

- **Roledefinitionıd**: asıl kimliği önceki hello atanan rolü toohello Azure AD tanıtıcısı hello Hello yerleşik rol tabanlı erişim denetimi rollerinin hello publisher'ın kiracısında herhangi birinde olabilir. Daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Sonraki adımlar

* Yayımlama yönetilen uygulamaların toohello Market hakkında daha fazla bilgi için bkz: [Azure hello Market uygulamalarda yönetilen](managed-application-author-marketplace.md).
* Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).
* Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).
* Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).
* toocreate UI tanım dosyası bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
