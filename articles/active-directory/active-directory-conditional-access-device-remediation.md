---
title: "aaaYou alınamıyor var. hello edilecektir Azure portalından bir Windows aygıtının | Microsoft Docs"
description: "Burada yapamazsınız öğrenin get buradan gelir vardır ve bu iletişim kutusuna çalıştıran tooavoid iade edilemedi."
services: active-directory
keywords: "cihaz temelli koşullu erişim, cihaz kaydı, cihaz kaydını etkinleştirme, cihaz kaydı ve MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="c2cad-104">Bir Windows cihazında bu uygulamaya buradan erişemezsiniz</span><span class="sxs-lookup"><span data-stu-id="c2cad-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="c2cad-105">Örneğin, kuruluşunuzun SharePoint Online intranetine erişim denemesi sırasında, *bu uygulamaya buradan erişemezsiniz* ifadesini içeren bir sayfa ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2cad-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="c2cad-106">Yöneticiniz belirli koşullar altında erişim tooyour kurumunuzun kaynaklarına engelleyen bir koşullu erişim ilkesi yapılandırmış için bu sayfayı görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="c2cad-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="c2cad-107">Gerekli toocontact yardım masasına veya bu sorun çözüldüğünde, yönetici tooget olabilir ancak kendiniz ilk deneyebileceğiniz birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="c2cad-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="c2cad-108">Kullanıyorsanız bir **Windows** aygıt, aşağıdaki hello kontrol etmelidir:</span><span class="sxs-lookup"><span data-stu-id="c2cad-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="c2cad-109">Desteklenen bir tarayıcı mı kullanıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="c2cad-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="c2cad-110">Cihazınızda desteklenen bir Windows sürümü çalıştırıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="c2cad-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="c2cad-111">Cihazınız uyumlu mu?</span><span class="sxs-lookup"><span data-stu-id="c2cad-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="c2cad-112">Desteklenen tarayıcı</span><span class="sxs-lookup"><span data-stu-id="c2cad-112">Supported browser</span></span>

<span data-ttu-id="c2cad-113">Yöneticiniz bir koşullu erişim ilkesi yapılandırdıysa, kuruluşunuzun kaynaklarına yalnızca desteklenen bir tarayıcı kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2cad-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="c2cad-114">Bir Windows cihazda yalnızca **Internet Explorer** ve **Edge** desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c2cad-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="c2cad-115">Merhaba hata sayfasının ayrıntıları bölümünü hello bakarak tooan desteklenmeyen tarayıcı nedeniyle bir kaynağa erişemiyor olup olmadığını, kolayca tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c2cad-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="c2cad-116">![Desteklenmeyen tarayıcılar için "Oraya buradan ulaşamazsınız" iletisi](./media/active-directory-conditional-access-device-remediation/02.png "Senaryo")</span><span class="sxs-lookup"><span data-stu-id="c2cad-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="c2cad-117">Merhaba yalnızca düzeltme toouse Merhaba uygulaması cihaz platformunuz için destekleyen bir tarayıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="c2cad-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="c2cad-118">Desteklenen tarayıcıların tam listesi için bkz. [desteklenen tarayıcılar](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="c2cad-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="c2cad-119">Desteklenen Windows sürümleri</span><span class="sxs-lookup"><span data-stu-id="c2cad-119">Supported versions of Windows</span></span>

<span data-ttu-id="c2cad-120">Merhaba aşağıdaki hello Windows işletim sistemi, Cihazınızda hakkında doğru olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2cad-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="c2cad-121">Cihazınızda bir Windows masaüstü işletim sistemi çalıştırıyorsanız, 7 veya üzeri toobe Windows gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2cad-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="c2cad-122">Cihazınızda bir Windows server işletim sistemi çalıştırıyorsanız, Windows Server 2008 R2 toobe gerekiyor veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c2cad-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="c2cad-123">Uyumlu cihaz</span><span class="sxs-lookup"><span data-stu-id="c2cad-123">Compliant device</span></span>

<span data-ttu-id="c2cad-124">Yöneticiniz erişim tooyour kuruluşunuzun kaynaklardan yalnızca uyumlu cihazların izin veren bir koşullu erişim ilkesi yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="c2cad-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="c2cad-125">Cihazınızı ya da birleştirilmiş tooyour olmalıdır uyumlu toobe şirket içi Active Directory veya tooyour Azure Active Directory birleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="c2cad-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="c2cad-126">Bir kaynak hello hata sayfasının ayrıntıları bölümünü hello bakarak uyumlu değil tooa aygıt son erişemiyor olup olmadığını, kolayca tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c2cad-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="c2cad-127">![Kaydedilmemiş cihazlar için "Oraya buradan ulaşamazsınız" iletileri](./media/active-directory-conditional-access-device-remediation/01.png "Senaryo")</span><span class="sxs-lookup"><span data-stu-id="c2cad-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="c2cad-128">Birleşik aygıt tooan içi Active Directory mi?</span><span class="sxs-lookup"><span data-stu-id="c2cad-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="c2cad-129">**Cihazınızı katılmışsa tooan Active Directory, kuruluşunuzda şirket içi:**</span><span class="sxs-lookup"><span data-stu-id="c2cad-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="c2cad-130">İş hesabınızı (Active Directory hesabınızla) kullanarak tooWindows içinde oturum emin olun.</span><span class="sxs-lookup"><span data-stu-id="c2cad-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="c2cad-131">Bir sanal özel ağ (VPN) veya DirectAccess üzerinden iç kurumsal ağa tooyour bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="c2cad-132">Bağlantı kurulduktan sonra basın hello Windows logosu tuşu + L hello anahtar toolock Windows oturumunuzu.</span><span class="sxs-lookup"><span data-stu-id="c2cad-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="c2cad-133">İş hesabınızın kimlik bilgilerini girerek Windows oturumunuzun kilidini açın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="c2cad-134">Bir dakika bekleyin ve ardından tooaccess hello uygulaması veya hizmeti yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2cad-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="c2cad-135">Görürseniz aynı hello hello sayfasında, **daha fazla ayrıntı** bağlamak ve ardından hello ayrıntılarla yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="c2cad-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="c2cad-136">Birleştirilmemiş aygıt tooan içi Active Directory mi?</span><span class="sxs-lookup"><span data-stu-id="c2cad-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="c2cad-137">Cihazınızı katılmadı tooan şirket içi Active Directory ve Windows 10 çalıştıran, iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="c2cad-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="c2cad-138">Azure AD'ye Katılım’ı çalıştırmak</span><span class="sxs-lookup"><span data-stu-id="c2cad-138">Run Azure AD Join</span></span>
* <span data-ttu-id="c2cad-139">Çalışmanızı ekleyin veya Okul hesabı tooWindows</span><span class="sxs-lookup"><span data-stu-id="c2cad-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="c2cad-140">Bu iki seçenek arasındaki farklar hakkında bilgi edinmek için bkz. [Çalışma alanınızda Windows 10 cihazlarını kullanma](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c2cad-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="c2cad-141">Cihazınız:</span><span class="sxs-lookup"><span data-stu-id="c2cad-141">If your device:</span></span>

- <span data-ttu-id="c2cad-142">Tooyour kuruluş ait, Azure AD katılım çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2cad-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="c2cad-143">Kişisel bir cihazı veya bir Windows phone çalışmanızı ekleyin veya Okul hesabı tooWindows gerekir</span><span class="sxs-lookup"><span data-stu-id="c2cad-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="c2cad-144">Windows 10’da Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="c2cad-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="c2cad-145">Merhaba, aygıt tooAzure AD olan adımları toojoin hello sürüm olarak Windows 10 üzerinde çalıştırılan bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c2cad-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="c2cad-146">toodetermine hello hello çalıştırmak, Windows 10 işletim sistemi sürümü **winver** komutu:</span><span class="sxs-lookup"><span data-stu-id="c2cad-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Windows sürümü](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="c2cad-148">**Windows 10 Yıldönümü Güncelleştirmesi (Sürüm 1607):**</span><span class="sxs-lookup"><span data-stu-id="c2cad-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="c2cad-149">Açık hello **ayarları** uygulama.</span><span class="sxs-lookup"><span data-stu-id="c2cad-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2cad-150">**Hesaplar** > **İş veya okul erişimi** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="c2cad-151">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-151">Click **Connect**.</span></span>
4. <span data-ttu-id="c2cad-152">Tıklatın **bu aygıt tooAzure AD katılma**.</span><span class="sxs-lookup"><span data-stu-id="c2cad-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="c2cad-153">Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="c2cad-154">Oturumu kapatın ve iş hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="c2cad-155">Tooaccess hello uygulama yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2cad-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="c2cad-156">**Windows 10 Kasım 2015 Güncelleştirmesi (Sürüm 1511):**</span><span class="sxs-lookup"><span data-stu-id="c2cad-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="c2cad-157">Açık hello **ayarları** uygulama.</span><span class="sxs-lookup"><span data-stu-id="c2cad-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2cad-158">**Sistem** > **Hakkında** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="c2cad-159">**Azure AD'ye Katıl**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="c2cad-160">Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2cad-161">Oturumu kapatın ve ardından iş hesabınızla (Azure AD hesabınız) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="c2cad-162">Tooaccess hello uygulama yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2cad-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="c2cad-163">Windows 8.1’de Workplace Join</span><span class="sxs-lookup"><span data-stu-id="c2cad-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="c2cad-164">Cihazınızı etki alanına katılmış değil ve bir çalışma alanına katılma Windows 8.1, toodo çalıştıran ve Microsoft Intune kaydederseniz adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="c2cad-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="c2cad-165">**PC Ayarları**'nı açın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="c2cad-166">**Ağ** > **Çalışma Alanı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="c2cad-167">**Katıl**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-167">Click **Join**.</span></span>
4. <span data-ttu-id="c2cad-168">Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2cad-169">**Aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="c2cad-170">Tooaccess hello uygulama yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2cad-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="c2cad-171">Çalışmanızı ekleyin veya Okul hesabı tooWindows</span><span class="sxs-lookup"><span data-stu-id="c2cad-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="c2cad-172">**Windows 10 Yıldönümü Güncelleştirmesi (Sürüm 1607):**</span><span class="sxs-lookup"><span data-stu-id="c2cad-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="c2cad-173">Açık hello **ayarları** uygulama.</span><span class="sxs-lookup"><span data-stu-id="c2cad-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2cad-174">**Hesaplar** > **İş veya okul erişimi** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="c2cad-175">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-175">Click **Connect**.</span></span>
4. <span data-ttu-id="c2cad-176">Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2cad-177">Tooaccess hello uygulama yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2cad-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="c2cad-178">**Windows 10 Kasım 2015 Güncelleştirmesi (Sürüm 1511):**</span><span class="sxs-lookup"><span data-stu-id="c2cad-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="c2cad-179">Açık hello **ayarları** uygulama.</span><span class="sxs-lookup"><span data-stu-id="c2cad-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2cad-180">**Hesaplar** > **Hesaplarınız** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="c2cad-181">**İş veya okul hesabı ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="c2cad-182">Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2cad-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2cad-183">Tooaccess hello uygulama yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2cad-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="c2cad-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2cad-184">Next steps</span></span>
[<span data-ttu-id="c2cad-185">Azure Active Directory koşullu erişimi</span><span class="sxs-lookup"><span data-stu-id="c2cad-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

