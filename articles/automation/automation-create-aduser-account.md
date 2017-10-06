---
title: "Azure AD kullanıcı hesabı aaaCreate | Microsoft Docs"
description: "Bu makalede, Azure ve klasik Azure Azure Otomasyonu tooauthenticate runbook'lar için nasıl toocreate bir Azure AD kullanıcı hesabı kimlik bilgileri açıklar."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "azure active directory kullanıcısı, azure hizmet yönetimi, azure ad kullanıcı hesabı"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Azure klasik dağıtımı ve Resource Manager ile Runbook'ların kimliklerini doğrulama
Bu makalede, Azure Klasik dağıtım modeli veya Azure Resource Manager kaynaklarına karşı çalışan Azure Automation runbook'ları için tooconfigure bir Azure AD kullanıcı hesabı gerçekleştirmeniz gereken hello adımları açıklanmaktadır.  Bu toobe devam ederken desteklenen kimlik doğrulama kimliği, Azure Resource Manager tabanlı runbook, Azure farklı çalıştır hesabı yöntemiyle hello önerilir.       

## <a name="create-a-new-azure-active-directory-user"></a>Yeni bir Azure Active Directory kullanıcısı oluşturma
1. Toohello Klasik Azure Portalı'nda hello toomanage istediğiniz Azure aboneliği için Hizmet Yöneticisi olarak oturum açın.
2. Seçin **Active Directory**ve ardından kuruluş dizininizin hello adını seçin.
3. Select hello **kullanıcılar** sekmesini tıklatın ve ardından hello komut alanında seçin **Kullanıcı Ekle**.
4. Merhaba üzerinde **bu kullanıcı hakkında bize** sayfasında **kullanıcı türünü**seçin **kuruluşunuzdaki yeni kullanıcı**.
5. Bir kullanıcı adı girin.  
6. Merhaba Active Directory sayfasında Azure aboneliğinizle ilişkili hello dizin adını seçin.
7. Merhaba üzerinde **kullanıcı profili** sayfasında, bir ilk ve son adı, kullanıcı dostu bir ad ve kullanıcı hello sağlayın **rolleri** listesi.  **Multi-Factor Authentication’ı Etkinleştir** seçeneğini kullanmayın.
8. Merhaba kullanıcının tam adını ve geçici parolasını unutmayın.
9. **Ayarlar > Yöneticiler > Ekle**’yi seçin.
10. Merhaba, oluşturduğunuz hello kullanıcının tam kullanıcı adını yazın.
11. Kullanıcı toomanage hello istediğiniz hello aboneliği seçin.
12. Azure oturumunu kapatın ve ardından yeni oluşturduğunuz geri hello hesabıyla oturum. İstendiğinde toochange hello kullanıcının parolasını olacaktır.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Klasik Azure portalında Otomasyon hesabı oluşturma
Bu bölümde, Azure Klasik dağıtım kaynakları yöneten runbook'larınızla ile adımları toocreate hello Azure portalı kullanmak için Azure Automation hesabında aşağıdaki hello gerçekleştirin.  

> [!NOTE]
> Merhaba Klasik Azure portalıyla oluşturulan automation hesapları hem hello Azure Klasik ve Azure portal ile ya da yönetilebilir cmdlet'leri kümesi. Merhaba hesap oluşturulduktan sonra nasıl oluşturmak ve kaynakları hello hesabı içinde yönetmek yönelttiğiniz fark etmez. Azure portal toocreate yerine bunu kullanmalısınız sonra toocontinue toouse hello Klasik Azure portalı, planlıyorsanız, Automation hesaplarını hello.
> 
> 

1. Toohello Klasik Azure Portalı'nda hello toomanage istediğiniz Azure aboneliği için Hizmet Yöneticisi olarak oturum açın.
2. **Automation**’ı seçin.
3. Merhaba üzerinde **Otomasyon** sayfasında, **Automation hesabı oluşturma**.
4. Merhaba, **Automation hesabı oluşturma** kutusunda, yeni Automation hesabınız için bir ad yazın ve seçin bir **bölge** hello aşağı açılan listeden.  
5. Tıklatın **Tamam** tooaccept ayarlarınızı ve hello hesabı oluşturun.
6. Oluşturulduktan sonra hello üzerinde listelenecektir **Otomasyon** sayfası.
7. Merhaba hesabına tıklayın ve, toohello Pano sayfası çıkarır.  
8. Merhaba Automation panosu sayfasında, seçin **varlıklar**.
9. Merhaba üzerinde **varlıklar** sayfasında, **ayarları Ekle** hello hello sayfa sonunda yer alan.
10. Merhaba üzerinde **ayarları Ekle** sayfasında, **kimlik bilgileri Ekle**.
11. Merhaba üzerinde **kimlik bilgisi tanımla** sayfasında, **Windows PowerShell kimlik bilgisi** hello gelen **kimlik bilgisi türü** aşağı açılan listesinde ve hello kimlik bilgisi için bir ad sağlayın.
12. Merhaba aşağıdaki üzerinde **kimlik bilgisi tanımla** sayfasında hello daha önce oluşturulmuş hello AD kullanıcı hesabı hello kullanıcı adı türü **kullanıcı adı** hello alan ve hello Parolada **parola**ve **parolayı onayla** alanları. Tıklatın **Tamam** toosave değişikliklerinizi.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Hello Azure portalından Automation hesabı oluşturma
Bu bölümde, Azure Kaynak Yöneticisi modunda kaynakları yöneten runbook'larınızla ile adımları toocreate hello Azure portalı kullanmak için Azure Automation hesabında aşağıdaki hello gerçekleştirin.  

1. Toohello Azure portal hello toomanage istediğiniz Azure aboneliği için Hizmet Yöneticisi olarak oturum açın.
2. **Automation Hesapları**’nı seçin.
3. Merhaba Automation hesapları dikey penceresinde tıklayın **Ekle**.<br><br>![Otomasyon Hesabı ekleme](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. Merhaba, **Automation hesabı Ekle** dikey penceresinde hello **adı** kutusuna yeni Automation hesabınız için bir ad yazın.
5. Birden fazla aboneliğiniz varsa, mevcut veya yeni hesap hello yanı sıra yeni için hello belirtin **kaynak grubu** ve Azure veri merkezi **konumu**.
6. Merhaba değeri seçin **Evet** hello için **oluşturma Azure farklı çalıştır hesabı** seçeneği ve Başlangıç'ı tıklatın **oluşturma** düğmesi.  
   
    > [!NOTE]
    > Seçerseniz toonot oluşturma hello farklı çalıştır hesabı hello seçeneğini belirleyerek **Hayır**, bir uyarı iletisi hello sunulur **Automation hesabı Ekle** dikey.  Merhaba hesabı oluşturuldu ve toohello atanmış durumdayken **katkıda bulunan** rol hello abonelikte, abonelikler dizini hizmetinizde ve bu nedenle, hiçbir erişim karşılık gelen bir kimlik doğrulama kimliği olmaz aboneliğinizde kaynaklar.  Bu mümkün tooauthenticate bu hesaba başvuran runbook'ları önlemek ve Azure Resource Manager kaynaklarına karşı görevleri gerçekleştirin.
    > 
    >

    <br>![Automation Hesabı Uyarısı ekleme](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Azure hello Automation hesabını oluşturduğu sırada altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

Merhaba kimlik bilgisi Hello oluşturulması tamamlandığında, hello AD kullanıcı hesabı ile bir kimlik bilgisi varlığı tooassociate hello Automation hesabını daha önce oluşturduğunuz toocreate gerekir.  Unutmayın, yalnızca hello Automation hesabı oluşturduk ve bir kimlik doğrulama kimliğiyle ilişkili değil.  Hello özetlenen hello adımları gerçekleştirin [kimlik bilgisi varlıkları Azure automation'da](automation-credentials.md#creating-a-new-credential-asset) ve hello değerini girmeniz **kullanıcıadı** hello biçiminde **etki alanı\kullanıcı**.

## <a name="use-hello-credential-in-a-runbook"></a>Bir runbook'ta Hello kimlik bilgisi kullanma
Hello kullanarak bir runbook'taki hello kimlik bilgisini getirebilir [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) etkinliği ve onunla kullanmak [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour Azure aboneliği. Merhaba kimlik bilgisi birden çok Azure aboneliği Yöneticisi olduğunu sonra da kullanmalısınız [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello doğru. Bu, genellikle çoğu Azure Automation runbook hello üstünde görünür hello örnek aşağıdaki Windows PowerShell içinde gösterilir.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Runbook uygulamanızdaki her [kontrol noktası](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) sonrasında bu satırları yinelemelisiniz. Merhaba runbook askıya alınır ve başka bir çalışan üzerinde işlemi sürdürürse, tooperform hello yeniden kimlik doğrulaması gerekir.

## <a name="next-steps"></a>Sonraki Adımlar
* Gözden geçirme hello farklı runbook türleri ve kendi runbook'ların nereden oluşturma adımları hello makalede [Azure Automation runbook türleri](automation-runbook-types.md)

