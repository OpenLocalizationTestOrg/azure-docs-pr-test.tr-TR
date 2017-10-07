---
title: "aaa \"Azure CDN özel etki alanı üzerinde HTTPS etkinleştirme | Microsoft Docs\""
description: "Bilgi nasıl tooenable HTTPS ile özel bir etki alanı Azure CDN uç noktanız üzerinde."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="f9b41-103">Azure CDN özel etki alanı üzerinde HTTPS'yi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f9b41-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="f9b41-104">Azure CDN özel etki alanları için HTTPS desteği, aktarım sırasında verileri kendi etki alanı adı tooimprove hello güvenliğini kullanarak SSL üzerinden toodeliver güvenli içerik sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9b41-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="f9b41-105">Merhaba uçtan uca iş akışı tooenable HTTPS özel etki alanınız için ek ücret ödemeden tüm ile tek tıklatmayla etkinleştirme, eksiksiz bir sertifika yönetimi aracılığıyla basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="f9b41-106">Bu kritik tooensure hello gizlilik ve veri bütünlüğü tüm web uygulamaları gizli veriler aktarım sırasında olur.</span><span class="sxs-lookup"><span data-stu-id="f9b41-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="f9b41-107">HTTPS protokolü üzerinden gönderildiğinde, hassas verilerin şifrelenmesini sağlar hello kullanarak hello Internet.</span><span class="sxs-lookup"><span data-stu-id="f9b41-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="f9b41-108">Sağladığı güven, kimlik doğrulama ve web uygulamalarınızın saldırılara karşı korur.</span><span class="sxs-lookup"><span data-stu-id="f9b41-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="f9b41-109">Şu anda Azure CDN bir CDN uç noktası HTTPS destekler.</span><span class="sxs-lookup"><span data-stu-id="f9b41-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="f9b41-110">Örneğin, Azure CDN (örneğin https://contoso.azureedge.net) bir CDN uç noktası oluşturursanız, HTTPS varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="f9b41-111">Şimdi, özel etki alanı ile HTTPS, güvenli teslimat özel bir etki alanı (örneğin https://www.contoso.com) için de etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="f9b41-112">Merhaba anahtar öznitelikleri HTTPS özelliğinin bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f9b41-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="f9b41-113">Ek ücret ödemeden: sertifika edinme veya yenileme için hiçbir maliyetleri ve HTTPS trafiği için ek ücret ödemeden vardır.</span><span class="sxs-lookup"><span data-stu-id="f9b41-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="f9b41-114">Yalnızca hello CDN gelen GB çıkışı için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="f9b41-115">Basit etkinleştirme: bir tıklatın sağlama kullanılabilir hello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9b41-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f9b41-116">REST API veya diğer geliştirici araçları tooenable hello özelliğini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="f9b41-117">Sertifika yönetimi tamamlamak: tüm tedarik sertifika ve yönetim sizin için işlenir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="f9b41-118">Sertifikaları otomatik olarak sağlanır ve önceki tooexpiration yenilendi.</span><span class="sxs-lookup"><span data-stu-id="f9b41-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="f9b41-119">Bu sertifikanın sona ermesinden sonucu olarak hizmet kesintisi hello risklerini tamamen kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f9b41-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="f9b41-120">Önceki tooenabling HTTPS desteği, önceden oluşturulmuş gereken bir [Azure CDN özel etki alanı](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="f9b41-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="f9b41-121">1. adım: hello özelliğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f9b41-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="f9b41-122">Merhaba, [Azure portal](https://portal.azure.com), tooyour Verizon standart veya premium CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="f9b41-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="f9b41-123">Uç noktaları Hello listesinde özel etki alanınızı içeren hello endpoint tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9b41-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="f9b41-124">Tooenable HTTPS istediğiniz hello özel etki alanını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f9b41-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Uç nokta dikey penceresi](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="f9b41-126">Tıklatın **üzerinde** tooenable HTTPS ve hello değişikliği kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f9b41-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Özel HTTPS iletişim](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="f9b41-128">2. adım: Etki alanı doğrulama</span><span class="sxs-lookup"><span data-stu-id="f9b41-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="f9b41-129">HTTPS etkin özel etki alanınızda önce etki alanı doğrulama tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="f9b41-130">6 iş günleri tooapprove hello etki alanı var.</span><span class="sxs-lookup"><span data-stu-id="f9b41-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="f9b41-131">6 iş günü içinde hiçbir onay ile isteği iptal edilecek.</span><span class="sxs-lookup"><span data-stu-id="f9b41-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="f9b41-132">Özel etki alanınızı üzerindeki HTTPS etkinleştirdikten sonra bizim HTTPS sertifika sağlayıcısı DigiCert etki alanınızın sahipliğini (varsayılan) e-posta veya telefon üzerinden WHOIS registrant bilgilere dayanarak, etki alanı için hello registrant başvurarak doğrular.</span><span class="sxs-lookup"><span data-stu-id="f9b41-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="f9b41-133">DigiCert hello doğrulama e-posta toohello adresleri aşağıda da gönderir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="f9b41-134">WHOIS registrant bilgi özel ise, doğrudan bu adreslerden birinden onaylayabilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9b41-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="f9b41-135">Yönetici @< bilgisayarınızı-etki-name.com zaman > yönetici @< bilgisayarınızı-etki-name.com zaman ></span><span class="sxs-lookup"><span data-stu-id="f9b41-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="f9b41-136">yayımlanması @< bilgisayarınızı-etki-name.com zaman ></span><span class="sxs-lookup"><span data-stu-id="f9b41-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="f9b41-137">hostmaster @< bilgisayarınızı-etki-name.com zaman ></span><span class="sxs-lookup"><span data-stu-id="f9b41-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="f9b41-138">Yöneticisi @< bilgisayarınızı-etki-name.com zaman ></span><span class="sxs-lookup"><span data-stu-id="f9b41-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="f9b41-139">Merhaba e-posta alındıktan sonra iki doğrulama seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="f9b41-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="f9b41-140">Aynı hesap Merhaba hello verilen gelecekteki tüm siparişler onaylayabilirsiniz aynı kök etki alanı, örneğin consoto.com. Tooadd ek özel etki alanlarında hello Merhaba gelecekteki planlıyorsanız bu bir önerilen yaklaşımdır aynı kök etki alanı.</span><span class="sxs-lookup"><span data-stu-id="f9b41-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="f9b41-141">Bu istekte kullanılan hello belirli ana bilgisayar adı yalnızca onaylayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="f9b41-142">Ek onay sonraki istekleri için gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f9b41-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="f9b41-143">Örnek e-posta:</span><span class="sxs-lookup"><span data-stu-id="f9b41-143">Example email:</span></span>
    
    ![Özel HTTPS iletişim](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="f9b41-145">Onay sonrasında DigiCert özel etki alanı adı toohello SAN sertifikanızı ekler.</span><span class="sxs-lookup"><span data-stu-id="f9b41-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="f9b41-146">Merhaba sertifikası bir yıl için geçerli olur ve sona ermeden önce otomatik olarak yenilenir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="f9b41-147">3. adım: hello yayması bekleyin, sonra özelliğini kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f9b41-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="f9b41-148">Merhaba etki alanı adı doğrulandıktan sonra işlemin hello özel etki alanı HTTPS özelliği toobe etkin too6-8 saat sürecek.</span><span class="sxs-lookup"><span data-stu-id="f9b41-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="f9b41-149">Merhaba işlemi tamamlandıktan sonra hello Azure portal hello "özel HTTPS" Durum "Enabled" çok ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f9b41-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="f9b41-150">HTTPS ile özel etki alanınızı artık kullanımınız için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="f9b41-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="f9b41-151">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="f9b41-151">Frequently asked questions</span></span>

1. <span data-ttu-id="f9b41-152">*Merhaba sertifika sağlayıcısı ve ne tür bir sertifika kullanılan kim?*</span><span class="sxs-lookup"><span data-stu-id="f9b41-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="f9b41-153">DigiCert tarafından sağlanan konu alternatif adları (SAN) sertifika kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f9b41-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="f9b41-154">Bir SAN sertifika bir sertifika ile birden fazla tam etki alanı adları güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="f9b41-155">*My ayrılmış sertifika kullanabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="f9b41-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="f9b41-156">Şu anda değil ancak onun üzerinde hello yol haritası.</span><span class="sxs-lookup"><span data-stu-id="f9b41-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="f9b41-157">*DigiCert ne hello etki alanı doğrulama e-posta alıyorum mu?*</span><span class="sxs-lookup"><span data-stu-id="f9b41-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="f9b41-158">24 saat içinde bir e-posta almazsanız, lütfen Microsoft'a başvurun.</span><span class="sxs-lookup"><span data-stu-id="f9b41-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="f9b41-159">*Ayrılmış bir sertifika az güvenli bir SAN sertifikası kullanıyor?*</span><span class="sxs-lookup"><span data-stu-id="f9b41-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="f9b41-160">Aynı şifreleme ve güvenlik standartları bir ayrılmış sertifika olarak aşağıdaki hello bir SAN sertifika. Verilen tüm SSL sertifikaları SHA-256 Gelişmiş server güvenliği için kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="f9b41-161">*Akamai'den Azure CDN ile özel etki alanı HTTPS kullanabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="f9b41-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="f9b41-162">Şu anda bu özellik yalnızca verizon'dan Azure CDN ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f9b41-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="f9b41-163">Bu özellik akamai'den Azure CDN ile Merhaba önümüzdeki aylarda desteklemeye çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="f9b41-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f9b41-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9b41-164">Next steps</span></span>

- <span data-ttu-id="f9b41-165">Bilgi nasıl tooset oluşturan bir [Azure CDN uç noktanız özel etki alanında](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="f9b41-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


