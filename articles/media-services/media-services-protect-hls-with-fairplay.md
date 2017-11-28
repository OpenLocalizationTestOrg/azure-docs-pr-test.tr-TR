---
title: "aaaProtect HLS içerik Microsoft PlayReady veya Apple FairPlay - Azure ile | Microsoft Docs"
description: "Bu konu genel bir bakış sağlar ve nasıl toouse Azure Media Services toodynamically şifrelemek Apple FairPlay, HTTP canlı akışı (HLS) içeriğinizle gösterir. Aynı zamanda, nasıl toouse hello Media Services lisans teslimat hizmeti toodeliver FairPlay lisansları tooclients gösterir."
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
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="89de0-104">Apple FairPlay veya Microsoft PlayReady ile içerik, HLS koruma</span><span class="sxs-lookup"><span data-stu-id="89de0-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="89de0-105">Toodynamically şifrelemek HTTP canlı akışı (HLS) içeriğinizi biçimleri aşağıdaki hello kullanarak azure Media Services etkinleştirir:</span><span class="sxs-lookup"><span data-stu-id="89de0-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="89de0-106">**AES-128 Zarf şifresiz anahtar**</span><span class="sxs-lookup"><span data-stu-id="89de0-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="89de0-107">Merhaba tüm öbek hello kullanılarak şifrelenir **AES-128 CBC** modu.</span><span class="sxs-lookup"><span data-stu-id="89de0-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="89de0-108">Merhaba akış Hello şifrelerinin iOS ve OS X oyuncu tarafından yerel olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="89de0-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="89de0-109">Daha fazla bilgi için bkz: [AES-128 kullanarak dinamik şifreleme ve anahtar teslim hizmeti](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="89de0-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="89de0-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="89de0-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="89de0-111">hello tek tek video ve ses örnekleri hello kullanarak şifrelenir **AES-128 CBC** modu.</span><span class="sxs-lookup"><span data-stu-id="89de0-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="89de0-112">**FairPlay akış** (FPS), iOS ve Apple TV yerel desteğiyle hello cihaz işletim sistemlerinin bütünleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="89de0-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="89de0-113">OS X üzerinde Safari hello şifrelenmiş medya Uzantıları (EME) arabirimi desteği kullanarak FPS sağlar.</span><span class="sxs-lookup"><span data-stu-id="89de0-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="89de0-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="89de0-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="89de0-115">Merhaba aşağıdaki resimde gösterilmiştir hello **HLS + FairPlay veya PlayReady dinamik şifreleme** iş akışı.</span><span class="sxs-lookup"><span data-stu-id="89de0-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Dinamik şifreleme iş akışı diyagramı](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="89de0-117">Bu konuda nasıl toouse Media Services toodynamically şifrelemek HLS içeriğinizi Apple FairPlay ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="89de0-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="89de0-118">Aynı zamanda, nasıl toouse hello Media Services lisans teslimat hizmeti toodeliver FairPlay lisansları tooclients gösterir.</span><span class="sxs-lookup"><span data-stu-id="89de0-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="89de0-119">Ayrıca tooencrypt, HLS PlayReady ile içerik isterseniz, toocreate ortak bir içerik anahtarı gerekir ve Varlığınızı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="89de0-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="89de0-120">Ayrıca tooconfigure hello içerik anahtarının yetkilendirme ilkesini açıklandığı gibi gerekir [dinamik ortak şifreleme kullanarak PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="89de0-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="89de0-121">Gereksinimleri ve konular</span><span class="sxs-lookup"><span data-stu-id="89de0-121">Requirements and considerations</span></span>

<span data-ttu-id="89de0-122">Merhaba HLS şifrelenmiş Media Services toodeliver FairPlay ve toodeliver FairPlay lisansları ile kullanırken gerekli şunlardır:</span><span class="sxs-lookup"><span data-stu-id="89de0-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="89de0-123">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="89de0-123">An Azure account.</span></span> <span data-ttu-id="89de0-124">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="89de0-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="89de0-125">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="89de0-125">A Media Services account.</span></span> <span data-ttu-id="89de0-126">toocreate biri bkz [hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="89de0-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="89de0-127">İle kaydolmak [Apple geliştirme programı](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="89de0-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="89de0-128">Apple gerektirir hello içerik sahibi tooobtain hello [dağıtım paketi](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="89de0-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="89de0-129">Media Services ile anahtar güvenlik modülü (KSM) zaten uygulanan ve hello son FPS paket isteyen durumu.</span><span class="sxs-lookup"><span data-stu-id="89de0-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="89de0-130">Son FPS toogenerate sertifika paketini ve elde hello'ndaki yönergeleri hello uygulama gizli anahtarı (İSTEYİN) vardır.</span><span class="sxs-lookup"><span data-stu-id="89de0-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="89de0-131">ASK tooconfigure FairPlay kullanın.</span><span class="sxs-lookup"><span data-stu-id="89de0-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="89de0-132">Azure Media Services .NET SDK sürümü **3.6.0** veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="89de0-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="89de0-133">Media Services anahtar teslim tarafında şeyler aşağıdaki hello ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="89de0-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="89de0-134">**Uygulama sertifika (AC)**: hello özel anahtarı içeren bir .pfx dosyası budur.</span><span class="sxs-lookup"><span data-stu-id="89de0-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="89de0-135">Bu dosyayı oluşturmak ve bir parolayla şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="89de0-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="89de0-136">Bir anahtar teslim İlkesi yapılandırdığınızda, o parola ve hello .pfx dosyasını Base64 biçiminde sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="89de0-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="89de0-137">Aşağıdaki adımları hello nasıl toogenerate bir .pfx sertifika dosyası için FairPlay açıklar:</span><span class="sxs-lookup"><span data-stu-id="89de0-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="89de0-138">OpenSSL https://slproweb.com/products/Win32OpenSSL.html yükleyin.</span><span class="sxs-lookup"><span data-stu-id="89de0-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="89de0-139">Merhaba FairPlay sertifika ve Apple tarafından sunulan diğer dosyaların nerede toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="89de0-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="89de0-140">Komut hello komut satırından aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89de0-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="89de0-141">Merhaba .cer dosyasını tooa .pem dosyasını dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="89de0-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="89de0-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509-der bildirmek-fairplay.cer içinde-fairplay out.pem çıkışı</span><span class="sxs-lookup"><span data-stu-id="89de0-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="89de0-143">Komut hello komut satırından aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89de0-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="89de0-144">Bu hello .pem tooa .pfx dosyası hello özel anahtarla dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="89de0-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="89de0-145">Merhaba .pfx dosyası için Hello parolayı sonra OpenSSL tarafından istendi.</span><span class="sxs-lookup"><span data-stu-id="89de0-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="89de0-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12-- out fairplay out.pfx export-inkey privatekey.pem-fairplay out.pem - passin file:privatekey-pem-pass.txt içinde</span><span class="sxs-lookup"><span data-stu-id="89de0-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="89de0-147">**Uygulama sertifika parola**: hello .pfx dosyasını oluşturmak için başlangıç parolası.</span><span class="sxs-lookup"><span data-stu-id="89de0-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="89de0-148">**Uygulama sertifika parolası kimliği**: hello parola, benzer toohow diğer Media Services anahtarları bunlar karşıya yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="89de0-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="89de0-149">Kullanım hello **ContentKeyType.FairPlayPfxPassword** enum değeri tooget hello Media Services kimliği</span><span class="sxs-lookup"><span data-stu-id="89de0-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="89de0-150">Bu gereksinim duydukları ne olduğunu toouse hello anahtar teslim İlkesi seçeneği içinde.</span><span class="sxs-lookup"><span data-stu-id="89de0-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="89de0-151">**IV**: 16 bayt rastgele bir değeri budur.</span><span class="sxs-lookup"><span data-stu-id="89de0-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="89de0-152">Bu eşleşmelidir IV hello varlık teslim İlkesi'nde hello.</span><span class="sxs-lookup"><span data-stu-id="89de0-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="89de0-153">Oluşturduğunuz IV hello ve her iki yerde de yerleştirin: hello varlık teslim ilkesini ve hello anahtar teslim İlkesi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="89de0-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="89de0-154">**SORUN**: hello Apple Geliştirici Portalı kullanarak hello sertifika oluşturduğunuzda bu anahtar aldı.</span><span class="sxs-lookup"><span data-stu-id="89de0-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="89de0-155">Her geliştirme ekibi benzersiz ASK alır.</span><span class="sxs-lookup"><span data-stu-id="89de0-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="89de0-156">Merhaba ASK bir kopyasını kaydedin ve güvenli bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="89de0-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="89de0-157">Daha sonra FairPlayAsk tooMedia Hizmetleri olarak tooconfigure ASK ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="89de0-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="89de0-158">**SORUN kimliği**: Media Services'e ASK karşıya yüklediğinizde bu kimliği elde edilir.</span><span class="sxs-lookup"><span data-stu-id="89de0-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="89de0-159">Hello kullanarak ASK yüklemelisiniz **ContentKeyType.FairPlayAsk** enum değeri.</span><span class="sxs-lookup"><span data-stu-id="89de0-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="89de0-160">Merhaba sonucunda hello Media Services ID döndürülür ve ne hello anahtar teslim İlkesi seçeneği ayarlarken kullanılması gereken budur.</span><span class="sxs-lookup"><span data-stu-id="89de0-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="89de0-161">Merhaba şunları FPS istemci tarafı hello tarafından ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="89de0-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="89de0-162">**Uygulama sertifika (AC)**: Bu, bazı yükü hangi hello işletim sisteminin kullandığı tooencrypt hello ortak anahtarı içeren bir.cer/.der dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="89de0-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="89de0-163">Merhaba oynatıcısının gerektirdiğinden Media Services tooknow ilgili gerekir.</span><span class="sxs-lookup"><span data-stu-id="89de0-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="89de0-164">Merhaba anahtar teslim hizmeti hello karşılık gelen özel anahtarı kullanarak şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="89de0-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="89de0-165">tooplay FairPlay şifrelenmiş akış geri, gerçek ASK ilk ulaşmak ve gerçek bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89de0-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="89de0-166">Bu işlem, tüm üç bölümden oluşturur:</span><span class="sxs-lookup"><span data-stu-id="89de0-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="89de0-167">.DER dosya</span><span class="sxs-lookup"><span data-stu-id="89de0-167">.der file</span></span>
  * <span data-ttu-id="89de0-168">.pfx dosyası</span><span class="sxs-lookup"><span data-stu-id="89de0-168">.pfx file</span></span>
  * <span data-ttu-id="89de0-169">Merhaba .pfx için parolayı</span><span class="sxs-lookup"><span data-stu-id="89de0-169">password for hello .pfx</span></span>

<span data-ttu-id="89de0-170">Merhaba aşağıdaki istemcileri desteklemek ile HLS **AES-128 CBC** şifreleme: OS X, Apple TV iOS Safari.</span><span class="sxs-lookup"><span data-stu-id="89de0-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="89de0-171">FairPlay dinamik şifreleme ve lisans teslimat hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89de0-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="89de0-172">Merhaba, FairPlay ile varlıklarınızı hello Media Services lisans teslimat hizmeti kullanarak ve dinamik şifreleme kullanarak koruma için genel adımlar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="89de0-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="89de0-173">Bir varlık oluşturun ve dosyaları hello varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="89de0-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="89de0-174">Merhaba dosya toohello Uyarlamalı bit hızı MP4 kümesine içeren hello varlık kodlayın.</span><span class="sxs-lookup"><span data-stu-id="89de0-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="89de0-175">Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="89de0-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="89de0-176">Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89de0-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="89de0-177">Merhaba aşağıdakileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="89de0-177">Specify hello following:</span></span>

   * <span data-ttu-id="89de0-178">Merhaba teslim yöntemini (Bu durumda, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="89de0-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="89de0-179">FairPlay ilkesi seçenekleri yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="89de0-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="89de0-180">Ayrıntılar için tooconfigure FairPlay, bkz: Merhaba **ConfigureFairPlayPolicyOptions()** aşağıdaki hello örneği yöntemi.</span><span class="sxs-lookup"><span data-stu-id="89de0-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="89de0-181">Genellikle, yalnızca bir sertifika ve ASK kümesi olacağı için yalnızca bir kez tooconfigure FairPlay ilkesi seçenekleri istersiniz.</span><span class="sxs-lookup"><span data-stu-id="89de0-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="89de0-182">Kısıtlamalar (açık veya belirteç).</span><span class="sxs-lookup"><span data-stu-id="89de0-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="89de0-183">Başlangıç anahtarı toohello istemci nasıl teslim edildiğini tanımlayan bilgileri belirli toohello anahtar teslim türüne.</span><span class="sxs-lookup"><span data-stu-id="89de0-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="89de0-184">Merhaba varlık teslim ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89de0-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="89de0-185">Merhaba teslim ilkesi yapılandırması şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="89de0-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="89de0-186">Merhaba teslim Protokolü (HLS).</span><span class="sxs-lookup"><span data-stu-id="89de0-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="89de0-187">dinamik şifreleme (ortak CBC şifreleme) Hello türü.</span><span class="sxs-lookup"><span data-stu-id="89de0-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="89de0-188">Merhaba lisans edinme URL'si.</span><span class="sxs-lookup"><span data-stu-id="89de0-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="89de0-189">Toodeliver FairPlay ve başka bir dijital hak yönetimi (DRM) sistemiyle şifrelenmiş bir akış istiyorsanız, tooconfigure ayrı teslim ilkeleri vardır:</span><span class="sxs-lookup"><span data-stu-id="89de0-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="89de0-190">Bir IAssetDeliveryPolicy tooconfigure dinamik Uyarlamalı akış HTTP (DASH) ile ortak şifreleme (CENC) (PlayReady + Widevine) ve kesintisiz PlayReady ile üzerinden</span><span class="sxs-lookup"><span data-stu-id="89de0-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="89de0-191">Başka bir IAssetDeliveryPolicy tooconfigure FairPlay HLS için</span><span class="sxs-lookup"><span data-stu-id="89de0-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="89de0-192">Bir OnDemand Bulucu tooget bir akış URL'si oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89de0-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="89de0-193">FairPlay anahtar teslim tarafından oynatıcı uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="89de0-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="89de0-194">Merhaba iOS SDK'sını kullanarak oynatıcı uygulamaları geliştirme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89de0-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="89de0-195">toobe mümkün tooplay FairPlay içeriği, tooimplement hello lisans değişimi Protokolü sahip.</span><span class="sxs-lookup"><span data-stu-id="89de0-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="89de0-196">Bu protokol, Apple tarafından belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="89de0-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="89de0-197">Bu, tooeach uygulamasını nasıl toosend anahtar teslim istekleri olur.</span><span class="sxs-lookup"><span data-stu-id="89de0-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="89de0-198">Merhaba Media Services FairPlay anahtar teslim hizmeti hello SPC toocome www-form-url kodlanmış post ileti, form aşağıdaki hello olarak bekler:</span><span class="sxs-lookup"><span data-stu-id="89de0-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="89de0-199">Azure Media Player hello kutusu dışında FairPlay oynatmayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="89de0-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="89de0-200">MAC OS X, tooget FairPlay kayıttan yürütme, Apple developer hesabı hello hello örnek oynatıcı edinin.</span><span class="sxs-lookup"><span data-stu-id="89de0-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="89de0-201">Akış URL'leri</span><span class="sxs-lookup"><span data-stu-id="89de0-201">Streaming URLs</span></span>
<span data-ttu-id="89de0-202">Varlığınızı birden çok DRM ile şifrelenmiş bir şifreleme etiketi akış URL'si hello kullanmalısınız: (biçimi 'm3u8-aapl' = şifreleme = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="89de0-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="89de0-203">ilgili önemli noktalar aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="89de0-203">hello following considerations apply:</span></span>

* <span data-ttu-id="89de0-204">Yalnızca sıfır veya bir şifreleme türü belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="89de0-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="89de0-205">Merhaba şifreleme türü bir şifreleme uygulanan toohello varlık ise yalnızca hello URL'SİNDE belirtilen toobe sahip değil.</span><span class="sxs-lookup"><span data-stu-id="89de0-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="89de0-206">Merhaba şifreleme türü büyük küçük harfe duyarlı değil.</span><span class="sxs-lookup"><span data-stu-id="89de0-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="89de0-207">şu şifreleme türlerini hello belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="89de0-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="89de0-208">**cenc**: ortak şifreleme (PlayReady veya Widevine)</span><span class="sxs-lookup"><span data-stu-id="89de0-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="89de0-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="89de0-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="89de0-210">**CBC**: AES zarfı şifreleme</span><span class="sxs-lookup"><span data-stu-id="89de0-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="89de0-211">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89de0-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="89de0-212">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="89de0-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="89de0-213">Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="89de0-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="89de0-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="89de0-214">Example</span></span>

<span data-ttu-id="89de0-215">örnek aşağıdaki hello hello özelliği toouse Media Services toodeliver FairPlay ile şifrelenmiş içeriğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="89de0-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="89de0-216">Bu işlevsellik için .NET sürüm 3.6.0 hello Azure Media Services SDK'sı sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="89de0-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="89de0-217">Bu bölümde gösterilen hello koduyla Hello kodu Program.cs dosyanızdaki üzerine.</span><span class="sxs-lookup"><span data-stu-id="89de0-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="89de0-218">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="89de0-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="89de0-219">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="89de0-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="89de0-220">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="89de0-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="89de0-221">Emin tooupdate değişkenleri, giriş dosyalarınızın bulunduğu toopoint toofolders olun.</span><span class="sxs-lookup"><span data-stu-id="89de0-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
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

            // Associate hello key with hello asset.
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

            // Associate hello content key authorization policy with hello content key.
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

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="89de0-222">Sonraki adımlar: Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="89de0-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="89de0-223">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="89de0-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
