---
title: Azure bulut Hizmetleri rolleri ile ilgili SSS | Microsoft Docs
description: "Azure Cloud Services hakkında sık sorulan sorular. Sertifikalar, web rolleri ve çalışan rolleri hakkında bazı sık sorulan soruları yanıtlar."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a>Cloud Services SSS
Bu makalede, Microsoft Azure bulut hizmetleri hakkında sık sorulan bazı sorular yanıtlanmaktadır. Ayrıca, ziyaret edebilirsiniz [Azure destek SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma ve destek bilgileri için. Ayrıca başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.

## <a name="certificates"></a>Sertifikalar
### <a name="where-should-i-install-my-certificate"></a>My sertifika burada yüklemeniz gerekir?
* **Uygulamam**  
  Uygulama sertifikayı özel anahtarla (\*.pfx, \*.p12).
* **CA**  
  Tüm ara sertifikalarınız bu deposunda (ilke ve alt CA'lar) gidin.
* **KÖK**  
  Ana kök CA sertifikası burada gitmesi gereken şekilde kök CA depolar.

### <a name="i-cant-remove-expired-certificate"></a>Süresi dolan sertifika kaldırılamıyor.
Azure kullanımda olduğu sırada bir sertifika kaldırmasını engeller. Sertifikayı kullanan dağıtımını silerseniz veya dağıtım farklı veya yenilenmiş bir sertifika ile güncelleştirmeniz gerekir.

### <a name="delete-an-expired-certificate"></a>Süresi dolmuş bir sertifika Sil
Sertifika kullanılmadığı sürece, kullanabileceğiniz [Kaldır AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet'ini bir sertifikayı kaldırın.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Windows Azure hizmet yönetimi için Uzantılar adlı sertifikalar süresi dolmuş
Bu sertifikalar, Uzak Masaüstü uzantısı gibi bulut hizmeti uzantı eklendiğinde oluşturulur. Bu sertifikalar yalnızca şifreleme ve uzantı özel yapılandırması şifresini çözmek için kullanılır. Bu sertifikalar zaman aşımına uğrarsa önemli değildir. Sona erme tarihini işaretlenmemiştir.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Silinmiş sertifikalar beliriyor
Bu, büyük olasılıkla bir aracı gibi Visual Studio kullanıyorsanız nedeniyle beliriyor. Her bir sertifika kullanarak bir aracıyla bağladığınızda, Azure'a yeniden yüklenecek.

### <a name="my-certificates-keep-disappearing"></a>My sertifikaları kayboluyor tutun
Sanal makine örneğini geri dönüştürüldüğünde, tüm yerel değişiklikler kaybolur. Kullanım bir [başlangıç görevi](cloud-services-startup-tasks.md) sertifikaları için sanal makine rolü her başlatılışında yüklemek için.

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a>My yönetim sertifikaları Portalı'nda bulunamıyor
[Yönetim sertifikaları](../azure-api-management-certs.md) yalnızca Azure Klasik Portalı'nda bulunur. Geçerli Azure portalına yönetim sertifikaları kullanmaz. 

### <a name="how-can-i-disable-a-management-certificate"></a>Bir yönetim sertifikası nasıl devre dışı bırakabilirim?
[Yönetim sertifikaları](../azure-api-management-certs.md) devre dışı bırakılamaz. Artık kullanılması istemediğinizde Klasik Azure Portalı aracılığıyla silin.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Belirli bir IP adresi için bir SSL sertifikası nasıl oluşturulur?
İçindeki yönergeleri izleyin [sertifika öğretici oluşturma](cloud-services-certs-create.md). IP adresi DNS adı olarak kullanın.

## <a name="security"></a>Güvenlik
### <a name="disable-ssl-30"></a>SSL 3.0 devre dışı bırak
SSL 3.0 devre dışı bırakın ve TLS güvenlik kullanmak için bu blog gönderisi konusunda belgelenen bir başlangıç görevi oluşturun: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-to-your-website"></a>Ekleme **nosniff** Web sitesine
MIME türleri algılaması istemcilerin önlemek için bir ayar ekleyin, *web.config* dosya.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

Ayrıca bu ayarı IIS'de olarak ekleyebilirsiniz. Aşağıdaki komutla kullanmak [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>IIS web rolü için özelleştirme
IIS başlangıç komut dosyasını kullanın [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.

## <a name="scaling"></a>Ölçeklendirme
### <a name="i-cannot-scale-beyond-x-instances"></a>X ölçeklendirme olamaz örnekleri
Azure aboneliğinizi kullanabileceğiniz çekirdek sayısına bir sınır vardır. Kullanılabilir tüm çekirdek kullanılırsa ölçeklendirme çalışmaz. Bir sınır 100 çekirdek varsa, örneğin, bu 100 A1 boyuta sahip sanal makine örneklerini bulut hizmetiniz için olabilir veya sanal makine örnekleri 50 A2 boyutu anlamına gelir.

## <a name="networking"></a>Ağ
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Bir çoklu VIP bulut hizmetindeki bir IP rezerve edilemez
İlk olarak, IP için ayrılacak çalıştığınız sanal makine örneğini açık olduğundan emin olun. İkinci olarak, ayrılmış IP'ler rahatsız için hazırlama ve üretim dağıtımları kullandığınızdan emin olun. **Sağlamadığı** dağıtım yükseltme sırasında ayarlarını değiştirin.

## <a name="remote-desktop"></a>Uzak Masaüstü
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Nasıl yedeklerim Uzak Masaüstü bir NSG olduğunda?
Noktalarında trafiğine izin veren NSG kuralları eklemek **3389** ve **20000**.  Uzak Masaüstü bağlantı noktasını kullanır **3389**.  Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, doğrudan bağlanmak için hangi örneğinin denetleyemezsiniz.  *RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve istemcisinin bir RDP tanımlama bilgisi göndermek ve bağlanmak için tek bir örnek belirtin.  *RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.
