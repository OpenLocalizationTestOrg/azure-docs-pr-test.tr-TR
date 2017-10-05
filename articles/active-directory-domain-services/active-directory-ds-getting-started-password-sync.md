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
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="83cf3-103">Azure Active Directory Domain Services ile parola eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="83cf3-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="83cf3-104">Önceki görevlerde Azure Active Directory (Azure AD) kiracınız için Azure Active Directory Domain Services hizmetini etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="83cf3-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="83cf3-105">Sıradaki görev, NT LAN Manager (NTLM) ve Kerberos kimlik doğrulaması için gereken kimlik bilgisi karmalarının Azure AD Domain Services ile eşitlemesini etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="83cf3-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="83cf3-106">Kimlik bilgisi eşitlemesini ayarladıktan sonra kullanıcılar, şirket kimlik bilgileri ile yönetilen etki alanında oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="83cf3-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="83cf3-107">İşlemin adımları, yalnızca bulutta yer alan kullanıcı hesapları ile Azure AD Connect kullanılarak şirket içi dizininizden eşitlenmiş hesaplar arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="83cf3-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="83cf3-108">Azure AD kiracınızda yalnızca bulut kullanıcılarıyla ve şirket içi AD kullanıcılarının bir bileşimi varsa her iki işlemin de adımlarını takip etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="83cf3-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="83cf3-109">**Yalnızca bulutta yer alan kullanıcı hesapları**: [Yönetilen etki alanınıza yalnızca bulutta yer alan kullanıcı hesaplarının parolalarını eşitleyin.](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="83cf3-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="83cf3-110">**Şirket içi kullanıcı hesapları**: [Yönetilen etki alanınıza şirket içi AD’nizden eşitlenmiş kullanıcı hesaplarının parolalarını eşitleyin.](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="83cf3-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="83cf3-111">5. Görev: Yönetilen etki alanınıza yalnızca bulutta yer alan kullanıcı hesaplarının parolalarını eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="83cf3-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="83cf3-112">Yönetilen etki alanındaki kullanıcıların kimliklerini doğrulamak için, Azure Active Directory Domain Services’ın NTLM ve Kerberos kimlik doğrulamasına uygun biçimde kimlik bilgisi karmaları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83cf3-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="83cf3-113">Kiracınız için Azure Active Directory Domain Services’ı etkinleştirene kadar, Azure AD, NTLM veya Kerberos kimlik doğrulaması için gereken biçimde kimlik bilgisi karmaları oluşturmaz veya depolamaz.</span><span class="sxs-lookup"><span data-stu-id="83cf3-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="83cf3-114">Güvenliğe dayalı bariz nedenlerle, Azure AD düz metin biçiminde de hiçbir parola kimlik bilgisi depolamaz.</span><span class="sxs-lookup"><span data-stu-id="83cf3-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="83cf3-115">Bu nedenle, Azure AD’nin kullanıcıların mevcut kimlik bilgileri temelinde otomatik olarak bu NTLM veya Kerberos kimlik bilgisi karmalarını oluşturabileceği bir yol yoktur.</span><span class="sxs-lookup"><span data-stu-id="83cf3-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="83cf3-116">Kuruluşunuz yalnızca bulutta yer alan bir kullanıcı hesabına sahipse Azure Active Directory Domain Services'i kullanması gereken kullanıcıların parolalarını değiştirmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="83cf3-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="83cf3-117">Yalnızca bulutta yer alan bir kullanıcı hesabı, Azure portal veya Azure AD PowerShell cmdlet’leri kullanılarak Azure AD dizininizde oluşturulmuş bir hesaptır.</span><span class="sxs-lookup"><span data-stu-id="83cf3-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="83cf3-118">Bu tür kullanıcı hesapları şirket içi dizinden eşitlenmez.</span><span class="sxs-lookup"><span data-stu-id="83cf3-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="83cf3-119">Bu parola değişikliği işlemi, Kerberos ve NTLM kimlik doğrulaması için Azure Active Directory Domain Services'in gerektirdiği kimlik bilgisi karmalarının Azure AD'de oluşturulmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="83cf3-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="83cf3-120">Kiracıdaki Azure Active Directory Domain Services'i kullanması gereken tüm kullanıcıların parolalarının süresinin dolmasını sağlayabilir veya bu kullanıcılardan parolalarını değiştirmelerini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83cf3-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="83cf3-121">Yalnızca bulutta yer alan kullanıcı hesabı için NTLM ve Kerberos kimlik bilgileri karması oluşturmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="83cf3-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="83cf3-122">Kullanıcılara parolalarını değiştirebilmeleri için sağlamanız gereken yönergeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="83cf3-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="83cf3-123">Kuruluşunuzun [Azure AD Erişim Paneli](http://myapps.microsoft.com) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="83cf3-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Azure AD erişim panelini başlatma](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="83cf3-125">Sağ üst köşede adınıza tıklayın ve menüden **Profil**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="83cf3-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Profil seçme](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="83cf3-127">**Profil** sayfasında **Parola değiştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83cf3-127">On the **Profile** page, click on **Change password**.</span></span>

    ![“Parola değiştir”e tıklayın](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="83cf3-129">Erişim Paneli penceresinde **Parola değiştir** seçeneği gösterilmiyorsa, kuruluşunuzun [Azure AD'de parola yönetimini](../active-directory/active-directory-passwords-getting-started.md) yapılandırdığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="83cf3-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="83cf3-130">**Parola değiştir** sayfasında mevcut (eski) parolanızı yazın ve ardından yeni bir parola yazıp onaylayın.</span><span class="sxs-lookup"><span data-stu-id="83cf3-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Azure AD Etki Alanı Hizmetleri için bir sanal ağ oluşturun.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="83cf3-132">**Gönder**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83cf3-132">Click **submit**.</span></span>

<span data-ttu-id="83cf3-133">Parolanızı değiştirdikten birkaç dakika sonra, yeni parola Azure Active Directory Domain Services ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="83cf3-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="83cf3-134">Birkaç dakika daha geçtikten sonra (genellikle 20 dakika civarı), yönetilen etki alanına katılmış bilgisayarlarda yeni değiştirilen parolayı kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83cf3-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="83cf3-135">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="83cf3-135">Related Content</span></span>
* [<span data-ttu-id="83cf3-136">Kendi parolanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="83cf3-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="83cf3-137">Azure AD’de Parola Yönetimi kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="83cf3-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="83cf3-138">Eşitlenmiş Azure AD kiracısı için Azure Active Directory Domain Services ile parola eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="83cf3-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="83cf3-139">Azure Active Directory Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="83cf3-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="83cf3-140">Windows sanal makinesini Azure Active Directory Domain Services tarafından yönetilen bir etki alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="83cf3-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="83cf3-141">Red Hat Enterprise Linux sanal makinesini Azure Active Directory Domain Services tarafından yönetilen bir etki alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="83cf3-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
