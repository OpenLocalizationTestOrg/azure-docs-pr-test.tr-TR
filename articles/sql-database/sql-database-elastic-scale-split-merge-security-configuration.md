---
title: "aaaSplit birleştirme güvenlik yapılandırması | Microsoft Docs"
description: "X409 ayarlamak şifreleme için sertifikalar"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="beaaa-103">Bölünmüş birleştirme güvenlik yapılandırması</span><span class="sxs-lookup"><span data-stu-id="beaaa-103">Split-merge security configuration</span></span>
<span data-ttu-id="beaaa-104">toouse hello bölünmüş/Merge hizmeti, güvenlik doğru şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="beaaa-105">Merhaba hizmet hello esnek ölçek özelliği Microsoft Azure SQL veritabanı'nın bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="beaaa-106">Daha fazla bilgi için bkz: [esnek ölçek bölme ve birleştirme hizmet öğretici](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="beaaa-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="beaaa-107">Sertifikaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-107">Configuring certificates</span></span>
<span data-ttu-id="beaaa-108">Sertifikalar iki şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="beaaa-109">tooConfigure hello SSL sertifikası</span><span class="sxs-lookup"><span data-stu-id="beaaa-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="beaaa-110">tooConfigure istemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="beaaa-111">tooobtain sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-111">tooobtain certificates</span></span>
<span data-ttu-id="beaaa-112">Ortak sertifika yetkilileri (CA) ya da hello sertifikaları elde edilebilir [Windows sertifika hizmeti](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="beaaa-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="beaaa-113">Bu tercih edilen hello yöntemleri tooobtain sertifikalardır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="beaaa-114">Bu seçenek mevcut değilse, oluşturabileceğiniz **otomatik olarak imzalanan sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="beaaa-115">Araçlar toogenerate sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="beaaa-116">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="beaaa-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="beaaa-117">Pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="beaaa-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="beaaa-118">toorun hello araçları</span><span class="sxs-lookup"><span data-stu-id="beaaa-118">toorun hello tools</span></span>
* <span data-ttu-id="beaaa-119">Bir geliştirici komut isteminden Visual stüdyoları için bkz: [Visual Studio komut istemi](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="beaaa-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="beaaa-120">Yüklü değilse, aşağıdaki adrese gidin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="beaaa-121">Alma gelen WDK hello [Windows 8.1: indirme setleri ve araçları](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="beaaa-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="beaaa-122">tooconfigure hello SSL sertifikası</span><span class="sxs-lookup"><span data-stu-id="beaaa-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="beaaa-123">Bir SSL sertifikası gerekli tooencrypt hello iletişim ve hello sunucusuna kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="beaaa-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="beaaa-124">Merhaba hello üç senaryoları aşağıdaki en uygun seçin ve tüm adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="beaaa-125">Yeni bir otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="beaaa-126">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="beaaa-127">PFX dosyası için otomatik olarak imzalanan SSL sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="beaaa-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="beaaa-128">SSL sertifikası tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="beaaa-129">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="beaaa-130">SSL sertifika yetkilisi alma</span><span class="sxs-lookup"><span data-stu-id="beaaa-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="beaaa-131">var olan bir sertifikayı hello sertifikasından toouse depolama</span><span class="sxs-lookup"><span data-stu-id="beaaa-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="beaaa-132">SSL sertifikası, sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="beaaa-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="beaaa-133">SSL sertifikası tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="beaaa-134">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="beaaa-135">var olan bir sertifikayı bir PFX dosyasına toouse</span><span class="sxs-lookup"><span data-stu-id="beaaa-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="beaaa-136">SSL sertifikası tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="beaaa-137">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="beaaa-138">tooconfigure istemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-138">tooconfigure client certificates</span></span>
<span data-ttu-id="beaaa-139">İstemci sertifikaları, sipariş tooauthenticate istekleri toohello hizmetinde gereklidir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="beaaa-140">Merhaba hello üç senaryoları aşağıdaki en uygun seçin ve tüm adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="beaaa-141">İstemci sertifikaları devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="beaaa-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="beaaa-142">İstemci sertifikası tabanlı kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="beaaa-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="beaaa-143">Yeni otomatik olarak imzalanan istemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="beaaa-144">Bir otomatik olarak imzalanan sertifika yetkilisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="beaaa-145">CA sertifikasını tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="beaaa-146">Hizmet yapılandırma dosyasında CA sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="beaaa-147">İstemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="beaaa-148">PFX dosyaları için istemci sertifikaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="beaaa-149">İstemci sertifikası Al</span><span class="sxs-lookup"><span data-stu-id="beaaa-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="beaaa-150">İstemci sertifikası parmak kopyalayın</span><span class="sxs-lookup"><span data-stu-id="beaaa-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="beaaa-151">Merhaba hizmet yapılandırma dosyası izin verilen istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="beaaa-152">Mevcut istemci sertifikalarını kullanın</span><span class="sxs-lookup"><span data-stu-id="beaaa-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="beaaa-153">CA ortak anahtarı bulma</span><span class="sxs-lookup"><span data-stu-id="beaaa-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="beaaa-154">CA sertifikasını tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="beaaa-155">Hizmet yapılandırma dosyasında CA sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="beaaa-156">İstemci sertifikası parmak kopyalayın</span><span class="sxs-lookup"><span data-stu-id="beaaa-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="beaaa-157">Merhaba hizmet yapılandırma dosyası izin verilen istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="beaaa-158">İstemci sertifikası iptal denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="beaaa-159">İzin verilen IP adresi</span><span class="sxs-lookup"><span data-stu-id="beaaa-159">Allowed IP addresses</span></span>
<span data-ttu-id="beaaa-160">Erişim toohello hizmet uç noktaları kısıtlı toospecific aralıkları IP adresleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="beaaa-161">Merhaba deposu için tooconfigure şifreleme</span><span class="sxs-lookup"><span data-stu-id="beaaa-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="beaaa-162">Bir sertifika hello meta veri deposunda saklanır gerekli tooencrypt hello kimlik bilgileri yok.</span><span class="sxs-lookup"><span data-stu-id="beaaa-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="beaaa-163">Merhaba hello üç senaryoları aşağıdaki en uygun seçin ve tüm adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="beaaa-164">Yeni bir otomatik olarak imzalanan sertifika kullan</span><span class="sxs-lookup"><span data-stu-id="beaaa-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="beaaa-165">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="beaaa-166">PFX dosyası için otomatik olarak imzalanan şifreleme sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="beaaa-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="beaaa-167">Şifreleme sertifikası tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="beaaa-168">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="beaaa-169">Varolan bir sertifikayı hello sertifika deposundan kullanın</span><span class="sxs-lookup"><span data-stu-id="beaaa-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="beaaa-170">Şifreleme sertifikası sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="beaaa-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="beaaa-171">Şifreleme sertifikası tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="beaaa-172">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="beaaa-173">Varolan bir sertifikayı bir PFX dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="beaaa-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="beaaa-174">Şifreleme sertifikası tooCloud hizmet karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="beaaa-175">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="beaaa-176">Merhaba varsayılan yapılandırması</span><span class="sxs-lookup"><span data-stu-id="beaaa-176">hello default configuration</span></span>
<span data-ttu-id="beaaa-177">Merhaba varsayılan yapılandırması erişim toohello tüm HTTP uç noktası reddeder.</span><span class="sxs-lookup"><span data-stu-id="beaaa-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="beaaa-178">Merhaba istekleri toothese uç noktaları veritabanı kimlik bilgileri gibi hassas bilgileri taşımak beri Önerilen ayar, hello budur.</span><span class="sxs-lookup"><span data-stu-id="beaaa-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="beaaa-179">Merhaba varsayılan yapılandırması erişim toohello tüm HTTPS uç noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="beaaa-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="beaaa-180">Bu ayar daha fazla kısıtlanabilir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="beaaa-181">Merhaba yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="beaaa-181">Changing hello Configuration</span></span>
<span data-ttu-id="beaaa-182">Merhaba tooand uç nokta geçerli erişim denetim kurallarını grubunun yapılandırılmış olan hello  **<EndpointAcls>**  hello bölümünde **hizmet yapılandırma dosyası**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="beaaa-183">bir erişim denetimi grubu Hello kurallarında yapılandırılmış bir <AccessControl name=""> hello hizmet yapılandırma dosyasının.</span><span class="sxs-lookup"><span data-stu-id="beaaa-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="beaaa-184">Merhaba biçimi ağ erişim denetimi listelerini belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="beaaa-185">Örneğin, tooallow yalnızca IP'leri hello aralığı 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS uç noktada hello kuralları şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="beaaa-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="beaaa-186">Hizmet önleme reddi</span><span class="sxs-lookup"><span data-stu-id="beaaa-186">Denial of service prevention</span></span>
<span data-ttu-id="beaaa-187">İki farklı mekanizmaları toodetect desteklenen ve hizmet reddi saldırılarını vardır:</span><span class="sxs-lookup"><span data-stu-id="beaaa-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="beaaa-188">Uzak ana bilgisayar başına eşzamanlı istek sayısını kısıtlayın (varsayılan olarak kapalıdır)</span><span class="sxs-lookup"><span data-stu-id="beaaa-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="beaaa-189">Uzak ana bilgisayar başına erişimi oranını kısıtlamak (üzerinde varsayılan olarak)</span><span class="sxs-lookup"><span data-stu-id="beaaa-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="beaaa-190">Bunlar daha fazla dinamik IP Güvenlik IIS'de açıklandığı hello özellikleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="beaaa-191">Ne zaman bu yapılandırmasını değiştirme Etkenler aşağıdaki Merhaba dikkat:</span><span class="sxs-lookup"><span data-stu-id="beaaa-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="beaaa-192">Proxy ve ağ adresi çevirisi cihazların Merhaba uzak ana bilgisayar bilgilerini üzerinden Hello davranışı</span><span class="sxs-lookup"><span data-stu-id="beaaa-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="beaaa-193">Her istek tooany kaynak hello web rolü (örn. yükleme komut dosyaları, görüntüler, vb.) olarak kabul edilir</span><span class="sxs-lookup"><span data-stu-id="beaaa-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="beaaa-194">Eşzamanlı erişimi sayısını sınırlandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="beaaa-195">Bu davranışı yapılandırmak hello ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="beaaa-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="beaaa-196">Bu koruma DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable değiştirin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="beaaa-197">Erişim kısıtlama oranı</span><span class="sxs-lookup"><span data-stu-id="beaaa-197">Restricting rate of access</span></span>
<span data-ttu-id="beaaa-198">Bu davranışı yapılandırmak hello ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="beaaa-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="beaaa-199">Merhaba yanıt tooa yapılandırma isteğini reddetti</span><span class="sxs-lookup"><span data-stu-id="beaaa-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="beaaa-200">Merhaba aşağıdaki ayar isteğini reddetti hello yanıt tooa yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="beaaa-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="beaaa-201">Desteklenen diğer değerler için IIS içinde dinamik IP Güvenlik toohello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="beaaa-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="beaaa-202">Hizmet sertifikaları yapılandırma işlemleri</span><span class="sxs-lookup"><span data-stu-id="beaaa-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="beaaa-203">Bu konu yalnızca başvuru amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-203">This topic is for reference only.</span></span> <span data-ttu-id="beaaa-204">Lütfen özetlenen hello yapılandırma adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="beaaa-205">Merhaba SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="beaaa-206">İstemci sertifikaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="beaaa-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="beaaa-207">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-207">Create a self-signed certificate</span></span>
<span data-ttu-id="beaaa-208">Yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="beaaa-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="beaaa-209">toocustomize:</span></span>

* <span data-ttu-id="beaaa-210">-n hello ile hizmet URL'si.</span><span class="sxs-lookup"><span data-stu-id="beaaa-210">-n with hello service URL.</span></span> <span data-ttu-id="beaaa-211">Joker karakterler ("CN = * .cloudapp .net") ve diğer adları ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") desteklenir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="beaaa-212">-e hello sertifika sona erme tarihi ile güçlü bir parola oluşturmak ve istendiğinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="beaaa-213">Otomatik olarak imzalanan SSL Sertifika PFX dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="beaaa-214">Yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="beaaa-215">Bir parola girin ve sonra bu seçenekler ile sertifika verme:</span><span class="sxs-lookup"><span data-stu-id="beaaa-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="beaaa-216">Evet, hello özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-216">Yes, export hello private key</span></span>
* <span data-ttu-id="beaaa-217">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="beaaa-218">SSL sertifikası, sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="beaaa-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="beaaa-219">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="beaaa-219">Find certificate</span></span>
* <span data-ttu-id="beaaa-220">Tıklatın Eylemler -> tüm görevleri Export ->...</span><span class="sxs-lookup"><span data-stu-id="beaaa-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="beaaa-221">İçinde sertifika verme bir. Bu seçenekler PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="beaaa-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="beaaa-222">Evet, hello özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="beaaa-223">Mümkünse hello sertifika yolundaki tüm sertifikaları dahil et * tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="beaaa-224">SSL sertifika toocloud hizmeti karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="beaaa-225">Karşıya yükleme hello var olan sertifika veya oluşturulabilir. Merhaba SSL anahtar çifti PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="beaaa-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="beaaa-226">Merhaba özel anahtar bilgisi koruma hello parolayı girin</span><span class="sxs-lookup"><span data-stu-id="beaaa-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="beaaa-227">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="beaaa-228">Merhaba parmak izi hello karşıya sertifika toohello bulut hizmeti ile Merhaba hizmet yapılandırma dosyası ayarında aşağıdaki hello Hello parmak izi değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="beaaa-229">SSL sertifika yetkilisi alma</span><span class="sxs-lookup"><span data-stu-id="beaaa-229">Import SSL certification authority</span></span>
<span data-ttu-id="beaaa-230">Tüm hesap/hello hizmeti ile iletişim kuracak makinesinde aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="beaaa-231">Merhaba çift tıklayın. Windows Gezgini'nde CER dosyasını</span><span class="sxs-lookup"><span data-stu-id="beaaa-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="beaaa-232">Merhaba sertifikası iletişim kutusunda, sertifikayı yükle düğmesine...</span><span class="sxs-lookup"><span data-stu-id="beaaa-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="beaaa-233">Sertifikayı güvenilir kök sertifika yetkilileri deposuna hello alın</span><span class="sxs-lookup"><span data-stu-id="beaaa-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="beaaa-234">İstemci sertifikası tabanlı kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="beaaa-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="beaaa-235">Yalnızca istemci sertifika tabanlı kimlik doğrulaması desteklenmez ve diğer mekanizmaları (örneğin Microsoft Azure sanal ağı) yerinde olmadığı sürece, devre dışı bırakmasını genel erişim toohello hizmeti için uç noktaları, izin verir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="beaaa-236">Bu ayarları toofalse hello hizmet yapılandırma dosyası tooturn hello özelliğindeki değişiklik devre dışı:</span><span class="sxs-lookup"><span data-stu-id="beaaa-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="beaaa-237">Ardından, aynı parmak izine hello SSL sertifika hello hello CA sertifikası ayarında kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="beaaa-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="beaaa-238">Bir otomatik olarak imzalanan sertifika yetkilisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="beaaa-239">Aşağıdaki adımları toocreate bir sertifika yetkilisi olarak otomatik olarak imzalanan sertifika tooact hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="beaaa-240">toocustomize,</span><span class="sxs-lookup"><span data-stu-id="beaaa-240">toocustomize it</span></span>

* <span data-ttu-id="beaaa-241">-e hello sertifika sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="beaaa-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="beaaa-242">CA ortak anahtarı bulma</span><span class="sxs-lookup"><span data-stu-id="beaaa-242">Find CA public key</span></span>
<span data-ttu-id="beaaa-243">İstemci sertifikalarının tümünü hello hizmeti tarafından güvenilen bir sertifika yetkilisi tarafından verilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="beaaa-244">Merhaba ortak anahtar toohello toobe giderek hello istemci sertifikaları veren sertifika yetkilisi kimlik doğrulaması için sipariş tooupload ile toohello bulut hizmeti kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="beaaa-245">Merhaba dosya hello ortak anahtarla kullanılabilir durumda değilse, hello sertifika deposundan dışarı aktarın:</span><span class="sxs-lookup"><span data-stu-id="beaaa-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="beaaa-246">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="beaaa-246">Find certificate</span></span>
  * <span data-ttu-id="beaaa-247">Merhaba aynı sertifika yetkilisi tarafından verilen bir istemci sertifikası arayın</span><span class="sxs-lookup"><span data-stu-id="beaaa-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="beaaa-248">Merhaba sertifikayı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="beaaa-249">Merhaba sertifikası iletişim kutusunda Hello sertifika yolu sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="beaaa-250">Merhaba CA hello yolu girişi çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="beaaa-251">Hello sertifika özellikleri not alın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="beaaa-252">Kapat hello **sertifika** iletişim.</span><span class="sxs-lookup"><span data-stu-id="beaaa-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="beaaa-253">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="beaaa-253">Find certificate</span></span>
  * <span data-ttu-id="beaaa-254">Merhaba yukarıda belirtilen CA'yı arayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="beaaa-255">Tıklatın Eylemler -> tüm görevleri Export ->...</span><span class="sxs-lookup"><span data-stu-id="beaaa-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="beaaa-256">İçinde sertifika verme bir. CER bu seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="beaaa-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="beaaa-257">**Hayır, hello özel anahtarı verme**</span><span class="sxs-lookup"><span data-stu-id="beaaa-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="beaaa-258">Tüm sertifikaları hello sertifika yolunda mümkünse içerir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="beaaa-259">Tüm genişletilmiş özellikleri dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="beaaa-260">CA sertifika toocloud hizmeti karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="beaaa-261">Karşıya yükleme hello var olan sertifika veya oluşturulabilir. CER dosyasını hello CA ortak anahtara sahip.</span><span class="sxs-lookup"><span data-stu-id="beaaa-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="beaaa-262">Hizmet yapılandırma dosyasında güncelleştirme CA sertifikası</span><span class="sxs-lookup"><span data-stu-id="beaaa-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="beaaa-263">Merhaba parmak izi hello karşıya sertifika toohello bulut hizmeti ile Merhaba hizmet yapılandırma dosyası ayarında aşağıdaki hello Hello parmak izi değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="beaaa-264">Merhaba ile aynı ayarı aşağıdaki hello Hello değerini güncelleştirmek parmak izi:</span><span class="sxs-lookup"><span data-stu-id="beaaa-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="beaaa-265">İstemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="beaaa-265">Issue client certificates</span></span>
<span data-ttu-id="beaaa-266">Her bireysel yetkili tooaccess hello hizmeti kullanmak özel his/hers için yayımlanan bir istemci sertifikasına sahip olmalıdır ve özel anahtarını his/hers güçlü parola tooprotect kendi seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="beaaa-267">Aşağıdaki adımları hello burada hello CA sertifikası otomatik olarak imzalanan aynı makine oluşturulan ve depolanan hello yürütülmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="beaaa-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="beaaa-268">Özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="beaaa-268">Customizing:</span></span>

* <span data-ttu-id="beaaa-269">-n Bu sertifika ile kimlik doğrulaması yapılacak toohello istemci için bir kimliği</span><span class="sxs-lookup"><span data-stu-id="beaaa-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="beaaa-270">-e hello sertifika sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="beaaa-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="beaaa-271">MyID.pvk ve bu istemci sertifikası için benzersiz adlarıyla MyID.cer</span><span class="sxs-lookup"><span data-stu-id="beaaa-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="beaaa-272">Bu komut, oluşturulan ve bir kez kullanılan bir parola toobe için sorar.</span><span class="sxs-lookup"><span data-stu-id="beaaa-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="beaaa-273">Güçlü bir parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="beaaa-274">PFX dosyaları için istemci sertifikaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="beaaa-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="beaaa-275">Her oluşturulan istemci sertifikası için yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="beaaa-276">Özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="beaaa-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="beaaa-277">Bir parola girin ve sonra bu seçenekler ile sertifika verme:</span><span class="sxs-lookup"><span data-stu-id="beaaa-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="beaaa-278">Evet, hello özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-278">Yes, export hello private key</span></span>
* <span data-ttu-id="beaaa-279">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-279">Export all extended properties</span></span>
* <span data-ttu-id="beaaa-280">Bu sertifikayı veren hello tek tek toowhom hello verme parola seçmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="beaaa-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="beaaa-281">İstemci sertifikası Al</span><span class="sxs-lookup"><span data-stu-id="beaaa-281">Import client certificate</span></span>
<span data-ttu-id="beaaa-282">Kendisi için bir istemci sertifikası yayımlandığı her hello anahtar çifti almalısınız hello makinelerinizde klasöründe toocommunicate hello hizmetiyle kullanır:</span><span class="sxs-lookup"><span data-stu-id="beaaa-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="beaaa-283">Merhaba çift tıklayın. Windows Gezgini'nde PFX dosyası</span><span class="sxs-lookup"><span data-stu-id="beaaa-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="beaaa-284">Sertifikayı kişisel deposu ile en az bu seçenek hello alın:</span><span class="sxs-lookup"><span data-stu-id="beaaa-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="beaaa-285">Seçili tüm genişletilmiş özellikleri Ekle</span><span class="sxs-lookup"><span data-stu-id="beaaa-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="beaaa-286">İstemci sertifikası parmak kopyalayın</span><span class="sxs-lookup"><span data-stu-id="beaaa-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="beaaa-287">Kendisi için bir istemci sertifikası yayımlandığı her sipariş tooobtain hello parmak izi his/hers'nda aşağıdaki adımları izlemelisiniz toohello hizmet yapılandırma dosyası eklenecek sertifikası:</span><span class="sxs-lookup"><span data-stu-id="beaaa-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="beaaa-288">Certmgr.exe çalıştırın</span><span class="sxs-lookup"><span data-stu-id="beaaa-288">Run certmgr.exe</span></span>
* <span data-ttu-id="beaaa-289">Merhaba kişisel sekmesini seçin</span><span class="sxs-lookup"><span data-stu-id="beaaa-289">Select hello Personal tab</span></span>
* <span data-ttu-id="beaaa-290">Toobe kimlik doğrulaması için kullanılan hello istemci sertifikasına çift tıklayın</span><span class="sxs-lookup"><span data-stu-id="beaaa-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="beaaa-291">Merhaba Ayrıntılar sekmesini açar hello sertifikası iletişim kutusunda, seçin</span><span class="sxs-lookup"><span data-stu-id="beaaa-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="beaaa-292">Göster tüm görüntülediğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="beaaa-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="beaaa-293">Parmak izi hello listesinde adlı select hello alanı</span><span class="sxs-lookup"><span data-stu-id="beaaa-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="beaaa-294">Merhaba hello parmak izi değerini kopyalayın ** hello ilk rakam önünde görünür olmayan Unicode karakterler silme ** tüm alanları Sil</span><span class="sxs-lookup"><span data-stu-id="beaaa-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="beaaa-295">Merhaba hizmet yapılandırma dosyasında izin verilen istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="beaaa-296">Merhaba hizmet yapılandırma dosyasında virgülle ayrılmış listesini içeren hello sertifikalarının parmak izleri erişim toohello hizmeti izin verilen hello istemci ayarı aşağıdaki hello Hello değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="beaaa-297">İstemci sertifikası iptal denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="beaaa-298">Merhaba varsayılan ayarı, istemcinin sertifika iptal durumunu Merhaba sertifika yetkilisi ile kontrol etmez.</span><span class="sxs-lookup"><span data-stu-id="beaaa-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="beaaa-299">hello üzerinde tooturn denetler Hello hello istemci sertifikaları veren sertifika yetkilisi bu tür denetimler destekliyorsa, hello X509RevocationMode numaralandırma tanımlanan hello değerlerden biriyle ayarı aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="beaaa-300">Otomatik olarak imzalanan şifreleme sertifikaları için PFX dosyası oluşturun</span><span class="sxs-lookup"><span data-stu-id="beaaa-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="beaaa-301">Bir şifreleme sertifikası için yürütün:</span><span class="sxs-lookup"><span data-stu-id="beaaa-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="beaaa-302">Özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="beaaa-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="beaaa-303">Bir parola girin ve sonra bu seçenekler ile sertifika verme:</span><span class="sxs-lookup"><span data-stu-id="beaaa-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="beaaa-304">Evet, hello özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-304">Yes, export hello private key</span></span>
* <span data-ttu-id="beaaa-305">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-305">Export all extended properties</span></span>
* <span data-ttu-id="beaaa-306">Merhaba sertifika toohello bulut hizmeti karşıya yüklenirken hello parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="beaaa-307">Şifreleme sertifikası sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="beaaa-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="beaaa-308">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="beaaa-308">Find certificate</span></span>
* <span data-ttu-id="beaaa-309">Tıklatın Eylemler -> tüm görevleri Export ->...</span><span class="sxs-lookup"><span data-stu-id="beaaa-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="beaaa-310">İçinde sertifika verme bir. Bu seçenekler PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="beaaa-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="beaaa-311">Evet, hello özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="beaaa-312">Mümkünse hello sertifika yolundaki tüm sertifikaları dahil et</span><span class="sxs-lookup"><span data-stu-id="beaaa-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="beaaa-313">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="beaaa-314">Şifreleme sertifikası toocloud hizmeti karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="beaaa-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="beaaa-315">Karşıya yükleme hello var olan sertifika veya oluşturulabilir. Merhaba şifreleme anahtar çifti PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="beaaa-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="beaaa-316">Merhaba özel anahtar bilgisi koruma hello parolayı girin</span><span class="sxs-lookup"><span data-stu-id="beaaa-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="beaaa-317">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="beaaa-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="beaaa-318">Merhaba parmak izi hello karşıya sertifika toohello bulut hizmeti ile Merhaba hizmet yapılandırma dosyası ayarlarında aşağıdaki hello Hello parmak izi değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="beaaa-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="beaaa-319">Ortak sertifika işlemleri</span><span class="sxs-lookup"><span data-stu-id="beaaa-319">Common certificate operations</span></span>
* <span data-ttu-id="beaaa-320">Merhaba SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="beaaa-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="beaaa-321">İstemci sertifikaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="beaaa-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="beaaa-322">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="beaaa-322">Find certificate</span></span>
<span data-ttu-id="beaaa-323">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="beaaa-323">Follow these steps:</span></span>

1. <span data-ttu-id="beaaa-324">MMC.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="beaaa-325">Dosya -> Ekle/Kaldır ek bileşenini...</span><span class="sxs-lookup"><span data-stu-id="beaaa-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="beaaa-326">Seçin **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="beaaa-327">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-327">Click **Add**.</span></span>
5. <span data-ttu-id="beaaa-328">Merhaba sertifika deposu konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="beaaa-329">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-329">Click **Finish**.</span></span>
7. <span data-ttu-id="beaaa-330">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-330">Click **OK**.</span></span>
8. <span data-ttu-id="beaaa-331">Genişletme **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="beaaa-332">Merhaba sertifika deposu düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="beaaa-333">Merhaba sertifika alt düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="beaaa-334">Bir sertifika hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="beaaa-335">Sertifika verme</span><span class="sxs-lookup"><span data-stu-id="beaaa-335">Export certificate</span></span>
<span data-ttu-id="beaaa-336">Merhaba, **Sertifika Verme Sihirbazı**:</span><span class="sxs-lookup"><span data-stu-id="beaaa-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="beaaa-337">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-337">Click **Next**.</span></span>
2. <span data-ttu-id="beaaa-338">Seçin **Evet**, ardından **verme hello özel anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="beaaa-339">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-339">Click **Next**.</span></span>
4. <span data-ttu-id="beaaa-340">Merhaba istenen çıktı dosyası biçimini seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="beaaa-341">İstenen başlangıç seçeneklerini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-341">Check hello desired options.</span></span>
6. <span data-ttu-id="beaaa-342">Denetleme **parola**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-342">Check **Password**.</span></span>
7. <span data-ttu-id="beaaa-343">Güçlü bir parola girin ve onaylayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="beaaa-344">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-344">Click **Next**.</span></span>
9. <span data-ttu-id="beaaa-345">Yazın veya burada toostore hello sertifika filename göz atın (kullanan bir. PFX uzantılı).</span><span class="sxs-lookup"><span data-stu-id="beaaa-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="beaaa-346">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-346">Click **Next**.</span></span>
11. <span data-ttu-id="beaaa-347">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-347">Click **Finish**.</span></span>
12. <span data-ttu-id="beaaa-348">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="beaaa-349">Sertifika İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="beaaa-349">Import certificate</span></span>
<span data-ttu-id="beaaa-350">Merhaba Sertifika Alma Sihirbazı:</span><span class="sxs-lookup"><span data-stu-id="beaaa-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="beaaa-351">Merhaba depolama konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="beaaa-352">Seçin **geçerli kullanıcı** geçerli kullanıcı altında çalışan işlemler hello hizmeti erişecek yalnızca</span><span class="sxs-lookup"><span data-stu-id="beaaa-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="beaaa-353">Seçin **yerel makine** bu bilgisayardaki diğer işlemlerin hello hizmet erişecekse</span><span class="sxs-lookup"><span data-stu-id="beaaa-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="beaaa-354">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-354">Click **Next**.</span></span>
3. <span data-ttu-id="beaaa-355">Bir dosyadan içeri aktarma, hello dosya yolunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="beaaa-356">İçeri aktarma, bir. PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="beaaa-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="beaaa-357">Merhaba özel anahtarın korunması hello parolayı girin</span><span class="sxs-lookup"><span data-stu-id="beaaa-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="beaaa-358">İçeri aktarma seçenekleri seçin</span><span class="sxs-lookup"><span data-stu-id="beaaa-358">Select import options</span></span>
5. <span data-ttu-id="beaaa-359">Mağaza aşağıdaki hello "Yerine" Sertifikalar'ı seçin</span><span class="sxs-lookup"><span data-stu-id="beaaa-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="beaaa-360">**Gözat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-360">Click **Browse**.</span></span>
7. <span data-ttu-id="beaaa-361">Merhaba istenen depolama alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-361">Select hello desired store.</span></span>
8. <span data-ttu-id="beaaa-362">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="beaaa-363">Merhaba güvenilen kök sertifika yetkilisi deposunda seçildiyse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="beaaa-364">Tıklatın **Tamam** tüm iletişim Windows.</span><span class="sxs-lookup"><span data-stu-id="beaaa-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="beaaa-365">Sertifikayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="beaaa-365">Upload certificate</span></span>
<span data-ttu-id="beaaa-366">Merhaba, [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="beaaa-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="beaaa-367">Seçin **bulut hizmetlerini**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="beaaa-368">Merhaba bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="beaaa-369">Merhaba üst menüsünde **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="beaaa-370">Merhaba alt çubuğunda **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="beaaa-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="beaaa-371">Merhaba sertifika dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="beaaa-372">Bu doğruysa bir. PFX dosyası, hello parola hello özel anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="beaaa-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="beaaa-373">Tamamlandığında, hello sertifika parmak izi hello yeni giriş hello listesinde kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="beaaa-374">Diğer güvenlik konuları</span><span class="sxs-lookup"><span data-stu-id="beaaa-374">Other security considerations</span></span>
<span data-ttu-id="beaaa-375">Merhaba HTTPS uç noktası kullanıldığında, bu belgede açıklanan hello SSL ayarları hello hizmet ve istemcileri arasındaki iletişimi şifrelemek.</span><span class="sxs-lookup"><span data-stu-id="beaaa-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="beaaa-376">Bu veritabanı erişimi için kimlik bilgilerini bu yana önemlidir ve hello iletişiminde büyük olasılıkla diğer hassas bilgiler yer alır.</span><span class="sxs-lookup"><span data-stu-id="beaaa-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="beaaa-377">Ancak, hello hizmeti kimlik bilgileri, kendi iç Microsoft Azure aboneliğiniz meta veri depolama alanı için sağlanan hello Microsoft Azure SQL veritabanı tablolarında dahil olmak üzere, iç durum devam ederse unutmayın.</span><span class="sxs-lookup"><span data-stu-id="beaaa-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="beaaa-378">Bu veritabanı ayarı hizmet yapılandırma dosyanızdaki aşağıdaki hello bir parçası olarak tanımlandı (. CSCFG dosyası):</span><span class="sxs-lookup"><span data-stu-id="beaaa-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="beaaa-379">Bu veritabanında depolanan kimlik bilgileri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="beaaa-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="beaaa-380">Ancak, en iyi uygulama, hizmet dağıtımlarınız web ve çalışan rolleri toodate tutulur ve güvenli olarak hem şifreleme ve şifre çözme depolanan kimlik bilgileri için kullanılan erişim toohello meta veri veritabanı ve hello sertifika içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="beaaa-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

