---
title: Azure automation'da aaaIntro tooauthentication | Microsoft Docs
description: "Bu makalede Azure automation'da Automation hesapları Automation güvenliği ve hello farklı kimlik doğrulama yöntemleri kullanılabilir genel bakış sağlar."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "otomasyon güvenliği, güvenli otomasyon; otomasyon kimlik doğrulaması"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Azure Automation giriş tooauthentication  
Azure Otomasyonu, Azure, şirket içi ve diğer bulut sağlayıcılarıyla Amazon Web Hizmetleri (AWS) gibi kaynaklara karşı tooautomate görevleri sağlar.  Bir runbook tooperform için gerekli işlemleri, onu hello kaynaklarına erişim izinleri toosecurely hello abonelikte gereken hello en düşük haklara sahip olması gerekir.

Bu makalede Azure Automation tarafından desteklenen çeşitli kimlik doğrulama senaryoları hello kapsar ve tooget nasıl başlamanıza hello ortam veya ortamlar, göre Göster toomanage gerekir.  

## <a name="automation-account-overview"></a>Otomasyon Hesabına genel bakış
Azure Otomasyonu hello için ilk kez başlattığınızda, en az bir Automation hesabı oluşturmanız gerekir. Automation hesapları Automation kaynaklarınızı (runbook'lar, varlıklar, yapılandırmalar) gelen diğer Automation hesaplarında yer alan kaynakları hello tooisolate izin verin. Automation hesapları tooseparate kaynaklarını ayrı mantıksal ortamlara kullanabilirsiniz. Örneğin, geliştirme için bir hesap, üretim için başka bir hesap ve şirket içi ortamınız için de başka bir hesap kullanabilirsiniz.  Azure Automation hesabı, Azure aboneliğinizde oluşturduğunuz Microsoft hesabı veya hesaplarından farklıdır.

Merhaba her Automation hesabı için Automation kaynakları tek bir Azure bölgesiyle ilişkilendirilir, ancak Automation hesapları tüm hello kaynakları yönetebilir. Merhaba ana nedeni toocreate Automation hesapları farklı bölgelerdeki verilerine ve kaynaklarına toobe yalıtılmış tooa belirli bölge gerektiren ilkelere sahip olmanız olabilir.

> [!NOTE]
> Automation hesapları ve içerdikleri hello kaynakları hello Azure portalında oluşturulur, hello Klasik Azure portalında erişilemez. Bu hesapları veya kaynaklarını Windows PowerShell ile toomanage istiyorsanız hello Azure Resource Manager modüllerini kullanmanız gerekir.
>

Tüm Azure Otomasyonu'nda Azure Resource Manager ve hello Azure cmdlet'lerini kullanan kaynaklara karşı gerçekleştirdiğiniz hello görevleri tooAzure kullanarak Azure Active Directory kuruluş kimlik bilgileri tabanlı kimlik doğrulaması gerekir.  Sertifika tabanlı kimlik doğrulaması için Azure hizmet yönetimi modu hello özgün kimlik doğrulama yöntemi olsa da, karmaşık toosetup oluştu.  TooAzure ile Azure AD kullanıcısının kimlik doğrulaması oluştu 2014 toonot sunulan arkada yalnızca basitleştirmek hello işlem tooconfigure toonon etkileşimli bir kimlik doğrulama hesabı, aynı zamanda destek hello özelliği tooAzure çalışan tek bir kullanıcı hesabı ile kimlik doğrulaması hem Azure Resource Manager hem de klasik kaynakları ile.   

Şu anda hello Azure portalında yeni bir Otomasyon hesabı oluşturduğunuzda, otomatik olarak oluşturur:

* Yeni bir hizmet sorumlusu Azure Active Directory'de, bir sertifika oluşturur ve olacağı hello katkıda bulunan rolü tabanlı erişim denetimi (RBAC) atayan farklı çalıştır hesabı runbook'ları kullanarak toomanage Resource Manager kaynakları kullanılır.
* Tarafından kullanılan toomanage Azure Hizmet Yönetimi olması ya da runbook kullanan Klasik kaynakları görüntüler yönetim sertifikasını karşıya yükleyen Klasik farklı çalıştır hesabı.  

Rol tabanlı erişim denetimi ile Azure Resource Manager toogrant Eylemler tooan Azure AD kullanıcı hesabı ve farklı çalıştır hesabı izin kullanılabilir ve bu hizmet sorumlusunun kimliğini.  Lütfen okuyun [Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md) daha fazla bilgi için toohelp Automation izinlerinin yönetilmesi için modelinizin geliştirin.  

Bir karma Runbook çalışanı, veri merkezinizdeki veya AWS'deki bilgi işlem hizmetlerine karşı çalışan runbook'ları kullanmak aynı hello olamaz genelde tooAzure kaynakları kimlik doğrulayan runbook'lar için kullanılan yöntem.  Bu kaynakların Azure dışında çalışmasıdır ve bu nedenle, yerel olarak erişecekleri Otomasyon tooauthenticate tooresources içinde tanımlanan kendi güvenlik kimlik bilgileri gerektirecektir olmasıdır.  

## <a name="authentication-methods"></a>Kimlik doğrulama yöntemleri
Merhaba aşağıdaki tabloda özetlenmiştir hello farklı kimlik doğrulama yöntemleri Azure Automation ve makale hello açıklayan tarafından desteklenen her ortam için nasıl toosetup kimlik doğrulaması runbook'larınızın.

| Yöntem | Ortam | Makale |
| --- | --- | --- |
| Azure AD Kullanıcı Hesabı |Azure Resource Manager ve Azure Hizmet Yönetimi |[Azure AD Kullanıcı hesabıyla Runbook Kimlik Doğrulaması](automation-create-aduser-account.md) |
| Azure Farklı Çalıştır Hesabı |Azure Resource Manager |[Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması](automation-sec-configure-azure-runas-account.md) |
| Azure Klasik Farklı Çalıştır Hesabı |Azure Service Management |[Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması](automation-sec-configure-azure-runas-account.md) |
| Windows Kimlik Doğrulaması |Şirket İçi Veri Merkezi |[Karma Runbook Çalışanları için Runbook Kimlik Doğrulaması](automation-hybrid-runbook-worker.md) |
| AWS Kimlik Bilgileri |Amazon Web Hizmetleri |[Amazon Web Hizmetleri (AWS) ile Runbook Kimlik Doğrulaması](automation-config-aws-account.md) |
