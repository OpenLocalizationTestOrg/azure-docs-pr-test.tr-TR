---
title: "aaaUse mevcut NPS sunucuları tooprovide Azure MFA özellikleri | Microsoft Docs"
description: "Merhaba ağ ilkesi sunucusu uzantısı Azure çok faktörlü kimlik doğrulaması için bir basit çözüm tooadd bulut tabanlı iki aşamalı vericiation özellikleri tooyour var olan kimlik doğrulama altyapısıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Varolan NPS altyapınızı Azure multi-Factor Authentication ile tümleştirme

Hello Azure MFA için ağ ilkesi sunucusu (NPS) uzantısı mevcut sunucularınızı kullanarak bulut tabanlı MFA yetenekleri tooyour kimlik doğrulaması altyapısı ekler. Merhaba NPS uzantısı telefon araması, SMS mesajı ya da telefon uygulama doğrulama tooyour var olan kimlik doğrulama akışı yapılandırın ve yeni sunucuların bakımını tooinstall gerek kalmadan ekleyebilirsiniz. 

Bu uzantı hello Azure MFA sunucusu dağıtmadan tooprotect VPN bağlantıları isteyen kuruluşların için oluşturuldu. Merhaba NPS uzantısı ikinci öğe olarak kimlik doğrulaması Federasyon ya da eşitlenmiş kullanıcı için RADIUS ve bulut tabanlı Azure MFA tooprovide arasında bir bağdaştırıcı olarak görev yapar.

Hello NPS uzantısı için Azure MFA kullanıldığında, hello kimlik doğrulaması akışı hello aşağıdaki bileşenleri içerir: 

1. **NAS/VPN sunucusu** VPN istemcilerinden gelen istekleri alır ve bunları RADIUS isteklerini tooNPS sunucularına dönüştürür. 
2. **NPS sunucusu** tooActive Directory tooperform hello birincil kimlik doğrulaması için RADIUS isteklerini ve, başarı hello istek yüklü tooany uzantılarının geçirir hello bağlanır.  
3. **NPS uzantısı** hello ikincil kimlik doğrulaması için bir istek tooAzure MFA tetikler. Merhaba uzantısı hello yanıtını aldıktan sonra ve MFA testini hello başarılı olursa, Azure STS tarafından verilen bir MFA talep dahil güvenlik belirteçleri hello NPS sunucusu sağlayarak hello kimlik doğrulama isteğini tamamlar.  
4. **Azure MFA** Azure Active Directory tooretrieve hello kullanıcının ayrıntılarını ile iletişim kurar ve bir doğrulama yapılandırılmış yöntemi toohello kullanıcı kullanılarak hello ikincil kimlik doğrulaması gerçekleştirir.

Aşağıdaki diyagramda hello bu üst düzey kimlik doğrulaması istek akışının gösterilmektedir: 

![Kimlik doğrulama akışı diyagramı](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Dağıtımınızı planlama

özel bir yapılandırma gerekmez şekilde hello NPS uzantısı artıklık, otomatik olarak yönetir.

Gereksinim duyduğunuz kadar Azure MFA etkin NPS sunucusu oluşturabilirsiniz. Birden çok sunucuya yüklerseniz, bunların her biri için bir fark istemci sertifikası kullanmanız gerekir. Her sunucu için bir sertifika oluşturmak, her sertifika tek tek güncelleştirin ve kapalı kalma süresi hakkında tüm sunucularınız üzerinde endişelenmeyin anlamına gelir.

Toobe hello yeni Azure MFA etkin NPS sunucuları farkında gerekiyor VPN sunucularını kimlik doğrulama isteklerini yönlendirir.

## <a name="prerequisites"></a>Ön koşullar

Merhaba NPS uzantısı mevcut altyapınızla toowork amaçlanmıştır. Önkoşullar, önce aşağıdaki hello başlamak olduğundan emin olun.

### <a name="licenses"></a>Lisansları

Hello Azure MFA için NPS uzantısı olan kullanılabilir toocustomers ile [Azure multi-Factor Authentication için lisans](multi-factor-authentication.md) (Azure AD Premium, EMS veya MFA abonelik dahil).

### <a name="software"></a>Yazılım

Windows Server 2008 R2 SP1 veya üstü.

### <a name="libraries"></a>Kitaplıkları

Bu kitaplıklar hello uzantısı ile otomatik olarak yüklenir.
-   [Visual Studio 2013 (X64) için Visual C++ yeniden dağıtılabilir paketleri](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Microsoft Azure Active Directory için Windows PowerShell modülü sürümü 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Merhaba NPS uzantısı kullanan herkes eşitlenen tooAzure Active Directory olmalıdır Azure AD Connect'i kullanarak ve MFA için kaydolması gerekir.

Merhaba uzantısını yüklediğinizde, Azure AD kiracınız için hello dizin kimliği ve yönetici kimlik bilgileri gerekir. Dizin Kimliğinizi hello bulabilirsiniz [Azure portal](https://portal.azure.com). Select hello yönetici olarak oturum aç **Azure Active Directory** hello soldaki simgesi seçip **özellikleri**. Kopya hello GUID hello **dizin kimliği** kutusunda ve kaydedin. Merhaba NPS uzantısını yüklediğinizde bu GUID hello Kiracı kimliği kullanın.

![Azure Active Directory özellikleri'nin altında dizin kimliği bulunamıyor](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Ortamınızı hazırlama

Merhaba NPS uzantısını yüklemeden önce tooprepare istediğiniz, ortam toohandle hello kimlik doğrulama trafiğini.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Etki alanına katılmış bir sunucuda Hello NPS rolünü etkinleştir

Merhaba NPS sunucusu tooAzure Active Directory bağlanır ve hello MFA istekleri doğrular. Bu rol için bir sunucu seçin. RADIUS olmayan tüm istekler hataları hello NPS uzantısı oluşturur çünkü diğer hizmetler gelen istekleri işleyemez bir sunucu seçme öneririz.

1. Merhaba, sunucunuzda açmak **Ekle roller ve Özellikler Sihirbazı** hello Sunucu Yöneticisi'ni Hızlı Başlangıç menüsünde gelen.
2. Seçin **rol tabanlı veya özellik tabanlı yükleme** için yükleme türü.
3. Select hello **Ağ İlkesi ve Erişim Hizmetleri** sunucu rolü. Bir pencere tooinform, gerekli özellikleri toorun bu rolü pop.
4. Hello sihirbaza hello onay sayfası kadar devam edin. Seçin **yükleme**.

NPS için belirlenmiş bir sunucunuz varsa, bu sunucu toohandle yapılandırmanız da hello VPN çözümü gelen gelen RADIUS istekleri.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>VPN çözümü toocommunicate ile Merhaba NPS sunucusunu yapılandırın

Kullandığınız VPN çözümüne bağlı olarak, RADIUS kimlik doğrulama İlkesi farklılık adımları tooconfigure hello. Bu ilke toopoint tooyour RADIUS NPS sunucusunu yapılandırın.

### <a name="sync-domain-users-toohello-cloud"></a>Eşitleme etki alanı kullanıcıları toohello bulut

Bu adım zaten kiracınız üzerinde tam olabilir, ancak onu iyi toodouble-Azure AD Connect veritabanlarınızı yakın zamanda eşitlendi olup olmadığını denetler.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Seçin **Azure Active Directory** > **Azure AD Connect**
3. Eşitleme durumunuzu doğrulayın **etkin** ve son eşitleme değerinden bir saatten önce gerçekleştirildi.

Yeni gidiş eşitleme devre dışı tookick gerekiyorsa, bize yönergeleri hello [Azure AD Connect eşitleme: Zamanlayıcı](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Kullanıcılarınızın kullanabilirsiniz hangi kimlik doğrulama yöntemlerini belirleme

NPS uzantısı dağıtımı ile hangi kimlik doğrulama yöntemleri kullanılabilir etkileyen iki Etkenler vardır:

1. Merhaba RADIUS istemcisi arasında kullanılan hello parola şifreleme algoritması (VPN, Netscaler sunucu veya diğer) ve hello NPS sunucuları.
   - **PAP** hello bulutta Azure mfa tüm hello kimlik doğrulama yöntemlerini destekler: telefon araması, tek yönlü SMS mesajı, mobil uygulama bildirimi ve mobil uygulama doğrulama kodu.
   - **CHAPV2** ve **EAP** telefon araması ve mobil uygulama bildirimi destekler.
2. Merhaba giriş istemci uygulaması hello yöntemler (VPN, Netscaler sunucu veya diğer) işleyebilir. Örneğin, bazı araçlar hello VPN istemcisi sahip bir metin veya mobil uygulama doğrulama kodu tooallow hello kullanıcı tootype?

Merhaba NPS uzantısı dağıtırken hangi yöntemler, kullanıcılarınız için kullanılabilir Bu etkenler tooevaluate kullanın. RADIUS istemciniz PAP destekler, ancak bir doğrulama kodu için girdi alanlarının hello istemci UX yok, ardından telefon araması ve mobil uygulama bildirimi hello iki desteklenen seçeneklerdir.

Yapabilecekleriniz [desteklenmeyen kimlik doğrulama yöntemleri devre dışı](multi-factor-authentication-whats-next.md#selectable-verification-methods) azure'da.

### <a name="enable-users-for-mfa"></a>Kullanıcılar için MFA'yı etkinleştirin

Merhaba tam NPS uzantısını dağıtmadan önce tooperform iki aşamalı doğrulamayı istediğiniz hello kullanıcıları için tooenable MFA gerekir. Daha fazla hemen tootest hello uzantısını dağıtmak, çok faktörlü kimlik doğrulaması için tam olarak kayıtlı en az bir sınama hesabı gerekir.

Bir test hesabı kullanmaya bu adımları tooget kullanın:
1. Çok oturum[https://aka.ms/mfasetup](https://aka.ms/mfasetup) bir test hesabıyla. 
2. Merhaba istemleri tooset doğrulama yöntem izleyin.
3. Ya da bir koşullu erişim ilkesi oluşturun veya [hello kullanıcı durumunu değiştirme](multi-factor-authentication-get-started-user-states.md) hello sınama hesabı için iki aşamalı doğrulamayı toorequire. 

Merhaba NPS uzantısı ile kimlik doğrulama gerçekleştirmeden önce kullanıcılarınızın toofollow bu adımları tooenroll da gerekir.

## <a name="install-hello-nps-extension"></a>Merhaba NPS uzantısını yükleyin

> [!IMPORTANT]
> Merhaba NPS uzantısı hello VPN erişim noktası başka bir sunucuya yükleyin.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Karşıdan yükleyip hello NPS uzantısı için Azure MFA

1.  [Merhaba NPS uzantısı karşıdan](https://aka.ms/npsmfa) hello Microsoft Download Center gelen.
2.  Merhaba ikili toohello tooconfigure istediğiniz ağ ilkesi sunucusu kopyalayın.
3.  Çalıştırma *setup.exe* ve hello yükleme yönergeleri izleyin. Hatalarla karşılaşırsanız, iki kitaplıkları hello önkoşul bölümünden başarıyla yüklenen, hello denetleyin.

### <a name="run-hello-powershell-script"></a>Merhaba PowerShell betiğini çalıştırın

Hello yükleyici, bu konumda bir PowerShell Betiği oluşturur: `C:\Program Files\Microsoft\AzureMfa\Config` (C:\ olduğu yükleme sürücüsü). Bu PowerShell Betiği hello aşağıdaki eylemleri gerçekleştirir:

-   Kendinden imzalı bir sertifika oluşturun.
-   Merhaba sertifika toohello hizmeti üzerinde Azure AD asıl ortak anahtarı Hello ilişkilendirin.
-   Merhaba cert hello yerel makine sertifika deposunda saklar.
-   GRANT erişim toohello sertifikanın özel anahtar tooNetwork kullanıcı.
-   Merhaba NPS yeniden başlatın.

Toouse kendi istediğiniz sürece (yerine PowerShell Betiği oluşturur hello hello otomatik olarak imzalanan sertifikalar), sertifikaları toocomplete hello yükleme hello PowerShell betiğini çalıştırın. Birden çok sunucu üzerinde hello uzantısı yüklerseniz, her biri kendi sertifikanın olması gerekir.

1. Windows PowerShell'i yönetici olarak çalıştırın.
2. Dizinleri değiştirin.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Merhaba yükleyici tarafından oluşturulan hello PowerShell betiğini çalıştırın.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. Kiracı kimliğinizi PowerShell sorar Merhaba hello hello Önkoşullar bölümüne Azure portalında kopyalanan dizin kimliği GUID kullanın.
5. TooAzure AD yönetici olarak oturum.
6. Merhaba betik tamamlandığında PowerShell bir başarı iletisi gösterilir.  

Yük Dengeleme için tooset istediğiniz ek herhangi NPS sunucularında bu adımları yineleyin.

>[!NOTE]
>Merhaba PowerShell Betiği sertifikalarla üretmek yerine kendi sertifikaları kullanıyorsanız, toohello NPS adlandırma kuralı Hizala emin olun. Merhaba konu adı olmalıdır **CN =\<Tenantıd\>, OU = Microsoft NPS uzantı**. 

## <a name="configure-your-nps-extension"></a>NPS uzantınızı yapılandırın

Bu bölümde, tasarım konuları ve başarılı NPS uzantısı dağıtımlar için öneriler içerir.

### <a name="configuration-limitations"></a>Yapılandırma sınırlamaları

- Hello Azure MFA için NPS uzantısı araçları toomigrate kullanıcılar ve MFA sunucusu toohello bulut ayarları içermez. Bu nedenle, varolan dağıtım yerine yeni dağıtımlar için hello uzantısıyla öneririz. Üzerinde var olan bir dağıtıma hello uzantısı kullanırsanız, kullanıcılarınızın tooperform kanıtı li sahip toopopulate kendi MFA hello buluta yeniden ayrıntıları.  
- Merhaba gelen UPN hello ikincil yetkili hello uzantısı gerçekleştirmek için Active directory tooidentify hello kullanıcı Azure MFA üzerinde yapılandırılmış toouse alternatif oturum açma kimliği veya özel Active Directory gibi farklı bir tanımlayıcı olabilir şirket içi hello Hello NPS uzantısı kullanır alan UPN dışında. Bkz: [Gelişmiş çok faktörlü kimlik doğrulaması için hello NPS uzantısı için yapılandırma seçenekleri](multi-factor-authentication-advanced-vpn-configurations.md) daha fazla bilgi için.
- Tüm şifreleme protokolleri tüm doğrulama yöntemlerini destekler.
   - **PAP** telefon araması, tek yönlü SMS mesajı, mobil uygulama bildirimi ve mobil uygulama doğrulama kodu destekler
   - **CHAPV2** ve **EAP** telefon araması ve mobil uygulama bildirimi desteği

### <a name="control-radius-clients-that-require-mfa"></a>MFA gerektirecek denetim RADIUS istemcileri

MFA hello NPS uzantısını kullanarak bir RADIUS istemcisi için etkinleştirdikten sonra tüm kimlik doğrulamaları bu istemci için gerekli tooperform MFA ' dir. Bazı RADIUS istemcileri ve diğerleri için tooenable MFA isterseniz, iki NPS sunucularını yapılandırın ve yalnızca bir tanesine hello uzantısını yükleyin. Toorequire MFA toosend istekleri toohello NPS sunucusu hello uzantısıyla yapılandırılmış ve hello uzantısı ile yapılandırılmamış diğer RADIUS istemcileri toohello NPS sunucusu istediğiniz RADIUS istemcileri yapılandırabilirsiniz.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>MFA için kayıtlı olmayan kullanıcılar için hazırlama

MFA için kayıtlı olmayan kullanıcılar varsa, tooauthenticate çalıştıklarında ne olacağını belirleyebilirsiniz. Merhaba kayıt defteri ayarını kullanın *REQUIRE_USER_MATCH* hello kayıt defteri yolunda *HKLM\Software\Microsoft\AzureMFA* toocontrol hello özelliği davranışı. Bu ayar tek yapılandırma seçeneği vardır:

| Anahtar | Değer | Varsayılan |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | TRUE/FALSE | (Eşdeğer tooTRUE) ayarlı değil |

Bu ayarın amacı Hello toodetermine kullanıcı MFA'ya kayıtlı olmayan hangi toodo durumdur. Ne zaman hello anahtarı yok, ayarlanmadı veya tooTRUE, ayarlayın ve hello kullanıcı kayıtlı olmayan, ardından hello uzantısı hello MFA sınama başarısız olur. Merhaba anahtar tooFALSE ayarlanır ve hello kullanıcı kayıtlı olmayan kimlik doğrulaması MFA yapmadan devam eder.

Bu anahtar toocreate seçin ve kullanıcılarınızın ekleme olduğu ve tüm henüz Azure MFA için kaydedilebilir zaman tooFALSE ayarlayın. Ancak, ayarı hello anahtar MFA toosign için kayıtlı olmayan kullanıcılar verdiğinden, devam eden tooproduction önce bu anahtar kaldırmanız gerekir.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>Bu hello istemci sertifikası beklendiği gibi yüklü nasıl doğrularım?

Merhaba otomatik olarak imzalanan sertifika hello sertifika deposu ve özel anahtarı hello onay hello yükleyici tarafından oluşturulan toouser izinler için Ara **ağ hizmeti**. Merhaba cert sahip bir konu adı **CN \<tenantıd\>, OU = Microsoft NPS uzantı**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>My istemci sertifikası ilişkili toomy Kiracı Azure Active Directory'de olup olmadığını nasıl doğrulayabilirsiniz?

PowerShell komut istemi ve aşağıdaki komutları çalıştırma hello açın:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Bu komutlar, Kiracı hello NPS uzantısı örneğinizle PowerShell oturumunuzda ilişkilendirme tüm hello sertifikaları yazdırın. Sertifikanız için istemci sertifikası hello özel anahtarı olmayan bir "X.509(.cer) Base-64 Kodlamalı" dosyası olarak dışa aktararak arayın ve PowerShell hello listeden ile karşılaştırır.

Geçerli-başlangıç ve geçerli-hello komut birden fazla sertifika döndürürse okunabilir formda bulunan, zaman damgaları belirgin misfits çıkışı kullanılan toofilter kadar.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>Neden isteklerim ADAL belirteci hatasıyla başarısız oluyor?

Bu hata kaynaklanabilir çeşitli nedenlerle tooone. Toohelp sorun giderme adımları kullanın:

1. NPS sunucusunu yeniden başlatın.
2. Bu istemci sertifikası beklendiği gibi yüklü olduğunu doğrulayın.
3. Bu hello sertifika üzerinde Azure AD Kiracı ile ilişkili olduğunu doğrulayın.
4. Bu https://login.microsoftonline.com/ hello uzantısı'nı çalıştıran hello sunucusundan erişilebilir olduğundan emin olun.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>Neden kimlik doğrulaması, HTTP günlükleri hello kullanıcı bulunamadı bildiren bir hata ile başarısız?

AD Connect çalıştıran ve hello kullanıcının Windows Active Directory ve Azure Active Directory içinde mevcut olduğunu doğrulayın.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>HTTP hataları günlüklerinde başarısız olan tüm my kimlik doğrulamaları ile bağlanmak neden görüyor musunuz?

Bu https://adnotifications.windowsazure.com hello NPS uzantısı'nı çalıştıran hello sunucudan erişilebilir olduğundan emin olun.


## <a name="next-steps"></a>Sonraki adımlar

- İki aşamalı doğrulamayı gerçekleştirmek döndürmemelidir IP'ler için bir özel durum listesi ayarlamak veya alternatif kimlikleri oturum açma için yapılandırma [Gelişmiş çok faktörlü kimlik doğrulaması için hello NPS uzantısı için yapılandırma seçenekleri](nps-extension-advanced-configuration.md)

- [Azure çok faktörlü kimlik doğrulamasını hello NPS uzantısı hata iletilerini çözümleyin](multi-factor-authentication-nps-errors.md)
