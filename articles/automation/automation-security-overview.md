---
title: "Azure Otomasyonu’nda kimlik doğrulamasına giriş | Microsoft Docs"
description: "Bu makalede, Azure Otomasyonu’nda Otomasyon Hesapları için uygun Otomasyon güvenliği ve farklı kumluk doğrulasa yöntemlerine genel bakış verilmektedir."
services: automation
documentationcenter: 
author: georgewallace
manager: jwhit
editor: tysonn
keywords: "otomasyon güvenliği, güvenli otomasyon; otomasyon kimlik doğrulaması"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 99882c1ff7517beec2ca827c63620f773d7d07c3
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="introduction-to-authentication-in-azure-automation"></a>Azure Otomasyonu’nda kimlik doğrulamaya giriş  
Azure Automation, Azure’deki, şirket içindeki kaynaklara karşı ve Amazon Web Hizmetleri (AWS) gibi diğer bulut sağlayıcılarıyla görevleri otomatikleştirmenizi sağlar.  Runbook'un gerekli işlemlerini gerçekleştirebilmesi için, abonelikte gereken en düşük haklara sahip kaynaklara güvenli erişim izinlerinin olması gerekir.

Bu makale, Azure Automation’ın desteklediği çeşitli kimlik doğrulaması senaryolarını kapsamakta ve yönetmeniz gereken ortam veya ortamlar temelinde nasıl başlayacağınızı göstermektedir.  

## <a name="automation-account-overview"></a>Otomasyon Hesabına genel bakış
Azure Automation’ı ilk kez başlattığınızda, en az bir Automation hesabı oluşturmanız gerekir. Automation hesapları Automation kaynaklarınızı (runbook'lar, varlıklar, yapılandırmalar) diğer Automation hesaplarında yer alan kaynaklarından yalıtmanızı sağlar. Kaynaklarını ayrı mantıksal ortamlara ayırmak için Automation hesaplarını kullanabilirsiniz. Örneğin, geliştirme için bir hesap, üretim için başka bir hesap ve şirket içi ortamınız için de başka bir hesap kullanabilirsiniz.  Azure Automation hesabı, Azure aboneliğinizde oluşturduğunuz Microsoft hesabı veya hesaplarından farklıdır.

Her Otomasyon hesabı için Otomasyon kaynakları tek bir Azure bölgesiyle ilişkilendirilir, ancak Otomasyon hesapları aboneliğinizdeki tüm kaynakları yönetebilir. Farklı bölgelerde Automation hesapları oluşturmanın temel nedeni, veri ve kaynakların belirli bir bölgede yalıtılmasını gerektiren ilkelere sahip olmanız olabilir.

Azure Resource Manager ve Azure Otomasyonu’ndaki Azure cmdlet'lerini kullanan kaynaklara karşı gerçekleştirdiğiniz görevlerin tümü, Azure Active Directory kuruluş kimliğini kullanarak Azure’de kimlik bilgileri tabanlı kimlik doğrulamasını doğrulamalıdır.  Sertifika tabanlı kimlik doğrulaması Azure klasik ile asıl kimlik doğrulaması yöntemi olsa da, bunun kurulması karmaşıktır.  Azure AD kullanıcısının bulunduğu Azure’de kimlik doğrulaması, 2014’te yalnızca Kimlik Doğrulaması hesabını sadeleştirmek amacıyla değil, hem Azure Resource Manager hem de klasik kaynaklarla çalışan tek kullanıcı hesabıyla Azure’de etkileşimsiz kimlik doğrulamasını becerisini de destekler.   

Şu anda Azure portalında yeni bir Otomasyon hesabı oluşturduğunuzda otomatik olarak şunlar oluşturulur:

* Azure Active Directory'de yeni bir hizmet sorumlusu ve bir sertifika oluşturan ve Katkı Yapana runbook'lar kullanılarak Resource Manager kaynaklarını yönetmek için kullanılan rol tabanlı erişim denetimi (RBAC) atayan Farklı Çalıştır hesabı.
* Runbook kullanan Azure klasik kaynaklarını yönetmek için kullanılan bir yönetim sertifikasını karşıya yükleyen Klasik Farklı Çalıştır hesabı.  

Rol tabanlı erişim denetimi, Azure AD kullanıcı hesabı ve Farklı Çalıştır hesabına izin verilen eylemleri vermek, ve bu hizmet sorumlusunun kimliğini doğrulamak için Azure Resource Manager ile kullanılabilir.  Automation izinlerinin yönetilmesi için modelinizin geliştirilmesine yardımcı olma hakkında daha fazla bilgi için lütfen [Azure Automation’da rol tabanlı erişim denetimi](automation-role-based-access-control.md) makalesini okuyun.  

Veri merkezindeki Karma Runbook Çalışanı’nda veya AWS’deki bilgi işlem hizmetlerine karşı çalışan runbook'lar, genel olarak Azure kaynaklarında kimlik doğrulayan runbook’lar için kullanılan yöntemin aynısını kullanamaz.  Bunun nedeni, bu kaynakların Azure dışında çalışmasıdır; sonuç olarak da, yerel olarak erişecekleri kaynakların kimliğini doğrulamak için Otomasyon'da tanımlanan kendi güvenlik kimlik bilgileri gerekecektir.  

## <a name="authentication-methods"></a>Kimlik doğrulama yöntemleri
Aşağıdaki tabloda, Azure Automation tarafından desteklenen her ortamla ilgili farklı kimlik doğrulaması yöntemleri ve runbook’larınızın nasıl ayarlanacağını anlatan makaledeki bilgiler özetlenmiştir.

| Yöntem | Ortam | Makale |
| --- | --- | --- |
| Azure AD Kullanıcı Hesabı |Azure Resource Manager ve Azure klasik |[Azure AD Kullanıcı hesabıyla Runbook Kimlik Doğrulaması](automation-create-aduser-account.md) |
| Azure Farklı Çalıştır Hesabı |Azure Resource Manager |[Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması](automation-sec-configure-azure-runas-account.md) |
| Azure Klasik Farklı Çalıştır Hesabı |Azure klasik |[Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması](automation-sec-configure-azure-runas-account.md) |
| Windows Kimlik Doğrulaması |Şirket İçi Veri Merkezi |[Karma Runbook Çalışanları için Runbook Kimlik Doğrulaması](automation-hybrid-runbook-worker.md) |
| AWS Kimlik Bilgileri |Amazon Web Hizmetleri |[Amazon Web Hizmetleri (AWS) ile Runbook Kimlik Doğrulaması](automation-config-aws-account.md) |
