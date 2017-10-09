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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>PowerShell kullanarak azure uygulama hizmeti SSL sertifikası bağlama
Microsoft Azure PowerShell sürüm 1.1.0 yeni bir cmdlet eklenen Hello sürümle birlikte, Web uygulaması varolan hello kullanıcı hello özelliği toobind mevcut veya yeni SSL sertifikalarını tooan verirsiniz.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Azure Kaynak Yöneticisi'ni kullanma hakkında toolearn tabanlı Azure PowerShell cmdlet'leri toomanage Web Apps onay [Azure Web uygulaması için Azure Resource Manager tabanlı PowerShell komutları](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Karşıya yükleme ve yeni bir SSL sertifikası bağlama
Senaryo: hello kullanıcı toobind bir SSL sertifikası tooone kendi web uygulamalarının ister.

Hello web uygulaması, hello web uygulaması adı, hello sertifika .pfx dosyası yolu hello kullanıcı makinede içerir hello kaynak grubu adı bilerek hello hello sertifikanın parolasını ve özel ana bilgisayar adını Merhaba, aşağıdaki PowerShell komut toocreate hello kullanıyoruz, SSL bağlama:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Bir SSL bağlaması tooa web uygulaması eklemeden önce önceden yapılandırılmış bir ana bilgisayar adı (özel etki alanı) olması gerektiğini unutmayın. Merhaba ana bilgisayar adı yapılandırılmamış sonra bir hata iletisiyle karşılaşırsınız 'hostname' yeni AzureRmWebAppSSLBinding çalıştırılırken yok. Doğrudan hello portalı veya Azure PowerShell kullanarak bir ana bilgisayar adı ekleyebilirsiniz. Merhaba aşağıdaki PowerShell parçacığını tooconfigure hello hostname yeni AzureRmWebAppSSLBinding çalıştırmadan önce olabilir.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Set-AzureRmWebApp cmdlet'i hello toounderstand hello ana bilgisayar adları hello web uygulamasının üzerine yazar önemlidir. Bu nedenle PowerShell parçacığı yukarıda hello toohello varolan hello web uygulaması için hello ana bilgisayar adları listesi ekleme.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Karşıya yükleme ve bir SSL sertifikası bağlama
Senaryo: hello kullanıcı toobind kendi web uygulamaları, daha önce yüklenen bir SSL sertifikası tooone ister.

Biz hello listesini sertifikaları zaten karşıya yüklenen tooa belirli bir kaynak grubu hello aşağıdaki komutu kullanarak elde edebilirsiniz

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Yerel tooa belirli konum ve kaynak grubu hello sertifikalar, hello kullanıcı toore-karşıya yükleme hello sertifikasına ihtiyacınız farklı bir konumda yapılandırılmış hello web uygulaması ise ve kaynak grubuna diğer sertifikası gerekli, hello dikkat edin 

Hello web uygulamasını içeren hello kaynak grubu adı bilerek, web uygulaması adı Merhaba, sertifika parmak izi hello ve özel ana bilgisayar adını Merhaba, aşağıdaki PowerShell komut toocreate hello bu SSL bağlama kullanabilirsiniz:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Mevcut bir SSL bağlaması silme
Senaryo: hello kullanıcı toodelete varolan SSL bağlaması ister.

Merhaba web uygulamasını içeren hello kaynak grubu adı bilerek web uygulaması adı hello ve özel ana bilgisayar adını Merhaba, aşağıdaki PowerShell komut tooremove hello bu SSL bağlama kullanabilirsiniz:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Merhaba SSL bağlaması kaldırdıysanız, hello son Not Bu konumda bu sertifikayı kullanarak bağlama varsayılan hello sertifikası tarafından silinecek, hello kullanıcı tookeep hello sertifika istiyorsanız kendisinin hello DeleteCertificate seçeneği tookeep hello sertifikayı kullanabilirsiniz

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Başvurular
* [Azure Resource Manager PowerShell komutlarını Azure Web uygulaması için temel](app-service-web-app-azure-resource-manager-powershell.md)
* [Giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)
* [Azure PowerShell’i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md)

