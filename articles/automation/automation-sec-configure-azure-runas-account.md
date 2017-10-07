---
title: "bir Azure farklı çalıştır hesabı aaaConfigure | Microsoft Docs"
description: "Bu öğreticide, Azure automation'da güvenlik sorumlusu kimlik doğrulaması hello oluşturma, test ve örnek kullanım açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "hizmet asıl adı, setspn, azure kimlik doğrulaması"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Azure Farklı Çalıştır hesabıyla kimlik doğrulaması runbook’ları
Bu makalede nasıl tooconfigure bir Azure Otomasyonu hesabı hello Azure portal gösterilmektedir. toodo bu nedenle, Azure Resource Manager veya Azure Service Management kaynakları yönetme hello farklı çalıştır hesabı özelliği tooauthenticate runbook'ları kullanın.

Hello Azure portalında bir Otomasyon hesabı oluşturduğunuzda, otomatik olarak iki hesapları oluştur:

* Bir Farklı Çalıştır hesabı. Bu hesap, Azure Active Directory'de (Azure AD) bir hizmet sorumlusu ve bir sertifika oluşturur. Ayrıca, runbook'lar kullanılarak Resource Manager kaynaklarını yöneten hello katkıda bulunan rol tabanlı erişim denetimi (RBAC) atar.
* Klasik Farklı Çalıştır hesabı. Bu hesabı olan bir yönetim sertifikası karşıya yükleme kullanılan toomanage Hizmet Yönetimi veya Klasik kaynakları runbook'ları kullanarak.

Bir Otomasyon hesabı hello işlemi, oluşturma ve runbook'ları toosupport dağıtmaya hemen başlamanıza yardımcı olur için basitleştirir automation'ınızı oluşturma gerekir.

Farklı Çalıştır ve Klasik Farklı Çalıştır hesapları ile şunları yapabilirsiniz:

* Hello Azure portalındaki runbook'lardan kaynak yöneticisi veya Service Management kaynaklarına yönetirken standartlaştırılmış yol tooauthenticate Azure ile sağlayın.
* Azure Uyarıları'nda yapılandırabileceğiniz genel runbook'ların Hello kullan otomatikleştirin.

> [!NOTE]
> Merhaba [Azure uyarı tümleştirme özelliği](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) ile Otomasyon genel runbook'ları farklı çalıştır hesabı ve klasik farklı çalıştır hesabı ile yapılandırılmış bir Otomasyon hesabı gerektirir. Farklı Çalıştır ve klasik farklı çalıştır hesaplarını önceden tanımlanmış bir Otomasyon hesabı seçebilir veya yeni bir Otomasyon hesabı toocreate seçebilirsiniz.
>  

Bu makalede nasıl toocreate hello Azure portalında bir Otomasyon hesabının Azure PowerShell kullanarak Automation hesabını güncelleştirme, hello hesap yapılandırmasını yönetmek ve larınızda kimlik doğrulamasının gösterilmektedir.

Bir Otomasyon hesabı oluşturmaya başlamadan önce bir fikir toounderstand olan ve hello aşağıdakileri göz önünde bulundurun:

* Bir Otomasyon hesabı oluşturulurken zaten hello Klasik veya Resource Manager dağıtım modeli oluşturmuş olabileceğiniz Otomasyon hesaplarını etkilemez.
* Merhaba işlem hello Azure portalında oluşturduğunuz Automation hesapları için çalışır. Toocreate hello Klasik Azure portalında bir hesaptan çalışırken hello farklı çalıştır hesabının yapılandırması çoğaltılmaz.
* Runbook'ları ve varlıkları (örneğin, zamanlamaları veya değişkenleri) yer toomanage Klasik kaynaklar zaten ve runbook'ları tooauthenticate hello yeni Klasik farklı çalıştır hesabıyla istiyorsanız hello aşağıdakilerden birini yapın:

  * toocreate bir Klasik farklı çalıştır hesabı ", farklı çalıştır hesabı yönetme" Merhaba bölümündeki hello yönergeleri izleyin. 
  * tooupdate, var olan hesabınızı, kullanım hello PowerShell'hello "PowerShell kullanarak Automation hesabınız güncelleştir" bölümünde komut dosyası.
* Merhaba yeni farklı çalıştır hesabını ve klasik farklı çalıştır Otomasyon hesabını kullanarak tooauthenticate ihtiyacınız var olan runbook'larınızla hello hello bölümünde sağlanan örnek kod toomodify [kimlik doğrulaması kodu örnekleri](#authentication-code-examples).

    >[!NOTE]
    >Merhaba sertifika tabanlı hizmet sorumlusu kullanan Resource Manager kaynaklarına karşı kimlik doğrulamasını Hello farklı çalıştır hesabı içindir. Merhaba Klasik farklı çalıştır hesabı, bir yönetim sertifikası ile Service Management kaynaklarına göre kimlik doğrulaması için ' dir.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Azure portal hello Automation hesabı oluşturma
Bu bölümde, sırayla hem farklı çalıştır hesabı hem de klasik farklı çalıştır hesabı oluşturur Azure portal hello bir Azure Otomasyonu hesabı oluşturun.

>[!NOTE]
>bir Otomasyon hesabı toocreate, hello hizmet Yöneticileri rolünün üyesi ya da erişim toohello abonelik verme hello aboneliğinin ortak Yöneticisi olmalıdır. Ayrıca bir kullanıcı toothat aboneliğin varsayılan Active Directory örneği olarak eklenmiş olması gerekir. Merhaba hesap ayrıcalıklı bir role atanmış toobe gerekmez.
>
>Merhaba abonelik toohello ortak Yönetici rolü eklenmeden önce hello aboneliğinin Active Directory örneğine üyesi değilseniz, bir konuk olarak tooActive dizin eklenir. Bu örnekte, bir "sahip olmadığınız izinleri toocreate..." alırsınız Merhaba üzerinde uyarı **Automation hesabı Ekle** dikey.
>
>Toohello ortak Yönetici rolü ilk hello aboneliğinin Active Directory örneğinden kaldırılabilir ve yeniden, toomake eklendi eklenen kullanıcılar bunları Active Directory'de tam bir kullanıcı. tooverify hello bu durumdan **Azure Active Directory** hello seçerek Azure portal bölmesinde **kullanıcılar ve gruplar**, seçme **tüm kullanıcılar** ve siz seçtikten sonra Merhaba belirli bir kullanıcı, seçme **profil**. Merhaba hello değerini **kullanıcı türü** hello kullanıcı profili altındaki özniteliğini eşit değil **Konuk**.
>

1. Toohello hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla Azure Portalı'nda oturum açın.

2. **Automation Hesapları**’nı seçin.

3. Merhaba üzerinde **Automation hesapları** dikey penceresinde tıklatın **Ekle**.
Merhaba **Automation hesabı Ekle** dikey pencere açılır.

 ![Merhaba "Automation hesabı ekle" dikey penceresi](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Hesabınızı hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak Yöneticisi değilse, aşağıdaki uyarı hello hello üzerinde görüntülenir **Automation hesabı Ekle** dikey penceresinde:
   >
   >![Automation Hesabı Uyarısı ekleme](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. Merhaba üzerinde **Automation hesabı Ekle** dikey penceresinde hello **adı** kutusuna, yeni Automation hesabınız için bir ad yazın.

5. Birden fazla aboneliğiniz varsa, aşağıdaki hello:

    a. Altında **abonelik**, hello yeni hesap için bir tane belirtin.

    b. **Kaynak Grubu** altında, **Yeni oluştur** veya **Var olanı kullan**’a tıklayın.

    c. **Konum** altında bir Azure veri merkezi belirtin.

6. **Azure Farklı Çalıştır hesabı oluştur** altında **Evet**’i seçin ve ardından **Oluştur**’a tıklayın.

   > [!NOTE]
   > Seçerek toocreate hello farklı çalıştır hesabı değil seçerseniz **Hayır**, bir uyarı iletisi görüntülenir hello **Automation hesabı Ekle** dikey. Merhaba hesap hello Azure portalında oluşturulur, ancak klasik veya Resource Manager Abonelik dizin hizmeti içinde karşılık gelen bir kimlik doğrulama kimliği yok. Sonuç olarak, hello hesap, aboneliğinizde hiçbir erişim tooresources sahiptir. Bu senaryo, ilgili dağıtım modellerindeki kaynaklara göre kimlik doğrulama ve görev gerçekleştirme işlemlerinden bu hesaba başvuran runbook’ları engeller.
   >
   > ![Merhaba "Automation hesabı ekle" dikey uyarı iletisi](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Ayrıca, Hello hizmet sorumlusu oluşturulmadığında çünkü hello katkıda bulunan rolü atanmaz.
   >

7. Azure hello Automation hesabını oluşturduğu sırada altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

### <a name="resources"></a>Kaynaklar
Hello Otomasyon hesabı başarıyla oluşturulduğunda bazı kaynaklar sizin için otomatik olarak oluşturulur. Merhaba kaynakları iki tablo aşağıdaki hello özetlenmiştir:

#### <a name="run-as-account-resources"></a>Farklı Çalıştır hesabının kaynakları

| Kaynak | Açıklama |
| --- | --- |
| AzureAutomationTutorial Runbook | Farklı Çalıştır hesabını kullanarak tooauthenticate hello nasıl gösteren ve tüm hello Resource Manager kaynaklarını alan örnek bir grafik runbook. |
| AzureAutomationTutorialScript Runbook | Farklı Çalıştır hesabını kullanarak tooauthenticate hello nasıl gösteren ve tüm hello Resource Manager kaynaklarını alan örnek bir PowerShell runbook. |
| AzureRunAsCertificate | Automation hesabı oluşturma veya var olan bir hesap için PowerShell Betiği aşağıdaki hello kullandığınızda, otomatik olarak oluşturulan hello sertifika varlığı. Merhaba sertifika Azure Resource Manager kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate sağlar. Merhaba sertifikanın bir yıllık kullanım ömrü vardır. |
| AzureRunAsConnection | bir Otomasyon hesabı oluşturduğunuzda ya da mevcut hesap için hello PowerShell Betiği kullanmak, otomatik olarak oluşturulan hello bağlantı varlığı. |

#### <a name="classic-run-as-account-resources"></a>Klasik Farklı Çalıştır hesabının kaynakları

| Kaynak | Açıklama |
| --- | --- |
| AzureClassicAutomationTutorial Runbook | Tüm hello sanal makineleri alan örnek bir grafik runbook hello Klasik farklı çalıştır hesabı (sertifika) kullanarak bir abonelikte hello Klasik dağıtım modeli kullanılarak oluşturulur ve hello VM adını ve durumunu yazar. |
| AzureClassicAutomationTutorial Script Runbook | Tüm alır örnek bir PowerShell runbook hello Klasik farklı çalıştır hesabı (sertifika) kullanarak bir abonelikte Klasik sanal makineleri hello ve ardından yazma VM adını ve durumunu hello. |
| AzureClassicRunAsCertificate | Merhaba otomatik olarak oluşturulan sertifika varlığı Azure Klasik kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate kullanın. Merhaba sertifikanın bir yıllık kullanım ömrü vardır. |
| AzureClassicRunAsConnection | Merhaba otomatik olarak oluşturulan bağlantı varlığı Azure Klasik kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate kullanın. |

## <a name="verify-run-as-authentication"></a>Farklı Çalıştır kimlik doğrulamasını onaylama
Başarıyla hello yeni farklı çalıştır hesabını kullanarak kimlik doğrulaması bir küçük test tooconfirm gerçekleştirin.

1. Hello Azure portal, daha önce oluşturduğunuz hello Automation hesabını açın.

2. Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.

3. Select hello **AzureAutomationTutorialScript** runbook ve ardından **Başlat** toostart hello runbook. olayları aşağıdaki hello oluşur:
 * A [runbook işi](automation-runbook-execution.md) hello oluşturulur, **iş** dikey penceresinde görüntülenir ve hello iş durumu hello görüntülenir **iş özeti** döşeme.
 * Merhaba iş durumu başlar olarak **sıraya alınan**, bir runbook worker'hello bulut toobecome için bekleyen belirten.
 * Merhaba durumu olur **başlangıç** ne zaman bir çalışan talep hello işi.
 * Merhaba durumu olur **çalıştıran** hello runbook çalışmaya başladığında.
 * Çalışan Hello runbook işi tamamlandığında, durumunu görmelisiniz **tamamlandı**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, hello tıklatın **çıkış** döşeme.  
Merhaba **çıkış** dikey penceresinde görüntülenir, o hello runbook doğrulamasının başarıyla yapıldığını ve hello kaynak grubunda mevcut tüm kaynakların bir listesini döndürülen gösteriliyor.

5. Kapat hello **çıkış** dikey tooreturn toohello **iş özeti** dikey.

6. Kapat hello **iş özeti** dikey ve hello karşılık gelen **AzureAutomationTutorialScript** runbook dikey penceresinde.

## <a name="verify-classic-run-as-authentication"></a>Klasik Farklı Çalıştır kimlik doğrulamasını onaylama
Benzer küçük gerçekleştirmek, hello yeni Klasik farklı çalıştır hesabını kullanarak kimlik doğrulamasını başarıyla tooconfirm sınayın.

1. Hello Azure portal, daha önce oluşturduğunuz hello Automation hesabını açın.

2. Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.

3. Select hello **AzureClassicAutomationTutorialScript** runbook ve ardından **Başlat** çok hello runbook başlatın. olayları aşağıdaki hello oluşur:

 * A [runbook işi](automation-runbook-execution.md) hello oluşturulur, **iş** dikey penceresinde görüntülenir ve hello iş durumu hello görüntülenir **iş özeti** döşeme.
 * Merhaba iş durumu başlar olarak **sıraya alınan**, bir runbook worker'hello bulut toobecome için bekleyen belirten.
 * Merhaba durumu olur **başlangıç** ne zaman bir çalışan talep hello işi.
 * Merhaba durumu olur **çalıştıran** hello runbook çalışmaya başladığında.
 * Çalışan Hello runbook işi tamamlandığında, durumunu görmelisiniz **tamamlandı**.

    ![Güvenlik Sorumlusu Runbook Testi](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, hello tıklatın **çıkış** döşeme.  
Merhaba **çıkış** dikey penceresinde görüntülenir, o hello runbook doğrulamasının başarıyla yapıldığını ve hello Abonelikteki tüm Klasik sanal makineleri listesini döndürülen gösteriliyor.

5. Kapat hello **çıkış** dikey tooreturn toohello **iş özeti** dikey.

6. Kapat hello **iş özeti** dikey ve hello karşılık gelen **AzureAutomationTutorialScript** runbook dikey penceresinde.

## <a name="managing-your-run-as-account"></a>Farklı Çalıştır hesabınızı yönetme
Belirli bir noktada, Automation hesabınız süresi dolmadan önce toorenew hello sertifika gerekir. Bu farklı çalıştır hesabı hello tehlikeye düşünüyorsanız, silin ve yeniden oluşturun. Bu bölümde ele alınmaktadır nasıl tooperform bu işlemler.

### <a name="self-signed-certificate-renewal"></a>Otomatik olarak imzalanan sertifika yenileme
hello farklı çalıştır hesabı için oluşturulan hello otomatik olarak imzalanan sertifika oluşturma başlangıç tarihinden itibaren bir yıl süresi dolar. Sertifikayı süresi dolmadan önce herhangi bir zamanda yenileyebilirsiniz. Yenilediğinizde, yukarı veya etkin olarak çalışan sıraya ve bu farklı çalıştır hesabını hello ile kimlik doğrulaması runbook'ları olumsuz etkilenmez tutulan tooensure hello geçerli geçerli sertifika yok. Merhaba sertifika sona erme tarihini kadar geçerli kalır.

> [!NOTE]
> Automation farklı çalıştır hesabı toouse, kuruluş sertifika yetkiliniz tarafından verilen bir sertifika yapılandırdıktan ve bu seçeneği kullanırsanız, hello Kurumsal Sertifika tarafından otomatik olarak imzalanan bir sertifika kullanılacaktır.

toorenew hello sertifika, aşağıdaki hello:

1. Hello Azure portal, hello Automation hesabını açın.

2. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello **hesap özellikleri** bölmesi altında **hesap ayarlarını**seçin **farklı çalıştır hesapları**.

    ![Otomasyon hesabı özellikleri bölmesi](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. Merhaba üzerinde **farklı çalıştır hesapları** ya da hello Çalıştır hesabı veya toorenew hello sertifika için istediğiniz hello Klasik farklı çalıştır hesabı olarak özellikleri dikey penceresinde, seçin.

4. Merhaba üzerinde **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **yenileme sertifika**.

    ![Farklı Çalıştır hesabının sertifikasını yenileme](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Merhaba sertifika yenileme sırasında altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silme
Bu bölümde açıklanmıştır nasıl toodelete ve bir farklı çalıştır veya Klasik farklı çalıştır hesabını yeniden oluşturun. Bu eylemi gerçekleştirdiğinizde, hello Otomasyon hesabı korunur. Bir farklı çalıştır veya Klasik farklı çalıştır hesabını sildikten sonra hello Azure portalında yeniden oluşturabilirsiniz.

1. Hello Azure portal, hello Automation hesabını açın.

2. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello hesap Özellikler bölmesinde, **farklı çalıştır hesapları**.

3. Merhaba üzerinde **farklı çalıştır hesapları** özellikleri dikey penceresinde, seçin ya da hello Çalıştır hesabı veya Klasik farklı çalıştır hesabı toodelete istiyor. Ardından, hello **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **silmek**.

 ![Farklı Çalıştır hesabını silme](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Merhaba hesap silindi, ancak altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

5. Merhaba hesabı silindikten sonra bunu hello üzerinde yeniden oluşturabilirsiniz **farklı çalıştır hesapları** hello seçerek özellikler dikey penceresini oluşturma seçeneği **Azure farklı çalıştır hesabını**.

 ![Merhaba Automation farklı çalıştır hesabını yeniden oluşturun](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Yanlış yapılandırma
Merhaba Çalıştır veya Klasik farklı çalıştır hesabı toofunction için gereken bazı yapılandırma öğeleri düzgün silinmiş veya yanlış ilk kurulum sırasında oluşturuldu. Merhaba öğeleri içerir:

* Sertifika varlığı
* Bağlantı varlığı
* Farklı Çalıştır hesabı hello katkıda bulunan rolü ' kaldırıldı
* Azure AD'de hizmet sorumlusu veya uygulama

Hello önceki ve diğer örnekleri yanlış hello Otomasyon hesabı hello değiştirir ve durumunu görüntüler algılar *tamamlanmamış* hello üzerinde **farklı çalıştır hesapları** hello özellikleri dikey penceresi hesabı.

![Tamamlanmamış Farklı Çalıştır hesabı yapılandırma durumu](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Merhaba farklı çalıştır hesabı seçin, hesap hello **özellikleri** bölmesi hello aşağıdaki hata iletisini görüntüler:

![Tamamlanmamış Farklı Çalıştır yapılandırma uyarısı iletisi](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Bu farklı çalıştır hesabı sorunları hızla, silme ve hello hesabını yeniden oluşturmayı da çözebilirsiniz.

## <a name="update-your-automation-account-by-using-powershell"></a>PowerShell kullanarak Otomasyon hesabınızı güncelleştirme
Varsa, PowerShell tooupdate var olan Otomasyon hesabınızı kullanabilirsiniz:

* Automation hesabı oluşturma ancak toocreate hello farklı çalıştır hesabı reddedin.
* Runbook kimlik doğrulaması için tooupdate hello tooinclude hello farklı çalıştır hesabı istediğiniz ve zaten bir Automation hesabı toomanage Resource Manager kaynakları kullanın.
* Zaten bir Automation hesabı toomanage Klasik kaynakları kullanır ve tooupdate isterseniz bunu toouse hello yeni bir hesap oluşturma ve runbook'ları ve varlıkları tooit geçirmek yerine Klasik farklı çalıştır hesabı.   
* Kuruluş sertifika yetkilisi (CA) tarafından verilen bir sertifikayı kullanarak toocreate bir farklı çalıştır ve klasik farklı çalıştır hesabı istiyor.

Merhaba komut dosyasında aşağıdaki önkoşullar hello vardır:

* Hello betik yalnızca Windows 10 ve Windows Server 2016 ile Azure Resource Manager modüllerini 2.01 ve daha sonra çalıştırılabilir. Windows'un önceki sürümleri desteklenmez.
* Azure PowerShell 1.0 ve üzeri. Hello PowerShell 1.0 sürümü hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* Merhaba hello değeri olarak başvurulan bir Otomasyon hesabı *– AutomationAccountName* ve *- ApplicationDisplayName* hello PowerShell Betiği aşağıdaki parametreleri.

tooget hello değerleri *Subscriptionıd*, *ResourceGroup*, ve *AutomationAccountName*hello komut dosyaları için gerekli parametreler olan, aşağıdaki hello:
1. İçinde Azure portal Merhaba, Automation hesabınızı hello üzerinde seçin **Otomasyon hesabı** dikey ve ardından **tüm ayarları**. 
2. Merhaba üzerinde **tüm ayarları** dikey altında **hesap ayarlarını**seçin **özellikleri**. 
3. Not hello hello değerlerine **özellikleri** dikey.

![Merhaba Otomasyon hesabı "Özellikler" dikey](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Farklı Çalıştır hesabı PowerShell betiği oluşturma
Bu PowerShell Betiği yapılandırmaları aşağıdaki hello destekler:

* Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.
* Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.
* Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.
* Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturun.

Seçtiğiniz hello yapılandırma seçeneğine bağlı olarak aşağıdaki öğelerindeki hello hello komut dosyası oluşturur.

**Farklı Çalıştır hesapları için:**

* Bir Azure oluşturduğu AD uygulama toobe verilen kendinden imzalı ya da hello ile veya Kurumsal Sertifika genel anahtarı, Azure AD'de Merhaba uygulaması için bir hizmet sorumlusu hesabı oluşturur ve hello mevcut hello hesap için katılımcı rolü atar aboneliği. Bu ayar tooOwner veya başka bir rolle değiştirebilirsiniz. Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).
* Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureRunAsCertificate* hello Otomasyon hesabı belirtilmedi. Merhaba sertifika varlığı hello Azure AD uygulama tarafından kullanılan hello sertifika özel anahtarı içerir.
* Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureRunAsConnection* hello Otomasyon hesabı belirtilmedi. Merhaba bağlantı varlığı hello ApplicationId, Tenantıd, Subscriptionıd ve sertifika parmak izi tutar.

**Klasik Farklı Çalıştır hesapları için:**

* Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureClassicRunAsCertificate* hello Otomasyon hesabı belirtilmedi. Merhaba sertifika varlığı hello yönetim sertifikası tarafından kullanılan hello sertifika özel anahtarı içerir.
* Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureClassicRunAsConnection* hello Otomasyon hesabı belirtilmedi. Merhaba bağlantı varlığı hello abonelik adı, Subscriptionıd ve sertifika varlık adı tutar.

>[!NOTE]
> Merhaba betik yürütüldükten sonra Klasik farklı çalıştır hesabı oluşturmak için her iki seçeneği seçerseniz, karşıya yükleme hello ortak sertifika (.cer dosya adı uzantısı) toohello yönetim deposu hello abonelik için bu hello Otomasyon hesabı içinde oluşturuldu.
> 

tooexecute Merhaba komut dosyası ve hello sertifikasını karşıya yükleyin, aşağıdaki hello:

1. Komut dosyası, bilgisayarınızda aşağıdaki hello kaydedin. İsteğe bağlı olarak bu örnekte, hello dosya adıyla kaydedin *yeni RunAsAccount.ps1*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Bilgisayarınızda **Başlat**’a tıklayın ve yükseltilmiş kullanıcı haklarıyla **Windows PowerShell**’i başlatın.

3. Merhaba PowerShell komut satırı kabuğundan, 1. adımda oluşturduğunuz hello betik içeren gidin toohello klasörü yükseltilmiş.

4. İçin gerek duyduğunuz hello yapılandırma hello parametre değerlerini kullanarak Hello betiğini yürütün.

    **Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Merhaba betiği yürüttükten sonra Azure ile istendiğinde tooauthenticate olacaktır. Merhaba abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.
    >
    >

Merhaba betiği başarıyla yürütüldü sonra hello aşağıdakileri göz önünde bulundurun:
* Otomatik olarak imzalanan bir PKI sertifikası (.cer dosyası) ile bir Klasik farklı çalıştır hesabını oluşturduysanız, hello komut dosyası oluşturur ve bilgisayarınızda hello kullanıcı profili altındaki toohello geçici dosyalar klasörüne kaydeder *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell oturumu kullanılan.
* Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın. Merhaba yönergeleri izleyin [yönetim API sertifikası toohello Klasik Azure portalı karşıya](../azure-api-management-certs.md)ve ardından hello kullanarak Service Management kaynaklarıyla hello kimlik bilgisi yapılandırmasını doğrulamak [örnek kod Service Management kaynaklarıyla tooauthenticate](#sample-code-to-authenticate-with-service-management-resources). 
* Kaldırdıysanız *değil* Klasik farklı çalıştır hesabı oluşturma, Resource Manager kaynaklarıyla kimlik doğrulaması ve hello kullanarak hello kimlik bilgisi yapılandırmasını doğrulamak [örnek Hizmet Yönetimi ile kimlik doğrulaması için kod Kaynakları](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Örnek kod tooauthenticate Resource Manager kaynaklarıyla
Güncelleştirilmiş hello aşağıdakileri kullanabilirsiniz örnek kod, hello gerçekleştirilecek *AzureAutomationTutorialScript* örnek runbook, runbook'larınızla hello farklı çalıştır hesabı toomanage Resource Manager kaynaklarını kullanarak tooauthenticate.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp, tooeasily iş arasında birden fazla abonelik, abonelik bağlamına başvuruyu destekleyen iki ek kod satırı hello komut dosyası içerir. Adlı bir değişken varlığı *Subscriptionıd* hello hello abonelik Kimliğini içerir. Merhaba sonra `Add-AzureRmAccount` cmdlet'i deyiminden hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet ile Merhaba parametre kümesi belirtilen *- Subscriptionıd*. Merhaba değişken adı çok genelse, tooinclude bir önek düzeltmek veya başka bir adlandırma kuralı toomake kullanmak, daha kolay tooidentify. Alternatif olarak, hello parametre kümesini kullanabilirsiniz *varlığıyla - SubscriptionName* yerine *- Subscriptionıd* karşılık gelen bir değişken varlığı ile.

Merhaba runbook'ta kimlik doğrulaması için kullandığınız cmdlet'in hello `Add-AzureRmAccount`, kullandığı hello *ServicePrincipalCertificate* parametre kümesi. Merhaba hizmet asıl sertifikasını değil hello kullanıcı kimlik bilgilerini kullanarak kimlik doğrulamasını yapar.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Örnek kod tooauthenticate Service Management kaynaklarıyla
Merhaba alınan güncelleştirilmiş örnek kodu aşağıdaki hello kullanabilirsiniz *AzureClassicAutomationTutorialScript* örnek runbook, Klasik farklı çalıştır toomanage Klasik kaynakları hesap hello kullanarak tooauthenticate, runbook'ları.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Sonraki adımlar
* [Azure AD’de uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md)
* [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md)
* [Azure Cloud Services’da sertifikalara genel bakış](../cloud-services/cloud-services-certs-create.md)
