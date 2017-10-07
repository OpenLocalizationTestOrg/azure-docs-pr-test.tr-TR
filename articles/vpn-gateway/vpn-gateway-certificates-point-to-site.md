---
title: "Oluştur ve noktası Site için sertifikalar verme: PowerShell: Azure | Microsoft Docs"
description: "Windows 10'PowerShell kullanarak istemci sertifikalarını oluşturmak ve hello ortak anahtarını dışarı aktarmak veya bu makalede adımları toocreate otomatik olarak imzalanan sertifikayı içerir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="34d9d-103">Oluşturma ve PowerShell kullanarak Windows 10 noktadan siteye bağlantıları için sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="34d9d-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="34d9d-104">Noktadan siteye bağlantılar, sertifikalar tooauthenticate kullanır.</span><span class="sxs-lookup"><span data-stu-id="34d9d-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="34d9d-105">Bu makalede Windows 10'PowerShell kullanarak istemci sertifikalarını oluşturmak ve nasıl toocreate otomatik olarak imzalanan bir kök sertifika gösterir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="34d9d-106">Nasıl tooupload kök sertifikaları, aşağıdaki hello hello ' yapılandırma noktası siteye ' makalelerinden birini seçin listeler gibi noktadan siteye yapılandırma adımları için istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="34d9d-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="34d9d-107">Otomatik olarak imzalanan sertifikalar - PowerShell oluşturma</span><span class="sxs-lookup"><span data-stu-id="34d9d-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="34d9d-108">Otomatik olarak imzalanan sertifikalar - MakeCert oluşturma</span><span class="sxs-lookup"><span data-stu-id="34d9d-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="34d9d-109">Noktası-Site - Resource Manager - Azure portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="34d9d-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="34d9d-110">Noktadan siteye - Resource Manager - PowerShell yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34d9d-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="34d9d-111">Noktası-Site - Classic - Azure portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="34d9d-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="34d9d-112">Bu makalede Windows 10 çalıştıran bir bilgisayarda hello adımları gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="34d9d-113">Merhaba PowerShell cmdlet'leri toogenerate sertifikalar kullanmak hello Windows 10 işletim sisteminin bir parçası olan ve diğer Windows sürümlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="34d9d-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="34d9d-114">Merhaba Windows 10, yalnızca gerekli toogenerate hello sertifikaları bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="34d9d-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="34d9d-115">Merhaba sertifikaları oluşturduktan sonra bunları karşıya yükleyebilir veya tüm desteklenen istemci işletim sistemine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="34d9d-116">Erişim tooa Windows 10 bilgisayarı yoksa kullanabileceğiniz [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate sertifikalar.</span><span class="sxs-lookup"><span data-stu-id="34d9d-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="34d9d-117">Merhaba her iki yöntemi kullanarak oluşturduğunuz sertifikalar herhangi yüklenebilir [desteklenen](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) istemci işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="34d9d-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="34d9d-118"><a name="rootcert"></a>Otomatik olarak imzalanan sertifika oluştur</span><span class="sxs-lookup"><span data-stu-id="34d9d-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="34d9d-119">Merhaba yeni SelfSignedCertificate cmdlet toocreate otomatik olarak imzalanan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="34d9d-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="34d9d-120">Ek parametre bilgi için bkz: [yeni SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="34d9d-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="34d9d-121">Windows 10 çalıştıran bir bilgisayarda, yükseltilmiş ayrıcalıklarla bir Windows PowerShell konsolu açın.</span><span class="sxs-lookup"><span data-stu-id="34d9d-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="34d9d-122">Aşağıdaki örnek toocreate hello otomatik olarak imzalanan sertifika hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="34d9d-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="34d9d-123">Merhaba aşağıdaki örnek 'otomatik 'Sertifikalar-Geçerli User\Personal\Certificates' yüklü P2SRootCert' adlı otomatik olarak imzalanan bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34d9d-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="34d9d-124">Açarak hello sertifikayı görüntüleyebilirsiniz *certmgr.msc*, veya *kullanıcı sertifikaları yönetme*.</span><span class="sxs-lookup"><span data-stu-id="34d9d-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="34d9d-125"><a name="cer"></a>Dışarı aktarma hello ortak anahtarı (.cer)</span><span class="sxs-lookup"><span data-stu-id="34d9d-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="34d9d-126">Merhaba exported.cer dosyası karşıya yüklenen tooAzure olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="34d9d-127">Yönergeler için bkz: [noktadan siteye bağlantı yapılandırma](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="34d9d-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="34d9d-128">bir ek güvenilen kök sertifika tooadd [Bu bölümde](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello makalenin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="34d9d-129">Merhaba otomatik olarak imzalanan sertifika ve ortak anahtar toostore vermek, (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="34d9d-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="34d9d-130">Tooexport hello otomatik olarak imzalanan kök sertifikası ve güvenli bir şekilde depolamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34d9d-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="34d9d-131">Varsa olmadan, yapabilir daha sonra başka bir bilgisayara yükleyin ve daha fazla istemci sertifikalarını oluşturmak veya başka bir .cer dosyasına dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="34d9d-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="34d9d-132">tooexport hello .pfx, select hello kök sertifikası ve kullanım aynı adımları açıklandığı gibi hello olarak kök sertifikayı otomatik olarak imzalanan [bir istemci sertifikası verme](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="34d9d-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="34d9d-133"><a name="clientcert"></a>İstemci sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="34d9d-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="34d9d-134">Tooa bağlanan her istemci bilgisayar noktadan siteye kullanarak VNet yüklü bir istemci sertifikası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="34d9d-135">Ardından dışa hello otomatik olarak imzalanan kök sertifikasından bir istemci sertifikasını oluşturmak ve hello istemci sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="34d9d-136">Merhaba istemci sertifikası yüklü değilse, kimlik doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="34d9d-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="34d9d-137">Merhaba aşağıdaki adımlar, otomatik olarak imzalanan kök sertifikasından bir istemci sertifikası oluşturma aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="34d9d-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="34d9d-138">Merhaba birden çok istemci sertifikaları verebilir aynı kök sertifikaya.</span><span class="sxs-lookup"><span data-stu-id="34d9d-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="34d9d-139">Merhaba adımları kullanarak istemci sertifikalarını oluşturmak, hello istemci sertifikasını otomatik olarak hello bilgisayarda toogenerate hello sertifika kullanılan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="34d9d-140">Tooinstall başka bir istemci bilgisayarında bir istemci sertifikası istiyorsanız hello sertifika verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34d9d-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="34d9d-141">Merhaba örnekler hello yeni SelfSignedCertificate cmdlet toogenerate bir yıl içinde süresi dolar bir istemci sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="34d9d-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="34d9d-142">Merhaba istemci sertifikası, farklı sona erme değeri ayarlanırken gibi ek parametre bilgi için bkz [yeni SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="34d9d-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="34d9d-143">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="34d9d-143">Example 1</span></span>

<span data-ttu-id="34d9d-144">Bu örnekte '$cert' hello önceki bölümde değişkeninden bildirilen hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="34d9d-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="34d9d-145">Otomatik olarak imzalanan sertifika Merhaba, veya yeni bir PowerShell konsol oturumda oluşturarak ek istemci sertifikaları sonra hello PowerShell konsolunu kapattıysanız, hello adımlarda kullanmak [örnek 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="34d9d-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="34d9d-146">Değiştirme ve bir istemci sertifikası hello örnek toogenerate çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34d9d-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="34d9d-147">Değişiklik yapmadan aşağıdaki örneğine hello çalıştırırsanız, hello 'P2SChildCert' adlı bir istemci sertifikası sonucudur.</span><span class="sxs-lookup"><span data-stu-id="34d9d-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="34d9d-148">Tooname hello alt sertifika başka bir konuda istiyorsanız hello CN değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="34d9d-149">Bu örnek çalıştırırken Hello TextExtension değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="34d9d-150">oluşturduğunuz hello istemci sertifikası, bilgisayarınızda 'Sertifikalar - Geçerli User\Personal\Certificates' otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="34d9d-151"><a name="ex2"></a>Örnek 2</span><span class="sxs-lookup"><span data-stu-id="34d9d-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="34d9d-152">Ek istemci sertifikaları oluşturma veya olan kullanmıyorsa hello aynı PowerShell oturumunda, otomatik olarak imzalanan sertifika, aşağıdaki adımları kullanın hello toocreate kullanılan:</span><span class="sxs-lookup"><span data-stu-id="34d9d-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="34d9d-153">Merhaba bilgisayarda yüklü hello otomatik olarak imzalanan kök sertifikayı belirleyin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="34d9d-154">Bu cmdlet, bilgisayarınızda yüklü sertifikaların listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="34d9d-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="34d9d-155">Liste, sonra bulunan sonraki tooit tooa metin Kopyala hello parmak izi döndürülen hello Hello konu adını bulun dosya.</span><span class="sxs-lookup"><span data-stu-id="34d9d-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="34d9d-156">Aşağıdaki örnek hello, iki sertifika vardır.</span><span class="sxs-lookup"><span data-stu-id="34d9d-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="34d9d-157">Merhaba CN adı toogenerate alt sertifika istediğiniz hello otomatik olarak imzalanan sertifika hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="34d9d-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="34d9d-158">Bu durumda, 'P2SRootCert'.</span><span class="sxs-lookup"><span data-stu-id="34d9d-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="34d9d-159">Merhaba parmak hello önceki adımdaki kullanarak hello kök sertifikası için bir değişken bildirin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="34d9d-160">Parmak İZİ toogenerate alt sertifika istediğiniz hello kök sertifikası hello parmak iziyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="34d9d-161">Örneğin, hello parmak hello önceki adımda P2SRootCert için kullanarak, hello değişkeni şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="34d9d-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="34d9d-162">Değiştirme ve bir istemci sertifikası hello örnek toogenerate çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34d9d-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="34d9d-163">Değişiklik yapmadan aşağıdaki örneğine hello çalıştırırsanız, hello 'P2SChildCert' adlı bir istemci sertifikası sonucudur.</span><span class="sxs-lookup"><span data-stu-id="34d9d-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="34d9d-164">Tooname hello alt sertifika başka bir konuda istiyorsanız hello CN değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="34d9d-165">Bu örnek çalıştırırken Hello TextExtension değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="34d9d-166">oluşturduğunuz hello istemci sertifikası, bilgisayarınızda 'Sertifikalar - Geçerli User\Personal\Certificates' otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34d9d-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="34d9d-167"><a name="clientexport"></a>Bir istemci sertifikasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="34d9d-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="34d9d-168"><a name="install"></a>Dışarı aktarılan istemci sertifikası yükleme</span><span class="sxs-lookup"><span data-stu-id="34d9d-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="34d9d-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34d9d-169">Next steps</span></span>

<span data-ttu-id="34d9d-170">Noktası Site yapılandırmanızı ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="34d9d-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="34d9d-171">İçin **Resource Manager** dağıtım modeli adımları bkz [bir noktadan siteye bağlantı tooa VNet yapılandırma](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34d9d-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="34d9d-172">İçin **Klasik** dağıtım modeli adımları bkz [bir noktadan siteye VPN bağlantısı tooa VNet (Klasik) yapılandırma](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34d9d-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
