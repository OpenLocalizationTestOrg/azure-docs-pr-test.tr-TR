---
title: aaaPen test | Microsoft Docs
description: "Merhaba makale (pentest) işlem sınama hello sızma genel bir bakış sağlar ve uygulamalarınızı Azure altyapısında çalışan karşı pentest nasıl gerçekleştirin."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>Kalem test etme
Uygulama test ve dağıtım için Microsoft Azure kullanma konusunda hello harika şeylerden biri olan bir şirket içi altyapı toodevelop birlikte tooput gerekmez, test ve uygulamalarınızı dağıtma. Tüm hello altyapısı tarafından hello Microsoft Azure platform hizmetlerini dikkate. Requisitioning, alma, "racking ve yığınlama" hakkında tooworry yoksa, kendi şirket içi donanım.

Bu harika –, ancak yine de toomake normal güvenlik gerçekleştirdiğiniz emin gerekir durum tespitlerini. Bir gereksinim duyduğunuz hello şey Azure'da dağıtımı sızma test hello uygulamaları toodo olduğu.

Microsoft yaptığı zaten biliyor olabilirsiniz [bizim Azure ortamının sızma testi](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e). Bu bizim platform geliştirmemize yardımcı olur ve güvenlik denetimleri geliştirme, yeni güvenlik denetimleri tanıtımı ve bizim güvenlik işlemleri geliştirme açısından bizim Eylemler size yol gösterir.

Kalem yok, uygulamanızı test etmek, ancak biz, istediğiniz ve tooperform kalem kendi uygulamaları sınama gerekiyor olduğunu anlamak. Uygulamalarınızın hello güvenliğini, hello tüm Azure ekosistemi daha güvenli olmasına yardımcı olmak için iyi bir şey olmasıdır.

Uygulamalarınızı, kalem test ederken bir saldırı toous gibi görünebilir. Biz [sürekli izleme](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) için saldırı desenleri ve biz gerekiyorsa, bir olay yanıtlama işlemi başlatır. Bu işe yaramazsa ve biz bir olay yanıtlama harekete geçirirseniz bize yardımcı değil son tooyour tespitlerini kalem sınama son kendi.

Hangi toodo?

Hazır olduğunuzda toopen test Azure barındırılan uygulamalar, bir seçenek çok sahip[bize bildirin](https://portal.msrc.microsoft.com/en-us/engage/pentest). Belirli testleri gerçekleştirme toobe oluşturacağız öğrendikten sonra biz olmaz yanlışlıkla (test ettiğiniz hello IP adresi engelleme gibi) kapatmak, testlerinizi toohello Azure uygun sürece test hüküm ve koşullar içindeaçıklanankalem[Microsoft bulut birleşik kuralları of katılım sınama sızma](https://technet.microsoft.com/en-us/mt784683).
Standart testler gerçekleştirebileceğiniz içerir:

* Uç noktaları toouncover hello testleri [açık Web uygulaması güvenlik proje (OWASP) ilk 10 güvenlik açıkları](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Rastgele test](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) , uç noktaları
* [Bağlantı noktası tarama](https://en.wikipedia.org/wiki/Port_scanner) , uç noktaları

Bir işlemi gerçekleştiremezsiniz test türünde herhangi bir tür [hizmet reddi (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) saldırı. Bu bir DoS saldırısı başlatmasını veya belirlemek, göstermek veya DoS saldırısı herhangi bir türde benzetimini ilgili testleri gerçekleştirme içerir.

Microsoft Azure üzerinde barındırılan uygulamalarınızı test etme kalem kullanmaya tooget hazır misiniz? Bunu yeniden toohello üzerinden baş [sızma testi genel bakış](https://technet.microsoft.com/library/mt784683.aspx) sayfa (ve hello Oluştur hello sayfanın hello sonundaki test etme isteği düğmesini tıklatın. Ayrıca hello kalem hüküm ve koşullar ve güvenlik açıkları ilgili tooAzure veya diğer herhangi bir Microsoft hizmeti nasıl raporlayabilirsiniz üzerinde yardımcı bağlantılar test etme hakkında daha fazla bilgi bulabilirsiniz.
