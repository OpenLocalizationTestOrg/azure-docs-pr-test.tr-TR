---
title: "Sessiz yükleme Azure AD uygulama ara sunucusu Bağlayıcısı | Microsoft Docs"
description: "Şirket içi uygulamalara güvenli uzaktan erişim sağlamak için Azure AD uygulama ara sunucusu Bağlayıcısı katılımsız yüklemesini gerçekleştirmek nasıl ele alınmaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="a056b-103">Azure AD uygulama ara sunucusu Bağlayıcısı gerek kalmadan sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="a056b-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="a056b-104">Bir yükleme komut dosyası birden çok Windows sunucuları veya etkin kullanıcı arabirimine sahip olmayan Windows sunucularına göndermek kullanabilmek ister.</span><span class="sxs-lookup"><span data-stu-id="a056b-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="a056b-105">Bu konu, katılımsız yükleme ve kaydetme, Azure AD uygulama ara sunucusu Bağlayıcısı etkinleştiren bir Windows PowerShell betik oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a056b-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="a056b-106">Bu özellik, aşağıdakileri yapmak istediğinizde yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="a056b-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="a056b-107">UI katman yok veya makineye RDP yapamadığında makinelere Bağlayıcısı'nı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a056b-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="a056b-108">Yükleme ve aynı anda birçok bağlayıcılar kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a056b-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="a056b-109">Bağlayıcısını yükleme ve başka bir yordamının parçası olarak kayıt tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="a056b-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="a056b-110">Bağlayıcı BITS içerir ancak kaydedilmemiş standart sunucu görüntüsünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a056b-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="a056b-111">Uygulama Ara sunucusu Bağlayıcısı'nı ağınızdaki adlı ince bir Windows Server hizmetini yükleyerek çalışır.</span><span class="sxs-lookup"><span data-stu-id="a056b-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="a056b-112">Uygulama Ara sunucusu Bağlayıcısı çalışmaya bir genel yönetici ve parola kullanarak Azure AD dizininizi ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a056b-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="a056b-113">Normalde bu bilgileri açılan iletişim kutusunda Bağlayıcısı yüklemesi sırasında girilir.</span><span class="sxs-lookup"><span data-stu-id="a056b-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="a056b-114">Ancak, kayıt bilgilerinizi girmek için bir kimlik bilgisi nesnesi oluşturmak için Windows PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a056b-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="a056b-115">Veya, kendi belirteç oluşturmak ve kayıt bilgilerinizi girmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a056b-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="a056b-116">Bağlayıcısı'nı yüklemek</span><span class="sxs-lookup"><span data-stu-id="a056b-116">Install the connector</span></span>
<span data-ttu-id="a056b-117">Bağlayıcı MSI'lerini bağlayıcı gibi kaydettirmeden yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a056b-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="a056b-118">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="a056b-118">Open a command prompt.</span></span>
2. <span data-ttu-id="a056b-119">/Q Sessiz yükleme - yani aşağıdaki komutu çalıştırın yükleme Son Kullanıcı Lisans Sözleşmesi'ni kabul ister değil.</span><span class="sxs-lookup"><span data-stu-id="a056b-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="a056b-120">Bağlayıcı Azure AD ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="a056b-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="a056b-121">Bağlayıcı kaydetmek için kullanabileceğiniz iki yöntem vardır:</span><span class="sxs-lookup"><span data-stu-id="a056b-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="a056b-122">Bir Windows PowerShell kimlik bilgisi nesnesi kullanarak bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a056b-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="a056b-123">Çevrimdışı oluşturan bir belirteç kullanarak bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a056b-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="a056b-124">Bir Windows PowerShell kimlik bilgisi nesnesi kullanarak bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a056b-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="a056b-125">Windows PowerShell kimlik bilgilerini nesnesi şu komutu çalıştırarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a056b-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="a056b-126">Değiştir  *\<kullanıcıadı\>*  ve  *\<parola\>*  kullanıcı adı ve parola dizininiz için:</span><span class="sxs-lookup"><span data-stu-id="a056b-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="a056b-127">Git **C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı** ve kimlik bilgileri, oluşturduğunuz nesne PowerShell kullanarak komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a056b-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="a056b-128">Değiştir *$cred* oluşturduğunuz nesne kimlik bilgileri PowerShell adı ile:</span><span class="sxs-lookup"><span data-stu-id="a056b-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="a056b-129">Çevrimdışı oluşturan bir belirteç kullanarak bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a056b-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="a056b-130">Kod parçacığında değerleri kullanarak Authenticationcontext'i sınıfını kullanarak çevrimdışı bir belirteç oluşturur:</span><span class="sxs-lookup"><span data-stu-id="a056b-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="a056b-131">Belirteç olduktan sonra belirteci kullanarak bir SecureString oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a056b-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="a056b-132">Aşağıdaki Windows PowerShell komutunu çalıştırın değiştirme \<GUID Kiracı\> , dizin kimliği:</span><span class="sxs-lookup"><span data-stu-id="a056b-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="a056b-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a056b-133">Next steps</span></span> 
* [<span data-ttu-id="a056b-134">Kendi etki alanı adınızı kullanarak uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="a056b-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="a056b-135">Çoklu oturum açmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a056b-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="a056b-136">Uygulama Ara sunucusu ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="a056b-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


