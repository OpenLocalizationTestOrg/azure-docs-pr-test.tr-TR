---
title: "SIEM sistemlerinizi içine Azure kaynaklarını aaaIntegrate günlüklerinden | Microsoft Docs"
description: "Azure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Giriş tooMicrosoft Azure günlük tümleştirme
Azure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin.

## <a name="overview"></a>Genel Bakış

Azure günlük tümleştirme tooyour şirket içi güvenlik bilgileri ve Olay yönetimi (SIEM) sistemlerinde toointegrate ham Azure kaynaklarınızı günlüklerinden sağlayan ücretsiz bir çözümdür.

Azure günlük tümleştirme toplar Windows olaylarını Windows Olay Görüntüleyicisi'ni günlüklerinden [Azure etkinlik günlükleri](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Güvenlik Merkezi uyarılarını](../security-center/security-center-intro.md), ve [Azure tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) gelen Azure kaynakları. Bu tümleştirme tüm varlıklar için birleştirilmiş bir Pano sağlar, SIEM çözümünüzün yardımcı olur, şirket içi veya hello bulutta araya getirebilirsiniz böylece ilişkilendirmek, çözümlemek ve güvenlik olayları için uyarı.

>[!NOTE]
Şu anda yalnızca desteklenen hello Bulutlar ticari Azure ve Azure kamu var. Diğer bulut desteklenmez.

![Azure günlük tümleştirmesi][1]

## <a name="what-logs-can-i-integrate"></a>Hangi günlükleri ı tümleştirebilir miyim?
Azure Azure her hizmet için ayrıntılı günlük kaydını üretir. Bu günlükler günlükleri üç tür temsil eder:

* **Denetim/Yönetim günlüklerini** hello görünürlük sağlayan [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) oluşturma, güncelleştirme ve silme işlemleri. Azure etkinlik günlükleri, günlük bu tür bir örnektir.
* **Veri günlüklerini düzlemine** bir Azure kaynağı hello kullanımını bir parçası olarak oluşturulan hello olaylara görünürlük sağlar. Bu günlük türü hello Windows Olay Görüntüleyicisi'nin örneğidir **sistem**, **güvenlik**, ve **uygulama** Windows sanal makine kanallarında. Azure İzleyicisi aracılığıyla yapılandırılmış Tanılama Günlüğü başka bir örnek verilmiştir
* **İşlenen olayların** çözümlenen olay ve sizin adınıza işlenen uyarı bilgileri sağlar. Azure Güvenlik Merkezi burada ve işlenen abonelik tooprovide uyarılar ilgili tooyour geçerli güvenlikle ilgili tutumunuzu analiz Azure Güvenlik Merkezi uyarılarını, bu olay türü örnektir.

Azure günlük tümleştirme ArcSight, QRadar ve Splunk destekler. Tüm durumlarda, SIEM satıcı tooassess ile yerel bir bağlayıcı yüklü olup olmadığını gözden geçirin. Yerel bağlayıcılar kullanılabilir olduğunda bazı durumlarda, toouse Azure günlük tümleştirme gerekmez. Ziyaret edin türleri hakkında ek bilgi için desteklenen bir günlük SSS hello.

>[!NOTE]
Azure günlük tümleştirme boş bir çözüm olsa da, Azure storage maliyetleri hello günlük dosyası bilgilerini depolama alanından kaynaklanan vardır.

Topluluk Yardım hello kullanılabilir [Azure günlük tümleştirme MSDN Forumu](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Merhaba Forumu hello AzLog topluluk hello özelliği toosupport birbirine sorular ve yanıtlar, ipuçları ve nasıl tooget hello en Azure günlük tümleştirme dışında üzerinde püf noktaları sağlar. Ayrıca, hello Azure günlük tümleştirme takım Bu forumda izler ve geçebiliriz her yardımcı olur.

Ayrıca açabilirsiniz bir [destek isteği](../azure-supportability/how-to-create-azure-support-request.md). toodo Bu, select **günlük tümleştirme** destek isteyen hello hizmet olarak.

## <a name="next-steps"></a>Sonraki adımlar
Bu belgede, sunulan tooAzure günlük tümleştirme yoktu. Azure hakkında daha fazla oturum tümleştirme ve desteklenen, günlük hello türlerini toolearn hello aşağıdaki bakın:

* [Microsoft Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324) – merkezi ayrıntılı bilgi için sistem gereksinimleri, yükleyip yönergeler Azure günlük tümleştirme.
* [Azure günlük tümleştirme ile çalışmaya başlama](security-azure-log-integration-get-started.md) - Bu öğretici, Azure günlük tümleştirme yüklenmesinde size yol gösterir ve Azure WAD depolama, Azure etkinlik günlükleri günlüklerinden tümleştirme Azure Güvenlik Merkezi uyarılarını ve Azure Active Directory denetim günlükleri.
* [Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – bu blog gönderisine nasıl tooconfigure Azure oturum tümleştirme toowork Splunk, HP ArcSight ve IBM QRadar ile iş ortağı çözümlerini gösterir. Bu blog hello iş ortağı çözümleri yapılandırma bizim geçerli konumu temsil eder. Her durumda, Lütfen ilk toopartner çözüm belgelerine bakın.
* [Etkinlik ve ASC uyarıları syslog tooQRadar üzerinden](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – bu blog gönderisine hello adımları toosend etkinliği ve Azure Güvenlik Merkezi uyarıları syslog tooQRadar sağlar
* [Azure günlük sık sorulan sorular (SSS) tümleştirme](security-azure-log-integration-faq.md) -bu SSS Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.
* [Güvenlik Merkezi tümleştirme uyarıları Azure ile tümleştirme oturum](../security-center/security-center-integrating-alerts-with-log-integration.md) – bu belgeyi nasıl toosync Azure Güvenlik Merkezi ile Azure günlük tümleştirme uyarıları gösterir.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
