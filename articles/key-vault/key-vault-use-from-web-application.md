---
title: "aaaUse Azure anahtar Kasası'nı bir Web uygulaması | Microsoft Docs"
description: "Bu öğretici toohelp nasıl toouse Azure anahtar kasası bir web uygulamasından öğrenin kullanın."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="d3e24-103">Bir Web uygulamasından Azure anahtar kasası kullanın</span><span class="sxs-lookup"><span data-stu-id="d3e24-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="d3e24-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="d3e24-104">Introduction</span></span>
<span data-ttu-id="d3e24-105">Bu öğretici toohelp toouse Azure anahtar kasası nasıl Azure web uygulamasından öğrenin kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="d3e24-106">Bu, böylece web uygulamanızda kullanılabilir gizli bir Azure anahtar Kasası'erişme hello işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="d3e24-107">**Zaman toocomplete tahmini:** 15 dakika</span><span class="sxs-lookup"><span data-stu-id="d3e24-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="d3e24-108">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d3e24-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3e24-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d3e24-109">Prerequisites</span></span>
<span data-ttu-id="d3e24-110">toocomplete Bu öğreticiyi izleyerek hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d3e24-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d3e24-111">Azure anahtar Kasası'nda bir URI tooa gizlilik</span><span class="sxs-lookup"><span data-stu-id="d3e24-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="d3e24-112">Azure Active Directory ile erişim tooyour anahtar kasası sahip kayıtlı bir istemci kimliği ve bir web uygulaması için bir istemci parolası</span><span class="sxs-lookup"><span data-stu-id="d3e24-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="d3e24-113">Bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-113">A web application.</span></span> <span data-ttu-id="d3e24-114">Biz gösteren bir Web uygulaması olarak azure'da dağıtılan bir ASP.NET MVC uygulaması için başlangıç adımları.</span><span class="sxs-lookup"><span data-stu-id="d3e24-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e24-115">Listelenen hello adımları tamamladınız gereklidir [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md) , böylece Bu öğretici için URI tooa gizli ve hello istemci kimliği ve istemci parolası için bir web uygulaması hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="d3e24-116">Merhaba anahtar kasası erişecek Merhaba web uygulaması, Azure Active Directory'de kayıtlı ve erişim tooyour anahtar kasası belirtilen hello bir ' dir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="d3e24-117">Merhaba durum bu değilse, tooRegister hello Başlarken Öğreticisi uygulamada geri dönün ve listelenen hello adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d3e24-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="d3e24-118">Bu öğretici, Azure üzerinde web uygulamaları oluşturmak, hello temellerini anlamak web geliştiricileri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="d3e24-119">Azure Web Apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3e24-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="d3e24-120"><a id="packages"></a>Nuget paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d3e24-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="d3e24-121">Yüklü toohave web uygulamanız gereken iki paket vardır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="d3e24-122">Active Directory Authentication Library - Azure Active Directory ile etkileşim ve kullanıcı kimliği yönetmek için yöntemler içerir</span><span class="sxs-lookup"><span data-stu-id="d3e24-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="d3e24-123">Azure anahtar kasası Library - Azure anahtar kasası ile etkileşim için yöntemler içerir</span><span class="sxs-lookup"><span data-stu-id="d3e24-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="d3e24-124">Bu paketleri her ikisi de kullanılarak yüklenebilir hello Install-Package komutunu kullanarak Paket Yöneticisi konsolu hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="d3e24-125"><a id="webconfig"></a>Web.Config değiştirme</span><span class="sxs-lookup"><span data-stu-id="d3e24-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="d3e24-126">Toobe eklenen toohello web.config dosyasında aşağıdaki gibi gereken üç uygulama ayarlarını vardır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="d3e24-127">Uygulamanızı Azure Web uygulaması olarak toohost yapmayacağınız, hello gerçek ClientID, istemci gizli anahtarı ve gizli anahtar URI'sini değerleri toohello web.config eklemeniz gerekir. Aksi takdirde hello Azure Portal için ek bir güvenlik düzeyi içinde hello gerçek değerler biz alacağınız çünkü bu kukla değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="d3e24-128"><a id="gettoken"></a>Yöntem tooGet bir erişim belirteci Ekle</span><span class="sxs-lookup"><span data-stu-id="d3e24-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="d3e24-129">Sipariş toouse hello anahtar kasası API'sini bir erişim belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="d3e24-130">Merhaba anahtar kasası istemci işleme toohello anahtar kasası API ancak gereksinim toosupply çağrıları hello erişim belirteci alan bir işlev ile.</span><span class="sxs-lookup"><span data-stu-id="d3e24-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="d3e24-131">Merhaba kod tooget bir erişim belirteci Azure Active Directory'den aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="d3e24-132">Bu kodu, uygulamanızda herhangi bir yere gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3e24-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="d3e24-133">I tooadd bir yardımcı programları veya EncryptionHelper sınıfı gibi.</span><span class="sxs-lookup"><span data-stu-id="d3e24-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="d3e24-134">Bir istemci kimliği ve istemci parolası hello en kolay yolu tooauthenticate Azure AD uygulaması kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="d3e24-135">Ve web uygulamanızı kullanarak ayrılması görevlerini ve anahtar yönetimi üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3e24-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="d3e24-136">Ancak, yapılandırma ayarlarınızı tooprotect istediğiniz hello gizli koyma olarak olarak riskli olabilecek bazı yapılandırma ayarlarınızın hello gizli koyma kullanır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="d3e24-137">Azure AD uygulaması toouse bir istemci kimliği ve istemci kimliği ve istemci parolası tooauthenticate yerine sertifikanın nasıl hello üzerinde bir tartışma için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="d3e24-138"><a id="appstart"></a>Uygulama başlangıç Hello gizli alma</span><span class="sxs-lookup"><span data-stu-id="d3e24-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="d3e24-139">Şimdi biz toocall hello anahtar kasası API kod ve hello gizli almak.</span><span class="sxs-lookup"><span data-stu-id="d3e24-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="d3e24-140">toouse ihtiyacınız önce çağırılır sürece hello aşağıdaki kodu her yerden yerleştirilebileceği onu.</span><span class="sxs-lookup"><span data-stu-id="d3e24-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="d3e24-141">I bu kodu hello uygulama başlatma olayı hello Global.asax başlangıç kez çalışır ve gizli hello uygulama için kullanılabilir hale getirir hello koymak.</span><span class="sxs-lookup"><span data-stu-id="d3e24-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="d3e24-142"><a id="portalsettings"></a>Uygulama ayarları hello Azure portalı (isteğe bağlı) Ekle</span><span class="sxs-lookup"><span data-stu-id="d3e24-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="d3e24-143">Bir Azure Web uygulaması varsa hello Azure Portal hello gerçek değerler hello AppSettings için artık ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3e24-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="d3e24-144">Bunu yaparak hello gerçek değerler hello web.config dosyasında olmaz ancak ayrı bir erişim denetimi özelliklerinden sahip olduğu Portal hello korumalı.</span><span class="sxs-lookup"><span data-stu-id="d3e24-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="d3e24-145">Bu değerler, web.config dosyanızda girdiğiniz hello değerleri için değiştirilecektir. Merhaba adları olan Merhaba, aynı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3e24-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Azure Portalı'nda görüntülenen uygulama ayarları][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="d3e24-147">Bir istemci parolası yerine bir sertifika ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d3e24-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="d3e24-148">Başka bir şekilde tooauthenticate Azure AD uygulaması bir istemci kimliği ve bir sertifika bir istemci kimliği ve istemci parolası yerine kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="d3e24-149">Aşağıdaki adımları toouse Azure Web uygulaması sertifikada hello:</span><span class="sxs-lookup"><span data-stu-id="d3e24-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="d3e24-150">Alma veya bir sertifika oluşturun</span><span class="sxs-lookup"><span data-stu-id="d3e24-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="d3e24-151">Merhaba sertifika bir Azure AD uygulama ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="d3e24-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="d3e24-152">Kod tooyour Web uygulaması toouse hello sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="d3e24-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="d3e24-153">Sertifika tooyour Web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="d3e24-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="d3e24-154">**Alma veya bir sertifika oluşturmak** bizim amacıyla bir test sertifikası yapacağız.</span><span class="sxs-lookup"><span data-stu-id="d3e24-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="d3e24-155">Birkaç sertifika bir geliştirici komut istemi toocreate kullanabileceğiniz komutlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="d3e24-156">Oluşturulan hello sertifika dosyaları istediğiniz dizin toowhere değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d3e24-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="d3e24-157">Ayrıca, başlangıç ve bitiş tarihi başlangıç sertifikanın hello hello geçerli tarih artı 1 yıl kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="d3e24-158">Merhaba bitiş tarihi ve hello .pfx hello parolasını not edin (Bu örnekte: 07/31/2016 ve test123).</span><span class="sxs-lookup"><span data-stu-id="d3e24-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="d3e24-159">Bunları aşağıdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-159">You will need them below.</span></span>

<span data-ttu-id="d3e24-160">Bir test sertifikası oluşturma hakkında daha fazla bilgi için bkz: [nasıl yapılır: bilgisayarınızı kendi Test sertifikası oluşturma](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="d3e24-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="d3e24-161">**Azure AD uygulaması ile ilişkilendirme hello sertifika** bir sertifikanız, tooassociate gereken Azure AD uygulaması ile.</span><span class="sxs-lookup"><span data-stu-id="d3e24-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="d3e24-162">Şu anda hello Azure portalı, bu iş akışı desteklemiyor; Bu PowerShell aracılığıyla tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="d3e24-163">Aşağıdaki komutları tooassoicate hello Merhaba Azure AD uygulaması sertifikayla hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d3e24-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="d3e24-164">Bu komutları çalıştırdıktan sonra Azure AD'de Merhaba uygulaması görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3e24-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="d3e24-165">Arama yaparken, "Şirketimin sahip olduğu uygulamalar" seçin "uygulamaları Şirketim kullandığından yerine" Merhaba arama iletişim kutusunda emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3e24-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="d3e24-166">Azure AD uygulama nesneleri ve ServicePrincipal nesneleri hakkında daha fazla toolearn bakın [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="d3e24-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="d3e24-167">**Kod tooyour Web uygulaması toouse hello sertifika Ekle** artık kod tooyour Web uygulaması tooaccess hello cert ve kimlik doğrulaması için kullanmak ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d3e24-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="d3e24-168">İlk kod tooaccess hello cert yoktur.</span><span class="sxs-lookup"><span data-stu-id="d3e24-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="d3e24-169">Bu hello StoreLocation LocalMachine yerine Currentuser'a olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d3e24-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="d3e24-170">Bir test sertifikası kullanıyoruz yöntemi ve biz 'false' toohello sağladığı bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="d3e24-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="d3e24-171">Sonraki hello CertificateHelper kullanır ve kimlik doğrulaması için gerekli olan bir ClientAssertionCertificate oluşturan kodudur.</span><span class="sxs-lookup"><span data-stu-id="d3e24-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="d3e24-172">Merhaba yeni kod tooget hello erişim belirteci aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="d3e24-173">Merhaba GetToken yöntemi yukarıdaki değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="d3e24-174">I kolaylık sağlamak için farklı bir ad verilen.</span><span class="sxs-lookup"><span data-stu-id="d3e24-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="d3e24-175">I tüm bu kod, kullanım kolaylığı için my Web uygulaması projenin yardımcı programları sınıfı yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d3e24-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="d3e24-176">Merhaba son kod hello uygulama_başlatma yönteminin değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="d3e24-177">İlk toocall hello GetCert() yöntemi tooload hello ClientAssertionCertificate gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="d3e24-178">Ve biz Biz yeni KeyVaultClient oluştururken sağladığınız hello geri çağırma yöntemini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d3e24-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="d3e24-179">Bu size yukarıda vardı hello kod değiştirir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="d3e24-180">**Web uygulaması hello Azure Portal aracılığıyla bir sertifika tooyour ekleme** sertifika tooyour Web uygulaması ekleme olan basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d3e24-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="d3e24-181">İlk olarak, toohello Azure Portal gidin ve tooyour Web uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d3e24-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="d3e24-182">Hello ayarları dikey penceresinde, Web uygulamanız için "özel etki alanları ve SSL" Merhaba giriş'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="d3e24-183">Merhaba üzerinde açılan dikey mümkün tooupload hello KVWebApp.pfx yukarıda oluşturduğunuz sertifika olması, hello pfx hello parolasını anımsamasını emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3e24-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Hello Azure Portal sertifika tooa Web uygulaması ekleme][2]

<span data-ttu-id="d3e24-185">Merhaba toodo gereken son tooadd bir uygulama ayarı tooyour hello adını Web sitesi olan bir Web uygulaması şeydir\_yük\_SERTİFİKALARI ve değerini *.</span><span class="sxs-lookup"><span data-stu-id="d3e24-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="d3e24-186">Bu, tüm sertifikaların yüklü olduğundan güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="d3e24-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="d3e24-187">Tooload yalnızca hello sertifikalar istediyseniz karşıya yüklediğiniz sonra virgülle ayrılmış bir liste kendi parmak izleri girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3e24-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="d3e24-188">Sertifika tooa Web uygulaması ekleme hakkında daha fazla toolearn bakın [kullanarak sertifikaları Azure Web siteleri uygulamalarında](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="d3e24-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="d3e24-189">**Sertifika tooKey kasası gizlilik olarak ekleme** , sertifika toohello Web App service doğrudan yüklemek yerine, anahtar kasası gizli olarak depolayın ve buradan dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d3e24-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="d3e24-190">Bu blog gönderisine aşağıdaki hello özetlenen iki adımlı bir işlemdir [anahtar kasası aracılığıyla Azure Web uygulaması sertifikası dağıtma](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="d3e24-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="d3e24-191"><a id="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3e24-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="d3e24-192">Programlama başvuruları için bkz: [Azure anahtar kasası C# istemci API Başvurusu](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3e24-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
