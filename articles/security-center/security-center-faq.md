---
title: "aaaAzure güvenlik sık sorulan sorular (SSS) merkezi | Microsoft Docs"
description: "Bu SSS, Azure Güvenlik Merkezi ile ilgili sorular yanıtlanmaktadır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Azure Güvenlik Merkezi - Sık sorulan sorular (SSS)
Bu SSS, Azure Güvenlik Merkezi, engellemek, algılamak ve toothreats artırılmış görünürlük aracılığıyla Merhaba, Microsoft Azure kaynaklarınızın güvenliğini denetlemenize yanıtlamanıza yardımcı olan bir hizmeti ile ilgili sorular yanıtlanmaktadır.

> [!NOTE]
> İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak. toolearn daha, fazla [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md). Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>
>

## <a name="general-questions"></a>Genel sorular
### <a name="what-is-azure-security-center"></a>Azure Güvenlik Merkezi nedir?
Azure Güvenlik Merkezi engellemek, algılamanıza ve Artırılmış görünürlük aracılığıyla toothreats hello Azure kaynaklarınızın güvenliğini denetlemenize yanıtlamanıza yardımcı olur. Aboneliklerinizde tümleşik güvenlik izleme ve ilke yönetimi sağlar, normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

### <a name="how-do-i-get-azure-security-center"></a>Azure Güvenlik Merkezi nasıl sağlarım?
Azure Güvenlik Merkezi, Microsoft Azure aboneliğiniz ile etkin ve hello erişilen [Azure portal](https://azure.microsoft.com/features/azure-portal/). ([Toohello Portalı'nda oturum](https://portal.azure.com)seçin **Gözat**, çok kaydırarak**Güvenlik Merkezi**).  

## <a name="billing"></a>Faturalandırma
### <a name="how-does-billing-work-for-azure-security-center"></a>Azure Güvenlik Merkezi için fatura iş nasıl yapar?
Güvenlik Merkezi iki katmanı sunulur:

Merhaba **ücretsiz katmanı** hello güvenlik durumunu Azure kaynaklarını, temel güvenlik ilkesi, güvenlik önerileri ve tümleştirme görünürlük ortaklarından güvenlik ürün ve hizmetlerini sağlar.

Merhaba **standart katmanı** algılama özellikleri dahil olmak üzere, tehdit Intelligence, davranış analizi, anomali algılama, güvenlik olaylarına ve tehdit attribution raporları Gelişmiş tehdit ekler. Merhaba standart katmanı ilk 60 gün Merhaba ücretsizdir. 60 gün ötesinde toocontinue toouse hello hizmet seçmeniz gerekir, biz otomatik olarak toocharge hello hizmeti başlatın.  tooupgrade, hello select fiyatlandırma katmanı [Güvenlik İlkesi](security-center-policies.md#set-security-policies). toolearn daha, fazla [Güvenlik Merkezi fiyatlandırma](security-center-pricing.md).

## <a name="permissions"></a>İzinler
Azure Güvenlik Merkezi kullanan [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md), sağlayan [yerleşik roller](../active-directory/role-based-access-built-in-roles.md) atanabilen toousers, grupları ve Azure Hizmetleri.

Güvenlik Merkezi kaynakları tooidentify güvenlik sorunları ve güvenlik açıkları hello yapılandırmasını değerlendirir. Güvenlik Merkezi'nde, yalnızca bilgi sahibi, katkıda bulunan veya okuyucu bir kaynağa ait hello abonelik veya kaynak grubu için hello rolüne atandığında ilgili tooa kaynak.

Bkz: [izinleri Azure Güvenlik Merkezi'nde](security-center-permissions.md) toolearn rolleri ve Güvenlik Merkezi'nde izin verilen eylemleri hakkında daha fazla.

## <a name="data-collection"></a>Veri toplama
Güvenlik Merkezi, sanal makineleri tooassess güvenlik durumlarına toplar, güvenlik önerileri sağlamak ve toothreats sizi uyarır. Güvenlik Merkezi ilk eriştiğinizde, veri toplama, aboneliğinizin tüm sanal makinelerin etkinleştirilir. Veri toplama işlemini hello Güvenlik Merkezi ilke de etkinleştirebilirsiniz.

### <a name="how-do-i-disable-data-collection"></a>Veri toplama nasıl devre dışı bırakabilirim?
Hello Azure Güvenlik Merkezi ücretsiz katmanı kullanıyorsanız, sanal makinelerden veri toplamayı dilediğiniz zaman devre dışı bırakabilirsiniz. Veri toplama hello standart katmanında abonelikler için gereklidir. Bir abonelikte hello güvenlik ilkesi için veri toplama devre dışı bırakabilirsiniz. ([Toohello Azure portalında oturum](https://portal.azure.com)seçin **Gözat**seçin **Güvenlik Merkezi**seçip **İlkesi**.)  Bir abonelik seçtiğinizde, yeni bir dikey pencere açılır ve, hello seçeneği tooturn kapalı sağlar **veri toplama**.

### <a name="how-do-i-enable-data-collection"></a>Veri toplama nasıl etkinleştirebilirim?
Azure aboneliğinizde hello güvenlik ilkesi için veri koleksiyonunu etkinleştirebilirsiniz. tooenable veri koleksiyonu. [Toohello Azure portalında oturum](https://portal.azure.com)seçin **Gözat**seçin **Güvenlik Merkezi**seçip **İlkesi**. Ayarlama **veri toplama** çok**üzerinde**.

### <a name="what-happens-when-data-collection-is-enabled"></a>Veri toplama etkin olduğunda ne olur?
Veri toplama etkin olduğunda, tüm mevcut hello Microsoft Monitoring Agent otomatik olarak hazırlanmıştır ve desteklenen herhangi bir yeni dağıtılan sanal makineler hello abonelikte.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Merhaba İzleme Aracısı etkisi hello Sunucularım performansını mu?
Merhaba Aracısı nominal miktarda sistem kaynağı tüketir ve hello performans üzerinde çok az etkisi olması gerekir. Merhaba performans etkisi ve hello aracısı ve uzantı ile ilgili daha fazla bilgi için bkz [planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>Verilerim nerede depolanır?
Bu Aracıdan toplanan verileri aboneliğinizle ilişkili olan bir günlük analizi çalışma veya yeni bir çalışma alanı olarak depolanır. Daha fazla bilgi için bkz: [veri güvenliği](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Azure Güvenlik Merkezi'ni kullanma
### <a name="what-is-a-security-policy"></a>Bir güvenlik ilkesi nedir?
Bir güvenlik ilkesi hello belirtilen hello içindeki kaynaklar için önerilen denetimleri kümesini tanımlayan abonelik. Azure Güvenlik Merkezi'nde, Azure aboneliklerinize tooyour şirketinizin güvenlik gereksinimleri ve uygulamaların hello türü veya hello her Abonelikteki verilerin duyarlılığına göre ilkeleri tanımlar.

Azure Güvenlik Merkezi sürücü güvenlik önerilerini ve izlemeyi etkin hello güvenlik ilkeleri. güvenlik ilkeleri hakkında daha fazla toolearn bkz [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>Bir güvenlik ilkesi değiştirebilecekleri?
toomodify bir güvenlik ilkesi Güvenlik Yöneticisi veya sahibi veya katkıda bu aboneliğin olması gerekir.

tooconfigure bir güvenlik ilkesi nasıl görürüm toolearn [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>Güvenlik açısından nedir?
Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Olası güvenlik açıkları tanımlandığında, öneri oluşturulur. Merhaba önerileri Kılavuzu hello yapılandırma hello işlemini denetimi gerekli. Örnekler şunlardır:

* Kötü amaçlı yazılımdan koruma toohelp sağlama tanımlamak ve kötü amaçlı yazılım kaldırma
* Yapılandırma [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md) ve kurallarını toocontrol trafiği toovirtual makineler
* Web uygulamalarınızı hedefleyen saldırılara karşı korumaya web uygulaması güvenlik duvarı toohelp sağlama
* Eksik sistem güncelleştirmelerini dağıtma
* Önerilen taban çizgileri hello eşleşmeyen işletim sistemi yapılandırmalarını ele alma

Güvenlik İlkeleri'nde etkinleştirilmiş öneri burada gösterilir.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>Merhaba geçerli güvenlik durumunu Azure Kaynaklarım nasıl görebilirim?
Merhaba **Güvenlik Merkezi genel bakış** dikey penceresinde hello işlem, ağ, depolama ve veri ve uygulamaları tarafından ayrıntılarıyla ortamınızın genel güvenlik duruşunu gösterir. Olası güvenlik açıkları belirlediyseniz, her kaynak türünün bir göstergesi gösteren vardır. Her bölme tıklatarak aboneliğinizi hello kaynaklarında envanterini yanı sıra Güvenlik Merkezi tarafından belirlenen güvenlik sorunlarını listesini görüntüler.

### <a name="what-triggers-a-security-alert"></a>Bir güvenlik uyarısını neyin tetikleyeceğini?
Azure Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve kötü amaçlı yazılımdan koruma ve güvenlik duvarları gibi iş ortağı çözümlerinden günlük verilerini birleştirir. Tehditler algılandığında bir güvenlik uyarısı oluşturulur. Örneklere şunların algılanması dahildir:

* Bilinen kötü amaçlı IP adresleri ile iletişim kuran tehlikeye girmiş sanal makineler
* Windows Hata Raporlama kullanılarak algılanan Gelişmiş kötü amaçlı yazılım
* Sanal makinelere karşı deneme yanılma saldırıları
* Kötü amaçlı yazılım veya Web uygulaması güvenlik duvarı gibi tümleşik iş ortağı güvenlik çözümlerini güvenlik uyarıları

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Hello algılandı ve Microsoft Security Response Center karşı Azure Güvenlik Merkezi tarafından uyarı tehditlere arasındaki fark nedir?
Merhaba Microsoft Güvenlik Yanıt Merkezi (MSRC) select güvenlik hello Azure ağ ve altyapı izleme gerçekleştirir ve Üçüncü taraflardan tehdit Intelligence ve kötüye şikayetlerinden alır. Müşteri verileri yasadışı veya yetkisiz bir şirket tarafından erişilen veya Azure hello müşterinin kullanımını hello şartlarını kabul edilebilir kullanım için uyumlu değil MSRC hale, güvenlik olay Yöneticisi hello müşteri size bildirir. Bildirim, genellikle bir e-posta toohello güvenlik güvenlik kişi belirtilmezse, Azure Güvenlik Merkezi veya hello Azure abonelik sahibi belirtilen kişiler göndererek oluşur.

Güvenlik Merkezi, sürekli olarak hello müşterinin Azure ortamı izleyen ve analiz tooautomatically geçerli bir Azure hizmeti algılayan çeşitli kötü amaçlı etkinliği ' dir. Bu algılamaların hello Güvenlik Merkezi panosunda güvenlik uyarıları olarak ortaya çıkmış.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Hangi Azure kaynaklarını Azure Güvenlik Merkezi tarafından izlenen?
Azure Güvenlik Merkezi, Azure kaynaklarını aşağıdaki hello izler:

* Sanal makineler (VM'ler) (dahil olmak üzere [bulut Hizmetleri](../cloud-services/cloud-services-choose-me.md))
* Azure Sanal Ağları
* Azure SQL Hizmeti
* Azure Storage hesabı
* Azure Web uygulamaları (içinde [uygulama hizmeti ortamı](../app-service/app-service-app-service-environments-readme.md))
* İş ortağı çözümleri gibi bir web uygulaması güvenlik duvarı sanal makineleri ve üzerinde Azure aboneliğinizle tümleşik [uygulama hizmeti ortamı](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Virtual Machines
### <a name="what-types-of-virtual-machines-are-supported"></a>Sanal makineler ne tür destekleniyor mu?
İzleme ve öneriler her iki hello kullanılarak oluşturulan sanal makineleri için (VM'ler) kullanılabilir [Klasik ve Resource Manager dağıtım modellerinde](../azure-classic-rm.md).

Bkz: [desteklenen platformlar Azure Güvenlik Merkezi'nde](security-center-os-coverage.md) desteklenen platformlar listesi.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Neden Azure Güvenlik Merkezi my Azure VM'de çalışan hello kötü amaçlı yazılımdan koruma çözümünü tanımıyor?
Azure Güvenlik Merkezi Azure uzantılar kötü amaçlı yazılımdan koruma görünürlüğe sahiptir. Örneğin, Güvenlik Merkezi, sağlanan bir görüntüyü veya kendi işlemlerini (örneğin, yapılandırma yönetimi sistemleri) kullanarak, sanal makinelerde kötü amaçlı yazılımdan koruma yüklediyseniz önceden yüklenmiş mümkün toodetect antimalware değil.

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>Neden selamlama iletisine "Tarama verileri eksik" Benim VM için sağlarım?
Bir VM için tarama veri olduğunda bu ileti görüntülenir. Veri toplamayı Azure Güvenlik Merkezi'nde etkinleştirildikten sonra (bir saatten az)'için tarama veri toopopulate'e kadar biraz zaman alabilir. Merhaba ilk popülasyonunu tarama verileri sonra tarama verisi yok hiç veya son tarama veri olduğundan, bu iletiyi alabilirsiniz. Taramaları durdurulmuş bir durumda, bir VM için doldurmayın. Tarama verileri yakın zamanda (uygun olarak 30 gün varsayılan değeri olan hello Windows Aracısı hello bekletme ilkesi) doldurulmuş değil, bu iletiyi de görüntülenebilir.

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>Merhaba ileti "VM Aracısı eksik mi?" neden alıyorum
VM'ler tooenable veri toplama Hello VM Aracısı'nın yüklü olması gerekir. Merhaba VM Aracısı, Azure Marketi hello dağıtılan VM'ler için varsayılan olarak yüklenir. Merhaba blog gönderisi nasıl tooinstall hello diğer vm'lerde VM Aracısı hakkında daha fazla bilgi için bkz [VM aracısı ve Uzantılar](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).
