---
title: "SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştir | Microsoft Docs"
description: "Bir şirket içi SharePoint sunucusu Azure AD uygulama proxy'si ile tümleştirme hakkında temel bilgiler yer almaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="743f6-103">SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="743f6-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="743f6-104">Bu makalede, Azure Active Directory (Azure AD) uygulama ara sunucusu ile bir şirket içi SharePoint sunucusu tümleştirme anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="743f6-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="743f6-105">SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştirmek için bu makaledeki adım adım bölümler izleyin.</span><span class="sxs-lookup"><span data-stu-id="743f6-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="743f6-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="743f6-106">Prerequisites</span></span>

<span data-ttu-id="743f6-107">Bu makalede, ortamınızda SharePoint 2013 veya daha yeni zaten sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="743f6-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="743f6-108">Ayrıca, aşağıdaki önkoşulları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="743f6-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="743f6-109">SharePoint yerel Kerberos desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="743f6-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="743f6-110">Bu nedenle, iç siteleri Azure AD uygulama proxy'si aracılığıyla uzaktan erişen kullanıcılar, çoklu oturum açma (SSO) deneyimi sağlamak için kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="743f6-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="743f6-111">SharePoint server'ınızı birkaç yapılandırma değişiklikleri yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-111">You need to make a few configuration changes to your SharePoint server.</span></span> <span data-ttu-id="743f6-112">Hazırlama ortamında kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="743f6-112">We recommend using a staging environment.</span></span> <span data-ttu-id="743f6-113">Bu şekilde, güncelleştirmelerinin hazırlama sunucunuza ilk olması ve üretime geçmeden önce bir test döngüsü kolaylaştırmak.</span><span class="sxs-lookup"><span data-stu-id="743f6-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="743f6-114">Biz yayımlanan URL üzerinde SSL gerektirdiğinden SharePoint için SSL kurma zaten ayarladığınızdan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="743f6-114">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span></span> <span data-ttu-id="743f6-115">SSL gönderilen ve eşlenen bağlantılar doğru olduğundan emin olmak için iç sitenizde etkin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-115">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="743f6-116">SSL yapılandırmadıysanız bkz [SharePoint 2013 için SSL yapılandırma](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="743f6-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="743f6-117">Ayrıca, bağlayıcı makine dağıttığınız sertifika güvendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="743f6-117">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="743f6-118">(Sertifika herkese açık şekilde verilmesi gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="743f6-118">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="743f6-119">1. adım: çoklu oturum açma SharePoint'e ayarlama</span><span class="sxs-lookup"><span data-stu-id="743f6-119">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="743f6-120">Müşterilerimizin en iyi SSO deneyimi bu durumda kendi arka uç uygulamalar için SharePoint server istiyor.</span><span class="sxs-lookup"><span data-stu-id="743f6-120">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="743f6-121">Yeniden kimlik doğrulaması için istenmez çünkü bu ortak Azure AD senaryoda kullanıcı yalnızca bir kez kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="743f6-121">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="743f6-122">Gerektiren veya Windows kimlik doğrulaması kullanan şirket içi uygulamalar için Kerberos kimlik doğrulama protokolünü ve kısıtlı Kerberos temsilci (KCD) adlı bir özellik kullanarak SSO elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="743f6-123">Kullanıcı Windows doğrudan oturum kurmadı olsa bile yapılandırıldığında, KCD, bir kullanıcının windows bilet/belirteci almak uygulama ara sunucusu Bağlayıcısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="743f6-123">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="743f6-124">KCD hakkında daha fazla bilgi için bkz: [Kerberos Kısıtlı temsilci genel bakış](https://technet.microsoft.com/library/jj553400.aspx).</span><span class="sxs-lookup"><span data-stu-id="743f6-124">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="743f6-125">Bir SharePoint sunucusu için KCD ayarlamak için aşağıdaki sıralı bölümlerdeki yordamları kullanın:</span><span class="sxs-lookup"><span data-stu-id="743f6-125">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="743f6-126">SharePoint hizmet hesabı altında çalıştığından emin olun</span><span class="sxs-lookup"><span data-stu-id="743f6-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="743f6-127">İlk olarak, SharePoint bir tanımlanmış hizmet hesabı altında--değil yerel sistem, yerel hizmet veya ağ hizmeti çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="743f6-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="743f6-128">Geçerli bir hesap için hizmet asıl adları (SPN) iliştirebilirsiniz böylece bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-128">Do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="743f6-129">SPN'ler Kerberos protokolü farklı hizmetleri nasıl tanımlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="743f6-129">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="743f6-130">Ve daha sonra KCD yapılandırmak için hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-130">And you will need the account later to configure the KCD.</span></span>

<span data-ttu-id="743f6-131">Sitelerinizi tanımlanmış hizmet hesabı altında çalıştığından emin olmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="743f6-131">To ensure that your sites are running under a defined service account, perform the following steps:</span></span>

1. <span data-ttu-id="743f6-132">Açık **SharePoint 2013 Yönetim Merkezi** site.</span><span class="sxs-lookup"><span data-stu-id="743f6-132">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="743f6-133">Git **güvenlik** seçip **hizmet hesaplarını yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="743f6-133">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="743f6-134">Seçin **Web uygulama havuzu - SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="743f6-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="743f6-135">Seçenekler, web havuzu adına göre biraz farklı olabilir veya web havuzu varsayılan olarak SSL kullanıyorsa.</span><span class="sxs-lookup"><span data-stu-id="743f6-135">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![Bir hizmet hesabı yapılandırma seçenekleri](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="743f6-137">Varsa **bu bileşen için bir hesap seçin** olan **yerel hizmet** veya **ağ hizmeti**, bir hesap oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="743f6-138">Değilse, tamamlanmış ve sonraki bölüme geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-138">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="743f6-139">Seçin **kaydı yeni yönetilen hesabı**.</span><span class="sxs-lookup"><span data-stu-id="743f6-139">Select **Register new managed account**.</span></span> <span data-ttu-id="743f6-140">Hesabınızı oluşturduktan sonra ayarlamalısınız **Web uygulama havuzu** hesabını kullanabilmeniz için.</span><span class="sxs-lookup"><span data-stu-id="743f6-140">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

> [!NOTE]
<span data-ttu-id="743f6-141">Daha önce oluşturulmuş olmasına gerek hizmeti için Azure AD hesabı.</span><span class="sxs-lookup"><span data-stu-id="743f6-141">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="743f6-142">Bir otomatik parola değişikliğini izin öneririz.</span><span class="sxs-lookup"><span data-stu-id="743f6-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="743f6-143">Adımları ve sorunlarını giderme tamamını hakkında daha fazla bilgi için bkz: [SharePoint 2013'te Otomatik parola değişikliği yapılandırma](https://technet.microsoft.com/library/ff724280.aspx).</span><span class="sxs-lookup"><span data-stu-id="743f6-143">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="743f6-144">Kerberos için SharePoint Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="743f6-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="743f6-145">Bu, yalnızca Kerberos ile çalışır ve çoklu oturum açma SharePoint sunucusuna gerçekleştirmek için KCD kullanın.</span><span class="sxs-lookup"><span data-stu-id="743f6-145">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="743f6-146">SharePoint siteniz için Kerberos kimlik doğrulamasını yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="743f6-146">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="743f6-147">Açık **SharePoint 2013 Yönetim Merkezi** site.</span><span class="sxs-lookup"><span data-stu-id="743f6-147">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="743f6-148">Git **Uygulama Yönetimi**seçin **web uygulamalarını yönetme**, SharePoint sitenizi seçin.</span><span class="sxs-lookup"><span data-stu-id="743f6-148">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="743f6-149">Bu örnek, **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="743f6-149">In this example, it is **SharePoint - 80**.</span></span>

  ![SharePoint sitesi seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="743f6-151">Tıklatın **kimlik doğrulama sağlayıcıları** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="743f6-151">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="743f6-152">İçinde **kimlik doğrulama sağlayıcıları** kutusunda, **varsayılan bölge** ayarlarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="743f6-152">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="743f6-153">İçinde **Düzenle kimlik doğrulama** iletişim kutusunda, görene kadar aşağı kaydırın **talep kimlik doğrulama türleri** ve emin her ikisi de **Windows kimlik doğrulamasını etkinleştir** ve **Tümleşik Windows kimlik doğrulaması** seçilir.</span><span class="sxs-lookup"><span data-stu-id="743f6-153">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="743f6-154">Aşağı açılan kutusunda olduğundan emin olun **Negotiate (Kerberos)** seçilir.</span><span class="sxs-lookup"><span data-stu-id="743f6-154">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![Kimlik doğrulama iletişim kutusunu Düzenle](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="743f6-156">Ekranın alt kısmındaki **kimlik doğrulamasını Düzenle** iletişim kutusu, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="743f6-156">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="743f6-157">SharePoint hizmet hesabı hizmet asıl adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="743f6-157">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="743f6-158">KCD yapılandırmadan önce yapılandırdığınız hizmet hesabı olarak çalışan SharePoint hizmeti tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-158">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="743f6-159">Bunun için bir SPN ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="743f6-159">You do this by setting an SPN.</span></span> <span data-ttu-id="743f6-160">Daha fazla bilgi için bkz: [hizmet asıl adları](https://technet.microsoft.com/library/cc961723.aspx).</span><span class="sxs-lookup"><span data-stu-id="743f6-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="743f6-161">SPN biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="743f6-161">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="743f6-162">SPN biçimi:</span><span class="sxs-lookup"><span data-stu-id="743f6-162">In the SPN format:</span></span>

* <span data-ttu-id="743f6-163">_hizmet sınıfı_ hizmeti için benzersiz bir addır.</span><span class="sxs-lookup"><span data-stu-id="743f6-163">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="743f6-164">SharePoint için kullandığınız **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="743f6-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="743f6-165">_ana bilgisayar_ tam etki alanı ya da hizmetini çalıştıran ana bilgisayarın NetBIOS adı.</span><span class="sxs-lookup"><span data-stu-id="743f6-165">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="743f6-166">Bir SharePoint sitesi için bu metni kullandığınız IIS sürümüne bağlı olarak site URL'sini olması gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="743f6-166">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="743f6-167">_bağlantı noktası_ isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="743f6-167">_port_ is optional.</span></span>

<span data-ttu-id="743f6-168">SharePoint sunucusu FQDN'si ise:</span><span class="sxs-lookup"><span data-stu-id="743f6-168">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="743f6-169">SPN sonra:</span><span class="sxs-lookup"><span data-stu-id="743f6-169">Then the SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="743f6-170">SPN'ler belirli siteleri için sunucunuzda ayarlamak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="743f6-170">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="743f6-171">Daha fazla bilgi için bkz: [yapılandırma Kerberos kimlik doğrulaması](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span><span class="sxs-lookup"><span data-stu-id="743f6-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="743f6-172">Kapat dikkat bölümüne "Kerberos kimlik doğrulaması kullanan Web uygulamalarınız için Create hizmet asıl adları."</span><span class="sxs-lookup"><span data-stu-id="743f6-172">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="743f6-173">SPN'ler ayarlamanızı en kolay yolu zaten siteleriniz için bulunabilecek SPN biçimleri izlemektir.</span><span class="sxs-lookup"><span data-stu-id="743f6-173">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="743f6-174">Karşı hizmet hesabını kaydetmek için bu SPN kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="743f6-174">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="743f6-175">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="743f6-175">To do this:</span></span>

1. <span data-ttu-id="743f6-176">SPN sitesiyle başka bir makineden göz atın.</span><span class="sxs-lookup"><span data-stu-id="743f6-176">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="743f6-177">Bunu yaptığınızda, Kerberos biletleri ilgili kümesini makinede önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="743f6-177">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="743f6-178">Bu biletleri için taranan hedef site SPN'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="743f6-178">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="743f6-179">Adlı bir araç kullanarak bu site için SPN çekebilir [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span><span class="sxs-lookup"><span data-stu-id="743f6-179">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="743f6-180">Siteyi tarayıcıda erişen kullanıcının aynı bağlamda çalışan bir komut penceresinde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="743f6-180">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="743f6-181">Klist sonra hedef SPN kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="743f6-181">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="743f6-182">Bu örnekte vurgulanmış gerekli olan SPN değeridir:</span><span class="sxs-lookup"><span data-stu-id="743f6-182">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![Örnek Klist sonuçları](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="743f6-184">SPN sahip olduğunuza göre bunu doğru şekilde daha önce web uygulaması için ayarladığınız hizmet hesabının yapılandırıldığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-184">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="743f6-185">Komut isteminden aşağıdaki komutu etki alanının yönetici olarak çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="743f6-185">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="743f6-186">Bu komut olarak çalışan SharePoint hizmet hesabı SPN'yi ayarlar _demo\sp_svc_.</span><span class="sxs-lookup"><span data-stu-id="743f6-186">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="743f6-187">Değiştir _http/sharepoint.demo.o365identity.us_ sunucunuz için SPN ile ve _demo\sp_svc_ , ortamınızdaki hizmet hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="743f6-187">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="743f6-188">Bunu eklemeden önce SPN'yi Setspn komut arar.</span><span class="sxs-lookup"><span data-stu-id="743f6-188">The Setspn command searches for the SPN before it adds it.</span></span> <span data-ttu-id="743f6-189">Bu durumda, görebileceğiniz bir **yinelenen SPN değeri** hata.</span><span class="sxs-lookup"><span data-stu-id="743f6-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="743f6-190">Bu hatayı görürseniz, değer hizmeti hesabı ile ilişkili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="743f6-190">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="743f6-191">SPN -m seçeneğiyle Setspn komutunu çalıştırarak eklendiğini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-191">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="743f6-192">Bu komut hakkında daha fazla bilgi için bkz: [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span><span class="sxs-lookup"><span data-stu-id="743f6-192">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="743f6-193">Bağlayıcı SharePoint'e güvenilen temsilci olarak ayarlandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="743f6-193">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="743f6-194">KCD, Azure AD uygulama proxy'si hizmeti kullanıcı kimlikleri SharePoint hizmetine devredebilirsiniz şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="743f6-194">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="743f6-195">Kullanıcılarınızın Azure AD içinde kimlik doğrulaması için Kerberos biletleri almak uygulama ara sunucusu Bağlayıcısı etkinleştirerek bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-195">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="743f6-196">Daha sonra sunucu bağlamı hedef uygulama ya da SharePoint için bu durumda geçirir.</span><span class="sxs-lookup"><span data-stu-id="743f6-196">Then that server passes the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="743f6-197">KCD yapılandırmak için her bağlayıcı makine için aşağıdaki adımları yineleyin:</span><span class="sxs-lookup"><span data-stu-id="743f6-197">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="743f6-198">Bir etki alanı denetleyicisinin etki alanı yöneticisi olarak oturum açın ve ardından açın **Active Directory Kullanıcıları ve Bilgisayarları**.</span><span class="sxs-lookup"><span data-stu-id="743f6-198">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="743f6-199">Bağlayıcı üzerinde çalıştığı bilgisayar bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="743f6-199">Find the computer that the connector is running on.</span></span> <span data-ttu-id="743f6-200">Bu örnekte, aynı SharePoint sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="743f6-200">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="743f6-201">Bilgisayarı çift tıklatın ve ardından **temsilci** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="743f6-201">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="743f6-202">Temsilci ayarları ayarlandığından emin olun **bu bilgisayara yalnızca belirtilen hizmetlere temsilci seçmek için güven**ve ardından **herhangi bir kimlik doğrulama protokolünü kullan**.</span><span class="sxs-lookup"><span data-stu-id="743f6-202">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![Temsilci ayarları](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="743f6-204">Tıklatın **Ekle** düğmesini tıklatın, **kullanıcılar veya bilgisayarlar**ve hizmet hesabını bulun.</span><span class="sxs-lookup"><span data-stu-id="743f6-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![Hizmet hesabı için SPN ekleme](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="743f6-206">SPN'ler listesinde, hizmet hesabı için daha önce oluşturduğunuz bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="743f6-206">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="743f6-207">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743f6-207">Click **OK**.</span></span> <span data-ttu-id="743f6-208">Tıklatın **Tamam** yeniden değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="743f6-208">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="743f6-209">2. adım: SharePoint için uzaktan erişimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="743f6-209">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="743f6-210">Kerberos ve yapılandırılmış KCD için SharePoint etkinleştirdikten, çoklu oturum açma SharePoint'e ayarlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="743f6-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span></span> <span data-ttu-id="743f6-211">Ardından bir bağlayıcı, SharePoint grubu Azure AD uygulama proxy'si aracılığıyla uzaktan erişim için yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-211">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="743f6-212">Aşağıdaki adımları gerçekleştirmek için kuruluşunuzun Azure Active Directory hesabında genel yönetici rolünün bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-212">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="743f6-213">Oturum [Azure portal](https://manage.windowsazure.com) ve Azure AD kiracınıza bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-213">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="743f6-214">Tıklatın **uygulamaları**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="743f6-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="743f6-215">**Publish an application that will be accessible from outside your network (Ağınızın dışından erişilebilecek olan bir uygulamayı yayımlama)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="743f6-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="743f6-216">Bu seçeneği görmüyorsanız, Azure AD temel sahip veya Kiracı Premium ayarlanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="743f6-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span></span>
4. <span data-ttu-id="743f6-217">Seçeneklerin her biri aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="743f6-217">Complete each of the options as follows:</span></span>
 * <span data-ttu-id="743f6-218">**Ad**:--Örneğin, istediğiniz herhangi bir değer kullanmak **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="743f6-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="743f6-219">**İç URL**: SharePoint site URL'sidir dahili olarak gibi **https://SharePoint/**.</span><span class="sxs-lookup"><span data-stu-id="743f6-219">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="743f6-220">Bu örnekte, kullandığınızdan emin olun **https**.</span><span class="sxs-lookup"><span data-stu-id="743f6-220">In this example, make sure to use **https**.</span></span>
 * <span data-ttu-id="743f6-221">**Ön kimlik doğrulama yöntemi**: seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="743f6-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![Bir uygulama eklemek için Seçenekler](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="743f6-223">Uygulama yayımlandıktan sonra tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="743f6-223">After the app is published, click the **Configure** tab.</span></span>
6. <span data-ttu-id="743f6-224">Seçeneğine kaydırın **üstbilgileri Çevir URL'de**.</span><span class="sxs-lookup"><span data-stu-id="743f6-224">Scroll down to the option **Translate URL in Headers**.</span></span> <span data-ttu-id="743f6-225">Varsayılan değer **Evet**.</span><span class="sxs-lookup"><span data-stu-id="743f6-225">The default value is **YES**.</span></span> <span data-ttu-id="743f6-226">Şekilde değiştirin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="743f6-226">Change it to **NO**.</span></span>

 <span data-ttu-id="743f6-227">SharePoint kullanan _ana bilgisayar üstbilgisi_ siteyi aramak için değer.</span><span class="sxs-lookup"><span data-stu-id="743f6-227">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="743f6-228">Aynı zamanda bu değere göre bağlantılar da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="743f6-228">It also generates links based on this value.</span></span> <span data-ttu-id="743f6-229">Net etkisi, SharePoint oluşturur herhangi bir bağlantıyı dış URL'yi kullanmak üzere doğru şekilde ayarlanmış bir yayımlanan URL olduğundan emin olmaktır.</span><span class="sxs-lookup"><span data-stu-id="743f6-229">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="743f6-230">Ayar değeri **Evet** Ayrıca arka uç uygulama isteği iletmek bağlayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="743f6-230">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="743f6-231">Ancak, ayar değeri **Hayır** bağlayıcı iç ana bilgisayar adını göndermez anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="743f6-231">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="743f6-232">Bunun yerine, ana bilgisayar üstbilgisi bağlayıcı arka uç uygulaması için yayımlanan URL olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="743f6-232">Instead, the connector sends the host header as the published URL to the back-end application.</span></span>

 <span data-ttu-id="743f6-233">Ayrıca, SharePoint bu URL'yi kabul etmesini sağlamak için SharePoint sunucusu üzerindeki bir daha fazla yapılandırmayı tamamlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="743f6-233">Also, to ensure that SharePoint accepts this URL, you need to complete one more configuration on the SharePoint server.</span></span> <span data-ttu-id="743f6-234">Bu sonraki bölümde gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-234">You'll do that in the next section.</span></span>

7. <span data-ttu-id="743f6-235">Değişiklik **iç kimlik doğrulama yöntemini** için **tümleşik Windows kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="743f6-235">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span></span> <span data-ttu-id="743f6-236">Azure AD kiracınıza UPN şirket içinden farklı bulutta UPN kullanıyorsa, güncelleştirmeyi unutmayın **oturum açma kimlik temsilcisi** de.</span><span class="sxs-lookup"><span data-stu-id="743f6-236">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="743f6-237">Ayarlama **iç uygulama SPN** daha önce belirlediğiniz değeri.</span><span class="sxs-lookup"><span data-stu-id="743f6-237">Set **Internal Application SPN** to the value that you set earlier.</span></span> <span data-ttu-id="743f6-238">Örneğin, **http/sharepoint.demo.o365identity.us**.</span><span class="sxs-lookup"><span data-stu-id="743f6-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="743f6-239">Hedef kullanıcılarınızın uygulamaya atayın.</span><span class="sxs-lookup"><span data-stu-id="743f6-239">Assign the application to your target users.</span></span>

<span data-ttu-id="743f6-240">Uygulamanızı aşağıdaki örneğe benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="743f6-240">Your application should look similar to the following example:</span></span>

  ![Tamamlanan uygulama](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="743f6-242">Adım 3: SharePoint dış URL hakkında bilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="743f6-242">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="743f6-243">Böylece, dış URL temel alınarak bağlantılar kılacak SharePoint dış URL temel alınarak site bulabilirsiniz emin olmak için son adımı.</span><span class="sxs-lookup"><span data-stu-id="743f6-243">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="743f6-244">Bunun için SharePoint sitesi için diğer erişim eşleşmeleri yapılandırarak.</span><span class="sxs-lookup"><span data-stu-id="743f6-244">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="743f6-245">Açık **SharePoint 2013 Yönetim Merkezi** site.</span><span class="sxs-lookup"><span data-stu-id="743f6-245">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="743f6-246">Altında **sistem ayarlarını**seçin **yapılandırma diğer erişim eşleşmeleri**.</span><span class="sxs-lookup"><span data-stu-id="743f6-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="743f6-247">Bu açılır **diğer erişim eşleşmeleri** kutusu.</span><span class="sxs-lookup"><span data-stu-id="743f6-247">This opens the **Alternate Access Mappings** box.</span></span>

  ![Diğer erişim eşleşmeleri kutusu](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="743f6-249">Aşağı açılan listesinde **alternatif erişim eşleme koleksiyonu**seçin **değişiklik alternatif erişim eşleme koleksiyonu**.</span><span class="sxs-lookup"><span data-stu-id="743f6-249">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="743f6-250">Örneğin, siteniz--seçin **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="743f6-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![Bir site seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="743f6-252">Bir iç URL veya genel bir URL olarak yayımlanan URL'ye eklemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-252">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="743f6-253">Bu örnek genel bir URL extranet kullanır.</span><span class="sxs-lookup"><span data-stu-id="743f6-253">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="743f6-254">' I tıklatın **Düzenle ortak URL'leri** içinde **Extranet** yolu, önceki adımda olduğu gibi yayımlanan uygulama için yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="743f6-254">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span></span> <span data-ttu-id="743f6-255">Örneğin **https://sharepoint-iddemo.msappproxy.net**.</span><span class="sxs-lookup"><span data-stu-id="743f6-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![Yolun girme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="743f6-257">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="743f6-257">Click **Save**.</span></span>

 <span data-ttu-id="743f6-258">Artık Azure AD uygulama proxy'si aracılığıyla harici olarak SharePoint sitesine erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="743f6-258">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="743f6-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="743f6-259">Next steps</span></span>

- [<span data-ttu-id="743f6-260">Şirket içi uygulamalara güvenli uzaktan erişim sağlama</span><span class="sxs-lookup"><span data-stu-id="743f6-260">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="743f6-261">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="743f6-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="743f6-262">SharePoint 2016 ve Office Online Server Azure AD uygulama proxy'si ile uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="743f6-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
