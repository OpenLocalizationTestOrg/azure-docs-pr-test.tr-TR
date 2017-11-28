---
title: "Azure AD uygulama proxy'si aracılığıyla yayımlanan uygulamalar için özel bir ana sayfa ayarlama | Microsoft Docs"
description: "Azure AD uygulama proxy'si bağlayıcılar hakkında temel bilgiler yer almaktadır"
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="6c837-103">Azure AD uygulama proxy'si kullanarak yayımlanan uygulamalar için özel bir ana sayfa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6c837-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="6c837-104">Bu makalede, özel bir ana sayfa kullanıcıları yönlendirmek için uygulamaları yapılandırma anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6c837-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="6c837-105">Uygulama proxy'si ile bir uygulama yayımladığınızda, kullanıcılarınız ilk görmelisiniz sayfa olmayan bir iç URL ancak bazen ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6c837-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="6c837-106">Özel bir ana sayfa ayarlayabilir, böylece uygulamaları Azure Active Directory erişim paneli veya Office 365 uygulama Başlatıcı eriştiklerinde, kullanıcılarınızın sağ sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="6c837-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="6c837-107">Kullanıcıların uygulama başlattığında, varsayılan olarak yayımlanan uygulama kök etki alanı URL'si yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c837-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="6c837-108">Giriş sayfası genellikle giriş sayfası URL'si olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="6c837-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="6c837-109">Azure AD PowerShell modülü, uygulama kullanıcılarınızın uygulama içinde belirli bir sayfada güden istediğinizde özel giriş sayfası URL'leri tanımlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c837-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="6c837-110">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6c837-110">For example:</span></span>
- <span data-ttu-id="6c837-111">Kullanıcıların gidin, şirket ağı içinde *https://ExpenseApp/login/login.aspx* oturum açın ve uygulamanıza erişmek için.</span><span class="sxs-lookup"><span data-stu-id="6c837-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="6c837-112">Uygulama proxy'si klasör yapısını en üst düzeyde erişmesi görüntüleri gibi diğer varlıklar olduğundan ile uygulama yayımlama *https://ExpenseApp* İç URL olarak.</span><span class="sxs-lookup"><span data-stu-id="6c837-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="6c837-113">Varsayılan dış URL *https://ExpenseApp-contoso.msappproxy.net*, değil almakta kullanıcılarınıza oturum açma sayfasında.</span><span class="sxs-lookup"><span data-stu-id="6c837-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="6c837-114">Ayarlama *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* kullanıcılarınızın sorunsuz bir deneyim sunmak için giriş sayfası URL'si olarak.</span><span class="sxs-lookup"><span data-stu-id="6c837-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="6c837-115">Kullanıcıların yayımlanan uygulamalara erişim vermek, uygulamaları görüntülenen [Azure AD erişim paneli](active-directory-saas-access-panel-introduction.md) ve [Office 365 uygulama Başlatıcı](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="6c837-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6c837-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6c837-116">Before you start</span></span>

<span data-ttu-id="6c837-117">Giriş sayfası URL'si ayarlamadan önce aşağıdaki gereksinimleri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6c837-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="6c837-118">Belirttiğiniz yolda kök etki alanı URL'si bir alt etki alanı yolu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6c837-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="6c837-119">Kök etki alanı URL'si, örneğin, https://apps.contoso.com/app1/, yapılandırdığınız giriş sayfası URL'si ile https://apps.contoso.com/app1/ başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c837-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="6c837-120">Yayımlanan uygulama bir değişiklik yaparsanız, değişiklik giriş sayfası URL'si değerini sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6c837-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="6c837-121">Giriş sayfası URL'si, uygulama gelecekte yeniden denetle güncelleştirdiğinizde ve gerekirse güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c837-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="6c837-122">Azure portalında giriş sayfasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6c837-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="6c837-123">[Azure Portal](https://portal.azure.com)’da yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6c837-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="6c837-124">Gidin **Azure Active Directory** > **uygulama kayıtlar** ve uygulamanızı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="6c837-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="6c837-125">Seçin **özellikleri** ayarlarından.</span><span class="sxs-lookup"><span data-stu-id="6c837-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="6c837-126">Güncelleştirme **giriş sayfası URL'si** yeni yol ile alan.</span><span class="sxs-lookup"><span data-stu-id="6c837-126">Update the **Home page URL** field with your new path.</span></span> 

   ![Yeni giriş sayfası URL'si belirtin](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="6c837-128">Seçin **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="6c837-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="6c837-129">PowerShell ile giriş sayfasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6c837-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="6c837-130">Azure AD PowerShell modülünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="6c837-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="6c837-131">PowerShell kullanarak özel giriş sayfası URL'si tanımlamadan önce Azure AD PowerShell modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6c837-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="6c837-132">Paketten indirebilirsiniz [PowerShell Galerisi](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), Graph API uç noktası kullanır.</span><span class="sxs-lookup"><span data-stu-id="6c837-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="6c837-133">Paketi yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6c837-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="6c837-134">Standart bir PowerShell penceresi açın ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6c837-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="6c837-135">Bir yönetici olmayan komutu çalıştırıyorsanız kullanmak `-scope currentuser` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6c837-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="6c837-136">Yükleme sırasında seçin **Y** Nuget.org iki paketleri yüklemek için. Her iki paketin de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6c837-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="6c837-137">Uygulama objectID Bul</span><span class="sxs-lookup"><span data-stu-id="6c837-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="6c837-138">Uygulama objectID alın ve sonra uygulama için kendi giriş sayfasına göre arayın.</span><span class="sxs-lookup"><span data-stu-id="6c837-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="6c837-139">PowerShell'i açın ve Azure AD modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="6c837-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="6c837-140">Azure AD modülünü Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6c837-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="6c837-141">Giriş sayfası URL'sini tabanlı uygulamayı bulun.</span><span class="sxs-lookup"><span data-stu-id="6c837-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="6c837-142">Giderek URL portalında bulabilirsiniz **Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6c837-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="6c837-143">Bu örnekte *sharepoint iddemo*.</span><span class="sxs-lookup"><span data-stu-id="6c837-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="6c837-144">Burada gösterilen benzer bir sonuç almak.</span><span class="sxs-lookup"><span data-stu-id="6c837-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="6c837-145">Sonraki bölümde kullanmak için objectID GUID kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="6c837-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="6c837-146">Giriş sayfası URL'si güncelleştir</span><span class="sxs-lookup"><span data-stu-id="6c837-146">Update the home page URL</span></span>

<span data-ttu-id="6c837-147">1. adım için kullanılan aynı PowerShell modülü, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c837-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="6c837-148">Doğru uygulamanız ve Değiştir onaylayın *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* önceki adımda kopyaladığınız objectID ile.</span><span class="sxs-lookup"><span data-stu-id="6c837-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="6c837-149">Uygulama Onaylandı, giriş sayfası aşağıdaki gibi güncelleştirmek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="6c837-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="6c837-150">Yapmak istediğiniz değişiklikleri tutmak için bir boş uygulama nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c837-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="6c837-151">Bu değişken, güncelleştirmek istediğiniz değerleri tutar.</span><span class="sxs-lookup"><span data-stu-id="6c837-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="6c837-152">Hiçbir şey bu adımda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6c837-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="6c837-153">Giriş sayfası URL'si istediğiniz değerine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6c837-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="6c837-154">Değer yayımlanan uygulama bir alt yolu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c837-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="6c837-155">Örneğin, giriş sayfası URL'den değiştirirseniz *https://sharepoint-iddemo.msappproxy.net/* için *https://sharepoint-iddemo.msappproxy.net/hybrid/*, uygulama kullanıcılarınızın doğrudan özel giriş sayfasına git .</span><span class="sxs-lookup"><span data-stu-id="6c837-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="6c837-156">İçinde kopyaladığınız GUID (objectID) kullanarak güncelleştirme yapmak "1. adım: uygulama objectID bulunamıyor."</span><span class="sxs-lookup"><span data-stu-id="6c837-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="6c837-157">Değiştirme başarılı olduğunu doğrulamak için uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="6c837-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="6c837-158">Uygulama için yaptığınız tüm değişiklikler, giriş sayfası URL'si sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6c837-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="6c837-159">Giriş sayfası URL'nizi sıfırlar, 2. adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="6c837-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c837-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c837-160">Next steps</span></span>

- [<span data-ttu-id="6c837-161">SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6c837-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="6c837-162">Azure portalında uygulama ara sunucusunu etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="6c837-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
