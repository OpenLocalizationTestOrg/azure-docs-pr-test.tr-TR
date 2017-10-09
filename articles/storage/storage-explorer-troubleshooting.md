---
title: "aaaAzure Depolama Gezgini sorun giderme kılavuzu | Microsoft Docs"
description: "Azure hello iki hata ayıklama özelliğine genel bakış"
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
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="8563b-103">Azure Storage Gezgini sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8563b-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="8563b-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="8563b-104">Introduction</span></span>

<span data-ttu-id="8563b-105">Microsoft Azure Storage Gezgini (Önizleme), Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan tek başına bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="8563b-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="8563b-106">Merhaba uygulaması Azure, Sovereign Bulutlar ve Azure yığın üzerinde barındırılan toStorage hesapları bağlanabilirler.</span><span class="sxs-lookup"><span data-stu-id="8563b-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="8563b-107">Bu kılavuz, depolama Gezgini'nde görülen yaygın sorunlar için çözümleri özetler.</span><span class="sxs-lookup"><span data-stu-id="8563b-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="8563b-108">Oturum açma sorunları</span><span class="sxs-lookup"><span data-stu-id="8563b-108">Sign in issues</span></span>

<span data-ttu-id="8563b-109">Yalnızca Azure Active Directory (AAD) hesapları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8563b-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="8563b-110">Bir ADFS hesabını kullanıyorsanız, bu Explorer işe yaramayacaktır tooStorage içinde imzalama beklenen.</span><span class="sxs-lookup"><span data-stu-id="8563b-110">If you use an ADFS account, it’s expected that signing in tooStorage Explorer would not work.</span></span> <span data-ttu-id="8563b-111">Devam etmeden önce uygulamanızı yeniden başlatmayı deneyin ve hello sorunların giderilip giderilemeyeceğini bakın.</span><span class="sxs-lookup"><span data-stu-id="8563b-111">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="8563b-112">Hatası: Sertifika zincirindeki otomatik olarak imzalanan sertifika</span><span class="sxs-lookup"><span data-stu-id="8563b-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="8563b-113">Neden bu hatayla karşılaşabilirsiniz ve hello en yaygın iki sebepleri şunlardır birkaç nedeni vardır:</span><span class="sxs-lookup"><span data-stu-id="8563b-113">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="8563b-114">Merhaba uygulaması "(örneğin, şirket sunucunuzun) bir sunucu HTTPS trafiği kesintiye uğratan, şifre çözme ve kendinden imzalı bir sertifika kullanarak şifreleme anlamı saydam bir proxy", bağlı.</span><span class="sxs-lookup"><span data-stu-id="8563b-114">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="8563b-115">Bir uygulama otomatik olarak imzalanan bir SSL sertifikası aldığınız hello HTTPS iletilere injecting virüsten koruma yazılımı gibi çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="8563b-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="8563b-116">Depolama Gezgini hello sorunları karşılaştığında, artık alınan hello HTTPS ileti oynanmadığını bilebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8563b-116">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="8563b-117">Merhaba otomatik olarak imzalanan sertifika bir kopyasına sahipseniz, bu güven Depolama Gezgini izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8563b-117">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="8563b-118">Merhaba sertifika injecting emin değilseniz, bu adımları toofind izleyin:</span><span class="sxs-lookup"><span data-stu-id="8563b-118">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="8563b-119">Açık SSL yükleyin</span><span class="sxs-lookup"><span data-stu-id="8563b-119">Install Open SSL</span></span>

    - <span data-ttu-id="8563b-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (Merhaba hafif sürümlerinin herhangi birinin yeterli olmalıdır)</span><span class="sxs-lookup"><span data-stu-id="8563b-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="8563b-121">Mac ve Linux: işletim sisteminizle eklenmelidir</span><span class="sxs-lookup"><span data-stu-id="8563b-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="8563b-122">Açık SSL çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8563b-122">Run Open SSL</span></span>

    - <span data-ttu-id="8563b-123">Windows: hello yükleme dizinini açın, **/bin/**, çift tıklayın ve ardından **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="8563b-123">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="8563b-124">Mac ve Linux: çalıştırmak **openssl** bir terminal gelen.</span><span class="sxs-lookup"><span data-stu-id="8563b-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="8563b-125">S_client - showcerts yürütme-microsoft.com:443 Bağlan</span><span class="sxs-lookup"><span data-stu-id="8563b-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="8563b-126">Otomatik olarak imzalanan sertifikalar arayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-126">Look for self-signed certificates.</span></span> <span data-ttu-id="8563b-127">Kendinden imzalı olduğu emin değilseniz, herhangi bir yere hello konu ("%s") arayın ve veren ("i:") aynı hello şunlardır.</span><span class="sxs-lookup"><span data-stu-id="8563b-127">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="8563b-128">Herhangi bir otomatik olarak imzalanan sertifika bulduğunuzda, her biri için kopyalayıp her şeyi ilk ve son dahil olmak üzere **---başlangıç sertifika---** çok**---son SERTİFİKAYI---** tooa yeni .cer dosyası.</span><span class="sxs-lookup"><span data-stu-id="8563b-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="8563b-129">Depolama Gezgini'ni açın, **Düzenle** > **SSL sertifikalarını** > **alma sertifikaları**ve ardından kullanım hello dosya Seçici toofind, seçin ve oluşturduğunuz hello .cer dosyaları açın.</span><span class="sxs-lookup"><span data-stu-id="8563b-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="8563b-130">Merhaba yukarıdaki adımları kullanarak herhangi bir otomatik olarak imzalanan sertifika bulamazsanız, daha fazla yardım için hello geri bildirim araçla bize başvurun.</span><span class="sxs-lookup"><span data-stu-id="8563b-130">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="8563b-131">%S tooretrieve abonelikleri</span><span class="sxs-lookup"><span data-stu-id="8563b-131">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="8563b-132">Bu adımları tootroubleshoot aboneliklerinizi çalıştırdıktan sonra başarıyla oturum açamıyor tooretrieve varsa, bu sorunu izleyin:</span><span class="sxs-lookup"><span data-stu-id="8563b-132">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="8563b-133">Azure portal hello imzalayarak hesabınıza erişim toohello abonelikleri olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-133">Verify that your account has access toohello subscriptions by signing into hello Azure portal.</span></span>

- <span data-ttu-id="8563b-134">Merhaba doğru ortam (Azure, Azure Çin, Azure Almanya, Azure ABD devlet kurumları veya özel ortam/Azure yığın) kullanarak imzaladığınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="8563b-134">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="8563b-135">Bir proxy'nin arkasında varsa, hello Depolama Gezgini proxy düzgün şekilde yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8563b-135">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="8563b-136">Kaldırarak ve yeniden ekleniyor hello hesap deneyin.</span><span class="sxs-lookup"><span data-stu-id="8563b-136">Try removing and readding hello account.</span></span>

- <span data-ttu-id="8563b-137">Aşağıdaki dosyaları kök dizini (diğer bir deyişle, C:\Users\ContosoUser) ve ardından hello hesabı yeniden ekleyerek hello silmeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="8563b-137">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="8563b-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="8563b-138">.adalcache</span></span>

    - <span data-ttu-id="8563b-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="8563b-139">.devaccounts</span></span>

    - <span data-ttu-id="8563b-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="8563b-140">.extaccounts</span></span>

- <span data-ttu-id="8563b-141">İzleme hello geliştirici araçları konsolunu (F12 tuşuna basarak tarafından) ne zaman, imzaladığınız herhangi bir hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="8563b-141">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Geliştirici Araçları](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="8563b-143">%S toosee hello kimlik doğrulaması sayfası</span><span class="sxs-lookup"><span data-stu-id="8563b-143">Unable toosee hello authentication page</span></span>

<span data-ttu-id="8563b-144">Bu adımları tootroubleshoot oluşturulamıyor toosee hello kimlik doğrulaması sayfa varsa, bu sorunu izleyin:</span><span class="sxs-lookup"><span data-stu-id="8563b-144">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="8563b-145">Bağlantınızı Hello hızına bağlı olarak, bu hello oturum açma sayfası tooload için sürebilir, hello kimlik doğrulama iletişim kutusunu kapatmadan önce en az bir dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="8563b-145">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="8563b-146">Bir proxy'nin arkasında varsa, hello Depolama Gezgini proxy düzgün şekilde yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8563b-146">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="8563b-147">Merhaba F12 tuşuna basarak hello Geliştirici konsol görünümü.</span><span class="sxs-lookup"><span data-stu-id="8563b-147">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="8563b-148">Hello Geliştirici konsolundan Hello yanıtlarını izleyin ve tüm ipucu için neden Bul olup olmadığını görmek kimlik doğrulaması çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="8563b-148">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="8563b-149">Hesabını kaldıramaz</span><span class="sxs-lookup"><span data-stu-id="8563b-149">Cannot remove account</span></span>

<span data-ttu-id="8563b-150">Yüklenemiyor tooremove hesabınız yoksa veya hello yeniden kimlik doğrula bağlantı herhangi bir şey yapmanız durumunda, bu adımları tootroubleshoot bu sorunu izleyin:</span><span class="sxs-lookup"><span data-stu-id="8563b-150">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="8563b-151">Kök dizininden aşağıdaki dosyaları ve hello hesabı yeniden ekleniyor hello silmeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="8563b-151">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="8563b-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="8563b-152">.adalcache</span></span>

    - <span data-ttu-id="8563b-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="8563b-153">.devaccounts</span></span>

    - <span data-ttu-id="8563b-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="8563b-154">.extaccounts</span></span>

- <span data-ttu-id="8563b-155">Depolama kaynaklarını tooremove SAS bağlı istiyorsanız, aşağıdaki dosyaları hello silin:</span><span class="sxs-lookup"><span data-stu-id="8563b-155">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="8563b-156">Windows için %appdata%/StorageExplorer klasör</span><span class="sxs-lookup"><span data-stu-id="8563b-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="8563b-157">/Users/ < adiniz >/kitaplık/uygulaması destek/StorageExplorer Mac için</span><span class="sxs-lookup"><span data-stu-id="8563b-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="8563b-158">Linux için ~/.config/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="8563b-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="8563b-159">Bu dosyaları silerseniz, tüm kimlik bilgilerinizi tooreenter gerekir.</span><span class="sxs-lookup"><span data-stu-id="8563b-159">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="8563b-160">Proxy sorunları</span><span class="sxs-lookup"><span data-stu-id="8563b-160">Proxy issues</span></span>

<span data-ttu-id="8563b-161">İlk olarak, girdiğiniz bilgileri aşağıdaki o hello tüm doğru olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="8563b-161">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="8563b-162">Merhaba proxy URL'si ve bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="8563b-162">hello proxy URL and port number</span></span>

- <span data-ttu-id="8563b-163">Kullanıcı adı ve parola hello proxy tarafından gerekirse</span><span class="sxs-lookup"><span data-stu-id="8563b-163">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="8563b-164">Yaygın çözümleri</span><span class="sxs-lookup"><span data-stu-id="8563b-164">Common solutions</span></span>

<span data-ttu-id="8563b-165">Sorunları yaşamaya devam ediyorsanız, bu adımları tootroubleshoot izleyin bunları:</span><span class="sxs-lookup"><span data-stu-id="8563b-165">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="8563b-166">Toohello Internet proxy kullanmadan bağlanabiliyorsa Depolama Gezgini proxy ayarlarının etkin çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-166">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="8563b-167">Merhaba Durum buysa, proxy ayarlarınızı ile ilgili bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="8563b-167">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="8563b-168">Proxy yönetici tooidentify hello sorunlarınızı ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="8563b-168">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="8563b-169">Merhaba proxy sunucusu kullanan diğer uygulamalar beklendiği gibi çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-169">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="8563b-170">Toohello Microsoft Azure portal, web tarayıcısı kullanarak bağlanabildiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8563b-170">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="8563b-171">Hizmet uç noktalarından yanıtları alabilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="8563b-172">Uç nokta URL'leri birini tarayıcınıza girin.</span><span class="sxs-lookup"><span data-stu-id="8563b-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="8563b-173">Bağlanabiliyorsanız, bir InvalidQueryParameterValue veya benzeri bir XML yanıt almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8563b-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="8563b-174">Başka biri de Depolama Gezgini proxy sunucunuz ile kullanıyorsa, bunlar bağlanabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="8563b-175">Bağlanabiliyorsanız, proxy sunucu yöneticinizle toocontact olabilir.</span><span class="sxs-lookup"><span data-stu-id="8563b-175">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="8563b-176">Sorunları tanılamak için Araçlar</span><span class="sxs-lookup"><span data-stu-id="8563b-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="8563b-177">Windows Fiddler gibi ağ araçları varsa, mümkün toodiagnose hello sorunlar gibi olabilir:</span><span class="sxs-lookup"><span data-stu-id="8563b-177">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="8563b-178">Proxy üzerinden toowork varsa, Ağ aracı tooconnect hello proxy'si aracılığıyla tooconfigure olabilir.</span><span class="sxs-lookup"><span data-stu-id="8563b-178">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="8563b-179">Ağ aracı tarafından kullanılan başlangıç bağlantı noktası numarasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="8563b-179">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="8563b-180">Merhaba yerel ana bilgisayar URL'sini ve proxy ayarları Depolama Gezgini olarak aracın bağlantı noktası numarası ağ hello girin.</span><span class="sxs-lookup"><span data-stu-id="8563b-180">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="8563b-181">Bu doğru gerçekleştirilir, ağ aracınızı Depolama Gezgini toomanagement ve hizmet uç noktaları tarafından yapılan ağ istekleri günlüğünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="8563b-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="8563b-182">Örneğin, bir tarayıcıda blob uç noktanız için https://cawablobgrs.blob.core.windows.net/ girin ve bir yanıtı alırsınız Bu verilere erişemez olsa da, hello kaynak var, öneren hello aşağıdakine benzer.</span><span class="sxs-lookup"><span data-stu-id="8563b-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![kod örneği](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="8563b-184">Proxy sunucu yöneticisine başvurun</span><span class="sxs-lookup"><span data-stu-id="8563b-184">Contact proxy server admin</span></span>

<span data-ttu-id="8563b-185">Proxy ayarlarınızın doğru olduğunu, proxy sunucusu yöneticinize toocontact olabilir ve</span><span class="sxs-lookup"><span data-stu-id="8563b-185">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="8563b-186">Proxy trafiği tooAzure yönetim veya kaynak uç noktaları engellemez emin olun.</span><span class="sxs-lookup"><span data-stu-id="8563b-186">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="8563b-187">Proxy sunucunuz tarafından kullanılan hello kimlik doğrulama protokolü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-187">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="8563b-188">Depolama Gezgini NTLM proxy'leri şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="8563b-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="8563b-189">"Oluşturulamıyor tooRetrieve alt" hata iletisi</span><span class="sxs-lookup"><span data-stu-id="8563b-189">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="8563b-190">Bir proxy üzerinden bağlı tooAzure varsa, proxy ayarlarının doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8563b-190">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="8563b-191">Merhaba aboneliği veya hesabı hello sahibinden erişim tooa kaynak verilmiş, okuma veya bu kaynak için izinleri listesinde doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-191">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="8563b-192">SAS URL ile ilgili sorunları</span><span class="sxs-lookup"><span data-stu-id="8563b-192">Issues with SAS URL</span></span>
<span data-ttu-id="8563b-193">Bir SAS URL'si kullanarak ve bu hatanın tooa hizmeti bağlanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="8563b-193">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="8563b-194">Merhaba URL tooread veya liste kaynakları hello gerekli izinleri sağladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="8563b-194">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="8563b-195">URL süresi geçmemiş bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-195">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="8563b-196">Merhaba SAS URL bir erişim ilkesini temel alarak, hello erişim ilkesi edilmediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8563b-196">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8563b-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8563b-197">Next steps</span></span>

<span data-ttu-id="8563b-198">Hello çözümleri hiçbiri sizin için çalışıyorsanız, sorununuzu hello geri bildirim araçla e-posta ile gönderme ve böylece sizinle hello sorunu düzeltmek için iletişime geçebiliriz sayıda ayrıntılarını dahil ettiğiniz hello sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="8563b-198">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="8563b-199">toodo bunu, **yardımcı** menüsüne ve ardından **geri bildirim gönder**.</span><span class="sxs-lookup"><span data-stu-id="8563b-199">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Geri Bildirim](./media/storage-explorer-troubleshooting/4022503_en_1.png)
