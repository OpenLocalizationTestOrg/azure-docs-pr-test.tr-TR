---
title: "Ortak Azure Otomasyonu sorunları aaaTroubleshooting | Microsoft Docs"
description: "Bu makalede bilgiler sağlanmaktadır toohelp sorun giderme ve ortak Azure Otomasyonu hataları düzeltin."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "sorun giderme, Otomasyon hatası, sorunu"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Azure Automation sık karşılaşılan sorunları giderme 
Bu makalede Azure Otomasyonu'nda karşılaşabilirsiniz ve olası çözümlerini tooresolve önerir ortak hatalarında sorun giderme yardımı sunar bunları.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Azure Otomasyon çalışma kitabı ile çalışırken, kimlik doğrulama hataları
### <a name="scenario-sign-in-tooazure-account-failed"></a>Senaryo: Hesap oturum açma tooAzure başarısız oldu
**Hata:** hello Add-AzureAccount veya Login-AzureRmAccount cmdlet ile birlikte çalışırken "Unknown_user_type: Bilinmeyen kullanıcı türü" Merhaba hata alırsınız.

**Merhaba hata nedeni:** hello kimlik bilgisi varlığı adı geçerli değil veya Merhaba, kullanıcı adı ve parola toosetup hello Otomasyonu kimlik bilgisi varlığı kullanılan geçerli değil, bu hata oluşur.

**Sorun giderme ipuçları:** içinde yanlış nedir toodetermine sipariş, hello aşağıdaki adımları gerçekleştirin:  

1. Merhaba dahil olmak üzere tüm özel karakterleri içermediğinden emin olun  **@**  hello Otomasyonu kimlik bilgisi varlık adı tooconnect tooAzure kullandığınız karakter.  
2. Merhaba kullanıcı adı ve yerel PowerShell ISE düzenleyicinizde hello Azure Otomasyonu kimlik bilgisi depolanmış parola kullanıp kullanmadığını denetleyin. Merhaba PowerShell ISE cmdlet'leri aşağıdaki hello çalıştırarak bunu yapabilirsiniz:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Yerel olarak, kimlik doğrulama başarısız olursa, bu Azure Active Directory bilgilerinizi düzgün ayarlamadıysanız anlamına gelir. Çok başvuran[tooAzure Azure Active Directory'yi kullanarak kimlik doğrulaması](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) blog gönderisine tooget hello Azure Active Directory hesabı doğru şekilde ayarlanamıyor.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Senaryo: Oluşturulamıyor toofind hello Azure aboneliği
**Hata:** hello hatasını alıyorsunuz "Merhaba adlı abonelik ``<subscription name>`` bulunamıyor" Merhaba Select-AzureSubscription veya Select-AzureRmSubscription cmdlet ile birlikte çalışırken.

**Merhaba hata nedeni:** hello abonelik adı geçerli değil veya tooget hello Abonelik Ayrıntıları çalışan hello Azure Active Directory kullanıcı hello Abonelik Yöneticisi olarak yapılandırılmamışsa, bu hata oluşur.

**Sorun giderme ipuçları:** sırada toodetermine tooAzure düzgün bir şekilde doğrulandı ve tooselect, çalıştığınız erişim toohello aboneliğiniz ele aşağıdaki adımları hello:  

1. Merhaba çalıştırdığınızdan emin olun **Add-AzureAccount** hello çalıştırmadan önce **Select-AzureSubscription** cmdlet'i.  
2. Hala bu hata iletisini görürseniz, kodunuzu hello ekleyerek değiştirmeye **Get-AzureSubscription** hello aşağıdaki cmdlet'i **Add-AzureAccount** cmdlet'i ve hello kodunu yürütün.  Şimdi Get-AzureSubscription hello çıktısını abonelik ayrıntılarınızı içerip içermediğini doğrulayın.  

   * Tüm abonelik ayrıntıları hello çıktısında görmüyorsanız, bu hello abonelik henüz başlatılmadı anlamına gelir.  
   * Merhaba Abonelik Ayrıntıları hello çıktısında görürseniz, hello doğru abonelik adı veya kimliği ile Merhaba kullandığınızı doğrulayın **Select-AzureSubscription** cmdlet'i.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Senaryo: çok faktörlü kimlik doğrulamasının etkin kimlik doğrulama tooAzure başarısız oldu
**Hata:** hello hatasını alıyorsunuz "Add-AzureAccount: AADSTS50079: güçlü kimlik doğrulaması kayıt (yukarı kanıt) gereklidir" tooAzure Azure kullanıcı adı ve parola kimlik doğrulaması yapılırken.

**Merhaba hata nedeni:** çok faktörlü kimlik doğrulaması Azure hesabınız varsa, bir Azure Active Directory kullanıcı tooauthenticate tooAzure kullanamazsınız.  Bunun yerine, toouse bir sertifika veya bir hizmet asıl tooauthenticate tooAzure gerekir.

**Sorun giderme ipuçları:** toouse hello Azure Hizmet Yönetimi cmdlet'leri bir sertifikayla başvurmak çok[oluşturma ve sertifika toomanage Azure ekleme Hizmetleri.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) Azure Resource Manager cmdlet'lerini hizmet sorumlusuyla toouse başvurmak çok[hizmet sorumlusu Azure portalını kullanarak oluşturuluyor](../azure-resource-manager/resource-group-create-service-principal-portal.md) ve [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Runbook'larla çalışırken sık karşılaşılan hataları
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Senaryo: Merhaba runbook işi başlangıç üç kez denendi, ancak her zaman toostart başarısız oldu
**Hata:** runbook'unuz "" Merhaba iş girişiminde bulunulmamış üç kez ancak işlem başarısız oldu."Merhaba hatasıyla başarısız oluyor

**Merhaba hata nedeni:** bu hata tarafından hello aşağıdaki nedenlerden kaynaklanabilir:  

1. Bellek sınırı.  Biz tooa korumalı alan ne kadar bellek tahsis üzerinde sınırları belgelenen [Otomasyon hizmet sınırları](../azure-subscription-service-limits.md#automation-limits) şekilde bir iş 400 MB'tan fazla bellek kullanması durumunda başarısız. 

2. Modül uyumlu değil.  Bu modül bağımlılıkları doğru değildir ve değilse, runbook'a genellikle "komut bulunamadı" döndürür oluşabilir veya "parametresi bağlanılamıyor" iletisi. 

**Sorun giderme ipuçları:** çözümleri aşağıdaki hello hiçbirini hello sorunu çözer:  

* Önerilen yöntem toowork hello bellek sınırı içinde birden çok runbook arasında toosplit hello iş yükü olan, bellek, değil gereksiz çıktısı, runbook'ları toowrite kadar verileri işlemez veya PowerShell içinde yazma kaç kontrol noktaları göz önünde bulundurun İş akışı runbook'ları.  

* Merhaba adımları izleyerek Azure modüllerinizi ihtiyacınız tooupdate [nasıl tooupdate Azure PowerShell modülleri Azure Automation](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Senaryo: Runbook seri durumdan çıkarılmış nesne nedeniyle başarısız.
**Hata:** runbook'unuz hello hatasıyla başarısız olur. "parametre bağlanamıyor ``<ParameterName>``. Merhaba dönüştürülemiyor ``<ParameterType>`` Deserialized türünde değer ``<ParameterType>`` tootype ``<ParameterType>``".

**Merhaba hata nedeni:** runbook'unuz bir PowerShell iş akışı ise, hello iş akışı askıya alınırsa karmaşık nesneler sipariş toopersist seri durumdan çıkarılmış biçimde runbook durumunuza depolar.  

**Sorun giderme ipuçları:**  
Aşağıdaki üç çözümleri hello hiçbirini bu sorunu çözer:

1. Bir cmdlet tooanother karmaşık nesnelerden cmdlet'ine varsa, bu cmdlet'leri bir Inlinescript alın.  
2. Gereksinim duyduğunuz Hello ad veya değer nesnesinden nesnenin tamamı hello geçirme yerine hello karmaşık geçirin.  
3. Bir PowerShell runbook'u bir PowerShell iş akışı runbook yerine kullanın.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Senaryo: hello kotası aşıldı ayrılan Runbook işi başarısız oldu
**Hata:** runbook işi, "Merhaba aylık toplam iş çalışma zamanı için hello kotası, bu abonelik için de ulaşıldı" Merhaba hatasıyla başarısız oluyor.

**Merhaba hata nedeni:** bu hata hello iş yürütme aşıyor hello 500 dakikalık ücretsiz kota hesabınız için oluşur. Bu kota bir işi sınama, gibi hello Portalı'ndan bir iş başlatmayı Web kancalarını kullanarak ve her iki hello Azure portal kullanarak veya bir iş tooexecute zamanlama iş yürütme, veri merkezinizdeki iş yürütme görevleri tooall türleri geçerlidir. Otomasyon için fiyatlandırma hakkında daha fazla toolearn [Otomasyon fiyatlandırma](https://azure.microsoft.com/pricing/details/automation/).

**Sorun giderme ipuçları:** 500 toochange gerekir ayda hello ücretsiz katmanı toohello temel katmana aboneliğinizden işleme dakikadan fazla toouse istiyorsanız. Aşağıdaki adımları alma hello tarafından toohello temel katmana yükseltebilirsiniz:  

1. Azure aboneliği tooyour oturum  
2. Tooupgrade istediğiniz hello Otomasyon hesabı seçin  
3. Tıklayın **ayarları** > **fiyatlandırma katmanı ve kullanım** > **fiyatlandırma katmanı**  
4. Merhaba üzerinde **fiyatlandırma katmanınızı seçin** dikey penceresinde, select **temel**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Senaryo: bir runbook yürütülürken tanınmayan cmdlet'i
**Hata:** runbook işinizi hello hatasıyla başarısız olur. "``<cmdlet name>``: hello terim ``<cmdlet name>`` cmdlet, işlev, komut dosyası veya çalıştırılabilir program hello adı olarak tanınmıyor."

**Merhaba hata nedeni:** hello PowerShell altyapısı runbook'unuzda kullandığınız hello cmdlet bulamadığında bu hataya neden olur.  Bu hello cmdlet içeren hello modülü hello hesabından eksik olduğundan, bir runbook adı, bir ad çakışması veya başka bir modülde mevcut hello cmdlet da ve Otomasyon hello adı çözümlenemiyor olabilir.

**Sorun giderme ipuçları:** çözümleri aşağıdaki hello hiçbirini hello sorunu çözer:  

* Merhaba cmdlet adı doğru yazdığınızdan emin olun.  
* Merhaba cmdlet Automation hesabınız var ve herhangi bir çakışma olduğundan emin olun. Merhaba cmdlet varsa, tooverify düzenleme modu ve arama toofind hello Kitaplığı'nda istediğiniz ya da çalıştırmak hello cmdlet için bir runbook açmak **Get-Command ``<CommandName>``** .  Bu hello cmdlet doğruladıktan sonra kullanılabilir toohello hesabıdır ve diğer cmdlet'leri veya runbook'ları, hiçbir adıyla çakışıyor olduğunu toohello tuvale Ekle ve runbook'unuzda kümesi geçerli bir parametre kullandığından emin olun.  
* Bir ad çakışması varsa ve iki farklı modüllerde hello cmdlet kullanılabilir, bunu hello cmdlet'i için tam ad hello kullanarak çözebilirsiniz. Örneğin, kullanabileceğiniz **ModuleName\CmdletName**.  
* Merhaba runbook şirket içi karma çalışanı grubu yürütme, ardından o hello emin olun, modül/cmdlet hello karma çalışanı barındıran hello makineye yüklenir.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Senaryo: Bir uzun süre çalışan runbook sürekli hello özel durumuyla başarısız: "Merhaba işi art arda hello çıkarıldı çünkü çalıştıran devam edemiyor aynı denetim noktası".
**Merhaba hata nedeni:** bu toohello 3 saatten uzun yürütülürse, otomatik olarak bir runbook'u askıya Azure Otomasyonu süreçlerinde "Orta Share" izlenmesini son davranış tasarım gereğidir. Ancak, döndürülen hata iletisi "İleri hangi" sağlamaz hello seçenekleri. Bir runbook birçok nedenden dolayı askıya alınabilir. Durum askıya çoğunlukla son tooerrors. Örneğin, bir runbook, bir ağ hatası veya üzerinde bir kilitlenme yakalanmayan bir özel durum Merhaba hello runbook'u çalıştıran Runbook Worker, tüm askıya hello runbook toobe neden ve sürdürüldü olduğunda, son denetim noktasından başlatın.

**Sorun giderme ipuçları:** hello belgelenen çözüm tooavoid toouse denetim noktaları bir iş akışında bu sorunudur.  Daha fazla başvurmak çok toolearn[öğrenme PowerShell iş akışları](automation-powershell-workflow.md#checkpoints).  Daha kapsamlı bir açıklama "Orta paylaşımı" ve denetim noktası bu blog makalesinde bulunabilir [kullanarak denetim noktaları runbook'lardaki](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).

## <a name="common-errors-when-importing-modules"></a>Modülleri içeri aktarırken sık karşılaşılan hataları
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Senaryo: Tooimport modülü başarısız veya cmdlet'leri içeri aktardıktan sonra yürütülemez.
**Hata:** bir modül tooimport başarısız veya başarılı bir şekilde alır, ancak hiçbir cmdlet'leri ayıklanır.

**Merhaba hata nedeni:** bir modül başarıyla Otomasyon olan tooAzure alabilir değil, bazı ortak nedenleri:  

* Merhaba yapısı hello yapısı eşleşmiyor Otomasyonu'nun bu toobe içinde gerekiyor.  
* Merhaba modülü üzerinde dağıtılan tooyour Otomasyon hesabı ayarlanmadı başka bir modül bağlıdır.  
* Merhaba modülü bağımlılıklarını hello klasöründeki eksik.  
* Merhaba **yeni AzureRmAutomationModule** cmdlet kullanılan tooupload hello modülü olmasına ve hello tam depolama yolu vermedi veya hello modülü genel olarak erişilebilir bir URL kullanarak yüklenmedi.  

**Sorun giderme ipuçları:**  
Çözümleri aşağıdaki hello hiçbirini hello sorunu çözer:  

* Bu hello modül biçimini izleyen hello uyduğundan emin olun:  
  ModuleName.Zip  **->**  ModuleName veya sürüm numarası  **->**  (ModuleName.psm1, ModuleName.psd1)
* Merhaba .psd1 dosyasını açın ve hello modülü bağımlılıkları olup olmadığına bakın.  Varsa, bu modülleri toohello Otomasyon hesabı karşıya yükleyin.  
* Başvurulan tüm .dll hello modülü klasörde mevcut olduğundan emin olun.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>İstenen durum yapılandırması (DSC) ile çalışırken sık karşılaşılan hataları
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Senaryo: Bir "Bulunamadı" hatası ile başarısız durumundaki düğümdür
**Hata:** hello düğümü olan bir raporla **başarısız** durumu ve hello hata içeren "Merhaba girişimi tooget hello sunucu https:// eylemden``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction başarısız olduğundan geçerli bir yapılandırma ``<guid>`` bulunamıyor. "

**Merhaba hata nedeni:** bu hata genellikle hello düğümü, bir düğüm yapılandırma adı (örneğin, ABC. yerine tooa yapılandırma adı (örneğin, ABC) atandığı oluşur Web sunucusu).  

**Sorun giderme ipuçları:**  

* Merhaba düğümü "düğüm yapılandırması adı" hello "yapılandırma adı değil" ile atadığınız emin olun.  
* Azure portal veya bir PowerShell cmdlet'ini kullanarak bir düğümü yapılandırma tooa düğümü atayabilirsiniz.

  * İçinde Azure portalını kullanarak bir düğümü yapılandırma tooa düğümü tooassign sipariş, açık hello **DSC düğümleri** dikey penceresinde, ardından bir düğüm seçin ve tıklayın **Ata düğüm yapılandırması** düğmesi.  
  * Buna tooassign PowerShell cmdlet'ini kullanarak bir düğümü yapılandırma tooa düğümü sipariş, kullanın **kümesi AzureRmAutomationDscNode** cmdlet'i

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Senaryo: düğüm yapılandırması (MOF dosyaları) bir yapılandırma derlendiğinde oluşturulamadığı
**Hata:** hello hatasıyla DSC derleme işi askıya alır: "derleme başarıyla tamamlandı, ancak hiçbir düğüm yapılandırması .mofs oluşturuldu".

**Merhaba hata nedeni:** hello aşağıdaki ifade'ne zaman hello **düğümü** anahtar sözcüğü hello DSC yapılandırması değerlendirir çok$ null düğüm yapılandırması üretilen sonra.    

**Sorun giderme ipuçları:**  
Çözümleri aşağıdaki hello hiçbirini hello sorunu çözer:  

* Bu hello ifade sonraki toohello emin olun **düğümü** anahtar sözcüğü hello yapılandırma tanımında değil değerlendirme çok$ null.  
* Merhaba yapılandırması derlenirken ConfigurationData geçirme, hello beklenen değerler geçirdiğinizden emin olun gelen hello yapılandırmayı gerektirir [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Senaryo: hello DSC düğümü rapor "Sürüyor" durumunda kalmış olur
**Hata:** DSC Aracısı çıkarır "ile özellik değerlerini bulunan örneği yok."

**Merhaba hata nedeni:** WMF sürümünüzü yükseltmişseniz ve WMI bozulmuş.  

**Sorun giderme ipuçları:** hello hello'ndaki yönergeleri izlediğinizden [bilinen sorunlar ve sınırlamalar DSC](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix hello sorun.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Senaryo: Oluşturulamıyor toouse bir kimlik bilgisi DSC yapılandırması
**Hata:** hello hatasıyla DSC derleme işi askıya alındı: "özellik türü ' kimlik bilgisi' işlenirken System.InvalidOperationException hata ``<some resource name>``: dönüştürme ve şifreli bir parola düz metin yalnızca izin verilir olarak depolama PSDscAllowPlainTextPassword tootrue ayarlanmış".

**Merhaba hata nedeni:** bir kimlik bilgisi bir yapılandırmada kullanmış ancak uygun sağlamadı **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue her düğüm için yapılandırma.  

**Sorun giderme ipuçları:**  

* Merhaba uygun emin toopass olun **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue hello yapılandırmasında belirtilen her düğüm yapılandırması için. Daha fazla bilgi için çok başvurun[Azure Otomasyonu DSC varlıkları](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Sonraki adımlar
Sorun giderme adımları yukarıdaki hello izleyen ve hello yanıt bulamadıysanız, aşağıdaki hello ek destek seçenekleri gözden geçirebilirsiniz.

* Azure uzmanlarından yardım alın. Sorunu toohello gönderme [MSDN Azure veya yığın taşması forumlar.](https://azure.microsoft.com/support/forums/).
* Bir Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) tıklatıp **alma desteği** altında **teknik ve faturalama desteği**.
* İleti bir betik isteği [Komut Merkezi](https://azure.microsoft.com/documentation/scripts/) bir Azure Otomasyonu runbook çözümü veya bir tümleştirme modülü arıyorsanız.
* Azure Automation ile ilgili geribildirim ya da özellik isteğiniz ileti [kullanıcı sesi](https://feedback.azure.com/forums/34192--general-feedback).
