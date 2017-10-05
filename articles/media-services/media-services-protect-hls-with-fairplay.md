---
title: "HLS Microsoft PlayReady veya Apple FairPlay - Azure ile içerik koruma | Microsoft Docs"
description: "Bu konu genel bir bakış sağlar ve Azure Media Services dinamik olarak HTTP canlı akışı (HLS) içeriğinizi Apple FairPlay ile şifrelemek için nasıl kullanılacağını gösterir. Ayrıca, Media Services lisans teslimat hizmetinin istemcilere FairPlay lisansları teslim etmek için nasıl kullanılacağını gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="ac010-104">Apple FairPlay veya Microsoft PlayReady ile içerik, HLS koruma</span><span class="sxs-lookup"><span data-stu-id="ac010-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="ac010-105">Azure Media Services, dinamik olarak HTTP canlı akışı (HLS) içeriğinizi aşağıdaki biçimlerini kullanarak şifrelemenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="ac010-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="ac010-106">**AES-128 Zarf şifresiz anahtar**</span><span class="sxs-lookup"><span data-stu-id="ac010-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="ac010-107">Tüm öbek kullanılarak şifrelenir **AES-128 CBC** modu.</span><span class="sxs-lookup"><span data-stu-id="ac010-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="ac010-108">Şifre çözme akışın iOS ve OS X oyuncu tarafından yerel olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ac010-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="ac010-109">Daha fazla bilgi için bkz: [AES-128 kullanarak dinamik şifreleme ve anahtar teslim hizmeti](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="ac010-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="ac010-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="ac010-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="ac010-111">Tek tek video ve ses örnekleri kullanılarak şifrelenmiş **AES-128 CBC** modu.</span><span class="sxs-lookup"><span data-stu-id="ac010-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="ac010-112">**FairPlay akış** (FPS), cihaz işletim sistemlerinin yerel destek iOS ve Apple TV ile bütünleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ac010-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="ac010-113">OS X üzerinde Safari şifrelenmiş medya Uzantıları (EME) arabirimi desteği kullanarak FPS sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac010-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="ac010-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="ac010-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="ac010-115">Aşağıdaki resimde gösterildiği **HLS + FairPlay veya PlayReady dinamik şifreleme** iş akışı.</span><span class="sxs-lookup"><span data-stu-id="ac010-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Dinamik şifreleme iş akışı diyagramı](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="ac010-117">Bu konuda, Media Services dinamik olarak HLS içeriğinizi Apple FairPlay ile şifrelemek için nasıl kullanılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ac010-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="ac010-118">Ayrıca, Media Services lisans teslimat hizmetinin istemcilere FairPlay lisansları teslim etmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac010-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="ac010-119">Ayrıca, PlayReady HLS içeriğinizle şifrelemek isterseniz, ortak bir içerik anahtarı oluşturup, varlıkla ilişkilendirme gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac010-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="ac010-120">İçerik anahtarının yetkilendirme ilkesini yapılandırma bölümünde açıklandığı gibi etmeniz [dinamik ortak şifreleme kullanarak PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="ac010-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="ac010-121">Gereksinimleri ve konular</span><span class="sxs-lookup"><span data-stu-id="ac010-121">Requirements and considerations</span></span>

<span data-ttu-id="ac010-122">Media Services FairPlay ile şifrelenmiş HLS teslim etmek ve FairPlay lisansları teslim etmeyi kullanırken gerekli şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ac010-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="ac010-123">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ac010-123">An Azure account.</span></span> <span data-ttu-id="ac010-124">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ac010-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="ac010-125">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="ac010-125">A Media Services account.</span></span> <span data-ttu-id="ac010-126">Oluşturmak için bkz: [Azure portalını kullanarak Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ac010-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="ac010-127">İle kaydolmak [Apple geliştirme programı](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="ac010-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="ac010-128">Apple gerektirir almak içerik sahibi [dağıtım paketi](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="ac010-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="ac010-129">Media Services ile anahtar güvenlik modülü (KSM) zaten uygulanan ve son FPS paket isteyen durumu.</span><span class="sxs-lookup"><span data-stu-id="ac010-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="ac010-130">Sertifika oluşturma ve uygulama gizli anahtarı (İSTEYİN) elde etmek için son FPS paketinde yönergeler de vardır.</span><span class="sxs-lookup"><span data-stu-id="ac010-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="ac010-131">ASK FairPlay yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac010-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="ac010-132">Azure Media Services .NET SDK sürümü **3.6.0** veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ac010-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="ac010-133">Media Services anahtar teslim tarafında aşağıdakiler ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ac010-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="ac010-134">**Uygulama sertifika (AC)**: özel anahtarı içeren bir .pfx dosyası budur.</span><span class="sxs-lookup"><span data-stu-id="ac010-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="ac010-135">Bu dosyayı oluşturmak ve bir parolayla şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="ac010-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="ac010-136">Bir anahtar teslim İlkesi yapılandırdığınızda, bu parolayı ve Base64 biçiminde .pfx dosyası sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac010-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="ac010-137">Aşağıdaki adımlar, bir .pfx sertifika dosyası oluşturmak için FairPlay açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="ac010-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="ac010-138">OpenSSL https://slproweb.com/products/Win32OpenSSL.html yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ac010-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="ac010-139">FairPlay sertifika ve Apple tarafından sunulan diğer dosyaların nerede klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="ac010-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="ac010-140">Komut satırından aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac010-140">Run the following command from the command line.</span></span> <span data-ttu-id="ac010-141">Bu .cer dosyasını bir .pem dosyasına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ac010-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="ac010-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509-der bildirmek-fairplay.cer içinde-fairplay out.pem çıkışı</span><span class="sxs-lookup"><span data-stu-id="ac010-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="ac010-143">Komut satırından aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac010-143">Run the following command from the command line.</span></span> <span data-ttu-id="ac010-144">Bu .pem dosyasını özel anahtarla bir .pfx dosyasına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ac010-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="ac010-145">.Pfx dosyası için parolayı sonra OpenSSL tarafından istendi.</span><span class="sxs-lookup"><span data-stu-id="ac010-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="ac010-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12-- out fairplay out.pfx export-inkey privatekey.pem-fairplay out.pem - passin file:privatekey-pem-pass.txt içinde</span><span class="sxs-lookup"><span data-stu-id="ac010-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="ac010-147">**Uygulama sertifika parola**: .pfx dosyasını oluşturmak için parola.</span><span class="sxs-lookup"><span data-stu-id="ac010-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="ac010-148">**Uygulama sertifika parolası kimliği**: parola, bunlar diğer Media Services anahtarları nasıl yüklemek için benzer yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac010-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="ac010-149">Kullanım **ContentKeyType.FairPlayPfxPassword** enum değeri Media Services Kimliği almak için</span><span class="sxs-lookup"><span data-stu-id="ac010-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="ac010-150">Anahtar teslim İlkesi seçeneği kullanmak istedikleri budur.</span><span class="sxs-lookup"><span data-stu-id="ac010-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="ac010-151">**IV**: 16 bayt rastgele bir değeri budur.</span><span class="sxs-lookup"><span data-stu-id="ac010-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="ac010-152">Varlık teslim İlkesi'nde IV eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ac010-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="ac010-153">IV oluşturmak ve her iki yerde de yerleştirin: Varlık teslim ilkesini ve anahtar teslim İlkesi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ac010-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="ac010-154">**SORUN**: Apple Geliştirici Portalı'nı kullanarak sertifika oluşturduğunuzda bu anahtar aldı.</span><span class="sxs-lookup"><span data-stu-id="ac010-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="ac010-155">Her geliştirme ekibi benzersiz ASK alır.</span><span class="sxs-lookup"><span data-stu-id="ac010-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="ac010-156">SOR bir kopyasını kaydedin ve güvenli bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="ac010-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="ac010-157">Daha sonra Media Services'e FairPlayAsk olarak ASK yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac010-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="ac010-158">**SORUN kimliği**: Media Services'e ASK karşıya yüklediğinizde bu kimliği elde edilir.</span><span class="sxs-lookup"><span data-stu-id="ac010-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="ac010-159">Kullanarak ASK yüklemelisiniz **ContentKeyType.FairPlayAsk** enum değeri.</span><span class="sxs-lookup"><span data-stu-id="ac010-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="ac010-160">Sonuç olarak, Media Services ID döndürülür ve ne anahtar teslim İlkesi seçeneği ayarlarken kullanılması gereken budur.</span><span class="sxs-lookup"><span data-stu-id="ac010-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="ac010-161">Şunları FPS istemci tarafından ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac010-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="ac010-162">**Uygulama sertifika (AC)**: Bu işletim sisteminin bazı yükü şifrelemek için kullandığı ortak anahtarı içeren bir.cer/.der dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ac010-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="ac010-163">Media Services player tarafından gerekli olduğu hakkında bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ac010-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="ac010-164">Anahtar teslim hizmeti kullanarak ilgili özel anahtarın şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="ac010-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="ac010-165">FairPlay şifrelenmiş akışı kayıttan için gerçek ASK ilk alın ve ardından gerçek bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac010-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="ac010-166">Bu işlem, tüm üç bölümden oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ac010-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="ac010-167">.DER dosya</span><span class="sxs-lookup"><span data-stu-id="ac010-167">.der file</span></span>
  * <span data-ttu-id="ac010-168">.pfx dosyası</span><span class="sxs-lookup"><span data-stu-id="ac010-168">.pfx file</span></span>
  * <span data-ttu-id="ac010-169">.pfx için parolayı</span><span class="sxs-lookup"><span data-stu-id="ac010-169">password for the .pfx</span></span>

<span data-ttu-id="ac010-170">Aşağıdaki istemciler ile HLS Destek **AES-128 CBC** şifreleme: OS X, Apple TV iOS Safari.</span><span class="sxs-lookup"><span data-stu-id="ac010-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="ac010-171">FairPlay dinamik şifreleme ve lisans teslimat hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac010-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="ac010-172">FairPlay ile varlıklarınızı kullanarak Media Services lisans teslimat hizmeti ve dinamik şifreleme kullanarak koruma için genel adımlar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ac010-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="ac010-173">Bir varlık oluşturun ve dosyaları varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ac010-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="ac010-174">Varlığı, dosyada Uyarlamalı bit hızı MP4 kümesine kodlayın.</span><span class="sxs-lookup"><span data-stu-id="ac010-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="ac010-175">Bir içerik anahtarı oluşturup kodlanmış varlıkla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="ac010-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="ac010-176">İçerik anahtarının yetkilendirme ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ac010-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="ac010-177">Aşağıdakileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="ac010-177">Specify the following:</span></span>

   * <span data-ttu-id="ac010-178">Teslim yöntemi (Bu durumda, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="ac010-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="ac010-179">FairPlay ilkesi seçenekleri yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ac010-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="ac010-180">FairPlay yapılandırma hakkında daha fazla bilgi için bkz **ConfigureFairPlayPolicyOptions()** örnek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ac010-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ac010-181">Genellikle, yalnızca bir sertifika ve ASK kümesi olacağı için yalnızca bir kez FairPlay ilkesi seçeneklerini yapılandırmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="ac010-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="ac010-182">Kısıtlamalar (açık veya belirteç).</span><span class="sxs-lookup"><span data-stu-id="ac010-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="ac010-183">Anahtarın istemciye nasıl teslim edildiğini tanımlayan anahtar teslim türüne özgü bilgiler.</span><span class="sxs-lookup"><span data-stu-id="ac010-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="ac010-184">Varlık teslim ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ac010-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="ac010-185">Teslim ilkesi yapılandırması şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ac010-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="ac010-186">Teslim Protokolü (HLS).</span><span class="sxs-lookup"><span data-stu-id="ac010-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="ac010-187">Dinamik şifreleme (ortak CBC şifreleme) türü.</span><span class="sxs-lookup"><span data-stu-id="ac010-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="ac010-188">Lisans edinme URL'si.</span><span class="sxs-lookup"><span data-stu-id="ac010-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ac010-189">FairPlay ve başka bir dijital hak yönetimi (DRM) sistemiyle şifrelenmiş bir akış teslim etmek istiyorsanız, ayrı teslim ilkeleri yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac010-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="ac010-190">HTTP (DASH) ile ortak şifreleme (CENC) (PlayReady + Widevine) ve kesintisiz PlayReady ile üzerinden dinamik Uyarlamalı akış yapılandırmak için bir IAssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="ac010-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="ac010-191">FairPlay HLS için yapılandırmak için başka bir IAssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="ac010-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="ac010-192">Akış URL'si almak için bir OnDemand Bulucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac010-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="ac010-193">FairPlay anahtar teslim tarafından oynatıcı uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="ac010-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="ac010-194">İOS SDK kullanarak oynatıcı uygulamaları geliştirme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac010-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="ac010-195">FairPlay içeriği yürütmek lisans exchange protokolünü uygulayan gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac010-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="ac010-196">Bu protokol, Apple tarafından belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="ac010-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="ac010-197">Anahtar teslim istekleri göndermek nasıl kadar her bir uygulama olmasından.</span><span class="sxs-lookup"><span data-stu-id="ac010-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="ac010-198">Medya Hizmetleri FairPlay anahtar teslim hizmeti olarak aşağıdaki biçimde bir www-form-url kodlanmış posta iletisi gelmesini SPC bekler:</span><span class="sxs-lookup"><span data-stu-id="ac010-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="ac010-199">Azure Media Player, kutunun dışında FairPlay oynatmayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ac010-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="ac010-200">MAC OS X üzerinde FairPlay kayıttan yürütme almak için Apple Geliştirici hesabından örnek oynatıcı edinin.</span><span class="sxs-lookup"><span data-stu-id="ac010-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="ac010-201">Akış URL'leri</span><span class="sxs-lookup"><span data-stu-id="ac010-201">Streaming URLs</span></span>
<span data-ttu-id="ac010-202">Varlığınızı birden çok DRM ile şifrelenmiş bir şifreleme etiketi akış URL'SİNDE kullanmalısınız: (biçimi 'm3u8-aapl' = şifreleme = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="ac010-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="ac010-203">Aşağıdaki maddeler geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="ac010-203">The following considerations apply:</span></span>

* <span data-ttu-id="ac010-204">Yalnızca sıfır veya bir şifreleme türü belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="ac010-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="ac010-205">Şifreleme türü bir şifreleme varlık için uygulanan yalnızca URL'de belirtilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ac010-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="ac010-206">Şifreleme türü büyük küçük harfe duyarlı değil.</span><span class="sxs-lookup"><span data-stu-id="ac010-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="ac010-207">Aşağıdaki şifreleme türlerini belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="ac010-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="ac010-208">**cenc**: ortak şifreleme (PlayReady veya Widevine)</span><span class="sxs-lookup"><span data-stu-id="ac010-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="ac010-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="ac010-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="ac010-210">**CBC**: AES zarfı şifreleme</span><span class="sxs-lookup"><span data-stu-id="ac010-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ac010-211">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac010-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="ac010-212">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="ac010-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="ac010-213">App.config dosyanızda tanımlanan **appSettings**’e aşağıdaki öğeleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ac010-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="ac010-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="ac010-214">Example</span></span>

<span data-ttu-id="ac010-215">Aşağıdaki örnek Media Services ile FairPlay şifrelenmiş içeriğinizi teslim etmek için kullanma yeteneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ac010-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="ac010-216">Bu işlev Azure Media Services SDK'sı sürüm 3.6.0 .NET için sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ac010-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="ac010-217">Bu bölümde gösterilen kodu Program.cs dosyanızdaki kodun üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="ac010-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="ac010-218">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="ac010-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="ac010-219">Uzun süre boyunca kullanılmak için oluşturulan bulucu ilkeleri gibi aynı günleri / erişim izinlerini sürekli olarak kullanıyorsanız, aynı ilke kimliğini kullanmalısınız (karşıya yükleme olmayan ilkeler için).</span><span class="sxs-lookup"><span data-stu-id="ac010-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="ac010-220">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="ac010-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="ac010-221">Değişkenleri, giriş dosyalarınızın bulunduğu klasörlere işaret edecek şekilde güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ac010-221">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="ac010-222">Sonraki adımlar: Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="ac010-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ac010-223">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="ac010-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
