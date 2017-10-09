---
title: "aaaProtecting sanal makinelerinizi Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Yardımcı olacak öneriler Azure Güvenlik Merkezi'nde, sanal makinelerin korunmasına ve güvenlik ilkeleriyle uyumlu olmak bu belge adresleri."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde, sanal makineleri koruma
Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk öneriler oluşturur.  Önerileri tooAzure kaynak türleri geçerlidir: sanal ağ, SQL ve uygulamaları makineleri (VM'ler).

Bu makalede tooVMs uygulamak önerileri giderir.  VM önerileri merkezi veri toplama, kötü amaçlı yazılımdan koruma, sağlama sistemi güncelleştirmelerini uygulama etrafında VM disklerinizi ve daha fazlasını şifreleme.  Aşağıda kullanım hello tablo başvurusu toohelp olarak hello kullanılabilir VM önerileri ve onu uygularsanız her birini ne yapacağını anlamak.

## <a name="available-vm-recommendations"></a>Kullanılabilir VM önerileri
| Öneri | Açıklama |
| --- | --- |
| [Abonelikler için veri toplamayı etkinleştirin](security-center-enable-data-collection.md) |Her aboneliğiniz ve tüm sanal makineleri (VM'ler) için veri toplama hello Güvenlik İlkesi'nde aboneliklerinizde kapatmanız olmasını önerir. |
| [Azure depolama hesabı için şifrelemeyi etkinleştir](security-center-enable-encryption-for-storage-account.md) | Rest verileri için Azure depolama hizmeti şifrelemesi etkinleştirmenizi önerir. Depolama hizmeti şifreleme (SSE) tooAzure depolama yazılır ve alma önce şifresini çözer hello verileri şifreleyerek çalışır. SSE yalnızca hello Azure Blob hizmeti şu anda kullanılabilir değil ve blok blobları, sayfa bloblarını kullanılabilir ve ekleme blobları. toolearn daha, fazla [bekleyen veri için depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md).</br>SSE yalnızca Resource Manager depolama hesaplarında desteklenir. Klasik depolama hesapları şu anda desteklenmemektedir. toounderstand hello Klasik ve Resource Manager dağıtım modellerinde bkz [Azure dağıtım modelleri](../azure-classic-rm.md). |
| [İşletim sistemi güvenlik açıklarını düzeltin](security-center-remediate-os-vulnerabilities.md) |Yapılandırma kuralları, önerilen hello ile işletim sistemi yapılandırmalarını Hizala önerir örn izin verme parolaları toobe kaydedildi. |
| [Sistem güncelleştirmelerini uygulayın](security-center-apply-system-updates.md) |Eksik sistem güvenlik ve kritik güncelleştirmeler tooVMs dağıtmanızı önerir. |
| [Bir sadece zaman içinde geçerli ağ erişim denetimi](security-center-just-in-time.md) | Yalnızca süresi VM erişimi uygulamanızı önerir. yalnızca zaman özellik Hello önizlemede hello Güvenlik Merkezi'nin standart katmanı üzerinde kullanılabilir. Bkz: [fiyatlandırma](security-center-pricing.md) toolearn Güvenlik Merkezi hakkında daha fazla fiyatlandırma katmanları. |
| [Sistem güncelleştirmelerinden sonra yeniden başlatın](security-center-apply-system-updates.md#reboot-after-system-updates) |Sistemi güncelleştirmelerini uygulama VM toocomplete hello işlemi yeniden önerir. |
| [Endpoint Protection’ı yükleyin](security-center-install-endpoint-protection.md) |Kötü amaçlı yazılımdan koruma programları tooVMs (yalnızca Windows VM) sağlamasını önerir. |
| [Endpoint Protection sistem durumu uyarılarını çözümleyin](security-center-resolve-endpoint-protection-health-alerts.md) |Endpoint protection hatalarını gidermenizi önerir. |
| [VM Aracısını etkinleştirin](security-center-enable-vm-agent.md) |Sanal makineleri gerektiren, toosee hello VM Aracısı etkinleştirir. Merhaba VM Aracısı Vm'lerinde tarama, tarama temel ve kötü amaçlı yazılımdan koruma programları sipariş tooprovision düzeltme yüklü olması gerekir. Merhaba VM Aracısı, Azure Marketi hello dağıtılan VM'ler için varsayılan olarak yüklenir. Merhaba makale [VM aracısı ve uzantılar – Kısım 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) nasıl tooinstall hello üzerinde VM aracısı bilgi sağlar. |
| [Disk şifrelemesi uygulayın](security-center-apply-disk-encryption.md) |Azure Disk Şifrelemesi kullanarak VM’nizi şifrelemenizi önerir (Windows ve Linux VM’leri). Şifreleme hello işletim sistemi ve veri birimlerine, VM için önerilir. |
| [İşletim sistemi sürümünü güncelleştirme](security-center-update-os-version.md) |İşletim sistemi ailesi için bulut hizmet toohello en son sürümü için kullanılabilir hello işletim sistemi (OS) sürümünü güncelleştirme önerir.  Bulut hizmetleri hakkında daha fazla toolearn bkz hello [bulut hizmetlerine genel bakış](../cloud-services/cloud-services-choose-me.md). |
| [Güvenlik açığı değerlendirmesi yüklü değil](security-center-vulnerability-assessment-recommendations.md) |Sanal makinenize bir güvenlik açığı değerlendirme çözümü yüklemenizi önerir. |
| [Güvenlik açıklarını düzeltin](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Toosee sistem ve uygulama güvenlik açıkları, VM'de yüklü hello güvenlik açığı değerlendirmesi çözüm tarafından algılanan sağlar. |

## <a name="see-also"></a>Ayrıca bkz.
toolearn tooother Azure kaynak türleri bkz hello aşağıdaki öneriler hakkında daha fazla bilgi:

* [Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma](security-center-application-recommendations.md)
* [Azure Güvenlik Merkezi, ağınızda koruma](security-center-network-recommendations.md)
* [Azure SQL hizmetinizi Azure Güvenlik Merkezi'nde koruma](security-center-sql-service-recommendations.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
