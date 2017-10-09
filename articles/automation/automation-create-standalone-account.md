---
title: "aaaCreate tek başına Azure Otomasyon hesabı | Microsoft Docs"
description: "Öğretici, size hello oluşturma, test ve örnek Azure automation'da güvenlik temel elemanı kimlik doğrulaması yol göstermektedir."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Tek başına Azure Otomasyonu hesabı oluşturma
Bu konu, izleme toocreate hello hello ek yönetim çözümleri veya OMS günlük analizi tooprovide ile tümleştirme dahil olmak üzere olmadan Azure Otomasyonu öğrenin ve tooevaluate isterseniz Azure portalında bir Otomasyon hesabının nasıl Gelişmiş gösterir. runbook işi.  Bu yönetim çözümleri ekleyebilir veya hello gelecekteki herhangi bir noktada günlük analizi ile tümleştirin.  Merhaba Automation hesabı, Azure Resource Manager veya Azure Klasik dağıtım kaynakları yönetme mümkün tooauthenticate runbook'ları demektir.

Hello Azure portalında bir Otomasyon hesabı oluşturduğunuzda, otomatik olarak oluşturur:

* Farklı Çalıştır hesabı, Azure Active Directory'de, bir sertifika yeni bir hizmet sorumlusu oluşturur ve atar hello olan katılımcı rolü tabanlı erişim denetimi (RBAC), runbook'ları kullanarak toomanage Resource Manager kaynakları kullanılır.   
* Olan bir yönetim sertifikasını karşıya yükleyen Klasik farklı çalıştır hesabı runbook kullanan Klasik kaynakları toomanage kullanılır.  

Bu hello işlemi sizin için basitleştirir ve yapı hızla başlamanıza yardımcı olur ve runbook'ları toosupport dağıtma, Otomasyon gerekir.  

## <a name="permissions-required-toocreate-automation-account"></a>Toocreate Otomasyon hesabı gereken izinler
Bu konuda toocomplete gereken izinler ve toocreate veya güncelleştirme Automation hesabı, belirli ayrıcalıkları aşağıdaki hello sahip olmalıdır.   
 
* Sipariş toocreate bir Otomasyon hesabı'da, AD kullanıcı hesabınızın toobe eklenen tooa izinleri eşdeğer toohello sahip rolünü rolüyle Microsoft.Automation kaynaklar için makalesinde ana hatlarıyla gereken [Azure automation'da rol tabanlı erişim denetimi ](automation-role-based-access-control.md).  
* Merhaba uygulama kayıtlar ayarı ayarlarsanız çok**Evet**, Azure AD kiracınızda yönetici olmayan kullanıcılar [AD uygulamaları kaydetmek](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Merhaba uygulama kayıtlar ayarı ayarlarsanız çok**Hayır**, hello kullanıcının bu eylemi gerçekleştirmeden Azure AD genel yönetici olması gerekir. 

Toohello genel yönetici/co-administrator rolüne hello abonelik eklenmeden önce hello aboneliğinin Active Directory örneğine üyesi değilseniz, tooActive dizinine konuk olarak eklenir. Bu durumda, bir "sahip olmadığınız izinleri toocreate..." alırsınız. Merhaba üzerinde uyarı **Automation hesabı Ekle** dikey. Toohello genel yönetici/co-administrator rolü ilk hello aboneliğinin Active Directory örneğinden kaldırılabilir ve toomake öğesine yeniden eklendi eklenen kullanıcılar bunları Active Directory'de tam bir kullanıcı. tooverify bu durumdan hello **Azure Active Directory** hello Azure portal, select bölmesinde **kullanıcılar ve gruplar**seçin **tüm kullanıcılar** ve hello seçtikten sonra belirli bir kullanıcı, select **profil**. Merhaba hello değerini **kullanıcı türü** hello kullanıcı profili altındaki özniteliğini eşit değil **Konuk**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Hello Azure portal ' yeni bir Otomasyon hesabı oluşturma
Bu bölümde, aşağıdaki adımları toocreate hello Azure portalında Azure Automation hesabında hello gerçekleştirin.    

1. Toohello Azure portal hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.
2. **Yeni**’ye tıklayın.<br><br> ![Azure portalında Yeni seçeneğini belirleyin](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Arama **Otomasyon** ve ardından hello seçin arama sonuçları **otomasyon ve Denetim***.<br><br> ![Market’te Otomasyon araması yapıp seçin](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. Merhaba Automation hesapları dikey penceresinde tıklayın **Ekle**.<br><br>![Otomasyon Hesabı ekleme](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Merhaba uyarı aşağıdaki hello görürseniz **Automation hesabı Ekle** dikey penceresinde, hesabınızı hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğin ortak Yöneticisi olmadığından şu.<br><br>![Otomasyon Hesabı Ekleme Uyarısı](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. Merhaba, **Automation hesabı Ekle** dikey penceresinde hello **adı** kutusuna yeni Automation hesabınız için bir ad yazın.
5. Birden fazla aboneliğiniz varsa, hello yeni hesap için bir tane belirtin yeni veya varolan bir **kaynak grubu** ve Azure veri merkezi **konumu**.
6. Merhaba değeri doğrulayın **Evet** Merhaba seçili **oluşturma Azure farklı çalıştır hesabı** seçeneği ve Başlangıç'ı tıklatın **oluşturma** düğmesi.  
   
   > [!NOTE]
   > Seçerseniz toonot oluşturma hello farklı çalıştır hesabı hello seçeneğini belirleyerek **Hayır**, bir uyarı iletisi hello sunulan **Automation hesabı Ekle** dikey.  Merhaba hesap hello Azure portalında oluşturulurken Klasik veya Resource Manager Abonelik dizin hizmeti ve bu nedenle, hiçbir erişim tooresources karşılık gelen bir kimlik doğrulama kimliği aboneliğinizde yok.  Bu mümkün tooauthenticate bu hesaba başvuran runbook'ları engeller ve konusu dağıtım modellerindeki kaynaklara karşı görevleri gerçekleştirin.
   > 
   > ![Otomasyon Hesabı Ekleme Uyarısı](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Merhaba hizmet sorumlusu oluşturulmadığında hello katkıda bulunan rolü atanmaz.
   > 

7. Azure hello Automation hesabını oluşturduğu sırada altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

### <a name="resources-included"></a>Kaynaklar dahil
Hello Otomasyon hesabı başarıyla oluşturulduğunda bazı kaynaklar sizin için otomatik olarak oluşturulur.  Aşağıdaki tablonun hello hello farklı çalıştır hesabının kaynakları özetlenmektedir.<br>

| Kaynak | Açıklama |
| --- | --- |
| AzureAutomationTutorial Runbook |Nasıl tooauthenticate kullanarak izin ver hello farklı çalıştır hesabı gösteren ve tüm hello Resource Manager kaynaklarını alan örnek bir grafik runbook. |
| AzureAutomationTutorialScript Runbook |Nasıl tooauthenticate kullanarak izin ver hello farklı çalıştır hesabı gösteren ve tüm hello Resource Manager kaynaklarını alan örnek bir PowerShell runbook. |
| AzureRunAsCertificate |Otomatik olarak Automation hesabı oluşturma sırasında oluşturulan ya da mevcut hesap için aşağıdaki hello PowerShell komut dosyası kullanarak sertifika varlığı.  Azure Resource Manager kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate sağlar.  Bu sertifikanın bir yıllık kullanım ömrü vardır. |
| AzureRunAsConnection |Otomatik olarak Automation hesabı oluşturma sırasında oluşturulan ya da mevcut hesap için aşağıdaki hello PowerShell Betiği kullanılarak bağlantı varlığı. |

Aşağıdaki tablonun hello hello Klasik farklı çalıştır hesabının kaynakları özetlenmektedir.<br>

| Kaynak | Açıklama |
| --- | --- |
| AzureClassicAutomationTutorial Runbook |Merhaba Klasik farklı çalıştır hesabı (sertifika) kullanarak bir Abonelikteki tüm hello Klasik sanal makineleri alan ve hello VM adını ve durumunu çıkaran örnek grafik runbook. |
| AzureClassicAutomationTutorial Script Runbook |Merhaba Klasik farklı çalıştır hesabı (sertifika) kullanarak bir Abonelikteki tüm hello Klasik sanal makineleri alan ve sonra hello VM adını ve durumunu çıkaran örnek bir PowerShell runbook. |
| AzureClassicRunAsCertificate |Azure Klasik kaynaklarını runbook'lardan yönetebilmeniz için otomatik olarak diğer bir deyişle oluşturulan sertifika varlığı tooauthenticate Azure ile kullanılır.  Bu sertifikanın bir yıllık kullanım ömrü vardır. |
| AzureClassicRunAsConnection |Azure Klasik kaynaklarını runbook'lardan yönetebilmeniz için otomatik olarak diğer bir deyişle oluşturulan bağlantı varlığı tooauthenticate Azure ile kullanılır. |


## <a name="next-steps"></a>Sonraki adımlar
* Grafik yazma hakkında daha fazla toolearn bkz [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).
* PowerShell runbook'ları ile çalışmaya tooget bkz [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md).
* PowerShell iş akışı runbook'ları ile başlatılan tooget bkz [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md).
