---
title: Active Directory PoC Playbook malzemeleri aaaAzure | Microsoft Docs
description: "Keşfetmek ve hızlı bir şekilde kimlik ve erişim yönetimi senaryoları uygulayan"
services: active-directory
keywords: "Azure active directory, playbook, kavram kanıtı, PT"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Azure Active Directory Playbook malzemeleri kavram kanıtı 

## <a name="theme"></a>Tema
Azure AD kimlik ve erişim çözümleri birden fazla alanda hello kuruluş genelinde sağlar. Biz hello hello alanları aşağıdaki senaryolarda sınıflandırmak: 

* [Birçok uygulama, bir kimlik](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [Güvenlik Artırma](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Self Servis ölçekli](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Bu iş hedeflerini ile denenmemesi PT toofocus hello çabalarına yardımcı olan bir tema tooframe hello tanımlama, görmemeleri kavram kanıtı hello ilgi hello ilk yerinde hello tetikleyici olduğu. 

## <a name="environment"></a>Ortam

Bu önemli toodetermine hello burada hello PoC teslim eder hello ortamı ayrıntılarını gösterir. İdeal olarak üzerine hello PoC tamamlandıktan sonra oluşturabilirsiniz. Merhaba hedef ortam çok önemlidir ve olabildiğince gerçek ve sınırlamalar veya ek konular hello yükünü yapmadan arasında doğru dengeyi hello bulmanız gerekir. Merhaba tipik ortamları kanıtları için şunlardır:
* **Üretim:** hello senaryoları Canlı ortamınızda uygulanan ve Microsoft Cloud services (üretim AD, Office 365, Azure AD Kiracı/SSO çözüm) zaten dağıtılmış. 
* **Kullanıcı kabul testi (UAT) / geliştirme ortamında:** test altyapısına sahip (AD ve potansiyel olarak Azure AD paralel Kiracı/SSO çözüm) test verilerle üretim benzer. Genellikle, hello test ortamı hello kuruluştaki birden çok projeler arasında paylaşılır.

Bu kılavuzdaki çoğu senaryolar yapısı eklenebilir. Sonuç olarak, bunlar hello üretim kiracısında hello PoC dışındaki kullanıcılar etkilemeden dağıtılabilir. Bu belge boyunca biz Kiracı genelinde etkisi hangi senaryolar yoktur çağırma. Bu durumda, bir üretim ortamı dışındaki tooconsider isteyebilirsiniz. 


## <a name="target-users"></a>Hedef Kullanıcılar

Bu önemli toodetermine hello hedef özellikle hello ortam üretim ya da test olduğunda hello senaryoları çalışma kullanıcıları kümesidir. PoC için hedef kullanıcı Hello kategorileri şunlardır:
* **Pilot kullanıcıları:** hello çözümü kendi gün tooday için kullandıkları hello hesabıyla kullanarak hello ortamında gerçek kullanıcıların iş işlevleri
* **Test kullanıcılarını:** Test hello ortamında oluşturulan hesaplar 

Bu kılavuz Çoğu senaryoda, pilot kullanıcılar tarafından kullandı. Bu belge boyunca biz hedef kullanıcı konuları gerekirse sizi arayacaktır.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]