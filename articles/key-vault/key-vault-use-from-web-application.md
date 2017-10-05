---
title: "Bir Web uygulamasından Azure anahtar kasası kullanan | Microsoft Docs"
description: "Bir web uygulamasından Azure anahtar kasası kullanmayı öğrenmenize yardımcı olmak için bu öğreticiyi kullanın."
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="d3155-103">Bir Web uygulamasından Azure anahtar kasası kullanın</span><span class="sxs-lookup"><span data-stu-id="d3155-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="d3155-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="d3155-104">Introduction</span></span>
<span data-ttu-id="d3155-105">Azure web uygulamasından Azure anahtar kasası kullanmayı öğrenmenize yardımcı olmak için bu öğreticiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3155-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="d3155-106">Bu, böylece web uygulamanızda kullanılabilir gizli bir Azure anahtar Kasası'erişme işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3155-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="d3155-107">**Tahmini tamamlanma süresi:** 15 dakika</span><span class="sxs-lookup"><span data-stu-id="d3155-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="d3155-108">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d3155-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3155-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d3155-109">Prerequisites</span></span>
<span data-ttu-id="d3155-110">Bu öğreticiyi tamamlamak için aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d3155-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d3155-111">Azure anahtar Kasası'nda bir gizlilik için bir URI</span><span class="sxs-lookup"><span data-stu-id="d3155-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="d3155-112">Bir istemci kimliği ve bir web uygulaması için bir gizli anahtar kasanızı erişimi Azure Active Directory'ye kayıtlı</span><span class="sxs-lookup"><span data-stu-id="d3155-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="d3155-113">Bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d3155-113">A web application.</span></span> <span data-ttu-id="d3155-114">Biz gösteren Azure Web uygulaması olarak dağıtılmış bir ASP.NET MVC uygulaması için adımları.</span><span class="sxs-lookup"><span data-stu-id="d3155-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="d3155-115">Listelenen adımları tamamladınız gereklidir [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md) Bu öğretici için böylece bir web uygulaması için bir gizlilik ve istemci kimliği ve istemci parolası URI sahip.</span><span class="sxs-lookup"><span data-stu-id="d3155-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="d3155-116">Anahtar kasası erişecek web uygulamasını Azure Active Directory'de kayıtlı ve anahtar Kasası'na erişim verildi adrestir.</span><span class="sxs-lookup"><span data-stu-id="d3155-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="d3155-117">Bu durumda değilse, bir kasaya Başlarken Öğreticisi uygulamada geri dönün ve listelenen adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d3155-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="d3155-118">Bu öğretici, Azure üzerinde web uygulamaları oluşturma temelleri anlamak web geliştiricileri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d3155-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="d3155-119">Azure Web Apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3155-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="d3155-120"><a id="packages"></a>Nuget paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d3155-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="d3155-121">Yüklü web uygulamanız gereken iki paket vardır.</span><span class="sxs-lookup"><span data-stu-id="d3155-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="d3155-122">Active Directory Authentication Library - Azure Active Directory ile etkileşim ve kullanıcı kimliği yönetmek için yöntemler içerir</span><span class="sxs-lookup"><span data-stu-id="d3155-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="d3155-123">Azure anahtar kasası Library - Azure anahtar kasası ile etkileşim için yöntemler içerir</span><span class="sxs-lookup"><span data-stu-id="d3155-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="d3155-124">Bu paketleri her ikisi de Install-Package komutunu kullanarak Paket Yöneticisi konsolu kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d3155-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="d3155-125"><a id="webconfig"></a>Web.Config değiştirme</span><span class="sxs-lookup"><span data-stu-id="d3155-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="d3155-126">Web.config dosyasında aşağıdaki gibi eklenmesi gereken üç uygulama ayarlarını vardır.</span><span class="sxs-lookup"><span data-stu-id="d3155-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="d3155-127">Uygulamanızı Azure Web uygulaması olarak barındırmak için yapmayacağınız, web.config dosyasına gerçek ClientID, istemci gizli anahtarı ve gizli anahtar URI'sini değerleri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3155-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="d3155-128">Aksi takdirde ek bir güvenlik düzeyi için Azure Portalı'nda gerçek değerler biz alacağınız çünkü bu kukla değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="d3155-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="d3155-129"><a id="gettoken"></a>Bir erişim belirteci almak için bir yöntem ekleyin</span><span class="sxs-lookup"><span data-stu-id="d3155-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="d3155-130">Anahtar kasası API kullanmak için bir erişim belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3155-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="d3155-131">Anahtar kasası istemci anahtar kasası API çağrılarını işler, ancak erişim belirtecini alır işleviyle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3155-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="d3155-132">Azure Active Directory'den bir erişim belirteci alma kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d3155-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="d3155-133">Bu kodu, uygulamanızda herhangi bir yere gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="d3155-134">Bir yardımcı programları veya EncryptionHelper sınıfı eklemek ister.</span><span class="sxs-lookup"><span data-stu-id="d3155-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="d3155-135">Bir istemci kimliği ve istemci gizli anahtarı kullanarak, Azure AD uygulaması kimliğini doğrulamak için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="d3155-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="d3155-136">Ve web uygulamanızı kullanarak ayrılması görevlerini ve anahtar yönetimi üzerinde daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3155-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="d3155-137">Ancak, yapılandırma ayarlarınızda korumak istediğiniz gizli koyma olarak olarak riskli olabilecek bazı yapılandırma ayarlarınızın istemci gizli anahtarı koyma kullanır.</span><span class="sxs-lookup"><span data-stu-id="d3155-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="d3155-138">Bir istemci kimliği ve sertifika istemci kimliği ve istemci parolası yerine Azure AD uygulaması kimliğini doğrulamak için nasıl kullanılacağı hakkında tartışma için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d3155-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="d3155-139"><a id="appstart"></a>Uygulama başlangıç gizli anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="d3155-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="d3155-140">Şimdi anahtar kasası API çağrısı ve gizli anahtarı almak için kod gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3155-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="d3155-141">Aşağıdaki kod herhangi bir yere kullanmaya ihtiyacım önce çağırılır sürece koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="d3155-142">Böylece gizli uygulama için kullanılabilir hale getirir ve Başlat'bir kez çalıştırılır t bu kodu Global.asax uygulama başlatma olayı koymak.</span><span class="sxs-lookup"><span data-stu-id="d3155-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="d3155-143"><a id="portalsettings"></a>Uygulama ayarları (isteğe bağlı) Azure portalında ekleme</span><span class="sxs-lookup"><span data-stu-id="d3155-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="d3155-144">Bir Azure Web uygulaması varsa, Azure Portal'da AppSettings için gerçek değerler artık ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="d3155-145">Bunu yaparak, gerçek değerler Web.Config'de olmaz ancak ayrı bir erişim denetimi özelliklerinden sahip olduğu Portal korumalı.</span><span class="sxs-lookup"><span data-stu-id="d3155-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="d3155-146">Bu değerler, web.config dosyanızda girdiğiniz değerleri için değiştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="d3155-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="d3155-147">Adları aynı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3155-147">Make sure that the names are the same.</span></span>

![Azure Portalı'nda görüntülenen uygulama ayarları][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="d3155-149">Bir istemci parolası yerine bir sertifika ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d3155-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="d3155-150">Azure AD uygulaması kimliğini doğrulamak için başka bir istemci kimliği ve istemci parolası yerine bir istemci kimliği ve bir sertifika kullanarak yoludur.</span><span class="sxs-lookup"><span data-stu-id="d3155-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="d3155-151">Bir Azure Web uygulamasında bir sertifika kullanmak için adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d3155-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="d3155-152">Alma veya bir sertifika oluşturun</span><span class="sxs-lookup"><span data-stu-id="d3155-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="d3155-153">Sertifika bir Azure AD uygulama ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="d3155-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="d3155-154">Sertifikayı kullanmak üzere Web uygulamanıza kod ekleme</span><span class="sxs-lookup"><span data-stu-id="d3155-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="d3155-155">Web uygulamanız için bir sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="d3155-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="d3155-156">**Alma veya bir sertifika oluşturmak** bizim amacıyla bir test sertifikası yapacağız.</span><span class="sxs-lookup"><span data-stu-id="d3155-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="d3155-157">Burada, birkaç Geliştirici Komut İstemi'nde bir sertifika oluşturmak için kullanabileceğiniz komutlar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3155-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="d3155-158">Oluşturulan sertifika dosyaları istediğiniz dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d3155-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="d3155-159">Ayrıca, başlangıç ve bitiş tarihi sertifikanın için geçerli tarih artı 1 yıl kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3155-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="d3155-160">Bitiş tarihi ve .pfx için parolayı not edin (Bu örnekte: 07/31/2016 ve test123).</span><span class="sxs-lookup"><span data-stu-id="d3155-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="d3155-161">Bunları aşağıdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3155-161">You will need them below.</span></span>

<span data-ttu-id="d3155-162">Bir test sertifikası oluşturma hakkında daha fazla bilgi için bkz: [nasıl yapılır: bilgisayarınızı kendi Test sertifikası oluşturma](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="d3155-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="d3155-163">**Sertifika bir Azure AD uygulama ile ilişkilendirme** sertifika sahip olduğunuza göre Azure AD uygulaması ile ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3155-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="d3155-164">Şu anda Azure Portalı'nı bu iş akışı desteklemiyor; Bu PowerShell aracılığıyla tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d3155-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="d3155-165">Aşağıdaki komutları assoicate için sertifika ile Azure AD uygulaması çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d3155-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="d3155-166">Bu komutları çalıştırdıktan sonra Azure AD'de uygulama görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="d3155-167">Arama yaparken, "Şirketimin sahip olduğu uygulamalar" "Uygulamaları Şirketim kullanıyor yerine" arama iletişim kutusunda seçtiğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3155-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="d3155-168">Azure AD uygulama nesneleri ve ServicePrincipal nesneleri hakkında daha fazla bilgi için bkz: [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="d3155-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="d3155-169">**Web uygulamanız için sertifikayı kullanmak üzere kod eklemek** şimdi biz cert erişmek ve kimlik doğrulaması için kullanmak üzere Web uygulamanız için kod ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="d3155-170">İlk cert erişmek için kod yoktur.</span><span class="sxs-lookup"><span data-stu-id="d3155-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="d3155-171">StoreLocation Currentuser'a LocalMachine yerine olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d3155-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="d3155-172">Ve bir test sertifikası kullanıyoruz çünkü biz bulma yöntemine ' false' sağlamış olursunuz olduğunu.</span><span class="sxs-lookup"><span data-stu-id="d3155-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="d3155-173">Sonraki CertificateHelper kullanır ve kimlik doğrulaması için gerekli olan bir ClientAssertionCertificate oluşturan kodudur.</span><span class="sxs-lookup"><span data-stu-id="d3155-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="d3155-174">Erişim belirteci almak için yeni kod aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="d3155-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="d3155-175">GetToken yöntemi yukarıdaki değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d3155-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="d3155-176">I kolaylık sağlamak için farklı bir ad verilen.</span><span class="sxs-lookup"><span data-stu-id="d3155-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="d3155-177">I tüm bu kod, kullanım kolaylığı için my Web uygulaması projenin yardımcı programları sınıfı yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d3155-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="d3155-178">En son kod değişikliği Application_Start yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="d3155-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="d3155-179">İlk olarak kimliğinizi ClientAssertionCertificate yüklemek için GetCert() yöntemini çağırmak gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="d3155-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="d3155-180">Ve biz Biz yeni KeyVaultClient oluştururken sağladığınız geri çağırma yöntemi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="d3155-181">Bu size yukarıda vardı kod değiştirir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d3155-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="d3155-182">**Web uygulamanızı Azure Portal aracılığıyla bir sertifika eklemek** bir sertifika, Web uygulamanızın ekleme olan basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d3155-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="d3155-183">İlk olarak, Azure Portalı'na gidin ve Web uygulamanıza gidin.</span><span class="sxs-lookup"><span data-stu-id="d3155-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="d3155-184">"Özel etki alanları ve SSL" girişini ayarları dikey penceresinde, Web uygulamanız için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d3155-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="d3155-185">Açılan dikey penceresinde KVWebApp.pfx yukarıda oluşturduğunuz sertifikayı karşıya yüklemek için pfx parolasını anımsamasını emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3155-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Azure portalında bir Web uygulaması için bir sertifika ekleme][2]

<span data-ttu-id="d3155-187">Bir uygulama ayarı adı Web sitesi sahip, Web uygulamanızın eklemek için yapmanız gereken son şey.\_yük\_SERTİFİKALARI ve değerini *.</span><span class="sxs-lookup"><span data-stu-id="d3155-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="d3155-188">Bu, tüm sertifikaların yüklü olduğundan güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="d3155-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="d3155-189">Karşıya yüklediğiniz sertifikalar yüklemek istiyorsanız, virgülle ayrılmış bir liste kendi parmak izleri girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3155-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="d3155-190">Bir Web uygulaması için bir sertifika ekleme hakkında daha fazla bilgi edinmek için [kullanarak sertifikaları Azure Web siteleri uygulamalarında](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="d3155-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="d3155-191">**Anahtar kasasına gizli olarak bir sertifika eklemek** sertifikanızı Web App Service'e doğrudan yüklemek yerine, anahtar kasası gizli olarak depolayın ve buradan dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d3155-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="d3155-192">Bu aşağıdaki blog postasına özetlenen iki adımlı bir işlemdir [anahtar kasası aracılığıyla Azure Web uygulaması sertifikası dağıtma](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="d3155-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="d3155-193"><a id="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3155-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="d3155-194">Programlama başvuruları için bkz: [Azure anahtar kasası C# istemci API Başvurusu](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3155-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
