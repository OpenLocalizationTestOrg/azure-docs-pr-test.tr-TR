---
title: 'Sorun giderme: Azure AD SSPR''yi | Microsoft Docs'
description: "Sorun giderme Azure AD Self Servis parola sıfırlama"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 361ef5f37e4e9de83d3f9d5a8e5177d186fe86d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-self-service-password-reset"></a>Nasıl tootroubleshoot Self Servis parola sıfırlama

Self Servis parola sıfırlama ile ilgili sorunları yaşıyorsanız, izleyin hello öğeleri hızlı bir şekilde çalışmaya tooget şeyler yardımcı olabilir.

## <a name="troubleshoot-self-service-password-reset-errors-that-a-user-may-see"></a>Bir kullanıcı görebilirsiniz Self Servis parola sıfırlama hatalarında sorun giderme

| Hata | Ayrıntılar | Teknik Ayrıntılar |
| --- | --- | --- |
| TenantSSPRFlagDisabled = 9 | Özür dileriz <br> Yöneticinize parola sıfırlama, kuruluşunuz için devre dışı bıraktığından şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticinize başvurun ve tooenable isteyin bu özellik. toolearn daha fazlasını okuyun [Yardım, unuttum Azure AD parolamı](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-update-your-own-password#common-problems-and-their-solutions). | SSPR_0009: Parola sıfırlama yöneticiniz tarafından etkinleştirilmemiş olduğundan algıladık. Lütfen yöneticinize başvurun ve kuruluşunuz için tooenable parola sıfırlama isteyin. |
| WritebackNotEnabled = 10 |Özür dileriz <br> Yöneticiniz, kuruluşunuz için gerekli bir hizmeti etkin değil çünkü şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticinize başvurun ve toocheck isteyin kuruluşunuzun yapılandırması. Bu gerekli hizmet hakkında daha fazla toolearn okuma [parola geri yazma yapılandırma](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-writeback#configuring-password-writeback). | SSPR_0010: Parola geri yazma etkinleştirilmemiş olduğundan algıladık. Lütfen yöneticinize başvurun ve tooenable parola geri yazma isteyin. |
| SsprNotEnabledInUserPolicy = 11 | Özür dileriz  <br> Yöneticiniz, parola sıfırlama, kuruluşunuz için yapılandırılmamış olduğundan şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticinize başvurun ve tooconfigure parola sıfırlama isteyin. Parola hakkında daha fazla toolearn sıfırlama yapılandırma okuma hello makale [hızlı başlangıç: Azure AD Self Servis parola sıfırlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-getting-started). | SSPR_0011: Kuruluşunuz bir parola sıfırlama ilkesi tanımlı değil. Lütfen yöneticinize başvurun ve toodefine bir parola sıfırlama İlkesi isteyin. |
| UserNotLicensed = 12 | Özür dileriz <br> Gerekli olan lisansları kuruluşunuzdan eksik olduğundan şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticinize başvurun ve toocheck lisans atamasını isteyin. lisanslama hakkında daha fazla toolearn hello makalesini okuyun [lisans gereksinimleri için Azure AD Self Servis parola sıfırlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-licensing). | SSPR_0012: Kuruluşunuz gerekli hello lisansları gerekli tooperform parola sıfırlama sahip değil. Lütfen yöneticinize başvurun ve tooreview lisans anlaşmalarını isteyin. |
| UserNotMemberOfScopedAccessGroup = 13 | Özür dileriz <br> Yöneticiniz, hesap toouse parola sıfırlama yapılandırılmamış olduğundan şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticinize başvurun ve tooconfigure isteyin hesabınız parola sıfırlama için. Daha fazla hesap yapılandırması hakkında parola sıfırlama hello makaleyi okuyun için toolearn [parola sıfırlama kullanıcılar için kullanıma alma](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-best-practices). | SSPR_0012:, Parola sıfırlama için etkinleştirilmiş bir grup üyesi değildir. Yönetici ve istek toobe eklenen toohello grubunuza başvurun. |
| UserNotProperlyConfigured = 14 | Özür dileriz <br> Gerekli bilgileri hesabınızdan eksik olduğundan şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticisine başvurun ve tooreset isteyin parolanızı sizin için. Erişim tooyour hesabı yeniden başlattıktan sonra nasıl kaydı hello gerekli bilgileri hello izleyerek hello makaledeki adımları öğrenebilirsiniz [Self Servis parola sıfırlama için kaydetme](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-reset-register). | SSPR_0014: Ek güvenlik bilgisi gerekli tooreset, paroladır. tooproceed, yöneticinize başvurun ve tooreset isteyin parolanızı. Erişim tooyour hesabı oluşturduktan sonra ek güvenlik bilgisi https://aka.ms/ssprsetup adresindeki kaydedebilirsiniz. Yöneticiniz ek güvenlik bilgisi tooyour hesabını hello adımları izleyerek ekleyebilirsiniz [kümesi ve parola sıfırlama için okuma kimlik doğrulama verileri](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-data#set-and-read-authentication-data-using-powershell). |
| OnPremisesAdminActionRequired 29 = | Özür dileriz <br> Kuruluşunuzun parola sıfırlama yapılandırması ile ilgili bir sorun nedeniyle biz şu anda parolanızı sıfırlayamazsınız. Bu durum tooresolve sürebilir başka bir eylem yoktur. Lütfen yöneticinize başvurun ve tooinvestigate isteyin. Merhaba olası sorun hakkında daha fazla toolearn hello makalesini okuyun [parola geri yazma sorun giderme](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback). | SSPR_0029: Biz parolanızı, şirket içi yapılandırmasında tooan hata nedeniyle tamamlayamıyor tooreset şunlardır. Lütfen yöneticinize başvurun ve tooinvestigate isteyin. |
| OnPremisesConnectivityError = 30 | Özür dileriz <br> Bağlantı sorunları tooyour kuruluş nedeniyle şu anda biz parolanızı sıfırlayamazsınız. Hiçbir eylem tootake şu anda olmakla birlikte, daha sonra tekrar denerseniz hello sorun giderilebilir. Merhaba sorun devam ederse, lütfen yöneticinize başvurun ve tooinvestigate isteyin. bağlantı sorunları hakkında daha fazla bilgi toolearn [sorun giderme parola geri yazma bağlantı](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback-connectivity). | SSPR_0030: Biz şirket içi ortamınız ile tooa zayıf bağlantı nedeniyle, parolanızı sıfırlayamazsınız. Lütfen yöneticinize başvurun ve tooinvestigate isteyin.|


## <a name="troubleshoot-password-reset-configuration-in-hello-azure-portal"></a>Parola sıfırlama hello Azure portal yapılandırmasında sorun giderme

| **Hata** | Çözüm |
| --- | --- |
| Merhaba görüntülenmemesini **parola sıfırlama** hello Azure portalında Azure AD'de altında bölümü | Bir Azure AD Premium veya Basic lisansı atanmış toohello yönetici gerçekleştirme hello işlem yoksa bu durum oluşabilir. <br> Bu bir lisans toohello yönetici hesabı hello makale kullanarak söz konusu atayarak çözülebilir [atayabilir, doğrulayın ve lisans sorunları gidermek](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| Belirli yapılandırma seçeneği görmüyorum | Birçok hello UI öğelerini gerektiği kadar gizlenir. Toosee istediğiniz tüm hello seçeneklerini etkinleştirmeyi deneyin. |
| Merhaba görmüyorum **şirket içi tümleştirme** sekmesi | Azure AD Connect indirilir ve parola geri yazma yapılandırılmışsa bu seçenek yalnızca görünür hale gelir. Bu konu hakkında daha fazla bilgi için bkz: hello makale [hızlı ayarları kullanarak Azure AD Connect ile çalışmaya başlama](./connect/active-directory-aadconnect-get-started-express.md). |

## <a name="troubleshoot-password-reset-reporting"></a>Parola sıfırlama raporlama sorunlarını giderme

| **Hata** | Çözüm |
| --- | --- |
| Hello görünür herhangi parola yönetimi etkinlik türleri görmüyorum **Self Servis parola yönetimi** denetim olay kategorisi | Bir Azure AD Premium veya Basic lisansı atanmış toohello yönetici gerçekleştirme hello işlem yoksa bu durum oluşabilir. <br> Bu bir lisans toohello yönetici hesabı hello makale kullanarak söz konusu atayarak çözülebilir [atamak, doğrulayın ve lisans sorunları gidermek] |
| Birden çok kez kullanıcı kayıtlarını Göster | Bir kullanıcı kaydolduğunda, şu anda, şu anda ayrı bir olay olarak kayıtlı verileri tek tek her parçasının oturumunuzu. <br> Bu veriler tooaggregate istiyorsanız hello rapor indirebilirsiniz ve açık hello veri pivot tablo olarak daha fazla esneklik toohave excel.

## <a name="troubleshoot-password-reset-registration-portal"></a>Parola sıfırlama kayıt portalı sorun giderme

| **Hata** | Çözüm |
| --- | --- |
| Dizin, parola sıfırlama için etkinleştirilmedi **yöneticiniz bu özellik, toouse etkinleştirilmemiş** | Anahtar hello **Self Servis parola sıfırlama etkin** çok bayrak**bir grup** veya **herkes** tıklatıp **Kaydet** |
| Bir Azure AD Premium veya Basic lisansı atanmış kullanıcı yok **yöneticiniz bu özellik, toouse etkinleştirilmemiş** | Bir Azure AD Premium veya Basic lisansı atanmış toohello yönetici gerçekleştirme hello işlem yoksa bu durum oluşabilir. <br> Bu bir lisans toohello yönetici hesabı hello makale kullanarak söz konusu atayarak çözülebilir [atayabilir, doğrulayın ve lisans sorunları gidermek](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| İstek işlenirken hata oluştu | Bu pek çok sorundan kaynaklanabilir, ancak genellikle bu hata tarafından bir hizmet kesintisi veya yapılandırma sorunu nedeniyle oluşur. Bu hatayı görürseniz ve işinizin etkileyen ek Yardım için Microsoft Destek'e başvurun. |

## <a name="troubleshoot-password-reset-portal"></a>Parola sıfırlama portalı sorun giderme

| **Hata** | Çözüm |
| --- | --- |
| Dizin, parola sıfırlama için etkinleştirilmedi. | Anahtar hello **Self Servis parola sıfırlama etkin** çok bayrak**bir grup** veya **herkes** tıklatıp **Kaydet** |
| Bir Azure AD Premium veya Basic lisansı atanmış kullanıcı yok | Bir Azure AD Premium veya Basic lisansı atanmış toohello yönetici gerçekleştirme hello işlem yoksa bu durum oluşabilir. <br> Bu bir lisans toohello yönetici hesabı hello makale kullanarak söz konusu atayarak çözülebilir [atayabilir, doğrulayın ve lisans sorunları gidermek](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| Dizin, parola sıfırlama için etkin, ancak kullanıcı eksik veya yanlış biçimlendirilmiş kimlik doğrulama bilgilerine sahip değil | Bu kullanıcı kişi verilerini hello dizindeki devam etmeden önce dosyayı üzerinde düzgün bir şekilde oluşturulduğundan olun. Bu konu hakkında daha fazla bilgi için bkz: hello makale [Azure AD Self Servis parola sıfırlama tarafından kullanılan verileri](active-directory-passwords-data.md). |
| Dizin, parola sıfırlama için etkin, ancak ilke toorequire iki doğrulama adımları olarak ayarlandığında bir kullanıcı kişi verilerini bir parçasını dosyada yalnızca sahiptir. | Bu kullanıcının en az iki düzgün yapılandırılmış iletişim yöntemlerini sahip olduğundan emin olun (örnek: cep telefonu **ve** ofis telefonu) devam etmeden önce. |
| Dizin, parola sıfırlama için etkin ve kullanıcı düzgün şekilde yapılandırıldı, ancak kullanıcı temas oluşturulamıyor toobe | Bu geçici hizmet hatası veya değil biz düzgün algılayamadı yanlış kişi verilerini hello sonucu olabilir. <br> <br> Varsa Hello kullanıcı 10 saniye, yeniden deneyin bekler ve "yöneticinize başvurun" bağlantısı görüntülenir. "Sistem yöneticinize başvurun" a tıklayarak bu kullanıcı hesabı için gerçekleştirilen toobe bir parola sıfırlama isteyen form e-posta tooadministrators gönderir ancak deneyin yeniden tıklandığında hello çağrı yeniden dener. |
| Kullanıcı hiçbir zaman hello parola sıfırlama SMS veya telefon görüşmesi alır | Bu yanlış biçimlendirilmiş telefon numarası hello dizininde hello sonucu olabilir. Merhaba telefon numarası hello biçiminde olduğundan emin olun "+ bilgi xxxyyyzzzzXeeee". <br> <br> (Merhaba çağrısı dağıtılmasından önce bunlar kaldırılır) hello dizininde bir tane belirtin olsa bile parola sıfırlama uzantıları desteklemez. Bir uzantısı olmadan bir numara kullanmayı deneyin veya PBX'iniz hello telefon numarası içine hello uzantısı tümleştirme. |
| Kullanıcı parola sıfırlama e-posta hiçbir zaman alır. | Bu sorunu en yaygın nedeni Hello hello ileti istenmeyen posta Filtresi tarafından reddedilir olmasıdır. İstenmeyen posta, hello e-posta için Önemsiz veya silinen öğeler klasörünü denetleyin. <br> Ayrıca hello selamlama iletisine için doğru e-posta denetimi emin olun. |
| Bir parola sıfırlama İlkesi ayarlamış olmanız, ancak bir yönetici hesabı parola sıfırlama kullandığında, bu ilke uygulanmaz | Microsoft tarafından yönetilir ve ilke tooensure hello yüksek düzeyde güvenlik denetimleri hello yönetici parolasını sıfırlayamaz. |
| Kullanıcı parola sıfırlama bir gün içinde çok fazla kez çalışırken engelledi | Biz tooreset çalışırken mekanizması tooblock kullanıcıların parolalarını çok fazla kez bir kısa süre içinde azaltma otomatik uygulayın. Bu meydana zaman: <br> 1. Kullanıcı toovalidate bir telefon numarası bir saat içinde 5 kez çalışır. <br> 2. Kullanıcı 5 kez bir saat içinde toouse hello güvenlik soruları kapısı çalışır. <br> 3. Kullanıcı tooreset hello için bir parola denemesi 5 kez bir saat içinde aynı kullanıcı hesabı. <br> toofix Bu, 24 saat hello son denemeden sonra hello kullanıcı toowait istemek ve hello kullanıcı olacak sonra mümkün tooreset parolalarını olabilir. |
| Kullanıcı telefon numarasını doğrulanırken bir hata görür | Girilen hello telefon numarası dosya hello telefon numarası eşleşmiyor Bu hata oluşur. Hello kullanıcı hello tam telefon numarasını toouse parola sıfırlama için telefon tabanlı bir yöntem çalışılırken zaman alan ve ülke kodu da dahil olmak üzere, girdiğinden emin olun. |
| İstek işlenirken hata oluştu | Bu pek çok sorundan kaynaklanabilir, ancak genellikle bu hata tarafından bir hizmet kesintisi veya yapılandırma sorunu nedeniyle oluşur. Bu hatayı görürseniz ve işinizin etkileyen ek Yardım için Microsoft Destek'e başvurun. |

## <a name="troubleshoot-password-writeback"></a>Parola geri yazma sorunlarını giderme

| **Hata** | Çözüm |
| --- | --- |
| Parola sıfırlama hizmeti şirket içi hatasıyla hello Azure AD Connect makinenin uygulama olay günlüğünde 6800 başlatılmaz. <br> <br> Federe ekleme ya da parola karması eşitlenen sonra kullanıcıların parolalarını sıfırlayamazsınız. | Parola geri yazma etkinleştirildiğinde, hello eşitleme altyapısı toohello bulut ekleme hizmeti konuşarak hello geri yazma kitaplığı tooperform başlangıç yapılandırması (hazırlama) çağırır. Hazırlama sırasında veya hello WCF uç noktası parola geri yazma sonuçları için Azure AD Connect makinenizin olay günlüğünde hello olay günlüğündeki hatalara başlatılması sırasında karşılaşılan hataları. <br> <br> Geri yazma yapılandırıldıysa, ADSync hizmeti yeniden başlatma sırasında hello WCF uç noktası başlatıldıktan. Ancak, hello uç noktasının hello başlatma başarısız olursa, şu olay 6800 oturum ve hello eşitleme hizmeti başlangıç izin. Bu olay varlığını bu hello parola geri yazma uç başlatılmadı anlamına gelir. Bileşen neden hello uç nokta başlatılamadı gösterir ait tarafından olay günlüğü ayrıntıları olay günlüğü girişleri ile birlikte bu olay (6800) oluşturur. Bu olay günlüğü hatalarını gözden geçirin ve parola geri yazma hala çalışmıyorsa toorestart hello Azure AD Connect deneyin. Merhaba sorun devam ederse toodisable deneyin ve parola geri yazma yeniden etkinleştirin.
| Bir kullanıcı tooreset parola denemesi ya da parola geri yazma etkinleştirilmiş bir hesap kilidini hello işlemi başarısız olur. <br> <br> Hello Azure AD Connect olay günlüğü içeren, bir olay ek olarak, bkz: "eşitleme altyapısı hata hr döndürülen 800700CE, = message = filename hello veya uzantısıdır çok uzun" Merhaba kilidini açtıktan sonra işlemi gerçekleşir. | Merhaba Active Directory hesabı için Azure AD Connect bulmak ve hello parola toocontain en çok 127 karakter sıfırlayın. Daha sonra eşitleme hizmeti hello Başlat menüsünden açmak. TooConnectors gidin ve hello Active Directory bağlayıcısını bulun. Seçin ve Özellikler'i tıklatın. Toohello gidin kimlik bilgileri sayfasında ve hello yeni bir parola girin. Tamam tooclose hello sayfasını seçin. |
| Merhaba son adımı hello Azure AD Connect yükleme işlemi sırasında parola geri yazma yapılandırılamadı belirten bir hata görürsünüz. <br> <br> Hello Azure AD Connect uygulama olay günlüğü "Kimlik doğrulama belirteci alma hatası" hata 32009 metinle içerir. | Bu hata, iki durumda aşağıdaki hello oluşur:<br> <br> a. Merhaba hello Azure AD Connect yükleme işleminin başında belirtilen hello genel yönetici hesabı için hatalı bir parola belirttiniz.<br> b. Merhaba hello Azure AD Connect yükleme işleminin başında bir Federasyon kullanıcısı hello genel yönetici hesabı için belirtilen toouse denediniz.<br> <br> toofix bu hatayı hello genel yöneticinin hello hello Azure AD Connect yükleme işleminin başında belirtilen bir federe hesabını kullanmıyorsanız ve belirtilen bu hello parolanın doğru olduğundan emin olun. |
| Hello Azure AD Connect makine olay günlüğü hatası ait hello tarafından oluşturulan 32002 içerir. <br> <br> Merhaba hata okur: "TooServiceBus bağlanırken bir hata oluştu, hello belirteç sağlayıcısı oluşturamıyor tooprovide bir güvenlik belirteci... oluştu" | Şirket içi ortamınız hello bulutta mümkün tooconnect toohello service bus uç noktası değil. Bu hata genellikle bir giden bağlantı tooa belirli bağlantı noktası veya web adresini engelleyen bir güvenlik duvarı kuralı tarafından kaynaklanır. Bkz: [ağ gereksinimleri](active-directory-passwords-how-it-works.md#network-requirements) daha fazla bilgi için. Bu kurallar güncelleştirdikten sonra yeniden başlatma hello Azure AD Connect makine ve parola geri yazma yeniden çalışmaya başlamanız gerekir. |
| Bazı zaman, Federasyon veya parola karması için çalışma eşitlenen sonra kullanıcıların parolalarını sıfırlayamazsınız. | Azure AD Connect'i yeniden başlatıldığında bazı nadir durumlarda toorestart hello parola geri yazma hizmet başarısız olabilir. Bu durumlarda, ilk olarak, parola geri yazma toobe-tesis içi etkin görünüp görünmediğini denetleyin Bu yapılabilir hello Azure AD Connect Sihirbazı'nı veya powershell (yukarıdaki bkz HowTos bölümünde) kullanarak. Merhaba özelliği etkin toobe görünürse, etkinleştirme veya devre dışı bırakma hello özelliği yeniden hello kullanıcı Arabirimi veya PowerShell ile deneyin. Bu işe yaramazsa, tamamen kaldırıp Azure AD Connect'i yeniden yüklemeyi deneyin. |
| Federe veya parola karması hello var. parola belirten gönderme bir hizmet sorunu oluştu sonra parolalarını bir hata görürsünüz tooreset denemesi kullanıcılar eşitlenir. <br ><br> Ayrıca toothis, işlemleri sırasında parola sıfırlama, yönetim Aracısı ile ilgili bir hata oluştu, şirket içi olay günlüklerinde erişim reddedildi görebilirsiniz. | Olay Günlüğü'nde bu hatalar görürseniz, bu hello (Merhaba Sihirbazı'nda yapılandırma hello aynı anda belirtildi) AD MA hesabı hello parola geri yazma için gerekli izinlere sahip olduğunu doğrulayın. <br> <br> **Bu izin verildikten sonra onu too1 saat hello izinleri tootrickle için yukarı sdprop arka plan görevi hello DC üzerinde aracılığıyla alabilir.** <br> <br> Toowork parola sıfırlama için hello kullanıcı nesnesinin parolasını sıfırlama güvenlik tanımlayıcısını hello damgalı toobe hello izniniz gerekiyor. Bu izni hello kullanıcı nesnesi üzerinde görüntülenir kadar parola sıfırlama toofail erişim reddedildi hatasıyla devam eder. |
| Federe veya parola karması hello var. parola belirten gönderme bir hizmet sorunu oluştu sonra parolalarını bir hata görürsünüz tooreset denemesi kullanıcılar eşitlenir. <br> <br> Ayrıca toothis, işlemleri sırasında parola sıfırlama, hello Azure AD Connect hizmeti "Nesnesi bulunamadı" hata belirten, olay günlükleri, bir hata görebilirsiniz. | Bu hata genellikle o hello eşitleme altyapısı gösterir hello kullanıcı hello AAD bağlayıcı alanı nesnesinde veya hello bağlantılı MV veya AD bağlayıcı alanı nesne oluşturulamıyor toofind olduğu. <br> <br> tootroubleshoot Bu, hello kullanıcı hello geçerli örneğini Azure AD Connect yoluyla şirket içi tooAAD gelen eşzamanlı gerçekten emin olun ve hello bağlayıcı alanları ve MV hello nesneleri hello durumunu inceleyin. Bağlayıcı toohello MV nesne hello "Microsoft.InfromADUserAccountEnabled.xxx" kuralı aracılığıyla hello AD CS nesne olduğunu onaylayın.|
| Federe veya parola karması hello var. parola belirten gönderme bir hizmet sorunu oluştu sonra parolalarını bir hata görürsünüz tooreset denemesi kullanıcılar eşitlenir. <br> <br> Ayrıca toothis, işlemleri sırasında parola sıfırlama, olay günlüklerinde hello Azure AD Connect hizmetinden bir "birden çok eşleşme bulunamadı" hatası belirten bir hata görebilirsiniz. | Bu, o hello eşitleme altyapısı hello MV nesne hello "Microsoft.InfromADUserAccountEnabled.xxx" aracılığıyla bir AD CS nesneleri daha bağlı toomore algılandığında gösterir. Bu, birden fazla ormanda etkinleştirilmiş bir hesabı hello kullanıcının sahip anlamına gelir. **Bu senaryo, parola geri yazma için desteklenmiyor.** |
| Parola işlemleri, bir yapılandırma hatasıyla başarısız oluyor. Merhaba uygulama olay günlüğü içerir <br> <br> Azure AD Connect hata 6329 metinle: 0x8023061f (Merhaba işlemi bu yönetim Aracısı parola eşitleme etkin olmadığından başarısız oldu.) | Bu yeni bir AD ormanı (veya tooremove ve mevcut bir ormana Ekle) sonra değiştirilen tooadd hello Azure AD Connect yapılandırması ise, parola geri yazma özelliği etkinleştirilmiş hello oluşur. Parola işlemleri gibi kullanıcılar için yeni orman başarısız eklendi. toofix hello sorun, devre dışı bırakın ve hello orman yapılandırma değişiklikleri tamamladıktan sonra hello parola geri yazma özelliğini yeniden etkinleştirin. |

## <a name="password-writeback-event-log-error-codes"></a>Parola geri yazma olay günlüğü hata kodları

Parola geri yazma ile ilgili sorunları giderirken en iyi uygulama olay günlüğü, Azure AD Connect makinenizde tooinspect uygulamadır. Bu olay günlüğü olayı ilgilenilen iki kaynaklardan parola geri yazma için içerir. Merhaba ait kaynak işlemlerinin ve sorunları ilgili toohello parola geri yazma işlemi açıklar. Hello ADSync kaynak işlemlerinin ve AD ortamınızdaki sorunları ilgili toosetting parolalar açıklar.

### <a name="source-of-event-is-adsync"></a>Olay ADSync kaynağıdır

| Kod | Ad/iletisi | Açıklama |
| --- | --- | --- |
| 6329 | BAIL: MMS(4924) 0x80230619 – "Merhaba bir kısıtlama engeller engeller parola toohello belirtilen geçerli bir değiştirildi." | Merhaba parola geri yazma hizmet tooset bir parola hello parola geçerlilik süresi, geçmiş, karmaşıklık veya hello etki alanının filtreleme gereksinimlerini karşılamıyor, yerel dizin üzerinde çalıştığında bu olay oluşur. <br> <br> En az parola geçerlilik süresi ve bu zaman aralığı içinde hello parola kısa süre önce değiştirilmiştir varsa, belirtilen hello ulaşana kadar mümkün toochange hello parola yeniden olmayan etki alanınızdaki yaş. Test amacıyla, minimum yaş too0 ayarlanmalıdır. <br> <br> Parola geçmişi gereksinimlerini etkin olması durumunda hello son N zamanlarını N hello parola geçmişi, kullanılmamış bir parola seçmelisiniz ayarı. Hello son N kez kullanılmış bir parolayı seçerseniz, daha sonra bir hata bu durumda bakın. Test amacıyla, geçmiş too0 ayarlanmalıdır. <br> <br> Parola karmaşıklık gereksinimleri varsa, bunların tümünün hello kullanıcı toochange çalıştığında zorlanan veya parola sıfırlama. <br> <br> Parola filtreleri etkinleştirilmiş olması ve bir kullanıcı hello filtreleme ölçütleri karşılamayan bir parola seçerse sıfırlama hello veya işlemi başarısız değiştirin. |
| HR 8023042 | Eşitleme altyapısı döndürülen bir hata hr = 80230402, ileti bir nesne hello ile yinelenen girdiler olduğundan başarısız bir girişim tooget = aynı bağlantı | Bu olay hello birden çok etki alanında aynı kullanıcı kimliği etkin oluşur. Aynı kullanıcı kimliği bulunduğundan ve etkin her, bu hata oluşabilir hesap/kaynak ormanına eşitleniyor ve hello varsa örneğin. <br> <br> Bu hata, benzersiz olmayan bağlayıcı öznitelik (örneğin, diğer ad veya UPN) kullanıyorsanız ve iki kullanıcı o aynı bağlantı özniteliği paylaşan da oluşabilir. <br> <br> tooresolve Bu sorun, yinelenen tüm kullanıcılar, etki alanı içinde yoksa ve her kullanıcı için bir benzersiz bağlantı özniteliğini kullanarak emin olun. |

### <a name="source-of-event-is-passwordresetservice"></a>Olay kaynağına ait değil

| Kod | Ad/iletisi | Açıklama |
| --- | --- | --- |
| 31001 | PasswordResetStart | Bu olay hello şirket içi hizmet isteği hello buluttan kaynaklanan bir federe veya parola karma eşitlenmiş kullanıcı için bir parola sıfırlama algılanan gösterir. Bu olay hello ilk olay her parola geri yazma işlemi sıfırlanır. |
| 31002 | PasswordResetSuccess | Bu olay, bir kullanıcı bir parola sıfırlama işlemi sırasında yeni bir parola seçili, biz bu parola Kurumsal parola gereksinimlerini karşıladığından ve parola geri toohello yerel AD ortam yazıldı belirlenen gösterir. |
| 31003 | PasswordResetFail | Bu olay, bir kullanıcı bir parola seçili ve parola başarıyla toohello şirket içi ortamına geldi, ancak biz tooset hello parola hello yerel AD ortamında çalışırken bir hata oluştu gösterir. Bu durum çeşitli nedenlerle oluşabilir: <br> <br> Merhaba kullanıcının parolasını karşılamıyor hello yaşı, geçmiş, karmaşıklık, veya hello etki alanı için gereksinimleri filtre. Tamamen yeni bir parola tooresolve bu deneyin. <br> <br> Merhaba MA hizmet hesabının hello uygun izinleri tooset hello yeni parola söz konusu hello kullanıcı hesabında yok. <br> <br> Merhaba kullanıcının parola ayarlama işlemleri izin vermez, etki alanı veya enterprise admins gibi bir korumalı grup içindeki hesabıdır. |
| 31004 | OnboardingEventStart | Bu olay parola geri yazma özelliğini Azure AD Connect ile etkinleştirirseniz gerçekleşir ve biz ekleme, kuruluş toohello parola geri yazma web hizmeti başlatıldı gösterir. |
| 31005 | OnboardingEventSuccess | Bu olay hello onboarding işlemi başarılı oldu ve parola geri yazma özelliği hazır toouse olduğunu gösterir. |
| 31006 | ChangePasswordStart | Bu olay hello şirket içi hizmeti hello buluttan kaynaklanan bir federe veya parola karma eşitlenmiş kullanıcı için bir parola değiştirme isteği algıladı gösterir. Bu olay hello ilk olay her parola değişikliği geri yazma işleminde'dır. |
| 31007 | ChangePasswordSuccess | Bu olay, bir kullanıcı yeni bir parola parola değiştirme işlemi sırasında seçilen, biz bu parola Kurumsal parola gereksinimlerini karşıladığından ve parola geri toohello yerel AD ortam yazıldı belirlenen gösterir. |
| 31008 | ChangePasswordFail | Bu olay, bir kullanıcı bir parola seçili ve parola başarıyla toohello şirket içi ortamına geldi, ancak biz tooset hello parola hello yerel AD ortamında çalışırken bir hata oluştu gösterir. Bu durum çeşitli nedenlerle oluşabilir: <br> <br> Merhaba kullanıcının parolasını karşılamıyor hello yaşı, geçmiş, karmaşıklık, veya hello etki alanı için gereksinimleri filtre. Tamamen yeni bir parola tooresolve bu deneyin. <br> <br> Merhaba MA hizmet hesabının hello uygun izinleri tooset hello yeni parola söz konusu hello kullanıcı hesabında yok. <br> <br> Merhaba kullanıcının parola ayarlama işlemleri izin vermez, etki alanı veya enterprise admins gibi bir korumalı grup içindeki hesabıdır. |
| 31009 | ResetUserPasswordByAdminStart | Merhaba şirket içi hizmet isteği hello Yöneticisi'nden bir kullanıcı adına kaynaklanan bir federe veya parola karma eşitlenmiş kullanıcı için bir parola sıfırlama algıladı. Bu olay hello ilk olay her yönetici tarafından başlatılan parola sıfırlama geri yazma işleminde'dır. |
| 31010 | ResetUserPasswordByAdminSuccess | Hello Yöneticisi, bir yönetici tarafından başlatılan parola sıfırlama işlemi sırasında yeni bir parola seçili, biz bu parola Kurumsal parola gereksinimlerini karşıladığından ve parola geri toohello yerel AD ortam yazıldı belirledi. |
| 31011 | ResetUserPasswordByAdminFail | Hello Yöneticisi, bir kullanıcı adına bir parola seçili ve parola başarıyla toohello şirket içi ortamına geldi, ancak biz tooset hello parola hello yerel AD ortamında çalışırken bir hata oluştu. Bu durum çeşitli nedenlerle oluşabilir: <br> <br> Merhaba kullanıcının parolasını karşılamıyor hello yaşı, geçmiş, karmaşıklık, veya hello etki alanı için gereksinimleri filtre. Tamamen yeni bir parola tooresolve bu deneyin. <br> <br> Merhaba MA hizmet hesabının hello uygun izinleri tooset hello yeni parola söz konusu hello kullanıcı hesabında yok. <br> <br> Merhaba kullanıcının parola ayarlama işlemleri izin vermez, etki alanı veya enterprise admins gibi bir korumalı grup içindeki hesabıdır. |
| 31012 | OffboardingEventStart | Bu olay, Azure AD Connect ile parola geri yazma özelliğini devre dışı bırakırsanız oluşur ve biz çıkarma, kuruluş toohello parola geri yazma web hizmeti başlatıldı gösterir. |
| 31013| OffboardingEventSuccess| Bu olay hello çıkarma işlemi başarılı oldu ve parola geri yazma yeteneği başarıyla devre dışı olduğunu gösterir. |
| 31014| OffboardingEventFail| Bu olay hello çıkarma işlemi başarılı değil gösterir. Bu yapılandırması sırasında belirtilen hello Bulut veya şirket içi yönetici hesabı tooa izinleri hatası nedeniyle olabilir veya parola geri yazma özelliğini devre dışı bırakılırken toouse Federasyon bulut genel yönetici çalışıyorsunuz. toofix yönetim izinlerinizi ve bu, bu, onay kullanarak federe hesap hello parola geri yazma özelliği yapılandırılırken.|
| 31015| WriteBackServiceStarted| Bu olay, hello parola geri yazma hizmeti başarıyla başlatıldı ve hazır tooaccept parola yönetimi isteklerini hello buluttan olduğunu gösterir.|
| 31016| WriteBackServiceStopped| Bu olay hello parola geri yazma Hizmeti durdu ve hello bulut gelen tüm parola yönetimi isteklerin başarılı olmaz gösterir.|
| 31017| AuthTokenSuccess| Bu olay, size Azure AD Connect Kurulum toostart hello eklemek veya onboarding işlemi sırasında belirtilen hello genel Yöneticisi için bir yetkilendirme belirteci başarıyla alındı gösterir.|
| 31018| KeyPairCreationSuccess| Bu olay, başarılı bir şekilde hello bulut gönderilen toobe tooyour şirket içi ortamınızda kullanılan tooencrypt parolalardan hello parola şifreleme anahtarı oluşturduğumuz gösterir.|
| 32000| Başvuruları| Bu olay, bir parola yönetimi işlemi sırasında bilinmeyen bir hata gösterir. Daha fazla ayrıntı için olay hello hello özel durum metni bakın. Sorun yaşıyorsanız, devre dışı bırakma ve yeniden etkinleştirme parola geri yazma deneyin. Bu yardımcı olmazsa, olay günlüğü kimliği belirtilen Insider tooyour destek mühendisine izleme hello birlikte bir kopyasını içerir.|
| 32001| ServiceError| Bu olay oluştu toohello bulut parola bağlanırken bir hata hizmetini sıfırlamak gösterir ve genellikle hello şirket içi hizmeti oluşturamıyor tooconnect toohello parola sıfırlama web hizmeti, oluşur.|
| 32002| ServiceBusError| Bu olay tooyour kiracının hizmet veri yolu örneğine bağlanırken bir hata oluştu gösterir. Giden bağlantılar, şirket içi ortamınızda engelleme nedeni bu olabilir. TCP 443 ve toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/ üzerinden bağlantılara izin ver ve yeniden deneyin, güvenlik duvarı tooensure denetleyin. Hala sorun yaşıyorsanız, devre dışı bırakma ve yeniden etkinleştirme parola geri yazma deneyin.|
| 32003| InPutValidationError| Bu olay tooour web hizmeti API'sine geçirilen hello girişi geçersiz olduğunu gösterir. Merhaba işlemi yeniden deneyin.|
| 32004| DecryptionError| Bu olay hello buluttan gelen hello parola çözme bir hata olduğunu gösterir. Bu, hello bulut hizmeti ve şirket içi ortamınız arasında bir şifre çözme anahtarı uyuşmazlığı nedeniyle olabilir. tooresolve bunu devre dışı bırakın ve parola geri yazma, şirket içi ortamınızda yeniden etkinleştirin.|
| 32005| ConfigurationError| Onboarding işlemi sırasında bir yapılandırma dosyası, şirket içi ortamınızda Kiracı özgü bilgileri kaydedin. Bu olay oluştu hello hizmeti var. başlatıldığında bu dosya ya da kaydedilirken bir hata hello dosyası okunurken bir hata oluştu gösterir. toofix Bu sorun, devre dışı bırakma ve parola geri yazma tooforce bu yapılandırma dosyasının bir yeniden yazma yeniden etkinleştirmeyi deneyin.|
| 32007| OnBoardingConfigUpdateError| Hazırlama sırasında hello bulut toohello verilerden servis parola sıfırlama içi gönderin. Bu verileri tooan bellek içi dosyası olan önce bu bilgileri güvenli bir şekilde diskte toohello eşitleme hizmeti toostore gönderilen yazılır. Bu olay, yazma ya da bu verileri bellekte güncelleştirme ile ilgili bir sorun gösterir. toofix Bu sorun, devre dışı bırakma ve parola geri yazma tooforce Bu yapılandırmanın bir yeniden yazma yeniden etkinleştirmeyi deneyin.|
| 32008| ValidationError| Bu olay hello parola sıfırlama web hizmetinden geçersiz bir yanıt aldık gösterir. toofix Bu sorun, devre dışı bırakma ve parola geri yazma yeniden etkinleştirmeyi deneyin.|
| 32009| AuthTokenError| Bu olay, biz bir yetkilendirme Azure AD Connect Kurulum sırasında belirtilen hello genel yönetici hesabı için belirteç alınamadı olduğunu gösterir. Hatalı kullanıcı adı tarafından bu hataya neden olabilir veya parola hello genel yönetici hesabı için belirtilen veya hello genel yönetici hesabı belirtilmediğinden federe. toofix Bu sorun, yeniden çalıştır yapılandırma hello ile kullanıcı adı ve parola düzeltin ve yönetilen bir (yalnızca Bulut veya parola eşitlenmiş) hesap Merhaba yönetici olduğundan emin olun.|
| 32010| CryptoError| Bu olay, bir hata oluştu oluşturma hello parola şifreleme anahtarı veya hello bulut hizmetinden ulaşan parola çözme gösterir. Bu hata muhtemelen ortamınız ile ilgili bir sorunu gösterir. Daha fazla, olay günlüğü toolearn, Hello ayrıntılarını inceleyin ve bu sorunları çözün. Ayrıca bu devre dışı bırakma ve yeniden etkinleştirme hello parola geri yazma hizmet tooresolve deneyebilirsiniz.|
| 32011| OnBoardingServiceError| Bu olay hello şirket içi hizmeti düzgün şekilde hello parola sıfırlama web hizmeti tooinitiate hello onboarding işlemi ile iletişim kuramadı olduğunu gösterir. Bu bir güvenlik duvarı kuralı veya kiracınız için bir kimlik doğrulama belirteci alınırken bir sorun nedeniyle olabilir. toofix bunu, giden bağlantılar TCP 443 ve TCP 9350-9354 veya toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/ engellemediğinden ve o hello tooonboard kullandığınız AAD yönetici hesabı birleşik emin olun.|
| 32013| OffBoardingError| Bu olay hello şirket içi hizmeti düzgün şekilde hello parola sıfırlama web hizmeti tooinitiate hello çıkarma işlemi ile iletişim kuramadı olduğunu gösterir. Bu bir güvenlik duvarı kuralı veya kiracınız için bir yetki belirteci alınırken bir sorun nedeniyle olabilir. toofix bunu, giden bağlantılar 443 veya toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/ engellemediğinden ve o hello toooffboard kullandığınız AAD yönetici hesabı birleşik emin olun.|
| 32014| ServiceBusWarning| Bu olay, biz tooretry tooconnect tooyour kiracının hizmet veri yolu örneği olduğunu gösterir. Normal koşullar altında bu değil ilgili bir sorun olabilir, ancak çoğu zaman, bu olay görürseniz, özellikle bir gecikme süresi yüksek veya düşük bant genişlikli bağlantı olması durumunda, ağ bağlantısı tooservice bus denetimi göz önünde bulundurun.|
| 32015| ReportServiceHealthError| Sipariş toomonitor hello durumunu parola geri yazma hizmetinizi içinde her 5 dakikada bir web hizmeti sinyal veri tooour parola sıfırlama gönderin. Bu olay, bu sistem durumu bilgilerini geri toohello bulut web hizmeti gönderirken bir hata olduğunu gösterir. Bu sistem durumu bilgileri OII veya PII verilerini dahil etmez ve böylece hizmet durumu bilgileri hello bulutta sağladığımız zamanıyla ilgili bir sinyal ve temel hizmeti istatistikleri.|
| 33001| ADUnKnownError| Bu olay, AD tarafından döndürülen bilinmeyen bir hata olduğunu gösterir, bu hata hakkında daha fazla bilgi için hello ADSync kaynağından olayları için hello Azure AD Connect sunucusunun olay günlüğünü denetleyin.|
| 33002| ADUserNotFoundError| Bu olay tooreset veya bir parola hello şirket içi dizininde bulunamadı değişiklik çalışırken bu hello kullanıcıyı gösterir. Bu hello kullanıcı silinen şirket içi kaldığında ancak hello bulutta oluşabilir veya Eşitleme ile ilgili bir sorun varsa. Eşitleme günlüklerinizi denetleyin ve son birkaç çalıştırmak eşitleme ayrıntılar daha fazla bilgi için hello.|
| 33003| ADMutliMatchError| Parola sıfırlama ya da değişiklik isteğinin kaynaklandığı hello buluttan nasıl hello Kurulum işlemi Azure AD Connect toodetermine sırasında belirtilen hello bulut bağlantı kullanırız geri tooa kullanıcı, şirket içi ortamınızda isteği toolink. Bu olay, iki kullanıcı hello ile şirket içi dizininizdeki bulduk olduğunu gösterir. aynı bulut bağlayıcı özniteliği. Eşitleme günlüklerinizi denetleyin ve son birkaç çalıştırmak eşitleme ayrıntılar daha fazla bilgi için hello.|
| 33004| ADPermissionsError| Bu olay, o hello yönetim aracısı hizmet hesabı söz konusu tooset yeni bir parola hesap hello uygun izinleri hello yok gösterir. Bu hello MA hesabı hello kullanıcının ormanındaki hello ormandaki tüm nesneler üzerinde sıfırlama ve değiştirme parola izinleri olduğundan emin olun. Adım 4 toothis nasıl yapılacağı hakkında daha fazla bilgi için bkz: hello uygun Active Directory izinlerini ayarlayabilirsiniz.|
| 33005| ADUserAccountDisabled| Bu olay, biz tooreset çalıştı veya şirket içinde devre dışı bırakılmış bir hesap parolasını değiştirmek gösterir. Merhaba hesabını etkinleştirmek ve hello işlemi yeniden deneyin.|
| 33006| ADUserAccountLockedOut| Olay biz tooreset çalıştı veya şirket içinde kilitli bir hesap parolasını değiştirmek gösterir. Bir kullanıcı bir değişiklik denediniz veya parola işlemi çok fazla kez kısa bir süre içinde sıfırlama kilitlemeleri oluşabilir. Merhaba hesabın kilidini açıp hello işlemi yeniden deneyin.|
| 33007| ADUserIncorrectPassword| Bu olay, bir parola gerçekleştirme değiştirdiğinizde işlemi geçerli bir hatalı parola belirtilen hello kullanıcının gösterir. Merhaba doğru geçerli parolayı belirtin ve yeniden deneyin.|
| 33008| ADPasswordPolicyError| Merhaba parola geri yazma hizmet tooset bir parola hello parola geçerlilik süresi, geçmiş, karmaşıklık veya hello etki alanının filtreleme gereksinimlerini karşılamıyor, yerel dizin üzerinde çalıştığında bu olay oluşur. <br> <br> En az parola geçerlilik süresi ve bu zaman aralığı içinde hello parola kısa süre önce değiştirilmiştir varsa, belirtilen hello ulaşana kadar mümkün toochange hello parola yeniden olmayan etki alanınızdaki yaş. Test amacıyla, minimum yaş too0 ayarlanmalıdır. <br> <br> Parola geçmişi gereksinimlerini etkin olması durumunda hello son N zamanlarını N hello parola geçmişi, kullanılmamış bir parola seçmelisiniz ayarı. Hello son N kez kullanılmış bir parolayı seçerseniz, daha sonra bir hata bu durumda bakın. Test amacıyla, geçmiş too0 ayarlanmalıdır. <br> <br> Parola karmaşıklık gereksinimleri varsa, bunların tümünün hello kullanıcı toochange çalıştığında zorlanan veya parola sıfırlama. <br> <br> Parola filtreleri etkinleştirilmiş olması ve bir kullanıcı hello filtreleme ölçütleri karşılamayan bir parola seçerse sıfırlama hello veya işlemi başarısız değiştirin.|
| 33009| ADConfigurationError| Bu olay, bir parola geri tooyour tooa yapılandırma sorunu nedeniyle dizin Active Directory ile şirket içi yazılırken bir sorun oluştu gösterir. Merhaba ADSync hizmeti hangi hata hakkında daha fazla bilgi için gelen iletiler için Hello Azure AD Connect makinenin uygulama olay günlüğünü denetleyin.|


## <a name="troubleshoot-password-writeback-connectivity"></a>Parola geri yazma bağlantı sorunlarını giderme

Azure AD Connect hizmet kesintilerine hello parola geri yazma bileşeni ile karşılaşıyorsanız, bu tooresolve alabilir bazı hızlı adımlar şunlardır:

* [Yeniden başlatma hello Azure AD Connect eşitleme hizmeti](#restart-the-azure-ad-connect-sync-service)
* [Devre dışı bırakın ve yeniden hello parola geri yazma özelliğini etkinleştirin](#disable-and-re-enable-the-password-writeback-feature)
* [Merhaba en son Azure AD Connect yayın yükleyin](#install-the-latest-azure-ad-connect-release)
* [Parola Geri Yazma Sorunlarını Giderme](#troubleshoot-password-writeback)

Genel olarak, aşağıdaki adımları toorecover yukarıda hello sırayla hizmetinizi hello en hızlı şekilde yürütme öneririz.

### <a name="restart-hello-azure-ad-connect-sync-service"></a>Yeniden başlatma hello Azure AD Connect eşitleme hizmeti

Merhaba yeniden Azure AD Connect eşitleme hizmeti tooresolve bağlantı sorunları veya diğer geçici sorunlar hello hizmetiyle yardımcı olabilir.

1. Yönetici olarak **Başlat** çalıştıran hello sunucuda **Azure AD Connect**.
2. Tür **"Services.msc olanağını"** hello arama kutusu ve tuşuna **Enter**.
3. Merhaba Ara **Microsoft Azure AD eşitleme** girişi.
4. Merhaba hizmeti girişinde sağ tıklayın, **yeniden**ve hello işlemi toocomplete için bekleyin.

   ![Hello Azure AD eşitleme hizmetini yeniden başlatın][Service Restart]

Bu adımları bağlantınızı hello bulut hizmeti ile yeniden oluşturun ve yaşıyor olabilir kesintiler çözümleyin. Merhaba eşitleme hizmeti yeniden başlatmak sorunu çözmezse toodisable deneyin ve bir sonraki adım olarak hello parola geri yazma özelliği yeniden etkinleştirmek öneririz.

### <a name="disable-and-re-enable-hello-password-writeback-feature"></a>Devre dışı bırakın ve yeniden hello parola geri yazma özelliğini etkinleştirin

Devre dışı bırakma ve yeniden hello parola geri yazma özelliğini etkinleştirme özelliği tooresolve bağlantı sorunları yardımcı olabilir.

1. Merhaba yönetici olarak açın **Azure AD Connect Yapılandırma Sihirbazı'nı**.
2. Merhaba üzerinde **tooAzure AD Connect** iletişim kutusunda, girin, **Azure AD genel yönetici kimlik bilgileri**
3. Merhaba üzerinde **tooAD DS bağlanmak** iletişim kutusunda, girin, **AD etki alanı Hizmetleri yönetici kimlik bilgileri**.
4. Merhaba üzerinde **kullanıcılarınızı benzersiz olarak tanımlama** iletişim kutusunda, hello tıklatın **sonraki** düğmesi.
5. Merhaba üzerinde **isteğe bağlı özellikler** iletişim kutusunda, hello işaretini **parola geri yazma** onay kutusu.
6. Tıklatın **sonraki** toohello elde edene kadar değiştirmeden herhangi bir şey iletişim kutusu sayfaları kalan hello aracılığıyla **hazır tooconfigure** sayfası.
7. Bu hello yapılandırma sağlamak sayfası hello gösterir **devre dışı olarak parola geri yazma seçeneği** ve hello yeşil ardından **yapılandırma** değişikliklerinizi toocommit düğmesini.
8. Merhaba üzerinde **tamamlandı** iletişim kutusunda, hello seçimini **Şimdi Eşitle** seçeneğini ve ardından **son** tooclose hello Sihirbazı.
9. Merhaba yeniden **Azure AD Connect Yapılandırma Sihirbazı'nı**.
10. **2-8 arasındaki adımları yineleyin**, olmanız dışında **hello parola geri yazma seçeneği işaretleyin** hello üzerinde **isteğe bağlı özellikler** ekran toore etkinleştir hello hizmet.

Bu adımları bağlantınızı bizim bulut hizmeti ile yeniden oluşturmak ve yaşıyor olabilir kesintiler çözümleyin.

Devre dışı bırakma ve yeniden hello parola geri yazma özelliğini etkinleştirme sorununuzu çözmezse, sonraki adım olarak Azure AD Connect tooreinstall deneyin öneririz.

### <a name="install-hello-latest-azure-ad-connect-release"></a>Merhaba en son Azure AD Connect yayın yükleyin

Azure AD Connect'i yeniden yapılandırma ve bulut hizmetlerimizi ve yerel AD ortamınızı arasında bağlantı sorunları çözebilirsiniz.

Öneririz, yalnızca yukarıda açıklanan hello ilk iki adım denemeden sonra bu adımı gerçekleştirin.

> [!WARNING]
> Merhaba kutusunu eşitleme kuralları dışında özelleştirdiyseniz **yükseltmeye devam etmeden önce bu yedeklemek ve tamamladıktan sonra bunları el ile yeniden**.

1. Hello Hello Azure AD Connect'in en son sürümünü indirme [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).
2. Azure AD Connect zaten yüklü olduğundan, bir yerinde yükseltme tooupdate tooperform, Azure AD Connect yükleme toohello en son sürümü gerekir.
3. Merhaba indirilen paketi yürütmek ve hello ekrandaki yönergeleri tooupdate izleyin, Azure AD Connect makinenize.

Bu adımları bağlantınızı bizim bulut hizmeti ile yeniden oluşturun ve yaşıyor olabilir kesintiler çözümleyin.

Yükleme hello en son sürümünü hello Azure AD Connect sunucusu sorununuzu çözmezse, hello en son sürüm yükledikten sonra son adım olarak devre dışı bırakma ve yeniden etkinleştirme parola geri yazma deneyin öneririz.

## <a name="verify-whether-azure-ad-connect-has-hello-required-permission-for-password-writeback"></a>Azure AD Connect parola geri yazma için gereken hello iznine sahip olup olmadığını doğrulayın 
Azure AD Connect gerektirir AD **parola sıfırlama** izin tooperform parola geri yazma. IF toofind Azure AD Connect hello iznine sahip bir şirket içi AD kullanıcı hesabı, hello Windows etkin izni özelliğini kullanabilirsiniz:

1. TooAzure AD Connect sunucusunun oturum ve hello başlatın **Eşitleme Hizmeti Yöneticisi'ni** (Başlangıç → eşitleme hizmeti).
2. Merhaba altında **Bağlayıcılar** sekmesinde, seçmek içi hello **AD Bağlayıcısı** tıklatıp **özellikleri**.  
![Etkin izni - 2. adım](./media/active-directory-passwords-troubleshoot/checkpermission01.png)  
3. Merhaba Hello açılan iletişim kutusunda seçin **tooActive Directory ormanına Bağlan** sekmesi ve hello Not **kullanıcı adı** özelliği. Azure AD Connect tooperform dizin eşitlemesi tarafından kullanılan hello AD DS hesap budur. Azure AD Connect tooperform parola geri yazma özelliğini için başlangıç AD DS hesabı parola sıfırlama izninizin olması gerekir.  
![Etkin izni - 3. adım](./media/active-directory-passwords-troubleshoot/checkpermission02.png)  
4. Tooan günlüğüne şirket içi etki alanı denetleyicisi ve başlangıç hello **Active Directory Kullanıcıları ve Bilgisayarları** uygulama.
5. Tıklatın **Görünüm** ve emin olun **Gelişmiş Özellikler** seçeneği etkinleşir.  
![Etkin izni - 5. adım](./media/active-directory-passwords-troubleshoot/checkpermission03.png)  
6. Merhaba tooverify istediğiniz AD kullanıcı hesabını arayın. Merhaba hesabında sağ tıklatıp **özellikleri**.  
![Etkin izni - 6. adım](./media/active-directory-passwords-troubleshoot/checkpermission04.png)  
7. Merhaba açılan iletişim kutusunda toohello Git **güvenlik** sekmesinde **Gelişmiş**.  
![Etkin izni - 7. adım](./media/active-directory-passwords-troubleshoot/checkpermission05.png)  
8. Merhaba Gelişmiş güvenlik ayarları açılan iletişim kutusunda, toohello Git **etkili erişim** sekmesi.
9. Tıklayın **bir kullanıcı seçin** ve Azure AD Connect tarafından kullanılan hello AD DS hesabını seçin (3. adıma bakın). Ardından **görüntülemek etkili erişim**.  
![Etkin izni - 9. adım](./media/active-directory-passwords-troubleshoot/checkpermission06.png)  
10. Aşağı kaydırın ve Ara **parola sıfırlama**. Merhaba girdisi denetlenir, hello AD DS hesabı izne sahip demektir hello tooreset hello parolasını seçili AD kullanıcı hesabı.  
![Etkin izni - 10. adım](./media/active-directory-passwords-troubleshoot/checkpermission07.png)  

## <a name="azure-ad-forums"></a>Azure AD forumları

Azure AD hakkında genel bir sorunuz varsa ve Self Servis parola sıfırlama, isteyin hello Topluluk Yardım için hello üzerinde [Azure AD forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Merhaba topluluk üyeleri mühendisleri, ürün yöneticileri, MVP ve arkadaşa BT uzmanları içerir.

## <a name="contact-microsoft-support"></a>Microsoft Destek'e başvurun

Merhaba yanıt tooan sorunu bulamazsanız bizim destek ekiplerini her zaman, daha fazla kullanılabilir tooassist olur.

tooproperly Yardımcısı, servis talebi dahil olmak üzere açarken mümkün olduğu kadar ayrıntılarını sağlayın, isteyin:

* **Genel hello hatanın açıklaması** -hello hatası nedir? Bildirildi hello davranışı neydi? Nasıl biz hello hata üretebileceği? Lütfen mümkün olduğu kadar ayrıntı sağlar.
* **Sayfa** -hangi sayfa olan, hello hata olduğunda fark? Lütfen mümkün tooand bir ekran olduğunda hello URL içerir.
* **Kodu destekleyecek** -hello kullanıcı hello hata gördüğünüz zaman oluşturulan hello destek kodu neydi? 
    * toofind bu yeniden oluşturması hello hatası, ardından hello hello ekranın hello destek kodu bağlantısını ve gönderme hello destek mühendisi hello sonuçları GUID.
    ![Merhaba ekranında hello sonundaki Hello destek kodu bulun][Support Code]
    * Merhaba altındaki desteği olmadan bir sayfada varsa F12 ve SID ve arama CID tuşuna basın ve bu iki sonucu toohello destek mühendisine göndermek.
* **Tarih, saat ve saat dilimi** -Lütfen hello kesin tarih ve saat dahil **hello saat dilimi içeren** hello hata oluştu.
* **Kullanıcı Kimliği** -hello hata gördüğünüz hello kullanıcının edildi? (user@contoso.com)
    * Bu, bir Federasyon kullanıcısı mı?
    * Bu, bir parola karması eşitlenmiş kullanıcı mi?
    * Bu bulut tek kullanıcı mi?
* **Lisans** -hello kullanıcı Azure AD Premium veya Azure AD temel lisansı atanmış sahip mi?
* **Uygulama olay günlüğü** - parola geri yazma özelliğini kullanıyorsanız ve hello hatadır, şirket içi altyapıda, destek ile iletişim kurarken uygulama olay günlüğü'hello Azure AD Connect sunucusundan daraltılmış bir kopyasını içerir.

    

[Service Restart]: ./media/active-directory-passwords-troubleshoot/servicerestart.png "Hello Azure AD eşitleme hizmetini yeniden başlatın"
[Support Code]: ./media/active-directory-passwords-troubleshoot/supportcode.png "Destek kodu hello altında hello pencerenin sağ bulunur"

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
