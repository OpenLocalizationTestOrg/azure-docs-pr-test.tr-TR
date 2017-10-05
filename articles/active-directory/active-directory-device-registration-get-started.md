---
title: "Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma | Microsoft Docs"
description: "Azure Active Directory ile otomatik olarak ve sessiz bir şekilde kaydetmek için etki alanına katılmış Windows cihazları ayarlayın."
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="9d068-103">Azure Active Directory cihaz kaydına başlarken</span><span class="sxs-lookup"><span data-stu-id="9d068-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="9d068-104">Azure Active Directory cihaz kaydı, cihaz temelli koşullu erişim senaryoları için altyapıdır.</span><span class="sxs-lookup"><span data-stu-id="9d068-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="9d068-105">Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı, cihaza kullanıcı oturum açtığı zaman kimlik doğrulama için kullanılan kimliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d068-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="9d068-106">Kimliği doğrulanmış cihaz ve cihaz öznitelikleri böylece bulutta ve şirket içinde barındırılan uygulamalar için koşullu erişim ilkelerini zorlamak üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="9d068-107">Microsoft Intune gibi bir mobil cihaz yönetimi (MDM) çözümü ile birleştirildiğinde Azure Active Directory'deki cihaz öznitelikleri cihaz hakkındaki ek bilgilerle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="9d068-108">Bu durum, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak için cihazlardan erişimi zorlayan koşullu erişim kuralları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d068-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="9d068-109">Microsoft Intune kaydolan cihazlar hakkında daha fazla bilgi için Yönetim için ıntune'a kaydetme aygıtları bakın.</span><span class="sxs-lookup"><span data-stu-id="9d068-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="9d068-110">Azure Active Directory cihaz kaydı Azure Active Directory cihaz kaydı tarafından etkinleştirilen senaryolar iOS, Android ve Windows için destek içerir aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="9d068-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="9d068-111">Azure AD Cihaz Kaydı'nı kullanan bireysel senaryolar daha fazla özel gereksinime ve platform desteğine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="9d068-112">Bu senaryolar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9d068-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="9d068-113">**Microsoft Intune ile Office 365 uygulamaları için koşullu erişim:** BT yöneticileri, bilgi çalışanları üzerinde uyumlu cihazların erişmesine izin vererek aynı anda sırada şirket kaynaklarına güvenli hale getirmek için koşullu erişim cihaz ilkeleri sağlayabilirler Hizmetler.</span><span class="sxs-lookup"><span data-stu-id="9d068-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="9d068-114">Daha fazla bilgi edinmek için bkz. Office 365 hizmetleri için Koşullu Erişim Cihaz İlkeleri.</span><span class="sxs-lookup"><span data-stu-id="9d068-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="9d068-115">**Şirket içinde barındırılan uygulamalara koşullu erişim:** ile Windows Server 2012 R2 AD FS kullanmak üzere yapılandırılan uygulamalar için erişim ilkeleri ile kayıtlı cihazları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d068-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="9d068-116">Şirket içi uygulamalara koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory cihaz kaydı hizmetini kullanarak Şirket İçi Uygulamalara Koşullu Erişim](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9d068-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="9d068-117">Azure Active Directory Cihaz Kaydı'nı ayarlama</span><span class="sxs-lookup"><span data-stu-id="9d068-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="9d068-118">Kurulum bir aygıt kaydı için birçok seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="9d068-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="9d068-119">Azure AD etki alanına katıldığında cihazlarını kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="9d068-120">Bu konu hakkında daha fazla bilgi için Azure AD etki alanına katılmak için Azure AD birleştirme ve kullanıcılar için gerekli ayarları hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d068-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="9d068-121">Kullanıcıların iş veya Okul hesapları Windows kişisel bir cihazda veya Mobil cihazların kaydı gerektiren bir iş kaynaklarına bağladığınızda eklediğinizde aygıtları kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="9d068-122">Bunu sağlamak için Azure Portal'da Azure AD cihaz kaydı etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d068-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="9d068-123">Cihazlar, geleneksel etki alanına katılan makineler için otomatik cihaz kaydı kullanılarak kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="9d068-124">Otomatik cihaz kaydı ile devam etmeden önce bu emin olmak için ilk kurulum Azure AD Connect gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d068-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="9d068-125">En son yönergeler için bkz: [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9d068-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="9d068-126">Ayrıca gözden geçirin ve da etkinleştirebilir veya Azure Active Directory'de Yönetici portalı'nı kullanarak kayıtlı cihazları devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="9d068-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="9d068-127">Azure Active Directory cihaz kaydı hizmetini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9d068-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="9d068-128">**Azure Active Directory cihaz kayıt hizmeti etkinleştirmek için:**</span><span class="sxs-lookup"><span data-stu-id="9d068-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="9d068-129">Microsoft Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9d068-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="9d068-130">Sol bölmede **Active Directory**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9d068-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="9d068-131">Dizin sekmesinde dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="9d068-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="9d068-132">**Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9d068-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="9d068-133">Kaydırma **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="9d068-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="9d068-134">Select tüm kullanıcılar için AZURE AD ile CİHAZLARINI KAYDEDEBİLİR.</span><span class="sxs-lookup"><span data-stu-id="9d068-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="9d068-135">Kullanıcı başına yetkilendirmek istediğiniz maksimum cihaz sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="9d068-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="9d068-136">Office 365 için Microsoft Intune veya mobil cihaz yönetimi ile kayıt cihaz kaydı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9d068-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="9d068-137">Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9d068-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="9d068-138">Lütfen doğru şekilde yapılandırıldığından ve uygun lisans sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9d068-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="9d068-139">Varsayılan olarak hizmet için iki öğeli kimlik doğrulama etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="9d068-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="9d068-140">Yine de bir cihaz kaydedilirken iki öğeli kimlik doğrulama önerilir.</span><span class="sxs-lookup"><span data-stu-id="9d068-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="9d068-141">Bu hizmet için iki öğeli kimlik doğrulama istemeden önce Azure Active Directory'de iki öğeli kimlik doğrulama sağlayıcısını yapılandırmak ve kullanıcı hesaplarınızı çok faktörlü kimlik doğrulaması için yapılandırmanız gerekir, bkz: Azure çok faktörlü kimlik doğrulaması ekleme Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d068-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="9d068-142">Windows Server 2012 R2 ile AD FS kullanıyorsanız, AD FS'de iki öğeli kimlik doğrulama modülünü yapılandırmanız gerekir, bkz: Active Directory Federasyon Hizmetleri ile çok faktörlü kimlik doğrulaması kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9d068-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="9d068-143">Azure Active Directory'de cihaz nesnelerini görüntüleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="9d068-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="9d068-144">Azure Yönetici portalından cihazları görüntüleyebilir, engelleyebilir ve engellerini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d068-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="9d068-145">Bu işlemden sonra, engellenen bir cihaz yalnızca kayıtlı cihazlara izin vermek için yapılandırılan uygulamalara erişim sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="9d068-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="9d068-146">**Azure Active Directory'de cihaz nesnelerini görüntülemek ve yönetmek için:**</span><span class="sxs-lookup"><span data-stu-id="9d068-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="9d068-147">Microsoft Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9d068-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="9d068-148">Sol bölmede **Active Directory**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9d068-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="9d068-149">Dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="9d068-149">Select your directory.</span></span>

4.  <span data-ttu-id="9d068-150">Seçin **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9d068-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="9d068-151">Aygıtları görmek istediğiniz kullanıcıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9d068-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="9d068-152">Seçin **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="9d068-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="9d068-153">Seçin **kayıtlı cihazlar**.</span><span class="sxs-lookup"><span data-stu-id="9d068-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="9d068-154">Şimdi, gözden geçirin, engelleyebilir veya kullanıcının kayıtlı aygıtların engellemesini kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="9d068-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="9d068-155">Şirket içi etki alanına katılmış ve otomatik olarak kaydedilmiş Windows 10 cihazlarına, kullanıcılar sekmesi altında görünmez.</span><span class="sxs-lookup"><span data-stu-id="9d068-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="9d068-156">Lütfen tüm kurumsal aygıtları bulmak için Get-MsolDevice PowerShell komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d068-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="9d068-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d068-157">Next steps</span></span>

<span data-ttu-id="9d068-158">Otomatik cihaz kaydı kurulumu için bkz: [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9d068-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


