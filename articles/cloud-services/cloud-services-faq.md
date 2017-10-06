---
title: aaaAzure bulut Hizmetleri rolleri ile ilgili SSS | Microsoft Docs
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
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>Cloud Services SSS
Bu makalede, Microsoft Azure bulut hizmetleri hakkında sık sorulan bazı sorular yanıtlanmaktadır. Merhaba ziyaret edebilirsiniz [Azure destek SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma ve destek bilgileri için. Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.

## <a name="certificates"></a>Sertifikalar
### <a name="where-should-i-install-my-certificate"></a>My sertifika burada yüklemeniz gerekir?
* **Uygulamam**  
  Uygulama sertifikayı özel anahtarla (\*.pfx, \*.p12).
* **CA**  
  Tüm ara sertifikalarınız bu deposunda (ilke ve alt CA'lar) gidin.
* **KÖK**  
  Ana kök CA sertifikası burada gitmesi gereken şekilde Hello kök CA depolar.

### <a name="i-cant-remove-expired-certificate"></a>Süresi dolan sertifika kaldırılamıyor.
Azure kullanımda olduğu sırada bir sertifika kaldırmasını engeller. Merhaba sertifikayı kullanan tooeither Sil hello dağıtımı veya güncelleştirme hello dağıtımı farklı veya yenilenmiş bir sertifika ile gerekir.

### <a name="delete-an-expired-certificate"></a>Süresi dolmuş bir sertifika Sil
Hello sertifika kullanılmadığı sürece hello kullanabilirsiniz [Kaldır AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove bir sertifika.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Windows Azure hizmet yönetimi için Uzantılar adlı sertifikalar süresi dolmuş
Uzak Masaüstü uzantısı hello gibi toohello bulut hizmeti uzantı eklendiğinde bu sertifikaları oluşturulur. Bu sertifikalar yalnızca şifreleme ve hello özel yapılandırma hello uzantısı'nın şifresini çözmek için kullanılır. Bu sertifikalar zaman aşımına uğrarsa önemli değildir. Merhaba sona erme tarihi işaretlenmemiştir.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Silinmiş sertifikalar beliriyor
Bu, büyük olasılıkla bir aracı gibi Visual Studio kullanıyorsanız nedeniyle beliriyor. Her bir sertifika kullanarak bir aracıyla bağladığınızda, yeniden yüklenen tooAzure olur.

### <a name="my-certificates-keep-disappearing"></a>My sertifikaları kayboluyor tutun
Merhaba sanal makine örneğini geri dönüştürüldüğünde, tüm yerel değişiklikler kaybolur. Kullanım bir [başlangıç görevi](cloud-services-startup-tasks.md) tooinstall sertifikaları toohello sanal makineyi her zaman hello rol başlatır.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>My yönetim sertifikaları hello Portalı'nda bulunamıyor
[Yönetim sertifikaları](../azure-api-management-certs.md) yalnızca hello Klasik Azure portalı içinde kullanılabilir. Merhaba geçerli Azure portalına yönetim sertifikaları kullanmaz. 

### <a name="how-can-i-disable-a-management-certificate"></a>Bir yönetim sertifikası nasıl devre dışı bırakabilirim?
[Yönetim sertifikaları](../azure-api-management-certs.md) devre dışı bırakılamaz. Bunları istemiyorsanız, bunları hello Klasik Azure portalı artık kullanılan toobe silin.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Belirli bir IP adresi için bir SSL sertifikası nasıl oluşturulur?
Merhaba hello içindeki yönergeleri izleyin [sertifika öğretici oluşturma](cloud-services-certs-create.md). Başlangıç IP adresi, DNS adı hello olarak kullanın.

## <a name="security"></a>Güvenlik
### <a name="disable-ssl-30"></a>SSL 3.0 devre dışı bırak
toodisable SSL 3.0 ve TLS güvenlik kullanın, bu blog gönderisi konusunda belgelenen bir başlangıç görevi oluşturun: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Ekleme **nosniff** tooyour Web sitesi
Merhaba MIME türleri algılaması istemcilerinden tooprevent bir ayar ekleyin, *web.config* dosya.

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

Ayrıca bu ayarı IIS'de olarak ekleyebilirsiniz. Kullanım hello aşağıdaki komut ile Merhaba [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>IIS web rolü için özelleştirme
Merhaba IIS Başlangıç hello betikten kullanmak [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.

## <a name="scaling"></a>Ölçeklendirme
### <a name="i-cannot-scale-beyond-x-instances"></a>X ölçeklendirme olamaz örnekleri
Azure aboneliğinizi hello kullanabileceğiniz çekirdek sayısına bir sınır vardır. Kullanılabilir tüm hello çekirdek kullanılırsa ölçeklendirme çalışmaz. Bir sınır 100 çekirdek varsa, örneğin, bu 100 A1 boyuta sahip sanal makine örneklerini bulut hizmetiniz için olabilir veya sanal makine örnekleri 50 A2 boyutu anlamına gelir.

## <a name="networking"></a>Ağ
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Bir çoklu VIP bulut hizmetindeki bir IP rezerve edilemez
Öncelikle, tooreserve hello IP için çalıştığınız bu hello sanal makine örneğini açık olduğundan emin olun. İkinci olarak, ayrılmış IP'ler rahatsız hello hazırlama ve üretim dağıtımları için kullandığınızdan emin olun. **Sağlamadığı** hello dağıtım yükseltme sırasında hello ayarlarını değiştirin.

## <a name="remote-desktop"></a>Uzak Masaüstü
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Nasıl yedeklerim Uzak Masaüstü bir NSG olduğunda?
Kuralları toohello noktalarında trafiğine izin veren NSG ekleme **3389** ve **20000**.  Uzak Masaüstü bağlantı noktasını kullanır **3389**.  Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, hangi örneğinin tooconnect doğrudan denetleyemezsiniz.  Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve hello istemci toosend bir RDP izin ver ve bir tek tek örnek tooconnect belirtin.  Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.
