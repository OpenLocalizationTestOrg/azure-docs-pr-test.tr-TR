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
ms.openlocfilehash: c158c67a82e12501386179e19bc75fd852d7e308
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="cd440-103">Azure AD uygulama proxy'si bir Azure AD etki alanı Hizmetleri yönetilen etki alanında dağıtma</span><span class="sxs-lookup"><span data-stu-id="cd440-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="cd440-104">Azure Active Directory (AD) uygulama proxy'si, internet üzerinden erişilebilmesi için şirket içi uygulamaları yayımlama tarafından uzaktan çalışanlar destek yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cd440-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="cd440-105">Azure AD etki alanı Hizmetleri ile Azure altyapı hizmetleri için şirket içi çalışan şimdi yükseltme-ve-shift eski uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd440-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="cd440-106">Ardından, kuruluşunuzdaki kullanıcılar için güvenli uzaktan erişim sağlamak için Azure AD uygulama proxy'si kullanarak bu uygulamaları yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd440-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="cd440-107">Azure AD uygulama proxy'si yeniyseniz, bu özellik aşağıdaki makaleyi ile hakkında daha fazla bilgi: [güvenli uzaktan erişim sağlamak şirket içi uygulamalar](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd440-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="cd440-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="cd440-108">Before you begin</span></span>
<span data-ttu-id="cd440-109">Bu makalede listelenen görevleri gerçekleştirmek için gerekir:</span><span class="sxs-lookup"><span data-stu-id="cd440-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="cd440-110">Geçerli bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="cd440-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="cd440-111">Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="cd440-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="cd440-112">Bir **Azure AD Basic veya Premium lisansı** Azure AD uygulama proxy'si kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cd440-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="cd440-113">**Azure AD etki alanı Hizmetleri** Azure AD dizini için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="cd440-114">Bunu yapmadıysanız, özetlenen tüm görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd440-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="cd440-115">Görev 1 - etkinleştir Azure AD uygulama proxy'si Azure AD dizininiz için</span><span class="sxs-lookup"><span data-stu-id="cd440-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="cd440-116">Azure AD dizininiz için Azure AD uygulama proxy'si etkinleştirmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cd440-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="cd440-117">Bir yönetici olarak oturum açın [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd440-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="cd440-118">Tıklatın **Azure Active Directory** directory genel bakış getirmek için.</span><span class="sxs-lookup"><span data-stu-id="cd440-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="cd440-119">Tıklatın **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cd440-119">Click **Enterprise applications**.</span></span>

    ![Azure AD dizini seçin](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="cd440-121">Tıklatın **uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="cd440-121">Click **Application proxy**.</span></span> <span data-ttu-id="cd440-122">Bir Azure AD temel veya Azure AD Premium aboneliğiniz yoksa, bir deneme sürümü'nü etkinleştirmek için bir seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cd440-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="cd440-123">İki durumlu **uygulama ara sunucusunu etkinleştirme?** için **etkinleştirmek** tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cd440-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![Uygulama Ara sunucusunu etkinleştirme](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="cd440-125">Bağlayıcısı'nı indirmek için tıklayın **bağlayıcı** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cd440-125">To download the connector, click the **Connector** button.</span></span>

    ![Bağlayıcıyı indir](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="cd440-127">İndirme sayfasında, lisans koşullarını ve Gizlilik Sözleşmesi kabul edin ve tıklayın **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cd440-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![Yükleme Onayla](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="cd440-129">Görev 2 - Azure AD uygulama ara sunucusu Bağlayıcısı'nı dağıtmak için etki alanına katılmış Windows sunucuları hazırlama</span><span class="sxs-lookup"><span data-stu-id="cd440-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="cd440-130">Windows Server sanal Azure AD uygulama ara sunucusu Bağlayıcısı'nı yükleyebilmek için makinelerin etki alanına katılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="cd440-131">Yayımlanan uygulamalara bağlı olarak, bağlayıcı yüklü olduğu birden çok sunucuları sağlamak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd440-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="cd440-132">Yardımcı daha ağır kimlik doğrulama yükü işlemek ve bu dağıtım seçeneğini daha yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd440-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="cd440-133">Azure AD etki alanı Hizmetleri yönetilen etki alanınızı etkinleştirdiğiniz bağlayıcı sunucuları aynı sanal ağ (veya bağlı ve eşlenen bir sanal ağda) sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cd440-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="cd440-134">Benzer şekilde, uygulama proxy'si yayımlamak uygulamaları barındıran sunucuları aynı Azure sanal ağ üzerinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="cd440-135">Bağlayıcı sunucuları sağlamak için başlıklı makalesinde ana hatlarıyla görevleri izleyin [Windows sanal makinesini yönetilen bir etki alanına katma](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="cd440-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="cd440-136">Görev 3 - yükleme ve kaydetme Azure AD uygulama ara sunucusu Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="cd440-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="cd440-137">Daha önce Windows Server sanal makine sağlanan ve yönetilen etki alanına katılan.</span><span class="sxs-lookup"><span data-stu-id="cd440-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="cd440-138">Bu görevde, bu sanal makine üzerinde Azure AD uygulama ara sunucusu Bağlayıcısı'nı yükler.</span><span class="sxs-lookup"><span data-stu-id="cd440-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="cd440-139">Bağlayıcı yükleme paketini Azure AD Web uygulaması Ara sunucusu Bağlayıcısı'nı yüklemek VM kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cd440-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="cd440-140">Çalıştırma **AADApplicationProxyConnectorInstaller.exe** sanal makinede.</span><span class="sxs-lookup"><span data-stu-id="cd440-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="cd440-141">Yazılım Lisans Koşulları'nı kabul edin.</span><span class="sxs-lookup"><span data-stu-id="cd440-141">Accept the software license terms.</span></span>

    ![Yükleme için koşulları kabul edin](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="cd440-143">Yükleme sırasında bağlayıcı Azure AD dizininizi uygulaması proxy'si ile kaydetmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="cd440-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="cd440-144">Sağlayın, **Azure AD genel yönetici kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="cd440-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="cd440-145">Genel yönetici kiracınız, Microsoft Azure kimlik bilgilerinizden farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd440-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="cd440-146">Bağlayıcı kaydetmek için kullanılan yönetici hesabını uygulaması Ara sunucusu hizmetini etkinleştirdiğiniz dizinine ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cd440-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="cd440-147">Örneğin, Kiracı etki alanı contoso.com ise, yönetici olmalıdır admin@contoso.com veya diğer geçerli diğer o etki alanı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="cd440-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="cd440-148">IE Artırılmış Güvenlik Yapılandırması sunucusu Bağlayıcısı'nı yüklemekte olduğunuz açıksa, kayıt ekranı engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="cd440-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="cd440-149">Erişime izin vermek için hata iletisindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="cd440-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="cd440-150">Internet Explorer Artırılmış Güvenlik seçeneğinin devre dışı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cd440-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="cd440-151">Bağlayıcı kaydı başarısız olursa bkz. [Uygulama Proxy’si Sorunlarını Giderme](../active-directory/active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="cd440-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Yüklü bağlayıcı](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="cd440-153">Bağlayıcı emin olmak için Azure AD uygulama ara sunucusu Bağlayıcısı sorun'gidericisini düzgün çalışır çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cd440-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="cd440-154">Sorun gidericisini çalıştırdıktan sonra başarılı bir rapor görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-154">You should see a successful report after running the troubleshooter.</span></span>

    ![Sorun gidericisini başarılı](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="cd440-156">Azure AD dizininizi uygulama proxy sayfasında listelenen yeni yüklenen bağlayıcı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="cd440-157">Azure AD uygulaması Proxy üzerinden yayımlanan uygulamalarla kimlik doğrulaması için yüksek kullanılabilirlik sağlamak için birden çok sunucuya bağlayıcıları yüklemeyi tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd440-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="cd440-158">Bağlayıcı, yönetilen etki alanına katılmış diğer sunuculara yüklemek için yukarıda listelenen aynı adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cd440-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="cd440-159">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="cd440-159">Next Steps</span></span>
<span data-ttu-id="cd440-160">Azure AD uygulama ara sunucusunu ayarlamadıysanız sahip ve Azure AD etki alanı Hizmetleri yönetilen etki alanınız ile tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="cd440-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="cd440-161">**Uygulamalarınızı Azure sanal makineleri geçirme:** yükseltme ve-şirket içi sunucular uygulamalarınızdan Azure sanal makineler için yönetilen etki alanına katılmış kaydırma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd440-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="cd440-162">Bunun yapılması, çalışmakta olan sunucuları şirket içi altyapı maliyetinden kurtulun yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cd440-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="cd440-163">**Azure AD uygulama proxy'si ile uygulama yayımlama:** , Azure Azure AD uygulama proxy'si kullanarak sanal makineleri üzerinde çalışan uygulamaları yayımlama.</span><span class="sxs-lookup"><span data-stu-id="cd440-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="cd440-164">Daha fazla bilgi için bkz: [Azure AD uygulama proxy'si ile uygulama yayımlama](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cd440-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="cd440-165">Dağıtım Not - Azure AD uygulama proxy'si kullanarak yayımlama IWA (tümleşik Windows kimlik doğrulaması) uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cd440-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="cd440-166">Kullanıcıların, kimliğine ve göndermek ve şirket adına belirteçleri almak için uygulama proxy'si bağlayıcıları izin vererek tümleşik Windows kimlik doğrulaması (IWA) kullanarak uygulamalarınızı için çoklu oturum açmayı etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="cd440-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="cd440-167">Kerberos Kısıtlı temsilci (KCD) yönetilen etki alanı kaynaklarına erişmek için gerekli izinleri vermek bağlayıcı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cd440-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="cd440-168">Kaynak tabanlı KCD mekanizması yönetilen etki alanlarında daha yüksek güvenlik için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd440-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="cd440-169">Kaynak tabanlı kerberos Kısıtlı temsilci için Azure AD uygulama ara sunucusu Bağlayıcısı'nı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cd440-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="cd440-170">Kullanıcıların kimliğine bürünebileceği şekilde Azure uygulama ara sunucusu Bağlayıcısı'nı kerberos Kısıtlı temsilci (KCD), yönetilen etki alanında yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="cd440-171">Bir Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında, etki alanı yönetici ayrıcalıklarına sahip değil.</span><span class="sxs-lookup"><span data-stu-id="cd440-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="cd440-172">Bu nedenle, **geleneksel hesap düzeyinde KCD, yönetilen bir etki alanında yapılandırılamaz**.</span><span class="sxs-lookup"><span data-stu-id="cd440-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="cd440-173">Bu konuda açıklandığı gibi kaynak tabanlı KCD kullanın [makale](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="cd440-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cd440-174">AD PowerShell cmdlet'lerini kullanarak yönetilen etki alanını yönetmek için 'AAD DC Yöneticiler' grubunun bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="cd440-175">Azure AD uygulama ara sunucusu Bağlayıcısı'nı yüklü olduğu bilgisayarın ayarlarını almak için Get-ADComputer PowerShell cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd440-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="cd440-176">Bundan sonra kaynak sunucu için kaynak tabanlı KCD ayarlamak için Set-ADComputer cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd440-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="cd440-177">Yönetilen etki alanınızda birden çok uygulama proxy'si bağlayıcı dağıttıysanız, kaynak tabanlı KCD her tür bağlayıcı örneği için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd440-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="cd440-178">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="cd440-178">Related Content</span></span>
* [<span data-ttu-id="cd440-179">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="cd440-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="cd440-180">Yönetilen bir etki alanında Kerberos Kısıtlanmış temsilci seçimini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cd440-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="cd440-181">Kerberos kısıtlanmış Temsile genel bakış</span><span class="sxs-lookup"><span data-stu-id="cd440-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
