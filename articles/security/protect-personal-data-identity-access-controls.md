---
title: "Azure kimlik ve erişim denetimleri ile kişisel veriler aaaProtect | Microsoft Docs"
description: "Azure kimlik ve erişim denetimleri toohelp kullanarak kişisel verilerinizi koruyun"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="c614d-103">Azure Active Directory ve çok faktörlü kimlik doğrulaması: kimlik ve erişim denetimleri ile kişisel verileri koruma</span><span class="sxs-lookup"><span data-stu-id="c614d-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="c614d-104">Bu makalede bilgi ve Azure Active Directory ve çok faktörlü kimlik doğrulama güvenlik özellikleri ve Hizmetleri kullanarak tooprotect kişisel verileri kullanabileceğiniz yordamlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="c614d-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="c614d-105">Senaryo</span><span class="sxs-lookup"><span data-stu-id="c614d-105">Scenario</span></span>

<span data-ttu-id="c614d-106">Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="c614d-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="c614d-107">toosupport bu çaba İtalya, dayanarak birkaç küçük seyahat satırları geçirmiş Almanya, Danimarka ve hello İngiltere</span><span class="sxs-lookup"><span data-stu-id="c614d-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="c614d-108">Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c614d-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="c614d-109">Bu ad, adres, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı, kredi kartı bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c614d-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="c614d-110">Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="c614d-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="c614d-111">Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.</span><span class="sxs-lookup"><span data-stu-id="c614d-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="c614d-112">Şirket çalışanları erişim hello ağdan hello şirketin şubelere ve seyahat aracılar bulunan Merhaba Dünya toosome şirket kaynaklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="c614d-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="c614d-113">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="c614d-113">Problem statement</span></span>

<span data-ttu-id="c614d-114">Merhaba şirket müşterilerin ve çalışanların kişisel verilerin hello gizliliği tehlikeye toouse kimlikleri toogain erişim aramayı saldırganlardan korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c614d-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="c614d-115">Bunlar ayrıca veri yasal kullanıcılar tarafından yalnızca toodo ihtiyacınız olan olanlar için sınırlı bu erişim toopersonal işlerini emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="c614d-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="c614d-116">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="c614d-116">Company goal</span></span>

<span data-ttu-id="c614d-117">Merhaba şirketin toopersonal veri erişim tooensure kesinlikle denetlenir hedeftir.</span><span class="sxs-lookup"><span data-stu-id="c614d-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="c614d-118">Erişim toopersonal veri ile kullanıcıların kimliklerini güçlü kimlik doğrulamasıyla korunması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="c614d-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="c614d-119">Bir ilke [en az ayrıcalık] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) gerekir zorunlu böylece yasal kullanıcıların ihtiyaç duydukları erişim ve artık yalnızca hello düzeyi.</span><span class="sxs-lookup"><span data-stu-id="c614d-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="c614d-120">Çözümler</span><span class="sxs-lookup"><span data-stu-id="c614d-120">Solutions</span></span>

<span data-ttu-id="c614d-121">Microsoft Azure kimlik ve erişim yönetimi araçları kişisel verileri içeren erişim tooresources sahip toohelp şirketler denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c614d-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="c614d-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c614d-122">Azure Active Directory</span></span>

<span data-ttu-id="c614d-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) kimlikleri yönetir ve sair şirket içi ve diğer bulut kaynakları, veri ve uygulamaları tooAzure erişimi kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="c614d-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="c614d-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) Azure Yöneticiler toominimize hello kişisel verileri gibi erişim toocertain bilgileri olan kişiler sayısı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c614d-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="c614d-125">Bu toodiscover sağlar, kısıtlamak ve ayrıcalıklı kimliklerinizi ve bunların erişim tooresources tooassign geçici, Just-In-Time (JIT) yönetici hakları tooeligible kullanıcıların ve izleme.</span><span class="sxs-lookup"><span data-stu-id="c614d-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="c614d-126">Ayrıca, kullanıcılar AAD yönetici ayrıcalıklarına sahip bir anlayış sağlar.</span><span class="sxs-lookup"><span data-stu-id="c614d-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="c614d-127">AAD PIM kullanarak söz konusu Hello etkinlikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c614d-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="c614d-128">Privileged Identity Management dizininiz için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c614d-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="c614d-129">Privileged Identity Management Yönetim Panosu toosee önemli bilgileri bir bakışta kullanma</span><span class="sxs-lookup"><span data-stu-id="c614d-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="c614d-130">Merhaba ayrıcalıklı kimlikleri (Yöneticiler) ekleyerek veya kaldırarak kalıcı veya uygun Yöneticiler tooeach rolünü yönetme</span><span class="sxs-lookup"><span data-stu-id="c614d-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="c614d-131">Merhaba rol etkinleştirme ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c614d-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="c614d-132">Rol etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c614d-132">Activating roles</span></span>

- <span data-ttu-id="c614d-133">Rol etkinliği gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="c614d-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="c614d-134">AAD PIM nasıl etkinleştirebilirim?</span><span class="sxs-lookup"><span data-stu-id="c614d-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="c614d-135">PIM dizininiz için kullanarak toostart aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="c614d-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="c614d-136">Toohello Azure portal dizininizin genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c614d-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="c614d-137">Kuruluşunuz birden fazla dizine sahipse, kullanıcı adınızı hello sağ üst köşesinde hello Azure portalı içinde seçin.</span><span class="sxs-lookup"><span data-stu-id="c614d-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="c614d-138">Burada, Azure AD Privileged Identity Management kullanacağınız hello dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="c614d-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="c614d-139">Seçin **daha fazla hizmet** ve hello **filtre** textbox toosearch Azure AD Privileged Identity Management için.</span><span class="sxs-lookup"><span data-stu-id="c614d-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="c614d-140">Denetleme **PIN toodashboard** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c614d-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="c614d-141">Merhaba Privileged Identity Management uygulaması açılır.</span><span class="sxs-lookup"><span data-stu-id="c614d-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="c614d-142">Azure AD Privileged Identity Management ayarladıktan sonra hello uygulamayı her açtığınızda hello Gezinti dikey penceresine bakın.</span><span class="sxs-lookup"><span data-stu-id="c614d-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="c614d-143">Daha fazla bilgi ve AAD PIM ile çalışmaya başlama hakkında yönergeler için bkz: [Başlat kullanarak Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="c614d-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="c614d-144">Azure rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="c614d-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="c614d-145">[Azure rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) tooAzure kaynaklarına erişim hello hello kullanıcının atanan rolüne dayalı erişim verme etkinleştirerek Azure yönetmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c614d-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="c614d-146">Ekip içinde görevlerini kurabilmeleri ve erişim toousers, grupları ve tooperform işlerini gereken uygulamalar, yalnızca hello miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c614d-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="c614d-147">Rol tabanlı erişim toousers hello Azure portal, Azure komut satırı araçları ve Azure Management API'leri kullanılarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="c614d-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="c614d-148">Azure RBAC temel kavramları hakkında daha fazla bilgi için bkz: [hello Azure Portal'ın rol tabanlı erişim denetimi kullanmaya başlayın.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="c614d-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="c614d-149">PowerShell ile Azure RBAC nasıl yönetebilirim?</span><span class="sxs-lookup"><span data-stu-id="c614d-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="c614d-150">PowerShell cmdlet'leri toomanage Azure RBAC, yönetim görevleri aşağıdaki hello dahil olmak üzere kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c614d-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="c614d-151">Liste rolleri</span><span class="sxs-lookup"><span data-stu-id="c614d-151">List roles</span></span>

- <span data-ttu-id="c614d-152">Kimlerin erişebileceğini bakın</span><span class="sxs-lookup"><span data-stu-id="c614d-152">See who has access</span></span>

- <span data-ttu-id="c614d-153">Erişim verme</span><span class="sxs-lookup"><span data-stu-id="c614d-153">Grant access</span></span>

- <span data-ttu-id="c614d-154">Erişimi kaldırma</span><span class="sxs-lookup"><span data-stu-id="c614d-154">Remove access</span></span>

- <span data-ttu-id="c614d-155">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="c614d-155">Create a custom role</span></span>

- <span data-ttu-id="c614d-156">Bir kaynak sağlayıcısı için Eylemler Al</span><span class="sxs-lookup"><span data-stu-id="c614d-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="c614d-157">Özel bir rol değiştirme</span><span class="sxs-lookup"><span data-stu-id="c614d-157">Modify a custom role</span></span>

- <span data-ttu-id="c614d-158">Bir özel rolü silmeyi</span><span class="sxs-lookup"><span data-stu-id="c614d-158">Delete a custom role</span></span>

- <span data-ttu-id="c614d-159">Liste özel roller</span><span class="sxs-lookup"><span data-stu-id="c614d-159">List custom roles</span></span>

<span data-ttu-id="c614d-160">Yönergeler için nasıl toomanage PowerShell ile Azure RBAC bkz [yönetmek rol tabanlı erişim Azure PowerShell ile](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="c614d-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="c614d-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c614d-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="c614d-162">[Azure çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA), koruma erişim toodata ve uygulamalar, basit bir oturum açma işlemi için kullanıcı talebine buluştururken yardımcı olan iki aşamalı doğrulama çözüm.</span><span class="sxs-lookup"><span data-stu-id="c614d-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="c614d-163">Bir dizi doğrulama yöntemi (ör. telefon çağrısı, metin mesajı veya mobil uygulama doğrulaması) aracılığıyla güçlü kimlik doğrulaması sunar.</span><span class="sxs-lookup"><span data-stu-id="c614d-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="c614d-164">MFA toodeploy hello Azure bulut içinde toofirst ihtiyacınız etkinleştirmek ve kullanıcılar için iki aşamalı doğrulamayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c614d-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="c614d-165">Azure toouse MFA nasıl etkinleştirebilirim?</span><span class="sxs-lookup"><span data-stu-id="c614d-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="c614d-166">Kullanıcılarınızın Azure çok faktörlü kimlik doğrulamasını içeren lisansına sahipseniz, hiçbir şey Azure MFA üzerinde toodo tooturn gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="c614d-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="c614d-167">Yoksa, dizininizde toocreate multi-Factor Auth sağlayıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c614d-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="c614d-168">toodo Bu, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c614d-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="c614d-169">Seçin **Active Directory** hello (yönetici olarak oturum açmış) Klasik Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="c614d-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="c614d-170">Seçin **çok faktörlü kimlik doğrulama sağlayıcıları.**</span><span class="sxs-lookup"><span data-stu-id="c614d-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="c614d-171">Seçin **yeni** altında ve **uygulama hizmetleri,** seçin **multi-Factor Auth sağlayıcısı.**</span><span class="sxs-lookup"><span data-stu-id="c614d-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="c614d-172">Seçin **hızlı oluştur.**</span><span class="sxs-lookup"><span data-stu-id="c614d-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="c614d-173">Merhaba ad alanını doldurun ve kullanım modeli (kimlik doğrulaması veya etkin kullanıcı başına) seçin.</span><span class="sxs-lookup"><span data-stu-id="c614d-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="c614d-174">MFA sağlayıcısı hangi hello ile ilişkili bir dizin belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c614d-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="c614d-175">Merhaba tıklatın **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c614d-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="c614d-176">Hakkında daha fazla yönerge için toomanage, çok faktörlü yetki sağlayıcı bkz [Azure multi-Factor Auth sağlayıcısı ile çalışmaya başlama.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="c614d-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="c614d-177">Kullanıcılar için iki aşamalı doğrulamayı nasıl kapatırım?</span><span class="sxs-lookup"><span data-stu-id="c614d-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="c614d-178">Tüm oturum açma işlemleri için iki aşamalı doğrulama zorunlu kılabilir veya yalnızca belirli koşullar geçerli olduğunda, koşullu erişim ilkeleri toorequire iki aşamalı doğrulamayı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c614d-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="c614d-179">Azure MFA kullanıcı durumları değiştirerek etkinleştirme iki aşamalı doğrulama gerektirme hello geleneksel bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="c614d-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="c614d-180">Etkinleştirmeniz tüm hello kullanıcıların gerekir oturum her zaman aynı gereksinim tooperform iki aşamalı doğrulamayı hello.</span><span class="sxs-lookup"><span data-stu-id="c614d-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="c614d-181">Bir kullanıcının kullanıcı etkileyebilecek herhangi bir koşullu erişim ilkeleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="c614d-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="c614d-182">Koşullu erişim ilkesi ile Azure MFA'yı etkinleştirerek, iki aşamalı doğrulama gerektirme daha esnek bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="c614d-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="c614d-183">Tek tek kullanıcılar yanı sıra toogroups uygulamak koşullu erişim ilkeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c614d-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="c614d-184">Daha fazla kısıtlama düşük riskli grupları daha yüksek riskli grupları verilebilir veya iki aşamalı doğrulamayı yalnızca yüksek riskli bulut uygulamaları için gereklidir ve düşük riskli için olanları atlandı.</span><span class="sxs-lookup"><span data-stu-id="c614d-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="c614d-185">Ancak, koşullu erişim Azure Active Directory, ücretli bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="c614d-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="c614d-186">kullanıcı durumunu değiştirerek MFA tooenable hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="c614d-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="c614d-187">İçinde toohello Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c614d-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="c614d-188">Çok Git**Azure Active Directory \> kullanıcılar ve gruplar \> tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c614d-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="c614d-189">Seçin **çok faktörlü kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="c614d-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="c614d-190">Azure MFA için tooenable istediğiniz Bul hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c614d-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="c614d-191">Toochange gerekebilir hello hello üstünde görüntüle.</span><span class="sxs-lookup"><span data-stu-id="c614d-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="c614d-192">Merhaba kutusunu sonraki toohello kullanıcının adını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="c614d-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="c614d-193">Hızlı adımlar altında sağ Hello üzerinde seçin **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="c614d-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="c614d-194">Açılır hello açılır pencerede Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c614d-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="c614d-195">MFA kendisi için etkinleştirilmiş kullanıcılar oturum açtığında tooregister hello istenir.</span><span class="sxs-lookup"><span data-stu-id="c614d-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="c614d-196">bir koşullu erişim ilkesi ile Azure MFA tooenable hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="c614d-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="c614d-197">İçinde toohello Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c614d-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="c614d-198">Çok Git**Azure Active Directory \> koşullu erişim**.</span><span class="sxs-lookup"><span data-stu-id="c614d-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="c614d-199">Seçin **yeni ilke**.</span><span class="sxs-lookup"><span data-stu-id="c614d-199">Select **New policy**.</span></span>

4. <span data-ttu-id="c614d-200">Altında **atamaları**seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c614d-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="c614d-201">Kullanım hello **INCLUDE** ve **hariç** hangi kullanıcıların ve grupların hello İlkesi tarafından yönetilecek toospecify sekmeler.</span><span class="sxs-lookup"><span data-stu-id="c614d-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="c614d-202">Altında **atamaları**seçin **bulut uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="c614d-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="c614d-203">Çok seçin**tüm bulut uygulamaları dahil**.</span><span class="sxs-lookup"><span data-stu-id="c614d-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="c614d-204">Altında **erişim denetimleri**seçin **Grant**.</span><span class="sxs-lookup"><span data-stu-id="c614d-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="c614d-205">Seçin **çok faktörlü kimlik doğrulaması gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="c614d-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="c614d-206">Kapatma **ilkesini etkinleştir** çok**üzerinde** ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c614d-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="c614d-207">Hakkında bilgi için bir kerelik geçiş tooconfigure Azure MFA ayarları tooset sahtekarlık uyarısı yukarı oluşturmak nasıl özel sesli mesajları kullanın, önbelleğe alınmasını yapılandırmak, güvenilen IP'leri belirtin, uygulama parolaları oluşturma, kullanıcıların güven cihazlar ve select için MFA hatırlama etkinleştir doğrulama yöntemlerini görmek [Azure çok faktörlü kimlik doğrulama ayarlarını yapılandırın.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="c614d-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c614d-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c614d-208">Next steps</span></span>

- [<span data-ttu-id="c614d-209">Azure AD'de ayrıcalıklı erişimi güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="c614d-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="c614d-210">Azure Multi-Factor Authentication hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="c614d-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="c614d-211">Rol tabanlı erişim denetimi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c614d-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="c614d-212">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="c614d-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
