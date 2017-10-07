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
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a><span data-ttu-id="fdde3-103">Varolan NPS altyapınızı Azure multi-Factor Authentication ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="fdde3-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="fdde3-104">Hello Azure MFA için ağ ilkesi sunucusu (NPS) uzantısı mevcut sunucularınızı kullanarak bulut tabanlı MFA yetenekleri tooyour kimlik doğrulaması altyapısı ekler.</span><span class="sxs-lookup"><span data-stu-id="fdde3-104">hello Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities tooyour authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="fdde3-105">Merhaba NPS uzantısı telefon araması, SMS mesajı ya da telefon uygulama doğrulama tooyour var olan kimlik doğrulama akışı yapılandırın ve yeni sunucuların bakımını tooinstall gerek kalmadan ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdde3-105">With hello NPS extension, you can add phone call, text message, or phone app verification tooyour existing authentication flow without having tooinstall, configure, and maintain new servers.</span></span> 

<span data-ttu-id="fdde3-106">Bu uzantı hello Azure MFA sunucusu dağıtmadan tooprotect VPN bağlantıları isteyen kuruluşların için oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="fdde3-106">This extension was created for organizations that want tooprotect VPN connections without deploying hello Azure MFA Server.</span></span> <span data-ttu-id="fdde3-107">Merhaba NPS uzantısı ikinci öğe olarak kimlik doğrulaması Federasyon ya da eşitlenmiş kullanıcı için RADIUS ve bulut tabanlı Azure MFA tooprovide arasında bir bağdaştırıcı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="fdde3-107">hello NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA tooprovide a second factor of authentication for federated or synced users.</span></span>

<span data-ttu-id="fdde3-108">Hello NPS uzantısı için Azure MFA kullanıldığında, hello kimlik doğrulaması akışı hello aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="fdde3-108">When using hello NPS extension for Azure MFA, hello authentication flow includes hello following components:</span></span> 

1. <span data-ttu-id="fdde3-109">**NAS/VPN sunucusu** VPN istemcilerinden gelen istekleri alır ve bunları RADIUS isteklerini tooNPS sunucularına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="fdde3-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests tooNPS servers.</span></span> 
2. <span data-ttu-id="fdde3-110">**NPS sunucusu** tooActive Directory tooperform hello birincil kimlik doğrulaması için RADIUS isteklerini ve, başarı hello istek yüklü tooany uzantılarının geçirir hello bağlanır.</span><span class="sxs-lookup"><span data-stu-id="fdde3-110">**NPS Server** connects tooActive Directory tooperform hello primary authentication for hello RADIUS requests and, upon success, passes hello request tooany installed extensions.</span></span>  
3. <span data-ttu-id="fdde3-111">**NPS uzantısı** hello ikincil kimlik doğrulaması için bir istek tooAzure MFA tetikler.</span><span class="sxs-lookup"><span data-stu-id="fdde3-111">**NPS Extension** triggers a request tooAzure MFA for hello secondary authentication.</span></span> <span data-ttu-id="fdde3-112">Merhaba uzantısı hello yanıtını aldıktan sonra ve MFA testini hello başarılı olursa, Azure STS tarafından verilen bir MFA talep dahil güvenlik belirteçleri hello NPS sunucusu sağlayarak hello kimlik doğrulama isteğini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="fdde3-112">Once hello extension receives hello response, and if hello MFA challenge succeeds, it completes hello authentication request by providing hello NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="fdde3-113">**Azure MFA** Azure Active Directory tooretrieve hello kullanıcının ayrıntılarını ile iletişim kurar ve bir doğrulama yapılandırılmış yöntemi toohello kullanıcı kullanılarak hello ikincil kimlik doğrulaması gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-113">**Azure MFA** communicates with Azure Active Directory tooretrieve hello user’s details and performs hello secondary authentication using a verification method configured toohello user.</span></span>

<span data-ttu-id="fdde3-114">Aşağıdaki diyagramda hello bu üst düzey kimlik doğrulaması istek akışının gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fdde3-114">hello following diagram illustrates this high-level authentication request flow:</span></span> 

![Kimlik doğrulama akışı diyagramı](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="fdde3-116">Dağıtımınızı planlama</span><span class="sxs-lookup"><span data-stu-id="fdde3-116">Plan your deployment</span></span>

<span data-ttu-id="fdde3-117">özel bir yapılandırma gerekmez şekilde hello NPS uzantısı artıklık, otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-117">hello NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span>

<span data-ttu-id="fdde3-118">Gereksinim duyduğunuz kadar Azure MFA etkin NPS sunucusu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdde3-118">You can create as many Azure MFA-enabled NPS servers as you need.</span></span> <span data-ttu-id="fdde3-119">Birden çok sunucuya yüklerseniz, bunların her biri için bir fark istemci sertifikası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="fdde3-120">Her sunucu için bir sertifika oluşturmak, her sertifika tek tek güncelleştirin ve kapalı kalma süresi hakkında tüm sunucularınız üzerinde endişelenmeyin anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span>

<span data-ttu-id="fdde3-121">Toobe hello yeni Azure MFA etkin NPS sunucuları farkında gerekiyor VPN sunucularını kimlik doğrulama isteklerini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-121">VPN servers route authentication requests, so they need toobe aware of hello new Azure MFA-enabled NPS servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdde3-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fdde3-122">Prerequisites</span></span>

<span data-ttu-id="fdde3-123">Merhaba NPS uzantısı mevcut altyapınızla toowork amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fdde3-123">hello NPS extension is meant toowork with your existing infrastructure.</span></span> <span data-ttu-id="fdde3-124">Önkoşullar, önce aşağıdaki hello başlamak olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fdde3-124">Make sure you have hello following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="fdde3-125">Lisansları</span><span class="sxs-lookup"><span data-stu-id="fdde3-125">Licenses</span></span>

<span data-ttu-id="fdde3-126">Hello Azure MFA için NPS uzantısı olan kullanılabilir toocustomers ile [Azure multi-Factor Authentication için lisans](multi-factor-authentication.md) (Azure AD Premium, EMS veya MFA abonelik dahil).</span><span class="sxs-lookup"><span data-stu-id="fdde3-126">hello NPS Extension for Azure MFA is available toocustomers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span></span>

### <a name="software"></a><span data-ttu-id="fdde3-127">Yazılım</span><span class="sxs-lookup"><span data-stu-id="fdde3-127">Software</span></span>

<span data-ttu-id="fdde3-128">Windows Server 2008 R2 SP1 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="fdde3-128">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="fdde3-129">Kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="fdde3-129">Libraries</span></span>

<span data-ttu-id="fdde3-130">Bu kitaplıklar hello uzantısı ile otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-130">These libraries are installed automatically with hello extension.</span></span>
-   [<span data-ttu-id="fdde3-131">Visual Studio 2013 (X64) için Visual C++ yeniden dağıtılabilir paketleri</span><span class="sxs-lookup"><span data-stu-id="fdde3-131">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="fdde3-132">Microsoft Azure Active Directory için Windows PowerShell modülü sürümü 1.1.166.0</span><span class="sxs-lookup"><span data-stu-id="fdde3-132">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a><span data-ttu-id="fdde3-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdde3-133">Azure Active Directory</span></span>

<span data-ttu-id="fdde3-134">Merhaba NPS uzantısı kullanan herkes eşitlenen tooAzure Active Directory olmalıdır Azure AD Connect'i kullanarak ve MFA için kaydolması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-134">Everyone using hello NPS extension must be synced tooAzure Active Directory using Azure AD Connect, and must be registered for MFA.</span></span>

<span data-ttu-id="fdde3-135">Merhaba uzantısını yüklediğinizde, Azure AD kiracınız için hello dizin kimliği ve yönetici kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-135">When you install hello extension, you need hello directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="fdde3-136">Dizin Kimliğinizi hello bulabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fdde3-136">You can find your directory ID in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fdde3-137">Select hello yönetici olarak oturum aç **Azure Active Directory** hello soldaki simgesi seçip **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fdde3-137">Sign in as an administrator, select hello **Azure Active Directory** icon on hello left, then select **Properties**.</span></span> <span data-ttu-id="fdde3-138">Kopya hello GUID hello **dizin kimliği** kutusunda ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-138">Copy hello GUID in hello **Directory ID** box and save it.</span></span> <span data-ttu-id="fdde3-139">Merhaba NPS uzantısını yüklediğinizde bu GUID hello Kiracı kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-139">You use this GUID as hello tenant ID when you install hello NPS extension.</span></span>

![Azure Active Directory özellikleri'nin altında dizin kimliği bulunamıyor](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a><span data-ttu-id="fdde3-141">Ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="fdde3-141">Prepare your environment</span></span>

<span data-ttu-id="fdde3-142">Merhaba NPS uzantısını yüklemeden önce tooprepare istediğiniz, ortam toohandle hello kimlik doğrulama trafiğini.</span><span class="sxs-lookup"><span data-stu-id="fdde3-142">Before you install hello NPS extension, you want tooprepare you environment toohandle hello authentication traffic.</span></span>

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="fdde3-143">Etki alanına katılmış bir sunucuda Hello NPS rolünü etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fdde3-143">Enable hello NPS role on a domain-joined server</span></span>

<span data-ttu-id="fdde3-144">Merhaba NPS sunucusu tooAzure Active Directory bağlanır ve hello MFA istekleri doğrular.</span><span class="sxs-lookup"><span data-stu-id="fdde3-144">hello NPS server connects tooAzure Active Directory and authenticates hello MFA requests.</span></span> <span data-ttu-id="fdde3-145">Bu rol için bir sunucu seçin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-145">Choose one server for this role.</span></span> <span data-ttu-id="fdde3-146">RADIUS olmayan tüm istekler hataları hello NPS uzantısı oluşturur çünkü diğer hizmetler gelen istekleri işleyemez bir sunucu seçme öneririz.</span><span class="sxs-lookup"><span data-stu-id="fdde3-146">We recommend choosing a server that doesn't handle requests from other services, because hello NPS extension throws errors for any requests that aren't RADIUS.</span></span>

1. <span data-ttu-id="fdde3-147">Merhaba, sunucunuzda açmak **Ekle roller ve Özellikler Sihirbazı** hello Sunucu Yöneticisi'ni Hızlı Başlangıç menüsünde gelen.</span><span class="sxs-lookup"><span data-stu-id="fdde3-147">On your server, open hello **Add Roles and Features Wizard** from hello Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="fdde3-148">Seçin **rol tabanlı veya özellik tabanlı yükleme** için yükleme türü.</span><span class="sxs-lookup"><span data-stu-id="fdde3-148">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="fdde3-149">Select hello **Ağ İlkesi ve Erişim Hizmetleri** sunucu rolü.</span><span class="sxs-lookup"><span data-stu-id="fdde3-149">Select hello **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="fdde3-150">Bir pencere tooinform, gerekli özellikleri toorun bu rolü pop.</span><span class="sxs-lookup"><span data-stu-id="fdde3-150">A window may pop up tooinform you of required features toorun this role.</span></span>
4. <span data-ttu-id="fdde3-151">Hello sihirbaza hello onay sayfası kadar devam edin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-151">Continue through hello wizard until hello Confirmation page.</span></span> <span data-ttu-id="fdde3-152">Seçin **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="fdde3-152">Select **Install**.</span></span>

<span data-ttu-id="fdde3-153">NPS için belirlenmiş bir sunucunuz varsa, bu sunucu toohandle yapılandırmanız da hello VPN çözümü gelen gelen RADIUS istekleri.</span><span class="sxs-lookup"><span data-stu-id="fdde3-153">Now that you have a server designated for NPS, you should also configure this server toohandle incoming RADIUS requests from hello VPN solution.</span></span>

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a><span data-ttu-id="fdde3-154">VPN çözümü toocommunicate ile Merhaba NPS sunucusunu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fdde3-154">Configure your VPN solution toocommunicate with hello NPS server</span></span>

<span data-ttu-id="fdde3-155">Kullandığınız VPN çözümüne bağlı olarak, RADIUS kimlik doğrulama İlkesi farklılık adımları tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="fdde3-155">Depending on which VPN solution you use, hello steps tooconfigure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="fdde3-156">Bu ilke toopoint tooyour RADIUS NPS sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-156">Configure this policy toopoint tooyour RADIUS NPS server.</span></span>

### <a name="sync-domain-users-toohello-cloud"></a><span data-ttu-id="fdde3-157">Eşitleme etki alanı kullanıcıları toohello bulut</span><span class="sxs-lookup"><span data-stu-id="fdde3-157">Sync domain users toohello cloud</span></span>

<span data-ttu-id="fdde3-158">Bu adım zaten kiracınız üzerinde tam olabilir, ancak onu iyi toodouble-Azure AD Connect veritabanlarınızı yakın zamanda eşitlendi olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="fdde3-158">This step may already be complete on your tenant, but it's good toodouble-check that Azure AD Connect has synchronized your databases recently.</span></span>

1. <span data-ttu-id="fdde3-159">İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="fdde3-159">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="fdde3-160">Seçin **Azure Active Directory** > **Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="fdde3-160">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="fdde3-161">Eşitleme durumunuzu doğrulayın **etkin** ve son eşitleme değerinden bir saatten önce gerçekleştirildi.</span><span class="sxs-lookup"><span data-stu-id="fdde3-161">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="fdde3-162">Yeni gidiş eşitleme devre dışı tookick gerekiyorsa, bize yönergeleri hello [Azure AD Connect eşitleme: Zamanlayıcı](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span><span class="sxs-lookup"><span data-stu-id="fdde3-162">If you need tookick off a new round of synchronization, us hello instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="determine-which-authentication-methods-your-users-can-use"></a><span data-ttu-id="fdde3-163">Kullanıcılarınızın kullanabilirsiniz hangi kimlik doğrulama yöntemlerini belirleme</span><span class="sxs-lookup"><span data-stu-id="fdde3-163">Determine which authentication methods your users can use</span></span>

<span data-ttu-id="fdde3-164">NPS uzantısı dağıtımı ile hangi kimlik doğrulama yöntemleri kullanılabilir etkileyen iki Etkenler vardır:</span><span class="sxs-lookup"><span data-stu-id="fdde3-164">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span></span>

1. <span data-ttu-id="fdde3-165">Merhaba RADIUS istemcisi arasında kullanılan hello parola şifreleme algoritması (VPN, Netscaler sunucu veya diğer) ve hello NPS sunucuları.</span><span class="sxs-lookup"><span data-stu-id="fdde3-165">hello password encryption algorithm used between hello RADIUS client (VPN, Netscaler server, or other) and hello NPS servers.</span></span>
   - <span data-ttu-id="fdde3-166">**PAP** hello bulutta Azure mfa tüm hello kimlik doğrulama yöntemlerini destekler: telefon araması, tek yönlü SMS mesajı, mobil uygulama bildirimi ve mobil uygulama doğrulama kodu.</span><span class="sxs-lookup"><span data-stu-id="fdde3-166">**PAP** supports all hello authentication methods of Azure MFA in hello cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span></span>
   - <span data-ttu-id="fdde3-167">**CHAPV2** ve **EAP** telefon araması ve mobil uygulama bildirimi destekler.</span><span class="sxs-lookup"><span data-stu-id="fdde3-167">**CHAPV2** and **EAP** support phone call and mobile app notification.</span></span>
2. <span data-ttu-id="fdde3-168">Merhaba giriş istemci uygulaması hello yöntemler (VPN, Netscaler sunucu veya diğer) işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-168">hello input methods that hello client application (VPN, Netscaler server, or other) can handle.</span></span> <span data-ttu-id="fdde3-169">Örneğin, bazı araçlar hello VPN istemcisi sahip bir metin veya mobil uygulama doğrulama kodu tooallow hello kullanıcı tootype?</span><span class="sxs-lookup"><span data-stu-id="fdde3-169">For example, does hello VPN client have some means tooallow hello user tootype in a verification code from a text or mobile app?</span></span>

<span data-ttu-id="fdde3-170">Merhaba NPS uzantısı dağıtırken hangi yöntemler, kullanıcılarınız için kullanılabilir Bu etkenler tooevaluate kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-170">When you deploy hello NPS extension, use these factors tooevaluate which methods are available for your users.</span></span> <span data-ttu-id="fdde3-171">RADIUS istemciniz PAP destekler, ancak bir doğrulama kodu için girdi alanlarının hello istemci UX yok, ardından telefon araması ve mobil uygulama bildirimi hello iki desteklenen seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-171">If your RADIUS client supports PAP, but hello client UX doesn't have input fields for a verification code, then phone call and mobile app notification are hello two supported options.</span></span>

<span data-ttu-id="fdde3-172">Yapabilecekleriniz [desteklenmeyen kimlik doğrulama yöntemleri devre dışı](multi-factor-authentication-whats-next.md#selectable-verification-methods) azure'da.</span><span class="sxs-lookup"><span data-stu-id="fdde3-172">You can [disable unsupported authentication methods](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.</span></span>

### <a name="enable-users-for-mfa"></a><span data-ttu-id="fdde3-173">Kullanıcılar için MFA'yı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="fdde3-173">Enable users for MFA</span></span>

<span data-ttu-id="fdde3-174">Merhaba tam NPS uzantısını dağıtmadan önce tooperform iki aşamalı doğrulamayı istediğiniz hello kullanıcıları için tooenable MFA gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-174">Before you deploy hello full NPS extension, you need tooenable MFA for hello users that you want tooperform two-step verification.</span></span> <span data-ttu-id="fdde3-175">Daha fazla hemen tootest hello uzantısını dağıtmak, çok faktörlü kimlik doğrulaması için tam olarak kayıtlı en az bir sınama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-175">More immediately, tootest hello extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span>

<span data-ttu-id="fdde3-176">Bir test hesabı kullanmaya bu adımları tooget kullanın:</span><span class="sxs-lookup"><span data-stu-id="fdde3-176">Use these steps tooget a test account started:</span></span>
1. <span data-ttu-id="fdde3-177">Çok oturum[https://aka.ms/mfasetup](https://aka.ms/mfasetup) bir test hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="fdde3-177">Sign in too[https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span></span> 
2. <span data-ttu-id="fdde3-178">Merhaba istemleri tooset doğrulama yöntem izleyin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-178">Follow hello prompts tooset up a verification method.</span></span>
3. <span data-ttu-id="fdde3-179">Ya da bir koşullu erişim ilkesi oluşturun veya [hello kullanıcı durumunu değiştirme](multi-factor-authentication-get-started-user-states.md) hello sınama hesabı için iki aşamalı doğrulamayı toorequire.</span><span class="sxs-lookup"><span data-stu-id="fdde3-179">Either create a conditional access policy or [change hello user state](multi-factor-authentication-get-started-user-states.md) toorequire two-step verification for hello test account.</span></span> 

<span data-ttu-id="fdde3-180">Merhaba NPS uzantısı ile kimlik doğrulama gerçekleştirmeden önce kullanıcılarınızın toofollow bu adımları tooenroll da gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-180">Your users also need toofollow these steps tooenroll before they can authenticate with hello NPS extension.</span></span>

## <a name="install-hello-nps-extension"></a><span data-ttu-id="fdde3-181">Merhaba NPS uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="fdde3-181">Install hello NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdde3-182">Merhaba NPS uzantısı hello VPN erişim noktası başka bir sunucuya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-182">Install hello NPS extension on a different server than hello VPN access point.</span></span>

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a><span data-ttu-id="fdde3-183">Karşıdan yükleyip hello NPS uzantısı için Azure MFA</span><span class="sxs-lookup"><span data-stu-id="fdde3-183">Download and install hello NPS extension for Azure MFA</span></span>

1.  <span data-ttu-id="fdde3-184">[Merhaba NPS uzantısı karşıdan](https://aka.ms/npsmfa) hello Microsoft Download Center gelen.</span><span class="sxs-lookup"><span data-stu-id="fdde3-184">[Download hello NPS Extension](https://aka.ms/npsmfa) from hello Microsoft Download Center.</span></span>
2.  <span data-ttu-id="fdde3-185">Merhaba ikili toohello tooconfigure istediğiniz ağ ilkesi sunucusu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-185">Copy hello binary toohello Network Policy Server you want tooconfigure.</span></span>
3.  <span data-ttu-id="fdde3-186">Çalıştırma *setup.exe* ve hello yükleme yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-186">Run *setup.exe* and follow hello installation instructions.</span></span> <span data-ttu-id="fdde3-187">Hatalarla karşılaşırsanız, iki kitaplıkları hello önkoşul bölümünden başarıyla yüklenen, hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-187">If you encounter errors, double-check that hello two libraries from hello prerequisite section were successfully installed.</span></span>

### <a name="run-hello-powershell-script"></a><span data-ttu-id="fdde3-188">Merhaba PowerShell betiğini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="fdde3-188">Run hello PowerShell script</span></span>

<span data-ttu-id="fdde3-189">Hello yükleyici, bu konumda bir PowerShell Betiği oluşturur: `C:\Program Files\Microsoft\AzureMfa\Config` (C:\ olduğu yükleme sürücüsü).</span><span class="sxs-lookup"><span data-stu-id="fdde3-189">hello installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="fdde3-190">Bu PowerShell Betiği hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="fdde3-190">This PowerShell script performs hello following actions:</span></span>

-   <span data-ttu-id="fdde3-191">Kendinden imzalı bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdde3-191">Create a self-signed certificate.</span></span>
-   <span data-ttu-id="fdde3-192">Merhaba sertifika toohello hizmeti üzerinde Azure AD asıl ortak anahtarı Hello ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-192">Associate hello public key of hello certificate toohello service principal on Azure AD.</span></span>
-   <span data-ttu-id="fdde3-193">Merhaba cert hello yerel makine sertifika deposunda saklar.</span><span class="sxs-lookup"><span data-stu-id="fdde3-193">Store hello cert in hello local machine cert store.</span></span>
-   <span data-ttu-id="fdde3-194">GRANT erişim toohello sertifikanın özel anahtar tooNetwork kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="fdde3-194">Grant access toohello certificate’s private key tooNetwork User.</span></span>
-   <span data-ttu-id="fdde3-195">Merhaba NPS yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-195">Restart hello NPS.</span></span>

<span data-ttu-id="fdde3-196">Toouse kendi istediğiniz sürece (yerine PowerShell Betiği oluşturur hello hello otomatik olarak imzalanan sertifikalar), sertifikaları toocomplete hello yükleme hello PowerShell betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-196">Unless you want toouse your own certificates (instead of hello self-signed certificates that hello PowerShell script generates), run hello PowerShell Script toocomplete hello installation.</span></span> <span data-ttu-id="fdde3-197">Birden çok sunucu üzerinde hello uzantısı yüklerseniz, her biri kendi sertifikanın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-197">If you install hello extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="fdde3-198">Windows PowerShell'i yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-198">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="fdde3-199">Dizinleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-199">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="fdde3-200">Merhaba yükleyici tarafından oluşturulan hello PowerShell betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-200">Run hello PowerShell script created by hello installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="fdde3-201">Kiracı kimliğinizi PowerShell sorar</span><span class="sxs-lookup"><span data-stu-id="fdde3-201">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="fdde3-202">Merhaba hello hello Önkoşullar bölümüne Azure portalında kopyalanan dizin kimliği GUID kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-202">Use hello Directory ID GUID that you copied from hello Azure portal in hello prerequisites section.</span></span>
5. <span data-ttu-id="fdde3-203">TooAzure AD yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="fdde3-203">Sign in tooAzure AD as an administrator.</span></span>
6. <span data-ttu-id="fdde3-204">Merhaba betik tamamlandığında PowerShell bir başarı iletisi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-204">PowerShell shows a success message when hello script is finished.</span></span>  

<span data-ttu-id="fdde3-205">Yük Dengeleme için tooset istediğiniz ek herhangi NPS sunucularında bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-205">Repeat these steps on any additional NPS servers that you want tooset up for load balancing.</span></span>

>[!NOTE]
><span data-ttu-id="fdde3-206">Merhaba PowerShell Betiği sertifikalarla üretmek yerine kendi sertifikaları kullanıyorsanız, toohello NPS adlandırma kuralı Hizala emin olun.</span><span class="sxs-lookup"><span data-stu-id="fdde3-206">If you use your own certificates instead of generating certificates with hello PowerShell script, make sure that they align toohello NPS naming convention.</span></span> <span data-ttu-id="fdde3-207">Merhaba konu adı olmalıdır **CN =\<Tenantıd\>, OU = Microsoft NPS uzantı**.</span><span class="sxs-lookup"><span data-stu-id="fdde3-207">hello subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span></span> 

## <a name="configure-your-nps-extension"></a><span data-ttu-id="fdde3-208">NPS uzantınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fdde3-208">Configure your NPS extension</span></span>

<span data-ttu-id="fdde3-209">Bu bölümde, tasarım konuları ve başarılı NPS uzantısı dağıtımlar için öneriler içerir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-209">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configuration-limitations"></a><span data-ttu-id="fdde3-210">Yapılandırma sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="fdde3-210">Configuration limitations</span></span>

- <span data-ttu-id="fdde3-211">Hello Azure MFA için NPS uzantısı araçları toomigrate kullanıcılar ve MFA sunucusu toohello bulut ayarları içermez.</span><span class="sxs-lookup"><span data-stu-id="fdde3-211">hello NPS extension for Azure MFA does not include tools toomigrate users and settings from MFA Server toohello cloud.</span></span> <span data-ttu-id="fdde3-212">Bu nedenle, varolan dağıtım yerine yeni dağıtımlar için hello uzantısıyla öneririz.</span><span class="sxs-lookup"><span data-stu-id="fdde3-212">For this reason, we suggest using hello extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="fdde3-213">Üzerinde var olan bir dağıtıma hello uzantısı kullanırsanız, kullanıcılarınızın tooperform kanıtı li sahip toopopulate kendi MFA hello buluta yeniden ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="fdde3-213">If you use hello extension on an existing deployment, your users have tooperform proof-up again toopopulate their MFA details in hello cloud.</span></span>  
- <span data-ttu-id="fdde3-214">Merhaba gelen UPN hello ikincil yetkili hello uzantısı gerçekleştirmek için Active directory tooidentify hello kullanıcı Azure MFA üzerinde yapılandırılmış toouse alternatif oturum açma kimliği veya özel Active Directory gibi farklı bir tanımlayıcı olabilir şirket içi hello Hello NPS uzantısı kullanır alan UPN dışında.</span><span class="sxs-lookup"><span data-stu-id="fdde3-214">hello NPS extension uses hello UPN from hello on-premises Active directory tooidentify hello user on Azure MFA for performing hello Secondary Auth. hello extension can be configured toouse a different identifier like alternate login ID or custom Active Directory field other than UPN.</span></span> <span data-ttu-id="fdde3-215">Bkz: [Gelişmiş çok faktörlü kimlik doğrulaması için hello NPS uzantısı için yapılandırma seçenekleri](multi-factor-authentication-advanced-vpn-configurations.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fdde3-215">See [Advanced configuration options for hello NPS extension for Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) for more information.</span></span>
- <span data-ttu-id="fdde3-216">Tüm şifreleme protokolleri tüm doğrulama yöntemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fdde3-216">Not all encryption protocols support all verification methods.</span></span>
   - <span data-ttu-id="fdde3-217">**PAP** telefon araması, tek yönlü SMS mesajı, mobil uygulama bildirimi ve mobil uygulama doğrulama kodu destekler</span><span class="sxs-lookup"><span data-stu-id="fdde3-217">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span></span>
   - <span data-ttu-id="fdde3-218">**CHAPV2** ve **EAP** telefon araması ve mobil uygulama bildirimi desteği</span><span class="sxs-lookup"><span data-stu-id="fdde3-218">**CHAPV2** and **EAP** support phone call and mobile app notification</span></span>

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="fdde3-219">MFA gerektirecek denetim RADIUS istemcileri</span><span class="sxs-lookup"><span data-stu-id="fdde3-219">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="fdde3-220">MFA hello NPS uzantısını kullanarak bir RADIUS istemcisi için etkinleştirdikten sonra tüm kimlik doğrulamaları bu istemci için gerekli tooperform MFA ' dir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-220">Once you enable MFA for a RADIUS client using hello NPS Extension, all authentications for this client are required tooperform MFA.</span></span> <span data-ttu-id="fdde3-221">Bazı RADIUS istemcileri ve diğerleri için tooenable MFA isterseniz, iki NPS sunucularını yapılandırın ve yalnızca bir tanesine hello uzantısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fdde3-221">If you want tooenable MFA for some RADIUS clients but not others, you can configure two NPS servers and install hello extension on only one of them.</span></span> <span data-ttu-id="fdde3-222">Toorequire MFA toosend istekleri toohello NPS sunucusu hello uzantısıyla yapılandırılmış ve hello uzantısı ile yapılandırılmamış diğer RADIUS istemcileri toohello NPS sunucusu istediğiniz RADIUS istemcileri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdde3-222">Configure RADIUS clients that you want toorequire MFA toosend requests toohello NPS server configured with hello extension, and other RADIUS clients toohello NPS server not configured with hello extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="fdde3-223">MFA için kayıtlı olmayan kullanıcılar için hazırlama</span><span class="sxs-lookup"><span data-stu-id="fdde3-223">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="fdde3-224">MFA için kayıtlı olmayan kullanıcılar varsa, tooauthenticate çalıştıklarında ne olacağını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdde3-224">If you have users that aren't enrolled for MFA, you can determine what happens when they try tooauthenticate.</span></span> <span data-ttu-id="fdde3-225">Merhaba kayıt defteri ayarını kullanın *REQUIRE_USER_MATCH* hello kayıt defteri yolunda *HKLM\Software\Microsoft\AzureMFA* toocontrol hello özelliği davranışı.</span><span class="sxs-lookup"><span data-stu-id="fdde3-225">Use hello registry setting *REQUIRE_USER_MATCH* in hello registry path *HKLM\Software\Microsoft\AzureMFA* toocontrol hello feature behavior.</span></span> <span data-ttu-id="fdde3-226">Bu ayar tek yapılandırma seçeneği vardır:</span><span class="sxs-lookup"><span data-stu-id="fdde3-226">This setting has a single configuration option:</span></span>

| <span data-ttu-id="fdde3-227">Anahtar</span><span class="sxs-lookup"><span data-stu-id="fdde3-227">Key</span></span> | <span data-ttu-id="fdde3-228">Değer</span><span class="sxs-lookup"><span data-stu-id="fdde3-228">Value</span></span> | <span data-ttu-id="fdde3-229">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="fdde3-229">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="fdde3-230">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="fdde3-230">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="fdde3-231">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="fdde3-231">TRUE/FALSE</span></span> | <span data-ttu-id="fdde3-232">(Eşdeğer tooTRUE) ayarlı değil</span><span class="sxs-lookup"><span data-stu-id="fdde3-232">Not set (equivalent tooTRUE)</span></span> |

<span data-ttu-id="fdde3-233">Bu ayarın amacı Hello toodetermine kullanıcı MFA'ya kayıtlı olmayan hangi toodo durumdur.</span><span class="sxs-lookup"><span data-stu-id="fdde3-233">hello purpose of this setting is toodetermine what toodo when a user is not enrolled for MFA.</span></span> <span data-ttu-id="fdde3-234">Ne zaman hello anahtarı yok, ayarlanmadı veya tooTRUE, ayarlayın ve hello kullanıcı kayıtlı olmayan, ardından hello uzantısı hello MFA sınama başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fdde3-234">When hello key does not exist, is not set, or is set tooTRUE, and hello user is not enrolled, then hello extension fails hello MFA challenge.</span></span> <span data-ttu-id="fdde3-235">Merhaba anahtar tooFALSE ayarlanır ve hello kullanıcı kayıtlı olmayan kimlik doğrulaması MFA yapmadan devam eder.</span><span class="sxs-lookup"><span data-stu-id="fdde3-235">When hello key is set tooFALSE and hello user is not enrolled, authentication proceeds without performing MFA.</span></span>

<span data-ttu-id="fdde3-236">Bu anahtar toocreate seçin ve kullanıcılarınızın ekleme olduğu ve tüm henüz Azure MFA için kaydedilebilir zaman tooFALSE ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-236">You can choose toocreate this key and set it tooFALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span></span> <span data-ttu-id="fdde3-237">Ancak, ayarı hello anahtar MFA toosign için kayıtlı olmayan kullanıcılar verdiğinden, devam eden tooproduction önce bu anahtar kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdde3-237">However, since setting hello key permits users that aren't enrolled for MFA toosign in, you should remove this key before going tooproduction.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fdde3-238">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fdde3-238">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a><span data-ttu-id="fdde3-239">Bu hello istemci sertifikası beklendiği gibi yüklü nasıl doğrularım?</span><span class="sxs-lookup"><span data-stu-id="fdde3-239">How do I verify that hello client cert is installed as expected?</span></span>

<span data-ttu-id="fdde3-240">Merhaba otomatik olarak imzalanan sertifika hello sertifika deposu ve özel anahtarı hello onay hello yükleyici tarafından oluşturulan toouser izinler için Ara **ağ hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="fdde3-240">Look for hello self-signed certificate created by hello installer in hello cert store, and check that hello private key has permissions granted toouser **NETWORK SERVICE**.</span></span> <span data-ttu-id="fdde3-241">Merhaba cert sahip bir konu adı **CN \<tenantıd\>, OU = Microsoft NPS uzantı**</span><span class="sxs-lookup"><span data-stu-id="fdde3-241">hello cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a><span data-ttu-id="fdde3-242">My istemci sertifikası ilişkili toomy Kiracı Azure Active Directory'de olup olmadığını nasıl doğrulayabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="fdde3-242">How can I verify that my client cert is associated toomy tenant in Azure Active Directory?</span></span>

<span data-ttu-id="fdde3-243">PowerShell komut istemi ve aşağıdaki komutları çalıştırma hello açın:</span><span class="sxs-lookup"><span data-stu-id="fdde3-243">Open PowerShell command prompt and run hello following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="fdde3-244">Bu komutlar, Kiracı hello NPS uzantısı örneğinizle PowerShell oturumunuzda ilişkilendirme tüm hello sertifikaları yazdırın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-244">These commands print all hello certificates associating your tenant with your instance of hello NPS extension in your PowerShell session.</span></span> <span data-ttu-id="fdde3-245">Sertifikanız için istemci sertifikası hello özel anahtarı olmayan bir "X.509(.cer) Base-64 Kodlamalı" dosyası olarak dışa aktararak arayın ve PowerShell hello listeden ile karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="fdde3-245">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without hello private key, and compare it with hello list from PowerShell.</span></span>

<span data-ttu-id="fdde3-246">Geçerli-başlangıç ve geçerli-hello komut birden fazla sertifika döndürürse okunabilir formda bulunan, zaman damgaları belirgin misfits çıkışı kullanılan toofilter kadar.</span><span class="sxs-lookup"><span data-stu-id="fdde3-246">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used toofilter out obvious misfits if hello command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="fdde3-247">Neden isteklerim ADAL belirteci hatasıyla başarısız oluyor?</span><span class="sxs-lookup"><span data-stu-id="fdde3-247">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="fdde3-248">Bu hata kaynaklanabilir çeşitli nedenlerle tooone.</span><span class="sxs-lookup"><span data-stu-id="fdde3-248">This error could be due tooone of several reasons.</span></span> <span data-ttu-id="fdde3-249">Toohelp sorun giderme adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="fdde3-249">Use these steps toohelp troubleshoot:</span></span>

1. <span data-ttu-id="fdde3-250">NPS sunucusunu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-250">Restart your NPS server.</span></span>
2. <span data-ttu-id="fdde3-251">Bu istemci sertifikası beklendiği gibi yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-251">Verify that that client cert is installed as expected.</span></span>
3. <span data-ttu-id="fdde3-252">Bu hello sertifika üzerinde Azure AD Kiracı ile ilişkili olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-252">Verify that hello certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="fdde3-253">Bu https://login.microsoftonline.com/ hello uzantısı'nı çalıştıran hello sunucusundan erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fdde3-253">Verify that https://login.microsoftonline.com/ is accessible from hello server running hello extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a><span data-ttu-id="fdde3-254">Neden kimlik doğrulaması, HTTP günlükleri hello kullanıcı bulunamadı bildiren bir hata ile başarısız?</span><span class="sxs-lookup"><span data-stu-id="fdde3-254">Why does authentication fail with an error in HTTP logs stating that hello user is not found?</span></span>

<span data-ttu-id="fdde3-255">AD Connect çalıştıran ve hello kullanıcının Windows Active Directory ve Azure Active Directory içinde mevcut olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fdde3-255">Verify that AD Connect is running, and that hello user is present in both Windows Active Directory and Azure Active Directory.</span></span>

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="fdde3-256">HTTP hataları günlüklerinde başarısız olan tüm my kimlik doğrulamaları ile bağlanmak neden görüyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="fdde3-256">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="fdde3-257">Bu https://adnotifications.windowsazure.com hello NPS uzantısı'nı çalıştıran hello sunucudan erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fdde3-257">Verify that https://adnotifications.windowsazure.com is reachable from hello server running hello NPS extension.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fdde3-258">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fdde3-258">Next steps</span></span>

- <span data-ttu-id="fdde3-259">İki aşamalı doğrulamayı gerçekleştirmek döndürmemelidir IP'ler için bir özel durum listesi ayarlamak veya alternatif kimlikleri oturum açma için yapılandırma [Gelişmiş çok faktörlü kimlik doğrulaması için hello NPS uzantısı için yapılandırma seçenekleri](nps-extension-advanced-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="fdde3-259">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for hello NPS extension for Multi-Factor Authentication](nps-extension-advanced-configuration.md)</span></span>

- [<span data-ttu-id="fdde3-260">Azure çok faktörlü kimlik doğrulamasını hello NPS uzantısı hata iletilerini çözümleyin</span><span class="sxs-lookup"><span data-stu-id="fdde3-260">Resolve error messages from hello NPS extension for Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-nps-errors.md)
