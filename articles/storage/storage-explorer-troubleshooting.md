---
title: "Azure Storage Gezgini sorun giderme kılavuzu | Microsoft Docs"
description: "Hata ayıklama özelliği Azure iki genel bakış"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: e9b833b07556378f17d9aaff0912c7d73dff44eb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="f39e8-103">Azure Storage Gezgini sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f39e8-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="f39e8-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="f39e8-104">Introduction</span></span>

<span data-ttu-id="f39e8-105">Microsoft Azure Storage Gezgini (Önizleme), Windows, macOS ve Linux Azure Storage ile kolayca çalışmanızı sağlayan tek başına bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="f39e8-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="f39e8-106">Uygulama Azure, Sovereign Bulutlar ve Azure yığın üzerinde barındırılan toStorage hesapları bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="f39e8-107">Bu kılavuz, depolama Gezgini'nde görülen yaygın sorunlar için çözümleri özetler.</span><span class="sxs-lookup"><span data-stu-id="f39e8-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="f39e8-108">Oturum açma sorunları</span><span class="sxs-lookup"><span data-stu-id="f39e8-108">Sign in issues</span></span>

<span data-ttu-id="f39e8-109">Yalnızca Azure Active Directory (AAD) hesapları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="f39e8-110">Bir ADFS hesabını kullanıyorsanız, Depolama Gezgini için oturum açma işe yaramayacaktır olduğunu beklenir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-110">If you use an ADFS account, it’s expected that signing in to Storage Explorer would not work.</span></span> <span data-ttu-id="f39e8-111">Devam etmeden önce uygulamanızı yeniden başlatmayı deneyin ve sorunların giderilip giderilemeyeceğini bakın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-111">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="f39e8-112">Hatası: Sertifika zincirindeki otomatik olarak imzalanan sertifika</span><span class="sxs-lookup"><span data-stu-id="f39e8-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="f39e8-113">Neden bu hatayla karşılaşabilirsiniz ve en yaygın iki sebepleri şunlardır birkaç nedeni vardır:</span><span class="sxs-lookup"><span data-stu-id="f39e8-113">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="f39e8-114">Uygulama "(örneğin, şirket sunucunuzun) bir sunucu HTTPS trafiği kesintiye uğratan, şifre çözme ve kendinden imzalı bir sertifika kullanarak şifreleme anlamı saydam proxy" bağlandı.</span><span class="sxs-lookup"><span data-stu-id="f39e8-114">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="f39e8-115">Bir uygulama otomatik olarak imzalanan bir SSL sertifikası aldığınız HTTPS iletilere injecting virüsten koruma yazılımı gibi çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="f39e8-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="f39e8-116">Depolama Gezgini sorunları karşılaştığında, artık alınan HTTPS ileti oynanmadığını bilebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f39e8-116">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="f39e8-117">Kendinden imzalı bir sertifika bir kopyasına sahipseniz, bu güven Depolama Gezgini izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f39e8-117">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="f39e8-118">Sertifika injecting emin değilseniz bulmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-118">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="f39e8-119">Açık SSL yükleyin</span><span class="sxs-lookup"><span data-stu-id="f39e8-119">Install Open SSL</span></span>

    - <span data-ttu-id="f39e8-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (açık sürümlerinin herhangi birinin yeterli olmalıdır)</span><span class="sxs-lookup"><span data-stu-id="f39e8-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="f39e8-121">Mac ve Linux: işletim sisteminizle eklenmelidir</span><span class="sxs-lookup"><span data-stu-id="f39e8-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="f39e8-122">Açık SSL çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f39e8-122">Run Open SSL</span></span>

    - <span data-ttu-id="f39e8-123">Windows: yükleme dizinini açın, **/bin/**, çift tıklayın ve ardından **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="f39e8-123">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="f39e8-124">Mac ve Linux: çalıştırmak **openssl** bir terminal gelen.</span><span class="sxs-lookup"><span data-stu-id="f39e8-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="f39e8-125">S_client - showcerts yürütme-microsoft.com:443 Bağlan</span><span class="sxs-lookup"><span data-stu-id="f39e8-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="f39e8-126">Otomatik olarak imzalanan sertifikalar arayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-126">Look for self-signed certificates.</span></span> <span data-ttu-id="f39e8-127">Kendinden imzalı olduğu emin değilseniz, herhangi bir yerde ("%s") konu arayın ve veren ("i:") aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f39e8-127">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="f39e8-128">Herhangi bir otomatik olarak imzalanan sertifika bulduğunuzda, her biri için kopyalayıp her şeyi ilk ve son dahil olmak üzere **---başlangıç sertifika---** için **---son SERTİFİKAYI---** yeni bir .cer dosyasına.</span><span class="sxs-lookup"><span data-stu-id="f39e8-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="f39e8-129">Depolama Gezgini'ni açın, **Düzenle** > **SSL sertifikalarını** > **alma sertifikaları**ve ardından dosya seçiciyi kullanın bulun, seçin ve oluşturduğunuz .cer dosyaları açın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="f39e8-130">Yukarıdaki adımları kullanarak herhangi bir otomatik olarak imzalanan sertifika bulamazsanız, daha fazla yardım için geri bildirim araçla bize başvurun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-130">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="f39e8-131">Abonelik alınamadı</span><span class="sxs-lookup"><span data-stu-id="f39e8-131">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="f39e8-132">Başarıyla oturum açtıktan sonra aboneliklerinizi alamadı varsa, bu sorunu gidermek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-132">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="f39e8-133">Azure portalında oturum açarak hesabınızı aboneliklere erişimi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-133">Verify that your account has access to the subscriptions by signing into the Azure portal.</span></span>

- <span data-ttu-id="f39e8-134">(Azure, Azure Çin, Azure Almanya, Azure ABD devlet kurumları veya özel ortam/Azure yığın) doğru ortamlarındaki açmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-134">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="f39e8-135">Bir proxy'nin arkasında varsa, Depolama Gezgini proxy düzgün şekilde yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-135">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="f39e8-136">Try kaldırarak ve hesap yeniden ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="f39e8-136">Try removing and readding the account.</span></span>

- <span data-ttu-id="f39e8-137">Kök dizin (diğer bir deyişle, C:\Users\ContosoUser) aşağıdaki dosyaları silerek ve hesap yeniden eklemeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-137">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="f39e8-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="f39e8-138">.adalcache</span></span>

    - <span data-ttu-id="f39e8-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="f39e8-139">.devaccounts</span></span>

    - <span data-ttu-id="f39e8-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="f39e8-140">.extaccounts</span></span>

- <span data-ttu-id="f39e8-141">Herhangi bir hata iletisi için oturum açarken (basarak, F12) geliştirici araçları konsol izleme:</span><span class="sxs-lookup"><span data-stu-id="f39e8-141">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Geliştirici Araçları](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="f39e8-143">Kimlik doğrulaması sayfası Görülemedi</span><span class="sxs-lookup"><span data-stu-id="f39e8-143">Unable to see the authentication page</span></span>

<span data-ttu-id="f39e8-144">Kimlik doğrulama sayfasına bakın, sorunu gidermek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-144">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="f39e8-145">Bağlantınızın hızına bağlı olarak biraz yüklenemedi, kimlik doğrulama iletişim kutusunu kapatmadan önce en az bir dakika bekleyin oturum açma sayfasına ilişkin devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-145">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="f39e8-146">Bir proxy'nin arkasında varsa, Depolama Gezgini proxy düzgün şekilde yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-146">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="f39e8-147">Geliştirici Konsolu F12 tuşuna basarak görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f39e8-147">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="f39e8-148">Geliştirici konsolundan yanıtlarını izleyin ve tüm ipucu için neden Bul olup olmadığını görmek kimlik doğrulaması çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="f39e8-148">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="f39e8-149">Hesabını kaldıramaz</span><span class="sxs-lookup"><span data-stu-id="f39e8-149">Cannot remove account</span></span>

<span data-ttu-id="f39e8-150">Bir hesap kaldıramadı ya da yeniden kimlik doğrula bağlantı herhangi bir şey yapmanız durumunda, bu sorunu gidermek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-150">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="f39e8-151">Kök dizininden aşağıdaki dosyaları silerek ve hesap yeniden ekleniyor deneyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-151">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="f39e8-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="f39e8-152">.adalcache</span></span>

    - <span data-ttu-id="f39e8-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="f39e8-153">.devaccounts</span></span>

    - <span data-ttu-id="f39e8-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="f39e8-154">.extaccounts</span></span>

- <span data-ttu-id="f39e8-155">Kaldırmak isterseniz, SAS depolama kaynaklarını eklenen, aşağıdaki dosyaları silin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-155">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="f39e8-156">Windows için %appdata%/StorageExplorer klasör</span><span class="sxs-lookup"><span data-stu-id="f39e8-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="f39e8-157">/Users/ < adiniz >/kitaplık/uygulaması destek/StorageExplorer Mac için</span><span class="sxs-lookup"><span data-stu-id="f39e8-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="f39e8-158">Linux için ~/.config/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="f39e8-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="f39e8-159">Bu dosyaları silerseniz, tüm kimlik bilgilerinizi yeniden girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-159">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="f39e8-160">Proxy sorunları</span><span class="sxs-lookup"><span data-stu-id="f39e8-160">Proxy issues</span></span>

<span data-ttu-id="f39e8-161">İlk olarak, aşağıdaki bilgileri, girdiğiniz tüm doğru olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="f39e8-161">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="f39e8-162">Proxy URL'si ve bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="f39e8-162">The proxy URL and port number</span></span>

- <span data-ttu-id="f39e8-163">Kullanıcı adı ve proxy sunucu tarafından gerekliyse parola</span><span class="sxs-lookup"><span data-stu-id="f39e8-163">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="f39e8-164">Yaygın çözümleri</span><span class="sxs-lookup"><span data-stu-id="f39e8-164">Common solutions</span></span>

<span data-ttu-id="f39e8-165">Sorunları yaşamaya devam ediyorsanız, bunları gidermek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f39e8-165">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="f39e8-166">Internet'e bir proxy sunucunuz kullanmadan bağlanabiliyorsa Depolama Gezgini proxy ayarlarının etkin çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-166">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="f39e8-167">Bu durumda, proxy ayarlarınızı ile ilgili bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-167">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="f39e8-168">Sorunları tanımlamak için proxy yöneticinizle birlikte çalışın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-168">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="f39e8-169">Proxy sunucusu kullanan diğer uygulamalar beklendiği gibi çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-169">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="f39e8-170">Web tarayıcınızı kullanarak Microsoft Azure portalına bağlanabildiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f39e8-170">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="f39e8-171">Hizmet uç noktalarından yanıtları alabilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="f39e8-172">Uç nokta URL'leri birini tarayıcınıza girin.</span><span class="sxs-lookup"><span data-stu-id="f39e8-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="f39e8-173">Bağlanabiliyorsanız, bir InvalidQueryParameterValue veya benzeri bir XML yanıt almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="f39e8-174">Başka biri de Depolama Gezgini proxy sunucunuz ile kullanıyorsa, bunlar bağlanabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="f39e8-175">Bağlanabiliyorsanız, proxy sunucusu yöneticinize başvurmanız gerekebilir</span><span class="sxs-lookup"><span data-stu-id="f39e8-175">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="f39e8-176">Sorunları tanılamak için Araçlar</span><span class="sxs-lookup"><span data-stu-id="f39e8-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="f39e8-177">Windows Fiddler gibi ağ araçları varsa, aşağıdaki gibi sorunları tanılamak doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f39e8-177">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="f39e8-178">Proxy üzerinden çalışmanız gerekiyorsa, proxy üzerinden bağlanmak için ağ aracınızı yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-178">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="f39e8-179">Ağ aracı tarafından kullanılan bağlantı noktası numarasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f39e8-179">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="f39e8-180">Proxy ayarları Depolama Gezgini olarak yerel ana bilgisayar URL'si ve ağ aracın bağlantı noktası numarası girin.</span><span class="sxs-lookup"><span data-stu-id="f39e8-180">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="f39e8-181">Bu doğru gerçekleştirilir, Ağ aracı yönetimi ve hizmet uç noktaları için Depolama Gezgini tarafından yapılan ağ istekleri günlüğünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="f39e8-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="f39e8-182">Örneğin, bir tarayıcıda blob uç noktanız için https://cawablobgrs.blob.core.windows.net/ girin ve alırsınız yanıt bu verilere erişemez olsa da, kaynağın var, önerir aşağıdakilere benzer.</span><span class="sxs-lookup"><span data-stu-id="f39e8-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![kod örneği](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="f39e8-184">Proxy sunucu yöneticisine başvurun</span><span class="sxs-lookup"><span data-stu-id="f39e8-184">Contact proxy server admin</span></span>

<span data-ttu-id="f39e8-185">Proxy ayarlarınızın doğru olduğunu, proxy sunucusu yöneticinize başvurmanız gerekebilir ve</span><span class="sxs-lookup"><span data-stu-id="f39e8-185">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="f39e8-186">Proxy Azure Yönetimi'ni veya kaynak uç noktaları için trafiği engellemediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-186">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="f39e8-187">Proxy sunucunuz tarafından kullanılan kimlik doğrulama protokolü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-187">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="f39e8-188">Depolama Gezgini NTLM proxy'leri şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f39e8-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="f39e8-189">"Almak alt oluşturulamıyor" hata iletisi</span><span class="sxs-lookup"><span data-stu-id="f39e8-189">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="f39e8-190">Azure için bir proxy üzerinden bağlıysanız, proxy ayarlarının doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-190">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="f39e8-191">Abonelik ya da hesap sahibinden bir kaynağa erişim verilmiş, okuma veya bu kaynak için izinleri listesinde doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-191">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="f39e8-192">SAS URL ile ilgili sorunları</span><span class="sxs-lookup"><span data-stu-id="f39e8-192">Issues with SAS URL</span></span>
<span data-ttu-id="f39e8-193">Bir SAS URL'si kullanarak ve bu hatanın bir hizmete bağlanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="f39e8-193">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="f39e8-194">URL okuma veya kaynakları listelemek için gerekli izinleri sağladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f39e8-194">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="f39e8-195">URL geçmediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-195">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="f39e8-196">SAS URL bir erişim ilkesini temel alarak, erişim ilkesi edilmediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f39e8-196">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f39e8-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f39e8-197">Next steps</span></span>

<span data-ttu-id="f39e8-198">Çözümlerin hiçbiri sizin için çalışıyorsanız, sorununuzu geri bildirim aracı e-posta ile göndermek ve böylece biz, sorunu düzeltmek için başvurabilirsiniz sayıda ayrıntılarını dahil ettiğiniz sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="f39e8-198">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="f39e8-199">Bunu yapmak için tıklatın **yardımcı** menüsüne ve ardından **geri bildirim gönder**.</span><span class="sxs-lookup"><span data-stu-id="f39e8-199">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Geri Bildirim](./media/storage-explorer-troubleshooting/4022503_en_1.png)
