---
title: "Azure Active Directory Domain Services: Parola eşitlemeyi etkinleştirme | Microsoft Docs"
description: "Azure Active Directory Etki Alanı Hizmetleri ile çalışmaya başlama"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Parola Eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme
Önceki görevlerde Azure Active Directory (Azure AD) kiracınız için Azure Active Directory Domain Services hizmetini etkinleştirdiniz. Merhaba sonraki kimlik bilgisi karmalarını tooenable eşitlenmesi için NT LAN Yöneticisi (NTLM) ve Kerberos kimlik doğrulaması tooAzure AD etki alanı Hizmetleri gerekli bir görevdir. Kimlik bilgisi eşitlemesini ayarladıktan sonra kullanıcılar toohello yönetilen etki alanında Kurumsal kimlik ile oturum açabilir.

Merhaba adımlar, Azure AD Connect kullanarak şirket içi dizininizden eşitlenen yalnızca bulut kullanıcı hesapları vs kullanıcı hesapları için farklıdır.  Azure AD kiracınıza bileşimini varsa ve yalnızca kullanıcılar, şirket içi bulut AD, her iki adımın tooperform gerekir.

<br>

> [!div class="op_single_selector"]
> * **Yalnızca bulut kullanıcı hesapları**: [yalnızca bulut kullanıcı tooyour yönetilen etki alanı hesapları için parola eşitleme](active-directory-ds-getting-started-password-sync.md)
> * **Şirket içi kullanıcı hesaplarını**: [, şirket içi eşitlenen kullanıcı hesapları için parola eşitleme AD tooyour yönetilen etki alanı](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Görev 5: sadece bulutta kullanıcı hesapları için parola eşitleme tooyour etki alanı yönetilen etkinleştir
Merhaba tooauthenticate kullanıcılar yönetilen etki alanı, Azure Active Directory etki alanı Hizmetleri NTLM ve Kerberos kimlik doğrulaması için uygun bir biçimde karmaları kimlik bilgisi. Azure AD bırakmaz oluşturmak veya Azure Active Directory etki alanı Hizmetleri, kiracınızın etkinleştirinceye kadar NTLM veya Kerberos kimlik doğrulaması için gerekli hello biçimi kimlik bilgisi karmalarını depolayın. Güvenliğe dayalı bariz nedenlerle, Azure AD düz metin biçiminde de hiçbir parola kimlik bilgisi depolamaz. Bu nedenle, Azure AD kullanıcıların varolan kimlik bilgilerine göre bu NTLM veya Kerberos kimlik bilgisi karmalarını oluşturur bir şekilde tooautomatically yok.

> [!NOTE]
> Kuruluşunuz yalnızca bulutta kullanıcı hesapları varsa, toouse Azure Active Directory etki alanı Hizmetleri gereksinim duyan kullanıcılar parolalarını değiştirmeniz gerekir. Azure AD dizininizi hello Azure portalında veya Azure AD PowerShell cmdlet'leri kullanılarak oluşturulmuş bir hesap bir yalnızca bulut kullanıcı hesabıdır. Bu tür kullanıcı hesapları şirket içi dizinden eşitlenmez.
>
>

Bu parola değişikliği işlemi, Azure Active Directory etki alanı Hizmetleri Azure AD'de oluşturulan Kerberos ve NTLM kimlik doğrulaması toobe için gerekli olan karmaları hello kimlik bilgisi neden olur. Hello tüm kullanıcılar Kiracı toouse Azure Active Directory etki alanı Hizmetleri gereksinim duyan veya bunları toochange söylemek için hello parolaları ya da dolabilir parolalarını.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Yalnızca bulutta yer alan kullanıcı hesabı için NTLM ve Kerberos kimlik bilgileri karması oluşturmayı etkinleştirme
Parolalarını değiştirebilmeniz için tooprovide kullanıcılar, gereken hello talimatlar şunlardır:

1. Toohello Git [Azure AD erişim paneli](http://myapps.microsoft.com) kuruluşunuz için sayfa.

    ![Hello Azure AD erişim Paneli başlatma](./media/active-directory-domain-services-getting-started/access-panel.png)

2. Merhaba sağ üst köşesindeki, adınızın tıklatın ve seçin **profil** hello menüsünde.

    ![Profil seçme](./media/active-directory-domain-services-getting-started/select-profile.png)

3. Merhaba üzerinde **profil** sayfasında, tıklatın **parola değiştirme**.

    ![“Parola değiştir”e tıklayın](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Merhaba, **parola değiştirme** seçeneği hello erişim paneli penceresinde görüntülenmez, kuruluşunuzun yapılandırılmış olduğundan emin olun [Azure AD'de parola yönetimi](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. Merhaba üzerinde **parolasını değiştirme** sayfasında, var olan (eski) parolanızı yazın, yeni bir parola yazın ve ardından onaylayın.

    ![Azure AD Etki Alanı Hizmetleri için bir sanal ağ oluşturun.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. **Gönder**’e tıklayın.

Parolanızı değiştirdikten sonra birkaç dakika hello yeni parola Azure Active Directory Etki Alanı Hizmetleri'nde kullanılabilir değil. Birkaç dakika sonra (genellikle, yaklaşık 20 dakika), yeni değiştirilen hello parola kullanarak yönetilen etki alanına katılmış toohello olan toocomputers oturum açabilirsiniz.

## <a name="related-content"></a>İlgili İçerik
* [Nasıl tooupdate kendi parolanızı](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Azure AD’de Parola Yönetimi kullanmaya başlama](../active-directory/active-directory-passwords-getting-started.md)
* [Parola eşitlemeyi etkinleştirme tooAzure Active Directory Etki Alanı Hizmetleri'nde eşitlenmiş Azure AD Kiracı](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Azure Active Directory Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
* [Windows sanal makine tooan Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md)
* [Red Hat Enterprise Linux sanal makine tooan Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
