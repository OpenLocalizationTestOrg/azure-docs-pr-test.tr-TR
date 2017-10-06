---
title: "Azure AD uygulama proxy'si ile aaaEnable uzaktan erişim tooSharePoint | Microsoft Docs"
description: "Merhaba ile nasıl ilgili temel bilgileri kapsayan toointegrate Azure AD uygulama proxy'si ile bir şirket içi SharePoint server."
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
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="fe846-103">Azure AD uygulama proxy'si ile uzaktan erişim tooSharePoint etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fe846-103">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="fe846-104">Bu makalede ele nasıl toointegrate Azure Active Directory (Azure AD) uygulama ara sunucusu ile bir şirket içi SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="fe846-104">This article discusses how toointegrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="fe846-105">Azure AD uygulama proxy'si ile tooenable uzaktan erişim tooSharePoint bu makalede adım adım hello bölümlerde izleyin.</span><span class="sxs-lookup"><span data-stu-id="fe846-105">tooenable remote access tooSharePoint with Azure AD Application Proxy, follow hello sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe846-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe846-106">Prerequisites</span></span>

<span data-ttu-id="fe846-107">Bu makalede, ortamınızda SharePoint 2013 veya daha yeni zaten sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="fe846-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="fe846-108">Ayrıca, aşağıdaki önkoşullar hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="fe846-108">In addition, consider hello following prerequisites:</span></span>

* <span data-ttu-id="fe846-109">SharePoint yerel Kerberos desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="fe846-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="fe846-110">Bu nedenle, iç siteleri Azure AD uygulama proxy'si aracılığıyla uzaktan erişen kullanıcılar bir tek oturum açma (SSO) deneyimi toohave varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume toohave a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="fe846-111">Toomake birkaç yapılandırma değişiklikleri tooyour SharePoint sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-111">You need toomake a few configuration changes tooyour SharePoint server.</span></span> <span data-ttu-id="fe846-112">Hazırlama ortamında kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="fe846-112">We recommend using a staging environment.</span></span> <span data-ttu-id="fe846-113">Bu şekilde, sunucu ilk hazırlama güncelleştirmeleri tooyour olun ve sonra üretime geçmeden önce bir test döngüsü kolaylaştırmak.</span><span class="sxs-lookup"><span data-stu-id="fe846-113">This way, you can make updates tooyour staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="fe846-114">URL hello SSL yayımlanan gerektirdiği için SharePoint için SSL kurma zaten ayarladığınızdan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="fe846-114">We assume that you have already set up SSL for SharePoint, because we require SSL on hello published URL.</span></span> <span data-ttu-id="fe846-115">SSL etkin toohave bağlantılar gönderilen/doğru eşleştirildiğini olduğunu tooensure, iç sitenizin gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-115">You need toohave SSL enabled on your internal site, tooensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="fe846-116">SSL yapılandırmadıysanız bkz [SharePoint 2013 için SSL yapılandırma](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="fe846-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="fe846-117">Ayrıca, dağıttığınız bu hello bağlayıcı makine güvenleri hello sertifika emin olun.</span><span class="sxs-lookup"><span data-stu-id="fe846-117">Also, make sure that hello connector machine trusts hello certificate that you issue.</span></span> <span data-ttu-id="fe846-118">(genel olarak verilen toobe hello sertifika gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="fe846-118">(hello certificate does not need toobe publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a><span data-ttu-id="fe846-119">1. adım: Tek oturum açma tooSharePoint ayarlama</span><span class="sxs-lookup"><span data-stu-id="fe846-119">Step 1: Set up single sign-on tooSharePoint</span></span>

<span data-ttu-id="fe846-120">Müşterilerimizin en iyi SSO bir deneyim arka uç için kendi uygulamalarında, SharePoint sunucu bu durumda hello istiyor.</span><span class="sxs-lookup"><span data-stu-id="fe846-120">Our customers want hello best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="fe846-121">Yeniden kimlik doğrulaması için istenmez çünkü bu ortak Azure AD senaryoda hello kullanıcı yalnızca bir kez kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="fe846-121">In this common Azure AD scenario, hello user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="fe846-122">Gerektiren veya Windows kimlik doğrulaması kullanan şirket içi uygulamalar için SSO hello Kerberos kimlik doğrulama protokolünü ve kısıtlı Kerberos temsilci (KCD) adlı bir özellik kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using hello Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="fe846-123">Yapılandırıldığında, KCD, bir windows hello uygulama Proxy Bağlayıcısı tooobtain sağlayan hello kullanıcı tooWindows içinde doğrudan oturum kurmadı olsa bile bilet/belirtecin bir kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="fe846-123">KCD, when configured, allows hello Application Proxy connector tooobtain a windows ticket/token for a user, even if hello user hasn’t signed in tooWindows directly.</span></span> <span data-ttu-id="fe846-124">KCD, hakkında daha fazla toolearn bkz [Kerberos Kısıtlı temsilci genel bakış](https://technet.microsoft.com/library/jj553400.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe846-124">toolearn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="fe846-125">bir SharePoint sunucusu için kullanım hello hello sıralı bölümleri aşağıdaki yordamlarda tooset KCD Yukarı:</span><span class="sxs-lookup"><span data-stu-id="fe846-125">tooset up KCD for a SharePoint server, use hello procedures in hello following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="fe846-126">SharePoint hizmet hesabı altında çalıştığından emin olun</span><span class="sxs-lookup"><span data-stu-id="fe846-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="fe846-127">İlk olarak, SharePoint bir tanımlanmış hizmet hesabı altında--değil yerel sistem, yerel hizmet veya ağ hizmeti çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fe846-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="fe846-128">Hizmet asıl adları (SPN) tooa geçerli hesabı iliştirebilirsiniz böylece bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-128">Do this so that you can attach service principal names (SPNs) tooa valid account.</span></span> <span data-ttu-id="fe846-129">SPN'ler nasıl hello Kerberos protokolü farklı hizmetleri tanımlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="fe846-129">SPNs are how hello Kerberos protocol identifies different services.</span></span> <span data-ttu-id="fe846-130">Ve hesap hello sonraki tooconfigure hello KCD.</span><span class="sxs-lookup"><span data-stu-id="fe846-130">And you will need hello account later tooconfigure hello KCD.</span></span>

<span data-ttu-id="fe846-131">sitelerinizin tanımlanmış hizmet hesabı altında çalışan tooensure hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fe846-131">tooensure that your sites are running under a defined service account, perform hello following steps:</span></span>

1. <span data-ttu-id="fe846-132">Açık hello **SharePoint 2013 Yönetim Merkezi** site.</span><span class="sxs-lookup"><span data-stu-id="fe846-132">Open hello **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="fe846-133">Çok Git**güvenlik** seçip **hizmet hesaplarını yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="fe846-133">Go too**Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="fe846-134">Seçin **Web uygulama havuzu - SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="fe846-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="fe846-135">Merhaba web havuzu SSL varsayılan olarak kullanıyorsa veya Hello seçenekleri hello web havuzu adına göre biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe846-135">hello options may be slightly different based on hello name of your web pool, or if hello web pool uses SSL by default.</span></span>

  ![Bir hizmet hesabı yapılandırma seçenekleri](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="fe846-137">Varsa **bu bileşen için bir hesap seçin** olan **yerel hizmet** veya **ağ hizmeti**, toocreate bir hesap gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need toocreate an account.</span></span> <span data-ttu-id="fe846-138">Değilse, tamamlanmış ve toohello sonraki bölüme geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-138">If not, you're finished and can move toohello next section.</span></span>
5. <span data-ttu-id="fe846-139">Seçin **kaydı yeni yönetilen hesabı**.</span><span class="sxs-lookup"><span data-stu-id="fe846-139">Select **Register new managed account**.</span></span> <span data-ttu-id="fe846-140">Hesabınızı oluşturduktan sonra ayarlamalısınız **Web uygulama havuzu** hello hesabını kullanabilmeniz için.</span><span class="sxs-lookup"><span data-stu-id="fe846-140">After your account is created, you must set **Web Application Pool** before you can use hello account.</span></span>

> [!NOTE]
<span data-ttu-id="fe846-141">Daha önce bir toohave ihtiyacınız hello hizmeti için Azure AD hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="fe846-141">You need toohave a previously created Azure AD account for hello service.</span></span> <span data-ttu-id="fe846-142">Bir otomatik parola değişikliğini izin öneririz.</span><span class="sxs-lookup"><span data-stu-id="fe846-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="fe846-143">Adımları ve sorunlarını giderme hello tam kümesi hakkında daha fazla bilgi için bkz: [SharePoint 2013'te Otomatik parola değişikliği yapılandırma](https://technet.microsoft.com/library/ff724280.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe846-143">For more information about hello full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="fe846-144">Kerberos için SharePoint Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fe846-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="fe846-145">KCD tooperform tek oturum açma toohello SharePoint server kullanın ve bu, yalnızca Kerberos ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="fe846-145">You use KCD tooperform single sign-on toohello SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="fe846-146">SharePoint sitesi için Kerberos kimlik doğrulamasını tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="fe846-146">tooconfigure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="fe846-147">Açık hello **SharePoint 2013 Yönetim Merkezi** site.</span><span class="sxs-lookup"><span data-stu-id="fe846-147">Open hello **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="fe846-148">Çok Git**Uygulama Yönetimi**seçin **web uygulamalarını yönetme**, SharePoint sitenizi seçin.</span><span class="sxs-lookup"><span data-stu-id="fe846-148">Go too**Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="fe846-149">Bu örnek, **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="fe846-149">In this example, it is **SharePoint - 80**.</span></span>

  ![Merhaba SharePoint sitesi seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="fe846-151">Tıklatın **kimlik doğrulama sağlayıcıları** hello araç.</span><span class="sxs-lookup"><span data-stu-id="fe846-151">Click **Authentication Providers** on hello toolbar.</span></span>
4. <span data-ttu-id="fe846-152">Merhaba, **kimlik doğrulama sağlayıcıları** kutusunda, **varsayılan bölge** tooview hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="fe846-152">In hello **Authentication Providers** box, click **Default Zone** tooview hello settings.</span></span>
5. <span data-ttu-id="fe846-153">Merhaba, **kimlik doğrulamasını Düzenle** iletişim kutusunda, görene kadar aşağı kaydırın **talep kimlik doğrulama türleri** ve emin olun her ikisi de **Windows kimlik doğrulamasını etkinleştir** ve ** Tümleşik Windows kimlik doğrulaması** seçilir.</span><span class="sxs-lookup"><span data-stu-id="fe846-153">In hello **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="fe846-154">Merhaba açılan kutusunda olduğundan emin olun **Negotiate (Kerberos)** seçilir.</span><span class="sxs-lookup"><span data-stu-id="fe846-154">In hello drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![Kimlik doğrulama iletişim kutusunu Düzenle](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="fe846-156">Merhaba hello sonundaki **kimlik doğrulamasını Düzenle** iletişim kutusu, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fe846-156">At hello bottom of hello **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a><span data-ttu-id="fe846-157">Merhaba SharePoint hizmet hesabı için bir hizmet asıl adını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="fe846-157">Set a service principal name for hello SharePoint service account</span></span>

<span data-ttu-id="fe846-158">Merhaba KCD yapılandırmadan önce yapılandırdığınız hello hizmet hesabı olarak çalışan tooidentify hello SharePoint hizmeti gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-158">Before you configure hello KCD, you need tooidentify hello SharePoint service running as hello service account that you've configured.</span></span> <span data-ttu-id="fe846-159">Bunun için bir SPN ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="fe846-159">You do this by setting an SPN.</span></span> <span data-ttu-id="fe846-160">Daha fazla bilgi için bkz: [hizmet asıl adları](https://technet.microsoft.com/library/cc961723.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe846-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="fe846-161">Merhaba SPN biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fe846-161">hello SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="fe846-162">Merhaba SPN biçimde:</span><span class="sxs-lookup"><span data-stu-id="fe846-162">In hello SPN format:</span></span>

* <span data-ttu-id="fe846-163">_hizmet sınıfı_ hello hizmeti için benzersiz bir addır.</span><span class="sxs-lookup"><span data-stu-id="fe846-163">_service class_ is a unique name for hello service.</span></span> <span data-ttu-id="fe846-164">SharePoint için kullandığınız **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="fe846-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="fe846-165">_ana bilgisayar_ hello tam etki alanı veya hizmet hello hello ana bilgisayarın NetBIOS adını çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="fe846-165">_host_ is hello fully qualified domain or NetBIOS name of hello host that hello service is running on.</span></span> <span data-ttu-id="fe846-166">Bir SharePoint sitesi için bu metni toobe hello kullanmakta olduğunuz IIS hello sürümüne bağlı olarak hello site URL'sini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="fe846-166">For a SharePoint site, this text might need toobe hello URL of hello site, depending on hello version of IIS that you're using.</span></span>

* <span data-ttu-id="fe846-167">_bağlantı noktası_ isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fe846-167">_port_ is optional.</span></span>

<span data-ttu-id="fe846-168">Merhaba hello SharePoint sunucusunun FQDN'si ise:</span><span class="sxs-lookup"><span data-stu-id="fe846-168">If hello FQDN of hello SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="fe846-169">Merhaba SPN ise:</span><span class="sxs-lookup"><span data-stu-id="fe846-169">Then hello SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="fe846-170">Ayrıca, belirli siteler için sunucunuzda tooset SPN'ler gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="fe846-170">You might also need tooset SPNs for specific sites on your server.</span></span> <span data-ttu-id="fe846-171">Daha fazla bilgi için bkz: [yapılandırma Kerberos kimlik doğrulaması](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span><span class="sxs-lookup"><span data-stu-id="fe846-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="fe846-172">Kapat dikkat toohello bölüm ödeme "Kerberos kimlik doğrulaması kullanan Web uygulamalarınız için Create hizmet asıl adları."</span><span class="sxs-lookup"><span data-stu-id="fe846-172">Pay close attention toohello section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="fe846-173">Merhaba kolay SPN'ler tooset için zaten siteleriniz için bulunabilecek toofollow hello SPN biçimleri yoludur.</span><span class="sxs-lookup"><span data-stu-id="fe846-173">hello easiest way for you tooset SPNs is toofollow hello SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="fe846-174">Bu SPN'ler tooregister hello hizmet hesabı karşı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="fe846-174">Copy those SPNs tooregister against hello service account.</span></span> <span data-ttu-id="fe846-175">toodo bu:</span><span class="sxs-lookup"><span data-stu-id="fe846-175">toodo this:</span></span>

1. <span data-ttu-id="fe846-176">Başka bir makineden hello SPN toohello sitesiyle göz atın.</span><span class="sxs-lookup"><span data-stu-id="fe846-176">Browse toohello site with hello SPN from another machine.</span></span>
 <span data-ttu-id="fe846-177">Merhaba olduğunda Kerberos biletleri ilgili kümesi hello makinede önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="fe846-177">When you do, hello relevant set of Kerberos tickets is cached on hello machine.</span></span> <span data-ttu-id="fe846-178">Bu biletler hello için taranan hello hedef site SPN'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="fe846-178">These tickets contain hello SPN of hello target site that you browsed to.</span></span>

2. <span data-ttu-id="fe846-179">Adlı bir araç kullanarak bu site için SPN hello çekebilir [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span><span class="sxs-lookup"><span data-stu-id="fe846-179">You can pull hello SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="fe846-180">Hello çalışan bir komut penceresinde hello tarayıcıda erişilen hello siteyi çalıştırın hello kullanıcısı olarak aynı bağlam hello komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="fe846-180">In a command window that's running in hello same context as hello user who accessed hello site in hello browser, run hello following command:</span></span>
```
Klist
```
<span data-ttu-id="fe846-181">Klist sonra hedef SPN hello kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fe846-181">Klist then returns hello set of target SPNs.</span></span> <span data-ttu-id="fe846-182">Bu örnekte vurgulanmış hello hello gerekli olan SPN değeridir:</span><span class="sxs-lookup"><span data-stu-id="fe846-182">In this example, hello highlighted value is hello SPN that's needed:</span></span>

  ![Örnek Klist sonuçları](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="fe846-184">Merhaba SPN sahip olduğunuza göre bunu doğru şekilde önceki hello web uygulaması için ayarladığınız hello hizmet hesabının yapılandırıldığından emin toomake gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-184">Now that you have hello SPN, you need toomake sure that it's configured correctly on hello service account that you set up for hello web application earlier.</span></span> <span data-ttu-id="fe846-185">Komut hello komut isteminden hello etki alanının yönetici olarak aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe846-185">Run hello following command from hello command prompt as an administrator of hello domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="fe846-186">Ayarlar hello SPN hello SharePoint hizmeti için bu komutu hesabı olarak çalışan _demo\sp_svc_.</span><span class="sxs-lookup"><span data-stu-id="fe846-186">This command sets hello SPN for hello SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="fe846-187">Değiştir _http/sharepoint.demo.o365identity.us_ hello SPN sunucunuz için sahip ve _demo\sp_svc_ ortamınızdaki hello hizmet hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="fe846-187">Replace _http/sharepoint.demo.o365identity.us_ with hello SPN for your server and _demo\sp_svc_ with hello service account in your environment.</span></span> <span data-ttu-id="fe846-188">Bunu eklemeden önce hello Setspn komut Merhaba SPN arar.</span><span class="sxs-lookup"><span data-stu-id="fe846-188">hello Setspn command searches for hello SPN before it adds it.</span></span> <span data-ttu-id="fe846-189">Bu durumda, görebileceğiniz bir **yinelenen SPN değeri** hata.</span><span class="sxs-lookup"><span data-stu-id="fe846-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="fe846-190">Bu hatayı görürseniz, hello değeri hello hizmeti hesabı ile ilişkili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fe846-190">If you see this error, make sure that hello value is associated with hello service account.</span></span>

<span data-ttu-id="fe846-191">SPN hello -m seçeneğiyle hello Setspn komutunu çalıştırarak eklendi bu hello doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-191">You can verify that hello SPN was added by running hello Setspn command with hello -l option.</span></span> <span data-ttu-id="fe846-192">Bu komut hakkında daha fazla toolearn bkz [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe846-192">toolearn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a><span data-ttu-id="fe846-193">Bu hello bağlayıcı güvenilen temsilci tooSharePoint ayarlandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="fe846-193">Ensure that hello connector is set as a trusted delegate tooSharePoint</span></span>

<span data-ttu-id="fe846-194">Merhaba KCD Hello Azure AD uygulama proxy'si hizmeti kullanıcı kimlikleri toohello SharePoint hizmeti temsilci seçebilirsiniz şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fe846-194">Configure hello KCD so that hello Azure AD Application Proxy service can delegate user identities toohello SharePoint service.</span></span> <span data-ttu-id="fe846-195">Merhaba uygulama ara sunucusu Bağlayıcısı etkinleştirerek tooretrieve Kerberos biletleri için Azure AD içinde kimlik doğrulaması, kullanıcılar bunu.</span><span class="sxs-lookup"><span data-stu-id="fe846-195">You do this by enabling hello Application Proxy connector tooretrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="fe846-196">Daha sonra sunucu hello bağlam toohello hedef uygulama ya da SharePoint bu durumda geçirir.</span><span class="sxs-lookup"><span data-stu-id="fe846-196">Then that server passes hello context toohello target application, or SharePoint in this case.</span></span>

<span data-ttu-id="fe846-197">tooconfigure hello KCD, aşağıdaki adımları her bağlayıcı makine yineleme hello:</span><span class="sxs-lookup"><span data-stu-id="fe846-197">tooconfigure hello KCD, repeat hello following steps for each connector machine:</span></span>

1. <span data-ttu-id="fe846-198">Bir etki alanı yönetici tooa DC oturum açın ve ardından açın **Active Directory Kullanıcıları ve Bilgisayarları**.</span><span class="sxs-lookup"><span data-stu-id="fe846-198">Log in as a domain administrator tooa DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="fe846-199">Bağlayıcı hello hello bilgisayarın çalışıp çalışmadığını bulun.</span><span class="sxs-lookup"><span data-stu-id="fe846-199">Find hello computer that hello connector is running on.</span></span> <span data-ttu-id="fe846-200">Bu örnekte, onu sahip hello aynı SharePoint sunucusu.</span><span class="sxs-lookup"><span data-stu-id="fe846-200">In this example, it's hello same SharePoint server.</span></span>
3. <span data-ttu-id="fe846-201">Merhaba bilgisayarı çift tıklatın ve hello ardından **temsilci** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fe846-201">Double-click hello computer, and then click hello **Delegation** tab.</span></span>
4. <span data-ttu-id="fe846-202">Merhaba temsilci ayarları çok ayarlandığından emin olun**belirtilen temsilci toohello bu bilgisayara güven yalnızca Hizmetleri**ve ardından **herhangi bir kimlik doğrulama protokolünü kullan**.</span><span class="sxs-lookup"><span data-stu-id="fe846-202">Ensure that hello delegation settings are set too**Trust this computer for delegation toohello specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![Temsilci ayarları](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="fe846-204">Merhaba tıklatın **Ekle** düğmesini tıklatın, **kullanıcılar veya bilgisayarlar**ve hello hizmet hesabını bulun.</span><span class="sxs-lookup"><span data-stu-id="fe846-204">Click hello **Add** button, click **Users or Computers**, and locate hello service account.</span></span>

  ![Merhaba hizmet hesabı için SPN ekleme hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="fe846-206">SPN'ler Hello listesinde hello hello hizmet hesabı için daha önce oluşturduğunuz birini seçin.</span><span class="sxs-lookup"><span data-stu-id="fe846-206">In hello list of SPNs, select hello one that you created earlier for hello service account.</span></span>
7. <span data-ttu-id="fe846-207">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe846-207">Click **OK**.</span></span> <span data-ttu-id="fe846-208">Tıklatın **Tamam** yeniden toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="fe846-208">Click **OK** again toosave hello changes.</span></span>

## <a name="step-2-enable-remote-access-toosharepoint"></a><span data-ttu-id="fe846-209">2. adım: uzaktan erişim tooSharePoint etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fe846-209">Step 2: Enable remote access tooSharePoint</span></span>

<span data-ttu-id="fe846-210">SharePoint için Kerberos etkinleştirilmiş ve yapılandırılmış KCD göre tek oturum açma tooSharePoint yukarı hazır tooset demektir.</span><span class="sxs-lookup"><span data-stu-id="fe846-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready tooset up single sign-on tooSharePoint.</span></span> <span data-ttu-id="fe846-211">Ardından hello bağlayıcısından hello SharePoint grubu Azure AD uygulama proxy'si aracılığıyla uzaktan erişim için yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-211">Then from hello connector, you can publish hello SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="fe846-212">tooperform hello adımları izleyerek toobe kuruluşunuzun Azure Active Directory hesabı hello genel yönetici rolü üyesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-212">tooperform hello following steps, you need toobe a member of hello Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="fe846-213">İçinde toohello oturum [Azure portal](https://manage.windowsazure.com) ve Azure AD kiracınıza bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-213">Sign in toohello [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="fe846-214">Tıklatın **uygulamaları**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="fe846-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="fe846-215">**Publish an application that will be accessible from outside your network (Ağınızın dışından erişilebilecek olan bir uygulamayı yayımlama)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="fe846-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="fe846-216">Bu seçeneği görmüyorsanız, Azure AD temel sahip veya Premium hello Kiracı içinde ayarlanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fe846-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in hello tenant.</span></span>
4. <span data-ttu-id="fe846-217">Merhaba seçeneklerin her biri aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="fe846-217">Complete each of hello options as follows:</span></span>
 * <span data-ttu-id="fe846-218">**Ad**:--Örneğin, istediğiniz herhangi bir değer kullanmak **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="fe846-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="fe846-219">**İç URL**: hello hello SharePoint sitesinin URL'sini budur dahili olarak gibi **https://SharePoint/**.</span><span class="sxs-lookup"><span data-stu-id="fe846-219">**Internal URL**: This is hello URL of hello SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="fe846-220">Bu örnekte, emin toouse olun **https**.</span><span class="sxs-lookup"><span data-stu-id="fe846-220">In this example, make sure toouse **https**.</span></span>
 * <span data-ttu-id="fe846-221">**Ön kimlik doğrulama yöntemi**: seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe846-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![Bir uygulama eklemek için Seçenekler](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="fe846-223">Merhaba uygulama yayımlandıktan sonra hello tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fe846-223">After hello app is published, click hello **Configure** tab.</span></span>
6. <span data-ttu-id="fe846-224">Toohello seçeneği aşağı **üstbilgileri Çevir URL'de**.</span><span class="sxs-lookup"><span data-stu-id="fe846-224">Scroll down toohello option **Translate URL in Headers**.</span></span> <span data-ttu-id="fe846-225">Merhaba varsayılan değer **Evet**.</span><span class="sxs-lookup"><span data-stu-id="fe846-225">hello default value is **YES**.</span></span> <span data-ttu-id="fe846-226">Çok değiştirme**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="fe846-226">Change it too**NO**.</span></span>

 <span data-ttu-id="fe846-227">SharePoint kullanan hello _ana bilgisayar üstbilgisi_ değeri toolook hello site.</span><span class="sxs-lookup"><span data-stu-id="fe846-227">SharePoint uses hello _Host Header_ value toolook up hello site.</span></span> <span data-ttu-id="fe846-228">Aynı zamanda bu değere göre bağlantılar da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe846-228">It also generates links based on this value.</span></span> <span data-ttu-id="fe846-229">Merhaba net etkisi toomake SharePoint oluşturur herhangi bir bağlantıyı toouse hello dış URL doğru olarak ayarlanmış bir yayımlanan URL olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="fe846-229">hello net effect is toomake sure that any link that SharePoint generates is a published URL that is correctly set toouse hello external URL.</span></span> <span data-ttu-id="fe846-230">Ayar Hello değeri çok**Evet** de etkinleştirir bağlayıcı tooforward hello isteği toohello arka uç uygulaması hello.</span><span class="sxs-lookup"><span data-stu-id="fe846-230">Setting hello value too**YES** also enables hello connector tooforward hello request toohello back-end application.</span></span> <span data-ttu-id="fe846-231">Ancak, hello değeri çok ayarı**Hayır** bağlayıcı hello anlamına gelir hello iç ana bilgisayar adı değil gönderecek.</span><span class="sxs-lookup"><span data-stu-id="fe846-231">However, setting hello value too**NO** means that hello connector will not send hello internal host name.</span></span> <span data-ttu-id="fe846-232">Bunun yerine, URL toohello arka uç uygulaması Hello yayımlanmış olarak hello bağlayıcı hello ana bilgisayar üstbilgisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="fe846-232">Instead, hello connector sends hello host header as hello published URL toohello back-end application.</span></span>

 <span data-ttu-id="fe846-233">Ayrıca, tooensure SharePoint kabul eder, bu URL, toocomplete hello SharePoint sunucusundaki bir daha fazla yapılandırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe846-233">Also, tooensure that SharePoint accepts this URL, you need toocomplete one more configuration on hello SharePoint server.</span></span> <span data-ttu-id="fe846-234">Bu hello sonraki bölümde gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-234">You'll do that in hello next section.</span></span>

7. <span data-ttu-id="fe846-235">Değişiklik **iç kimlik doğrulama yöntemini** çok**tümleşik Windows kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="fe846-235">Change **Internal Authentication Method** too**Integrated Windows Authentication**.</span></span> <span data-ttu-id="fe846-236">Azure AD kiracınıza hello UPN şirket içinden farklı hello bulutta UPN kullanıyorsa, tooupdate unutmayın **oturum açma kimlik temsilcisi** de.</span><span class="sxs-lookup"><span data-stu-id="fe846-236">If your Azure AD tenant uses a UPN in hello cloud that's different from hello UPN on-premises, remember tooupdate **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="fe846-237">Ayarlama **iç uygulama SPN** daha önce belirlediğiniz toohello değeri.</span><span class="sxs-lookup"><span data-stu-id="fe846-237">Set **Internal Application SPN** toohello value that you set earlier.</span></span> <span data-ttu-id="fe846-238">Örneğin, **http/sharepoint.demo.o365identity.us**.</span><span class="sxs-lookup"><span data-stu-id="fe846-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="fe846-239">Merhaba uygulama tooyour hedef kullanıcılar atayın.</span><span class="sxs-lookup"><span data-stu-id="fe846-239">Assign hello application tooyour target users.</span></span>

<span data-ttu-id="fe846-240">Uygulamanızı benzer toohello örnek aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fe846-240">Your application should look similar toohello following example:</span></span>

  ![Tamamlanan uygulama](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a><span data-ttu-id="fe846-242">Adım 3: SharePoint hello dış URL hakkında bilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="fe846-242">Step 3: Ensure that SharePoint knows about hello external URL</span></span>

<span data-ttu-id="fe846-243">SharePoint hello dış URL temel alınarak hello site bulabilirsiniz ve böylece bu dış URL temel alınarak bağlantılar oluşturmaz, son adım tooensure.</span><span class="sxs-lookup"><span data-stu-id="fe846-243">Your last step tooensure that SharePoint can find hello site based on hello external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="fe846-244">Bunun için diğer erişim eşleşmeleri hello SharePoint sitesi için yapılandırarak.</span><span class="sxs-lookup"><span data-stu-id="fe846-244">You do this by configuring alternate access mappings for hello SharePoint site.</span></span>

1. <span data-ttu-id="fe846-245">Açık hello **SharePoint 2013 Yönetim Merkezi** site.</span><span class="sxs-lookup"><span data-stu-id="fe846-245">Open hello **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="fe846-246">Altında **sistem ayarlarını**seçin **yapılandırma diğer erişim eşleşmeleri**.</span><span class="sxs-lookup"><span data-stu-id="fe846-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="fe846-247">Merhaba açılır **diğer erişim eşleşmeleri** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fe846-247">This opens hello **Alternate Access Mappings** box.</span></span>

  ![Diğer erişim eşleşmeleri kutusu](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="fe846-249">Hello aşağı açılan listesinde **alternatif erişim eşleme koleksiyonu**seçin **değişiklik alternatif erişim eşleme koleksiyonu**.</span><span class="sxs-lookup"><span data-stu-id="fe846-249">In hello drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="fe846-250">Örneğin, siteniz--seçin **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="fe846-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![Bir site seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="fe846-252">Bir iç URL veya genel bir URL olarak tooadd hello URL yayımlanan seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-252">You can choose tooadd hello published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="fe846-253">Bu örnek, genel bir URL hello extranet kullanır.</span><span class="sxs-lookup"><span data-stu-id="fe846-253">This example uses a public URL as hello extranet.</span></span>
6. <span data-ttu-id="fe846-254">' I tıklatın **ortak URL'leri Düzenle** hello içinde **Extranet** , yol ve enter hello hello yolu yayımlanan hello önceki adımda olduğu gibi uygulama.</span><span class="sxs-lookup"><span data-stu-id="fe846-254">Click **Edit Public URLs** in hello **Extranet** path, and then enter hello path for hello published application, as in hello previous step.</span></span> <span data-ttu-id="fe846-255">Örneğin **https://sharepoint-iddemo.msappproxy.net**.</span><span class="sxs-lookup"><span data-stu-id="fe846-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![Merhaba yolu girme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="fe846-257">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe846-257">Click **Save**.</span></span>

 <span data-ttu-id="fe846-258">Artık hello SharePoint sitesi harici olarak Azure AD uygulama proxy'si aracılığıyla erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe846-258">You can now access hello SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe846-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe846-259">Next steps</span></span>

- [<span data-ttu-id="fe846-260">Nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="fe846-260">How tooprovide secure remote access tooon-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="fe846-261">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="fe846-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="fe846-262">SharePoint 2016 ve Office Online Server Azure AD uygulama proxy'si ile uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="fe846-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
