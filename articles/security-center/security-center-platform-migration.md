---
title: "Güvenlik Merkezi platformu geçiş aaaAzure | Microsoft Docs"
description: "Bu belge, bazı değişiklikler toohello şekilde Azure Güvenlik Merkezi veri toplanan açıklar."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Azure Güvenlik Merkezi platform geçişi

İçinde erken Haziran 2017'den itibaren Azure Güvenlik Merkezi değişiklikleri toohello şekilde güvenlik verileri toplanan ve depolanan önemli yapar.  Bu değişiklikler hello özelliği tooeasily arama güvenlik verileri gibi yeni özellikler kilidini açın ve diğer Azure yönetimi ve hizmetlerini izleme ile daha iyi hizalar.

> [!NOTE]
> Merhaba platform geçiş Üretim kaynaklarınızla etkileyen değil ve hiçbir eylem, taraftan gerekli değildir.


## <a name="whats-happening-during-this-platform-migration"></a>Bu platform geçişi sırasında ne oluyor?

Daha önce Güvenlik Merkezi hello Azure Monitoring Agent toocollect güvenlik Vm'leriniz verilerden kullanılır. Bu, kullanılan tooidentify güvenlik açıkları olan güvenlik yapılandırmalarını ve kullanılan toodetect tehdit güvenlik olayları hakkında bilgi içerir. Bu veriler, Azure’daki Depolama hesabınızda veya hesaplarınızda saklanıyordu.

Güvenlik Merkezi, Microsoft İzleme Aracısı – hello kullanır ileride hello Operations Management Suite ve günlük analizi hizmeti tarafından kullanılan aynı aracı hello budur. Bu Aracıdan toplanan verileri ya da var olan içinde depolanan *günlük analizi* [çalışma](../log-analytics/log-analytics-manage-access.md) hesabı hello coğrafi konuma hello VM, alma, Azure aboneliğinizin veya yeni bir çalışma alanları ile ilişkili .

## <a name="agent"></a>Aracı

Microsoft Monitoring Agent hello geçişin bir parçası olarak hello (için [Windows](../log-analytics/log-analytics-windows-agents.md) veya [Linux](../log-analytics/log-analytics-linux-agents.md)) içinden veri şu anda toplanır tüm Azure VM'ler üzerinde yüklü.  VM hello yüklü, Microsoft İzleme Aracısı zaten hello Güvenlik Merkezi hello geçerli yararlanır aracısının yüklü.

Bir süre (genellikle birkaç gün), her iki aracıları yan yana tooensure veri kaybı olmadan sorunsuz bir geçiş çalıştırın. Bu Microsoft etkinleştirecek yeni veri ardışık hello toovalidate işletimsel hello geçerli ardışık düzen kullanımını sona erdirme önce. Bir kez doğrulanmış hello Azure Monitoring Agent, VM'lerin kaldırılacak. Sizin herhangi bir iş yapmanız gerekmez. Tüm müşterilerin geçişi tamamlandıktan sonra bir e-posta bildirimi alırsınız.
 
Güvenlik veri boşlukları sonuçlanabilir gibi hello Azure Monitoring Agent hello geçiş sırasında el ile kaldırmanız önerilmez. Daha fazla yardıma ihtiyacınız varsa lütfen [Microsoft Müşteri Hizmetleri ve Destek](https://support.microsoft.com/contactus/) birimine başvurun. 

Microsoft İzleme Aracısı için Windows Hello kullan TCP bağlantı noktası 443, okuma gerektirir [Azure Güvenlik Merkezi sorun giderme kılavuzu](security-center-troubleshooting-guide.md) daha fazla bilgi için.


> [!NOTE] 
> Ne zaman Hello Microsoft Monitoring Agent diğer Azure Yönetimi tarafından kullanılabilir ve hizmetlerini izleme, hello Aracısı otomatik olarak kaldırılacak değil çünkü Güvenlik Merkezi'nde veri toplamayı devre dışı bırakma. Ancak, el ile Merhaba Aracısı gerekirse kaldırabilirsiniz.

## <a name="workspace"></a>Çalışma alanı

Microsoft Monitoring Agent (adına, Güvenlik Merkezi) ya da bir var olan günlük analizi içinde depolanan hello'den toplanan verileri daha önce açıklandığı gibi çalışma alanları, Azure aboneliğinizin veya hesap hello alarak yeni bir çalışma alanları ile ilişkili Merhaba VM, coğrafi konum.

Hello Azure portal, toosee herhangi bir Güvenlik Merkezi tarafından oluşturulan dahil olmak üzere, günlük analizi çalışma alanları listesini göz atabilirsiniz. Yeni çalışma alanları için bir ilgili kaynak grubu oluşturulur. İkisi de şu adlandırma kuralını izler:

- Çalışma Alanı: *DefaultWorkspace-[abonelik-kimliği]-[bölge]*
- Kaynak Grubu: *DefaultResouceGroup-[bölge]* 
 
Güvenlik Merkezi tarafından oluşturulan çalışma alanları için veriler 30 gün boyunca tutulur. Varolan çalışma alanları için bekletme hello çalışma alanında fiyatlandırma katmanını temel alır.

> [!NOTE]
> Güvenlik Merkezi tarafından daha önce toplanan veriler Depolama hesaplarınızda kalır. Merhaba geçiş tamamlandıktan sonra bu depolama hesapları silebilirsiniz.

### <a name="oms-security-solution"></a>OMS Güvenlik Çözümü 

OMS Güvenlik Çözümü, çözümü yüklememiş olan mevcut müşterilerin çalışma alanına Microsoft tarafından yalnızca Azure VM’lerini hedefleyecek şekilde yükleniyor. OMS yönetim konsolundan bu çözümün kaldırılması otomatik olarak düzeltilemeyen bir işlem olduğundan, bunun yapılması önerilmez.


## <a name="other-updates"></a>Diğer güncelleştirmeler

Merhaba platform geçiş ile birlikte, biz bazı ek küçük güncelleştirmeler geri:

- Ek işletim sistemi sürümleri desteklenecek. Merhaba listesine bakın [burada](security-center-faq.md#virtual-machines).
- işletim sistemi güvenlik açıklarının Hello listesi genişletilir. Merhaba listesine bakın [burada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- [Fiyatlandırma](https://azure.microsoft.com/pricing/details/security-center/) saatlere eşit olarak bölünecek (önceden günlere bölünüyordu) ve bu sayede bazı müşteriler tasarruf edebilecek.
- Veri toplama gereklidir ve hello standart fiyatlandırma katmanında müşterileri için otomatik olarak etkinleştirilir.
- Azure Güvenlik Merkezi, Azure uzantıları aracılığıyla dağıtılmamış kötü amaçlı yazılım çözümlerini bulmaya başlayacak. İlk olarak Symantec Endpoint Protection ve Windows 2016 için Defender’ı bulma özelliği kullanılabilecek.
- Önleme ilkelerini ve bildirimler yalnızca hello yapılandırılabilir *abonelik* düzey ancak fiyatlandırma hala ayarlanabilir hello *kaynak grubu* düzeyi

