---
title: "aaaTroubleshoot Azure noktası site bağlantısı sorunlarını giderme | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot noktadan siteye bağlantı sorunları."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="6d5f2-103">Giderme: Azure noktadan siteye bağlantı sorunlarını</span><span class="sxs-lookup"><span data-stu-id="6d5f2-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="6d5f2-104">Bu makalede karşılaşabileceğiniz genel noktadan siteye bağlantı sorunları listeler.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="6d5f2-105">Ayrıca bu sorunlar için olası nedenler ve çözümler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="6d5f2-106">VPN istemci hatası: bir sertifika bulunamadı</span><span class="sxs-lookup"><span data-stu-id="6d5f2-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-107">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-107">Symptom</span></span>

<span data-ttu-id="6d5f2-108">Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-109">**Bu Genişletilebilir kimlik doğrulama protokolü ile kullanılabilir bir sertifika bulunamadı. (Hata 798)**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-110">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-110">Cause</span></span>

<span data-ttu-id="6d5f2-111">Merhaba istemci sertifikası eksik Bu sorun oluşur **Sertifikalar - Geçerli User\Personal\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-112">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-112">Solution</span></span>

<span data-ttu-id="6d5f2-113">Bu hello istemci sertifikası (Certmgr.msc) hello sertifika deposunun konumu aşağıdaki hello yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="6d5f2-114">**Sertifikalar - Geçerli User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="6d5f2-115">Nasıl tooinstall hello istemci sertifikası hakkında daha fazla bilgi için bkz: [noktadan siteye bağlantıları için oluşturma ve verme sertifikaları](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="6d5f2-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6d5f2-116">Merhaba istemci sertifikasını içeri aktardığınızda hello seçmeyin **güçlü özel anahtar korumasını etkinleştir** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="6d5f2-117">VPN istemci hatası: beklenmeyen veya hatalı biçimlendirilmiş hello ileti alındı</span><span class="sxs-lookup"><span data-stu-id="6d5f2-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-118">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-118">Symptom</span></span>

<span data-ttu-id="6d5f2-119">Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-120">**beklenmeyen veya hatalı biçimlendirilmiş hello iletisi alındı. (Hata 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-121">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-121">Cause</span></span>

<span data-ttu-id="6d5f2-122">Merhaba kök sertifika genel anahtarı hello Azure VPN ağ geçidine yüklenmemiştir Bu sorun oluşur.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="6d5f2-123">Başlangıç anahtarı bozuk veya süresi dolmuş da oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-124">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-124">Solution</span></span>

<span data-ttu-id="6d5f2-125">Bu sorun, hello kök hello durumunu kontrol sertifika hello Azure portal toosee iptal edildi olup olmadığını tooresolve.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="6d5f2-126">Bunu iptal edilmediğini, toodelete hello kök sertifikasını ve reupload deneyin.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="6d5f2-127">Daha fazla bilgi için bkz: [oluşturma sertifikaları](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="6d5f2-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="6d5f2-128">VPN istemci hatası: bir sertifika zinciri işlendi, ancak sona erdi</span><span class="sxs-lookup"><span data-stu-id="6d5f2-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="6d5f2-129">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-129">Symptom</span></span> 

<span data-ttu-id="6d5f2-130">Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-131">**Bir sertifika zinciri işlendi, ancak hello güven sağlayıcısı tarafından güvenilmeyen bir kök sertifika sona erdi.**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-132">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-132">Solution</span></span>

1. <span data-ttu-id="6d5f2-133">Sertifika aşağıdaki o hello hello doğru konumda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="6d5f2-134">Sertifika</span><span class="sxs-lookup"><span data-stu-id="6d5f2-134">Certificate</span></span> | <span data-ttu-id="6d5f2-135">Konum</span><span class="sxs-lookup"><span data-stu-id="6d5f2-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="6d5f2-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="6d5f2-136">AzureClient.pfx</span></span>  | <span data-ttu-id="6d5f2-137">Geçerli User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="6d5f2-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="6d5f2-138">Azuregateway -*GUID*. cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="6d5f2-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="6d5f2-139">Geçerli User\Trusted kök sertifika yetkilileri</span><span class="sxs-lookup"><span data-stu-id="6d5f2-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="6d5f2-140">AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="6d5f2-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="6d5f2-141">Yerel bilgisayar/güvenilen kök sertifika yetkilileri</span><span class="sxs-lookup"><span data-stu-id="6d5f2-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="6d5f2-142">Merhaba sertifikaları hello konumda zaten varsa, toodelete hello sertifikaları deneyin ve yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="6d5f2-143">Merhaba  **azuregateway -*GUID*. hello Azure portal ' yüklenen hello VPN istemcisi yapılandırma paketini cloudapp.net** sertifika konusu.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="6d5f2-144">Dosya archivers tooextract hello dosyaları hello paketten kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="6d5f2-145">Dosya indirme hatası: hedef URI belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="6d5f2-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-146">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-146">Symptom</span></span>

<span data-ttu-id="6d5f2-147">Merhaba aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-147">You receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-148">**Dosya indirme hatası. Hedef URI belirtilmedi.**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-149">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-149">Cause</span></span> 

<span data-ttu-id="6d5f2-150">Bu sorun bir hatalı ağ geçidi türü nedeniyle oluşur.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="6d5f2-151">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-151">Solution</span></span>

<span data-ttu-id="6d5f2-152">Merhaba VPN ağ geçidi türü olmalıdır **VPN**, ve hello VPN türü olmalıdır **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="6d5f2-153">VPN istemci hatası: Azure VPN özel komut başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="6d5f2-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="6d5f2-154">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-154">Symptom</span></span>

<span data-ttu-id="6d5f2-155">Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-156">**Özel bir komut dosyası (tooupdate, yönlendirme tablosu) başarısız oldu. (Hata 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-157">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-157">Cause</span></span>

<span data-ttu-id="6d5f2-158">Kısayol kullanarak tooopen hello site noktası VPN bağlantısı çalışıyorsanız, bu sorun ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-159">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-159">Solution</span></span> 

<span data-ttu-id="6d5f2-160">Merhaba kısayoldan açmadan yerine doğrudan hello VPN paketini açın.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="6d5f2-161">Merhaba VPN istemcisi yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="6d5f2-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-162">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-162">Cause</span></span> 

<span data-ttu-id="6d5f2-163">Sanal ağınız için gerekli tootrust hello VPN ağ geçidi bir ek sertifikadır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="6d5f2-164">Merhaba sertifika hello Azure portal ' oluşturulan hello VPN istemcisi yapılandırma paketini dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-165">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-165">Solution</span></span>

<span data-ttu-id="6d5f2-166">Merhaba VPN istemcisi yapılandırma paketini ayıklayın ve hello .cer dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="6d5f2-167">tooinstall hello sertifika, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="6d5f2-168">MMC.exe açın.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="6d5f2-169">Merhaba eklemek **sertifikaları** ek bileşenini.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="6d5f2-170">Select hello **bilgisayar** hesap hello yerel bilgisayar için.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="6d5f2-171">Sağ hello **güvenilen kök sertifika yetkilileri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="6d5f2-172">Tıklatın **tüm görev** > **alma**ve hello VPN istemci yapılandırma paketi ayıkladığınız gözatma toohello .cer dosyası.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="6d5f2-173">Merhaba bilgisayarı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="6d5f2-174">Tooinstall hello VPN istemcisi deneyin.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="6d5f2-175">Azure portal hata: toosave hello VPN ağ geçidi başarısız oldu ve hello verileri geçersiz</span><span class="sxs-lookup"><span data-stu-id="6d5f2-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-176">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-176">Symptom</span></span>

<span data-ttu-id="6d5f2-177">Hello Azure portal hello VPN ağ geçidi için toosave hello değişiklikleri çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-178">**Başarısız toosave sanal ağ geçidi &lt;* ağ geçidi adı*&gt;.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="6d5f2-179">Sertifikasının verileri &lt; *kimliği sertifika* &gt; olan invalid.* *</span><span class="sxs-lookup"><span data-stu-id="6d5f2-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-180">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-180">Cause</span></span> 

<span data-ttu-id="6d5f2-181">Yüklediğiniz hello kök sertifikanın ortak anahtarı bir alanı gibi geçersiz bir karakter içeriyorsa, bu sorun ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-182">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-182">Solution</span></span>

<span data-ttu-id="6d5f2-183">Merhaba sertifikada Hello veri satır sonları (satır başı) gibi geçersiz karakterler içermediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="6d5f2-184">Merhaba tüm değer uzun bir satır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-184">hello entire value should be one long line.</span></span> <span data-ttu-id="6d5f2-185">metin aşağıdaki hello hello sertifika örneğidir:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="6d5f2-186">Azure portal hata: toosave hello VPN ağ geçidi başarısız oldu ve hello kaynak adı geçersiz</span><span class="sxs-lookup"><span data-stu-id="6d5f2-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-187">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-187">Symptom</span></span>

<span data-ttu-id="6d5f2-188">Hello Azure portal hello VPN ağ geçidi için toosave hello değişiklikleri çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="6d5f2-189">**Başarısız toosave sanal ağ geçidi &lt;* ağ geçidi adı*&gt;.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="6d5f2-190">Kaynak adı &lt; *tooupload deneyin sertifika adı* &gt; geçersiz ** değil.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-191">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-191">Cause</span></span>

<span data-ttu-id="6d5f2-192">Merhaba sertifikanın Hello adı bir boşluk gibi geçersiz bir karakter içerdiğinden bu sorun oluşur.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="6d5f2-193">Azure portal hata: VPN paket dosyasını indirme hatası 503</span><span class="sxs-lookup"><span data-stu-id="6d5f2-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-194">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-194">Symptom</span></span>

<span data-ttu-id="6d5f2-195">Toodownload hello VPN istemcisi yapılandırma paketini çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="6d5f2-196">**Toodownload hello dosyası açılamadı. Hata ayrıntıları: 503 hatası. Merhaba sunucu meşgul.**</span><span class="sxs-lookup"><span data-stu-id="6d5f2-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="6d5f2-197">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-197">Solution</span></span>

<span data-ttu-id="6d5f2-198">Bu hata geçici bir ağ sorunu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="6d5f2-199">Toodownload hello VPN paketi birkaç dakika sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="6d5f2-200">Azure VPN ağ geçidi yükseltme: tüm P2S istemcileridir oluşturulamıyor tooconnect</span><span class="sxs-lookup"><span data-stu-id="6d5f2-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-201">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-201">Cause</span></span>

<span data-ttu-id="6d5f2-202">Merhaba sertifika yüzde 50'den fazla ise yaşam hello sertifika alındı.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-203">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-203">Solution</span></span>

<span data-ttu-id="6d5f2-204">tooresolve bu sorunu oluşturun ve yeni sertifikalar toohello VPN istemcileri yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="6d5f2-205">Çok fazla VPN istemcileri aynı anda bağlı</span><span class="sxs-lookup"><span data-stu-id="6d5f2-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="6d5f2-206">Her VPN ağ geçidi için hello en fazla izin verilen bağlantı sayısı 128'dir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="6d5f2-207">Hello Azure portal'ın bağlanan istemcilerin toplam sayısı hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="6d5f2-208">Noktadan siteye VPN yanlış 10.0.0.0/8 toohello yol tablosu için bir yol ekler</span><span class="sxs-lookup"><span data-stu-id="6d5f2-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-209">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-209">Symptom</span></span>

<span data-ttu-id="6d5f2-210">Merhaba hello noktadan siteye istemci VPN bağlantısıyla çevirdiğinizde hello VPN istemcisi hello Azure sanal ağı doğru bir yol eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="6d5f2-211">Merhaba IP yardımcı hizmeti hello alt hello VPN istemcileri için bir rota eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="6d5f2-212">Merhaba VPN istemci aralığı 10.0.12.0/24 gibi 10.0.0.0/8 tooa daha küçük alt aittir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="6d5f2-213">10.0.12.0/24 için bir yol yerine, daha yüksek önceliğe sahip 10.0.0.0/8 için bir rota eklenir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="6d5f2-214">Bu yanlış yol tanımlanan belirli bir yolu olmayan tooanother alt 10.50.0.0/24 gibi hello 10.0.0.0/8 aralıkta ait diğer şirket içi ağlar ile bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="6d5f2-215">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-215">Cause</span></span>

<span data-ttu-id="6d5f2-216">Bu davranış, Windows istemcileri için tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="6d5f2-217">Hello istemci hello PPP IPCP protokol kullandığında, hello hello tünel arabirimi için IP adresi (Merhaba VPN ağ geçidi bu durumda) hello sunucusundan alır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="6d5f2-218">Ancak, hello protokolünde bir sınırlama nedeniyle hello alt ağ maskesi hello istemci sahip değil.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="6d5f2-219">Başka bir şekilde tooget olduğundan, hello istemci tooguess hello alt ağ maskesi hello tünel arabirimi IP adresi hello sınıfına göre çalışır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="6d5f2-220">Bu nedenle, bir yol statik eşleme aşağıdaki hello göre eklenir:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="6d5f2-221">Adres tooclass A aitse--> /8 Uygula</span><span class="sxs-lookup"><span data-stu-id="6d5f2-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="6d5f2-222">Adres aitse B--> tooclass /16 Uygula</span><span class="sxs-lookup"><span data-stu-id="6d5f2-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="6d5f2-223">Adres aitse C--> tooclass /24 Uygula</span><span class="sxs-lookup"><span data-stu-id="6d5f2-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="6d5f2-224">VPN istemcisi ağ dosya paylaşımlarına erişemez</span><span class="sxs-lookup"><span data-stu-id="6d5f2-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-225">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-225">Symptom</span></span>

<span data-ttu-id="6d5f2-226">Merhaba VPN istemci toohello Azure sanal ağı bağlandı.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="6d5f2-227">Ancak, hello istemci ağ paylaşımlarına erişemez.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="6d5f2-228">Nedeni</span><span class="sxs-lookup"><span data-stu-id="6d5f2-228">Cause</span></span>

<span data-ttu-id="6d5f2-229">Merhaba SMB protokolü dosya paylaşımı erişimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="6d5f2-230">Hello bağlantısı başlatıldığında hello VPN istemcisi hello oturum bilgilerini ekler ve hello hatası oluşur.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="6d5f2-231">Merhaba bağlantı kurulduktan sonra hello istemci toouse hello kimlik bilgilerini önbelleğe Kerberos kimlik doğrulaması zorlanır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="6d5f2-232">Bu işlem sorguları toohello Anahtar Dağıtım Merkezi (bir etki alanı denetleyicisi) tooget bir belirteç başlatır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="6d5f2-233">Merhaba istemci Internet hello bağlandığından, mümkün tooreach hello etki alanı denetleyicisi olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="6d5f2-234">Bu nedenle, hello istemci üzerinden Kerberos tooNTLM kapatamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="6d5f2-235">Merhaba hello istemci için geçerli bir sertifika sahip olduğunda bir kimlik bilgisi sorulup yalnızca zaman (SAN ile UPN =) birleştirilmiş hello etki alanı toowhich tarafından verilmiş.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="6d5f2-236">Merhaba istemci ayrıca fiziksel olarak bağlı toohello etki alanı ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="6d5f2-237">Bu durumda, hello istemci toouse hello sertifika dener ve toohello etki alanı denetleyicisi ulaşır.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="6d5f2-238">Ardından hello anahtar dağıtım merkezi bir "KDC_ERR_C_PRINCIPAL_UNKNOWN" hatası döndürür.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="6d5f2-239">Merhaba zorlanmış toofail tooNTLM istemcidir.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="6d5f2-240">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-240">Solution</span></span>

<span data-ttu-id="6d5f2-241">toowork hello soruna geçici bir çözüm hello hello kayıt defteri alt anahtarını aşağıdaki etki alanı kimlik bilgilerini önbelleğe almayı devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="6d5f2-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="6d5f2-242">Merhaba VPN istemcisi yeniden yükledikten sonra Windows Hello noktadan siteye VPN bağlantısı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="6d5f2-243">Belirti</span><span class="sxs-lookup"><span data-stu-id="6d5f2-243">Symptom</span></span>

<span data-ttu-id="6d5f2-244">Merhaba noktadan siteye VPN bağlantısını kaldırın ve hello VPN istemcisini yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="6d5f2-245">Bu durumda, hello VPN bağlantısı başarıyla yapılandırılmadı.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="6d5f2-246">Merhaba hello VPN bağlantısının görüyor musunuz **ağ bağlantıları** Windows ayarları.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="6d5f2-247">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6d5f2-247">Solution</span></span>

<span data-ttu-id="6d5f2-248">tooresolve hello sorunu delete hello eski VPN istemci yapılandırma dosyalarından **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, ve hello VPN istemci yükleyiciyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6d5f2-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
