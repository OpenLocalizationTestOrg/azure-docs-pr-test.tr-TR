---
title: "Azure karma kimlik çözümünü aaaChoose | Microsoft Docs"
description: "Merhaba kullanılabilir karma kimlik çözümleri ve öneriler, toomake hello en iyi Kimlik Yönetimi kararı, kuruluşunuz için temel bir anlayış alın."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Microsoft karma kimlik çözümleri
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) karma kimlik çözümleri toosynchronize şirket içi dizin nesneleri hala kullanıcıların şirket içi yönetme sırasında Azure AD ile etkinleştirin. ilk karar toomake toouse kimlik eşitlenen veya kimlik Federasyon isteyip istemediğiniz şirket içi Windows Server Active Directory'nizi Azure AD ile olan toosynchronize planlarken hello. Eşitlenen kimlikler ve isteğe bağlı olarak parola karmaları etkinleştirmek, kullanıcılarınızın toouse hello aynı parola tooaccess şirket içi ve bulut tabanlı kuruluş kaynakları. Çoklu oturum açma (SSO) veya şirket içi MFA gibi daha gelişmiş senaryo gereksinimleri için toodeploy Active Directory Federasyon Hizmetleri (AD FS) toofederate kimlikleri gerekir. 

Karma kimlik yapılandırmak için kullanılabilen birkaç seçeneğiniz vardır. Bu makalede dağıtım kolaylığı üzerinde göre kuruluşunuz için en iyi bir hello ve belirli kimlik ve erişim yönetimi gereksinimlerini seçtiğiniz bilgi toohelp sağlar. En iyi hangi kimlik modelinde, kuruluşunuzun gereksinimlerine uygun göz önünde bulundurun gibi toothink zaman, mevcut altyapınızı, karmaşıklığı ve maliyeti hakkında da gerekir. Bu faktörlerin her kuruluş için farklıdır ve zaman içinde değişebilir. Ancak, gereksinimlerinizi değiştirirseniz, bu da hello esneklik tooswitch tooa farklı kimlik modeline sahip.

> [!TIP]
> Bu çözümler tüm tarafından sunulur [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="synchronized-identity"></a>Eşitlenen kimliği 
Eşitlenen hello en basit yolu toosynchronize içi dizin nesneleri (kullanıcılar ve gruplar) Azure AD ile kimliğidir. 

![Eşitlenen karma kimlik](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Eşitlenen kimlik hello kolay ve hızlı yöntem olsa da, kullanıcılarınızın bulut tabanlı kaynaklar için hala toomaintain ayrı bir parola gerekir. tooavoid Bu, ayrıca (isteğe bağlı) [kullanıcı parola karmasını eşitleme](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) tooyour Azure AD dizini. Parola karmaları etkinleştirir kullanıcılar toolog toocloud tabanlı kuruluş kaynakları ile eşitleme hello aynı kullanıcı adı ve parola şirket içi kullanın. Azure AD Connect, şirket içi dizininize değişiklikler ve Azure AD dizininizi eşitlenmiş tutar düzenli olarak denetler. Bir kullanıcı özniteliği ya da parola değiştirilen şirket içi Active Directory olduğunda, Azure AD içinde otomatik olarak güncelleştirilir. 

Yalnızca kendi kullanıcı toosign tooOffice 365, SaaS uygulamaları ve diğer Azure AD tabanlı kaynakları tooenable isteyen çoğu kuruluş için hello varsayılan parola eşitleme seçeneği önerilir. Sizin için işe yaramazsa, geçişli kimlik doğrulaması ve AD FS arasında toodecide gerekir.

> [!TIP]
> Kullanıcı parolalarını şirket içi Windows Server Active Directory hello gerçek kullanıcı parolası temsil eden bir karma değer hello biçiminde depolanır. Bir karma değer, tek yönlü matematiksel işlevi (Merhaba karma algoritması) sonucudur. Tek yönlü işlevin toohello düz metin sürümünün bir parola yöntemi toorevert hello sonuç yok. Parola karma toosign tooyour şirket ağında kullanamazsınız. Toosynchronize parolalar opt, Azure AD Connect ayıklar parola karmaları hello gelen şirket içi Active Directory ve eşitlenmiş tooAzure AD silinmeden önce toohello parola karması işleme ek güvenlik uygular. Parola Eşitleme, ayrıca parola geri yazma tooenable Self Servis parola sıfırlama Azure AD ile birlikte kullanılabilir. Ayrıca, bağlı toohello kurumsal ağ etki alanına katılmış bilgisayarlarda kullanıcılar için çoklu oturum açma (SSO) etkinleştirebilirsiniz. Çoklu oturum açma ile etkin kullanıcılar yalnızca bir kullanıcı adı toosecurely erişim bulut kaynakları tooenter gerekir. 

## <a name="pass-through-authentication"></a>Doğrudan kimlik doğrulama
[Azure AD doğrudan kimlik doğrulama](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) kullanarak şirket içi Active Directory'nizi Azure AD tabanlı hizmetler için bir basit parola doğrulama çözümü sağlar. Kuruluşunuz için güvenlik ve uyumluluk ilkeleri kullanıcıların parolalarını bile karma bir formda gönderme izin vermez ve etki alanına katılmış cihazlar için yalnızca toosupport Masaüstü SSO ihtiyacınız varsa, geçişli kimlik doğrulaması kullanmayı değerlendir önerilir. Doğrudan kimlik doğrulama hello AD FS ile karşılaştırıldığında hello dağıtım altyapısı basitleştirir DMZ herhangi bir dağıtımında gerektirmez. Azure AD kullanarak kullanıcılar oturum açtığında, bu kimlik doğrulama yöntemi kullanıcıların parolalarını şirket içi Active Directory'nizi karşı doğrudan doğrular.

![Doğrudan kimlik doğrulama](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Doğrudan kimlik doğrulama ile bir karmaşık ağ altyapısı için gerek yoktur ve toostore şirket içi parolaları hello bulutta olması gerekmez. Çoklu oturum açma ile birlikte doğrudan kimlik doğrulama tooAzure AD veya diğer bulut hizmetlerine imzalarken gerçekten tümleşik bir deneyim sağlar.

Doğrudan kimlik doğrulaması için parola doğrulama isteklerini dinleyen bir basit şirket içi Aracısı kullanan Azure AD Connect ile yapılandırılır. Merhaba Aracısı kolayca dağıtılan toomultiple makineler tooprovide yüksek kullanılabilirlik ve Yük Dengeleme değiştirebilirsiniz. Tüm iletişimler yalnızca giden olduğundan, bir çevre ağınızda yüklü hello bağlayıcı toobe gerekli değildir. Merhaba bağlayıcı Hello sunucu bilgisayar gereksinimleri aşağıdaki gibidir:

- Windows Server 2012 R2 veya üzeri
- Üzerinden kullanıcıların doğrulandığı hello ormandaki tooa etki alanına katılmış

> [!NOTE]
> Azure AD doğrudan kimlik doğrulama şu anda önizlemede ve web tarayıcısı tabanlı ve modern kimlik doğrulamasını destekleyen Office istemciler için desteklenir. Desteklenmeyen istemcileri için eski Office istemcileri ve Exchange ActiveSync, (mobil cihazlardaki yerel e-posta istemcileri de dahil olmak üzere) gibi önerilen toouse hello modern kimlik doğrulaması eşdeğer kullanılır. Modern kimlik doğrulaması yalnızca doğrudan kimlik doğrulama sağlar, ancak koşullu erişim ilkeleri toobe, çok faktörlü kimlik doğrulaması gibi uygulanan da sağlar. 

Windows 10 cihazları kullanarak tooAzure AD alanına katıldığında doğrudan kimlik doğrulama şu anda desteklenmiyor. Ancak, otomatik bir geri dönüş toosupport Windows 10 parola karması eşitlemesi kullanabilirsiniz ve hello eski istemciler daha önce bahsedilen. Azure AD Connect oturum açma hello seçenek olarak geçişli kimlik doğrulaması seçildiğinde hello Önizleme sırasında parola karması eşitlemesi varsayılan olarak etkindir.


## <a name="federated-identity-ad-fs"></a>Federe kimlik (AD FS)
Kullanıcıların Office 365 ve diğer bulut hizmetlerine erişme üzerinde daha fazla denetim için çoklu oturum açma (SSO) kullanarak dizin eşitlemeyi ayarlayabilirsiniz [Active Directory Federasyon Hizmetleri (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). Kullanıcı oturum açma işlemleri ile AD FS temsilciler kimlik doğrulama tooan federasyonunu kullanıcı kimlik bilgilerini doğrular sunucu şirket içi. Bu modelde, şirket içi Active Directory kimlik bilgileri hiçbir zaman tooAzure AD geçirilir.

![Federe kimlik](./media/choose-hybrid-identity-solution/federated-identity.png)

Kimlik Federasyonu olarak da bilinen bu oturum açma yöntemi tüm kullanıcı kimlik doğrulaması denetimli şirket içi ve yöneticilerine verir sağlar tooimplement daha ayrıntılı erişim denetimi düzeylerini. AD FS ile Kimlik Federasyonu en karmaşık hello seçenektir ve şirket içi ortamınızdaki ek sunuculara dağıtılması gerekir. Kimlik Federasyonu Ayrıca Active Directory ve AD FS altyapınızı tooproviding 7 x 24 desteği kaydeder. Şirket içi Internet erişimi engelliyorsa, etki alanı denetleyicisi veya AD FS sunucuları toocloud Hizmetleri'nde kullanıcılar oturum açamaz, kullanılamadığından bu yüksek düzeyde desteği gereklidir.

> [!TIP]
> Active Directory Federasyon Hizmetleri (AD FS) ile Federasyon toouse karar verirseniz, AD FS altyapınızı başarısız olursa, isteğe bağlı olarak parola eşitleme yedek olarak ayarlayabilirsiniz.


## <a name="common-scenarios-and-recommendations"></a>Yaygın senaryolar ve öneriler
İşte bazı ortak bir karma kimlik ve erişim yönetimi senaryoları toowhich karma kimlik seçeneği (veya Seçenekler) olarak öneriler her biri için uygun olabilir.

|İçin gerekir:|PWS ve SSO<sup>1</sup>| PTA ve SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Yeni kullanıcı, kişi ve grup hesapları my şirket içi Active Directory toohello bulutta otomatik olarak oluşturulan eşitleyin.|![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png) |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|My Kiracı Office 365 karma senaryolar için ayarlama|![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png) |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|My kullanıcılar toosign etkinleştirin ve şirket içi parolalarını kullanarak bulut hizmetlerine erişim|![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png) |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Tekli Kurumsal kimlik bilgilerini kullanarak oturum uygulama|![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png) |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Parola karmaları hello bulutta depolanan emin olun| |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Şirket içi çok faktörlü kimlik doğrulaması çözümlerle| | |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Kullanıcılarım için destek akıllı kart kimlik doğrulaması<sup>4</sup>| | |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Merhaba Office portalı ve hello Windows 10 Masaüstü parola süre sonu bildirimleri görüntüleme| | |![Önerilen](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Parola Eşitleme ile çoklu oturum açma. 

> <sup>2</sup> doğrudan kimlik doğrulaması ve çoklu oturum açma. 

> <sup>3</sup> çoklu oturum açma AD FS ile Federasyon.

> <sup>4</sup> AD FS, Kuruluş PKI tooallow ile tümleştirilebilir sertifikaları kullanarak oturum açın. Bu sertifikalar, MDM veya GPO ya da akıllı kart sertifikaları (PIV/Önbellek kartları dahil) veya iş (güven sertifikası) için Hello gibi güvenilir sağlama kanallar aracılığıyla dağıtılan yazılımla sertifikalarının olabilir. Akıllı kart kimlik doğrulaması desteği hakkında daha fazla bilgi için bkz: [bu blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure kavram kanıtı ortamda daha fazla bilgi edinin](https://aka.ms/aad-poc)

[Azure AD Connect'i yükleme](http://go.microsoft.com/fwlink/?LinkId=615771)

[Karma kimlik eşitleme izleme](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

