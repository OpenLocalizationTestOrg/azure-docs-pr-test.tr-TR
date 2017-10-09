---
title: "Azure Güvenlik Merkezi'nde bir web uygulaması güvenlik duvarı aaaAdd | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** bir web uygulaması güvenlik duvarı ** ekleyin ve ** uygulama koruma ** sonlandır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde bir web uygulaması güvenlik duvarı ekleme
Azure Güvenlik Merkezi, web uygulamalarınızı Microsoft iş ortağı toosecure bir web uygulaması Güvenlik Duvarı (WAF) eklemenizi öneririz. Bu belge, nasıl bir örnek üzerinden anlatan tooapply Bu öneri.

WAF öneri açık gelen web bağlantı noktaları (80,443) içeren bir ilişkili ağ güvenlik grubu olan tüm genel kullanıma yönelik IP'si için (örnek düzeyinde IP veya yük dengeli IP) gösterilir.

Güvenlik Merkezi WAF toohelp provizyon sanal makineler ve uygulama hizmeti ortamı, web uygulamalarınızı hedefleyen saldırılara karşı korumaya önerir. Uygulama hizmeti ortamı (ana) olan bir [Premium](https://azure.microsoft.com/pricing/details/app-service/) hizmet planı seçeneği Azure App Service, güvenli bir şekilde Azure App Service uygulamalarını çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlar. toolearn ana, hakkında daha fazla bilgi görmek hello [uygulama hizmeti ortamı belgeleri](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu belge hakkında adım adım kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **güvenli web uygulaması Güvenlik Duvarı'nı kullanarak web uygulamasına**.
   ![Güvenli web uygulaması][1]
2. Merhaba, **web uygulaması Güvenlik Duvarı'nı kullanarak web uygulamalarınızı güvenli** dikey penceresinde, bir web uygulaması seçin. Merhaba **bir Web uygulaması güvenlik duvarı ekleme** dikey pencere açılır.
   ![Web uygulaması güvenlik duvarı ekleme][2]
3. Varsa mevcut bir web uygulaması güvenlik duvarı toouse seçebilir veya yeni bir tane oluşturabilirsiniz. Bu örnekte, yok hiçbir varolan WAFs bir WAF oluşturuyoruz şekilde.
4. toocreate bir WAF hello tümleşik ortakları listesinden bir çözümü seçin. Bu örnekte, biz seçin **Barracuda Web uygulaması güvenlik duvarı**.
5. Merhaba **Barracuda Web uygulaması güvenlik duvarı** dikey pencere açılır hello iş ortağı çözümü hakkında bilgi sağlar. Seçin **oluşturma** hello bilgi dikey penceresinde.

   ![Güvenlik Duvarı bilgileri dikey penceresi][3]

6. Merhaba **yeni Web uygulaması güvenlik duvarı** dikey penceresi açılır ve sizi gerçekleştirebileceğiniz **VM Yapılandırması** sağlamak ve adımlarını **WAF bilgi**. Seçin **VM Yapılandırması**.
7. Merhaba, **VM Yapılandırması** dikey penceresinde gerekli toospin çalıştıran hello sanal makineyi hello WAF bilgileri girin.
   ![VM yapılandırması][4]
8. Toohello iade **yeni Web uygulaması güvenlik duvarı** dikey penceresinde ve select **WAF bilgi**. Merhaba, **WAF bilgi** dikey penceresinde hello WAF kendisini yapılandırın. 7. adım, hangi hello WAF çalıştırır ve 8. adım sağlar tooprovision hello WAF kendisini tooconfigure hello sanal makine sağlar.

## <a name="finalize-application-protection"></a>Uygulama korumayı Sonlandır
1. Toohello iade **önerileri** dikey. Adlı hello WAF oluşturduktan sonra yeni bir giriş oluşturulan **uygulama korumayı Sonlandır**. Bu giriş, Merhaba uygulaması koruyabilmeniz için gerçekten hello WAF hello Azure sanal ağ içinde yukarı bağlantı kabloları toocomplete hello işlemi gereksinim bilmenizi sağlar.

   ![Uygulama korumayı Sonlandır][5]

2. Seçin **uygulama korumayı Sonlandır**. Yeni bir dikey pencere açılır. Yönlendirdi trafiği toohave gerektiren bir web uygulaması olduğunu görebilirsiniz.
3. Merhaba web uygulaması seçin. Merhaba web uygulaması güvenlik duvarı Kurulumu Tamamlanıyor için adımları sağlayan bir dikey pencere açılır. Merhaba adımları tamamlayın ve ardından **trafiği kısıtlamak**. Güvenlik Merkezi, ardından sizin için kablolama yukarı hello.

   ![Trafiği kısıtlama][6]

> [!NOTE]
> Bu uygulamalar tooyour varolan WAF dağıtımlar ekleyerek, birden çok web uygulamasına Güvenlik Merkezi'nde koruyabilirsiniz.
>
>

Bu WAF Hello günlüklerinden artık tam olarak tümleşiktir. Güvenlik Merkezi otomatik olarak toplamak ve böylece bu önemli güvenlik uyarıları tooyou yüzey hello günlüklerini analiz başlatabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "Ekleme bir web uygulaması." gösterdi. bir web uygulaması güvenlik duvarı yapılandırma hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Bir Web uygulaması Güvenlik Duvarı (WAF) için uygulama hizmeti ortamını yapılandırma](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
