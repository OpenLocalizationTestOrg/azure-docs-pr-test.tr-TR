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
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Oluşturma ve PowerShell kullanarak Windows 10 noktadan siteye bağlantıları için sertifikaları verme

Noktadan siteye bağlantılar, sertifikalar tooauthenticate kullanır. Bu makalede Windows 10'PowerShell kullanarak istemci sertifikalarını oluşturmak ve nasıl toocreate otomatik olarak imzalanan bir kök sertifika gösterir. Nasıl tooupload kök sertifikaları, aşağıdaki hello hello ' yapılandırma noktası siteye ' makalelerinden birini seçin listeler gibi noktadan siteye yapılandırma adımları için istiyorsanız:

> [!div class="op_single_selector"]
> * [Otomatik olarak imzalanan sertifikalar - PowerShell oluşturma](vpn-gateway-certificates-point-to-site.md)
> * [Otomatik olarak imzalanan sertifikalar - MakeCert oluşturma](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Noktası-Site - Resource Manager - Azure portalında yapılandırın](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Noktadan siteye - Resource Manager - PowerShell yapılandırma](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Noktası-Site - Classic - Azure portalında yapılandırın](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Bu makalede Windows 10 çalıştıran bir bilgisayarda hello adımları gerçekleştirmeniz gerekir. Merhaba PowerShell cmdlet'leri toogenerate sertifikalar kullanmak hello Windows 10 işletim sisteminin bir parçası olan ve diğer Windows sürümlerinde çalışmaz. Merhaba Windows 10, yalnızca gerekli toogenerate hello sertifikaları bilgisayardır. Merhaba sertifikaları oluşturduktan sonra bunları karşıya yükleyebilir veya tüm desteklenen istemci işletim sistemine yükleyin. 

Erişim tooa Windows 10 bilgisayarı yoksa kullanabileceğiniz [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate sertifikalar. Merhaba her iki yöntemi kullanarak oluşturduğunuz sertifikalar herhangi yüklenebilir [desteklenen](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) istemci işletim sistemi.

## <a name="rootcert"></a>Otomatik olarak imzalanan sertifika oluştur

Merhaba yeni SelfSignedCertificate cmdlet toocreate otomatik olarak imzalanan bir sertifika kullanın. Ek parametre bilgi için bkz: [yeni SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Windows 10 çalıştıran bir bilgisayarda, yükseltilmiş ayrıcalıklarla bir Windows PowerShell konsolu açın.
2. Aşağıdaki örnek toocreate hello otomatik olarak imzalanan sertifika hello kullanın. Merhaba aşağıdaki örnek 'otomatik 'Sertifikalar-Geçerli User\Personal\Certificates' yüklü P2SRootCert' adlı otomatik olarak imzalanan bir sertifika oluşturur. Açarak hello sertifikayı görüntüleyebilirsiniz *certmgr.msc*, veya *kullanıcı sertifikaları yönetme*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Dışarı aktarma hello ortak anahtarı (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Merhaba exported.cer dosyası karşıya yüklenen tooAzure olması gerekir. Yönergeler için bkz: [noktadan siteye bağlantı yapılandırma](vpn-gateway-howto-point-to-site-rm-ps.md#upload). bir ek güvenilen kök sertifika tooadd [Bu bölümde](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello makalenin.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Merhaba otomatik olarak imzalanan sertifika ve ortak anahtar toostore vermek, (isteğe bağlı)

Tooexport hello otomatik olarak imzalanan kök sertifikası ve güvenli bir şekilde depolamak isteyebilirsiniz. Varsa olmadan, yapabilir daha sonra başka bir bilgisayara yükleyin ve daha fazla istemci sertifikalarını oluşturmak veya başka bir .cer dosyasına dışarı aktarma. tooexport hello .pfx, select hello kök sertifikası ve kullanım aynı adımları açıklandığı gibi hello olarak kök sertifikayı otomatik olarak imzalanan [bir istemci sertifikası verme](#clientexport).

## <a name="clientcert"></a>İstemci sertifikası oluşturma

Tooa bağlanan her istemci bilgisayar noktadan siteye kullanarak VNet yüklü bir istemci sertifikası olması gerekir. Ardından dışa hello otomatik olarak imzalanan kök sertifikasından bir istemci sertifikasını oluşturmak ve hello istemci sertifikası yükleyin. Merhaba istemci sertifikası yüklü değilse, kimlik doğrulaması başarısız olur. 

Merhaba aşağıdaki adımlar, otomatik olarak imzalanan kök sertifikasından bir istemci sertifikası oluşturma aracılığıyla yol. Merhaba birden çok istemci sertifikaları verebilir aynı kök sertifikaya. Merhaba adımları kullanarak istemci sertifikalarını oluşturmak, hello istemci sertifikasını otomatik olarak hello bilgisayarda toogenerate hello sertifika kullanılan yüklenir. Tooinstall başka bir istemci bilgisayarında bir istemci sertifikası istiyorsanız hello sertifika verebilirsiniz.

Merhaba örnekler hello yeni SelfSignedCertificate cmdlet toogenerate bir yıl içinde süresi dolar bir istemci sertifikası kullanır. Merhaba istemci sertifikası, farklı sona erme değeri ayarlanırken gibi ek parametre bilgi için bkz [yeni SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Örnek 1

Bu örnekte '$cert' hello önceki bölümde değişkeninden bildirilen hello kullanır. Otomatik olarak imzalanan sertifika Merhaba, veya yeni bir PowerShell konsol oturumda oluşturarak ek istemci sertifikaları sonra hello PowerShell konsolunu kapattıysanız, hello adımlarda kullanmak [örnek 2](#ex2).

Değiştirme ve bir istemci sertifikası hello örnek toogenerate çalıştırın. Değişiklik yapmadan aşağıdaki örneğine hello çalıştırırsanız, hello 'P2SChildCert' adlı bir istemci sertifikası sonucudur.  Tooname hello alt sertifika başka bir konuda istiyorsanız hello CN değeri değiştirin. Bu örnek çalıştırırken Hello TextExtension değiştirmeyin. oluşturduğunuz hello istemci sertifikası, bilgisayarınızda 'Sertifikalar - Geçerli User\Personal\Certificates' otomatik olarak yüklenir.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Örnek 2

Ek istemci sertifikaları oluşturma veya olan kullanmıyorsa hello aynı PowerShell oturumunda, otomatik olarak imzalanan sertifika, aşağıdaki adımları kullanın hello toocreate kullanılan:

1. Merhaba bilgisayarda yüklü hello otomatik olarak imzalanan kök sertifikayı belirleyin. Bu cmdlet, bilgisayarınızda yüklü sertifikaların listesini döndürür.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Liste, sonra bulunan sonraki tooit tooa metin Kopyala hello parmak izi döndürülen hello Hello konu adını bulun dosya. Aşağıdaki örnek hello, iki sertifika vardır. Merhaba CN adı toogenerate alt sertifika istediğiniz hello otomatik olarak imzalanan sertifika hello adıdır. Bu durumda, 'P2SRootCert'.

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Merhaba parmak hello önceki adımdaki kullanarak hello kök sertifikası için bir değişken bildirin. Parmak İZİ toogenerate alt sertifika istediğiniz hello kök sertifikası hello parmak iziyle değiştirin.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Örneğin, hello parmak hello önceki adımda P2SRootCert için kullanarak, hello değişkeni şöyle görünür:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Değiştirme ve bir istemci sertifikası hello örnek toogenerate çalıştırın. Değişiklik yapmadan aşağıdaki örneğine hello çalıştırırsanız, hello 'P2SChildCert' adlı bir istemci sertifikası sonucudur. Tooname hello alt sertifika başka bir konuda istiyorsanız hello CN değeri değiştirin. Bu örnek çalıştırırken Hello TextExtension değiştirmeyin. oluşturduğunuz hello istemci sertifikası, bilgisayarınızda 'Sertifikalar - Geçerli User\Personal\Certificates' otomatik olarak yüklenir.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Bir istemci sertifikasını dışarı aktarma   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Dışarı aktarılan istemci sertifikası yükleme

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Noktası Site yapılandırmanızı ile devam edin. 

* İçin **Resource Manager** dağıtım modeli adımları bkz [bir noktadan siteye bağlantı tooa VNet yapılandırma](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* İçin **Klasik** dağıtım modeli adımları bkz [bir noktadan siteye VPN bağlantısı tooa VNet (Klasik) yapılandırma](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
