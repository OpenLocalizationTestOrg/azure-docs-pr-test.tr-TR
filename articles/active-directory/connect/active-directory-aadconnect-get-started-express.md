---
title: "Azure AD Connect: Hızlı ayarlar ile çalışmaya başlama | Microsoft Belgeleri"
description: "Azure AD Connect'i indirme, yükleme ve kurulum sihirbazını çalıştırma hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/03/2018
ms.author: billmath
ms.openlocfilehash: 15101e1edb483f49c7570a5d4eab66865bbceb87
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/18/2018
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Hızlı ayarları kullanarak Azure AD Connect ile çalışmaya başlama
Kimlik doğrulaması için [parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) özelliğine ve tek ormanlı bir topolojiye sahipseniz Azure AD Connect **Hızlı Ayarları** kullanılır. **Hızlı Ayarlar** varsayılan seçenek olup yaygın olarak dağıtılan senaryo için kullanılır. Şirket içi dizininizi buluta genişletmek için yalnızca birkaç tıklama yapmanız yeterli.

Azure AD Connect'i yüklemeye başlamadan önce [Azure AD Connect'i indirdiğinizden](http://go.microsoft.com/fwlink/?LinkId=615771) ve [Azure AD Connect: Donanım ve önkoşullar](active-directory-aadconnect-prerequisites.md) bölümündeki önkoşul adımlarını tamamladığınızdan emin olun.

Hızlı ayarlar, topolojinizle eşleşmiyorsa diğer senaryolar için [ilgili belgelere](#related-documentation) göz atın.

## <a name="express-installation-of-azure-ad-connect"></a>Azure AD Connect'i hızlı yükleme
Bu adımların nasıl gerçekleştirildiğini [videolar](#videos) bölümünden görebilirsiniz.

1. Azure AD Connect'i yüklemek istediğiniz sunucuda yerel yönetici olarak oturum açın. Bu işlemi eşitleme sunucusu olmasını istediğiniz sunucuda yapmanız gerekir.
2. **AzureADConnect.msi** öğesine gidin ve çift tıklayın.
3. Hoş Geldiniz ekranında, lisans koşullarını kabul ettiğinizi belirten kutuyu seçin ve **Devam**'a tıklayın.  
4. Hızlı ayarlar ekranında **Hızlı ayarları kullan**'a tıklayın.  
   ![Azure AD Connect'e Hoş Geldiniz](./media/active-directory-aadconnect-get-started-express/express.png)
5. Azure AD'ye Bağlanma ekranında Azure AD'niz için genel yönetici kullanıcı adını ve parolasını girin. **İleri**’ye tıklayın.  
   ![Azure AD'ye Bağlanma](./media/active-directory-aadconnect-get-started-express/connectaad.png)  
   Bir hatayla karşılaştıysanız ve bağlantı sorunlarınız varsa bkz. [Bağlantı sorunlarını giderme](active-directory-aadconnect-troubleshoot-connectivity.md).
6. AD DS'ye Bağlanma ekranında kuruluş yöneticisi hesabına ilişkin kullanıcı adını ve parolayı girin. Etki alanı bölümünü NetBIOS veya FQDN biçiminde (örneğin, FABRIKAM\yönetici veya fabrikam.com\yönetici) girebilirsiniz. **İleri**’ye tıklayın.  
   ![AD DS'ye Bağlanma](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. [**Azure AD oturum açma yapılandırması**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) sayfası, yalnızca [önkoşullar](active-directory-aadconnect-prerequisites.md) bölümündeki [etki alanlarınızı doğrulama](../active-directory-domains-add-azure-portal.md) adımını tamamlamamış olmanız halinde görüntülenir.
   ![Doğrulanmamış etki alanları](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Bu sayfayı görüyorsanız **Eklenmedi** ve **Doğrulanmadı** olarak işaretlenen tüm etki alanlarını gözden geçirin. Kullandığınız etki alanlarının Azure AD'de doğrulanmış olduğundan emin olun. Etki alanlarınızı doğruladıktan sonra Yenile simgesine tıklayın.
8. Yapılandırma için hazır ekranında **Yükle**'ye tıklayın.
   * İsteğe bağlı olarak, Yapılandırma için hazır sayfasında **Start the synchronization process as soon as configuration completes (Yapılandırma tamamlanınca eşitlemeyi başlat)** onay kutusunun işaretini kaldırabilirsiniz. Başka yapılandırmalar (örneğin, [filtreleme](active-directory-aadconnectsync-configure-filtering.md)) gerçekleştirmek istiyorsanız bu onay kutusunun işaretini kaldırmanız gerekir. Bu seçeneğin işaretini kaldırırsanız sihirbaz eşitlemeyi yapılandırır ancak zamanlayıcıyı devre dışı bırakır. [Yükleme sihirbazını yeniden çalıştırarak](active-directory-aadconnectsync-installation-wizard.md) elle etkinleştirmediğiniz sürece çalışmaz.
   * Şirket içi Active Directory'nizde Exchange varsa [**Exchange Karma dağıtımını**](https://technet.microsoft.com/library/jj200581.aspx) da etkinleştirebilirsiniz. Aynı anda hem bulutta ve hem de şirket içinde Exchange posta kutunuzun olmasını istiyorsanız bu seçeneği etkinleştirin.
     ![Azure AD Connect yapılandırma için hazır](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Yükleme tamamlandığında **Çıkış**'a tıklayın.
10. Yükleme tamamlandıktan sonra Synchronization Service Manager'ı veya Synchronization Rule Editor'ı kullanmadan önce oturumunuzu kapatıp tekrar açın.

## <a name="videos"></a>Videolar
Hızlı yüklemeyi kullanmaya ilişkin video için bkz.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
>
>

## <a name="next-steps"></a>Sonraki adımlar
Azure AD Connect'i yüklediniz, artık [yüklemeyi doğrulayabilir ve lisans atayabilirsiniz](active-directory-aadconnect-whats-next.md).

Yüklemeyle etkinleştirilen özellikler hakkında daha fazla bilgi edinin: [Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md), [Yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) ve [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Şu genel konu başlıkları hakkında daha fazla bilgi edinin: [Zamanlayıcı ve eşitleme tetikleme](active-directory-aadconnectsync-feature-scheduler.md).

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

## <a name="related-documentation"></a>İlgili belgeler

| Konu | Bağlantı |
| --- | --- |
| Azure AD Connect'e genel bakış | [Şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
| Özelleştirilmiş ayarları kullanarak yükleme | [Azure AD Connect özel yüklemesi](active-directory-aadconnect-get-started-custom.md) |
| DirSync'ten yükseltme | [Azure AD eşitleme aracından (DirSync) yükseltme](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
| Yükleme için kullanılan hesaplar | [Azure AD Connect kimlik bilgileri ve izinleri hakkında daha fazla bilgi](active-directory-aadconnect-accounts-permissions.md) |
