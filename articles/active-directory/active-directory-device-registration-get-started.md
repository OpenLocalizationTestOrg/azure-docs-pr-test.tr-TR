---
title: "etki alanına katılmış Windows cihazlarının Azure Active Directory ile aaaHow tooconfigure otomatik kayıt | Microsoft Docs"
description: "Etki alanına katılmış Windows cihazları tooregister, Azure Active Directory ile otomatik olarak ve sessiz bir şekilde ayarlayın."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="4d11a-103">Azure Active Directory cihaz kaydına başlarken</span><span class="sxs-lookup"><span data-stu-id="4d11a-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="4d11a-104">Azure Active Directory cihaz kaydı, cihaz temelli koşullu erişim senaryoları için hello temelidir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="4d11a-105">Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı hello hello kullanıcı oturum açtığında kullanılan tooauthenticate hello cihaz olan bir kimliğe sahip cihazı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d11a-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="4d11a-106">Kimliği doğrulanmış hello cihaz ve hello cihazın hello öznitelikleri hello bulutta ve şirket içi barındırılan uygulamalar için kullanılan tooenforce koşullu erişim ilkeleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="4d11a-107">Microsoft Intune gibi bir mobil cihaz birleştirildiğinde çözümü ile birleştirildiğinde Azure Active Directory'de hello cihaz öznitelikleri hello cihaz hakkındaki ek bilgilerle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="4d11a-108">Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d11a-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="4d11a-109">Microsoft Intune kaydolan cihazlar hakkında daha fazla bilgi için Yönetim için ıntune'a kaydetme aygıtları bakın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="4d11a-110">Azure Active Directory cihaz kaydı Azure Active Directory cihaz kaydı tarafından etkinleştirilen senaryolar iOS, Android ve Windows için destek içerir aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="4d11a-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="4d11a-111">hello Azure AD cihaz kaydı'nı kullanan bireysel senaryolar daha fazla özel gereksinime ve platform desteğine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="4d11a-112">Bu senaryolar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4d11a-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="4d11a-113">**Microsoft Intune ile Office 365 uygulamaları için koşullu erişim:** BT yöneticileri, koşullu erişim cihaz ilkeleri toosecure şirket kaynaklarına, hazırlayabilirsiniz, hello aynı zaman uyumlu cihazlara izin verme bilgi çalışanları sırada tooaccess hello Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="4d11a-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="4d11a-114">Daha fazla bilgi edinmek için bkz. Office 365 hizmetleri için Koşullu Erişim Cihaz İlkeleri.</span><span class="sxs-lookup"><span data-stu-id="4d11a-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="4d11a-115">**Olan koşullu erişim tooapplications şirket içinde barındırılan:** olan uygulamalar Windows Server 2012 R2 ile AD FS toouse yapılandırılmış için kayıtlı cihazlara erişim ilkeleri ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11a-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="4d11a-116">Şirket içi uygulamalara koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory cihaz kaydı hizmetini kullanarak Şirket İçi Uygulamalara Koşullu Erişim](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="4d11a-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="4d11a-117">Azure Active Directory Cihaz Kaydı'nı ayarlama</span><span class="sxs-lookup"><span data-stu-id="4d11a-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="4d11a-118">toosetup cihaz kaydı, birden fazla seçeneği vardır:</span><span class="sxs-lookup"><span data-stu-id="4d11a-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="4d11a-119">Aygıtlar kayıt birleştirilmiş tooAzure AD etki alanı.</span><span class="sxs-lookup"><span data-stu-id="4d11a-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="4d11a-120">Bu konu hakkında daha fazla bilgi için kullanıcılar toojoin Azure AD etki alanı için gereken Azure AD katılımı ve hello ayarları hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11a-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="4d11a-121">Cihazlar, kullanıcılar iş veya Okul tooWindows kişisel bir cihazı veya Mobil cihazların kaydı gerektiren tooa iş kaynaklarına bağlandığınızda hesapları kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="4d11a-122">tooensure Bu, Azure AD cihaz kaydı hello Azure Portalı'nı etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="4d11a-123">Cihazlar, geleneksel etki alanına katılan makineler için otomatik cihaz kaydı kullanılarak kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="4d11a-124">tooensure bunu ile otomatik cihaz kaydı devam etmeden önce ilk kurulum Azure AD Connect gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="4d11a-125">En son yönergeler için bkz: [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="4d11a-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="4d11a-126">Ayrıca gözden geçirin ve da etkinleştirebilir veya Azure Active Directory'de Yönetici portalı hello kullanarak kayıtlı cihazları devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="4d11a-127">Hello Azure Active Directory cihaz kaydı hizmetini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4d11a-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="4d11a-128">**tooenable hello Azure Active Directory cihaz kayıt hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="4d11a-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="4d11a-129">İçinde toohello Microsoft Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="4d11a-130">Merhaba soldaki bölmede bulunan seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="4d11a-131">Merhaba dizin sekmesinde dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="4d11a-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="4d11a-132">**Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="4d11a-133">Çok kaydırma**aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="4d11a-134">Select tüm kullanıcılar için AZURE AD ile CİHAZLARINI KAYDEDEBİLİR.</span><span class="sxs-lookup"><span data-stu-id="4d11a-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="4d11a-135">Merhaba en büyük sayı seçin aygıtların kullanıcı başına tooauthorize istiyor.</span><span class="sxs-lookup"><span data-stu-id="4d11a-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="4d11a-136">Office 365 için Microsoft Intune veya mobil cihaz yönetimi ile Merhaba kayıt cihaz kaydı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="4d11a-137">Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="4d11a-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="4d11a-138">Lütfen doğru şekilde yapılandırıldığından ve hello uygun lisans sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d11a-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="4d11a-139">Varsayılan olarak, iki öğeli kimlik doğrulama hello hizmeti için etkin değil.</span><span class="sxs-lookup"><span data-stu-id="4d11a-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="4d11a-140">Yine de bir cihaz kaydedilirken iki öğeli kimlik doğrulama önerilir.</span><span class="sxs-lookup"><span data-stu-id="4d11a-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="4d11a-141">Bu hizmet için iki öğeli kimlik doğrulama istemeden önce Azure Active Directory'de iki öğeli kimlik doğrulama sağlayıcısını yapılandırmak ve kullanıcı hesaplarınızı çok faktörlü kimlik doğrulaması için yapılandırmanız gerekir, bkz: çok faktörlü kimlik doğrulaması ekleme tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d11a-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="4d11a-142">Windows Server 2012 R2 ile AD FS kullanıyorsanız, AD FS'de iki öğeli kimlik doğrulama modülünü yapılandırmanız gerekir, bkz: Active Directory Federasyon Hizmetleri ile çok faktörlü kimlik doğrulaması kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4d11a-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="4d11a-143">Azure Active Directory'de cihaz nesnelerini görüntüleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="4d11a-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="4d11a-144">Hello Azure yönetici portalından görüntülemek, engelleme ve aygıtların engellemesini kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="4d11a-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="4d11a-145">Engellenen bir cihaz artık yapılandırılmış tooallow yalnızca kayıtlı aygıtların erişim tooapplications sahip olur.</span><span class="sxs-lookup"><span data-stu-id="4d11a-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="4d11a-146">**tooview ve Azure Active Directory'de cihaz nesnelerini yönetme:**</span><span class="sxs-lookup"><span data-stu-id="4d11a-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="4d11a-147">Üzerinde toohello Microsoft Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="4d11a-148">Merhaba soldaki bölmede bulunan seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="4d11a-149">Dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="4d11a-149">Select your directory.</span></span>

4.  <span data-ttu-id="4d11a-150">Seçin **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="4d11a-151">Toosee hello cihazların istediğiniz hello kullanıcı'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="4d11a-152">Seçin **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="4d11a-153">Seçin **kayıtlı cihazlar**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="4d11a-154">Şimdi, gözden geçirin, engelleyebilir veya hello kullanıcının kayıtlı aygıtların engellemesini kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="4d11a-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="4d11a-155">Şirket içi etki alanına katılmış ve otomatik olarak kaydedilmiş Windows 10 cihazları hello kullanıcılar sekmesi altında görünmez. Lütfen hello Get-MsolDevice PowerShell komut toofind tüm kurumsal aygıtları kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d11a-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4d11a-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d11a-156">Next steps</span></span>

<span data-ttu-id="4d11a-157">toosetup otomatik cihaz kaydı bkz [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="4d11a-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


