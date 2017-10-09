---
title: "Azure Active Directory etki alanı Hizmetleri: Azure Active Directory Uygulama Ara sunucusu dağıtma | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanları üzerinde Azure AD uygulama proxy'si kullanın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2ac60-103">Azure AD uygulama proxy'si bir Azure AD etki alanı Hizmetleri yönetilen etki alanında dağıtma</span><span class="sxs-lookup"><span data-stu-id="2ac60-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="2ac60-104">Azure Active Directory (AD) uygulama proxy'si hello erişilen şirket içi uygulamalar toobe yayımlayarak uzaktan çalışanlar destek yardımcı olan Internet.</span><span class="sxs-lookup"><span data-stu-id="2ac60-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="2ac60-105">Azure AD etki alanı Hizmetleri ile şirket içi tooAzure altyapı Hizmetleri çalışan şimdi yükseltme-ve-shift eski uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises tooAzure Infrastructure Services.</span></span> <span data-ttu-id="2ac60-106">Ardından hello Azure AD uygulama proxy'si, kuruluşunuzdaki tooprovide güvenli uzaktan erişim toousers kullanarak bu uygulamaları yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ac60-106">You can then publish these applications using hello Azure AD Application Proxy, tooprovide secure remote access toousers in your organization.</span></span>

<span data-ttu-id="2ac60-107">Yeni toohello Azure AD uygulama proxy'si değilseniz, bu özellik hakkında daha fazla bilgi ile Merhaba aşağıdaki makaleye bakın: [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ac60-107">If you're new toohello Azure AD Application Proxy, learn more about this feature with hello following article: [How tooprovide secure remote access tooon-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="2ac60-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="2ac60-108">Before you begin</span></span>
<span data-ttu-id="2ac60-109">Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ac60-109">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="2ac60-110">Geçerli bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="2ac60-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="2ac60-111">Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="2ac60-112">Bir **Azure AD Basic veya Premium lisansı** olan gerekli toouse hello Azure AD uygulama proxy'si.</span><span class="sxs-lookup"><span data-stu-id="2ac60-112">An **Azure AD Basic or Premium license** is required toouse hello Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="2ac60-113">**Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-113">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="2ac60-114">Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ac60-114">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="2ac60-115">Görev 1 - etkinleştir Azure AD uygulama proxy'si Azure AD dizininiz için</span><span class="sxs-lookup"><span data-stu-id="2ac60-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="2ac60-116">Aşağıdaki adımları tooenable hello Azure AD dizininiz için Azure AD uygulama proxy'si hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ac60-116">Perform hello following steps tooenable hello Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="2ac60-117">Merhaba içinde bir yönetici olarak oturum açın [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ac60-117">Sign in as an administrator in hello [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="2ac60-118">Tıklatın **Azure Active Directory** toobring hello directory genel bakış ayarlama.</span><span class="sxs-lookup"><span data-stu-id="2ac60-118">Click **Azure Active Directory** toobring up hello directory overview.</span></span> <span data-ttu-id="2ac60-119">Tıklatın **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2ac60-119">Click **Enterprise applications**.</span></span>

    ![Azure AD dizini seçin](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="2ac60-121">Tıklatın **uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="2ac60-121">Click **Application proxy**.</span></span> <span data-ttu-id="2ac60-122">Bir Azure AD temel veya Azure AD Premium aboneliğiniz yoksa, bir seçenek tooenable bir deneme bakın.</span><span class="sxs-lookup"><span data-stu-id="2ac60-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option tooenable a trial.</span></span> <span data-ttu-id="2ac60-123">İki durumlu **uygulama ara sunucusunu etkinleştirme?** çok**etkinleştirmek** tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2ac60-123">Toggle **Enable Application Proxy?** too**Enable** and click **Save**.</span></span>

    ![Uygulama Ara sunucusunu etkinleştirme](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="2ac60-125">toodownload bağlayıcı Merhaba, hello tıklatın **bağlayıcı** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ac60-125">toodownload hello connector, click hello **Connector** button.</span></span>

    ![Bağlayıcıyı indir](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="2ac60-127">Hello indirme sayfasında hello lisans koşullarını ve Gizlilik Sözleşmesi kabul ve hello **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ac60-127">On hello download page, accept hello license terms and privacy agreement and click hello **Download** button.</span></span>

    ![Yükleme Onayla](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="2ac60-129">Görev 2 - sağlama etki alanına katılmış Windows sunucuları toodeploy hello Azure AD uygulama ara sunucusu Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="2ac60-129">Task 2 - Provision domain-joined Windows servers toodeploy hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="2ac60-130">Windows Server sanal hello Azure AD uygulama ara sunucusu Bağlayıcısı yükleme makinelerin etki alanına katılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-130">You need domain-joined Windows Server virtual machines on which you can install hello Azure AD Application Proxy connector.</span></span> <span data-ttu-id="2ac60-131">Yayımlanmakta hello uygulamalara bağlı olarak birden çok sunucu hello bağlayıcı yüklendiği tooprovision seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ac60-131">Depending on hello applications being published, you may choose tooprovision multiple servers on which hello connector is installed.</span></span> <span data-ttu-id="2ac60-132">Yardımcı daha ağır kimlik doğrulama yükü işlemek ve bu dağıtım seçeneğini daha yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="2ac60-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="2ac60-133">Merhaba bağlayıcı sunucuları sağlamak hello aynı sanal ağ (veya bağlı ve eşlenen bir sanal ağ), etkinleştirdiğiniz içinde Azure AD etki alanı Hizmetleri yönetilen etki alanı.</span><span class="sxs-lookup"><span data-stu-id="2ac60-133">Provision hello connector servers on hello same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="2ac60-134">Benzer şekilde, hello uygulama proxy'si yayımlama hello uygulamaları barındıran hello hello üzerinde yüklü toobe sunucunuz aynı Azure sanal ağı.</span><span class="sxs-lookup"><span data-stu-id="2ac60-134">Similarly, hello servers hosting hello applications you publish via hello Application Proxy need toobe installed on hello same Azure virtual network.</span></span>

<span data-ttu-id="2ac60-135">tooprovision bağlayıcı sunucuları başlıklı hello makalesinde ana hatlarıyla hello görevleri izleyin [Windows sanal makine tooa yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2ac60-135">tooprovision connector servers, follow hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="2ac60-136">Görev 3 - yükleme ve kaydetme hello Azure AD uygulama ara sunucusu Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="2ac60-136">Task 3 - Install and register hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="2ac60-137">Daha önce Windows Server sanal makine sağlanan ve toohello yönetilen etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="2ac60-137">Previously, you provisioned a Windows Server virtual machine and joined it toohello managed domain.</span></span> <span data-ttu-id="2ac60-138">Bu görevde, bu sanal makineye hello Azure AD uygulama ara sunucusu Bağlayıcısı yükler.</span><span class="sxs-lookup"><span data-stu-id="2ac60-138">In this task, you will install hello Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="2ac60-139">Merhaba connector yükleme paketini toohello VM hello Azure AD Web uygulaması Ara sunucusu Bağlayıcısı yüklemeniz kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2ac60-139">Copy hello connector installation package toohello VM on which you install hello Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="2ac60-140">Çalıştırma **AADApplicationProxyConnectorInstaller.exe** hello sanal makine üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2ac60-140">Run **AADApplicationProxyConnectorInstaller.exe** on hello virtual machine.</span></span> <span data-ttu-id="2ac60-141">Merhaba yazılım lisans koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="2ac60-141">Accept hello software license terms.</span></span>

    ![Yükleme için koşulları kabul edin](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="2ac60-143">Yükleme sırasında istendiğinde tooregister hello Bağlayıcısı hello Azure AD dizininizin uygulama proxy'si ile demektir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-143">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="2ac60-144">Sağlayın, **Azure AD genel yönetici kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="2ac60-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="2ac60-145">Genel yönetici kiracınız, Microsoft Azure kimlik bilgilerinizden farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="2ac60-146">Hello Yöneticisi kullanılan hesap tooregister hello bağlayıcı toohello ait olmalıdır hello uygulaması Ara sunucusu hizmetini etkinleştirdiğiniz aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="2ac60-146">hello administrator account used tooregister hello connector must belong toohello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="2ac60-147">Hello Yöneticisi hello Kiracı etki alanı contoso.com ise, örneğin, olmalıdır admin@contoso.com veya diğer geçerli diğer o etki alanı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2ac60-147">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="2ac60-148">IE Artırılmış güvenlik yapılandırması için hello sunucusu Merhaba bağlayıcısını yüklediğiniz açıksa, hello kayıt ekranı engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-148">If IE Enhanced Security Configuration is turned on for hello server where you are installing hello connector, hello registration screen might be blocked.</span></span> <span data-ttu-id="2ac60-149">tooallow erişimi, hello hata iletisindeki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="2ac60-149">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="2ac60-150">Internet Explorer Artırılmış Güvenlik seçeneğinin devre dışı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2ac60-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="2ac60-151">Bağlayıcı kaydı başarısız olursa bkz. [Uygulama Proxy’si Sorunlarını Giderme](../active-directory/active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="2ac60-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Yüklü bağlayıcı](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="2ac60-153">tooensure hello bağlayıcı çalışma hello Azure AD uygulama ara sunucusu Bağlayıcısı sorun gidericisini düzgün çalışır.</span><span class="sxs-lookup"><span data-stu-id="2ac60-153">tooensure hello connector works properly, run hello Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="2ac60-154">Başarılı bir rapor sonra çalışan hello sorun gidericisini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-154">You should see a successful report after running hello troubleshooter.</span></span>

    ![Sorun gidericisini başarılı](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="2ac60-156">Azure AD dizininizi'hello uygulama proxy sayfasında listelenen yeni yüklenmiş hello bağlayıcı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-156">You should see hello newly installed connector listed on hello Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="2ac60-157">Birden çok sunucuya tooinstall bağlayıcılar hello Azure AD uygulama proxy'si yayımlanan uygulamalar kimlik doğrulaması için yüksek kullanılabilirlik tooguarantee seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ac60-157">You may choose tooinstall connectors on multiple servers tooguarantee high availability for authenticating applications published through hello Azure AD Application Proxy.</span></span> <span data-ttu-id="2ac60-158">Merhaba tooinstall hello Bağlayıcısı diğer sunucuları birleştirilmiş tooyour yönetilen etki alanı, yukarıda listelenen aynı adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ac60-158">Perform hello same steps listed above tooinstall hello connector on other servers joined tooyour managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2ac60-159">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="2ac60-159">Next Steps</span></span>
<span data-ttu-id="2ac60-160">Azure AD uygulama proxy'si hello ayarlayın ve Azure AD etki alanı Hizmetleri yönetilen etki alanınız ile tümleşik.</span><span class="sxs-lookup"><span data-stu-id="2ac60-160">You have set up hello Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="2ac60-161">**Uygulamaları tooAzure sanal makinelerinizi geçirmek:** uygulamalarınızı şirket içi sunucuları tooAzure sanal makineleri birleştirilmiş tooyour yönetilen etki alanından yükseltme ve üst karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-161">**Migrate your applications tooAzure virtual machines:** You can lift-and-shift your applications from on-premises servers tooAzure virtual machines joined tooyour managed domain.</span></span> <span data-ttu-id="2ac60-162">Bunun yapılması, sunucuları şirket içi çalışan hello altyapı maliyetinden kurtulun yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2ac60-162">Doing so helps you get rid of hello infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="2ac60-163">**Azure AD uygulama proxy'si ile uygulama yayımlama:** , Azure hello Azure AD uygulama proxy'si kullanarak sanal makineleri üzerinde çalışan uygulamaları yayımlama.</span><span class="sxs-lookup"><span data-stu-id="2ac60-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using hello Azure AD Application Proxy.</span></span> <span data-ttu-id="2ac60-164">Daha fazla bilgi için bkz: [Azure AD uygulama proxy'si ile uygulama yayımlama](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2ac60-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="2ac60-165">Dağıtım Not - Azure AD uygulama proxy'si kullanarak yayımlama IWA (tümleşik Windows kimlik doğrulaması) uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2ac60-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="2ac60-166">Tooimpersonate kullanıcılar, uygulama Proxy bağlayıcıları izin vererek tümleşik Windows kimlik doğrulaması (IWA) kullanarak oturum açma tek tooyour uygulamaları etkinleştirmek ve gönderip şirket adına belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="2ac60-166">Enable single sign-on tooyour applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission tooimpersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="2ac60-167">Merhaba bağlayıcı toogrant hello gerekli izinleri tooaccess kaynakları için hello yönetilen etki alanı kerberos Kısıtlı temsilci (KCD) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2ac60-167">Configure kerberos constrained delegation (KCD) for hello connector toogrant hello required permissions tooaccess resources on hello managed domain.</span></span> <span data-ttu-id="2ac60-168">Merhaba kaynak tabanlı KCD mekanizması yönetilen etki alanlarında daha yüksek güvenlik için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ac60-168">Use hello resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="2ac60-169">Kaynak tabanlı kerberos Kısıtlı temsilci hello Azure AD uygulama ara sunucusu Bağlayıcısı için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2ac60-169">Enable resource-based kerberos constrained delegation for hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="2ac60-170">Kullanıcıların kimliğine bürünebileceği şekilde hello Azure uygulama ara sunucusu Bağlayıcısı kerberos Kısıtlı temsilci (KCD), hello yönetilen etki alanında yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ac60-170">hello Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on hello managed domain.</span></span> <span data-ttu-id="2ac60-171">Bir Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında, etki alanı yönetici ayrıcalıklarına sahip değil.</span><span class="sxs-lookup"><span data-stu-id="2ac60-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="2ac60-172">Bu nedenle, **geleneksel hesap düzeyinde KCD, yönetilen bir etki alanında yapılandırılamaz**.</span><span class="sxs-lookup"><span data-stu-id="2ac60-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="2ac60-173">Bu konuda açıklandığı gibi kaynak tabanlı KCD kullanın [makale](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="2ac60-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2ac60-174">Toobe üyesi ihtiyacınız hello 'AAD DC yöneticileri' grubunun tooadminister hello yönetilen AD PowerShell cmdlet'lerini kullanarak etki alanı.</span><span class="sxs-lookup"><span data-stu-id="2ac60-174">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister hello managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="2ac60-175">Merhaba Get-ADComputer PowerShell cmdlet tooretrieve hello ayarları hangi hello Azure AD uygulama ara sunucusu bağlayıcısının yüklendiği hello bilgisayar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ac60-175">Use hello Get-ADComputer PowerShell cmdlet tooretrieve hello settings for hello computer on which hello Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="2ac60-176">Bundan sonra kaynak tabanlı KCD yukarı hello Set-ADComputer cmdlet'i tooset hello kaynak sunucusu için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ac60-176">Thereafter, use hello Set-ADComputer cmdlet tooset up resource-based KCD for hello resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="2ac60-177">Yönetilen etki alanınızda birden çok uygulama proxy'si bağlayıcı dağıttıysanız, tooconfigure gereken kaynak tabanlı KCD her tür bağlayıcı örneği.</span><span class="sxs-lookup"><span data-stu-id="2ac60-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need tooconfigure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="2ac60-178">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="2ac60-178">Related Content</span></span>
* [<span data-ttu-id="2ac60-179">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="2ac60-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2ac60-180">Yönetilen bir etki alanında Kerberos Kısıtlanmış temsilci seçimini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2ac60-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="2ac60-181">Kerberos kısıtlanmış Temsile genel bakış</span><span class="sxs-lookup"><span data-stu-id="2ac60-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
