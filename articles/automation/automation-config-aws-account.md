---
title: "Amazon Web Hizmetleri ile kimlik doğrulaması aaaConfigure | Microsoft Docs"
description: "Bu makalede nasıl toocreate ve AWS kaynaklarını yöneten Azure automation'daki runbook'lar için bir AWS kimlik bilgisi doğrulayın."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "aws kimlik doğrulaması, aws yapılandırma"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1e312df2422d9da3cd3331fe01aeaa3a43c8b9d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Amazon Web Hizmetleri ile Kimlik Doğrulaması Runbook'ları
Amazon Web Hizmetleri’ndeki (AWS) kaynaklarla ortak görevlerin otomatikleştirilmesi Azure’ün Automation runbook'ları ile sonuçlandırılabilir.  Tıpkı Azure’deki kaynaklarla yapabildiğiniz gibi Automation runbook'ları kullanarak AWS’deki birçok görevi otomatik hale getirebilirsiniz.  Gerekenlerin tümü şu iki şeydir:

* Bir AWS aboneliği ve bir dizi kimlik bilgisi.  Özellikle AWS Erişim Anahtarınız ve Gizli Anahtarınız.  Daha fazla bilgi için lütfen hello makalesini inceleyin [AWS kimlik bilgilerini kullanma](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Bir Azure aboneliği ve Automation hesabı.  Bir Azure Otomasyonu hesabını ayarlama hakkında daha fazla bilgi için lütfen hello makalesini inceleyin [yapılandırma Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md).  

tooauthenticate AWS ile Azure Automation'dan çalışan runbook'larınızın bir dizi AWS kimlik bilgileri tooauthenticate belirtmeniz gerekir. Oluşturulan bir Otomasyon hesabınız zaten var ve bu tooauthenticate AWS ile toouse istiyorsanız bölümden hello hello adımları izleyebilirsiniz.  Toodedicated bir hesap için runbook'ları atamak AWS kaynaklarını istiyorsanız, önce yeni bir oluşturmalısınız [Otomasyon hesabı](automation-offering-get-started.md) (Merhaba seçeneği toocreate bir hizmet sorumlusu atlayın) ve hello adımları izleyin.

## <a name="configure-automation-account"></a>Automation hesabı yapılandırma
Azure Otomasyonu toocommunicate AWS ile için önce AWS kimlik bilgilerinizi tooretrieve gerekir ve bunları Azure automation'da varlıklar olarak saklar.  Merhaba AWS belgesinde belgelenen adımları izleyerek hello gerçekleştirmek [AWS hesabınız için erişim anahtarlarını yönetme](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate bir erişim anahtarı ve kopyalama hello **erişim anahtarı kimliği** ve **gizli erişim anahtar** (isteğe bağlı olarak, anahtar dosyası toostore karşıdan güvenli bir yerde).

Oluşturduğunuz ve AWS güvenlik anahtarlarınızı kopyaladığınız sonra toocreate bir kimlik bilgisi varlığı ile bir Azure Otomasyonu hesabı toosecurely gerekir depolamak ve runbook'larınızla başvuru.  Merhaba hello bölümdeki adımları **toocreate yeni bir kimlik bilgisi** hello içinde [kimlik bilgisi varlıkları Azure Automation](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) makalesi ve aşağıdaki bilgilerle hello girin:

1. Merhaba, **adı** kutusuna **AWScred** veya adlandırma standartlarınıza uygun bir değer.  
2. Merhaba, **kullanıcı adı** kutusuna yazın, **erişim kimliği** ve **gizli erişim anahtar** hello içinde **parola** ve **Onayla Parola** kutusu.   

## <a name="next-steps"></a>Sonraki adımlar
* Aws'de hello çözüm makalesini [Amazon Web Hizmetleri'nde VM'nin dağıtımını otomatik hale getirme](automation-scenario-aws-deployment.md) nasıl toocreate runbook'lar tooautomate görevler AWS toolearn.

