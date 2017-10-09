---
title: "PowerShell kullanarak bağlama aaaSSL sertifikaları"
description: "PowerShell kullanarak tooyour web uygulaması nasıl toobind SSL sertifikaları hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="f054d-103">PowerShell kullanarak azure uygulama hizmeti SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="f054d-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="f054d-104">Microsoft Azure PowerShell sürüm 1.1.0 yeni bir cmdlet eklenen Hello sürümle birlikte, Web uygulaması varolan hello kullanıcı hello özelliği toobind mevcut veya yeni SSL sertifikalarını tooan verirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f054d-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="f054d-105">Azure Kaynak Yöneticisi'ni kullanma hakkında toolearn tabanlı Azure PowerShell cmdlet'leri toomanage Web Apps onay [Azure Web uygulaması için Azure Resource Manager tabanlı PowerShell komutları](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f054d-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="f054d-106">Karşıya yükleme ve yeni bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="f054d-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="f054d-107">Senaryo: hello kullanıcı toobind bir SSL sertifikası tooone kendi web uygulamalarının ister.</span><span class="sxs-lookup"><span data-stu-id="f054d-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="f054d-108">Hello web uygulaması, hello web uygulaması adı, hello sertifika .pfx dosyası yolu hello kullanıcı makinede içerir hello kaynak grubu adı bilerek hello hello sertifikanın parolasını ve özel ana bilgisayar adını Merhaba, aşağıdaki PowerShell komut toocreate hello kullanıyoruz, SSL bağlama:</span><span class="sxs-lookup"><span data-stu-id="f054d-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="f054d-109">Bir SSL bağlaması tooa web uygulaması eklemeden önce önceden yapılandırılmış bir ana bilgisayar adı (özel etki alanı) olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f054d-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="f054d-110">Merhaba ana bilgisayar adı yapılandırılmamış sonra bir hata iletisiyle karşılaşırsınız 'hostname' yeni AzureRmWebAppSSLBinding çalıştırılırken yok.</span><span class="sxs-lookup"><span data-stu-id="f054d-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="f054d-111">Doğrudan hello portalı veya Azure PowerShell kullanarak bir ana bilgisayar adı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f054d-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="f054d-112">Merhaba aşağıdaki PowerShell parçacığını tooconfigure hello hostname yeni AzureRmWebAppSSLBinding çalıştırmadan önce olabilir.</span><span class="sxs-lookup"><span data-stu-id="f054d-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="f054d-113">Set-AzureRmWebApp cmdlet'i hello toounderstand hello ana bilgisayar adları hello web uygulamasının üzerine yazar önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f054d-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="f054d-114">Bu nedenle PowerShell parçacığı yukarıda hello toohello varolan hello web uygulaması için hello ana bilgisayar adları listesi ekleme.</span><span class="sxs-lookup"><span data-stu-id="f054d-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="f054d-115">Karşıya yükleme ve bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="f054d-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="f054d-116">Senaryo: hello kullanıcı toobind kendi web uygulamaları, daha önce yüklenen bir SSL sertifikası tooone ister.</span><span class="sxs-lookup"><span data-stu-id="f054d-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="f054d-117">Biz hello listesini sertifikaları zaten karşıya yüklenen tooa belirli bir kaynak grubu hello aşağıdaki komutu kullanarak elde edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f054d-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="f054d-118">Yerel tooa belirli konum ve kaynak grubu hello sertifikalar, hello kullanıcı toore-karşıya yükleme hello sertifikasına ihtiyacınız farklı bir konumda yapılandırılmış hello web uygulaması ise ve kaynak grubuna diğer sertifikası gerekli, hello dikkat edin</span><span class="sxs-lookup"><span data-stu-id="f054d-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="f054d-119">Hello web uygulamasını içeren hello kaynak grubu adı bilerek, web uygulaması adı Merhaba, sertifika parmak izi hello ve özel ana bilgisayar adını Merhaba, aşağıdaki PowerShell komut toocreate hello bu SSL bağlama kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f054d-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="f054d-120">Mevcut bir SSL bağlaması silme</span><span class="sxs-lookup"><span data-stu-id="f054d-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="f054d-121">Senaryo: hello kullanıcı toodelete varolan SSL bağlaması ister.</span><span class="sxs-lookup"><span data-stu-id="f054d-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="f054d-122">Merhaba web uygulamasını içeren hello kaynak grubu adı bilerek web uygulaması adı hello ve özel ana bilgisayar adını Merhaba, aşağıdaki PowerShell komut tooremove hello bu SSL bağlama kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f054d-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="f054d-123">Merhaba SSL bağlaması kaldırdıysanız, hello son Not Bu konumda bu sertifikayı kullanarak bağlama varsayılan hello sertifikası tarafından silinecek, hello kullanıcı tookeep hello sertifika istiyorsanız kendisinin hello DeleteCertificate seçeneği tookeep hello sertifikayı kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f054d-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="f054d-124">Başvurular</span><span class="sxs-lookup"><span data-stu-id="f054d-124">References</span></span>
* [<span data-ttu-id="f054d-125">Azure Resource Manager PowerShell komutlarını Azure Web uygulaması için temel</span><span class="sxs-lookup"><span data-stu-id="f054d-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="f054d-126">Giriş tooApp hizmeti ortamı</span><span class="sxs-lookup"><span data-stu-id="f054d-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="f054d-127">Azure PowerShell’i Azure Resource Manager ile kullanma</span><span class="sxs-lookup"><span data-stu-id="f054d-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

