---
title: Azure Otomasyonu Visual Stuido Team Services kaynak denetimi ile aaaIntegrate | Microsoft Docs
description: "Senaryo, bir Azure Otomasyonu hesabı ve Visual Stuido Team Services kaynak denetimi tümleştirmesi kurma açıklanmaktadır."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: Azure powershell, VSTS, kaynak denetimi, Otomasyon
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Azure otomasyonu senaryosu - Visual Studio Team Services ile Otomasyon kaynak denetimi tümleştirme

Bu senaryoda, toomanage Azure Otomasyon çalışma kitabı ya da kaynak denetimi altındaki DSC yapılandırmaları kullanmakta olduğunuz bir Visual Studio Team Services projesi vardır.
Bu makalede nasıl toointegrate VSTS ortamınızla her giriş için sürekli tümleştirme olacağı şekilde Azure Otomasyonu.

## <a name="getting-hello-scenario"></a>Merhaba senaryo alma

Bu senaryo doğrudan hello alabileceğiniz iki PowerShell runbook'ları oluşur [Runbook Galerisi](automation-runbook-gallery.md) de Azure portal hello veya indirme hello [PowerShell Galerisi](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbook'lar

Runbook | Açıklama| 
--------|------------|
Eşitleme VSTS | Runbook'ları veya yapılandırmaları bir iade yapıldığında VSTS kaynak denetiminden içeri aktarın. El ile çalıştırırsanız, içeri aktarma ve tüm runbook'ları veya hello Otomasyon hesabı yapılandırmaları yayımlayın.| 
Eşitleme VSTSGit | Bir iade yapıldığında VSTS Git kaynak denetimi altında yok veya yapılandırmalarını içeri aktarın. El ile çalıştırırsanız, içeri aktarma ve tüm runbook'ları veya hello Otomasyon hesabı yapılandırmaları yayımlayın.|

### <a name="variables"></a>Değişkenler

Değişken | Açıklama|
-----------|------------|
VSToken | Güvenli değişken varlığı hello VSTS kişisel erişim belirteci içeren oluşturur. Nasıl toocreate VSTS kişisel erişim öğrenebilirsiniz hello üzerinde belirteci [VSTS kimlik doğrulaması sayfası](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Bu senaryoyu yükleme ve yapılandırma

Oluşturma bir [kişisel erişim belirteci](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) içinde VSTS Otomasyon hesabınızda toosync hello runbook'ları veya yapılandırması kullanır.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Oluşturma bir [güvenli değişkeni](automation-variables.md) , Otomasyon hesabı toohold hello kişisel erişim belirteci hello runbook tooVSTS ve eşitleme hello runbook'lar veya hello Otomasyon hesabı yapılandırmaları doğrulanabilmesi. Bu VSToken adı verebilirsiniz. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Runbook'ları veya hello Otomasyon hesabı yapılandırmaları eşitlenecek hello runbook içeri aktarın. Merhaba kullanabilirsiniz [VSTS örnek runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) veya hello [Git örnek runbook ile VSTS] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) hello PowerShellGallery.com IF bağlı olarak from VSTS kullanın. Kaynak denetimi veya Git ile VSTS ve tooyour Otomasyon hesabı dağıtın.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Artık [yayımlama](automation-creating-importing-runbook.md#publishing-a-runbook) bir Web kancası oluşturabilmesi için bu runbook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Oluşturma bir [Web kancası](automation-webhooks.md) bu Eşitleme VSTS runbook ve aşağıda gösterildiği gibi hello parametrelerini doldurun. VSTS içinde bir hizmet kancası için ihtiyacınız şekilde hello Web kancası URL'si kopyaladığınızdan emin olun. Merhaba VSAccessTokenVariableName hello (VSToken) önceki toohold hello kişisel erişim belirteci oluşturulan hello güvenli değişkenin adıdır. 

VSTS (Eşitleme-VSTS.ps1) ile tümleştirme şu parametreler hello olur.
### <a name="sync-vsts-parameters"></a>Eşitleme VSTS parametreleri

Parametre | Açıklama| 
--------|------------|
WebhookData | Bu hello VSTS hizmet kanca gönderilen hello iade bilgiler içerir. Bu parametre boş bırakmanız gerekir.| 
ResourceGroup | Bu hello hello Otomasyon hesabı olan hello kaynak grubunun adıdır.|
AutomationAccountName | VSTS ile eşitlenecek hello Otomasyon hesabı Hello adı.|
VSFolder | Merhaba runbook'ları ve yapılandırmaların bulunduğu VSTS hello klasöründe adı.|
VSAccount | Visual Studio Team Services hesabı hello Hello adı.| 
VSAccessTokenVariableName | Merhaba hello VSTS kişisel erişim belirteci tutan hello güvenli değişkeninin adını (VSToken).| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

VSTS GIT (Sync-VSTSGit.ps1) ile kullanıyorsanız, şu parametreler hello sürer.

Parametre | Açıklama|
--------|------------|
WebhookData | Bu hello VSTS hizmet kanca gönderilen hello iade bilgiler içerir. Bu parametre boş bırakmanız gerekir.| ResourceGroup | Bu Otomasyon hesabı hello hello kaynak grubunun hello adı kullanılıyor.|
AutomationAccountName | VSTS ile eşitlenecek hello Otomasyon hesabı Hello adı.|
VSAccount | Visual Studio Team Services hesabı hello Hello adı.|
VSProject | Merhaba runbook'ları ve yapılandırmaların bulunduğu VSTS hello projesinde Hello adı.|
GitRepo | Merhaba Git deposu Hello adı.|
GitBranch | VSTS Git deposu hello dalında Hello adı.|
Klasör | VSTS Git dal hello klasörünün Hello adı.|
VSAccessTokenVariableName | Merhaba hello VSTS kişisel erişim belirteci tutan hello güvenli değişkeninin adını (VSToken).|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Hizmet kanca VSTS içinde bu Web kancası kod girişinde tetikler iadeler toohello klasörü oluşturun. Yeni bir abonelik oluşturduğunuzda Web Kancalarını ile Merhaba hizmet toointegrate olarak seçin. Üzerindeki hizmet kancaları hakkında daha fazla bilgiyi [VSTS hizmet kancaları belgelerine](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Runbook'ları ve VSTS yapılandırmaları tüm iadeler mümkün toodo olması ve bunlar otomatik olarak şimdi eşitleme yapması gerektiğini Otomasyon hesabınızda vardı.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Bu runbook el ile VSTS tarafından tetiklenen olmadan çalıştırırsanız, hello webhookdata parametresi boş bırakabilirsiniz ve belirtilen hello VSTS klasöründen bir tam eşitleme yapar.

Toouninstall hello senaryo istiyorsanız, VSTS hello hizmet kanca kaldırmak için hello VSToken değişkeni silip hello runbook.
