---
title: "kullanarak aaaManaging cihazları hello Azure portal - Önizleme | Microsoft Docs"
description: "Nasıl toouse hello Azure portal toomanage aygıtlar hakkında bilgi edinin."
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
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="cdd52-103">Azure portal hello - Önizleme kullanarak cihazları yönetme</span><span class="sxs-lookup"><span data-stu-id="cdd52-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="cdd52-104">Bu özellik şu anda genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="cdd52-104">This capability currently is in public preview.</span></span> <span data-ttu-id="cdd52-105">Toorevert hazırlanması veya herhangi bir değişiklik kaldırın.</span><span class="sxs-lookup"><span data-stu-id="cdd52-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="cdd52-106">Genel Önizleme sırasında herhangi bir Azure Active Directory (Azure AD) abonelik Hello özelliği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="cdd52-107">Ancak, Hello özelliği genel kullanıma sunulduğunda hello özelliği bazı yönlerini bir Azure Active Directory premium aboneliği gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="cdd52-108">Azure Active Directory'de (Azure AD) ile cihaz yönetimi, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="cdd52-109">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="cdd52-109">This topic:</span></span>

- <span data-ttu-id="cdd52-110">Merhaba ile bilgi sahibi olduğunuzu varsayar [giriş toodevice Yönetimi Azure Active Directory'de](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="cdd52-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="cdd52-111">Azure portal kullanarak, cihazları yönetme hakkında bilgi ile Merhaba sağlar</span><span class="sxs-lookup"><span data-stu-id="cdd52-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="cdd52-112">toomanage aygıtları hello Azure Portalı'ndaki tooclick ihtiyacınız **aygıtları** hello içinde **Yönet** hello hello bölümünü **Azure Active Directory** dikey.</span><span class="sxs-lookup"><span data-stu-id="cdd52-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="cdd52-114">Aygıt ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="cdd52-114">Configure device settings</span></span>

<span data-ttu-id="cdd52-115">Hello Azure portal kullanarak aygıtlarınızı toobe ihtiyaç toomanage kayıtlı veya tooAzure AD alanına katılmış.</span><span class="sxs-lookup"><span data-stu-id="cdd52-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="cdd52-116">Yönetici olarak, kaydetme ve cihazların Merhaba aygıt ayarları yapılandırarak birleştirme hello işleminde ince ayar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/22.png)


<span data-ttu-id="cdd52-118">Merhaba aygıt ayarları dikey tooconfigure sağlar:</span><span class="sxs-lookup"><span data-stu-id="cdd52-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="cdd52-119">**Kullanıcıların cihazları tooAzure AD katılma** - bu ayarları, cihazları tooAzure AD katılabilirsiniz tooselect hello kullanıcılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdd52-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="cdd52-120">Merhaba varsayılandır **tüm**.</span><span class="sxs-lookup"><span data-stu-id="cdd52-120">hello default is **All**.</span></span>

- <span data-ttu-id="cdd52-121">**Ek yerel Yöneticiler Azure AD alanına katılmış aygıtlar** -bir cihazda yerel yönetici haklarına sahip olurlar hello kullanıcılar seçebilir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="cdd52-122">Buraya eklenen kullanıcılar toohello eklendiğinde *cihaz yöneticileri* Azure AD'de rol.</span><span class="sxs-lookup"><span data-stu-id="cdd52-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="cdd52-123">Azure AD'de genel Yöneticiler ve cihaz sahiplerine yerel yönetici hakları varsayılan olarak verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="cdd52-124">Bu seçenek bir premium edition Azure AD Premium veya Enterprise Mobility Suite (EMS) hello gibi ürünler aracılığıyla kullanılabilen bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="cdd52-125">**Kullanıcıları Azure AD ile cihazlarını kaydetme** -Bu ayar tooallow aygıtları toobe kayıtlı Azure AD ile tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="cdd52-126">Seçerseniz **hiçbiri**, Azure AD alanına bağlı olmadıkları zaman tooregister ya da karma Azure AD alanına katılmış aygıtlar izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="cdd52-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="cdd52-127">Office 365 için Microsoft Intune veya mobil cihaz Yönetimi (MDM) ile kayıt kayıt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="cdd52-128">Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** kullanılamıyor...</span><span class="sxs-lookup"><span data-stu-id="cdd52-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="cdd52-129">**Multi-Factor Auth toojoin cihazları gerektirir** -kullanıcılar gerekli tooprovide olup bir ikinci öğeli kimlik doğrulamasını toojoin kendi cihaz tooAzure AD seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="cdd52-130">Merhaba varsayılandır **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="cdd52-130">hello default is **No**.</span></span> <span data-ttu-id="cdd52-131">Bir cihaz kaydedilirken çok faktörlü kimlik doğrulaması gerektiren öneririz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="cdd52-132">Bu hizmet için çok faktörlü kimlik doğrulamasını etkinleştirmek için önce bu çok faktörlü kimlik doğrulaması, kullanıcıların aygıtlarını kaydetmesini hello kullanıcılar için yapılandırılmış emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="cdd52-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="cdd52-133">Farklı Azure çok faktörlü kimlik doğrulama hizmetleri hakkında daha fazla bilgi için bkz: [Azure multi-Factor authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cdd52-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="cdd52-134">**En fazla cihaz sayısını** -Bu ayar tooselect hello cihaz sayısı üst sınırı bir kullanıcı Azure AD'de sahip olabileceği sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdd52-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="cdd52-135">Bir kullanıcı bu kota ulaşırsa, olan değil olmaları mümkün tooadd ek cihazlar kadar veya daha fazla var olan cihazların Merhaba kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="cdd52-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="cdd52-136">Merhaba aygıt teklif, Azure AD alanına katılmış ya da Azure AD bugün kayıtlı tüm aygıtlar için sayılır.</span><span class="sxs-lookup"><span data-stu-id="cdd52-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="cdd52-137">Merhaba varsayılan değer **20**.</span><span class="sxs-lookup"><span data-stu-id="cdd52-137">hello default value is **20**.</span></span>

- <span data-ttu-id="cdd52-138">**Kullanıcıların eşitleme ayarları ve uygulama verileri cihaz üzerinden** -varsayılan olarak, bu çok ayarı**NONE**.</span><span class="sxs-lookup"><span data-stu-id="cdd52-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="cdd52-139">Belirli kullanıcıları veya grupları veya tüm seçilmesi hello kullanıcının ayarları ve uygulama veri toosync arasında Windows 10 cihazlarını tanır.</span><span class="sxs-lookup"><span data-stu-id="cdd52-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="cdd52-140">Eşitleme Windows 10'da nasıl çalıştığı hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="cdd52-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="cdd52-141">Bu seçenek bir premium Azure AD Premium veya Enterprise Mobility Suite (EMS) hello gibi ürünler aracılığıyla kullanılabilen bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Bir Intune cihaz yönetme](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="cdd52-143">Aygıtlar bulunamadı</span><span class="sxs-lookup"><span data-stu-id="cdd52-143">Locate devices</span></span>

<span data-ttu-id="cdd52-144">Bir yönetici olarak hello Azure portal toolocate kayıtlı ve katılmış cihazlarda iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="cdd52-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="cdd52-145">**Tüm cihazlar** hello içinde **Yönet** hello bölümünü **aygıtları** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="cdd52-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Tüm cihazlar](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="cdd52-147">**Aygıtları** hello içinde **Yönet** bölümünü bir **kullanıcı** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="cdd52-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Tüm cihazlar](./media/device-management-azure-portal/43.png)



<span data-ttu-id="cdd52-149">Her iki seçenek ile tooa görünümü, alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cdd52-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="cdd52-150">Filtre olarak hello görünen adı kullanarak cihazları için toosearch sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdd52-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="cdd52-151">Kayıtlı ve birleştirilmiş aygıtları ayrıntılı bakış sağlar</span><span class="sxs-lookup"><span data-stu-id="cdd52-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="cdd52-152">Tooperform ortak aygıt yönetim görevleri sağlar</span><span class="sxs-lookup"><span data-stu-id="cdd52-152">Enables you tooperform common device management tasks</span></span>
   

![Tüm cihazlar](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="cdd52-154">Aygıt yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="cdd52-154">Device management tasks</span></span>

<span data-ttu-id="cdd52-155">Yönetici olarak, yönettiğiniz hello katılmış cihazlarda veya kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="cdd52-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="cdd52-156">Bu bölümde, genel cihaz yönetim görevleri hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdd52-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="cdd52-157">**Bir Intune cihaz yönetme** -Intune yöneticisiyseniz, olarak işaretlenmiş cihazlarını yönetebilmeniz için **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="cdd52-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="cdd52-158">Bir yönetici ek aygıt görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cdd52-158">An administrator can see additional device</span></span> 

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/31.png)


<span data-ttu-id="cdd52-160">**Etkinleştir / devre dışı bir Azure AD cihaz**</span><span class="sxs-lookup"><span data-stu-id="cdd52-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="cdd52-161">tooenable veya devre dışı bir aygıt, Azure AD'de toobe genel yönetici gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="cdd52-162">Bir aygıtı devre dışı bırakma, bir aygıt, Azure AD kaynaklarını erişmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="cdd52-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="cdd52-163">toodisable hello aygıt yapabilecekleriniz'i *...*</span><span class="sxs-lookup"><span data-stu-id="cdd52-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="cdd52-164">Merhaba aygıtı ek ayrıntılar için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cdd52-164">click hello device for additional details.</span></span>

 
![Bir Intune cihaz yönetme](./media/device-management-azure-portal/33.png)

<span data-ttu-id="cdd52-166">Bir aygıtı devre dışı bırakma değişiklikleri hello hello durumda **etkin** sütun çok**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="cdd52-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Bir aygıtı devre dışı](./media/device-management-azure-portal/32.png)


<span data-ttu-id="cdd52-168">**Bir Azure AD cihaz silme** -toodelete bir aygıtı toobe genel yöneticinin Azure AD içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="cdd52-169">Bir cihazı silme:</span><span class="sxs-lookup"><span data-stu-id="cdd52-169">Deleting a device:</span></span>
 
- <span data-ttu-id="cdd52-170">Bir aygıt, Azure AD kaynaklarına erişmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="cdd52-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="cdd52-171">Tüm iliştirilmiş toohello aygıt, örneğin: ayrıntıları, Windows cihazları için BitLocker anahtarları kaldırır</span><span class="sxs-lookup"><span data-stu-id="cdd52-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="cdd52-172">Kurtarılamaz bir etkinliği temsil eder ve gerekli olmadığı sürece önerilmez.</span><span class="sxs-lookup"><span data-stu-id="cdd52-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="cdd52-173">Lütfen bir cihaz başka bir yönetim yetkilisi (örneğin Microsoft Intune) tarafından yönetiliyorsa hello aygıt temizlenmeden / Azure AD'de hello aygıt silmeden önce devre dışı bırakılan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cdd52-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="cdd52-174">Ya da seçebileceğiniz "..."</span><span class="sxs-lookup"><span data-stu-id="cdd52-174">You can either select “…”</span></span> <span data-ttu-id="cdd52-175">toodelete hello aygıt veya hello cihazda ek ayrıntılar için tıklatın</span><span class="sxs-lookup"><span data-stu-id="cdd52-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Bir aygıtı silme](./media/device-management-azure-portal/34.png)


<span data-ttu-id="cdd52-177">**Görüntüleme veya cihaz kimliği kopyalama** -hello cihazında veya sorun giderme sırasında PowerShell kullanarak bir cihaz kimliği tooverify hello cihaz kimliği ayrıntıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="cdd52-178">tooaccess hello Kopyala seçeneğini, hello cihaz seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cdd52-178">tooaccess hello copy option, click hello device.</span></span>

![Bir cihaz kimliği görüntüleyin](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="cdd52-180">**Görüntüleme veya BitLocker anahtarları kopyalama** -bir yönetici görebilir ve kopyalama hello BitLocker anahtarları toohelp kullanıcılar toorecover kendi şifreli sürücüyü.</span><span class="sxs-lookup"><span data-stu-id="cdd52-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="cdd52-181">Bu anahtarlar yalnızca şifrelenmiş Windows cihazları için kullanılabilir ve kendi anahtarları Azure AD'de depolanan sahip.</span><span class="sxs-lookup"><span data-stu-id="cdd52-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="cdd52-182">Bu anahtarları hello cihaz ayrıntılarını erişirken kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-182">You can copy these keys when accessing details of hello device.</span></span>
 
![BitLocker anahtarları görüntüleyin](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="cdd52-184">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="cdd52-184">Audit logs</span></span>


<span data-ttu-id="cdd52-185">Merhaba aygıt etkinlikleri hello etkinlik günlükleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cdd52-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="cdd52-186">Merhaba cihaz kayıt hizmeti veya hello kullanıcı tarafından tetiklenen etkinliklerin içerir:</span><span class="sxs-lookup"><span data-stu-id="cdd52-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="cdd52-187">Cihaz oluşturma ve hello aygıtta sahipleri/kullanıcıları ekleme</span><span class="sxs-lookup"><span data-stu-id="cdd52-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="cdd52-188">Toodevice ayarlarını değiştirir</span><span class="sxs-lookup"><span data-stu-id="cdd52-188">Changes toodevice settings</span></span>

- <span data-ttu-id="cdd52-189">Bir aygıt güncelleştirme veya silme gibi aygıt işlemleri</span><span class="sxs-lookup"><span data-stu-id="cdd52-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="cdd52-190">Giriş noktası verileri denetleme toohello olan **denetim günlüklerini** hello içinde **etkinlik** hello bölümünü **aygıtları* dikey.</span><span class="sxs-lookup"><span data-stu-id="cdd52-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Denetim günlükleri](./media/device-management-azure-portal/61.png)


<span data-ttu-id="cdd52-192">Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:</span><span class="sxs-lookup"><span data-stu-id="cdd52-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="cdd52-193">Başlangıç tarihi ve saati hello oluşum</span><span class="sxs-lookup"><span data-stu-id="cdd52-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="cdd52-194">Merhaba hedefleri</span><span class="sxs-lookup"><span data-stu-id="cdd52-194">hello targets</span></span>

- <span data-ttu-id="cdd52-195">Başlatıcı hello / aktör (kimin) etkinliğin</span><span class="sxs-lookup"><span data-stu-id="cdd52-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="cdd52-196">Merhaba etkinlik (ne)</span><span class="sxs-lookup"><span data-stu-id="cdd52-196">hello activity (what)</span></span>

![Denetim günlükleri](./media/device-management-azure-portal/63.png)

<span data-ttu-id="cdd52-198">Tıklatarak hello liste görünümü özelleştirebilirsiniz **sütunları** hello araç.</span><span class="sxs-lookup"><span data-stu-id="cdd52-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Denetim günlükleri](./media/device-management-azure-portal/64.png)


<span data-ttu-id="cdd52-200">Merhaba aşağı toonarrow veri tooa düzeyinde çalışır, alanları izleyen hello kullanarak hello denetim verileri filtreleyebilirsiniz bildirdi:</span><span class="sxs-lookup"><span data-stu-id="cdd52-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="cdd52-201">Catergory</span><span class="sxs-lookup"><span data-stu-id="cdd52-201">Catergory</span></span>
- <span data-ttu-id="cdd52-202">Etkinlik kaynak türü</span><span class="sxs-lookup"><span data-stu-id="cdd52-202">Activity resource type</span></span>
- <span data-ttu-id="cdd52-203">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="cdd52-203">Activity</span></span>
- <span data-ttu-id="cdd52-204">Tarih aralığı</span><span class="sxs-lookup"><span data-stu-id="cdd52-204">Date range</span></span>
- <span data-ttu-id="cdd52-205">Hedef</span><span class="sxs-lookup"><span data-stu-id="cdd52-205">Target</span></span>
- <span data-ttu-id="cdd52-206">(Aktör) tarafından başlatılan</span><span class="sxs-lookup"><span data-stu-id="cdd52-206">Initiated By (Actor)</span></span>

<span data-ttu-id="cdd52-207">Ayrıca toohello filtreleri, belirli girişleri için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd52-207">In addition toohello filters, you can search for specific entries.</span></span>

![Denetim günlükleri](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="cdd52-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cdd52-209">Next steps</span></span>

* [<span data-ttu-id="cdd52-210">Azure Active Directory'de giriş toodevice Yönetimi</span><span class="sxs-lookup"><span data-stu-id="cdd52-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



