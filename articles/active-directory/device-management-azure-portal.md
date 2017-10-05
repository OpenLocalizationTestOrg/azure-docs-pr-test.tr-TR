---
title: "Azure kullanarak cihazları yönetme portalı - Önizleme | Microsoft Docs"
description: "Cihazları yönetmek için Azure portalını kullanmayı öğrenin."
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
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="15f5a-103">Azure kullanarak cihazları yönetme portalı - Önizleme</span><span class="sxs-lookup"><span data-stu-id="15f5a-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="15f5a-104">Bu özellik şu anda genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="15f5a-104">This capability currently is in public preview.</span></span> <span data-ttu-id="15f5a-105">Geri veya herhangi bir değişiklik kaldırmak hazırlıklı olun.</span><span class="sxs-lookup"><span data-stu-id="15f5a-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="15f5a-106">Genel Önizleme sırasında herhangi bir Azure Active Directory (Azure AD) Abonelik özelliği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="15f5a-107">Ancak, özelliği genel kullanıma sunulduğunda özelliği bazı yönlerini bir Azure Active Directory premium aboneliği gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="15f5a-108">Azure Active Directory'de (Azure AD) ile cihaz yönetimi, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="15f5a-109">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="15f5a-109">This topic:</span></span>

- <span data-ttu-id="15f5a-110">Aşina olduğunuzu varsayar [Azure Active Directory'de cihaz yönetimine giriş](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="15f5a-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="15f5a-111">Azure Portalı'nı kullanarak, aygıtları yönetme hakkında bilgi sağlar</span><span class="sxs-lookup"><span data-stu-id="15f5a-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="15f5a-112">Azure portalında cihazları yönetmek için tıklatın ihtiyacınız **aygıtları** içinde **Yönet** bölümünü **Azure Active Directory** dikey.</span><span class="sxs-lookup"><span data-stu-id="15f5a-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="15f5a-114">Aygıt ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="15f5a-114">Configure device settings</span></span>

<span data-ttu-id="15f5a-115">Azure Portalı'nı kullanarak, cihazlarınızı yönetmek için bunlar, Azure AD alanına katılmış ya da kayıtlı gerekir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="15f5a-116">Yönetici olarak, kaydetme ve aygıt ayarlarını yapılandırarak aygıtları birleştirme işleminin ince ayar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/22.png)


<span data-ttu-id="15f5a-118">Cihaz ayarları dikey yapılandırmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="15f5a-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="15f5a-119">**Kullanıcılar cihazları Azure AD'ye katılma** - bu ayarları cihazları Azure AD'ye katılabilirsiniz kullanıcıları seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="15f5a-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="15f5a-120">Varsayılan değer **tüm**.</span><span class="sxs-lookup"><span data-stu-id="15f5a-120">The default is **All**.</span></span>

- <span data-ttu-id="15f5a-121">**Ek yerel Yöneticiler Azure AD alanına katılmış aygıtlar** -bir cihazda yerel yönetici hakları verilen kullanıcılar seçebilir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="15f5a-122">Buraya eklenen kullanıcılar için eklendiğinde *cihaz yöneticileri* Azure AD'de rol.</span><span class="sxs-lookup"><span data-stu-id="15f5a-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="15f5a-123">Azure AD'de genel Yöneticiler ve cihaz sahiplerine yerel yönetici hakları varsayılan olarak verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="15f5a-124">Bu seçenek bir premium edition Azure AD Premium veya Enterprise Mobility Suite (EMS) gibi ürünler aracılığıyla kullanılabilen bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="15f5a-125">**Kullanıcıları Azure AD ile cihazlarını kaydetme** -Azure AD ile kaydedilecek cihazları izin vermek için bu ayarı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="15f5a-126">Seçerseniz **hiçbiri**, Azure AD alanına bağlı olmadıkları zaman Kaydet veya karma Azure AD alanına katılmış aygıtlar izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="15f5a-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="15f5a-127">Office 365 için Microsoft Intune veya mobil cihaz Yönetimi (MDM) ile kayıt kayıt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="15f5a-128">Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** kullanılamıyor...</span><span class="sxs-lookup"><span data-stu-id="15f5a-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="15f5a-129">**Aygıtları katılmak çok öğeli kimlik doğrulama gerektiren** -kullanıcıların cihazlarını Azure AD'ye katılmak için ikinci bir kimlik doğrulama faktörü sağlamalarının gerekip gerekmediğini seçin.</span><span class="sxs-lookup"><span data-stu-id="15f5a-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="15f5a-130">Varsayılan değer **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="15f5a-130">The default is **No**.</span></span> <span data-ttu-id="15f5a-131">Bir cihaz kaydedilirken çok faktörlü kimlik doğrulaması gerektiren öneririz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="15f5a-132">Bu hizmet için çok faktörlü kimlik doğrulamasını etkinleştirmeden önce çok faktörlü kimlik doğrulamasının cihazlarını kaydeden kullanıcılar için yapılandırılmış emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="15f5a-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="15f5a-133">Farklı Azure çok faktörlü kimlik doğrulama hizmetleri hakkında daha fazla bilgi için bkz: [Azure multi-Factor authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15f5a-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="15f5a-134">**En fazla cihaz sayısını** -Bu ayar, Azure AD'de kullanıcı olan aygıtların sayısı seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="15f5a-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="15f5a-135">Bir kullanıcı bu kota ulaşırsa, bunlar olan değil kadar ek cihaz ekleyemez veya daha fazla var olan cihazları kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="15f5a-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="15f5a-136">Azure AD alanına katılmış veya Azure AD bugün kayıtlı olan tüm aygıtları için aygıt teklif sayılır.</span><span class="sxs-lookup"><span data-stu-id="15f5a-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="15f5a-137">Varsayılan değer **20**.</span><span class="sxs-lookup"><span data-stu-id="15f5a-137">The default value is **20**.</span></span>

- <span data-ttu-id="15f5a-138">**Kullanıcıların eşitleme ayarları ve uygulama verileri cihaz üzerinden** -varsayılan olarak, bu ayar **NONE**.</span><span class="sxs-lookup"><span data-stu-id="15f5a-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="15f5a-139">Belirli kullanıcıları veya grupları veya tüm seçilmesi, kullanıcının ayarları ve uygulama verilerini Windows 10 cihazlarını arasında eşitlemeye izin verir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="15f5a-140">Eşitleme Windows 10'da nasıl çalıştığı hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="15f5a-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="15f5a-141">Bu seçenek bir premium Azure AD Premium veya Enterprise Mobility Suite (EMS) gibi ürünler aracılığıyla kullanılabilen bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Bir Intune cihaz yönetme](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="15f5a-143">Aygıtlar bulunamadı</span><span class="sxs-lookup"><span data-stu-id="15f5a-143">Locate devices</span></span>

<span data-ttu-id="15f5a-144">Azure portalında yönetici olarak, kayıtlı ve birleştirilmiş cihazları bulmak için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="15f5a-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="15f5a-145">**Tüm cihazlar** içinde **Yönet** bölümünü **aygıtları** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="15f5a-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Tüm cihazlar](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="15f5a-147">**Aygıtları** içinde **Yönet** bölümünü bir **kullanıcı** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="15f5a-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Tüm cihazlar](./media/device-management-azure-portal/43.png)



<span data-ttu-id="15f5a-149">Her iki seçenek ile bir görünüm elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="15f5a-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="15f5a-150">Filtre olarak görünen adı kullanarak cihazları için aramanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="15f5a-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="15f5a-151">Kayıtlı ve birleştirilmiş aygıtları ayrıntılı bakış sağlar</span><span class="sxs-lookup"><span data-stu-id="15f5a-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="15f5a-152">Genel cihaz yönetim görevlerini gerçekleştirmenize olanak sağlar</span><span class="sxs-lookup"><span data-stu-id="15f5a-152">Enables you to perform common device management tasks</span></span>
   

![Tüm cihazlar](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="15f5a-154">Aygıt yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="15f5a-154">Device management tasks</span></span>

<span data-ttu-id="15f5a-155">Bir yönetici olarak kayıtlı veya birleştirilmiş cihazları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="15f5a-156">Bu bölümde, genel cihaz yönetim görevleri hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="15f5a-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="15f5a-157">**Bir Intune cihaz yönetme** -Intune yöneticisiyseniz, olarak işaretlenmiş cihazlarını yönetebilmeniz için **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="15f5a-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="15f5a-158">Bir yönetici ek aygıt görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="15f5a-158">An administrator can see additional device</span></span> 

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/31.png)


<span data-ttu-id="15f5a-160">**Etkinleştir / devre dışı bir Azure AD cihaz**</span><span class="sxs-lookup"><span data-stu-id="15f5a-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="15f5a-161">Etkinleştirmek veya bir aygıtı devre dışı bırakmak için Azure AD genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="15f5a-162">Bir aygıtı devre dışı bırakma, bir aygıt, Azure AD kaynaklarını erişmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="15f5a-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="15f5a-163">Aygıt devre dışı bırakmak için her iki tıklatabilirsiniz *...*</span><span class="sxs-lookup"><span data-stu-id="15f5a-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="15f5a-164">Aygıt ek ayrıntılar için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="15f5a-164">click the device for additional details.</span></span>

 
![Bir Intune cihaz yönetme](./media/device-management-azure-portal/33.png)

<span data-ttu-id="15f5a-166">Bir aygıtı devre dışı bırakma durumunda değişiklikler **etkin** sütuna **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="15f5a-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Bir aygıtı devre dışı](./media/device-management-azure-portal/32.png)


<span data-ttu-id="15f5a-168">**Bir Azure AD cihaz silme** - bir cihazı silmek için Azure AD genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="15f5a-169">Bir cihazı silme:</span><span class="sxs-lookup"><span data-stu-id="15f5a-169">Deleting a device:</span></span>
 
- <span data-ttu-id="15f5a-170">Bir aygıt, Azure AD kaynaklarına erişmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="15f5a-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="15f5a-171">Tüm aygıt örneğin bağlı ayrıntıları, Windows cihazları için BitLocker anahtarları kaldırır</span><span class="sxs-lookup"><span data-stu-id="15f5a-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="15f5a-172">Kurtarılamaz bir etkinliği temsil eder ve gerekli olmadığı sürece önerilmez.</span><span class="sxs-lookup"><span data-stu-id="15f5a-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="15f5a-173">Bir cihaz başka bir yönetim yetkilisi (örneğin Microsoft Intune) tarafından yönetiliyorsa, lütfen aygıt yok temizlenmeden / Azure AD'de cihazın silmeden önce devre dışı olduğunu emin olun.</span><span class="sxs-lookup"><span data-stu-id="15f5a-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="15f5a-174">Ya da seçebileceğiniz "..."</span><span class="sxs-lookup"><span data-stu-id="15f5a-174">You can either select “…”</span></span> <span data-ttu-id="15f5a-175">cihazı silmek veya cihazı ek ayrıntılar için tıklatın</span><span class="sxs-lookup"><span data-stu-id="15f5a-175">to delete the device or click on the device for additional details</span></span>
 
![Bir aygıtı silme](./media/device-management-azure-portal/34.png)


<span data-ttu-id="15f5a-177">**Görüntüleme veya cihaz kimliği kopyalama** -cihaz kimliği ayrıntıları aygıttaki veya sorun giderme sırasında PowerShell kullanarak doğrulamak için bir cihaz kimliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="15f5a-178">Kopyalama seçeneği erişmek için aygıt'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="15f5a-178">To access the copy option, click the device.</span></span>

![Bir cihaz kimliği görüntüleyin](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="15f5a-180">**Görüntüleme veya BitLocker anahtarları kopyalama** -bir yöneticiyseniz, görüntüleyebilir ve kullanıcıların kendi şifreli sürücüyü kurtarmasına yardımcı olmak için BitLocker anahtarları kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="15f5a-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="15f5a-181">Bu anahtarlar yalnızca şifrelenmiş Windows cihazları için kullanılabilir ve kendi anahtarları Azure AD'de depolanan sahip.</span><span class="sxs-lookup"><span data-stu-id="15f5a-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="15f5a-182">Cihaz ayrıntılarını erişirken bu anahtarları kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-182">You can copy these keys when accessing details of the device.</span></span>
 
![BitLocker anahtarları görüntüleyin](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="15f5a-184">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="15f5a-184">Audit logs</span></span>


<span data-ttu-id="15f5a-185">Cihaz etkinliklerini, etkinlik günlükleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="15f5a-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="15f5a-186">Bu, kullanıcı veya cihaz kayıt hizmeti tarafından tetiklenen etkinliklerin içerir:</span><span class="sxs-lookup"><span data-stu-id="15f5a-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="15f5a-187">Cihaz oluşturma ve cihazda sahipleri/kullanıcıları ekleme</span><span class="sxs-lookup"><span data-stu-id="15f5a-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="15f5a-188">Cihaz ayarlarındaki değişiklikler</span><span class="sxs-lookup"><span data-stu-id="15f5a-188">Changes to device settings</span></span>

- <span data-ttu-id="15f5a-189">Bir aygıt güncelleştirme veya silme gibi aygıt işlemleri</span><span class="sxs-lookup"><span data-stu-id="15f5a-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="15f5a-190">Giriş noktanızdır denetim verilere **denetim günlüklerini** içinde **etkinlik** bölümünü **aygıtları* dikey.</span><span class="sxs-lookup"><span data-stu-id="15f5a-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Denetim günlükleri](./media/device-management-azure-portal/61.png)


<span data-ttu-id="15f5a-192">Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:</span><span class="sxs-lookup"><span data-stu-id="15f5a-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="15f5a-193">Olayın tarihi ve saati</span><span class="sxs-lookup"><span data-stu-id="15f5a-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="15f5a-194">hedefleri</span><span class="sxs-lookup"><span data-stu-id="15f5a-194">the targets</span></span>

- <span data-ttu-id="15f5a-195">Başlatıcı / aktör (kimin) etkinliğin</span><span class="sxs-lookup"><span data-stu-id="15f5a-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="15f5a-196">Etkinlik (ne)</span><span class="sxs-lookup"><span data-stu-id="15f5a-196">the activity (what)</span></span>

![Denetim günlükleri](./media/device-management-azure-portal/63.png)

<span data-ttu-id="15f5a-198">Araç çubuğunda **Sütunlar**’a tıklayarak liste görünümünü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Denetim günlükleri](./media/device-management-azure-portal/64.png)


<span data-ttu-id="15f5a-200">Raporlanan verileri istediğiniz düzeye gelecek şekilde daraltmak için, aşağıdaki alanları kullanarak denetim verilerini filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="15f5a-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="15f5a-201">Catergory</span><span class="sxs-lookup"><span data-stu-id="15f5a-201">Catergory</span></span>
- <span data-ttu-id="15f5a-202">Etkinlik kaynak türü</span><span class="sxs-lookup"><span data-stu-id="15f5a-202">Activity resource type</span></span>
- <span data-ttu-id="15f5a-203">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="15f5a-203">Activity</span></span>
- <span data-ttu-id="15f5a-204">Tarih aralığı</span><span class="sxs-lookup"><span data-stu-id="15f5a-204">Date range</span></span>
- <span data-ttu-id="15f5a-205">Hedef</span><span class="sxs-lookup"><span data-stu-id="15f5a-205">Target</span></span>
- <span data-ttu-id="15f5a-206">(Aktör) tarafından başlatılan</span><span class="sxs-lookup"><span data-stu-id="15f5a-206">Initiated By (Actor)</span></span>

<span data-ttu-id="15f5a-207">Filtreler yanı sıra belirli girişleri için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f5a-207">In addition to the filters, you can search for specific entries.</span></span>

![Denetim günlükleri](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="15f5a-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15f5a-209">Next steps</span></span>

* [<span data-ttu-id="15f5a-210">Azure Active Directory'de cihaz yönetimine giriş</span><span class="sxs-lookup"><span data-stu-id="15f5a-210">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



