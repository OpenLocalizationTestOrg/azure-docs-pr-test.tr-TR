---
title: "Oluştur ve noktası Site için sertifikalar verme: PowerShell: Azure | Microsoft Docs"
description: "Bu makale, otomatik olarak imzalanan sertifika oluşturmak, ortak anahtarını dışarı aktarmak ve Windows 10'PowerShell kullanarak istemci sertifikalarını oluşturmak için adımlar içerir."
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
ms.openlocfilehash: f96b9b212b9322d0677e49ff95184d0feccca2df
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="0e96d-103">Oluşturma ve PowerShell kullanarak Windows 10 noktadan siteye bağlantıları için sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="0e96d-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="0e96d-104">Noktadan siteye bağlantılar, kimlik doğrulaması için sertifikaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e96d-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="0e96d-105">Bu makalede bir otomatik olarak imzalanan sertifika oluşturmak ve Windows 10'PowerShell kullanarak istemci sertifikalarını oluşturmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-105">This article shows you how to create a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="0e96d-106">Kök sertifikalarını yüklemek nasıl gibi noktadan siteye yapılandırma adımlarını arıyorsanız ' yapılandırma noktası siteye ' makaleleri birini aşağıdaki listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="0e96d-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e96d-107">Otomatik olarak imzalanan sertifikalar - PowerShell oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e96d-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="0e96d-108">Otomatik olarak imzalanan sertifikalar - MakeCert oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e96d-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="0e96d-109">Noktası-Site - Resource Manager - Azure portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0e96d-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="0e96d-110">Noktadan siteye - Resource Manager - PowerShell yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e96d-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="0e96d-111">Noktası-Site - Classic - Azure portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0e96d-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="0e96d-112">Windows 10 çalıştıran bir bilgisayarda bu makaledeki adımları uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-112">You must perform the steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="0e96d-113">Sertifikalarını oluşturmak için kullandığınız PowerShell cmdlet'leri Windows 10 işletim sisteminin bir parçası olan ve diğer Windows sürümlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="0e96d-113">The PowerShell cmdlets that you use to generate certificates are part of the Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="0e96d-114">Windows 10 bilgisayarını, yalnızca sertifikalarını oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-114">The Windows 10 computer is only needed to generate the certificates.</span></span> <span data-ttu-id="0e96d-115">Sertifikaları oluşturduktan sonra bunları karşıya yükleyebilir veya tüm desteklenen istemci işletim sistemine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-115">Once the certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="0e96d-116">Bir Windows 10 bilgisayara erişiminiz yoksa kullanabileceğiniz [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) sertifikalarını oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0e96d-116">If you do not have access to a Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) to generate certificates.</span></span> <span data-ttu-id="0e96d-117">Her iki yöntemi kullanarak oluşturduğunuz sertifikalar herhangi yüklenebilir [desteklenen](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) istemci işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="0e96d-117">The certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="0e96d-118"><a name="rootcert"></a>Otomatik olarak imzalanan sertifika oluştur</span><span class="sxs-lookup"><span data-stu-id="0e96d-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="0e96d-119">Bir otomatik olarak imzalanan sertifika oluşturmak için New-SelfSignedCertificate cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-119">Use the New-SelfSignedCertificate cmdlet to create a self-signed root certificate.</span></span> <span data-ttu-id="0e96d-120">Ek parametre bilgi için bkz: [yeni SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="0e96d-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="0e96d-121">Windows 10 çalıştıran bir bilgisayarda, yükseltilmiş ayrıcalıklarla bir Windows PowerShell konsolu açın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="0e96d-122">Otomatik olarak imzalanan sertifika oluşturmak için aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-122">Use the following example to create the self-signed root certificate.</span></span> <span data-ttu-id="0e96d-123">Aşağıdaki örnek, '' Sertifikalar-Geçerli User\Personal\Certificates' otomatik olarak yüklenen P2SRootCert' adlı otomatik olarak imzalanan bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e96d-123">The following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="0e96d-124">Sertifika açarak görüntüleyebileceğiniz *certmgr.msc*, veya *kullanıcı sertifikaları yönetme*.</span><span class="sxs-lookup"><span data-stu-id="0e96d-124">You can view the certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="0e96d-125"><a name="cer"></a>Ortak anahtarı (.cer) aktarın</span><span class="sxs-lookup"><span data-stu-id="0e96d-125"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="0e96d-126">Exported.cer dosyasını Azure'a yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-126">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="0e96d-127">Yönergeler için bkz: [noktadan siteye bağlantı yapılandırma](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="0e96d-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="0e96d-128">Bir ek güvenilen kök sertifika eklemek için [Bu bölümde](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) makalenin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-128">To add an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of the article.</span></span>

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a><span data-ttu-id="0e96d-129">(İsteğe bağlı) depolamak için ortak anahtar ve otomatik olarak imzalanan kök sertifikasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="0e96d-129">Export the self-signed root certificate and public key to store it (optional)</span></span>

<span data-ttu-id="0e96d-130">Otomatik olarak imzalanan kök sertifikasını dışarı aktarma ve güvenli bir şekilde depolamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e96d-130">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="0e96d-131">Varsa olmadan, yapabilir daha sonra başka bir bilgisayara yükleyin ve daha fazla istemci sertifikalarını oluşturmak veya başka bir .cer dosyasına dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="0e96d-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="0e96d-132">Bir .pfx otomatik olarak imzalanan kök sertifikasını dışarı aktarmak için kök sertifikasını seçin ve açıklandığı gibi aynı adımları kullanın [bir istemci sertifikası verme](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="0e96d-132">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="0e96d-133"><a name="clientcert"></a>İstemci sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e96d-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="0e96d-134">Noktadan Siteye bağlantı kullanarak bir sanal ağa bağlanan her istemci bilgisayarda bir istemci sertifikası yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0e96d-134">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="0e96d-135">Ardından dışa otomatik olarak imzalanan kök sertifikasından bir istemci sertifikasını oluşturmak ve istemci sertifikasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-135">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="0e96d-136">İstemci sertifikası yüklü değilse, kimlik doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0e96d-136">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="0e96d-137">Aşağıdaki adımlarda, otomatik olarak imzalanan kök sertifikasından bir istemci sertifikası oluşturma aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="0e96d-137">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="0e96d-138">Birden çok istemci sertifikaları aynı kök sertifikası oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-138">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="0e96d-139">Aşağıdaki adımları kullanarak istemci sertifikalarını oluşturmak, istemci sertifikasının, sertifikayı oluşturmak için kullanılan bilgisayarda otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-139">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="0e96d-140">Bir istemci sertifikası başka bir istemci bilgisayara yüklemek istiyorsanız, sertifikayı dışa aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e96d-140">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>

<span data-ttu-id="0e96d-141">Örnekler, bir yıl içinde süresi dolar bir istemci sertifikasını oluşturmak için yeni SelfSignedCertificate cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-141">The examples use the New-SelfSignedCertificate cmdlet to generate a client certificate that expires in one year.</span></span> <span data-ttu-id="0e96d-142">İstemci sertifikası için farklı süre sonu değeri ayarlama gibi ek parametre bilgi için bkz [yeni SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="0e96d-142">For additional parameter information, such as setting a different expiration value for the client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="0e96d-143">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="0e96d-143">Example 1</span></span>

<span data-ttu-id="0e96d-144">Bu örnek önceki bölümden bildirilen '$cert' değişkeni kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e96d-144">This example uses the declared '$cert' variable from the previous section.</span></span> <span data-ttu-id="0e96d-145">PowerShell Konsolu otomatik olarak imzalanan sertifika oluşturduktan sonra kapalı veya yeni bir PowerShell konsol oturumda ek istemci sertifikaları oluşturma, içindeki adımları kullanın [örnek 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="0e96d-145">If you closed the PowerShell console after creating the self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use the steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="0e96d-146">Değiştirme ve bir istemci sertifikasını oluşturmak için örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-146">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="0e96d-147">Değişiklik yapmadan aşağıdaki örneği çalıştırırsanız, 'P2SChildCert' adlı bir istemci sertifikası sonucudur.</span><span class="sxs-lookup"><span data-stu-id="0e96d-147">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="0e96d-148">Alt sertifika başka bir ad vermek istiyorsanız, CN değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-148">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="0e96d-149">Bu örnek çalıştırırken TextExtension değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-149">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="0e96d-150">Oluşturduğunuz istemci sertifikası, bilgisayarınızda 'Sertifikalar - Geçerli User\Personal\Certificates' otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-150">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="0e96d-151"><a name="ex2"></a>Örnek 2</span><span class="sxs-lookup"><span data-stu-id="0e96d-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="0e96d-152">Ek istemci sertifikalarını oluşturmakta ya da otomatik olarak imzalanan sertifika oluşturmak için kullanılan aynı PowerShell oturumunda kullanmıyorsanız, aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e96d-152">If you are creating additional client certificates, or are not using the same PowerShell session that you used to create your self-signed root certificate, use the following steps:</span></span>

1. <span data-ttu-id="0e96d-153">Bilgisayarda yüklü otomatik olarak imzalanan kök sertifikayı belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-153">Identify the self-signed root certificate that is installed on the computer.</span></span> <span data-ttu-id="0e96d-154">Bu cmdlet, bilgisayarınızda yüklü sertifikaların listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0e96d-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="0e96d-155">Konu adı döndürülen listesinden bulun ve sonra onu yanında bir metin dosyasına bulunur parmak izini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-155">Locate the subject name from the returned list, then copy the thumbprint that is located next to it to a text file.</span></span> <span data-ttu-id="0e96d-156">Aşağıdaki örnekte, iki sertifika vardır.</span><span class="sxs-lookup"><span data-stu-id="0e96d-156">In the following example, there are two certificates.</span></span> <span data-ttu-id="0e96d-157">CN adı bir alt sertifika oluşturmak istediğiniz otomatik olarak imzalanan sertifika adıdır.</span><span class="sxs-lookup"><span data-stu-id="0e96d-157">The CN name is the name of the self-signed root certificate from which you want to generate a child certificate.</span></span> <span data-ttu-id="0e96d-158">Bu durumda, 'P2SRootCert'.</span><span class="sxs-lookup"><span data-stu-id="0e96d-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="0e96d-159">Önceki adımdan parmak kullanarak kök sertifikası için bir değişken bildirin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-159">Declare a variable for the root certificate using the thumbprint from the previous step.</span></span> <span data-ttu-id="0e96d-160">Parmak İZİ alt sertifika oluşturmak istediğiniz kök sertifika parmak iziyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-160">Replace THUMBPRINT with the thumbprint of the root certificate from which you want to generate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="0e96d-161">Örneğin, önceki adımda P2SRootCert için parmak izini kullanarak değişkeni şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="0e96d-161">For example, using the thumbprint for P2SRootCert in the previous step, the variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="0e96d-162">Değiştirme ve bir istemci sertifikasını oluşturmak için örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e96d-162">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="0e96d-163">Değişiklik yapmadan aşağıdaki örneği çalıştırırsanız, 'P2SChildCert' adlı bir istemci sertifikası sonucudur.</span><span class="sxs-lookup"><span data-stu-id="0e96d-163">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="0e96d-164">Alt sertifika başka bir ad vermek istiyorsanız, CN değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-164">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="0e96d-165">Bu örnek çalıştırırken TextExtension değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-165">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="0e96d-166">Oluşturduğunuz istemci sertifikası, bilgisayarınızda 'Sertifikalar - Geçerli User\Personal\Certificates' otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0e96d-166">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="0e96d-167"><a name="clientexport"></a>Bir istemci sertifikasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="0e96d-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="0e96d-168"><a name="install"></a>Dışarı aktarılan istemci sertifikası yükleme</span><span class="sxs-lookup"><span data-stu-id="0e96d-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0e96d-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e96d-169">Next steps</span></span>

<span data-ttu-id="0e96d-170">Noktası Site yapılandırmanızı ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="0e96d-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="0e96d-171">İçin **Resource Manager** dağıtım modeli adımları bkz [bir sanal ağa noktadan siteye bağlantı yapılandırma](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0e96d-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="0e96d-172">İçin **Klasik** dağıtım modeli adımları bkz [bir sanal ağ (Klasik) bir noktadan siteye VPN bağlantısı yapılandırma](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0e96d-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>