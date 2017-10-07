---
title: "Güvenlik Merkezi ile günlük tümleştirme aaaAzure | Microsoft Docs"
description: "Nasıl tooget Azure Güvenlik Merkezi ile günlük tümleştirme çalışma uyarıları öğrenin"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Nasıl tooget Azure günlük tümleştirme, Güvenlik Merkezi uyarıları
Bu makalede hello adımları gerekli tooenable hello Azure günlük tümleştirme hizmeti toopull Azure Güvenlik Merkezi tarafından üretilen güvenlik uyarısı bilgileri sağlar. Merhaba hello adımları tamamladınız gerekir [başlama](security-azure-log-integration-get-started.md) bu makalede hello adımları gerçekleştirmeden önce makalesi.

## <a name="detailed-steps"></a>Ayrıntılı adımlar
Merhaba aşağıdaki adımları oluşturacak hello gerekli Azure Active Directory hizmet asıl ve ata hello hizmet ilkesi Okuma izinleri toohello abonelik:
1. Merhaba komut istemi açın ve çok gidin**c:\Program Files\Microsoft Azure günlük tümleştirme**
2. Merhaba komutunu çalıştırın``azlog createazureid``

    Bu komut için Azure oturum açma bilgilerinizi ister. Merhaba komutu ardından oluşturur bir [Azure Active Directory hizmet asıl](../active-directory/develop/active-directory-application-objects.md) hello konak Azure AD Kiracılarıyla hangi hello kullanıcı olarak oturum açmış olan bir yönetici, bir ortak yönetici veya bir sahip Azure abonelikleri hello. Kullanıcı oturum hello yalnızca Konuk kullanıcı hello Azure AD Kiracı olarak ise hello komut başarısız olur. Kimlik doğrulama tooAzure Azure Active Directory (AD ile) yapılır. Azlog tümleştirmesi için bir hizmet sorumlusu oluşturma hello Azure aboneliklerinden erişim tooread verilir Azure AD kimlik oluşturur.

2. Sonraki 2. adımda oluşturduğunuz hello abonelik toohello hizmet sorumlusu okuyucu erişim atayan bir komut çalışır. Bir Subscriptionıd belirtmezseniz, hello komutu tooassign hello hizmet asıl okuyucu rolü tooall abonelikleri toowhich herhangi erişimi deneyecek. </br></br>
``azlog authorize <SubscriptionID>`` </br> Örneğin </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Merhaba çalıştırırsanız uyarıları görebilirsiniz hemen hello createazureid komutundan sonra komut yetkilendirin. Hello Azure AD hesabı oluşturulduğunda ve hello hesabı kullanılabilir olduğunda arasındaki bazı gecikme süresi yok. Beklerseniz hello createazureid komutu toorun hello çalıştırdıktan sonra 60 saniye komutu yetkilendirmek sonra bu uyarılar görülmemelidir.

4. Denetim günlüğü JSON dosyalarını hello klasörleri tooconfirm aşağıdaki hello vardır denetleyin:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Güvenlik Merkezi uyarılarını bunları mevcut klasörleri tooconfirm aşağıdaki hello denetleyin:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Merhaba yükleme ve yapılandırma sırasında herhangi bir sorunla çalıştırırsanız, lütfen açık bir [destek isteği](/azure-supportability/how-to-create-azure-support-request.md)seçin **günlük tümleştirme** destek isteyen hello hizmet olarak.

## <a name="next-steps"></a>Sonraki adımlar
Azure günlük tümleştirme hakkında daha fazla toolearn belgeleri aşağıdaki hello bakın:

* [Microsoft Azure günlük tümleştirme Azure günlükleri için](https://www.microsoft.com/download/details.aspx?id=53324) – merkezi ayrıntılı bilgi için sistem gereksinimleri, yükleyip yönergeler Azure günlük tümleştirme.
* [Giriş tooAzure günlük tümleştirme](security-azure-log-integration-overview.md) – bu belgeyi tooAzure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı tanıtır.
* [Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – bu blog gönderisine nasıl tooconfigure Azure oturum tümleştirme toowork Splunk, HP ArcSight ve IBM QRadar ile iş ortağı çözümlerini gösterir.
* [Azure günlük sık sorulan sorular (SSS) tümleştirme](security-azure-log-integration-faq.md) -bu SSS Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.
* [Güvenlik Merkezi tümleştirme uyarıları Azure ile tümleştirme oturum](../security-center/security-center-integrating-alerts-with-log-integration.md) – bu belgeyi nasıl toosync Güvenlik Merkezi, sanal makine güvenlik olayları, günlük analizi ile Azure tanılama ve Azure denetim günlükleri tarafından toplanan birlikte uyarıları gösterir veya SIEM çözümü.
* [Azure tanılama ve Azure denetim günlükleri için yeni özellikler](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – bu blog gönderisine tooAzure denetim günlüklerini tanıtır ve yardımcı diğer özellikleri Azure kaynaklarınızı hello işlemlerini alın.
