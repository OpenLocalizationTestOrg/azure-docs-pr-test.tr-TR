---
title: "Azure AD Connect: Hızlı ayarlar ile çalışmaya başlama | Microsoft Belgeleri"
description: "Nasıl toodownload, yükleyin ve Azure AD Connect'i hello Kurulum Sihirbazı'nı çalıştırın öğrenin."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Hızlı ayarları kullanarak Azure AD Connect ile çalışmaya başlama
Kimlik doğrulaması için [parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) özelliğine ve tek ormanlı bir topolojiye sahipseniz Azure AD Connect **Hızlı Ayarları** kullanılır. **Hızlı Ayarlar** hello varsayılan seçenektir ve en yaygın olarak dağıtılan hello senaryo için kullanılır. Yalnızca birkaç tıklama koyma tooextend, şirket içi dizin toohello bulut şunlardır.

Azure AD Connect'i yüklemeye başlamadan önce emin olun çok[Azure AD Connect indirin](http://go.microsoft.com/fwlink/?LinkId=615771) ve tam hello önkoşul adımlarını [Azure AD Connect: donanım ve Önkoşullar](active-directory-aadconnect-prerequisites.md).

Hızlı ayarlar, topolojinizle eşleşmiyorsa diğer senaryolar için [ilgili belgelere](#related-documentation) göz atın.

## <a name="express-installation-of-azure-ad-connect"></a>Azure AD Connect'i hızlı yükleme
Bu adımların nasıl gerçekleştirildiğini hello görebilirsiniz [videolar](#videos) bölümü.

1. Üzerinde Azure AD Connect tooinstall istediğiniz yerel yönetici toohello sunucusu olarak oturum açın. Merhaba sunucuda yapmalısınız toobe hello eşitleme sunucusu istiyor.
2. Tooand çift gidin **AzureADConnect.msi**.
3. Merhaba Hoş Geldiniz ekranında hello kutusunu kabul ettiğinizi belirten toohello Lisans Koşulları'nı seçin ve **devam**.  
4. Merhaba hızlı ayarlar ekranında tıklatın **hızlı ayarları kullan**.  
   ![Hoş Geldiniz tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Merhaba Bağlan tooAzure AD ekranda hello kullanıcı adı ve parola genel yöneticinin Azure AD için girin. **İleri**’ye tıklayın.  
   ![TooAzure AD connect](./media/active-directory-aadconnect-get-started-express/connectaad.png) bir hatayla karşılaştıysanız ve bağlantı sorunlarınız varsa, daha sonra bkz [bağlantı sorunlarını giderme](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Hello Bağlan tooAD DS ekranında kuruluş yöneticisi hesabı için hello kullanıcı adı ve parola girin. Merhaba etki alanı bölümünü NetBIOS veya FQDN biçiminde, diğer bir deyişle, ör. fabrıkam\yönetici veya fabrikam.com\administrator girebilirsiniz. **İleri**’ye tıklayın.  
   ![TooAD DS Bağlan](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Merhaba [ **Azure AD oturum açma yapılandırması** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) sayfası yalnızca gösterir, tamamlanmadı, [etki alanlarınızı doğrulama](../active-directory-add-domain.md) hello içinde [Önkoşullar](active-directory-aadconnect-prerequisites.md).
   ![Doğrulanmamış etki alanları](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Bu sayfayı görüyorsanız **Eklenmedi** ve **Doğrulanmadı** olarak işaretlenen tüm etki alanlarını gözden geçirin. Kullandığınız etki alanlarının Azure AD'de doğrulanmış olduğundan emin olun. Etki alanlarınızı doğruladıktan hello Yenile simgesine tıklayın.
8. Merhaba hazır tooconfigure ekranında tıklatın **yükleme**.
   * İsteğe bağlı olarak hello hazır tooconfigure sayfasında hello işaretini kaldırabilirsiniz **Yapılandırma tamamlandıktan hemen sonra hello eşitleme işlemini başlatmak** onay kutusu. Toodo ek yapılandırma gibi istiyorsanız bu onay kutusunun işaretini kaldırmanız gerekir [filtreleme](active-directory-aadconnectsync-configure-filtering.md). Bu seçeneğin işaretini kaldırırsanız hello sihirbaz eşitlemeyi yapılandırır ancak hello Zamanlayıcı devre dışı bırakır. El ile etkinleştirmediğiniz sürece çalışmaz [hello yükleme sihirbazını yeniden](active-directory-aadconnectsync-installation-wizard.md).
   * Exchange şirket içi Active Directory içinde olması durumunda bir seçenek tooenable de [ **Exchange karma dağıtımı**](https://technet.microsoft.com/library/jj200581.aspx). Toohave Exchange posta kutuları her iki hello bulutta planlar ve hello aynı şirket, bu seçeneği etkinleştirin zaman.
     ![Azure AD Connect tooconfigure hazır](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Merhaba yüklemesi tamamlandığında, tıklatın **çıkış**.
10. Merhaba yükleme tamamlandıktan sonra oturumunu kapatmak ve Eşitleme Hizmeti Yöneticisi'ni veya Synchronization Rule Editor'ı kullanmadan önce yeniden oturum açın.

## <a name="videos"></a>Videolar
Merhaba hızlı yükleme kullanarak, bir video izlemek için bkz:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Azure AD Connect'i sahip olduğunuza göre şunları yapabilirsiniz [hello yüklemeyi doğrulayın ve lisansları atama](active-directory-aadconnect-whats-next.md).

Merhaba yüklemeyle etkinleştirilen özellikler hakkında daha fazla bilgi edinin: [otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md), [yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), ve [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Bu genel konular hakkında daha fazla bilgi edinin: [Zamanlayıcı ve nasıl tootrigger eşitleme](active-directory-aadconnectsync-feature-scheduler.md).

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

## <a name="related-documentation"></a>İlgili belgeler
| Konu başlığı |
| --- | --- |
| Azure AD Connect'e genel bakış |
| Özelleştirilmiş ayarları kullanarak yükleme |
| DirSync'ten yükseltme |
| Yükleme için kullanılan hesaplar |

