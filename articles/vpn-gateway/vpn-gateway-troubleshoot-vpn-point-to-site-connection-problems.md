---
title: "Azure noktadan siteye bağlantı sorunlarını giderme | Microsoft Docs"
description: "Noktadan siteye bağlantı sorunlarını giderme öğrenin."
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
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="aed4d-103">Giderme: Azure noktadan siteye bağlantı sorunlarını</span><span class="sxs-lookup"><span data-stu-id="aed4d-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="aed4d-104">Bu makalede karşılaşabileceğiniz genel noktadan siteye bağlantı sorunları listeler.</span><span class="sxs-lookup"><span data-stu-id="aed4d-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="aed4d-105">Ayrıca bu sorunlar için olası nedenler ve çözümler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="aed4d-106">VPN istemci hatası: bir sertifika bulunamadı</span><span class="sxs-lookup"><span data-stu-id="aed4d-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-107">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-107">Symptom</span></span>

<span data-ttu-id="aed4d-108">VPN istemcisi kullanarak bir Azure sanal ağa bağlanmaya çalıştığında aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="aed4d-109">**Bu Genişletilebilir kimlik doğrulama protokolü ile kullanılabilir bir sertifika bulunamadı. (Hata 798)**</span><span class="sxs-lookup"><span data-stu-id="aed4d-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-110">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-110">Cause</span></span>

<span data-ttu-id="aed4d-111">İstemci sertifikası eksik Bu sorun oluşur **Sertifikalar - Geçerli User\Personal\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="aed4d-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-112">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-112">Solution</span></span>

<span data-ttu-id="aed4d-113">İstemci sertifikası sertifika deposu (Certmgr.msc) aşağıdaki konumda yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="aed4d-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="aed4d-114">**Sertifikalar - Geçerli User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="aed4d-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="aed4d-115">İstemci sertifikası yükleme hakkında daha fazla bilgi için bkz: [noktadan siteye bağlantıları için oluşturma ve verme sertifikaları](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="aed4d-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aed4d-116">İstemci sertifikasını içeri aktardığınızda seçmeyin **güçlü özel anahtar korumasını etkinleştir** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="aed4d-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="aed4d-117">VPN istemci hatası: beklenmeyen veya hatalı biçimlendirilmiş bir ileti alındı</span><span class="sxs-lookup"><span data-stu-id="aed4d-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-118">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-118">Symptom</span></span>

<span data-ttu-id="aed4d-119">VPN istemcisi kullanarak bir Azure sanal ağa bağlanmaya çalıştığında aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="aed4d-120">**Alınan ileti beklenmeyen veya hatalı biçimlendirilmiş. (Hata 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="aed4d-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-121">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-121">Cause</span></span>

<span data-ttu-id="aed4d-122">Kök sertifika genel anahtarı Azure VPN ağ geçidine yüklenmemiştir Bu sorun oluşur.</span><span class="sxs-lookup"><span data-stu-id="aed4d-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="aed4d-123">Anahtar bozulmuş ya da süresi dolmuş da oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-124">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-124">Solution</span></span>

<span data-ttu-id="aed4d-125">Bu sorunu gidermek için kök sertifikası iptal edilmiş olup olmadığını görmek için Azure portalında durumunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="aed4d-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="aed4d-126">Bunu iptal edilmediğini, kök sertifikasını ve reupload silmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="aed4d-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="aed4d-127">Daha fazla bilgi için bkz: [oluşturma sertifikaları](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="aed4d-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="aed4d-128">VPN istemci hatası: bir sertifika zinciri işlendi, ancak sona erdi</span><span class="sxs-lookup"><span data-stu-id="aed4d-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="aed4d-129">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-129">Symptom</span></span> 

<span data-ttu-id="aed4d-130">VPN istemcisi kullanarak bir Azure sanal ağa bağlanmaya çalıştığında aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="aed4d-131">**Bir sertifika zinciri işlendi, ancak güven sağlayıcısı tarafından güvenilmeyen bir kök sertifika sona erdi.**</span><span class="sxs-lookup"><span data-stu-id="aed4d-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-132">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-132">Solution</span></span>

1. <span data-ttu-id="aed4d-133">Aşağıdaki sertifikalar ve doğru konumda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="aed4d-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="aed4d-134">Sertifika</span><span class="sxs-lookup"><span data-stu-id="aed4d-134">Certificate</span></span> | <span data-ttu-id="aed4d-135">Konum</span><span class="sxs-lookup"><span data-stu-id="aed4d-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="aed4d-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="aed4d-136">AzureClient.pfx</span></span>  | <span data-ttu-id="aed4d-137">Geçerli User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="aed4d-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="aed4d-138">Azuregateway -*GUID*. cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="aed4d-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="aed4d-139">Geçerli User\Trusted kök sertifika yetkilileri</span><span class="sxs-lookup"><span data-stu-id="aed4d-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="aed4d-140">AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="aed4d-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="aed4d-141">Yerel bilgisayar/güvenilen kök sertifika yetkilileri</span><span class="sxs-lookup"><span data-stu-id="aed4d-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="aed4d-142">Sertifikaları konumu zaten varsa, sertifikaları silin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="aed4d-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="aed4d-143"> **Azuregateway -*GUID*. Azure portalından indirdiğiniz VPN istemcisi yapılandırma paketini cloudapp.net** sertifika konusu.</span><span class="sxs-lookup"><span data-stu-id="aed4d-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="aed4d-144">Dosya archivers paketinden dosyaları ayıklayın için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed4d-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="aed4d-145">Dosya indirme hatası: hedef URI belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="aed4d-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-146">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-146">Symptom</span></span>

<span data-ttu-id="aed4d-147">Aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-147">You receive the following error message:</span></span>

<span data-ttu-id="aed4d-148">**Dosya indirme hatası. Hedef URI belirtilmedi.**</span><span class="sxs-lookup"><span data-stu-id="aed4d-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-149">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-149">Cause</span></span> 

<span data-ttu-id="aed4d-150">Bu sorun bir hatalı ağ geçidi türü nedeniyle oluşur.</span><span class="sxs-lookup"><span data-stu-id="aed4d-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="aed4d-151">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-151">Solution</span></span>

<span data-ttu-id="aed4d-152">VPN ağ geçidi türü olmalıdır **VPN**, ve VPN türü olmalıdır **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="aed4d-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="aed4d-153">VPN istemci hatası: Azure VPN özel komut başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="aed4d-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="aed4d-154">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-154">Symptom</span></span>

<span data-ttu-id="aed4d-155">VPN istemcisi kullanarak bir Azure sanal ağa bağlanmaya çalıştığında aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="aed4d-156">**(Yönlendirme tablonuzu güncelleştirmek için) özel bir komut dosyası başarısız oldu. (Hata 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="aed4d-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-157">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-157">Cause</span></span>

<span data-ttu-id="aed4d-158">Kısayol kullanarak site noktası VPN bağlantısı açmaya çalıştığınız, bu sorun ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-159">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-159">Solution</span></span> 

<span data-ttu-id="aed4d-160">Kısayoldan açmadan yerine doğrudan VPN paketini açın.</span><span class="sxs-lookup"><span data-stu-id="aed4d-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="aed4d-161">VPN istemci yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="aed4d-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-162">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-162">Cause</span></span> 

<span data-ttu-id="aed4d-163">Ek bir sertifika, VPN ağ geçidi sanal ağınız için güvenmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="aed4d-164">Sertifika Azure portalından oluşturulan VPN istemcisi yapılandırma paketini dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-165">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-165">Solution</span></span>

<span data-ttu-id="aed4d-166">VPN istemcisi yapılandırma paketini ayıklamak ve .cer dosyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="aed4d-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="aed4d-167">Sertifikayı yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="aed4d-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="aed4d-168">MMC.exe açın.</span><span class="sxs-lookup"><span data-stu-id="aed4d-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="aed4d-169">Ekleme **sertifikaları** ek bileşenini.</span><span class="sxs-lookup"><span data-stu-id="aed4d-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="aed4d-170">Seçin **bilgisayar** yerel bilgisayar hesabı.</span><span class="sxs-lookup"><span data-stu-id="aed4d-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="aed4d-171">Sağ **güvenilen kök sertifika yetkilileri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="aed4d-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="aed4d-172">Tıklatın **tüm görev** > **alma**ve VPN istemci yapılandırma paketi ayıkladığınız .cer dosyasının konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="aed4d-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="aed4d-173">Bilgisayarı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="aed4d-173">Restart the computer.</span></span> 
6. <span data-ttu-id="aed4d-174">VPN istemcisi yüklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="aed4d-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="aed4d-175">Azure portal hata: VPN ağ geçidi kaydedemedi ve veri geçersiz</span><span class="sxs-lookup"><span data-stu-id="aed4d-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-176">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-176">Symptom</span></span>

<span data-ttu-id="aed4d-177">Azure portalında VPN ağ geçidi değişiklikleri kaydetmeyi denediğinizde aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="aed4d-178">**Sanal ağ geçidi kaydedilemedi &lt;* ağ geçidi adı*&gt;.</span><span class="sxs-lookup"><span data-stu-id="aed4d-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="aed4d-179">Sertifikasının verileri &lt; *kimliği sertifika* &gt; olan invalid.* *</span><span class="sxs-lookup"><span data-stu-id="aed4d-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-180">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-180">Cause</span></span> 

<span data-ttu-id="aed4d-181">Karşıya yüklediğiniz kök sertifikanın ortak anahtarı bir alanı gibi geçersiz bir karakter içeriyorsa, bu sorun ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-182">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-182">Solution</span></span>

<span data-ttu-id="aed4d-183">Sertifika verileri satır sonları (satır başı) gibi geçersiz karakterler içermediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="aed4d-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="aed4d-184">Değerin tamamını uzun bir satır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-184">The entire value should be one long line.</span></span> <span data-ttu-id="aed4d-185">Aşağıdaki metni, sertifikanın bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="aed4d-185">The following text is a sample of the certificate:</span></span>

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

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="aed4d-186">Azure portal hata: VPN ağ geçidi kaydedilemedi ve kaynak adı geçersiz</span><span class="sxs-lookup"><span data-stu-id="aed4d-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-187">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-187">Symptom</span></span>

<span data-ttu-id="aed4d-188">Azure portalında VPN ağ geçidi değişiklikleri kaydetmeyi denediğinizde aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="aed4d-189">**Sanal ağ geçidi kaydedilemedi &lt;* ağ geçidi adı*&gt;.</span><span class="sxs-lookup"><span data-stu-id="aed4d-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="aed4d-190">Kaynak adı &lt; *deneyin karşıya yüklemek için sertifika adı* &gt; geçersiz ** değil.</span><span class="sxs-lookup"><span data-stu-id="aed4d-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-191">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-191">Cause</span></span>

<span data-ttu-id="aed4d-192">Sertifika adı bir boşluk gibi geçersiz bir karakter içerdiğinden bu sorun oluşur.</span><span class="sxs-lookup"><span data-stu-id="aed4d-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="aed4d-193">Azure portal hata: VPN paket dosyasını indirme hatası 503</span><span class="sxs-lookup"><span data-stu-id="aed4d-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-194">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-194">Symptom</span></span>

<span data-ttu-id="aed4d-195">VPN istemcisi yapılandırma paketini yüklemeye çalışırken aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="aed4d-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="aed4d-196">**Dosyası karşıdan yüklenemedi. Hata ayrıntıları: 503 hatası. Sunucu meşgul.**</span><span class="sxs-lookup"><span data-stu-id="aed4d-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="aed4d-197">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-197">Solution</span></span>

<span data-ttu-id="aed4d-198">Bu hata geçici bir ağ sorunu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="aed4d-199">VPN paketini indir birkaç dakika sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="aed4d-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="aed4d-200">Azure VPN ağ geçidi yükseltme: tüm P2S istemcileridir bağlanamıyor</span><span class="sxs-lookup"><span data-stu-id="aed4d-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-201">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-201">Cause</span></span>

<span data-ttu-id="aed4d-202">Sertifika yüzde 50'den fazla ise yaşam sertifika alındı.</span><span class="sxs-lookup"><span data-stu-id="aed4d-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-203">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-203">Solution</span></span>

<span data-ttu-id="aed4d-204">Bu sorunu gidermek için oluşturun ve yeni sertifikalar VPN istemcileri için yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="aed4d-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="aed4d-205">Çok fazla VPN istemcileri aynı anda bağlı</span><span class="sxs-lookup"><span data-stu-id="aed4d-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="aed4d-206">Her VPN ağ geçidi için en fazla izin verilen bağlantı sayısı 128'dir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="aed4d-207">Azure portalında bağlanan istemcilerin toplam sayısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aed4d-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="aed4d-208">Noktadan siteye VPN, 10.0.0.0/8 için bir yol yanlış yol tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="aed4d-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-209">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-209">Symptom</span></span>

<span data-ttu-id="aed4d-210">Noktadan siteye istemci VPN bağlantısında çevirdiğinizde, VPN istemcisi Azure sanal ağı doğru bir yol eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="aed4d-211">IP yardımcı hizmeti, VPN istemcileri alt ağ için bir yol eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="aed4d-212">VPN istemci aralığı 10.0.12.0/24 gibi 10.0.0.0/8, daha küçük bir alt ağa ait.</span><span class="sxs-lookup"><span data-stu-id="aed4d-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="aed4d-213">10.0.12.0/24 için bir yol yerine, daha yüksek önceliğe sahip 10.0.0.0/8 için bir rota eklenir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="aed4d-214">Bu yanlış yol tanımlanan belirli bir yolu olmayan bu 10.0.0.0/8 aralıkta 10.50.0.0/24 gibi başka bir alt ağa ait olabilir diğer şirket içi ağlar ile bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="aed4d-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="aed4d-215">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-215">Cause</span></span>

<span data-ttu-id="aed4d-216">Bu davranış, Windows istemcileri için tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="aed4d-217">İstemci PPP IPCP protokol kullandığında, tünel arabirimi için IP adresi (Bu durumda VPN gateway) sunucusundan alır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="aed4d-218">Ancak, protokolünde bir sınırlama nedeniyle, istemci alt ağ maskesi yok.</span><span class="sxs-lookup"><span data-stu-id="aed4d-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="aed4d-219">Edinilir başka hiçbir yolu olduğundan, istemci tünel arabirimi IP adresi sınıfına göre alt ağ maskesi tahmin etmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="aed4d-220">Bu nedenle, bir yol aşağıdaki statik eşleme göre eklenir:</span><span class="sxs-lookup"><span data-stu-id="aed4d-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="aed4d-221">Adres sınıf A aitse--> /8 Uygula</span><span class="sxs-lookup"><span data-stu-id="aed4d-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="aed4d-222">Adres B--> sınıfına aitse /16 Uygula</span><span class="sxs-lookup"><span data-stu-id="aed4d-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="aed4d-223">Adres C--> sınıfına aitse /24 Uygula</span><span class="sxs-lookup"><span data-stu-id="aed4d-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="aed4d-224">VPN istemcisi ağ dosya paylaşımlarına erişemez</span><span class="sxs-lookup"><span data-stu-id="aed4d-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-225">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-225">Symptom</span></span>

<span data-ttu-id="aed4d-226">Azure sanal ağı için VPN istemcisi bağlandı.</span><span class="sxs-lookup"><span data-stu-id="aed4d-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="aed4d-227">Ancak, istemci ağ paylaşımlarına erişemez.</span><span class="sxs-lookup"><span data-stu-id="aed4d-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="aed4d-228">Nedeni</span><span class="sxs-lookup"><span data-stu-id="aed4d-228">Cause</span></span>

<span data-ttu-id="aed4d-229">SMB protokolü dosya paylaşımı erişimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="aed4d-230">Bağlantısı başlatıldığında VPN istemcisi oturum bilgilerini ekler ve hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="aed4d-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="aed4d-231">Bağlantı kurulduktan sonra istemci kimlik bilgilerini önbelleğe için Kerberos kimlik doğrulamasını kullanmak için zorlanır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="aed4d-232">Bu işlem merkezi bir belirteç almak üzere anahtar dağıtım (bir etki alanı denetleyicisi) sorguları başlatır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="aed4d-233">İstemci Internet'ten bağlandığından, etki alanı denetleyicisi ulaşabilmesi olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="aed4d-234">Bu nedenle, istemci üzerinde Kerberos'tan NTLM olarak çalışamaz.</span><span class="sxs-lookup"><span data-stu-id="aed4d-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="aed4d-235">Olduğunda bir kimlik bilgisi için istemci istenir yalnızca bir kez geçerli bir sertifika sahiptir (SAN ile UPN =) katılan etki alanı tarafından verilmiş.</span><span class="sxs-lookup"><span data-stu-id="aed4d-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="aed4d-236">İstemci ayrıca fiziksel etki alanı ağına bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aed4d-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="aed4d-237">Bu durumda, istemci sertifikasını kullanmayı dener ve etki alanı denetleyicisine ulaştığında.</span><span class="sxs-lookup"><span data-stu-id="aed4d-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="aed4d-238">Daha sonra anahtar dağıtım merkezi bir "KDC_ERR_C_PRINCIPAL_UNKNOWN" hatası döndürür.</span><span class="sxs-lookup"><span data-stu-id="aed4d-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="aed4d-239">İstemci için NTLM üzerinden vermesine zorlanır.</span><span class="sxs-lookup"><span data-stu-id="aed4d-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="aed4d-240">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-240">Solution</span></span>

<span data-ttu-id="aed4d-241">Sorunu çözmek için aşağıdaki kayıt defteri alt etki alanı kimlik bilgilerini önbelleğe alma devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="aed4d-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="aed4d-242">Noktadan siteye VPN bağlantısı VPN istemcisi yeniden yükledikten sonra Windows bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="aed4d-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="aed4d-243">Belirti</span><span class="sxs-lookup"><span data-stu-id="aed4d-243">Symptom</span></span>

<span data-ttu-id="aed4d-244">Noktadan siteye VPN bağlantısını kaldırın ve VPN istemcisi yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aed4d-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="aed4d-245">Bu durumda, VPN bağlantısı başarıyla yapılandırılmadı.</span><span class="sxs-lookup"><span data-stu-id="aed4d-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="aed4d-246">VPN bağlantısı görüyor musunuz **ağ bağlantıları** Windows ayarları.</span><span class="sxs-lookup"><span data-stu-id="aed4d-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="aed4d-247">Çözüm</span><span class="sxs-lookup"><span data-stu-id="aed4d-247">Solution</span></span>

<span data-ttu-id="aed4d-248">Sorunu gidermek için eski VPN istemci yapılandırma dosyalarını silin **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, ve ardından VPN istemcisi yükleyicisini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aed4d-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
