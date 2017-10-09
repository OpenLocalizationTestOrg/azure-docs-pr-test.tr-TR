---
title: "bir expressroute bağlantı hattı yapılandırma aaaWorkflows | Microsoft Docs"
description: "Bu sayfada, expressroute bağlantı hattı ve eşlemeleri yapılandırma hello iş akışları açıklanmaktadır"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Devre sağlama ve devre durumları için ExpressRoute iş akışları
Bu sayfayı hello hizmet sağlama ve yüksek düzeyde yönlendirme yapılandırması iş akışları size yol göstermektedir.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Merhaba aşağıdaki şekilde ve ilgili adımlarda hello görevleri bir ExpressRoute bağlantı hattı sağlanan uçtan uca sipariş toohave izlemelisiniz gösterin. 

1. PowerShell tooconfigure bir expressroute bağlantı hattı kullanın. Merhaba Hello yönergeleri izleyin [oluşturma ExpressRoute bağlantı hatları](expressroute-howto-circuit-classic.md) daha fazla ayrıntı için makale.
2. Bağlantı hello hizmet sağlayıcısı'ndan sipariş. Bu işlem değişir. Nasıl hakkında daha fazla ayrıntı için bağlantı sağlayıcınıza başvurun tooorder bağlantısı.
3. Merhaba hattı başarıyla hello expressroute bağlantı hattı sağlama durumu PowerShell aracılığıyla doğrulayarak sağlandığından emin olun. 
4. Yönlendirme etki alanlarını yapılandırın. Bağlantı sağlayıcınızdan sizin için Katman 3 yönetiyorsa hattı için yönlendirmeyi yapılandırır. Bağlantı sağlayıcınız yalnızca Katman 2 Hizmetleri sunuyorsa, hello açıklanan yönergeleri başına yönlendirme yapılandırmalısınız [yönlendirme gereksinimleri](expressroute-routing.md) ve [yönlendirme yapılandırması](expressroute-howto-routing-classic.md) sayfaları.
   
   * Azure özel eşlemeyi etkinleştirmesini - Bu eşleme tooconnect tooVMs etkinleştir / bulut Hizmetleri sanal ağlar içinde dağıtılır.
   * Azure ortak eşleme enable - genel IP adresleri üzerinde barındırılan tooconnect tooAzure Hizmetleri isterseniz, Azure ortak eşleme etkinleştirmeniz gerekir. Azure özel eşleme için varsayılan tooenable yönlendirme seçtiyseniz gereksinim tooaccess Azure kaynaklarını budur.
   * Microsoft eşlemesi - etkinleştirmek bu tooaccess Office 365 ve Dynamics 365 etkinleştirmeniz gerekir. 
     
     > [!IMPORTANT]
     > Ayrı bir proxy sunucu kullan / kenar tooconnect tooMicrosoft için kullandığınız hello daha Internet hello sağlanmalıdır. Hem ExpressRoute hem de hello Internet için aynı sınır asimetrik yönlendirme neden ve ağ bağlantı kesintileri neden hello kullanma.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Sanal bağlama tooExpressRoute devreler ağları - sanal ağlar tooyour expressroute bağlantı hattı bağlayabilirsiniz. Yönergeleri izleyerek [toolink Vnet'ler](expressroute-howto-linkvnet-arm.md) tooyour hattı. Bu sanal ağlar ya da olabilir hello hello expressroute bağlantı hattı olarak aynı Azure aboneliğinden veya farklı bir abonelikte olabilir.

## <a name="expressroute-circuit-provisioning-states"></a>Expressroute bağlantı hattı durumları sağlama
Her expressroute bağlantı hattı iki durum vardır:

* Hizmet Sağlayıcısı sağlama durumu
* Durum

Durum Microsoft'un sağlama durumunu temsil eder. Bir expressroute bağlantı hattı oluşturduğunuzda, bu özellik tooEnabled ayarlanır

Merhaba bağlantı Sağlayıcısı sağlama durumu hello bağlantı sağlayıcısı tarafında hello durumunu temsil eder. Ya da olabilir *NotProvisioned*, *sağlama*, veya *hazırlandı*. Merhaba expressroute bağlantı hattı, toobe mümkün toouse için hazırlandı durumunda bu olmalıdır.

### <a name="possible-states-of-an-expressroute-circuit"></a>Olası bir expressroute bağlantı hattı durumları
Bu bölümde bir expressroute bağlantı hattı için olası durumlar hello çıkışı listelenir.

**Oluşturma sırasında**

Merhaba expressroute bağlantı hattı durumu kısa sürede, aşağıdaki hello hello PowerShell cmdlet toocreate hello expressroute bağlantı hattı çalıştırmak görürsünüz.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Bağlantı sağlayıcı hello devre sağlama hello işleminde olduğunda**

Merhaba expressroute bağlantı hattı durumu kısa sürede, aşağıdaki hello hello hizmet anahtar toohello bağlantı sağlayıcı geçirmek görür ve sağlama işlemi hello başlamış olması.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Bağlantı sağlayıcı sağlama işlemi hello zaman tamamlandı**

Göreceğiniz hello durumu hello bağlantı sağlayıcı hello sağlama işlemi tamamlandıktan hemen sonra aşağıdaki hello'daki expressroute bağlantı hattına.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Durumu hello hattı içinde toobe mümkün toouse için yalnızca hello sağlanmış ve etkin olduğundan. Bir katman 2 sağlayıcısı kullanıyorsanız, yalnızca bu durumda olduğunda, hattı için yönlendirmeyi yapılandırabilirsiniz.

**Bağlantı sağlayıcı hello hattı zaman sağlamayı kaldırma**

Merhaba hizmet sağlayıcısı toodeprovision hello expressroute bağlantı hattı istediyseniz hello hattı hello hizmet sağlayıcısı hello sağlamayı kaldırma işlemi tamamlandıktan sonra durumu aşağıdaki toohello ayarlamak görürsünüz.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Toore etkinleştir seçebilirsiniz, gerekli ya da toodelete hello hattı PowerShell cmdlet'lerini çalıştırın.  

> [!IMPORTANT]
> Çalıştırırsanız hello hello ServiceProviderProvisioningState sağlama veya hazırlandı hello işlemi olduğunda PowerShell cmdlet toodelete hello hattı başarısız olur. Lütfen, bağlantı sağlayıcısı toodeprovision hello expressroute bağlantı hattı ile ilk iş ve hello hattı silin. Merhaba PowerShell cmdlet toodelete hello hattı çalıştırana kadar Microsoft toobill hello hattı devam edecektir.
> 
> 

## <a name="routing-session-configuration-state"></a>Yönlendirme oturum yapılandırma durumu
Merhaba BGP sağlama durumu, hello BGP oturumu Microsoft edge hello üzerinde etkinleştirilirse bilmenizi sağlar. Merhaba durumu sizin için etkinleştirilmelidir toobe mümkün toouse hello eşleme.

Microsoft eşlemesi için özellikle önemli toocheck hello BGP oturumu durumu değil. Toplama toohello BGP sağlama durumunda, yok adlı başka bir duruma *tanıtılan genel ön ekten durumu*. Merhaba tanıtılan genel ön ekten durumu olmalıdır *yapılandırılmış* durum hem, yönlendirme toowork uçtan uca ve hello BGP oturumu toobe için. 

Ortak önek durumu tooa ayarlanmış Hello tanıtılan varsa *gerekli doğrulama* durumunda, hello BGP oturumu etkin değil, hello öneklerini hello eşleşmedi bildirilen herhangi bir kayıt defterlerini yönlendirme hello sayı olarak. 

> [!IMPORTANT]
> Merhaba tanıtılan genel ön ek durum ise, *el ile doğrulama* durum ile bir destek bileti açmanız [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ve hello IP adreslerini tanıtılan boyunca kendi kanıt Otonom sistem numarası Hello ile ilişkilendirilmiş.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* ExpressRoute bağlantınızı yapılandırın.
  
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md)
  * [Yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md)
  * [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md)

