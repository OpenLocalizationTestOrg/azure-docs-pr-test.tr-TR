---
title: "Azure AD Connect eşitleme: hello Azure AD Connect eşitleme hizmeti hesabını değiştirme | Microsoft Docs"
description: "Bu konuda belge hello şifreleme anahtarını ve nasıl tooabandon hello parola sonra açıklar değiştirildi."
services: active-directory
keywords: "Azure AD eşitleme hizmeti hesabını, parola"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Hello Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirme
Hello Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirirseniz, hello şifreleme anahtarı terk ve hello Azure AD Connect eşitleme hizmeti hesabının parolasını yeniden kadar hello eşitleme hizmeti mümkün başlangıç doğru olmaz. 

Azure AD Connect Eşitleme Hizmetleri hello bir parçası olarak bir şifreleme anahtarı toostore hello parolaları hello AD DS ve Azure AD hizmet hesaplarını kullanır.  Bu hesapları hello veritabanında depolanan önce şifrelenir. 

Merhaba kullanılan şifreleme anahtarı güvenliğinin ile [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI korur hello kullanarak hello şifreleme anahtarı **hello Azure AD Connect eşitleme hizmeti hesabı parolasını**. 

Toochange hello hizmet hesabı parolası gerekirse hello yordamlarda kullanabilirsiniz [Abandoning hello Azure AD Connect eşitleme şifreleme anahtarı](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish bu.  Bu yordamları da tooabandon hello şifreleme anahtarı herhangi bir nedenle ihtiyacınız varsa kullanılmalıdır.

##<a name="issues-that-arise-from-changing-hello-password"></a>Merhaba parolasını değiştirme ortaya çıkan sorunları
Merhaba hizmet hesabı parolasını değiştirdiğinizde bitti toobe gereken iki şey vardır.

İlk olarak, Windows Hizmet Denetimi Yöneticisi hello altında toochange hello parola gerekir.  Bu sorun çözülene kadar aşağıdaki hatalar görürsünüz:


- Merhaba hatasını alıyorsunuz toostart hello eşitleme hizmeti Windows Hizmet Denetimi Yöneticisi'nde çalışırsanız, "**Windows hello Microsoft Azure AD eşitleme hizmeti yerel bilgisayarda başlatılamadı**". **Hata 1069: tooa oturum açma hatası hello hizmeti başlatılmadı.** "
- Windows Olay Görüntüleyicisi'ni altında bir hata ile Merhaba sistem olay günlüğünü içeren **olay kimliği 7038** ve ileti "**hello ADSync hizmeti tarihi oluşturulamıyor toolog parolayla şu anda yapılandırılmış hello gibi toohello aşağıdaki son hata: Merhaba kullanıcı adı veya parola doğru değil.** "

Merhaba parola güncelleştirilirse, ikinci olarak, belirli koşullar altında hello eşitleme hizmeti artık hello şifreleme anahtarı DPAPI aracılığıyla alabilir. Merhaba şifreleme anahtar olmadan, eşitleme hizmeti hello parolaları gerekli toosynchronize denetleyicisinden şifresi çözülemiyor hello AD ve Azure AD şirket içi.
Hataları gibi görürsünüz:

- Windows Hizmet Denetimi Yöneticisi altında toostart hello eşitleme hizmeti çalışırsanız ve hello şifreleme anahtarını alamıyor hatasıyla başarısız "** Windows hello Microsoft Azure AD eşitleme yerel bilgisayarda başlatılamadı. Daha fazla bilgi için hello sistem olay günlüğünü gözden geçirin. Bu Microsoft dışı service ise, hello hizmet satıcısını ve tooservice özel hata kodunu **-21451857952 ***. "
- Windows Olay Görüntüleyicisi'ni altında hello uygulama olay günlüğüne bir hata ile içeren **olay kimliği 6028** ve hata iletisi *"**hello sunucusu şifreleme anahtarı erişilemez.* *"*

Bu hatalar almazsınız tooensure hello yordamları izleyin [Abandoning hello Azure AD Connect eşitleme şifreleme anahtarı](#abandoning-the-azure-ad-connect-sync-encryption-key) hello parola değiştirme.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Hello Azure AD Connect eşitleme şifreleme anahtarını bırakıp
>[!IMPORTANT]
>Merhaba aşağıdaki yordamlar yalnızca tooAzure AD Connect yapı 1.1.443.0 uygulanır veya daha eski.

Aşağıdaki yordamlar tooabandon hello şifreleme anahtarı hello kullanın.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Tooabandon hello şifreleme anahtarı gerekiyorsa hangi toodo

Tooabandon hello şifreleme anahtarı gerekiyorsa, aşağıdaki yordamları tooaccomplish hello bunu kullanın.

1. [Merhaba varolan şifreleme anahtarını iptal](#abandon-the-existing-encryption-key)

2. [Merhaba AD DS hesabı Hello parolasını sağlayın](#provide-the-password-of-the-ad-ds-account)

3. [Merhaba hello Azure AD eşitleme hesabının parolasını yeniden Başlat](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Merhaba eşitleme hizmetini Başlat](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Merhaba varolan şifreleme anahtarını iptal
Bu yeni bir şifreleme anahtarı oluşturulabilmesi hello var olan şifreleme anahtarı bırakın:

1. Tooyour içinde Azure AD Connect Server yönetici olarak oturum.

2. Yeni bir PowerShell oturumu başlatın.

3. Toofolder gidin:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Merhaba komutu çalıştırın:`./miiskmu.exe /a`

![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Merhaba AD DS hesabı Hello parolasını sağlayın
Merhaba var olan parolaların Hello veritabanı içinde depolanan artık şifresi çözülebilir gibi hello AD DS hesabının hello parolayla tooprovide hello eşitleme hizmeti gerekiyor. Merhaba eşitleme hizmeti hello parolaları hello yeni bir şifreleme anahtarı kullanarak şifreler:

1. Merhaba Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.
</br>![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Toohello Git **Bağlayıcılar** sekmesi.
3. Select hello **AD Bağlayıcısı** tooyour karşılık gelen şirket içi AD. Birden fazla AD bağlayıcısı varsa, bunların her biri için aşağıdaki adımları hello yineleyin.
4. Altında **Eylemler**seçin **özellikleri**.
5. Merhaba açılan iletişim kutusunda seçin **tooActive Directory ormanına Bağlan**:
6. Hello hello AD DS hesap Hello parolasını girin **parola** metin kutusu. Parolasını bilmiyorsanız, bu adımı uygulamadan önce değer bilinen tooa ayarlamanız gerekir.
7. Tıklatın **Tamam** toosave hello yeni parola ve Kapat hello açılan iletişim.
![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Merhaba hello Azure AD eşitleme hesabının parolasını yeniden Başlat
Doğrudan hello parolasını hello Azure AD hizmet hesabı toohello eşitleme hizmeti sağlayamıyor. Bunun yerine, toouse hello cmdlet gerekir **Ekle ADSyncAADServiceAccount** tooreinitialize hello Azure AD hizmet hesabı. Merhaba cmdlet hello hesabı parolasını sıfırlar ve kullanılabilir toohello eşitleme hizmeti yapar:

1. Hello Azure AD Connect sunucuda yeni bir PowerShell oturumu başlatın.
2. Cmdlet'i çalıştırmak `Add-ADSyncAADServiceAccount`.
3. Merhaba açılan iletişim kutusunda, Azure AD kiracınız için hello Azure AD genel yönetici kimlik bilgilerini sağlayın.
![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Başarılı olursa, hello PowerShell komut istemi görürsünüz.

#### <a name="start-hello-synchronization-service"></a>Merhaba eşitleme hizmetini Başlat
Merhaba eşitleme hizmeti erişim toohello şifreleme anahtarına sahiptir ve tüm parolaları hello göre gereksinim duyduğu, hello Windows Hizmet Denetimi Yöneticisi hello hizmetini yeniden başlatabilirsiniz:


1. TooWindows Hizmet Denetim Yöneticisi (Başlangıç → Hizmetleri) gidin.
2. Seçin **Microsoft Azure AD eşitleme** ve yeniden Başlat'ı tıklatın.

## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)

* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
