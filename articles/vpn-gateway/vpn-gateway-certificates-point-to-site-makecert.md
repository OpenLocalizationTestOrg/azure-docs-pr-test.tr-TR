---
title: "Oluştur ve noktası Site için sertifikalar verme: MakeCert: Azure | Microsoft Docs"
description: "MakeCert kullanarak istemci sertifikalarını oluşturmak ve hello ortak anahtarını dışarı aktarmak veya bu makalede adımları toocreate otomatik olarak imzalanan sertifikayı içerir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Oluştur ve noktadan siteye bağlantıları MakeCert kullanarak için sertifikaları verme

Noktadan siteye bağlantılar, sertifikalar tooauthenticate kullanır. Bu makalede MakeCert kullanarak istemci sertifikalarını oluşturmak ve nasıl toocreate otomatik olarak imzalanan bir kök sertifika gösterir. Nasıl tooupload kök sertifikaları, aşağıdaki hello hello ' yapılandırma noktası siteye ' makalelerinden birini seçin listeler gibi noktadan siteye yapılandırma adımları için istiyorsanız:

> [!div class="op_single_selector"]
> * [Otomatik olarak imzalanan sertifikalar - PowerShell oluşturma](vpn-gateway-certificates-point-to-site.md)
> * [Otomatik olarak imzalanan sertifikalar - MakeCert oluşturma](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Noktası-Site - Resource Manager - Azure portalında yapılandırın](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Noktadan siteye - Resource Manager - PowerShell yapılandırma](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Noktası-Site - Classic - Azure portalında yapılandırın](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Merhaba kullanmanızı öneririz sırada [Windows 10 PowerShell adımları](vpn-gateway-certificates-point-to-site.md) toocreate, sertifikalarınızı bu MakeCert yönergeleri isteğe bağlı bir yöntem olarak sağlıyoruz. Her iki yöntemi kullanarak oluşturduğunuz hello sertifikaları yüklenebilir [herhangi bir desteklenen istemci işletim sistemi](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). Bununla birlikte, MakeCert sınırlaması aşağıdaki hello vardır:

* MakeCert kullanım dışıdır. Başka bir deyişle, bu aracı herhangi bir noktada kaldırılamadı. MakeCert artık kullanılabilir olduğunda zaten MakeCert kullanılarak oluşturulan herhangi bir sertifika etkilenmeyecek. MakeCert yalnızca kullanılan toogenerate hello sertifikaları doğrulama mekanizması olarak değil.

## <a name="rootcert"></a>Otomatik olarak imzalanan sertifika oluştur

Aşağıdaki adımları hello nasıl toocreate otomatik olarak imzalanan bir sertifika MakeCert kullanarak gösterir. Bu adımları dağıtım modeli özel değildir. Bunlar, Resource Manager ve klasik için geçerli olur.

1. İndirme ve yükleme [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Yükleme tamamlandıktan sonra bu yol altındaki hello makecert.exe yardımcı programını genellikle bulabilirsiniz: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'. Rağmen yüklü tooanother konumu olduğunu mümkündür. Yönetici olarak bir komut istemi açın ve hello MakeCert yardımcı programı toohello konumuna gidin. Aşağıdaki örnek, hello uygun konumu ayarlama hello kullanabilirsiniz:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Oluşturun ve bilgisayarınızda hello kişisel sertifika deposunda bir sertifika yükleyin. Merhaba aşağıdaki örnek karşılık gelen oluşturur *.cer* P2S yapılandırırken tooAzure karşıya dosya. 'P2SRootCert' ve 'P2SRootCert.cer' hello sertifikası toouse istediğiniz hello adla değiştirin. Merhaba sertifika 'Sertifikalarınızı içinde - geçerli User\Personal\Certificates' bulunur.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Dışarı aktarma hello ortak anahtarı (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Merhaba exported.cer dosyası karşıya yüklenen tooAzure olması gerekir. Yönergeler için bkz: [noktadan siteye bağlantı yapılandırma](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd ek güvenilen kök sertifika bkz [Bu bölümde](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) hello makalenin.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Merhaba otomatik olarak imzalanan sertifika ve özel anahtar toostore vermek, (isteğe bağlı)

Tooexport hello otomatik olarak imzalanan kök sertifikası ve güvenli bir şekilde depolamak isteyebilirsiniz. Varsa olmadan, yapabilir daha sonra başka bir bilgisayara yükleyin ve daha fazla istemci sertifikalarını oluşturmak veya başka bir .cer dosyasına dışarı aktarma. tooexport hello .pfx, select hello kök sertifikası ve kullanım aynı adımları açıklandığı gibi hello olarak kök sertifikayı otomatik olarak imzalanan [bir istemci sertifikası verme](#clientexport).

## <a name="create-and-install-client-certificates"></a>Oluşturun ve istemci sertifikalarını yükleyin

Doğrudan hello istemci bilgisayarda otomatik olarak imzalanan sertifika hello yüklemeyin. Toogenerate hello otomatik olarak imzalanan sertifika bir istemci sertifikası gerekir. Sonra dışarı aktarma ve hello istemci sertifikası toohello istemci bilgisayara yükleyin. Aşağıdaki adımları hello dağıtım modeli özel değildir. Bunlar, Resource Manager ve klasik için geçerli olur.

### <a name="clientcert"></a>İstemci sertifikası oluşturma

Tooa bağlanan her istemci bilgisayar noktadan siteye kullanarak VNet yüklü bir istemci sertifikası olması gerekir. Ardından dışa hello otomatik olarak imzalanan kök sertifikasından bir istemci sertifikasını oluşturmak ve hello istemci sertifikası yükleyin. Merhaba istemci sertifikası yüklü değilse, kimlik doğrulaması başarısız olur. 

Merhaba aşağıdaki adımlar, otomatik olarak imzalanan kök sertifikasından bir istemci sertifikası oluşturma aracılığıyla yol. Merhaba birden çok istemci sertifikaları verebilir aynı kök sertifikaya. Merhaba adımları kullanarak istemci sertifikalarını oluşturmak, hello istemci sertifikasını otomatik olarak hello bilgisayarda toogenerate hello sertifika kullanılan yüklenir. Tooinstall başka bir istemci bilgisayarında bir istemci sertifikası istiyorsanız hello sertifika verebilirsiniz.
 
1. Merhaba üzerinde toocreate hello kullanılan aynı bilgisayara otomatik olarak imzalanan sertifikası, yönetici olarak bir komut istemi açın.
2. Değiştirme ve bir istemci sertifikası hello örnek toogenerate çalıştırın.
  * Değişiklik *"P2SRootCert"* hello istemci sertifika oluşturma hello otomatik olarak imzalanan kök toohello adı. Ne olursa olsun hello olduğu hello kök sertifikasının hello adı kullandığınızdan emin olun ' CN =' değer olan hello otomatik olarak imzalanan kök oluşturduğunuzda belirttiğiniz.
  * Değişiklik *P2SChildCert* toogenerate bir istemci sertifikası toobe istediğiniz toohello adı.

  Değişiklik yapmadan aşağıdaki örneğine hello çalıştırırsanız Merhaba, kişisel sertifika deposunda kök sertifikasının P2SRootCert oluşturulan P2SChildcert adlı bir istemci sertifikası sonucudur.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Bir istemci sertifikasını dışarı aktarma

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Dışarı aktarılan istemci sertifikası yükleme

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Noktası Site yapılandırmanızı ile devam edin. 

* İçin **Resource Manager** dağıtım modeli adımları bkz [bir noktadan siteye bağlantı tooa VNet yapılandırma](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* İçin **Klasik** dağıtım modeli adımları bkz [bir noktadan siteye VPN bağlantısı tooa VNet (Klasik) yapılandırma](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
