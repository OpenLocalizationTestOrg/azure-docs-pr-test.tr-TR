---
title: "aaaAzure sanal makine en iyi güvenlik uygulamaları | Microsoft Docs"
description: "Bu makalede, Azure'da bulunan sanal makineleri kullanılan güvenlik en iyi yöntemler toobe çeşitli sağlar."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Azure VM Güvenlik için en iyi yöntemler

Bir hizmet (Iaas) senaryoları çoğu altyapıda [Azure sanal makineleri (VM'ler)](https://docs.microsoft.com/en-us/azure/virtual-machines/) olan hello ana iş yükü bulut kullanan kuruluşlar için bilgi işlem. Bu durum özellikle açıktır [karma senaryolar](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) burada kuruluşlar istediğiniz tooslowly geçirme iş yükleri toohello bulut. Bu tür senaryolarda hello izleyin [Iaas için genel güvenlik konuları](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)ve güvenlik en iyi yöntemler tooall Vm'leriniz uygulayın.

Bu makalede ele çeşitli VM en iyi güvenlik uygulamalarını, her müşterilerimizden aldığımız türetilmiş ve sanal makineler ile doğrudan kendi deneyimlerini.

Hello iyi bir fikir anlaşma üzerinde temel alır ve geçerli Azure platformu özellikleri ile çalışma ve ayarlar özellik. Görüşlerini ve teknolojileri zamanla değişebilir biz tooupdate planlama Bu makale düzenli olarak tooreflect bu değişiklikleri.

En iyi her uygulama için hello makalede açıklanmaktadır:

* Hangi hello en iyi uygulamadır.
* İyi bir fikir tooenable olmasının onu.
* Tooenable nasıl öğrenebilirsiniz onu.
* Tooenable başarısız oluşabileceklerden onu.
* Olası alternatifler toohello en iyi yöntem.

Merhaba makale VM en iyi güvenlik uygulamalarını takip hello inceler:

* VM kimlik doğrulaması ve erişim denetimi
* VM kullanılabilirlik ve ağ erişim
* Şifreleme zorlayarak VM'ler, kalan verileri koruma
* VM güncelleştirmelerini yönetme
* VM güvenlikle ilgili tutumunuzu yönetme
* VM performansını izleme

## <a name="vm-authentication-and-access-control"></a>VM kimlik doğrulaması ve erişim denetimi

VM koruma hello ilk adımı yalnızca yetkili kullanıcıların tooensure yeni Vm'leri yedekleme yapabilir tooset'dır. Kullanabileceğiniz [Azure Resource Manager ilkeleri](../azure-resource-manager/resource-manager-policy.md) tooestablish kuralları, kuruluşunuzdaki kaynakların özelleştirilmiş ilkeler oluşturma ve bu ilkeleri tooresources gibi uygulama [kaynak grupları](../azure-resource-manager/resource-group-overview.md).

Tooa kaynak grubu doğal ait VM'ler ilkelerine devralır. Bu yaklaşım toomanaging VM'ler öneririz rağmen ayrıca Denetim erişim tooindividual VM ilkeleri kullanarak yapabilecekleriniz [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md).

Resource Manager ilkeleri ve RBAC toocontrol VM erişimi etkinleştirdiğinizde, genel VM Güvenlik geliştirilmesine yardımcı olun. Aynı yaşam döngüsü hello hello ile sanal makineleri birleştirmek öneririz aynı kaynak grubu. Kaynak grupları kullanarak, dağıtmak, izlemek ve maliyetleri kaynaklarınız için faturalama yukarı alma. tooenable kullanıcılar tooaccess ve Vm'leri, yedekleme kümesi kullanın bir [en az ayrıcalık yaklaşım](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). Ve ayrıcalıkları toousers atadığınızda, yerleşik Azure rolleri aşağıdaki toouse hello planlayın:

- [Sanal makine Katılımcısı](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): sanal makineleri yönetme ancak sanal ağ veya depolama hesabı toowhich ilgili bağlı olduğunuzdan hello değil.
- [Klasik sanal makine Katılımcısı](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): hello Klasik dağıtım modeli, ancak sanal makineleri bağlı değil hello sanal ağ veya depolama hesabı toowhich hello kullanılarak oluşturulan sanal makineleri yönetebilirsiniz.
- [Güvenlik Yöneticisi](../active-directory/role-based-access-built-in-roles.md#security-manager): güvenlik bileşenleri, güvenlik ilkeleri ve sanal makineleri yönetebilirsiniz.
- [DevTest Labs kullanıcı](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): her şeyi görüntüleyip bağlamak, başlatmak, yeniden başlatın ve sanal makineleri kapatın.

Hesapları ve parolaları Yöneticiler arasında paylaşmayın ve parolaları birden çok kullanıcı hesapları veya hizmetleri, özellikle sosyal medya için parolaları veya diğer yönetim dışı etkinlikler arasında yeniden yok. İdeal olarak, kullanmanız gereken [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) şablonları tooset, Vm'leri yedekleme güvenli bir şekilde. Bu yaklaşımı kullanarak, dağıtım seçenekleriniz güçlendirmek ve hello dağıtım boyunca güvenlik ayarlarını zorlayacaktır.

Veri erişim denetimi RBAC gibi özelliklerinden yararlanarak zorlamaz kuruluşlar, kullanıcılar gerekenden daha fazla ayrıcalıklarını verme. Uygun kullanıcı erişimi toocertain verileri doğrudan bu verileri tehlikeye atabilir.

## <a name="vm-availability-and-network-access"></a>VM kullanılabilirlik ve ağ erişim

VM toohave yüksek kullanılabilirlik gereken Kritik uygulamalar çalıştırıyorsa, birden çok VM kullanmanızı öneririz. Daha iyi kullanılabilirlik için en az iki VM hello oluşturma [kullanılabilirlik kümesi](../virtual-machines/windows/tutorial-availability-sets.md).

[Azure yük dengeleyici](../load-balancer/load-balancer-overview.md) ayrıca yük dengeli sanal makineleri toohello ait gerektirir aynı kullanılabilirlik kümesi. Bu sanal makineleri Internet hello erişilmesi gerekiyorsa yapılandırmalısınız bir [Internet'e yönelik Yük Dengeleyici](../load-balancer/load-balancer-internet-overview.md).

VM'ler gösterilen toohello Internet olduğunda önemlidir, [kontrol ağ güvenlik grupları (Nsg'ler) ile ağ trafiği akışını](../virtual-network/virtual-networks-nsg.md). Nsg'ler uygulanan toosubnets olabileceğinden, kaynaklarınızı alt ağa göre gruplandırma ve Nsg'ler toohello alt uygulayarak hello sayısını küçültebilirsiniz. Merhaba hedefi olan toocreate hello düzgün şekilde yapılandırarak yapabilirsiniz Ağ yalıtım katmanı [ağ güvenliği](../best-practices-network-security.md) Azure özellikleri.

Merhaba tam zamanında (JIT) VM-erişim uzaktan erişim tooa sahip Azure Güvenlik Merkezi toocontrol özelliğinden de kullanabilirsiniz belirli VM ve ne kadar süreyle.

Ağ erişim kısıtlamalarını tooInternet dönük VM'ler zorlamaz kuruluşlar Uzak Masaüstü Protokolü (RDP) yanılma saldırısı gibi toosecurity riskleri açığa.

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Şifreleme zorlayarak, sanal makineleri, kalan verileri koruma

[Bekleyen verileri şifreleme](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) veri gizliliği, uyumluluk ve veri egemenliği doğru zorunlu bir adımdır. [Azure Disk şifrelemesi](../security/azure-security-disk-encryption.md) BT yöneticileri tooencrypt Windows ve Linux Iaas VM diskleri sağlar. Disk şifrelemesi hello endüstri standardı Windows BitLocker özellik ve hello Linux dm-crypt özelliği tooprovide birim şifrelemesi hello işletim sistemi ve hello veri diskleri için birleştirir.

Disk şifrelemesi uygulayabilirsiniz toohelp kuruluşunuzun güvenlik ve uyumluluk gereksinimlerini veri toomeet koruyun. Kuruluşunuz şifreleme kullanmayı düşünmelisiniz toohelp riskleri ilgili toounauthorized veri erişimi etkisini azaltır. Ayrıca hassas verileri toothem yazmadan önce sürücülerinizin şifrelemek öneririz.

Emin tooencrypt adresinde Azure depolama hesabınızdaki rest, VM veri birimleri tooprotect olabilir. Koruma hello şifreleme anahtarları ve gizli anahtarı kullanarak [Azure anahtar kasası](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

Veri şifrelemeyi zorunlu olmayan kuruluşlar daha gösterilen toodata bütünlüğü sorunlardır. Örneğin, yetkisiz veya standart dışı kullanıcılar bir veri güvenliği aşılmış hesaplarındaki çalmak veya ClearFormat kodlanmış yetkisiz erişim toodata elde. Alma gibi riskleri üzerinde sektör düzenlemelerini ile toocomply yanı sıra, şirketler tespitlerini kullanan ve doğru güvenlik kullanarak tooenhance kendi veri güvenlik denetimleri kanıtlamanız gerekir.

Disk şifrelemesi hakkında daha fazla toolearn bkz [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>VM güncelleştirmelerini yönetme

Azure VM'ler, tüm gibi VM'ler şirket olduğundan, kullanıcı tarafından yönetilen hedeflenen toobe, Azure Windows güncelleştirmeleri toothem anında değil. Ancak, etkin tooleave hello otomatik Windows Update ayarını teşvik. Başka bir seçenektir toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) veya başka bir uygun güncelleştirme yönetimi ürün başka bir VM veya şirket içi. WSUS ve Windows Update VM'ler güncel kalmasını sağlayın. Ayrıca, tüm Iaas Vm'leri toodate olan tarama bir ürün tooverify kullanmanızı öneririz.

Azure tarafından sağlanan stok görüntüleri düzenli olarak güncelleştirilen tooinclude hello Windows güncelleştirmelerini en son round bağımsızdır. Ancak, hello görüntüleri dağıtım sırasında geçerli olacağını garanti yoktur. Ortak sürümleri izleyen bir hafif gecikme (en fazla birkaç hafta) mümkün olabilir. Denetleme ve tüm Windows güncelleştirmelerini yükleme her dağıtımın hello ilk adım olmalıdır. Siz veya kendi kitaplığınızı gelen görüntüleri dağıtırken bu özellikle önemli tooapply ölçüsüdür. Hello Azure Marketi bir parçası olarak sağlanan görüntüleri, varsayılan olarak otomatik olarak güncelleştirilir.

Yazılım güncelleştirme ilkelerini zorunlu olmayan kuruluşlar daha bilinen, daha önce sabit güvenlik açıklarından yararlanma gösterilen toothreats şunlardır. Bu tür tehditleri toocomply sektör düzenlemelerini ile riski yanı sıra şirketler tespitlerini kullanan ve doğru güvenlik denetimleri toohelp kullanarak hello buluttaki, iş yükü hello güvenliğini sağlamak kanıtlamanız gerekir.

Yazılım güncelleştirme geleneksel veri merkezleri için en iyi uygulamaları önemli tooemphasize olduğunda ve Azure Iaas benzer şekilde. Bu nedenle, geçerli yazılım güncelleştirme ilkeleri tooinclude VM'ler değerlendirmek öneririz.

## <a name="manage-your-vm-security-posture"></a>VM güvenlikle ilgili tutumunuzu yönetme

Gelişen siber tehditlere ve Vm'lerinizi koruma hızla tehditleri algılayabilir, yetkisiz erişim tooyour kaynakları engellemek, uyarılarını tetikler ve hatalı pozitif sonuçları azaltmak izleme kapasitesine zengin gerektirir. Bu tür, bir iş yükü için Hello güvenlik tutumunu hello VM, güncelleştirme yönetimi toosecure ağ Access'ten tüm güvenlik yönlerini oluşur.

toomonitor hello güvenlik duruşunu, [Windows](../security-center/security-center-virtual-machine.md) ve [Linux VM'ler](../security-center/security-center-linux-virtual-machine.md), kullanın [Azure Güvenlik Merkezi](../security-center/security-center-intro.md). Azure Güvenlik Merkezi'nde özellikleri aşağıdaki hello yararlanarak Vm'lerinizi koruma:

* Önerilen yapılandırma kuralları ile işletim sistemi güvenlik ayarlarını uygula
* Tanımlamak ve sistem güvenliğini ve eksik olabilir kritik güncelleştirmeleri yükleyin
* Uç nokta kötü amaçlı yazılımdan koruma koruma önerileri dağıtma
* Disk şifrelemesi doğrula
* Değerlendirmek ve güvenlik açıkları düzeltmek
* Tehditleri algılama

Güvenlik Merkezi, tehditleri için etkin olarak izleyebilir ve olası risklere açığa altında **güvenlik uyarıları**. Bağıntılı tehditleri adlı tek bir görünümde toplanan **güvenlik olayı**.

toounderstand Güvenlik Merkezi, Azure'da bulunan, sanal makineleri, olası tehditler belirlemenize yardımcı olabilir nasıl video aşağıdaki hello izleyin:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

Güçlü güvenlik tutumunu Vm'leri için zorlamaz kuruluşlar tarafından yetkisiz kullanıcıların kurulan toocircumvent güvenlik denetimleri olası girişimleri farkında kalır.

## <a name="monitor-vm-performance"></a>VM performansını izleme

Kaynak kötüye VM işlemleri izin verilenden daha fazla kaynak tüketmesine bir sorun olabilir. VM performans sorunlarını kullanılabilirlik hello güvenlik ilkesini ihlal tooservice kesintiye neden olabilir. Bir sorun gerçekleştirildiği sırada, bu nedenle, bu kesinlik temelli toomonitor VM erişim yalnızca Tepkisel, değildir, ancak aynı zamanda bir proaktif olarak normal işlem sırasında ölçülen temel performans karşı.

Çözümleme tarafından [Azure tanılama günlük dosyaları](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), VM kaynaklarınızı izlemek ve performans ve kullanılabilirlik tehlikeye atabilir olası sorunları. Hello Azure tanılama uzantısını Windows tabanlı sanal makinelerin izleme ve tanılama olanakları sağlar. Merhaba bir parçası olarak hello uzantısı dahil olmak üzere, bu yetenekleri etkinleştirebilirsiniz [Azure Resource Manager şablonu](../virtual-machines/windows/extensions-diagnostics-template.md).

Aynı zamanda [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview-metrics.md) , kaynağın durumu toogain görünürlük.

Performans modellerini bazı değişiklikler normal veya anormal olup VM performans izleme kuruluşlar oluşturulamıyor toodetermine şunlardır. Merhaba VM normalden daha fazla kaynak tüketen, böyle bir anomali dış kaynak veya hello VM çalışan güvenliği aşılmış bir işlem olası bir saldırı gelebilir.
