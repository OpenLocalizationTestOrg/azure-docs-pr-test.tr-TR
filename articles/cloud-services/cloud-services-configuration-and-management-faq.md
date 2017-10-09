---
title: "aaaConfiguration ve yönetimi sorunları için Microsoft Azure bulut Hizmetleri ile ilgili SSS | Microsoft Docs"
description: "Bu makalede, yapılandırması ve yönetimi için Microsoft Azure bulut hizmetleri hakkında sık sorulan sorular hello listelenmektedir."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure bulut Hizmetleri için yapılandırma ve yönetme sorununu: sık sorulan sorular (SSS)

Bu makale için yapılandırması ve yönetimi sorunları hakkında sık sorulan sorular içerir [Microsoft Azure bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services). Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>"Nosniff" toomy Web sitesi nasıl eklenir?
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

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Web rolü için nasıl IIS özelleştirebilir?
Merhaba IIS Başlangıç hello betikten kullanmak [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.

## <a name="i-cannot-scale-beyond-x-instances"></a>X ölçeklendirme olamaz örnekleri
Azure aboneliğinizi hello kullanabileceğiniz çekirdek sayısına bir sınır vardır. Kullanılabilir tüm hello çekirdek kullanılırsa ölçeklendirme çalışmaz. Bir sınır 100 çekirdek varsa, örneğin, bu 100 A1 boyuta sahip sanal makine örneklerini bulut hizmetiniz için olabilir veya sanal makine örnekleri 50 A2 boyutu anlamına gelir.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Nasıl ı bulut Hizmetleri için rol tabanlı erişim uygulayabilirsiniz?
Bulut Hizmetleri bir Azure Resource Manager temelli hizmeti olmadığından hello rol tabanlı erişim denetimi (RBAC) modelini desteklemez.

Bkz: [Klasik abonelik yöneticileri ve Azure RBAC](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Merhaba boşta kalma zaman aşımı için Azure yük dengeleyici nasıl ayarlarım?
Bu gibi hizmet tanımı (csdef) dosyanızdaki hello zaman aşımı belirtebilirsiniz:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Bkz: [yeni: yapılandırılabilir boşta kalma zaman aşımı Azure yük dengeleyici için](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) daha fazla bilgi için.

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>Microsoft iç mühendisleri RDP toocloud hizmet örnekleri izniniz olmadan kullanabilir?
Bulut hizmeti olmadan içine tooRDP iç izin vermez katı bir işlem mühendisleri Microsoft aşağıdaki hello sahibi veya kendi yetkilinin izni (e-posta veya diğer yazılı iletişimde) yazılır.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Neden hello sertifika zinciri my bulut hizmeti SSL sertifikası eksik mi?
Müşteriler hello tam sertifika zinciri (Yaprak sertifikası, Ara sertifikaları ve kök sertifika) yalnızca Yaprak sertifikası hello yerine yüklemenizi öneririz. Yalnızca hello Yaprak sertifikası yüklediğinizde, Windows toobuild hello sertifika zinciri üzerinde hello CTL adım adım ilerlemenizi sağlayarak kullanır. Windows toovalidate hello sertifika çalışırken aralıklı ağ veya DNS sorunlarına Azure veya Windows Update meydana gelirse, hello sertifika geçersiz kabul. Merhaba tam sertifika zinciri yükleyerek bu sorun önlenebilir. blog adresindeki hello [nasıl tooinstall zincirleme bir SSL sertifikası](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) gösterir nasıl toodo bu.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Bir statik IP adresi toomy bulut hizmeti nasıl ilişkilendirmek?
tooset statik bir IP adresi yukarı toocreate ayrılmış IP gerekir. Bu ayrılmış IP ilişkili tooa yeni bulut hizmeti veya tooan mevcut dağıtımı olabilir. Ayrıntılar için belgelere aşağıdaki hello bakın:
* [Nasıl toocreate ayrılmış bir IP adresi](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Var olan bir bulut hizmetinin başlangıç IP adresi ayırın](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Ayrılmış IP tooa yeni bir bulut hizmeti ilişkilendirme](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Dağıtım çalıştıran ayrılmış bir IP tooa ilişkilendirme](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Hizmet yapılandırma dosyası kullanarak bir ayrılmış IP tooa bulut hizmeti ilişkilendirin](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>Merhaba kota sınırını my bulut hizmeti nedir?
Bkz: [hizmete özgü sınırlar](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>My bulut hizmeti VM hello sürücüde çok az boş disk alanı neden Göster?
Bu beklenen davranıştır ve herhangi bir sorun tooyour uygulama neden döndürmemelidir. Merhaba % uproot için temelde çift hello dosyaları normalde kapladığı alanı miktarını tüketir Azure PaaS VM'ler % sürücüde günlük kaydı etkinleştirilir. Ancak, farkında toobe temelde bir olmayan-sorunu bu Aç birkaç şey vardır.

Merhaba % approot % sürücü boyutu hesaplanır < .cspkg + max günlük boyutu boyutunu > + Kenar boşluğu boş alan olarak ya da 1,5 GB, hangisi daha büyüktür. VM Hello boyutu bu hesaplamayı şifrelemeyle vardır. (Merhaba VM boyutu yalnızca hello geçici C: sürücüsü hello boyutunu etkiler.) 

Desteklenmeyen toowrite toohello % approot % sürücü değil. Azure VM toohello yazıyorsanız, bunu bir geçici LocalStorage kaynak yapmalısınız (veya başka bir seçeneği gibi Blob Depolama, Azure dosyaları, vb..). Bu nedenle hello hello % approot % klasöründeki boş alan miktarını anlamı yoktur. Uygulamanızı toohello % approot % sürücüsünü yazarken emin değilseniz, hizmetiniz birkaç gün boyunca çalıştırın ve ardından "önce" ve "sonra" boyutları hello karşılaştırın her zaman izin verebilirsiniz. 

Azure herhangi bir şey yazmayacak toohello % approot % sürücü. Merhaba VHD, .cspkg oluşturulur ve Azure VM hello takılı sonra toothis sürücü yazabilir hello tek şey, uygulamasıdır. 

kapatamaz şekilde hello günlük yapılandırılamayan, ayarlardır.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Azure temel IP'leri/Kimlikleri ve DDOS sağlayan hello özellikleri ve yetenekleri nelerdir?
Azure veri merkezi fiziksel sunucuları toodefend tehditlere karşı IP'leri/Kimlikler sahiptir. Buna ek olarak, müşteriler, web uygulaması güvenlik duvarı, ağ güvenlik duvarları, kötü amaçlı yazılımdan koruma, izinsiz giriş algılama, önleme sistemleri (Kimlikleri/IP) ve daha fazla gibi üçüncü taraf güvenlik çözümleri dağıtabilirsiniz. Daha fazla bilgi için bkz: [veri ve varlıkların korumak ve genel güvenlik standartları ile uyum](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Microsoft, sunucuları, ağları ve uygulamaları toodetect tehditleri sürekli olarak izler. Azure'nın multipronged tehdit Yönetimi yaklaşımı kullanır izinsiz giriş algılama, dağıtılmış--hizmet engelleme (DDoS) saldırısı önleme, sızma sınama, davranış analizi, anomali algılama ve makine öğrenme tooconstantly güçlendirme, savunma ve riskleri azaltın. Azure için Microsoft Antimalware Azure bulut Hizmetleri ve sanal makineleri korur. Hello seçeneği toodeploy üçüncü taraf güvenlik çözümleri Ayrıca, web uygulaması güvenlik duvarları, ağ güvenlik duvarları, kötü amaçlı yazılımdan koruma, izinsiz giriş algılama ve önleme sistemleri (Kimlikleri/IP) ve daha fazlası gibi sahiptir.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>IIS toohello günlük dizini yazma neden durdurur?
Toohello günlük dizini yazmak için yerel depolama kotası hello azaltılmıştır. Bu sorunu gidermek için işlemlerden birini yapabilirsiniz:
* IIS için tanılamayı etkinleştirin ve hello tanılama düzenli aralıklarla tooblob depolama taşınmış.
* El ile günlük dosyalarının dizin günlüğü hello kaldırın.
* Yerel kaynaklar için kota sınırını artırın.

Daha fazla bilgi için aşağıdaki belgeleri hello bakın:
* [Azure Depolama’daki tanılama verilerini depolama ve görüntüleme](cloud-services-dotnet-diagnostics-storage.md)
* [Bulut hizmetinde yazma IIS günlüklerini durdurur](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Merhaba "Windows Azure Araçları şifreleme sertifikası için uzantıları" Merhaba amacı nedir?
Toohello bulut hizmeti uzantı eklendiğinde bu sertifikaları otomatik olarak oluşturulur. En yaygın olarak, bu hello WAD uzantısı veya hello RDP uzantısı, ancak diğer kötü amaçlı yazılımdan koruma veya günlük Toplayıcı uzantısını hello gibi olabilir. Bu sertifikalar yalnızca şifreleme ve hello uzantısı için özel yapılandırma hello şifresini çözmek için kullanılır. Merhaba sertifika süresi dolmuşsa önemli değildir şekilde hello sona erme tarihi hiçbir zaman denetlenir. 

Bu sertifikalar yoksayabilirsiniz. Merhaba sertifikaları temizlemek isterseniz, tüm silerek deneyebilirsiniz. Toodelete çalışırsanız azure kullanımda olan bir sertifikayı bir hata özel durum oluşturacak.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Nasıl t bir sertifika imzalama isteği (CSR) "RDP-lık" olmadan toohello örneğinde oluşturabilir miyim?
Kılavuzu belge aşağıdaki hello bakın:

>[Windows Azure Web siteleri (WAWS) ile kullanılacak bir sertifika edinme](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Bir CSR yalnızca bir metin dosyası olduğunu unutmayın. Merhaba makineden oluşturulan toobe hello sertifika sonuçta nerede kullanılacak yok. Bu belgede bir uygulama hizmeti için yazılmış olsa da hello CSR oluşturma geneldir ve bulut Hizmetleri için de geçerlidir.
