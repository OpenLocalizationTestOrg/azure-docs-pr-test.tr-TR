---
title: "Azure Güvenlik Merkezi'nde güvenlik önerilerini aaaManaging | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi'nde öneriler, Azure kaynaklarınızı korumanıza ve güvenlik ilkeleriyle uyumlu kalın nasıl yardımcı aracılığıyla açıklanmaktadır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme
Bu belge, nasıl Azure Güvenlik Merkezi toohelp toouse önerileri koruma aracılığıyla anlatan Azure kaynaklarınızı.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu belge hakkında adım adım kılavuz değildir.
>
>

## <a name="what-are-security-recommendations"></a>Güvenlik önerileri nelerdir?
Güvenlik Merkezi düzenli aralıklarla hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur. Merhaba önerileri gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk.

## <a name="implementing-security-recommendations"></a>Güvenlik önerilerini uygulama
### <a name="set-recommendations"></a>Ayarlama önerileri
İçinde [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md), getirmeyi öğrenin:

* Güvenlik ilkeleri yapılandırın.
* Veri koleksiyonunu Aç.
* Güvenlik ilkenizin bir parçası olarak hangi önerileri toosee seçin.

Geçerli ilke önerileri Merkezi sistem güncelleştirmeleri, temel kurallar, kötü amaçlı yazılımdan koruma programları etrafında [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) alt ağlar ve ağ arabirimleri, SQL veritabanı denetimi, SQL veritabanında saydam veri şifrelemesi web uygulaması güvenlik duvarı ve.  [Güvenlik ilkelerini ayarlama](security-center-policies.md) her öneri seçeneği açıklamasını sağlar.

### <a name="monitor-recommendations"></a>İzleyici önerileri
Bir güvenlik ilkesi ayarladıktan sonra Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenlik durumunu çözümler. Merhaba **önerileri** döşeme hello üzerinde **Güvenlik Merkezi** dikey penceresinde hello Güvenlik Merkezi tarafından tanımlanan önerileri toplam sayısını bilmek olanak sağlar.

![Öneriler döşeme][1]

Her öneri toosee hello ayrıntıları:

Select hello **önerileri döşeme** hello üzerinde **Güvenlik Merkezi** dikey. Merhaba **önerileri** dikey pencere açılır.

Merhaba öneriler her satırın belirli bir önerinin temsil ettiği bir tablo biçiminde gösterilir. Bu tablonun sütunlarının Hello şunlardır:

* **Açıklama**: hello öneri ve tooaddress bitti toobe gerekenler açıklanmaktadır.
* **Kaynak**: listeler hello kaynakları toowhich Bu öneri uygular.
* **Durum**: hello hello öneri geçerli durumunu açıklar:
  * **Açık**: hello öneri kurmadı ele henüz.
  * **Devam eden**: hello öneri yüklenmekte olduğu uygulanan toohello kaynakları ve herhangi bir işlem yapmanız gerekmez.
  * **Çözümlenen**: hello öneri zaten tamamlanmış (Bu durumda, hello satır gri renkte görüntülenir).
* **Önem DERECESİ**: belirli bir önerinin hello önemini açıklar:
  * **Yüksek**: bir güvenlik açığı (örneğin, bir uygulama, bir VM veya bir ağ güvenlik grubu) anlamlı bir kaynakta var ve dikkat gerektiriyor.
  * **Orta**: bir güvenlik açığı var ve kritik olmayan veya ek adımlardır gerekli tooeliminate veya toocomplete bir işlem.
  * **Düşük**: bir güvenlik açığı bulunduğunu ele alınması gerekiyor ancak hemen ilgilenilmesi gerekmiyor. (Varsayılan olarak, düşük öneriler sunulan değil, ancak toosee istiyorsanız düşük öneriler filtresini kullanabilirsiniz bunları.)

Bir başvuru toohelp olarak kullanımı hello tablo aşağıda hello kullanılabilir önerileri ve onu uygularsanız her birini ne yaptığını anlayın.

> [!NOTE]
> Toounderstand hello isteyeceksiniz [Klasik ve Resource Manager dağıtım modellerinde](../azure-classic-rm.md) Azure kaynakları için.
>
>

| Öneri | Açıklama |
| --- | --- |
| [Abonelikler için veri toplamayı etkinleştirin](security-center-enable-data-collection.md) |Her aboneliğiniz ve tüm sanal makineleri (VM'ler) için veri toplama hello Güvenlik İlkesi'nde aboneliklerinizde kapatmanız olmasını önerir. |
| [İşletim sistemi güvenlik açıklarını düzeltin](security-center-remediate-os-vulnerabilities.md) |Yapılandırma kuralları, örneğin önerilen hello ile işletim sistemi yapılandırmalarını Hizala, kaydedilen parolaları toobe izin verme önerir. |
| [Sistem güncelleştirmelerini uygulayın](security-center-apply-system-updates.md) |Eksik sistem güvenlik ve kritik güncelleştirmeler tooVMs dağıtmanızı önerir. |
| [Bir sadece zaman içinde geçerli ağ erişim denetimi](security-center-just-in-time.md) | Yalnızca süresi VM erişimi uygulamanızı önerir. yalnızca zaman özellik Hello önizlemede hello Güvenlik Merkezi'nin standart katmanı üzerinde kullanılabilir. Bkz: [fiyatlandırma](security-center-pricing.md) toolearn Güvenlik Merkezi hakkında daha fazla fiyatlandırma katmanları. |
| [Sistem güncelleştirmelerinden sonra yeniden başlatın](security-center-apply-system-updates.md#reboot-after-system-updates) |Sistemi güncelleştirmelerini uygulama VM toocomplete hello işlemi yeniden önerir. |
| [Web uygulaması güvenlik duvarı ekleme](security-center-add-web-application-firewall.md) |Web uç noktaları için web uygulaması Güvenlik Duvarı (WAF) dağıtmak önerir. WAF öneri açık gelen web bağlantı noktaları (80,443) içeren bir ilişkili ağ güvenlik grubu olan tüm genel kullanıma yönelik IP'si için (örnek düzeyinde IP veya yük dengeli IP) gösterilir. </br>Güvenlik Merkezi WAF toohelp provizyon sanal makineler ve uygulama hizmeti ortamı, web uygulamalarınızı hedefleyen saldırılara karşı korumaya önerir. Uygulama hizmeti ortamı (ana) olan bir [Premium](https://azure.microsoft.com/pricing/details/app-service/) hizmet planı seçeneği Azure App Service, güvenli bir şekilde Azure App Service uygulamalarını çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlar. toolearn ana, hakkında daha fazla bilgi görmek hello [uygulama hizmeti ortamı belgeleri](../app-service/app-service-app-service-environments-readme.md).</br>Bu uygulamalar tooyour varolan WAF dağıtımlar ekleyerek, birden çok web uygulamasına Güvenlik Merkezi'nde koruyabilirsiniz. |
| [Uygulama korumasını sonlandırma](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello yapılandırmasını WAF, trafiği yeniden yönlendirilen toohello WAF Gereci olması gerekir. Bu öneri aşağıdaki hello gerekli Kurulum değişiklikleri tamamlar. |
| [Yeni Nesil Güvenlik Duvarı ekleme](security-center-add-next-generation-firewall.md) |Güvenlik korumaları bir Microsoft iş ortağı tooincrease İleri nesil Güvenlik Duvarı (NGFW) eklemek önerir. |
| [Trafiği yalnızca NGFW aracılığıyla yönlendirme](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Gelen trafik tooyour, NGFW aracılığıyla VM zorla ağ güvenlik grubu (NSG) kurallarını yapılandırmak önerir. |
| [Endpoint Protection’ı yükleyin](security-center-install-endpoint-protection.md) |Kötü amaçlı yazılımdan koruma programları tooVMs (yalnızca Windows VM) sağlamasını önerir. |
| [Endpoint Protection sistem durumu uyarılarını çözümleyin](security-center-resolve-endpoint-protection-health-alerts.md) |Endpoint protection hatalarını gidermenizi önerir. |
| [Ağ güvenlik grupları alt ağları veya sanal makinelerde etkinleştir](security-center-enable-network-security-groups.md) |Nsg'ler alt ağları veya VM'ler etkinleştirmenizi önerir. |
| [Uç nokta Internet'e aracılığıyla erişimi kısıtlama](security-center-restrict-access-through-internet-facing-endpoints.md) |İçin Nsg'ler gelen trafik kurallarını yapılandırmak önerir. |
| [SQL sunucularında denetim ve tehdit algılamayı etkinleştirme](security-center-enable-auditing-on-sql-servers.md) |Azure SQL sunucuları için Denetim ve tehdit algılama Aç önerir. (Yalnızca azure SQL Hizmeti. Sanal makinelerde çalışan SQL içermez.) |
| [SQL veritabanlarında denetim ve tehdit algılamayı etkinleştirme](security-center-enable-auditing-on-sql-databases.md) |Azure SQL veritabanı için Denetim ve tehdit algılama Aç önerir. (Yalnızca azure SQL Hizmeti. Sanal makinelerde çalışan SQL içermez.) |
| [SQL veritabanlarını saydam veri şifreleme etkinleştir](security-center-enable-transparent-data-encryption.md) |SQL veritabanları için şifrelemeyi etkinleştirmek önerir. (Yalnızca azure SQL Hizmeti.) |
| [VM Aracısını etkinleştirin](security-center-enable-vm-agent.md) |Sanal makineleri gerektiren, toosee hello VM Aracısı etkinleştirir. Tarama, tarama temel ve kötü amaçlı yazılımdan koruma programları VM'ler tooprovision düzeltme ekini Hello VM Aracısı'nın yüklü olması gerekir. Merhaba VM Aracısı, Azure Marketi hello dağıtılan VM'ler için varsayılan olarak yüklenir. Merhaba makale [VM aracısı ve uzantılar – Kısım 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) nasıl tooinstall hello üzerinde VM aracısı bilgi sağlar. |
| [Disk şifrelemesi uygulayın](security-center-apply-disk-encryption.md) |Azure Disk Şifrelemesi kullanarak VM’nizi şifrelemenizi önerir (Windows ve Linux VM’leri). Şifreleme hello işletim sistemi ve veri birimlerine, VM için önerilir. |
| [Güvenlik ilgili kişi bilgilerini belirtin](security-center-provide-security-contact-details.md) |Güvenlik sağlamasını önerir bilgi her aboneliğiniz için başvurun. Bir e-posta adresi ve telefon numarası iletişim bilgileridir. Merhaba kullanılan toocontact bilgidir, güvenlik ekibimiz kaynaklarınızı riske atılması bulursa. |
| [İşletim sistemi sürümünü güncelleştirme](security-center-update-os-version.md) |İşletim sistemi ailesi için bulut hizmet toohello en son sürümü için kullanılabilir hello işletim sistemi (OS) sürümünü güncelleştirme önerir.  Bulut hizmetleri hakkında daha fazla toolearn bkz hello [bulut hizmetlerine genel bakış](../cloud-services/cloud-services-choose-me.md). |
| [Güvenlik açığı değerlendirmesi yüklü değil](security-center-vulnerability-assessment-recommendations.md) |Sanal makinenize bir güvenlik açığı değerlendirme çözümü yüklemenizi önerir. |
| [Güvenlik açıklarını düzeltin](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Toosee sistem ve uygulama güvenlik açıkları, VM'de yüklü hello güvenlik açığı değerlendirmesi çözüm tarafından algılanan sağlar. |
| [Azure depolama hesabı için şifrelemeyi etkinleştir](security-center-enable-encryption-for-storage-account.md) | Rest verileri için Azure depolama hizmeti şifrelemesi etkinleştirmenizi önerir. Depolama hizmeti şifreleme (SSE) tooAzure depolama yazılır ve alma önce şifresini çözer hello verileri şifreleyerek çalışır. SSE yalnızca hello Azure Blob hizmeti şu anda kullanılabilir değil ve blok blobları, sayfa bloblarını kullanılabilir ve ekleme blobları. toolearn daha, fazla [bekleyen veri için depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md).</br>SSE yalnızca Resource Manager depolama hesaplarında desteklenir. |

Filtre uygulayabilir ve öneriler yok sayın.

1. Seçin **filtre** hello üzerinde **önerileri** dikey. Merhaba **filtre** dikey penceresi açılır ve toosee istediğiniz hello önem ve durum değerleri seçin.

    ![Filtre önerileri][2]
2. Bir öneri uygulanamaz olarak belirlerseniz, hello öneri yok sayın ve görünümünüzü dışında filtre. Bir öneri iki yolu toodismiss vardır. Bir yolu tooright'ü tıklatın bir öğeyi ve ardından **atla**. Merhaba diğer toohover bir öğenin üzerine, toohello sağ görünür ve ardından hello üç noktaya tıklayın **atla**. Kapatıldı önerileri tıklatarak görüntüleyebileceğiniz **filtre**ve ardından seçerek **çıkarıldı**.

    ![Öneri yok sayın][3]

### <a name="apply-recommendations"></a>Önerileri geçerlidir
Tüm önerileri gözden geçirdikten sonra bir önce uygulamanız karar verebilirsiniz. Hangi önerileri önce uygulanması gereken ana parametre tooevaluate hello gibi hello önem derecesi kullanmanızı öneririz.

Yukarıdaki önerileri Merhaba tablonun bir öneri seçin ve bir örnek olarak size yol tooapply bir öneri.

## <a name="next-steps"></a>Sonraki adımlar
Bu belgede, Güvenlik Merkezi'nde sunulan toosecurity önerileri yoktu. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
