---
title: "aaaEnable Microsoft iş için Windows Hello kuruluşunuzdaki | Microsoft Docs"
description: "Dağıtım yönergeleri tooenable Microsoft Passport, kuruluşunuzda."
services: active-directory
documentationcenter: 
keywords: "Microsoft Passport, Microsoft Windows Hello iş dağıtım için yapılandırma"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="98faa-104">Microsoft iş için Windows Hello kuruluşunuzda etkinleştir</span><span class="sxs-lookup"><span data-stu-id="98faa-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="98faa-105">Sonra [Windows 10 etki alanına katılmış cihazları Azure Active Directory ile bağlanma](active-directory-azureadjoin-devices-group-policy.md), kuruluşunuzda iş için Microsoft Windows Hello tooenable aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="98faa-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do hello following tooenable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="98faa-106">System Center Configuration Manager dağıtma</span><span class="sxs-lookup"><span data-stu-id="98faa-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="98faa-107">İlke ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="98faa-107">Configure policy settings</span></span>
3. <span data-ttu-id="98faa-108">Merhaba sertifika profili yapılandırma</span><span class="sxs-lookup"><span data-stu-id="98faa-108">Configure hello certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="98faa-109">System Center Configuration Manager dağıtma</span><span class="sxs-lookup"><span data-stu-id="98faa-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="98faa-110">Windows Hello üzerinde iş tuşları temel alarak toodeploy kullanıcı sertifikaları hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="98faa-110">toodeploy user certificates based on Windows Hello for Business keys, you need hello following:</span></span>

* <span data-ttu-id="98faa-111">**System Center Configuration Manager geçerli dalının** -tooinstall sürümü 1606 veya üzeri gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="98faa-111">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span> <span data-ttu-id="98faa-112">Daha fazla bilgi için bkz: Merhaba [System Center Configuration Manager belgeleri](https://technet.microsoft.com/library/mt346023.aspx) ve [System Center Configuration Manager ekip blogu](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="98faa-112">For more information, see hello [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="98faa-113">**Ortak anahtar altyapısı (PKI)** -tooenable Microsoft Windows Hello kullanıcı sertifikaları kullanarak işletmeler için bir PKI yerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="98faa-113">**Public key infrastructure (PKI)** - tooenable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="98faa-114">Bir yoksa veya toouse istemiyorsanız, kullanıcı sertifikaları için Windows Server yüklü 10551 (veya daha iyi) yapı 2016 sahip yeni bir etki alanı denetleyicisi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98faa-114">If you don’t have one, or you don’t want toouse it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="98faa-115">Çok olarak Hello adımları[varolan bir etki alanında etki alanı Denetleyicisi'nin çoğaltmasını yükleme](https://technet.microsoft.com/library/jj574134.aspx) veya çok[yeni bir ortam oluşturuyorsanız yeni bir Active Directory ormanı yüklemek](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="98faa-115">Follow hello steps too[install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or too[install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="98faa-116">(Merhaba ISO'ları indirmek için kullanılabilir [Signiant medya Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="98faa-116">(hello ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="98faa-117">İlke ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="98faa-117">Configure policy settings</span></span>
<span data-ttu-id="98faa-118">Microsoft Windows Hello tooconfigure hello iş ilke ayarları için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="98faa-118">tooconfigure hello Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="98faa-119">Active Directory'de Grup İlkesi</span><span class="sxs-lookup"><span data-stu-id="98faa-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="98faa-120">Merhaba System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="98faa-120">hello System Center Configuration Manager</span></span> 

<span data-ttu-id="98faa-121">Grup İlkesi kullanarak Active Directory'de yöntemi tooconfigure Microsoft Windows Hello iş ilke ayarları için önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="98faa-121">Using Group Policy in Active Directory is hello recommended method tooconfigure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="98faa-122">Ayrıca toodeploy sertifikaları kullandığınızda, System Center Configuration Manager kullanarak hello tercih edilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="98faa-122">Using System Center Configuration Manager is hello preferred method when you also use it toodeploy certificates.</span></span> <span data-ttu-id="98faa-123">Bu senaryo:</span><span class="sxs-lookup"><span data-stu-id="98faa-123">This scenario:</span></span>

* <span data-ttu-id="98faa-124">Merhaba yeni dağıtım senaryoları ile uyumluluk sağlar</span><span class="sxs-lookup"><span data-stu-id="98faa-124">Ensures compatibility with hello newer deployment scenarios</span></span>
* <span data-ttu-id="98faa-125">Merhaba istemci tarafında Windows 10 sürüm 1607 ya da daha iyi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="98faa-125">Requires on hello client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="98faa-126">Microsoft iş için Windows Hello Active Directory'de Grup İlkesi aracılığıyla yapılandırın</span><span class="sxs-lookup"><span data-stu-id="98faa-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="98faa-127">**Adımları**:</span><span class="sxs-lookup"><span data-stu-id="98faa-127">**Steps**:</span></span>

1. <span data-ttu-id="98faa-128">Sunucu Yöneticisi'ni açın ve çok gidin**Araçları** > **Grup İlkesi Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="98faa-128">Open Server Manager, and navigate too**Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="98faa-129">Grup İlkesi Yönetimi'nden tooenable Azure AD katılım istediğiniz toohello etki alanı karşılık gelen toohello etki alanı düğümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="98faa-129">From Group Policy Management, navigate toohello domain node that corresponds toohello domain in which you want tooenable Azure AD Join.</span></span>
3. <span data-ttu-id="98faa-130">Sağ **Grup İlkesi nesneleri**seçip **yeni**.</span><span class="sxs-lookup"><span data-stu-id="98faa-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="98faa-131">Grup İlkesi nesnesi, örneğin, etkinleştirmek için Windows Hello iş adlandırın.</span><span class="sxs-lookup"><span data-stu-id="98faa-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="98faa-132">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98faa-132">Click **OK**.</span></span>
4. <span data-ttu-id="98faa-133">Yeni Grup İlkesi nesneniz sağ tıklayın ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="98faa-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="98faa-134">Çok gidin**Bilgisayar Yapılandırması** > **ilkeleri** > **Yönetim Şablonları** > **Windows Bileşenleri** > **iş için Windows Hello**.</span><span class="sxs-lookup"><span data-stu-id="98faa-134">Navigate too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="98faa-135">Sağ **etkinleştirmek için Windows Hello iş**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="98faa-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="98faa-136">Select hello **etkin** seçenek düğmesine ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="98faa-136">Select hello **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="98faa-137">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98faa-137">Click **OK**.</span></span>
8. <span data-ttu-id="98faa-138">Şimdi hello Grup İlkesi nesnesi tooa konumu tercih ettiğiniz bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98faa-138">You can now link hello Group Policy Object tooa location of your choice.</span></span> <span data-ttu-id="98faa-139">tooenable tüm hello etki alanına katılmış Windows 10 cihazları, kuruluşunuzda bağlantı hello Grup İlkesi toohello etki alanı için bu ilke.</span><span class="sxs-lookup"><span data-stu-id="98faa-139">tooenable this policy for all of hello domain-joined Windows 10 devices in your organization, link hello Group Policy toohello domain.</span></span> <span data-ttu-id="98faa-140">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="98faa-140">For example:</span></span>
   * <span data-ttu-id="98faa-141">Windows 10 etki alanına katılmış bilgisayarları nerede bulunacağı Active Directory'de belirli kuruluş birimi (OU)</span><span class="sxs-lookup"><span data-stu-id="98faa-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="98faa-142">Azure AD ile kayıtlı otomatik olarak Windows 10 etki alanına katılmış bilgisayarları içeren belirli bir güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="98faa-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="98faa-143">System Center Configuration Manager kullanarak iş için Windows Hello yapılandırın</span><span class="sxs-lookup"><span data-stu-id="98faa-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="98faa-144">**Adımları**:</span><span class="sxs-lookup"><span data-stu-id="98faa-144">**Steps**:</span></span>

1. <span data-ttu-id="98faa-145">Açık hello **System Center Configuration Manager**ve ardından çok gidin**varlıklar ve uyumluluk > uyumluluk ayarları > Şirket kaynağına erişim > İş profilleri için Windows Hello**.</span><span class="sxs-lookup"><span data-stu-id="98faa-145">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="98faa-147">Merhaba üstte Hello araç çubuğunda **iş profili için Windows Hello oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="98faa-147">In hello toolbar on hello top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="98faa-149">Merhaba üzerinde **genel** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="98faa-149">On hello **General** dialog, perform hello following steps:</span></span>
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="98faa-151">a.</span><span class="sxs-lookup"><span data-stu-id="98faa-151">a.</span></span> <span data-ttu-id="98faa-152">Merhaba, **adı** metin kutusuna, bu gibi bir durumda profil için bir ad yazın **WHfB Profilim**.</span><span class="sxs-lookup"><span data-stu-id="98faa-152">In hello **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="98faa-153">b.</span><span class="sxs-lookup"><span data-stu-id="98faa-153">b.</span></span> <span data-ttu-id="98faa-154">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98faa-154">Click **Next**.</span></span>
4. <span data-ttu-id="98faa-155">Merhaba üzerinde **desteklenen platformlar** iletişim, bu Windows Hello iş profili ile hazırlanacak ve ardından select hello platformları **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="98faa-155">On hello **Supported Platforms** dialog, select hello platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="98faa-157">Merhaba üzerinde **ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="98faa-157">On hello **Settings** dialog, perform hello following steps:</span></span>
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="98faa-159">a.</span><span class="sxs-lookup"><span data-stu-id="98faa-159">a.</span></span> <span data-ttu-id="98faa-160">Olarak **yapılandırmak için Windows Hello iş**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="98faa-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="98faa-161">b.</span><span class="sxs-lookup"><span data-stu-id="98faa-161">b.</span></span> <span data-ttu-id="98faa-162">Olarak **bir Güvenilir Platform Modülü (TPM) kullanmak**seçin **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="98faa-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="98faa-163">c.</span><span class="sxs-lookup"><span data-stu-id="98faa-163">c.</span></span> <span data-ttu-id="98faa-164">Olarak **kimlik doğrulama yöntemini**seçin **sertifika tabanlı**.</span><span class="sxs-lookup"><span data-stu-id="98faa-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="98faa-165">d.</span><span class="sxs-lookup"><span data-stu-id="98faa-165">d.</span></span> <span data-ttu-id="98faa-166">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98faa-166">Click **Next**.</span></span>
6. <span data-ttu-id="98faa-167">Merhaba üzerinde **Özet** iletişim kutusunda, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="98faa-167">On hello **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="98faa-168">Merhaba üzerinde **tamamlama** iletişim kutusunda, tıklatın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="98faa-168">On hello **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="98faa-169">Merhaba üstte Hello araç çubuğunda **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="98faa-169">In hello toolbar on hello top, click **Deploy**.</span></span>
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a><span data-ttu-id="98faa-171">Merhaba sertifika profili yapılandırma</span><span class="sxs-lookup"><span data-stu-id="98faa-171">Configure hello certificate profile</span></span>
<span data-ttu-id="98faa-172">Şirket içi kimlik doğrulaması için sertifika tabanlı kimlik doğrulaması kullanıyorsanız, tooconfigure gerekir ve bir sertifika profili dağıtın.</span><span class="sxs-lookup"><span data-stu-id="98faa-172">If you are using certificate-based authentication for on-premises authentication, you need tooconfigure and deploy a certificate profile.</span></span> <span data-ttu-id="98faa-173">Bu görev bir NDES sunucusu ve hello System Center Configuration Manager sertifika kayıt noktası site rolü tooset gerektirir.</span><span class="sxs-lookup"><span data-stu-id="98faa-173">This task requires you tooset up an NDES server and Certificate Registration Point site role in hello System Center Configuration Manager.</span></span> <span data-ttu-id="98faa-174">Daha fazla ayrıntı için bkz: Merhaba [Configuration Manager'da sertifika profilleri için Önkoşullar](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="98faa-174">For more details, see hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="98faa-175">Açık hello **System Center Configuration Manager**ve ardından çok gidin**varlıklar ve uyumluluk > uyumluluk ayarları > Şirket kaynağına erişim > sertifika profilleri**.</span><span class="sxs-lookup"><span data-stu-id="98faa-175">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="98faa-176">Akıllı kart oturum açma genişletilmiş anahtar kullanımı (EKU) sahip bir şablon seçin.</span><span class="sxs-lookup"><span data-stu-id="98faa-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="98faa-177">Merhaba üzerinde **SCEP kaydı** sayfa toochoose ihtiyacınız hello sertifika profili, **yükle yoksa başarısız iş için tooPassport** hello olarak **anahtar depolama sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="98faa-177">On hello **SCEP Enrollment** page of hello certificate profile, you need toochoose **Install tooPassport for Work otherwise fail** as hello **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98faa-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98faa-178">Next steps</span></span>
* [<span data-ttu-id="98faa-179">Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için</span><span class="sxs-lookup"><span data-stu-id="98faa-179">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="98faa-180">Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme</span><span class="sxs-lookup"><span data-stu-id="98faa-180">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="98faa-181">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="98faa-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="98faa-182">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="98faa-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="98faa-183">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="98faa-183">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="98faa-184">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="98faa-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

