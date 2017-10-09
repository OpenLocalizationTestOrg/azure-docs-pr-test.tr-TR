---
title: "Azure AD uygulama proxy'si kullanarak yayımlanan uygulamalar için özel bir ana sayfa aaaSet | Microsoft Docs"
description: "Merhaba temel Azure AD uygulama proxy'si bağlayıcılar hakkında bilgiler yer almaktadır"
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
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="a7441-103">Azure AD uygulama proxy'si kullanarak yayımlanan uygulamalar için özel bir ana sayfa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a7441-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="a7441-104">Bu makalede ele nasıl tooconfigure uygulamaları toodirect kullanıcılar tooa özel giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="a7441-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="a7441-105">Uygulama proxy'si ile bir uygulama yayımladığınızda, bir iç URL ayarlanmış ancak bazen, kullanıcılarınızın ilk görmelisiniz hello sayfa değil.</span><span class="sxs-lookup"><span data-stu-id="a7441-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="a7441-106">Özel bir ana sayfa hello uygulamaları hello Azure Active Directory erişim paneli veya hello Office 365 uygulama Başlatıcı eriştiklerinde, kullanıcılarınızın toohello sağ sayfa Git şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a7441-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="a7441-107">Kullanıcıların hello uygulama başlattığında, hello yayımlanan uygulama için varsayılan toohello kök etki alanı URL'si tarafından yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7441-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="a7441-108">Merhaba giriş sayfası genellikle hello giriş sayfası URL'si olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a7441-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="a7441-109">Uygulama kullanıcıların tooland hello uygulama içinde belirli bir sayfada istediğinizde hello Azure AD PowerShell modülü toodefine özel giriş sayfası URL'si kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7441-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="a7441-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a7441-110">For example:</span></span>
- <span data-ttu-id="a7441-111">Kullanıcılar, şirket ağı içinde çok giderek*https://ExpenseApp/login/login.aspx* toosign içinde ve uygulamanızı erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7441-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="a7441-112">Uygulama proxy'si hello klasör yapısının hello üst düzeyde tooaccess gerektiğini görüntüleri gibi diğer varlıklar olduğundan hello uygulamayla yayımlama *https://ExpenseApp* İç URL hello gibi.</span><span class="sxs-lookup"><span data-stu-id="a7441-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="a7441-113">dış URL varsayılan Hello *https://ExpenseApp-contoso.msappproxy.net*, değil almakta kullanıcılar toohello oturum sayfasında.</span><span class="sxs-lookup"><span data-stu-id="a7441-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="a7441-114">Ayarlama *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* kullanıcılarınız gibi hello giriş sayfası URL'si toogive sorunsuz bir deneyim.</span><span class="sxs-lookup"><span data-stu-id="a7441-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="a7441-115">Toopublished uygulamaları kullanıcılara erişim vermek, hello uygulamaları hello görüntülenen [Azure AD erişim paneli](active-directory-saas-access-panel-introduction.md) ve hello [Office 365 uygulama Başlatıcı](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="a7441-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a7441-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a7441-116">Before you start</span></span>

<span data-ttu-id="a7441-117">Merhaba giriş sayfası URL'si ayarlamadan önce aşağıdaki gereksinimleri göz hello tutun:</span><span class="sxs-lookup"><span data-stu-id="a7441-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="a7441-118">Bir alt etki alanı yolu hello kök etki alanı URL'si belirtmeniz hello yol olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a7441-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="a7441-119">Merhaba kök etki alanı URL ise, örneğin, https://apps.contoso.com/app1/, yapılandırdığınız hello giriş sayfası URL'si ile https://apps.contoso.com/app1/ başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7441-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="a7441-120">Bir değişiklik yaparsanız, toohello yayımlanan uygulama, hello değişiklik hello giriş sayfası URL'si hello değerini sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="a7441-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="a7441-121">Hello gelecekteki hello uygulamada güncelleştirdiğinizde yeniden denetle ve gerekir, gerekirse hello giriş sayfası URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a7441-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="a7441-122">Hello Azure portal'de Hello giriş sayfasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a7441-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="a7441-123">İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="a7441-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="a7441-124">Çok gidin**Azure Active Directory** > **uygulama kayıtlar** ve uygulamanızı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="a7441-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="a7441-125">Seçin **özellikleri** hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="a7441-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="a7441-126">Güncelleştirme hello **giriş sayfası URL'si** yeni yol ile alan.</span><span class="sxs-lookup"><span data-stu-id="a7441-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Yeni giriş sayfası URL'si belirtin](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="a7441-128">Seçin **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="a7441-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="a7441-129">PowerShell ile Merhaba giriş sayfasını Değiştir</span><span class="sxs-lookup"><span data-stu-id="a7441-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="a7441-130">Hello Azure AD PowerShell modülünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="a7441-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="a7441-131">PowerShell kullanarak özel giriş sayfası URL'si tanımlamadan önce hello Azure AD PowerShell modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a7441-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="a7441-132">Hello hello paketini indirebilirsiniz [PowerShell Galerisi](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), hangi hello Graph API uç noktası kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7441-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="a7441-133">tooinstall hello paketini, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a7441-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="a7441-134">Standart bir PowerShell penceresi açın ve ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a7441-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="a7441-135">Bir yönetici olmayan hello komutu çalıştırıyorsanız hello kullan `-scope currentuser` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a7441-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="a7441-136">Merhaba yükleme sırasında seçin **Y** tooinstall iki Nuget.org paketler. Her iki paketin de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a7441-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="a7441-137">Hello hello uygulamasının objectID bulur</span><span class="sxs-lookup"><span data-stu-id="a7441-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="a7441-138">Hello hello uygulamasının objectID alın ve ardından hello uygulaması için kendi giriş sayfası tarafından arayın.</span><span class="sxs-lookup"><span data-stu-id="a7441-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="a7441-139">PowerShell'i açın ve hello Azure AD modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="a7441-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="a7441-140">Toohello içinde Azure AD modülünü hello Kiracı Yöneticisi olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a7441-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="a7441-141">Kendi giriş sayfası URL'sine bağlı hello uygulamayı bulun.</span><span class="sxs-lookup"><span data-stu-id="a7441-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="a7441-142">Çok giderek hello URL hello Portalı'nda bulabilirsiniz**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a7441-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="a7441-143">Bu örnekte *sharepoint iddemo*.</span><span class="sxs-lookup"><span data-stu-id="a7441-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="a7441-144">Benzer toohello bir burada gösterilen bir sonuç almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7441-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="a7441-145">Merhaba objectID GUID toouse hello sonraki bölümde kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a7441-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="a7441-146">Güncelleştirme hello giriş sayfası URL'si</span><span class="sxs-lookup"><span data-stu-id="a7441-146">Update hello home page URL</span></span>

<span data-ttu-id="a7441-147">Adım 1 ' için kullanılan aynı PowerShell modülü Hello hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a7441-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="a7441-148">Uygulama düzeltin ve değiştirme hello sahip olduğunuzdan emin olun *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* hello hello önceki adımda kopyaladığınız objectID ile.</span><span class="sxs-lookup"><span data-stu-id="a7441-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="a7441-149">Merhaba uygulama Onaylandı, hazır tooupdate hello giriş sayfasında, aşağıdaki gibi demektir.</span><span class="sxs-lookup"><span data-stu-id="a7441-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="a7441-150">Boş uygulama nesnesi toohold toomake istediğiniz hello değişiklikleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a7441-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="a7441-151">Bu değişken tooupdate istediğiniz hello değerler tutar.</span><span class="sxs-lookup"><span data-stu-id="a7441-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="a7441-152">Hiçbir şey bu adımda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a7441-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="a7441-153">İstediğiniz hello giriş sayfası URL'si toohello değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a7441-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="a7441-154">Merhaba değerin hello yayımlanan uygulama bir alt yolu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7441-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="a7441-155">Giriş sayfası URL'den değiştirirseniz gibi hello *https://sharepoint-iddemo.msappproxy.net/* çok*https://sharepoint-iddemo.msappproxy.net/hybrid/*, uygulama kullanıcılarınızın Git doğrudan toohello özel Giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="a7441-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="a7441-156">Merhaba, kopyalanan GUID (objectID) kullanarak güncelleştirme hello olun "1. adım: Bul hello hello uygulamasının objectID."</span><span class="sxs-lookup"><span data-stu-id="a7441-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="a7441-157">Merhaba değişiklik başarılı olduğunu tooconfirm hello uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a7441-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="a7441-158">Toohello uygulama yaptığınız tüm değişiklikler hello giriş sayfası URL'si sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="a7441-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="a7441-159">Giriş sayfası URL'nizi sıfırlar, 2. adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a7441-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7441-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7441-160">Next steps</span></span>

- [<span data-ttu-id="a7441-161">Azure AD uygulama proxy'si ile uzaktan erişim tooSharePoint etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a7441-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="a7441-162">Hello Azure portalında uygulama ara sunucusunu etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a7441-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
