---
title: "aaaAzure Güvenlik Merkezi ve Azure sanal makineleri | Microsoft Docs"
description: "Bu belge toounderstand yardımcı olur nasıl Azure Güvenlik Merkezi, Azure sanal makineleri koruma."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Azure Güvenlik Merkezi ve Azure Sanal Makineler
[Azure Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/) engellemenize, algılamanıza ve toothreats yanıt yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Bu makalede Güvenlik Merkezi’nin Azure Sanal Makinelerinizi (VM) güvenli hale getirmeye nasıl yardımcı olduğu gösterilmektedir.

## <a name="why-use-security-center"></a>Güvenlik Merkezi neden kullanılır?
Güvenlik Merkezi, sanal makinenizin güvenlik ayarlarını görüntüleme olanağı sağlayarak Azure’da sanal makine verilerini korumanıza yardımcı olur. Güvenlik Merkezi Vm'lerinizi koruma sağlar, özellikleri aşağıdaki hello kullanılabilir:

* Yapılandırma kuralları önerilen hello ile işletim sistemi (OS) güvenlik ayarları
* Sistem güvenliği ve eksik olan kritik güncelleştirmeler
* Uç nokta koruması önerileri
* Disk şifreleme doğrulaması
* Güvenlik açığı değerlendirme ve düzeltme
* Tehdit algılama

Ayrıca toohelping koruma yazılımını Azure Vm'leriniz, Güvenlik Merkezi güvenlik izleme ve yönetim bulut Hizmetleri, uygulama hizmetleri, sanal ağlar ve daha fazlası için de sağlar. 

> [!NOTE]
> Bkz: [giriş tooAzure Güvenlik Merkezi](security-center-intro.md) toolearn Azure Güvenlik Merkezi hakkında daha fazla bilgi.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Azure Güvenlik Merkezi ile çalışmaya tooget ve tooknow gerekir hello aşağıdakileri göz önünde bulundurun:

* Abonelik tooMicrosoft Azure olması gerekir. Güvenlik Merkezi’nin ücretsiz ve standart katmanları hakkında daha fazla bilgi için bkz. [Güvenlik Merkezi Fiyatlandırması](https://azure.microsoft.com/pricing/details/security-center/).
* Güvenlik Merkezi'ni benimsemeyi planlama, bkz: [Azure Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) toolearn planlama ve işlemler ilgili önemli noktalar hakkında daha fazla bilgi.
* İşletim sistemi desteklenebilirliği ile ilgili daha fazla bilgi için bkz. [Azure Güvenlik Merkezi hakkında sık sorulan sorular (SSS)](security-center-faq.md). 

## <a name="set-security-policy"></a>Güvenlik ilkesi ayarlama
Bu Azure Güvenlik Merkezi tooprovide önerileri ve oluşturulan uyarılar ihtiyaç hello bilgilerini toplayabilirsiniz şekilde etkin veri toplama gereksinimlerini toobe yapılandırdığınız hello güvenlik ilkesini temel alarak. Merhaba aşağıdaki şekilde, görebilirsiniz **veri toplama** kapatılmış **üzerinde**.

Bir güvenlik ilkesi hello hello belirtilen abonelik veya kaynak grubu içindeki kaynaklar için önerilen denetimleri kümesini tanımlar. Güvenlik ilkesini etkinleştirme önce sanal makinelerinizi Güvenlik Merkezi topladığı verileri güvenlik durumlarına güvenlik önerileri sağlamak ve toothreats uyarı tooassess sipariş, etkin veri toplama olmalıdır. Güvenlik Merkezi'nde Azure Abonelikleriniz veya kaynak grupları tooyour şirketin güvenlik gereksinimlerini ve uygulamaların hello türü veya hello her Abonelikteki verilerin duyarlılığına göre ilkeleri tanımlarsınız. 

![Güvenlik ilkesi](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> Her hakkında daha fazla toolearn **önleme İlkesi** kullanılabilir, bkz: [güvenlik ilkelerini ayarlama](security-center-policies.md) makalesi.
> 
> 

## <a name="manage-security-recommendations"></a>Güvenlik önerilerini yönetme
Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur. Merhaba önerileri gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk.

Bir güvenlik ilkesi ayarladıktan sonra Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenlik durumunu çözümler. Merhaba öneriler her satırın belirli bir önerinin temsil ettiği bir tablo biçiminde gösterilir. Aşağıdaki Hello tablo bazı örnekler Azure Vm'leri ve onu uygularsanız her birini ne yapacağını öneriler sağlar. Bir öneri seçtiğinizde nasıl tooimplement hello öneri Güvenlik Merkezi'nde gösterilir bilgi sağlanacaktır.

| Öneri | Açıklama |
| --- | --- |
| [Abonelikler için veri toplamayı etkinleştirin](security-center-enable-data-collection.md) |Her aboneliğiniz ve tüm sanal makineleri (VM'ler) için veri toplama hello Güvenlik İlkesi'nde aboneliklerinizde kapatmanız olmasını önerir. |
| [İşletim sistemi güvenlik açıklarını düzeltin](security-center-remediate-os-vulnerabilities.md) |Yapılandırma kuralları, önerilen hello ile işletim sistemi yapılandırmalarını Hizala önerir örn izin verme parolaları toobe kaydedildi. |
| [Sistem güncelleştirmelerini uygulayın](security-center-apply-system-updates.md) |Eksik sistem güvenlik ve kritik güncelleştirmeler tooVMs dağıtmanızı önerir. |
| [Sistem güncelleştirmelerinden sonra yeniden başlatın](security-center-apply-system-updates.md#reboot-after-system-updates) |Sistemi güncelleştirmelerini uygulama VM toocomplete hello işlemi yeniden önerir. |
| [Endpoint Protection’ı yükleyin](security-center-install-endpoint-protection.md) |Kötü amaçlı yazılımdan koruma programları tooVMs (yalnızca Windows VM) sağlamasını önerir. |
| [Endpoint Protection sistem durumu uyarılarını çözümleyin](security-center-resolve-endpoint-protection-health-alerts.md) |Endpoint protection hatalarını gidermenizi önerir. |
| [VM Aracısını etkinleştirin](security-center-enable-vm-agent.md) |Sanal makineleri gerektiren, toosee hello VM Aracısı etkinleştirir. Merhaba VM Aracısı Vm'lerinde tarama, tarama temel ve kötü amaçlı yazılımdan koruma programları sipariş tooprovision düzeltme yüklü olması gerekir. Merhaba VM Aracısı, Azure Marketi hello dağıtılan VM'ler için varsayılan olarak yüklenir. Merhaba makale [VM aracısı ve uzantılar – Kısım 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) nasıl tooinstall hello üzerinde VM aracısı bilgi sağlar. |
| [Disk şifrelemesi uygulayın](security-center-apply-disk-encryption.md) |Azure Disk Şifrelemesi kullanarak VM’nizi şifrelemenizi önerir (Windows ve Linux VM’leri). Şifreleme hello işletim sistemi ve veri birimlerine, VM için önerilir. |
| [Güvenlik açığı değerlendirmesi yüklü değil](security-center-vulnerability-assessment-recommendations.md) |Sanal makinenize bir güvenlik açığı değerlendirme çözümü yüklemenizi önerir. |
| [Güvenlik açıklarını düzeltin](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Toosee sistem ve uygulama güvenlik açıkları, VM'de yüklü hello güvenlik açığı değerlendirmesi çözüm tarafından algılanan sağlar. |

> [!NOTE]
> toolearn öneriler hakkında daha fazla bilgi görmek [güvenlik önerilerini yönetme](security-center-recommendations.md) makalesi.
> 
> 

## <a name="monitor-security-health"></a>Güvenlik durumunu izleme
Etkinleştirdikten sonra [güvenlik ilkeleri](security-center-policies.md) bir aboneliğin kaynakları için Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenliğini analiz eder.  Merhaba herhangi bir sorun yanı sıra kaynaklarınızın güvenlik durumunu hello görüntüleyebilirsiniz **kaynak güvenlik durumu** dikey. Tıkladığınızda **sanal makineleri** hello içinde **kaynak güvenlik** durumu kutucuğu, hello **sanal makineleri** Vm'leriniz için öneriler dikey penceresi açılır. 

![Güvenlik durumu](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Yönetme ve yanıtlama toosecurity uyarıları
Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve bağlı iş ortağı çözümleri (güvenlik duvarı ve endpoint protection çözümleri gibi), günlük verilerini tümleştirir toodetect gerçek tehditleri ve hatalı pozitif sonuçları azaltmak. Farklı bir toplama yararlanarak [algılama özellikleri](security-center-detection-capabilities.md), güvenlik merkezidir mümkün toogenerate öncelikli güvenlik uyarıları toohelp hızlı bir şekilde hello sorununu araştırın ve nasıl için öneri sağlama tooremediate olası saldırıları.

![Güvenlik uyarıları](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Bir güvenlik uyarısı toolearn seçin, adımlar varsa tetikleyen hello uyarı ve hangi hello olaylar hakkında daha fazla tootake tooremediate saldırının gerekiyor. Güvenlik uyarıları, [türe](security-center-alerts-type.md) ve tarihe göre gruplandırılır.

## <a name="see-also"></a>Ayrıca bkz.
Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.

