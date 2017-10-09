---
title: "Azure ile aaaIntegrating Azure Güvenlik Merkezi uyarılarını oturum tümleştirme | Microsoft Docs"
description: "Bu makalede Azure günlük tümleşme Güvenlik Merkezi uyarılarını tümleştirme ile çalışmaya başlamanıza yardımcı olur."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Azure Güvenlik Merkezi uyarılarını Azure günlük tümleştirme ile tümleştirme
Birçok güvenlik işlemleri ve olay yanıtı takımlar başlangıç noktası önceliklendirmek ve güvenlik uyarıları İnceleme için hello olarak bir güvenlik bilgileri ve Olay yönetimi (SIEM) çözümünü kullanır. Azure günlük Tümleştirmesi ile Azure Güvenlik Merkezi uyarılarını SIEM çözümünüzle birlikte tümleştirebilirsiniz.

Azure günlük tümleştirme şu anda HP ArcSight, Splunk ve IBM QRadar destekler.

## <a name="what-logs-can-i-integrate"></a>Hangi günlükleri ı tümleştirebilir miyim?
Azure her hizmet için ayrıntılı günlük kaydını üretir. Bu günlükler olarak kategorilere ayrılır:

* **Denetim/Yönetim günlüklerini** Azure Kaynak Yöneticisi oluşturma, güncelleştirme ve silme işlemleri hello görünürlük sağlar. Bu denetim düzlemi olayları hello Azure etkinlik günlükleri çıkmış
* **Veri düzlemi günlüklerini** bir Azure kaynağı kullanırken başlatılan hello olayları görünürlük sağlar. Güvenlik olay bilgilerini hello Olay Görüntüleyicisi'nin güvenlik kanaldan alabileceğiniz hello Windows olay günlüğü örneğidir. (Bir sanal makine veya bir Azure hizmeti tarafından oluşturulan) veri düzlemi olaylar tarafından Azure tanılama günlükleri çıkmış.

Azure günlük tümleştirme şu anda hello tümleştirilmesi destekler:

* Azure VM günlükleri
* Azure denetim günlükleri
* Azure Güvenlik Merkezi uyarıları

## <a name="install-azure-log-integration"></a>Azure günlük tümleştirme yükleyin
Karşıdan [Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324).

Hello Azure günlük tümleştirme hizmeti yüklü olduğu hello makineden telemetri verileri toplar.  Toplanan telemetri verileri şöyledir:

* Azure günlük tümleştirme yürütülmesi sırasında oluşan özel durumlar
* Ölçümleri hello sayısı sorgular ve işlenen olayların hakkında
* Komut satırı seçenekleri hakkında hangi Azlog.exe kullanılan istatistikleri

> [!NOTE]
> Bu seçenek kaldırarak telemetri veri koleksiyonunu devre dışı bırakabilirsiniz.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Azure denetim günlükleri ve Güvenlik Merkezi uyarıları tümleştirme
1. Açık hello komut istemi ve **cd** içine **c:\Program Files\Microsoft Azure günlük tümleştirme**.
2. Merhaba çalıştırmak **azlog createazureid** komutu toocreate bir [Azure Active Directory hizmet asıl](../active-directory/active-directory-application-objects.md) hello Azure Active Directory (AD), Azure abonelikleri konak kiracılar hello.

    Azure oturum açma için istenir.

   > [!NOTE]
   > Merhaba abonelik sahibi veya hello aboneliğin ortak yöneticisi olmanız gerekir.
   >
   >

    Kimlik doğrulama tooAzure Azure AD üzerinden yapılır.  Azure günlük tümleştirmesi için bir hizmet sorumlusu oluşturma, erişim tooread Azure aboneliklerinden verilen hello Azure AD kimlik oluşturur.
3. Merhaba çalıştırmak **azlog yetkilendirmek <SubscriptionID>**  tooassign okuyucu erişimi hello abonelik toohello hizmet sorumlusu 2. adımda oluşturduğunuz komutu. Belirtmediyseniz bir **Subscriptionıd**, hello hizmet sorumlusu atanan hello okuyucu rolü tooall abonelikleri toowhich erişiminiz olur.

   > [!NOTE]
   > Merhaba çalıştırırsanız uyarıları görebilirsiniz **yetkilendirmek** hello hemen sonra komut **createazureid** komutu. Hello Azure AD hesabı oluşturulduğunda ve hello hesabı kullanılabilir olduğunda arasındaki bazı gecikme süresi yok. Merhaba çalıştırdıktan sonra yaklaşık 10 saniye bekleyin, **createazureid** komutu toorun hello **yetkilendirmek** Bu uyarılar görülmemelidir sonra komutu.
   >
   >
4. Denetim günlüğü JSON dosyalarını hello klasörleri tooconfirm aşağıdaki hello vardır denetleyin:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Güvenlik Merkezi uyarılarını bunları mevcut klasörleri tooconfirm aşağıdaki hello denetleyin:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Merhaba SIEM dosya iletici bağlayıcı toohello uygun klasör yapılandırın. Merhaba yordamı hello kullanmakta olduğunuz SIEM göre değişir.

## <a name="next-steps"></a>Sonraki adımlar
Azure etkinlik günlükleri ve özellik tanımları hakkında daha fazla toolearn bakın:

* [Resource Manager ile işlemleri denetleme](../azure-resource-manager/resource-group-audit.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — hello en son Azure güvenlik haberlerini ve bilgilerini alın.
