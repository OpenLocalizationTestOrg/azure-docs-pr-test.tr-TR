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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="bc610-103">Parola Eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bc610-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="bc610-104">Önceki görevlerde Azure Active Directory (Azure AD) kiracınız için Azure Active Directory Domain Services hizmetini etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="bc610-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="bc610-105">Merhaba sonraki kimlik bilgisi karmalarını tooenable eşitlenmesi için NT LAN Yöneticisi (NTLM) ve Kerberos kimlik doğrulaması tooAzure AD etki alanı Hizmetleri gerekli bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="bc610-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="bc610-106">Kimlik bilgisi eşitlemesini ayarladıktan sonra kullanıcılar toohello yönetilen etki alanında Kurumsal kimlik ile oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="bc610-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="bc610-107">Merhaba adımlar, Azure AD Connect kullanarak şirket içi dizininizden eşitlenen yalnızca bulut kullanıcı hesapları vs kullanıcı hesapları için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="bc610-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="bc610-108">Azure AD kiracınıza bileşimini varsa ve yalnızca kullanıcılar, şirket içi bulut AD, her iki adımın tooperform gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc610-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="bc610-109">**Yalnızca bulut kullanıcı hesapları**: [yalnızca bulut kullanıcı tooyour yönetilen etki alanı hesapları için parola eşitleme](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="bc610-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="bc610-110">**Şirket içi kullanıcı hesaplarını**: [, şirket içi eşitlenen kullanıcı hesapları için parola eşitleme AD tooyour yönetilen etki alanı](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="bc610-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="bc610-111">Görev 5: sadece bulutta kullanıcı hesapları için parola eşitleme tooyour etki alanı yönetilen etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bc610-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="bc610-112">Merhaba tooauthenticate kullanıcılar yönetilen etki alanı, Azure Active Directory etki alanı Hizmetleri NTLM ve Kerberos kimlik doğrulaması için uygun bir biçimde karmaları kimlik bilgisi.</span><span class="sxs-lookup"><span data-stu-id="bc610-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="bc610-113">Azure AD bırakmaz oluşturmak veya Azure Active Directory etki alanı Hizmetleri, kiracınızın etkinleştirinceye kadar NTLM veya Kerberos kimlik doğrulaması için gerekli hello biçimi kimlik bilgisi karmalarını depolayın.</span><span class="sxs-lookup"><span data-stu-id="bc610-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="bc610-114">Güvenliğe dayalı bariz nedenlerle, Azure AD düz metin biçiminde de hiçbir parola kimlik bilgisi depolamaz.</span><span class="sxs-lookup"><span data-stu-id="bc610-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="bc610-115">Bu nedenle, Azure AD kullanıcıların varolan kimlik bilgilerine göre bu NTLM veya Kerberos kimlik bilgisi karmalarını oluşturur bir şekilde tooautomatically yok.</span><span class="sxs-lookup"><span data-stu-id="bc610-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="bc610-116">Kuruluşunuz yalnızca bulutta kullanıcı hesapları varsa, toouse Azure Active Directory etki alanı Hizmetleri gereksinim duyan kullanıcılar parolalarını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc610-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="bc610-117">Azure AD dizininizi hello Azure portalında veya Azure AD PowerShell cmdlet'leri kullanılarak oluşturulmuş bir hesap bir yalnızca bulut kullanıcı hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="bc610-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="bc610-118">Bu tür kullanıcı hesapları şirket içi dizinden eşitlenmez.</span><span class="sxs-lookup"><span data-stu-id="bc610-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="bc610-119">Bu parola değişikliği işlemi, Azure Active Directory etki alanı Hizmetleri Azure AD'de oluşturulan Kerberos ve NTLM kimlik doğrulaması toobe için gerekli olan karmaları hello kimlik bilgisi neden olur.</span><span class="sxs-lookup"><span data-stu-id="bc610-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="bc610-120">Hello tüm kullanıcılar Kiracı toouse Azure Active Directory etki alanı Hizmetleri gereksinim duyan veya bunları toochange söylemek için hello parolaları ya da dolabilir parolalarını.</span><span class="sxs-lookup"><span data-stu-id="bc610-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="bc610-121">Yalnızca bulutta yer alan kullanıcı hesabı için NTLM ve Kerberos kimlik bilgileri karması oluşturmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bc610-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="bc610-122">Parolalarını değiştirebilmeniz için tooprovide kullanıcılar, gereken hello talimatlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bc610-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="bc610-123">Toohello Git [Azure AD erişim paneli](http://myapps.microsoft.com) kuruluşunuz için sayfa.</span><span class="sxs-lookup"><span data-stu-id="bc610-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Hello Azure AD erişim Paneli başlatma](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="bc610-125">Merhaba sağ üst köşesindeki, adınızın tıklatın ve seçin **profil** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="bc610-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Profil seçme](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="bc610-127">Merhaba üzerinde **profil** sayfasında, tıklatın **parola değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="bc610-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![“Parola değiştir”e tıklayın](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="bc610-129">Merhaba, **parola değiştirme** seçeneği hello erişim paneli penceresinde görüntülenmez, kuruluşunuzun yapılandırılmış olduğundan emin olun [Azure AD'de parola yönetimi](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc610-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="bc610-130">Merhaba üzerinde **parolasını değiştirme** sayfasında, var olan (eski) parolanızı yazın, yeni bir parola yazın ve ardından onaylayın.</span><span class="sxs-lookup"><span data-stu-id="bc610-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Azure AD Etki Alanı Hizmetleri için bir sanal ağ oluşturun.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="bc610-132">**Gönder**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc610-132">Click **submit**.</span></span>

<span data-ttu-id="bc610-133">Parolanızı değiştirdikten sonra birkaç dakika hello yeni parola Azure Active Directory Etki Alanı Hizmetleri'nde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="bc610-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="bc610-134">Birkaç dakika sonra (genellikle, yaklaşık 20 dakika), yeni değiştirilen hello parola kullanarak yönetilen etki alanına katılmış toohello olan toocomputers oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc610-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="bc610-135">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="bc610-135">Related Content</span></span>
* [<span data-ttu-id="bc610-136">Nasıl tooupdate kendi parolanızı</span><span class="sxs-lookup"><span data-stu-id="bc610-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="bc610-137">Azure AD’de Parola Yönetimi kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="bc610-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="bc610-138">Parola eşitlemeyi etkinleştirme tooAzure Active Directory Etki Alanı Hizmetleri'nde eşitlenmiş Azure AD Kiracı</span><span class="sxs-lookup"><span data-stu-id="bc610-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="bc610-139">Azure Active Directory Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="bc610-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="bc610-140">Windows sanal makine tooan Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="bc610-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="bc610-141">Red Hat Enterprise Linux sanal makine tooan Azure Active Directory etki alanı Hizmetleri tarafından yönetilen etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="bc610-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
