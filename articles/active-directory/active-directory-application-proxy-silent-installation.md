---
title: "aaaSilent Azure AD uygulama ara sunucusu Bağlayıcısı yükleme | Microsoft Docs"
description: "Nasıl tooperform Azure AD uygulama ara sunucusu Bağlayıcısı tooprovide güvenli uzaktan erişim tooyour katılımsız yüklemesi uygulamaları şirket içi kapsar."
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
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="577e1-103">Hello Azure AD uygulama ara sunucusu Bağlayıcısı gerek kalmadan sessiz yükleme</span><span class="sxs-lookup"><span data-stu-id="577e1-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="577e1-104">Bir yükleme komut dosyası toomultiple Windows sunucuları veya etkin kullanıcı arabirimi yok tooWindows sunucuları toobe mümkün toosend istiyor.</span><span class="sxs-lookup"><span data-stu-id="577e1-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="577e1-105">Bu konu, katılımsız yükleme ve kaydetme, Azure AD uygulama ara sunucusu Bağlayıcısı etkinleştiren bir Windows PowerShell betik oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="577e1-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="577e1-106">Bu özellik, aşağıdakileri yapmak istediğinizde yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="577e1-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="577e1-107">Merhaba bağlayıcı makinelere RDP toohello makine yapamadığında veya hiç kullanıcı Arabirimi katman ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="577e1-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="577e1-108">Yükleme ve aynı anda birçok bağlayıcılar kaydedin.</span><span class="sxs-lookup"><span data-stu-id="577e1-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="577e1-109">Merhaba Bağlayıcısı yükleme ve başka bir yordamının parçası olarak kayıt tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="577e1-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="577e1-110">Merhaba bağlayıcı BITS içerir ancak kaydedilmemiş standart sunucu görüntüsünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="577e1-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="577e1-111">Uygulama proxy'si hello bağlayıcı ağınızdaki adlı ince bir Windows Server hizmetini yükleyerek çalışır.</span><span class="sxs-lookup"><span data-stu-id="577e1-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="577e1-112">Merhaba uygulama Proxy Bağlayıcısı toowork için bir genel yönetici ve parola kullanarak Azure AD diziniyle kayıtlı toobe içeriyor.</span><span class="sxs-lookup"><span data-stu-id="577e1-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="577e1-113">Normalde bu bilgileri açılan iletişim kutusunda Bağlayıcısı yüklemesi sırasında girilir.</span><span class="sxs-lookup"><span data-stu-id="577e1-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="577e1-114">Ancak, Windows PowerShell toocreate bir kimlik bilgisi nesnesi tooenter kayıt bilgilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="577e1-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="577e1-115">Veya, kendi belirteç oluşturmak ve tooenter kullanmanızı kayıt bilgilerinizi.</span><span class="sxs-lookup"><span data-stu-id="577e1-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="577e1-116">Merhaba bağlayıcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="577e1-116">Install hello connector</span></span>
<span data-ttu-id="577e1-117">Merhaba bağlayıcı MSI'lerini hello bağlayıcı gibi kaydettirmeden yükleyin:</span><span class="sxs-lookup"><span data-stu-id="577e1-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="577e1-118">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="577e1-118">Open a command prompt.</span></span>
2. <span data-ttu-id="577e1-119">Hangi hello, sessiz yükleme /q anlamına gelir komutu aşağıdaki hello Çalıştır - hello yükleme tooaccept hello son kullanıcı lisans sözleşmesi ister değil.</span><span class="sxs-lookup"><span data-stu-id="577e1-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="577e1-120">Merhaba bağlayıcı Azure AD ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="577e1-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="577e1-121">Tooregister hello bağlayıcı kullanabileceğiniz iki yöntem vardır:</span><span class="sxs-lookup"><span data-stu-id="577e1-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="577e1-122">Bir Windows PowerShell kimlik bilgisi nesnesi kullanarak hello bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="577e1-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="577e1-123">Çevrimdışı oluşturan bir belirteç kullanarak hello bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="577e1-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="577e1-124">Bir Windows PowerShell kimlik bilgisi nesnesi kullanarak hello bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="577e1-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="577e1-125">Şu komutu çalıştırarak Hello Windows PowerShell kimlik bilgilerini nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="577e1-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="577e1-126">Değiştir  *\<kullanıcıadı\>*  ve  *\<parola\>*  hello kullanıcı adı ve parola dizininiz için:</span><span class="sxs-lookup"><span data-stu-id="577e1-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="577e1-127">Çok Git**C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı** ve kimlik bilgileri, oluşturduğunuz nesne hello PowerShell kullanarak hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="577e1-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="577e1-128">Değiştir *$cred* hello PowerShell hello adı ile oluşturduğunuz kimlik bilgilerini nesnesi:</span><span class="sxs-lookup"><span data-stu-id="577e1-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="577e1-129">Çevrimdışı oluşturan bir belirteç kullanarak hello bağlayıcı kaydetme</span><span class="sxs-lookup"><span data-stu-id="577e1-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="577e1-130">Merhaba kod parçacığında Hello değerleri kullanarak hello Authenticationcontext'i sınıfını kullanarak çevrimdışı bir belirteç oluşturur:</span><span class="sxs-lookup"><span data-stu-id="577e1-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
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


2. <span data-ttu-id="577e1-131">Merhaba belirteci olduktan sonra hello belirteci kullanarak bir SecureString oluşturun:</span><span class="sxs-lookup"><span data-stu-id="577e1-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="577e1-132">Windows PowerShell komutunu aşağıdaki, değiştirme çalıştırma hello \<GUID Kiracı\> , dizin kimliği:</span><span class="sxs-lookup"><span data-stu-id="577e1-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="577e1-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="577e1-133">Next steps</span></span> 
* [<span data-ttu-id="577e1-134">Kendi etki alanı adınızı kullanarak uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="577e1-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="577e1-135">Çoklu oturum açmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="577e1-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="577e1-136">Uygulama Ara sunucusu ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="577e1-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


