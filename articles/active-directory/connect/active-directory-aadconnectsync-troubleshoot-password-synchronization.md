---
title: "Azure AD Connect eşitleme ile aaaTroubleshoot parola eşitleme | Microsoft Docs"
description: "Bu makalede hakkında bilgi sağlar tootroubleshoot parola eşitleme sorunlarını."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="88e94-103">Parola Eşitleme ile Azure AD Connect eşitleme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="88e94-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="88e94-104">Bu konu, parola eşitleme ile nasıl tootroubleshoot sorunlar için adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="88e94-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="88e94-105">Parolalar beklendiği gibi eşitlemiyor, bir kullanıcı alt kümesini veya tüm kullanıcılar için olabilir.</span><span class="sxs-lookup"><span data-stu-id="88e94-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="88e94-106">Azure Active Directory (Azure AD) için dağıtım 1.1.524.0 sürümüyle bağlanın ya da daha sonra artık tootroubleshoot parola eşitleme sorunlarını kullanabileceğiniz bir tanı cmdlet:</span><span class="sxs-lookup"><span data-stu-id="88e94-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="88e94-107">Burada hiçbir parolalar eşitlenir bir sorun varsa, toohello başvurun [hiçbir parolalar eşitlenir: hello tanılama cmdlet'ini kullanarak sorun giderme](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) bölümü.</span><span class="sxs-lookup"><span data-stu-id="88e94-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="88e94-108">Ayrı ayrı nesneleri ile ilgili bir sorun varsa, toohello başvuran [bir nesne değil parolaları eşitleme: hello tanılama cmdlet'ini kullanarak sorun giderme](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) bölümü.</span><span class="sxs-lookup"><span data-stu-id="88e94-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="88e94-109">Azure AD Connect dağıtımı daha eski sürümleri için:</span><span class="sxs-lookup"><span data-stu-id="88e94-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="88e94-110">Burada hiçbir parolalar eşitlenir bir sorun varsa, toohello başvurmak [hiçbir parolalar eşitlenir: sorun giderme adımları el ile](#no-passwords-are-synchronized-manual-troubleshooting-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="88e94-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="88e94-111">Ayrı ayrı nesneleri ile ilgili bir sorun varsa, toohello başvuran [bir nesne değil parolaları eşitleme: sorun giderme adımları el ile](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="88e94-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="88e94-112">Hiçbir parolalar eşitlenir: hello tanılama cmdlet'ini kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="88e94-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="88e94-113">Merhaba kullanabilirsiniz `Invoke-ADSyncDiagnostics` hiçbir parolalar neden eşitlenir çıkışı cmdlet toofigure.</span><span class="sxs-lookup"><span data-stu-id="88e94-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="88e94-114">Merhaba `Invoke-ADSyncDiagnostics` cmdlet'ini veya üstünü yalnızca Azure AD Connect sürüm 1.1.524.0 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="88e94-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="88e94-115">Merhaba tanılama cmdlet'ini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="88e94-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="88e94-116">Burada hiçbir parolalar eşitlenir tootroubleshoot sorunlar:</span><span class="sxs-lookup"><span data-stu-id="88e94-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="88e94-117">Merhaba ile Azure AD Connect sunucunuzdaki yeni bir Windows PowerShell oturumu açın **yönetici olarak çalıştır** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="88e94-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="88e94-118">Çalıştırma `Set-ExecutionPolicy RemoteSigned` veya `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="88e94-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="88e94-119">`Import-Module ADSyncDiagnostics` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88e94-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="88e94-120">`Invoke-ADSyncDiagnostics -PasswordSync` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88e94-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="88e94-121">Merhaba hello cmdlet'inin sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="88e94-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="88e94-122">Merhaba tanılama cmdlet'i denetimleri aşağıdaki hello gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="88e94-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="88e94-123">Bu hello doğrular parola eşitleme özelliği, Azure AD kiracınız için etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="88e94-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="88e94-124">Bu hello Azure AD Connect sunucusu hazırlama modunda değil doğrular.</span><span class="sxs-lookup"><span data-stu-id="88e94-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="88e94-125">Varolan her (tooan var olan Active Directory ormanı karşılık gelir) Active Directory Bağlayıcısı şirket için:</span><span class="sxs-lookup"><span data-stu-id="88e94-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="88e94-126">Bu hello doğrular parola eşitleme özelliği etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="88e94-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="88e94-127">Parola eşitleme sinyali olayları hello arar Windows uygulama olay günlükleri.</span><span class="sxs-lookup"><span data-stu-id="88e94-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="88e94-128">Her Active Directory etki alanı için hello şirket içi Active Directory Bağlayıcısı altında:</span><span class="sxs-lookup"><span data-stu-id="88e94-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="88e94-129">Bu hello doğrular etki alanıdır hello Azure AD Connect sunucudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="88e94-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="88e94-130">Hello doğru kullanıcı adı, parola ve parola eşitlemesi için gerekli izinlere sahip olduğundan'Hello şirket içi Active Directory Bağlayıcısı tarafından kullanılan hello Active Directory etki alanı Hizmetleri (AD DS) hesaplarını doğrular.</span><span class="sxs-lookup"><span data-stu-id="88e94-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="88e94-131">Diyagram aşağıdaki hello hello cmdlet'i bir tek etki alanı, şirket içi Active Directory topolojisi için hello sonuçlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="88e94-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Parola Eşitleme için tanılama çıktıları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="88e94-133">Bu bölümde Hello kalan hello cmdlet tarafından döndürülen belirli sonuçları açıklar ve ilgili konular.</span><span class="sxs-lookup"><span data-stu-id="88e94-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="88e94-134">Parola eşitleme özelliği etkin değil</span><span class="sxs-lookup"><span data-stu-id="88e94-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="88e94-135">Parola Eşitleme hello Azure AD Connect Sihirbazı'nı kullanarak etkinleştirmediyseniz hello aşağıdaki hata döndürdü:</span><span class="sxs-lookup"><span data-stu-id="88e94-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![Parola Eşitleme etkin değil](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="88e94-137">Azure AD Connect'i hazırlama modunda sunucusudur</span><span class="sxs-lookup"><span data-stu-id="88e94-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="88e94-138">Hazırlama modu Hello Azure AD Connect sunucusu ise, parola eşitleme geçici olarak devre dışıdır ve hello aşağıdaki hata döndürülür:</span><span class="sxs-lookup"><span data-stu-id="88e94-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Azure AD Connect'i hazırlama modunda sunucusudur](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="88e94-140">Parola eşitleme sinyali olayı yok</span><span class="sxs-lookup"><span data-stu-id="88e94-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="88e94-141">Her bir şirket içi Active Directory Bağlayıcısı kendi parola eşitleme kanalının sahiptir.</span><span class="sxs-lookup"><span data-stu-id="88e94-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="88e94-142">Merhaba parola eşitleme kanalının kurulur ve eşitlenen tüm parola değişiklikleri toobe yok, bir sinyal olayı (EventID 654) her 30 dakikada hello Windows uygulama olay günlüğü altında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="88e94-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="88e94-143">Her şirket içi Active Directory Bağlayıcısı için hello cmdlet hello karşılık gelen sinyal olayları son üç saat arar.</span><span class="sxs-lookup"><span data-stu-id="88e94-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="88e94-144">Sinyal Olayı bulunamadı, hello aşağıdaki hata döndürülür:</span><span class="sxs-lookup"><span data-stu-id="88e94-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Olay yok parola eşitleme Kalp yapı](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="88e94-146">AD DS hesap doğru izinlere sahip değil</span><span class="sxs-lookup"><span data-stu-id="88e94-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="88e94-147">Merhaba tarafından kullanılan hello AD DS hesabı içi bağlı Active Directory Bağlayıcısı toosynchronize parola karmaları hello uygun izinlere sahip değil, hello aşağıdaki hata döndürülür:</span><span class="sxs-lookup"><span data-stu-id="88e94-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Yanlış kimlik bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="88e94-149">Kullanıcı adı veya parola yanlış AD DS hesap</span><span class="sxs-lookup"><span data-stu-id="88e94-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="88e94-150">Merhaba AD DS hesap tarafından kullanılan hello şirket içi Active Directory Bağlayıcısı toosynchronize parola karmaları sahip bir yanlış kullanıcı adı veya parola, hello aşağıdaki hata döndürülür:</span><span class="sxs-lookup"><span data-stu-id="88e94-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Yanlış kimlik bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="88e94-152">Bir nesne değil parolaları eşitleme: hello tanılama cmdlet'ini kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="88e94-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="88e94-153">Merhaba kullanabilirsiniz `Invoke-ADSyncDiagnostics` neden bir nesne not synchronızıng parolaları cmdlet toodetermine.</span><span class="sxs-lookup"><span data-stu-id="88e94-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="88e94-154">Merhaba `Invoke-ADSyncDiagnostics` cmdlet'ini veya üstünü yalnızca Azure AD Connect sürüm 1.1.524.0 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="88e94-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="88e94-155">Merhaba tanılama cmdlet'ini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="88e94-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="88e94-156">Burada hiçbir parolalar eşitlenir tootroubleshoot sorunlar:</span><span class="sxs-lookup"><span data-stu-id="88e94-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="88e94-157">Merhaba ile Azure AD Connect sunucunuzdaki yeni bir Windows PowerShell oturumu açın **yönetici olarak çalıştır** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="88e94-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="88e94-158">Çalıştırma `Set-ExecutionPolicy RemoteSigned` veya `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="88e94-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="88e94-159">`Import-Module ADSyncDiagnostics` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88e94-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="88e94-160">Hello aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="88e94-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="88e94-161">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="88e94-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="88e94-162">Merhaba hello cmdlet'inin sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="88e94-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="88e94-163">Merhaba tanılama cmdlet'i denetimleri aşağıdaki hello gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="88e94-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="88e94-164">Merhaba Active Directory Bağlayıcısı alanı, meta veri deposu ve Azure Active Directory nesnesindeki hello Hello durumunu inceler AD bağlayıcı alanı.</span><span class="sxs-lookup"><span data-stu-id="88e94-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="88e94-165">Parola Eşitleme ile eşitleme kuralları etkinleştirilmiş ve toohello Active Directory nesnesi geçerli olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="88e94-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="88e94-166">Merhaba son girişimi toosynchronize hello nesnesi için parolayı hello tooretrieve ve görüntü hello sonuçlarını çalışır.</span><span class="sxs-lookup"><span data-stu-id="88e94-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="88e94-167">Aşağıdaki diyagramda hello hello hello cmdlet'inin sonuçlarını tek bir nesne için parola eşitleme sorunlarını giderirken gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="88e94-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Parola Eşitleme - tek nesne için tanılama çıktıları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="88e94-169">Bu bölümde Hello kalan hello cmdlet tarafından döndürülen belirli sonuçları açıklar ve ilgili konular.</span><span class="sxs-lookup"><span data-stu-id="88e94-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="88e94-170">dışarı aktarılan tooAzure AD Hello Active Directory nesnesi değil</span><span class="sxs-lookup"><span data-stu-id="88e94-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="88e94-171">Hello Azure AD kiracısında karşılık gelen hiçbir nesne olduğundan bu şirket içi Active Directory hesabı için parola eşitleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="88e94-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="88e94-172">Merhaba aşağıdaki hata döndürdü:</span><span class="sxs-lookup"><span data-stu-id="88e94-172">hello following error is returned:</span></span>

![Azure AD nesnesi eksik.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="88e94-174">Kullanıcının geçici bir parolaya sahip</span><span class="sxs-lookup"><span data-stu-id="88e94-174">User has a temporary password</span></span>
<span data-ttu-id="88e94-175">Şu anda Azure AD Connect geçici parolaları Azure AD ile eşitleme desteklemez.</span><span class="sxs-lookup"><span data-stu-id="88e94-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="88e94-176">Bir parola toobe geçici hello durumunda olduğu kabul edilir **sonraki oturumda parola Değiştir** seçeneği hello şirket içi Active Directory kullanıcı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="88e94-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="88e94-177">Merhaba aşağıdaki hata döndürdü:</span><span class="sxs-lookup"><span data-stu-id="88e94-177">hello following error is returned:</span></span>

![Geçici parolayı verilmez](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="88e94-179">Son deneme toosynchronize parola sonuçlarını kullanılamaz</span><span class="sxs-lookup"><span data-stu-id="88e94-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="88e94-180">Varsayılan olarak, Azure AD Connect yedi gün için parola eşitleme denemesi hello sonuçlarını depolar.</span><span class="sxs-lookup"><span data-stu-id="88e94-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="88e94-181">Seçili hello Active Directory nesne için kullanılabilen hiç sonuç yoksa uyarı aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="88e94-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Tanılama çıktıları tek nesnesi - parola eşitleme geçmişi yok](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="88e94-183">Hiçbir parolalar eşitlenir: sorun giderme adımları el ile</span><span class="sxs-lookup"><span data-stu-id="88e94-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="88e94-184">Hiçbir parolalar neden eşitlenir bu adımları toodetermine izleyin:</span><span class="sxs-lookup"><span data-stu-id="88e94-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="88e94-185">Merhaba Bağlan sunucu, [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="88e94-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="88e94-186">Bir sunucu hazırlama modunda parolaları eşitlemez.</span><span class="sxs-lookup"><span data-stu-id="88e94-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="88e94-187">Hello Hello komut dosyasını çalıştırmak [alma, parola eşitleme ayarları hello durum](#get-the-status-of-password-sync-settings) bölümü.</span><span class="sxs-lookup"><span data-stu-id="88e94-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="88e94-188">Merhaba parola eşitleme yapılandırmasına genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="88e94-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Parola Eşitleme ayarlarını PowerShell komut dosyası çıktısı](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="88e94-190">Azure AD'de Hello özelliği etkin değilse veya hello eşitleme kanal durumu etkin değilse, hello Connect Yükleme Sihirbazı'nı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88e94-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="88e94-191">Seçin **eşitleme seçeneklerini özelleştirme**ve Parola Eşitleme'seçimini kaldırın. Bu değişiklik hello özelliğini geçici olarak devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="88e94-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="88e94-192">Ardından hello Sihirbazı'nı yeniden çalıştırın ve parola eşitleme yeniden etkinleştirin. Merhaba komut dosyasını çalıştırmak yeniden yapılandırma hello tooverify doğrudur.</span><span class="sxs-lookup"><span data-stu-id="88e94-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="88e94-193">Hatalar için hello olay günlüğüne bakın.</span><span class="sxs-lookup"><span data-stu-id="88e94-193">Look in hello event log for errors.</span></span> <span data-ttu-id="88e94-194">Bir sorunu gösterir olayları aşağıdaki hello arayın:</span><span class="sxs-lookup"><span data-stu-id="88e94-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="88e94-195">Kaynak: "Dizin eşitleme" kimliği: 0, 611, 652, bu olayları görürseniz 655 bağlantı sorun oluştu.</span><span class="sxs-lookup"><span data-stu-id="88e94-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="88e94-196">Merhaba olay günlüğü iletisi bir sorun olduğu orman ile ilgili bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="88e94-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="88e94-197">Daha fazla bilgi için bkz: [bağlantı sorunu](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="88e94-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="88e94-198">Sinyal alınmadı bakın veya başka bir şey çalışılan gerekiyorsa, çalıştırmak [tüm parolaların tam eşitlemesi](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="88e94-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="88e94-199">Merhaba komut yalnızca bir kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88e94-199">Run hello script only once.</span></span>

6. <span data-ttu-id="88e94-200">Merhaba bkz [parolaları eşitleme değil bir nesne sorun giderme](#one-object-is-not-synchronizing-passwords) bölümü.</span><span class="sxs-lookup"><span data-stu-id="88e94-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="88e94-201">Bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="88e94-201">Connectivity problems</span></span>

<span data-ttu-id="88e94-202">Azure AD ile bağlantı var mı?</span><span class="sxs-lookup"><span data-stu-id="88e94-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="88e94-203">Mu hello hesap gerekli izinleri tooread hello parola karmaları tüm etki alanlarında?</span><span class="sxs-lookup"><span data-stu-id="88e94-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="88e94-204">Hızlı ayarları kullanarak bağlan yüklediyseniz hello izinleri zaten doğru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="88e94-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="88e94-205">Özel yükleme kullandıysanız, hello izinlerini el ile Merhaba aşağıdakileri yaparak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="88e94-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="88e94-206">Merhaba Active Directory Bağlayıcısı, başlangıç tarafından kullanılan toofind hello hesabı **Eşitleme Hizmeti Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="88e94-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="88e94-207">Çok Git**Bağlayıcılar**ve hello şirket içi Active Directory ormanı sorun giderme için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="88e94-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="88e94-208">Merhaba bağlayıcıyı seçin ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="88e94-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="88e94-209">Çok Git**tooActive Directory ormanına Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="88e94-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Active Directory Bağlayıcısı tarafından kullanılan hesap](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="88e94-211">Merhaba kullanıcı adını ve parolayı hello hesabının bulunduğu hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="88e94-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="88e94-212">Başlat **Active Directory Kullanıcıları ve Bilgisayarları**ve ardından daha önce bulunan hello hesabının hello kökündeki ormanınızdaki tüm etki alanlarının hello izleyin izinlere sahip olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="88e94-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="88e94-213">Dizin Değişikliklerini Çoğaltma</span><span class="sxs-lookup"><span data-stu-id="88e94-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="88e94-214">Tüm çoğaltma dizini değiştirir</span><span class="sxs-lookup"><span data-stu-id="88e94-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="88e94-215">Merhaba, etki alanı denetleyicileri ulaşılabilir Azure AD Connect tarafından misiniz?</span><span class="sxs-lookup"><span data-stu-id="88e94-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="88e94-216">Merhaba Connect sunucusu tooall etki alanı denetleyicileri bağlanamıyorsanız, yapılandırma **yalnızca tercih edilen etki alanı denetleyicisini kullanmasını**.</span><span class="sxs-lookup"><span data-stu-id="88e94-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Active Directory Bağlayıcısı tarafından kullanılan etki alanı denetleyicisi](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="88e94-218">Çok dön**Eşitleme Hizmeti Yöneticisi'ni** ve **yapılandırma dizini bölümü**.</span><span class="sxs-lookup"><span data-stu-id="88e94-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="88e94-219">Etki alanınızda seçin **dizin bölümlerini Seç**seçin hello **yalnızca tercih edilen etki alanı denetleyicilerinin kullandığı** onay kutusunu işaretleyin ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="88e94-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="88e94-220">Merhaba listesinde Bağlan parola eşitleme için kullanması gereken hello etki alanı denetleyicileri girin. Merhaba aynı liste içeri ve dışarı aktarma de için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88e94-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="88e94-221">Tüm etki alanları için bu adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="88e94-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="88e94-222">Merhaba komut dosyası hiçbir sinyal olduğunu gösteriyorsa, hello komut dosyasını Çalıştır [tüm parolaların tam eşitlemesi](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="88e94-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="88e94-223">Bir nesne değil parolaları eşitleme: sorun giderme adımları el ile</span><span class="sxs-lookup"><span data-stu-id="88e94-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="88e94-224">Bir nesnenin hello durumunu gözden geçirerek kolayca parola eşitleme sorunlarını giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88e94-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="88e94-225">İçinde **Active Directory Kullanıcıları ve Bilgisayarları**hello kullanıcı için arama yapın ve ardından bu hello doğrulayın **kullanıcı bir sonraki oturumda parola değiştirmeli** onay kutusu işaretli.</span><span class="sxs-lookup"><span data-stu-id="88e94-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory üretken parolaları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="88e94-227">Merhaba onay kutusu seçiliyse, hello kullanıcı toosign isteyin ve hello parolayı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="88e94-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="88e94-228">Geçici parolalar Azure AD ile eşitlenmemiş.</span><span class="sxs-lookup"><span data-stu-id="88e94-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="88e94-229">Merhaba parolası Active Directory'de doğru görünüyorsa, hello eşitleme altyapısı hello kullanıcı izleyin.</span><span class="sxs-lookup"><span data-stu-id="88e94-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="88e94-230">Şirket içi Active Directory tooAzure AD alanından aşağıdaki hello kullanıcı tarafından hello nesnesinde açıklayıcı bir hata olup olmadığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88e94-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="88e94-231">a.</span><span class="sxs-lookup"><span data-stu-id="88e94-231">a.</span></span> <span data-ttu-id="88e94-232">Merhaba Başlat [Eşitleme Hizmeti Yöneticisi'ni](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="88e94-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="88e94-233">b.</span><span class="sxs-lookup"><span data-stu-id="88e94-233">b.</span></span> <span data-ttu-id="88e94-234">Tıklatın **Bağlayıcılar**.</span><span class="sxs-lookup"><span data-stu-id="88e94-234">Click **Connectors**.</span></span>

    <span data-ttu-id="88e94-235">c.</span><span class="sxs-lookup"><span data-stu-id="88e94-235">c.</span></span> <span data-ttu-id="88e94-236">Select hello **Active Directory Bağlayıcısı** hello kullanıcının bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="88e94-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="88e94-237">d.</span><span class="sxs-lookup"><span data-stu-id="88e94-237">d.</span></span> <span data-ttu-id="88e94-238">Seçin **bağlayıcı alanı arama**.</span><span class="sxs-lookup"><span data-stu-id="88e94-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="88e94-239">e.</span><span class="sxs-lookup"><span data-stu-id="88e94-239">e.</span></span> <span data-ttu-id="88e94-240">Merhaba, **kapsam** kutusunda **DN ya da bağlantı**ve sorun gidermeye hello kullanıcının tam DN hello girin.</span><span class="sxs-lookup"><span data-stu-id="88e94-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Bağlayıcı alanı DN'si kullanıcı ara](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="88e94-242">f.</span><span class="sxs-lookup"><span data-stu-id="88e94-242">f.</span></span> <span data-ttu-id="88e94-243">Aradığınız ve ardından hello kullanıcı bulun **özellikleri** toosee tüm öznitelikleri hello.</span><span class="sxs-lookup"><span data-stu-id="88e94-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="88e94-244">Merhaba kullanıcı hello arama sonucunda değilse doğrulayın, [filtreleme kuralları](active-directory-aadconnectsync-configure-filtering.md) ve, çalıştırdığınızdan emin olun [Uygula ve değişiklikleri doğrulamak](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) hello kullanıcı tooappear Bağlan için.</span><span class="sxs-lookup"><span data-stu-id="88e94-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="88e94-245">g.</span><span class="sxs-lookup"><span data-stu-id="88e94-245">g.</span></span> <span data-ttu-id="88e94-246">geçen hafta toosee hello parola eşitleme hello hello nesne ayrıntılarını tıklatın **günlük**.</span><span class="sxs-lookup"><span data-stu-id="88e94-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Nesne günlük ayrıntıları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="88e94-248">Merhaba nesne günlük boşsa, Azure AD Connect oluşturulamıyor tooread hello parola karması Active Directory'den kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="88e94-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="88e94-249">Sorunlarını giderme devam [bağlantı hataları](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="88e94-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="88e94-250">Başka bir değerden görürseniz **başarı**, toohello tabloya başvuruda [Parola Eşitleme günlüğü](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="88e94-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="88e94-251">h.</span><span class="sxs-lookup"><span data-stu-id="88e94-251">h.</span></span> <span data-ttu-id="88e94-252">Select hello **çizgileri** sekmesinde ve bu en az bir eşitleme kuralı hello emin **PasswordSync** sütunu **True**.</span><span class="sxs-lookup"><span data-stu-id="88e94-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="88e94-253">Merhaba Varsayılan yapılandırmada hello hello eşitleme kuralının adıdır **içinde AD'den - kullanıcı AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="88e94-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Bir kullanıcı hakkındaki bilgileri çizgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="88e94-255">ı.</span><span class="sxs-lookup"><span data-stu-id="88e94-255">i.</span></span> <span data-ttu-id="88e94-256">Tıklatın **meta veri deposu nesne özellikleri** toodisplay kullanıcı özniteliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="88e94-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Meta veri bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="88e94-258">Olduğunu doğrulayın hiçbir **cloudFiltered** özniteliği mevcut.</span><span class="sxs-lookup"><span data-stu-id="88e94-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="88e94-259">Merhaba etki alanı öznitelikler (domainFQDN ve domainNetBios) hello beklenen değerler olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88e94-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="88e94-260">j.</span><span class="sxs-lookup"><span data-stu-id="88e94-260">j.</span></span> <span data-ttu-id="88e94-261">Merhaba tıklatın **Bağlayıcılar** sekmesi. Bağlayıcılar tooboth şirket içi Active Directory gördüğünüzden emin olun ve Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e94-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Meta veri bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="88e94-263">k.</span><span class="sxs-lookup"><span data-stu-id="88e94-263">k.</span></span> <span data-ttu-id="88e94-264">Azure AD temsil eden select hello satıra tıklayın **özellikleri**ve ardından hello **Lineage** sekmesini hello bağlayıcı alanı nesne hello bir giden kuralı olmalıdır **PasswordSync** sütun kümesi çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="88e94-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="88e94-265">Merhaba Varsayılan yapılandırmada hello hello eşitleme kuralının adıdır **tooAAD - kullanıcı katılma çıkışı**.</span><span class="sxs-lookup"><span data-stu-id="88e94-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Bağlayıcı alanı nesne özellikleri iletişim kutusu](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="88e94-267">Parola Eşitleme günlüğü</span><span class="sxs-lookup"><span data-stu-id="88e94-267">Password sync log</span></span>
<span data-ttu-id="88e94-268">Merhaba durum sütun değerleri aşağıdaki hello sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="88e94-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="88e94-269">Durum</span><span class="sxs-lookup"><span data-stu-id="88e94-269">Status</span></span> | <span data-ttu-id="88e94-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88e94-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88e94-271">Başarılı</span><span class="sxs-lookup"><span data-stu-id="88e94-271">Success</span></span> |<span data-ttu-id="88e94-272">Parola başarıyla eşitlendi.</span><span class="sxs-lookup"><span data-stu-id="88e94-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="88e94-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="88e94-273">FilteredByTarget</span></span> |<span data-ttu-id="88e94-274">Parola çok ayarlamak**kullanıcı bir sonraki oturumda parola değiştirmeli**.</span><span class="sxs-lookup"><span data-stu-id="88e94-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="88e94-275">Parola eşitlenmemiş.</span><span class="sxs-lookup"><span data-stu-id="88e94-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="88e94-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="88e94-276">NoTargetConnection</span></span> |<span data-ttu-id="88e94-277">Nesne yok hello meta veri deposu veya hello Azure AD Bağlayıcısı alanı.</span><span class="sxs-lookup"><span data-stu-id="88e94-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="88e94-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="88e94-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="88e94-279">Nesnesi Hello şirket içi Active Directory Bağlayıcısı alanı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="88e94-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="88e94-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="88e94-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="88e94-281">hello Azure AD Bağlayıcısı alanı Hello nesnesinde henüz verilemez.</span><span class="sxs-lookup"><span data-stu-id="88e94-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="88e94-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="88e94-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="88e94-283">Günlük girişi 1.0.9125.0 Yapı önce oluşturuldu ve eski durumuna gösterilir.</span><span class="sxs-lookup"><span data-stu-id="88e94-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="88e94-284">Hata</span><span class="sxs-lookup"><span data-stu-id="88e94-284">Error</span></span> |<span data-ttu-id="88e94-285">Hizmet bilinmeyen bir hata döndürdü.</span><span class="sxs-lookup"><span data-stu-id="88e94-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="88e94-286">Bilinmeyen</span><span class="sxs-lookup"><span data-stu-id="88e94-286">Unknown</span></span> |<span data-ttu-id="88e94-287">Tooprocess parola karmaları toplu çalışırken bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="88e94-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="88e94-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="88e94-288">MissingAttribute</span></span> |<span data-ttu-id="88e94-289">Azure AD etki alanı Hizmetleri tarafından gereken belirli öznitelikleri (örneğin, Kerberos karması) kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="88e94-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="88e94-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="88e94-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="88e94-291">Azure AD etki alanı Hizmetleri tarafından gereken belirli öznitelikleri (örneğin, Kerberos karması) daha önce kullanılamıyordu.</span><span class="sxs-lookup"><span data-stu-id="88e94-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="88e94-292">Bir deneme tooresynchronize hello kullanıcının parola karmasını yapılır.</span><span class="sxs-lookup"><span data-stu-id="88e94-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="88e94-293">Betik toohelp sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="88e94-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="88e94-294">Parola Eşitleme ayarlarının Hello durumunu Al</span><span class="sxs-lookup"><span data-stu-id="88e94-294">Get hello status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="88e94-295">Tüm parolaların tam eşitlemesi</span><span class="sxs-lookup"><span data-stu-id="88e94-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="88e94-296">Bu komut dosyası yalnızca bir kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88e94-296">Run this script only once.</span></span> <span data-ttu-id="88e94-297">Bu birden çok kez toorun ihtiyacınız varsa, başka bir şey hello sorunudur.</span><span class="sxs-lookup"><span data-stu-id="88e94-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="88e94-298">tootroubleshoot hello sorun, Microsoft desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="88e94-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="88e94-299">Komut dosyası izleyen hello kullanarak bir tam eşitleme tüm parolaların tetikleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="88e94-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="88e94-300">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="88e94-300">Next steps</span></span>
* [<span data-ttu-id="88e94-301">Parola Eşitleme ile Azure AD Connect eşitleme uygulama</span><span class="sxs-lookup"><span data-stu-id="88e94-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="88e94-302">Azure AD Connect eşitleme: eşitleme seçeneklerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="88e94-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="88e94-303">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="88e94-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
