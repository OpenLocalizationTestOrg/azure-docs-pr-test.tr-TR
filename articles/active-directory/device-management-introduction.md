---
title: "Azure Active Directory'de aaaIntroduction toodevice Yönetimi | Microsoft Docs"
description: "Nasıl aygıt yönetimi, ortamınızdaki kaynakları erişen hello aygıtları üzerinde tooget denetim yardımcı olabileceğini öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="52018-103">Azure Active Directory'de giriş toodevice Yönetimi</span><span class="sxs-lookup"><span data-stu-id="52018-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="52018-104">Bir mobil ilk olarak, bulut ilk dünyada tek oturum açma toodevices, uygulama ve hizmetlere her yerden Azure Active Directory (Azure AD) sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="52018-105">Kendi cihazını getir (KCG), aygıtlar - Hello artışı ile BT uzmanları iki rakip hedefle karşılaştığı:</span><span class="sxs-lookup"><span data-stu-id="52018-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="52018-106">Merhaba son kullanıcıların toobe üretken yerde ve zamanda güç kazandırma</span><span class="sxs-lookup"><span data-stu-id="52018-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="52018-107">Herhangi bir zamanda Hello şirket varlıklarını koruma</span><span class="sxs-lookup"><span data-stu-id="52018-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="52018-108">Aygıtlar, kullanıcılarınızın tooyour Kurumsal varlıklar erişim sağlama.</span><span class="sxs-lookup"><span data-stu-id="52018-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="52018-109">tooprotect şirket varlıklarınızı bir BT yöneticisi olarak, bu aygıtlar üzerinde toohave denetimine istiyor.</span><span class="sxs-lookup"><span data-stu-id="52018-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="52018-110">Bu, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="52018-111">Cihaz yönetimi, ayrıca hello temeli [cihaz temelli koşullu erişim](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="52018-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="52018-112">Cihaz temelli koşullu erişim ile ortamınızdaki tooresources yalnızca ile mümkündür erişim cihazlar güvenilen emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="52018-113">Bu konuda, Azure Active Directory içindeki aygıt yönetimi nasıl çalıştığı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="52018-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="52018-114">Azure ad hello denetimindeki aygıtları alma</span><span class="sxs-lookup"><span data-stu-id="52018-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="52018-115">Azure ad hello denetimindeki bir aygıtı tooget, iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="52018-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="52018-116">Kaydetme</span><span class="sxs-lookup"><span data-stu-id="52018-116">Registering</span></span> 
- <span data-ttu-id="52018-117">Birleştirme</span><span class="sxs-lookup"><span data-stu-id="52018-117">Joining</span></span>

<span data-ttu-id="52018-118">**Kaydetme** aygıt tooAzure AD, toomanage bir cihazın kimliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="52018-119">Bir cihaz kaydedildiğinde Azure AD cihaz kaydı hello kullanılan tooauthenticate hello aygıt bir kullanıcı oturum açtığında tooAzure olduğunda AD olan kimliğe sahip cihazı sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="52018-120">Merhaba kimlik tooenable kullanın veya bir aygıtı devre dışı.</span><span class="sxs-lookup"><span data-stu-id="52018-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="52018-121">Microsoft Intune gibi bir mobil cihaz birleştirildiğinde çözüm ile birlikte kullanıldığında, Azure AD'de hello cihaz öznitelikleri hello cihaz hakkındaki ek bilgilerle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="52018-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="52018-122">Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="52018-123">Microsoft Intune kaydolan cihazlar hakkında daha fazla bilgi için Yönetim için ıntune'a kaydetme aygıtları bakın.</span><span class="sxs-lookup"><span data-stu-id="52018-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="52018-124">**Birleştirme** uzantısı tooregistering bir aygıtı aygıttır.</span><span class="sxs-lookup"><span data-stu-id="52018-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="52018-125">Bunun anlamı tüm hello avantajları bir cihaz kaydetme ve ayrıca toothis sağlar, ayrıca hello yerel bir cihazın durumunu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="52018-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="52018-126">Merhaba yerel durumunu değiştirme kişisel hesabı yerine bir kuruluş iş veya Okul hesabını kullanarak kullanıcılar toosign bileşenini tooa Cihazınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="52018-127">Azure AD kayıtlı cihazları</span><span class="sxs-lookup"><span data-stu-id="52018-127">Azure AD registered devices</span></span>   

<span data-ttu-id="52018-128">Hello Azure AD kayıtlı cihazlar ile desteklediğiniz Merhaba tooprovide hedefidir **kendi cihazını getir (KCG)** senaryo.</span><span class="sxs-lookup"><span data-stu-id="52018-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="52018-129">Bu senaryoda, bir kullanıcı kişisel bir cihazı kullanarak, kuruluşunuzun Azure Active Directory denetlenen kaynaklarına erişebilir.</span><span class="sxs-lookup"><span data-stu-id="52018-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Azure AD kayıtlı cihazları](./media/device-management-introduction/03.png)

<span data-ttu-id="52018-131">Merhaba erişim hello aygıtta girilen bir iş veya Okul hesabı temel alır.</span><span class="sxs-lookup"><span data-stu-id="52018-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="52018-132">Örneğin, Windows 10 iş veya Okul hesabı tooa kişisel bilgisayar, tablet veya telefon kullanıcıları tooadd sağlar.</span><span class="sxs-lookup"><span data-stu-id="52018-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="52018-133">Ne zaman bir kullanıcı eklenmiş bir iş veya Okul hesabı, hello aygıt Azure AD ile kayıtlı ve isteğe bağlı olarak, kuruluşunuz yapılandırılmış hello mobil cihaz Yönetimi (MDM) sisteminde kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="52018-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="52018-134">Kuruluşunuzdaki kullanıcılar bir iş ekleyebilir veya hesap tooa kişisel cihaz rahat Okul:</span><span class="sxs-lookup"><span data-stu-id="52018-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="52018-135">Bir iş uygulaması ilk kez hello için erişirken</span><span class="sxs-lookup"><span data-stu-id="52018-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="52018-136">Hello kullanarak el ile **ayarları** Windows 10 hello durumda menüsü</span><span class="sxs-lookup"><span data-stu-id="52018-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="52018-137">Azure AD kayıtlı cihazlara Windows 10, iOS, Android ve macOS için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="52018-138">Azure AD alanına katılmış aygıtlar</span><span class="sxs-lookup"><span data-stu-id="52018-138">Azure AD joined devices</span></span>

<span data-ttu-id="52018-139">Azure AD alanına katılmış aygıtlar Hello amacı toosimplify şöyledir:</span><span class="sxs-lookup"><span data-stu-id="52018-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="52018-140">Windows dağıtımları iş ait cihazlar</span><span class="sxs-lookup"><span data-stu-id="52018-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="52018-141">Erişim tooorganizational uygulamaları ve herhangi bir Windows aygıtı kaynaklardan</span><span class="sxs-lookup"><span data-stu-id="52018-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Azure AD kayıtlı cihazları](./media/device-management-introduction/02.png)


<span data-ttu-id="52018-143">Azure ad hello denetiminde çalışma şirkete ait cihazları almak için kullanıcılarınızın bir Self Servis deneyimi sağlayarak bu hedefleri gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="52018-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="52018-144">**Azure AD birleştirme** bulut ilk / salt bulut olan kuruluşlar için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="52018-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="52018-145">Bir şirket içi Windows Server Active Directory altyapısına sahip olmayan küçük ve orta ölçekli işletmeler genellikle şunlardır.</span><span class="sxs-lookup"><span data-stu-id="52018-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="52018-146">Azure AD alanına katılmış aygıtlar uygulama ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="52018-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="52018-147">**Çoklu oturum açma (SSO)** tooyour Azure yönetilen SaaS uygulamaları ve Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="52018-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="52018-148">Kullanıcılarınızın, iş kaynaklarına erişirken ek kimlik doğrulama istekleri görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="52018-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="52018-149">Merhaba SSO işlevlerini bağlı toohello etki alanı ağında kullanılabilir değil olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="52018-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="52018-150">**Kurumsal uyumlu gezici** alanına katılmış aygıtlar arasındaki kullanıcı ayarlarının.</span><span class="sxs-lookup"><span data-stu-id="52018-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="52018-151">Kullanıcılar, cihazlar arasında bir Microsoft hesabı (örneğin, Hotmail) toosee ayarları tooconnect ihtiyacınız yoktur.</span><span class="sxs-lookup"><span data-stu-id="52018-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="52018-152">**İş için erişim tooWindows mağazası** AD hesabı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="52018-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="52018-153">Kullanıcılarınızın hello kuruluş tarafından önceden seçilmiş uygulamalarının stoğunu arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="52018-154">**Windows Hello** toowork kaynaklarına güvenli ve kolay erişim için destek.</span><span class="sxs-lookup"><span data-stu-id="52018-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="52018-155">**Erişim kısıtlama** uyumluluk ilkesine uygun aygıtlardan tooapps.</span><span class="sxs-lookup"><span data-stu-id="52018-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="52018-156">Azure AD birleştirme öncelikle bir şirket içi Windows Server Active Directory altyapısına sahip olmayan kuruluşlar için tasarlanmıştır ancak kesinlikle yapabilecekleriniz senaryolarda de burada:</span><span class="sxs-lookup"><span data-stu-id="52018-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="52018-157">Tabletler ve telefonlardan denetimindeki gibi mobil cihazları tooget ihtiyacınız varsa, örneğin, bir şirket içi etki alanına katılma kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="52018-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="52018-158">Kullanıcılarınızın öncelikle tooaccess Office 365 veya Azure AD ile tümleşik diğer SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="52018-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="52018-159">Active Directory yerine Azure AD'de toomanage bir kullanıcı grubuna istiyor.</span><span class="sxs-lookup"><span data-stu-id="52018-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="52018-160">Bu, örneğin, tooseasonal çalışanları, Yükleniciler veya Öğrenciler uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="52018-161">Tooprovide katılma yetenekleri tooworkers sınırlı şirket içi altyapı ile uzak şube ofislerinde istiyor.</span><span class="sxs-lookup"><span data-stu-id="52018-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="52018-162">Windows 10 cihazlar için Azure AD alanına katılmış cihazları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="52018-163">Karma Azure AD alanına katılmış aygıtlar</span><span class="sxs-lookup"><span data-stu-id="52018-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="52018-164">Birden fazla bir süredir birçok kuruluş hello etki alanına katılma tootheir şirket içi Active Directory tooenable kullanmıştır:</span><span class="sxs-lookup"><span data-stu-id="52018-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="52018-165">BT departmanları toomanage iş şirkete ait cihazları merkezi bir konumdan.</span><span class="sxs-lookup"><span data-stu-id="52018-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="52018-166">Kullanıcıların toosign tootheir aygıtları kendi Active Directory ile iş veya Okul hesapları.</span><span class="sxs-lookup"><span data-stu-id="52018-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="52018-167">Genellikle, bir şirket içi ayak izini kuruluşlarla kullanan görüntüleme yöntemleri tooprovision aygıtları ve sık kullandıkları **System Center Configuration Manager (SCCM)** veya **Grup İlkesi (GP)** toomanage bunları.</span><span class="sxs-lookup"><span data-stu-id="52018-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="52018-168">Şirket içi ortamınız varsa, AD alanını ve ayrıca Azure Active Directory tarafından sağlanan hello özelliklerden avantajı istiyorsanız, karma Azure AD alanına katılmış aygıtlar uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="52018-169">Bunlar, her ikisi de aygıtlardır, birleştirilmiş tooyour şirket içi Active Directory ve Azure Active Directory'yi.</span><span class="sxs-lookup"><span data-stu-id="52018-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Azure AD kayıtlı cihazları](./media/device-management-introduction/01.png)


<span data-ttu-id="52018-171">Varsa Azure AD karma alanına katılmış aygıtlar kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="52018-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="52018-172">NTLM kullanan Win32 uygulamaları dağıtılan toothese aygıtlar sahip / Kerberos.</span><span class="sxs-lookup"><span data-stu-id="52018-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="52018-173">GP veya SCCM gerektiren / DCM toomanage aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="52018-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="52018-174">Çalışanlarınız için toocontinue toouse görüntüleme çözümleri tooconfigure cihazların istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="52018-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="52018-175">Karma Azure yapılandırabilirsiniz AD alanına katılmış cihazlar Windows 10 ve Windows 8 ve Windows 7 gibi alt düzey cihazlar.</span><span class="sxs-lookup"><span data-stu-id="52018-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="52018-176">Özet</span><span class="sxs-lookup"><span data-stu-id="52018-176">Summary</span></span>

<span data-ttu-id="52018-177">Azure AD'de cihaz yönetimi ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="52018-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="52018-178">Azure AD hello denetiminde aygıtlarını getiren hello işlemini basitleştirmek</span><span class="sxs-lookup"><span data-stu-id="52018-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="52018-179">Kullanıcılarınıza kolay toouse erişim tooyour kuruluşun bulut tabanlı kaynaklar ile sağlama</span><span class="sxs-lookup"><span data-stu-id="52018-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="52018-180">Bir Flash bir kural olarak kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="52018-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="52018-181">Kişisel cihazlar için Azure AD kayıtlı cihazları</span><span class="sxs-lookup"><span data-stu-id="52018-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="52018-182">Azure AD alanına katılmış aygıtlar tooan katılmış olmayan cihazlarda şirket içi AD</span><span class="sxs-lookup"><span data-stu-id="52018-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="52018-183">Karma Azure AD alanına katılmış aygıtlar tooan katılmış olan cihazlarda şirket içi AD</span><span class="sxs-lookup"><span data-stu-id="52018-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="52018-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52018-184">Next steps</span></span>

- <span data-ttu-id="52018-185">tooget nasıl toomanage aygıtı hello Azure portal, bkz: genel bakış [hello Azure portalını kullanarak cihazları yönetme](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="52018-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="52018-186">cihaz temelli koşullu erişim hakkında daha fazla toolearn bkz [Azure Active Directory cihaz temelli koşullu erişim ilkelerini yapılandırma](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="52018-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="52018-187">bkz: toosetup karma Azure AD alanına katılmış aygıtlar [nasıl tooconfigure karma Azure Active Directory'ye katılmış cihazlarda](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="52018-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


