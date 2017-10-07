---
title: "aaaAzure sözlüğü - Azure sözlüğünü | Microsoft Docs"
description: "Hello Azure sözlüğünü toounderstand bulut terminolojisi hello Azure platformu üzerinde kullanın. Bu kısa Azure sözlük tanımları için Azure ortak bulut koşulları sağlar."
keywords: "Azure sözlüğünü, bulut terminolojisi, Azure sözlüğünü, terim tanımları, bulut koşulları"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Microsoft Azure sözlüğü: hello Azure platformu üzerinde bulut terimler sözlüğü

Merhaba Microsoft Azure sözlüğü hello Azure platformu bulut terminolojisi kısa Sözlüğü ' dir. Ayrıca bkz:

* [Microsoft Azure ve Amazon Web Hizmetleri](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) -tanımları, Azure Hizmetleri ve AWS'dekiler.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Bulut bilgi işlem koşullarını](https://azure.microsoft.com/overview/cloud-computing-dictionary/) -genel endüstri bulut koşulları.

## <a name="account"></a>Hesabı
Bir Azure aboneliğini yönetmek ve tooaccess kullanılan bir hesap. Genellikle bir hesap herhangi birinde olabilir ancak bir Azure hesabı tooas adlandırılan: olan bir iş, okul, veya kişisel Microsoft hesabı veya bir Office 365 kullanıcı adı ve parola. Hello için kaydolduğunuzda bir hesap toomanage bir Azure aboneliği oluşturabilirsiniz [ücretsiz deneme sürümü](https://azure.microsoft.com).  
Bkz: [Office 365 hesabınıza bir Azure aboneliği için kaydolun](billing/billing-use-existing-office-365-account-azure-subscription.md) ve [toosign içinde kullanabileceğiniz hesapları](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>API uygulaması
Başka bir ad [App Service uygulaması](#app-service-app).

## <a name="app-service-app"></a>App Service uygulaması
Merhaba işlem kaynakları, [Azure App Service](app-service/app-service-value-prop-what-is.md) barındırma için sağlar bir [Web sitesi veya web uygulaması](app-service-web/app-service-web-overview.md), [web API'si](app-service-api/app-service-api-apps-why-best-platform.md), veya [mobil uygulama arka ucu](app-service-mobile/app-service-mobile-value-prop.md). Uygulama hizmeti uygulamalardır de başvurulan tooas *uygulama hizmetleri*, *web uygulamaları*, *API uygulamaları*, ve *mobil uygulamaları*.

## <a name="availability-set"></a>Kullanılabilirlik kümesi
Sanal makineleri koleksiyonu birlikte tooprovide uygulama artıklık ve güvenilirlik yönetilen. bir kullanılabilirlik kümesi Hello kullanımını ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir olmasını sağlar.  
Bkz: [hello Windows sanal makinelerin kullanılabilirliğini yönetme](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [hello Linux sanal makinelerin kullanılabilirliğini yönetme](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>Azure Klasik dağıtım modeli
İki birini [dağıtım modellerini](resource-manager-deployment-model.md) toodeploy kaynakları Azure içinde kullanılan (Merhaba yeni modeldir Azure Resource Manager). Destek bazı Azure Hizmetleri yalnızca hello Resource Manager dağıtım modeli, bazı yalnızca hello Klasik dağıtım modelini destekleyen ve bazı her ikisi de destekler. Her Azure hizmeti Hello belgelerine destekledikleri hangi modellere belirtir.

## <a name="cli"></a>Azure komut satırı arabirimi (CLI)
Kullanılan toomanage olabilecek bir komut satırı arabirimi, Windows, macOS ve Linux Azure Hizmetleri.  Bazı hizmet veya hizmet özellikleri yalnızca PowerShell veya CLI hello yönetilebilir. Bkz: [Azure CLI 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
Bir komut satırı arabirimi toomanage Windows bilgisayarlarından komut satırı aracılığıyla Azure Hizmetleri. Bazı hizmet veya hizmet özellikleri yalnızca PowerShell veya CLI hello yönetilebilir.
Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview)

## <a name="arm-model"></a>Azure Resource Manager dağıtım modeli
İki birini [dağıtım modellerini](resource-manager-deployment-model.md) toodeploy kaynakları (Merhaba diğer hello Klasik dağıtım modeli olur) Microsoft Azure'da kullanılan. Destek bazı Azure Hizmetleri yalnızca hello Resource Manager dağıtım modeli, bazı yalnızca hello Klasik dağıtım modelini destekleyen ve bazı her ikisi de destekler. Her Azure hizmeti Hello belgelerine destekledikleri hangi modellere belirtir.

## <a name="fault-domain"></a>hata etki alanı
Merhaba hello aynı büyük olasılıkla başarısız bir kullanılabilirlik kümesinde sanal makineler koleksiyonunda zaman. Bir örnek, bir dolapta ortak bir güç kaynağı ve ağ anahtarı paylaşmak makineler grubudur. Azure'da hello sanal makineleri bir kullanılabilirlik kümesinde birden çok hata etki alanları arasında otomatik olarak ayrılır.  
Bkz: [hello Windows sanal makinelerin kullanılabilirliğini yönetme](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [hello Linux sanal makinelerin kullanılabilirliğini yönetme](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>coğrafi
Genellikle iki veya daha fazla bölge içeren veri residency için tanımlanmış bir sınır. Merhaba sınırları içinde veya Ulusal sınırların dışında olabilir ve vergi düzenlemesi tarafından etkilenir. Her coğrafi en az bir bölge vardır. Asya Pasifik ve Japonya geos örnekleridir. Olarak da bilinir *Coğrafya*.  
Bkz: [Azure bölgeleri](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>coğrafi çoğaltma
BLOB'lar, tablolar ve Kuyruklar bölgesel çifti içinde gibi içeriği otomatik olarak çoğaltılıyor hello işlemi.  
Bkz: [Azure SQL veritabanı için etkin coğrafi çoğaltma](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>Görüntü
Merhaba işletim sistemi ve kullanılan toocreate olabilir uygulama yapılandırması herhangi bir sayıda sanal makineleri içeren dosya. Azure'da görüntülerinin iki tür vardır: VM görüntüsü ve işletim sistemi görüntüsü. Merhaba görüntü oluşturulduğunda tüm diskleri tooa sanal makineye bağlı ve bir VM görüntüsü bir işletim sistemini içerir. Bir işletim sistemi görüntüsü yalnızca bir genelleştirilmiş işletim sistemiyle hiçbir veri disk yapılandırmaları içerir.  
Bkz: [gidin ve Azure PowerShell veya CLI hello ile select Windows sanal makine görüntüleri](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>Sınırları
Merhaba oluşturulabilir veya elde edilebilir performans Kıyaslama hello kaynak sayısı. Sınırlar genellikle abonelikler, hizmetleri ve teklifleri ile ilişkilendirilir.  
Bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>Yük Dengeleyici
Gelen trafiği bir ağdaki bilgisayarlar arasında dağıtır bir kaynaktır. Azure üzerinde bir yük dengeleyici yük dengeleyici kümesinde tanımlanan trafiği toovirtual makineler dağıtır. A [yük dengeleyici](load-balancer/load-balancer-overview.md) iç olabilir veya internet'e yönelik olabilir.  

## <a name="mobile-app"></a>Mobil uygulama
Başka bir ad [uygulama hizmeti](#app-service-app).

## <a name="offer"></a>Teklif
Merhaba fiyatlandırma, kredi ve ilgili koşulların geçerli tooan Azure aboneliği.  
Merhaba bkz [Azure Teklifi Ayrıntıları sayfası](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portal
Merhaba güvenli web portalı ve Azure hizmetleri yönetmek toodeploy kullanılır.  İki portalı vardır: Merhaba [Azure portal](http://portal.azure.com/) ve hello [Klasik portal](http://manage.windowsazure.com/). Başkalarının yalnızca birinde kullanılabilir veya diğer hello ancak bazı hizmetler hem portallarında kullanılabilir. Merhaba [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/) hangi hizmetlerin hangi portalında kullanılabilir listeler.

## <a name="region"></a>Bölge
Çapraz Ulusal sınırların vermez ve bir veya daha fazla veri merkezleri içeren bir coğrafi içindeki bir alanı. Fiyatlandırma, bölgesel Hizmetleri ve teklif türleri hello bölge düzeyinde sunulur. Bir bölge genellikle hemen yüz mil tooseveral olabilir başka bir bölge ile eşleştirilmiş. Bölgesel çiftleri, olağanüstü durum kurtarma ve yüksek kullanılabilirlik senaryoları için bir mekanizma olarak kullanılabilir. Tooas ya da *konumu*.  
Bkz: [Azure bölgeleri](best-practices-availability-paired-regions.md)

## <a name="resource"></a>Kaynak
Azure çözümünüzü parçası olan bir öğe. Her Azure hizmeti veritabanları ya da sanal makineleri gibi kaynakları farklı türde toodeploy sağlar.   
Bkz: [Azure Resource Manager'a genel bakış](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>kaynak grubu
Kaynak bir uygulama için ilgili kaynakları tutan Yöneticisi'nde bir kapsayıcı. Merhaba kaynak grubunun tüm bir uygulama için hello kaynakları veya yalnızca mantıksal olarak birlikte gruplandırılmış kaynaklar dahil olabilir. Tooallocate kaynakları nasıl istemediğinize karar verebilirsiniz tooresource gruplara göre ne hello en kuruluşunuz için anlamlı üzerinde.  
Bkz: [Azure Resource Manager'a genel bakış](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>Resource Manager şablonu
Bir veya daha fazla Azure kaynaklarını bildirimli olarak tanımlayan ve hello arasındaki bağımlılıkları tanımlayan bir JSON dosyası kaynakları dağıtıldı. Merhaba şablon tutarlı ve sürekli olarak kullanılan toodeploy hello kaynakları olabilir.  
Bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>Kaynak sağlayıcısı
Merhaba kaynakları sağlayan bir hizmet dağıtmak ve Resource Manager aracılığıyla yönetebilirsiniz. Her kaynak sağlayıcısı, dağıtılan hello kaynaklarla çalışmak için işlem sunar. Kaynak sağlayıcıları hello Azure portal, Azure PowerShell ve çeşitli programlama SDK erişilebilir.  
Bkz: [Azure Resource Manager'a genel bakış](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>Rolü
Toousers, gruplara ve hizmetlere atanmış erişimi denetlemek için bir anlamına gelir. Roller gibi oluştururken, yönetmek ve Azure kaynakları okuma mümkün tooperform eylemlerdir.  
Bkz: [RBAC: yerleşik roller](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>Hizmet düzeyi sözleşmesi (SLA)
açık kalma süresi ve bağlantı için Microsoft'un taahhüt açıklar hello anlaşma. Her Azure hizmetin belirli bir SLA'sı vardır.  
Bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>paylaşılan erişim imzası (SAS)
Hesap anahtarınızı sokmadan toogrant sınırlı erişim tooa kaynak sağlayan bir imza. Örneğin, [Azure depolama kullanan SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant istemci erişim tooobjects BLOB'ları gibi. [IOT hub'ı kullanan SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) toogrant aygıtları izni toosend telemetri.

## <a name="storage-account"></a>Depolama hesabı
Size bir hesap Azure storage'da toohello Azure Blob, kuyruk, tablo ve dosya hizmetlere erişim. Merhaba depolama hesabı adı hello Azure Storage veri nesneleriniz için benzersiz ad alanını tanımlar.  
Bkz: [Azure storage hesapları hakkında](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>aboneliği
Müşteri'nin sözleşmesi tooobtain Azure sağlayan Microsoft Hizmetleri. Abonelik Hello fiyatlandırma ve ilgili koşulların hello abonelik için seçilen hello teklif tarafından yönetilir.
Bkz: [Microsoft çevrimiçi Abonelik Sözleşmesi](https://azure.microsoft.com/support/legal/subscription-agreement/) ve [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>Etiket
Yönetme ve fatura tooyour gereksinimlerine göre toocategorize kaynakları sağlayan bir dizin oluşturma terim. Kaynaklar karmaşık koleksiyonu varsa, bu varlıkları etiketleri toovisualize hello en anlamlı hello şekilde kullanabilirsiniz. Örneğin, kuruluşunuzda benzer bir rolü hizmet veya toohello ait olan kaynakları etiketleyebilirsiniz aynı bölüm.  
Bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketleri](resource-group-using-tags.md)

## <a name="update-domain"></a>etki alanı güncelleştirme
Merhaba koleksiyonu sanal makinelerin bir kullanılabilirlik kümesinde hello güncelleştirilir aynı anda. Aynı güncelleştirme etki alanı birlikte yeniden başlatılır sırasında hello içindeki sanal makineler planlı Bakım. Azure birden çok güncelleştirme etki alanı aynı anda yeniden başlatmaz. Tooas bir yükseltme etki alanını da denir.  
Bkz: [hello Windows sanal makinelerin kullanılabilirliğini yönetme](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [hello Linux sanal makinelerin kullanılabilirliğini yönetme](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>sanal makine
bir işletim sistemi çalıştıran fiziksel bir bilgisayar Hello yazılım uygulamasıdır. Birden çok sanal makine üzerinde aynı anda çalıştırabilirsiniz hello aynı donanım. Azure'da sanal makineler çeşitli boyutlarda kullanılabilir.  
Bkz: [Virtual Machines belgeleri](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>sanal makine uzantısı
Davranışları veya ya da iş veya çalışan bir bilgisayara, toointeract için hello yeteneği sağlamak diğer programları yardımcı olan özellikler uygulayan bir kaynaktır. Örneğin, hello VM erişim uzantısı tooreset kullanın veya bir Azure sanal makinesi üzerinde uzaktan erişim değerlerini değiştirin.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Bkz: [sanal makine uzantıları ve özellikleri (Windows) hakkında](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [sanal makine uzantıları ve özellikleri (Linux) hakkında](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>sanal ağ
Bir ağ, diğer tüm Azure kiracılardan yalıtılmış Azure kaynaklarınızı arasında bağlantı sağlar. Bir [Azure VPN ağ geçidi](vpn-gateway/vpn-gateway-about-vpngateways.md) sanal ağ arasında bağlantılar oluşturmanızı sağlar ve [bir sanal ağ ve bir şirket içi ağ arasındaki](vpn-gateway/vpn-gateway-plan-design.md). Başlangıç IP adresi blokları, DNS ayarları, güvenlik ilkeleri ve bir sanal ağ içinde yönlendirme tabloları tam olarak denetleyebilirsiniz.  
Bkz: [Virtual Network'e genel bakış](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Web uygulaması
Başka bir ad [uygulama hizmeti](#app-service-app).

## <a name="see-also"></a>Ayrıca bkz.

* [Azure ile çalışmaya başlama](https://azure.microsoft.com/get-started/)
* [Bulut kaynağı merkezi](https://azure.microsoft.com/resources/)  
* [İş uygulamanız için Azure](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure, veri merkezinizdeki](https://azure.microsoft.com/overview/business-apps-on-azure/)

