---
title: "Bölünmüş birleştirme güvenlik yapılandırması | Microsoft Docs"
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
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="34f2f-103">Bölünmüş birleştirme güvenlik yapılandırması</span><span class="sxs-lookup"><span data-stu-id="34f2f-103">Split-merge security configuration</span></span>
<span data-ttu-id="34f2f-104">Bölünmüş/Merge hizmetini kullanmak için güvenlik doğru şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="34f2f-105">Hizmet Microsoft Azure SQL veritabanı'nın esnek ölçeklendirme özelliği bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="34f2f-106">Daha fazla bilgi için bkz: [esnek ölçek bölme ve birleştirme hizmet öğretici](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="34f2f-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="34f2f-107">Sertifikaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-107">Configuring certificates</span></span>
<span data-ttu-id="34f2f-108">Sertifikalar iki şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="34f2f-109">SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="34f2f-110">İstemci sertifikalarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="34f2f-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="34f2f-111">Sertifikaları almak için</span><span class="sxs-lookup"><span data-stu-id="34f2f-111">To obtain certificates</span></span>
<span data-ttu-id="34f2f-112">Ortak sertifika yetkilileri (CA) ya da sertifika elde edilebilir [Windows sertifika hizmeti](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="34f2f-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="34f2f-113">Bu sertifikaları almak için tercih edilen yöntemler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="34f2f-114">Bu seçenek mevcut değilse, oluşturabileceğiniz **otomatik olarak imzalanan sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="34f2f-115">Sertifikalarını oluşturmak için Araçlar</span><span class="sxs-lookup"><span data-stu-id="34f2f-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="34f2f-116">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="34f2f-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="34f2f-117">Pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="34f2f-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="34f2f-118">Araçları çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="34f2f-118">To run the tools</span></span>
* <span data-ttu-id="34f2f-119">Bir geliştirici komut isteminden Visual stüdyoları için bkz: [Visual Studio komut istemi](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="34f2f-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="34f2f-120">Yüklü değilse, aşağıdaki adrese gidin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="34f2f-121">Gelen WDK almak [Windows 8.1: indirme setleri ve araçları](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="34f2f-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="34f2f-122">SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-122">To configure the SSL certificate</span></span>
<span data-ttu-id="34f2f-123">Bir SSL sertifikası, iletişimi şifrelemek ve sunucu kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="34f2f-124">Aşağıdaki üç senaryodan en uygun seçin ve tüm adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="34f2f-125">Yeni bir otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="34f2f-126">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="34f2f-127">PFX dosyası için otomatik olarak imzalanan SSL sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="34f2f-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="34f2f-128">Bulut hizmeti için SSL sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="34f2f-129">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="34f2f-130">SSL sertifika yetkilisi alma</span><span class="sxs-lookup"><span data-stu-id="34f2f-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="34f2f-131">Varolan bir sertifikayı sertifika deposundan kullanmak için</span><span class="sxs-lookup"><span data-stu-id="34f2f-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="34f2f-132">SSL sertifikası, sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="34f2f-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="34f2f-133">Bulut hizmeti için SSL sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="34f2f-134">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="34f2f-135">Varolan bir sertifikayı bir PFX dosyası kullanmak için</span><span class="sxs-lookup"><span data-stu-id="34f2f-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="34f2f-136">Bulut hizmeti için SSL sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="34f2f-137">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="34f2f-138">İstemci sertifikalarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="34f2f-138">To configure client certificates</span></span>
<span data-ttu-id="34f2f-139">İstemci sertifikalarını hizmet isteklerine kimlik doğrulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="34f2f-140">Aşağıdaki üç senaryodan en uygun seçin ve tüm adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="34f2f-141">İstemci sertifikaları devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="34f2f-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="34f2f-142">İstemci sertifikası tabanlı kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="34f2f-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="34f2f-143">Yeni otomatik olarak imzalanan istemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="34f2f-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="34f2f-144">Bir otomatik olarak imzalanan sertifika yetkilisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="34f2f-145">Bulut hizmeti için CA sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="34f2f-146">Hizmet yapılandırma dosyasında CA sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="34f2f-147">İstemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="34f2f-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="34f2f-148">PFX dosyaları için istemci sertifikaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="34f2f-149">İstemci sertifikası Al</span><span class="sxs-lookup"><span data-stu-id="34f2f-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="34f2f-150">İstemci sertifikası parmak kopyalayın</span><span class="sxs-lookup"><span data-stu-id="34f2f-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="34f2f-151">Hizmet yapılandırma dosyasında izin verilen istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="34f2f-152">Mevcut istemci sertifikalarını kullanın</span><span class="sxs-lookup"><span data-stu-id="34f2f-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="34f2f-153">CA ortak anahtarı bulma</span><span class="sxs-lookup"><span data-stu-id="34f2f-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="34f2f-154">Bulut hizmeti için CA sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="34f2f-155">Hizmet yapılandırma dosyasında CA sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="34f2f-156">İstemci sertifikası parmak kopyalayın</span><span class="sxs-lookup"><span data-stu-id="34f2f-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="34f2f-157">Hizmet yapılandırma dosyasında izin verilen istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="34f2f-158">İstemci sertifikası iptal denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="34f2f-159">İzin verilen IP adresi</span><span class="sxs-lookup"><span data-stu-id="34f2f-159">Allowed IP addresses</span></span>
<span data-ttu-id="34f2f-160">Hizmet uç noktalarına erişime belirli IP adresi aralıkları için kısıtlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="34f2f-161">Depolama alanı için şifrelemeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-161">To configure encryption for the store</span></span>
<span data-ttu-id="34f2f-162">Meta veri deposunda saklanan kimlik bilgilerini şifrelemek için bir sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="34f2f-163">Aşağıdaki üç senaryodan en uygun seçin ve tüm adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="34f2f-164">Yeni bir otomatik olarak imzalanan sertifika kullan</span><span class="sxs-lookup"><span data-stu-id="34f2f-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="34f2f-165">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="34f2f-166">PFX dosyası için otomatik olarak imzalanan şifreleme sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="34f2f-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="34f2f-167">Bulut hizmeti için şifreleme sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="34f2f-168">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="34f2f-169">Varolan bir sertifikayı sertifika deposundan kullanın</span><span class="sxs-lookup"><span data-stu-id="34f2f-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="34f2f-170">Şifreleme sertifikası sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="34f2f-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="34f2f-171">Bulut hizmeti için şifreleme sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="34f2f-172">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="34f2f-173">Varolan bir sertifikayı bir PFX dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="34f2f-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="34f2f-174">Bulut hizmeti için şifreleme sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="34f2f-175">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="34f2f-176">Varsayılan yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-176">The default configuration</span></span>
<span data-ttu-id="34f2f-177">Varsayılan yapılandırma, tüm HTTP uç noktası erişimi reddeder.</span><span class="sxs-lookup"><span data-stu-id="34f2f-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="34f2f-178">Bu uç noktalar isteklerine veritabanı kimlik bilgileri gibi hassas bilgileri taşımak beri önerilen, ayar budur.</span><span class="sxs-lookup"><span data-stu-id="34f2f-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="34f2f-179">Varsayılan yapılandırma tüm HTTPS uç noktasını erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="34f2f-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="34f2f-180">Bu ayar daha fazla kısıtlanabilir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="34f2f-181">Yapılandırmayı değiştirme</span><span class="sxs-lookup"><span data-stu-id="34f2f-181">Changing the Configuration</span></span>
<span data-ttu-id="34f2f-182">Grubun geçerli erişim denetim kurallarını ve uç nokta yapılandırılmış  **<EndpointAcls>**  bölümüne **hizmet yapılandırma dosyası**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="34f2f-183">Bir erişim denetimi grubu kurallarında yapılandırılan bir <AccessControl name=""> hizmet yapılandırma dosyasının.</span><span class="sxs-lookup"><span data-stu-id="34f2f-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="34f2f-184">Biçim ağ erişim denetimi listelerini belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="34f2f-185">Örneğin, yalnızca IP aralığı HTTPS uç noktasına erişmek için 100.100.0.0 için 100.100.255.255 izin vermek için kuralları şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="34f2f-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="34f2f-186">Hizmet önleme reddi</span><span class="sxs-lookup"><span data-stu-id="34f2f-186">Denial of service prevention</span></span>
<span data-ttu-id="34f2f-187">Desteklenen algılamak ve hizmet reddi saldırılarını önlemek için iki farklı mekanizma vardır:</span><span class="sxs-lookup"><span data-stu-id="34f2f-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="34f2f-188">Uzak ana bilgisayar başına eşzamanlı istek sayısını kısıtlayın (varsayılan olarak kapalıdır)</span><span class="sxs-lookup"><span data-stu-id="34f2f-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="34f2f-189">Uzak ana bilgisayar başına erişimi oranını kısıtlamak (üzerinde varsayılan olarak)</span><span class="sxs-lookup"><span data-stu-id="34f2f-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="34f2f-190">Bunlar daha fazla dinamik IP Güvenlik IIS'de açıklandığı özellikleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="34f2f-191">Ne zaman bu yapılandırmasını değiştirme aşağıdaki etmenlere dikkat:</span><span class="sxs-lookup"><span data-stu-id="34f2f-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="34f2f-192">Proxy ve ağ adresi çevirisi aygıtları üzerinden uzak ana bilgisayar bilgilerini davranışını</span><span class="sxs-lookup"><span data-stu-id="34f2f-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="34f2f-193">Web rolü herhangi bir kaynağa her istek (örneğin yükleme komut dosyaları, görüntüler, vb.) olarak kabul edilir</span><span class="sxs-lookup"><span data-stu-id="34f2f-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="34f2f-194">Eşzamanlı erişimi sayısını sınırlandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="34f2f-195">Bu davranışı yapılandırmak ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34f2f-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="34f2f-196">DynamicIpRestrictionDenyByConcurrentRequests bu korumayı etkinleştirmek için true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="34f2f-197">Erişim kısıtlama oranı</span><span class="sxs-lookup"><span data-stu-id="34f2f-197">Restricting rate of access</span></span>
<span data-ttu-id="34f2f-198">Bu davranışı yapılandırmak ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34f2f-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="34f2f-199">Reddedilen isteğinin yanıtı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="34f2f-200">Aşağıdaki ayar reddedilen isteğinin yanıtı yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="34f2f-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="34f2f-201">Desteklenen diğer değerler için dinamik IP Güvenlik IIS'de belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="34f2f-202">Hizmet sertifikaları yapılandırma işlemleri</span><span class="sxs-lookup"><span data-stu-id="34f2f-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="34f2f-203">Bu konu yalnızca başvuru amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-203">This topic is for reference only.</span></span> <span data-ttu-id="34f2f-204">Lütfen özetlenen yapılandırma adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="34f2f-205">SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="34f2f-206">İstemci sertifikaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="34f2f-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="34f2f-207">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-207">Create a self-signed certificate</span></span>
<span data-ttu-id="34f2f-208">Yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="34f2f-209">Özelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="34f2f-209">To customize:</span></span>

* <span data-ttu-id="34f2f-210">-n hizmet URL'si.</span><span class="sxs-lookup"><span data-stu-id="34f2f-210">-n with the service URL.</span></span> <span data-ttu-id="34f2f-211">Joker karakterler ("CN = * .cloudapp .net") ve diğer adları ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") desteklenir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="34f2f-212">-e sertifika sona erme tarihi ile güçlü bir parola oluşturmak ve istendiğinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="34f2f-213">Otomatik olarak imzalanan SSL Sertifika PFX dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="34f2f-214">Yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="34f2f-215">Bir parola girin ve sonra bu seçenekler ile sertifika verme:</span><span class="sxs-lookup"><span data-stu-id="34f2f-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="34f2f-216">Evet, özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-216">Yes, export the private key</span></span>
* <span data-ttu-id="34f2f-217">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="34f2f-218">SSL sertifikası, sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="34f2f-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="34f2f-219">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="34f2f-219">Find certificate</span></span>
* <span data-ttu-id="34f2f-220">Tıklatın Eylemler -> tüm görevleri Export ->...</span><span class="sxs-lookup"><span data-stu-id="34f2f-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="34f2f-221">İçinde sertifika verme bir. Bu seçenekler PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="34f2f-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="34f2f-222">Evet, özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-222">Yes, export the private key</span></span>
  * <span data-ttu-id="34f2f-223">Mümkünse sertifika yolundaki tüm sertifikaları dahil et * tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="34f2f-224">Bulut hizmeti için SSL sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="34f2f-225">Karşıya yükleme, var olan sertifika veya oluşturulabilir. SSL anahtar çifti PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="34f2f-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="34f2f-226">Özel anahtar bilgisi koruyan parolayı girin</span><span class="sxs-lookup"><span data-stu-id="34f2f-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="34f2f-227">Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="34f2f-228">Bulut hizmetine karşıya sertifikanın parmak izine sahip hizmet yapılandırma dosyasında aşağıdaki ayar parmak izi değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="34f2f-229">SSL sertifika yetkilisi alma</span><span class="sxs-lookup"><span data-stu-id="34f2f-229">Import SSL certification authority</span></span>
<span data-ttu-id="34f2f-230">Tüm hesap/hizmet ile iletişim kuracak makinesinde aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="34f2f-231">Çift tıklayın. Windows Gezgini'nde CER dosyasını</span><span class="sxs-lookup"><span data-stu-id="34f2f-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="34f2f-232">Sertifika iletişim kutusunda, sertifikayı yükle düğmesine...</span><span class="sxs-lookup"><span data-stu-id="34f2f-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="34f2f-233">Güvenilen Kök Sertifika Yetkilileri deposuna sertifika İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="34f2f-234">İstemci sertifikası tabanlı kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="34f2f-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="34f2f-235">Yalnızca istemci sertifika tabanlı kimlik doğrulaması desteklenmez ve diğer mekanizmaları (örneğin Microsoft Azure sanal ağı) yerinde olmadıkça devre dışı bırakmasını hizmet uç noktalarına erişimine izin verir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="34f2f-236">Hizmet yapılandırma dosyasında özelliği devre dışı bırakmak için false bu ayarları değiştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="34f2f-237">Ardından, SSL sertifikası ile aynı parmak izine CA sertifikası ayarında kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="34f2f-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="34f2f-238">Bir otomatik olarak imzalanan sertifika yetkilisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="34f2f-239">Bir sertifika yetkilisi olarak davranacak şekilde otomatik olarak imzalanan bir sertifika oluşturmak için aşağıdaki adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="34f2f-240">Özelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="34f2f-240">To customize it</span></span>

* <span data-ttu-id="34f2f-241">-e ile sertifika sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="34f2f-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="34f2f-242">CA ortak anahtarı bulma</span><span class="sxs-lookup"><span data-stu-id="34f2f-242">Find CA public key</span></span>
<span data-ttu-id="34f2f-243">İstemci sertifikalarının tümünü hizmeti tarafından güvenilen bir sertifika yetkilisi tarafından verilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="34f2f-244">İstemci kimlik doğrulaması için bulut hizmetine yüklemek için kullanılacak sertifikaları veren sertifika yetkilisine ortak anahtar bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34f2f-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="34f2f-245">Ortak anahtar dosyasıyla kullanılabilir durumda değilse, sertifika deposundan dışarı aktarın:</span><span class="sxs-lookup"><span data-stu-id="34f2f-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="34f2f-246">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="34f2f-246">Find certificate</span></span>
  * <span data-ttu-id="34f2f-247">Aynı sertifika yetkilisi tarafından verilen bir istemci sertifikası için arama yapın</span><span class="sxs-lookup"><span data-stu-id="34f2f-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="34f2f-248">Sertifikayı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-248">Double-click the certificate.</span></span>
* <span data-ttu-id="34f2f-249">Sertifika iletişim kutusunda sertifika yolu sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="34f2f-250">Yolun CA girişi çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="34f2f-251">Sertifika Özellikleri not alın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="34f2f-252">Kapat **sertifika** iletişim.</span><span class="sxs-lookup"><span data-stu-id="34f2f-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="34f2f-253">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="34f2f-253">Find certificate</span></span>
  * <span data-ttu-id="34f2f-254">Yukarıda belirtilen CA'yı arayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="34f2f-255">Tıklatın Eylemler -> tüm görevleri Export ->...</span><span class="sxs-lookup"><span data-stu-id="34f2f-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="34f2f-256">İçinde sertifika verme bir. CER bu seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="34f2f-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="34f2f-257">**Hayır, özel anahtarı verme**</span><span class="sxs-lookup"><span data-stu-id="34f2f-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="34f2f-258">Tüm sertifikaları mümkünse sertifika yolundaki içerir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="34f2f-259">Tüm genişletilmiş özellikleri dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="34f2f-260">Bulut hizmeti için CA sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="34f2f-261">Karşıya yükleme, var olan sertifika veya oluşturulabilir. CER dosyasını CA ortak anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="34f2f-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="34f2f-262">Hizmet yapılandırma dosyasında güncelleştirme CA sertifikası</span><span class="sxs-lookup"><span data-stu-id="34f2f-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="34f2f-263">Bulut hizmetine karşıya sertifikanın parmak izine sahip hizmet yapılandırma dosyasında aşağıdaki ayar parmak izi değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="34f2f-264">Aşağıdaki ayarı değerini aynı parmak izine sahip güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="34f2f-265">İstemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="34f2f-265">Issue client certificates</span></span>
<span data-ttu-id="34f2f-266">Her hizmete erişmek için yetkili kullanmak özel his/hers için yayımlanan bir istemci sertifikasına sahip olmalıdır ve his/hers kendi özel anahtarını korumak için güçlü bir parola seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="34f2f-267">Aşağıdaki adımları otomatik olarak imzalanan sertifika burada oluşturulan ve saklanan aynı makinede çalıştırılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="34f2f-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="34f2f-268">Özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="34f2f-268">Customizing:</span></span>

* <span data-ttu-id="34f2f-269">-n Bu sertifika ile kimlik doğrulaması yapılacak istemci için bir kimliği olan</span><span class="sxs-lookup"><span data-stu-id="34f2f-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="34f2f-270">-e ile sertifika sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="34f2f-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="34f2f-271">MyID.pvk ve bu istemci sertifikası için benzersiz adlarıyla MyID.cer</span><span class="sxs-lookup"><span data-stu-id="34f2f-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="34f2f-272">Bu komut oluşturulabilir ve bir kez kullanılması bir parola sorar.</span><span class="sxs-lookup"><span data-stu-id="34f2f-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="34f2f-273">Güçlü bir parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="34f2f-274">PFX dosyaları için istemci sertifikaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="34f2f-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="34f2f-275">Her oluşturulan istemci sertifikası için yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="34f2f-276">Özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="34f2f-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="34f2f-277">Bir parola girin ve sonra bu seçenekler ile sertifika verme:</span><span class="sxs-lookup"><span data-stu-id="34f2f-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="34f2f-278">Evet, özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-278">Yes, export the private key</span></span>
* <span data-ttu-id="34f2f-279">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-279">Export all extended properties</span></span>
* <span data-ttu-id="34f2f-280">Bu sertifika yayımlanmaktadır tek verme parola seçmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="34f2f-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="34f2f-281">İstemci sertifikası Al</span><span class="sxs-lookup"><span data-stu-id="34f2f-281">Import client certificate</span></span>
<span data-ttu-id="34f2f-282">Kendisi için bir istemci sertifikası verilmiş olan her anahtar çifti klasöründe hizmetiyle iletişim kurmak için kullanacağınız makinelerde almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="34f2f-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="34f2f-283">Çift tıklayın. Windows Gezgini'nde PFX dosyası</span><span class="sxs-lookup"><span data-stu-id="34f2f-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="34f2f-284">İçeri aktarma kişisel içine deposundan sertifika ile en az bu seçeneği:</span><span class="sxs-lookup"><span data-stu-id="34f2f-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="34f2f-285">Seçili tüm genişletilmiş özellikleri Ekle</span><span class="sxs-lookup"><span data-stu-id="34f2f-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="34f2f-286">İstemci sertifikası parmak kopyalayın</span><span class="sxs-lookup"><span data-stu-id="34f2f-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="34f2f-287">Kendisi için bir istemci sertifikası yayımlandığı her parmak izini his/hers almak için şu adımları izlemelisiniz service yapılandırma dosyasına eklenecek sertifikası:</span><span class="sxs-lookup"><span data-stu-id="34f2f-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="34f2f-288">Certmgr.exe çalıştırın</span><span class="sxs-lookup"><span data-stu-id="34f2f-288">Run certmgr.exe</span></span>
* <span data-ttu-id="34f2f-289">Kişisel sekmesini seçin</span><span class="sxs-lookup"><span data-stu-id="34f2f-289">Select the Personal tab</span></span>
* <span data-ttu-id="34f2f-290">Kimlik doğrulaması için kullanılacak istemci sertifikası çift tıklatın</span><span class="sxs-lookup"><span data-stu-id="34f2f-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="34f2f-291">Açılır sertifikası iletişim kutusunda, Ayrıntılar sekmesini seçin</span><span class="sxs-lookup"><span data-stu-id="34f2f-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="34f2f-292">Göster tüm görüntülediğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="34f2f-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="34f2f-293">Parmak izi listede adlı alanı seçin</span><span class="sxs-lookup"><span data-stu-id="34f2f-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="34f2f-294">Parmak izi değerini kopyalayın ** ilk rakam önünde görünür olmayan Unicode karakterler silme ** tüm alanları Sil</span><span class="sxs-lookup"><span data-stu-id="34f2f-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="34f2f-295">Hizmet yapılandırma dosyasında izin verilen istemcilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="34f2f-296">Hizmet yapılandırma dosyasında aşağıdaki ayarın değerini hizmetine erişim izni olan istemci sertifikalarının parmak izleri virgülle ayrılmış bir listesi ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="34f2f-297">İstemci sertifikası iptal denetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="34f2f-298">Varsayılan ayar, istemcinin sertifika iptal durumunu için sertifika yetkilisi ile kontrol etmez.</span><span class="sxs-lookup"><span data-stu-id="34f2f-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="34f2f-299">İstemci sertifikaları veren sertifika yetkilisini bu tür denetimler destekliyorsa üzerinde denetimleri, etkinleştirmek için X509RevocationMode sıralamasında tanımlanan değerlerden biriyle aşağıdaki ayarını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="34f2f-300">Otomatik olarak imzalanan şifreleme sertifikaları için PFX dosyası oluşturun</span><span class="sxs-lookup"><span data-stu-id="34f2f-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="34f2f-301">Bir şifreleme sertifikası için yürütün:</span><span class="sxs-lookup"><span data-stu-id="34f2f-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="34f2f-302">Özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="34f2f-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="34f2f-303">Bir parola girin ve sonra bu seçenekler ile sertifika verme:</span><span class="sxs-lookup"><span data-stu-id="34f2f-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="34f2f-304">Evet, özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-304">Yes, export the private key</span></span>
* <span data-ttu-id="34f2f-305">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-305">Export all extended properties</span></span>
* <span data-ttu-id="34f2f-306">Bulut hizmeti için sertifikayı karşıya yüklenirken parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="34f2f-307">Şifreleme sertifikası sertifika deposundan dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="34f2f-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="34f2f-308">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="34f2f-308">Find certificate</span></span>
* <span data-ttu-id="34f2f-309">Tıklatın Eylemler -> tüm görevleri Export ->...</span><span class="sxs-lookup"><span data-stu-id="34f2f-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="34f2f-310">İçinde sertifika verme bir. Bu seçenekler PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="34f2f-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="34f2f-311">Evet, özel anahtarı dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-311">Yes, export the private key</span></span>
  * <span data-ttu-id="34f2f-312">Mümkünse sertifika yolundaki tüm sertifikaları dahil et</span><span class="sxs-lookup"><span data-stu-id="34f2f-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="34f2f-313">Tüm genişletilmiş özellikleri Dışarı Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="34f2f-314">Bulut hizmetine şifreleme sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="34f2f-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="34f2f-315">Karşıya yükleme, var olan sertifika veya oluşturulabilir. Şifreleme anahtar çifti PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="34f2f-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="34f2f-316">Özel anahtar bilgisi koruyan parolayı girin</span><span class="sxs-lookup"><span data-stu-id="34f2f-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="34f2f-317">Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="34f2f-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="34f2f-318">Bulut hizmetine karşıya sertifikanın parmak izine sahip parmak izi değeri hizmet yapılandırma dosyasında aşağıdaki ayarlardan birini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="34f2f-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="34f2f-319">Ortak sertifika işlemleri</span><span class="sxs-lookup"><span data-stu-id="34f2f-319">Common certificate operations</span></span>
* <span data-ttu-id="34f2f-320">SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34f2f-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="34f2f-321">İstemci sertifikaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="34f2f-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="34f2f-322">Sertifika Bul</span><span class="sxs-lookup"><span data-stu-id="34f2f-322">Find certificate</span></span>
<span data-ttu-id="34f2f-323">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="34f2f-323">Follow these steps:</span></span>

1. <span data-ttu-id="34f2f-324">MMC.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="34f2f-325">Dosya -> Ekle/Kaldır ek bileşenini...</span><span class="sxs-lookup"><span data-stu-id="34f2f-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="34f2f-326">Seçin **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="34f2f-327">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-327">Click **Add**.</span></span>
5. <span data-ttu-id="34f2f-328">Sertifika depolama konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="34f2f-329">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-329">Click **Finish**.</span></span>
7. <span data-ttu-id="34f2f-330">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-330">Click **OK**.</span></span>
8. <span data-ttu-id="34f2f-331">Genişletme **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="34f2f-332">Sertifika deposu düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="34f2f-333">Sertifika alt düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="34f2f-334">Listeden bir sertifika seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="34f2f-335">Sertifika verme</span><span class="sxs-lookup"><span data-stu-id="34f2f-335">Export certificate</span></span>
<span data-ttu-id="34f2f-336">İçinde **Sertifika Verme Sihirbazı**:</span><span class="sxs-lookup"><span data-stu-id="34f2f-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="34f2f-337">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-337">Click **Next**.</span></span>
2. <span data-ttu-id="34f2f-338">Seçin **Evet**, ardından **özel anahtarı dışarı**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="34f2f-339">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-339">Click **Next**.</span></span>
4. <span data-ttu-id="34f2f-340">İstenen çıktı dosyası biçimini seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="34f2f-341">İstenen seçenekleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-341">Check the desired options.</span></span>
6. <span data-ttu-id="34f2f-342">Denetleme **parola**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-342">Check **Password**.</span></span>
7. <span data-ttu-id="34f2f-343">Güçlü bir parola girin ve onaylayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="34f2f-344">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-344">Click **Next**.</span></span>
9. <span data-ttu-id="34f2f-345">Yazın veya bir dosya adı sertifikanın depolanacağı yeri göz atın (kullanan bir. PFX uzantılı).</span><span class="sxs-lookup"><span data-stu-id="34f2f-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="34f2f-346">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-346">Click **Next**.</span></span>
11. <span data-ttu-id="34f2f-347">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-347">Click **Finish**.</span></span>
12. <span data-ttu-id="34f2f-348">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="34f2f-349">Sertifika İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="34f2f-349">Import certificate</span></span>
<span data-ttu-id="34f2f-350">Sertifika Alma Sihirbazı'nda:</span><span class="sxs-lookup"><span data-stu-id="34f2f-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="34f2f-351">Depolama konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-351">Select the store location.</span></span>
   
   * <span data-ttu-id="34f2f-352">Seçin **geçerli kullanıcı** geçerli kullanıcı altında çalışan işlemler hizmeti erişecek yalnızca</span><span class="sxs-lookup"><span data-stu-id="34f2f-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="34f2f-353">Seçin **yerel makine** bu bilgisayardaki diğer işlemlerin hizmet erişecekse</span><span class="sxs-lookup"><span data-stu-id="34f2f-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="34f2f-354">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-354">Click **Next**.</span></span>
3. <span data-ttu-id="34f2f-355">Bir dosyadan içeri aktarma, dosya yolunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="34f2f-356">İçeri aktarma, bir. PFX dosyası:</span><span class="sxs-lookup"><span data-stu-id="34f2f-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="34f2f-357">Özel anahtarın korunması için parolayı girin</span><span class="sxs-lookup"><span data-stu-id="34f2f-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="34f2f-358">İçeri aktarma seçenekleri seçin</span><span class="sxs-lookup"><span data-stu-id="34f2f-358">Select import options</span></span>
5. <span data-ttu-id="34f2f-359">"Yerine" sertifikaları aşağıdaki depolama alanına seçin</span><span class="sxs-lookup"><span data-stu-id="34f2f-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="34f2f-360">**Gözat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-360">Click **Browse**.</span></span>
7. <span data-ttu-id="34f2f-361">İstenen depolama alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-361">Select the desired store.</span></span>
8. <span data-ttu-id="34f2f-362">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="34f2f-363">Güvenilen kök sertifika yetkilisi deposunda seçildiyse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="34f2f-364">Tıklatın **Tamam** tüm iletişim Windows.</span><span class="sxs-lookup"><span data-stu-id="34f2f-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="34f2f-365">Sertifikayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="34f2f-365">Upload certificate</span></span>
<span data-ttu-id="34f2f-366">İçinde [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="34f2f-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="34f2f-367">Seçin **bulut hizmetlerini**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="34f2f-368">Bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-368">Select the cloud service.</span></span>
3. <span data-ttu-id="34f2f-369">Üst menüsünde **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="34f2f-370">Alt çubuğunda **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="34f2f-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="34f2f-371">Sertifika dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-371">Select the certificate file.</span></span>
6. <span data-ttu-id="34f2f-372">Bu doğruysa bir. PFX dosyası, özel anahtarı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="34f2f-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="34f2f-373">Tamamlandığında, sertifika parmak izini listede yeni girdiyi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="34f2f-374">Diğer güvenlik konuları</span><span class="sxs-lookup"><span data-stu-id="34f2f-374">Other security considerations</span></span>
<span data-ttu-id="34f2f-375">HTTPS uç noktası kullanıldığında, bu belgede açıklanan SSL ayarları hizmet ve istemcileri arasındaki iletişimi şifrelemek.</span><span class="sxs-lookup"><span data-stu-id="34f2f-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="34f2f-376">Bu veritabanı erişimi için kimlik bilgilerini bu yana önemlidir ve iletişime büyük olasılıkla diğer hassas bilgiler yer alır.</span><span class="sxs-lookup"><span data-stu-id="34f2f-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="34f2f-377">Ancak, hizmeti kimlik bilgileri, kendi iç Microsoft Azure aboneliğiniz meta veri depolama alanı için sağlanan Microsoft Azure SQL veritabanı tablolarında dahil olmak üzere, iç durum devam ederse unutmayın.</span><span class="sxs-lookup"><span data-stu-id="34f2f-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="34f2f-378">Bu veritabanı aşağıdaki ayarı hizmet yapılandırma dosyanızdaki bir parçası olarak tanımlandı (. CSCFG dosyası):</span><span class="sxs-lookup"><span data-stu-id="34f2f-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="34f2f-379">Bu veritabanında depolanan kimlik bilgileri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="34f2f-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="34f2f-380">Ancak, en iyi uygulama, hizmet dağıtımlarınız web ve çalışan rolleri güncel tutulması ve güvenli olarak her ikisi de meta veri veritabanı ve şifreleme ve şifre çözme depolanan kimlik bilgileri için kullanılan sertifikanın erişim içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="34f2f-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

