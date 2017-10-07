---
title: "Şirket içi Azure bağlantıları için VPN aygıtları aaaAbout | Microsoft Docs"
description: "Bu makalede VPN cihazları ve S2S VPN Gateway şirketler arası bağlantılar için IPsec parametreleri ele alınmaktadır. Bağlantılar tooconfiguration yönergeler ve örnekler verilmiştir."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>Siteden Siteye VPN Gateway bağlantıları için VPN cihazları ve IPsec/IKE parametreleri hakkında

Bir VPN cihazı gerekli tooconfigure bir VPN ağ geçidi kullanarak siteden siteye (S2S) şirketler arası VPN bağlantısı ' dir. Güvenli bağlantılar, şirket içi ağlar ve sanal ağlarınız arasında istediğiniz zaman veya siteden siteye bağlantıları kullanılan toocreate karma bir çözüm olabilir. Bu makalede, doğrulanmış VPN cihazlarının listesi ve VPN ağ geçitleri için IPsec/IKE parametrelerinin listesi verilmektedir.

> [!IMPORTANT]
> Şirket içi VPN cihazlarınız ve VPN ağ geçitleri arasında bağlantı sorunları yaşıyorsanız, çok başvuran[bilinen cihaz uyumluluk sorunları](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Merhaba tabloları görüntülerken öğeleri toonote:

* Azure VPN ağ geçitleri terimlerinde bir değişiklik meydana gelmiştir. Yalnızca hello adlarını değiştirilmiştir. İşlevsellik değişmez.
  * Statik Yönlendirme = PolicyBased
  * Dinamik Yönlendirme = RouteBased
* HighPerformance VPN ağ geçidi ve RouteBased VPN ağ geçidi için belirtimler olan hello aynı, aksi belirtilmediği sürece. Örneğin, RouteBased VPN gateway'ler ile uyumlu olan hello doğrulanan VPN cihazları da hello HighPerformance VPN ağ geçidi ile uyumlu değildir.

## <a name="devicetable"></a>Doğrulanmış VPN cihazları ve cihaz yapılandırma kılavuzları

> [!NOTE]
> Siteden Siteye bağlantı yapılandırırken, VPN cihazınız için genel kullanıma yönelik bir IPv4 IP adresi gereklidir.
>

Cihaz satıcılarıyla işbirliği yaparak bir grup standart VPN cihazını doğruladık. Tüm hello cihazların Merhaba cihaz ailelerindeki listesi aşağıdaki hello içinde VPN gateway'ler ile çalışması gerekir. Bkz: [hakkında VPN ağ geçidi ayarlarını](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand hello VPN türü hello tooconfigure istediğiniz VPN ağ geçidi çözüm için (PolicyBased veya RouteBased) kullanın.

toohelp VPN Cihazınızı yapılandırmak, tooappropriate cihaz ailesine karşılık gelen toohello bağlantılara bakın. Merhaba bağlantılar tooconfiguration yönergeleri en iyi çaba ilkesine göre sağlanır. VPN cihazı desteği için lütfen cihaz üreticinize başvurun.

|**Satıcı**          |**Cihaz ailesi**     |**En düşük işletim sistemi sürümü** |**PolicyBased yapılandırma yönergeleri** |**RouteBased yapılandırma yönergeleri** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Uyumlu Değil  |[Yapılandırma kılavuzu](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |AR Serisi VPN Yönlendiricileri |2.9.2                  |Çok yakında     |Uyumlu değil  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-serisi |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Yapılandırma kılavuzu](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Yapılandırma kılavuzu](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-serisi |Barracuda Güvenlik Duvarı 6.5  |[Yapılandırma kılavuzu](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Uyumlu değil |
| Brocade            |Vyatta 5400 vRouter   |Sanal Yönlendirici 6.6R3 GA|[Yapılandırma kılavuzu](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Uyumlu değil |
| Denetim Noktası |Güvenlik Ağ Geçidi |R77.30 |[Yapılandırma kılavuzu](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Yapılandırma kılavuzu](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Uyumlu değil |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Yapılandırma örnekleri*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 ve sonraki sürümleri |[Yapılandırma kılavuzu](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Uyumlu değil |
| F5 |BIG-IP serisi |12.0 |[Yapılandırma kılavuzu](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Yapılandırma kılavuzu](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Yapılandırma kılavuzu](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |SEIL Serisi |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Yapılandırma kılavuzu](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Uyumlu değil |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |J-Serisi |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Yapılandırma örnekleri](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Yönlendirme ve Uzaktan Erişim Hizmeti |Windows Server 2012 |Uyumlu değil |[Yapılandırma örnekleri](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Mission Control Security Ağ Geçidi |Yok |[Yapılandırma kılavuzu](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Uyumlu değil |
| Openswan |Openswan |2.6.32 |(Çok yakında) |Uyumlu değil |
| Palo Alto Networks |PAN-OS çalıştıran tüm cihazlar |PAN-OS<br>PolicyBased: 6.1.5 veya üzeri<br>RouteBased: 7.1.4 |[Yapılandırma kılavuzu](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Yapılandırma kılavuzu](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |TZ Series, NSA Series<br>SuperMassive Series<br>E-Class NSA Series |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[SonicOS 6.2 için yapılandırma kılavuzu](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[SonicOS 5.9 için yapılandırma kılavuzu](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[SonicOS 6.2 için yapılandırma kılavuzu](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[SonicOS 5.9 için yapılandırma kılavuzu](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Tümü |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Yapılandırma kılavuzu](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Yapılandırma kılavuzu](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) ISR 7200 Serisi yönlendiriciler yalnızca PolicyBased VPN'leri destekler.

## <a name="additionaldevices"></a>Doğrulanmayan VPN cihazları

Cihazınızı hello doğrulanan VPN cihazları tablosunda listede görmüyorsanız, Cihazınızı yine de siteden siteye bağlantı çalışabilir. Ek destek ve yapılandırma yönergeleri için cihaz üreticinize başvurun.

## <a name="editing"></a>Cihaz yapılandırma örneklerini düzenleme

Merhaba sağlanan VPN cihazı yapılandırma örneğini indirdikten sonra tooreplace gerekir hello bazıları değerleri ortamınız için tooreflect hello ayarları.

### <a name="tooedit-a-sample"></a>tooedit bir örnek:

1. Not Defteri'ni kullanarak hello örneği açın.
2. Arama ve tüm değiştirme <*metin*> dizeleri hello değerlerle tooyour ortamı ilgilidir. Emin tooinclude olması < ve >. Bir ad belirtildiğinde, seçtiğiniz hello adının benzersiz olması gerekir. Bir komut çalışmazsa, lütfen cihazınızın üretici belgelerine başvurun.

| **Örnek metin** | **Şununla değiştirin:** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |Bu nesne için seçtiğiniz ad. Örnek: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |Bu nesne için seçtiğiniz ad. Örnek: myAzureNetwork |
| &lt;RP_AccessList&gt; |Bu nesne için seçtiğiniz ad. Örnek: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |Bu nesne için seçtiğiniz ad. Örnek: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |Bu nesne için seçtiğiniz ad. Örnek: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Aralığı belirtin. Örnek: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Alt ağ maskesi belirtin. Örnek: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Şirket içi aralığı belirtin. Örnek: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Şirket içi alt ağ maskesini belirtin. Örnek: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Bu bilgi belirli tooyour sanal ağı ve Yönetim Portalı hello yer olarak **ağ geçidi IP adresi**. |
| &lt;SP_PresharedKey&gt; |Bu bilgiler belirli tooyour sanal ağ ve hello yönetme anahtarı olarak Yönetim Portalı bulunur. |

## <a name="ipsec"></a>IPsec/IKE parametreleri

> [!NOTE]
> Aşağıdaki tablonun hello listelenen hello değerleri hello VPN ağ geçidi tarafından şu anda var. desteklenir, ancak hiçbir mekanizmasıdır toospecify sizin için veya algoritmaları ya da parametreleri belirli bir bileşimini hello VPN ağ geçidi seçin. Tüm kısıtlamaları hello şirket içi VPN cihazı belirtmeniz gerekir. Ayrıca, **MSS**’i **1350**’de sıkıştırmanız gerekir.
> 
>

Aşağıdaki tablolar hello:

* SA = Güvenlik İlişkisi
* IKE Aşama 1 "Ana Mod" olarak da adlandırılır
* IKE Aşama 2 "Hızlı Mod" olarak da adlandırılır

### <a name="ike-phase-1-main-mode-parameters"></a>IKE Aşama 1 (Ana Mod) parametreleri

| **Özellik**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| IKE Sürümü           |IKEv1              |IKEv2              |
| Diffie-Hellman Grubu  |Grup 2 (1024 bit) |Grup 2 (1024 bit) |
| Kimlik Doğrulama Yöntemi |Önceden Paylaşılan Anahtar     |Önceden Paylaşılan Anahtar     |
| Şifreleme ve Karma Algoritmaları |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| SA Yaşam Süresi           |28.800 saniye     |28.800 saniye     |

### <a name="ike-phase-2-quick-mode-parameters"></a>IKE Aşama 2 (Hızlı Mod) parametreleri

| **Özellik**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| IKE Sürümü                   |IKEv1          |IKEv2                                        |
| Şifreleme ve Karma Algoritmaları |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[RouteBased QM SA Teklifleri](#RouteBasedOffers) |
| SA Yaşam Süresi (Zaman)            |3.600 saniye  |27.000 saniye                                |
| SA Yaşam Süresi (Bayt)           |102.400.000 KB | -                                           |
| Kusursuz İletme Gizliliği (PFS) |Hayır             |[RouteBased QM SA Teklifleri](#RouteBasedOffers) |
| Kullanılmayan Eş Algılama (DPD)     |Desteklenmiyor  |Destekleniyor                                    |


### <a name ="RouteBasedOffers"></a>RouteBased VPN IPsec Güvenlik İlişkisi (IKE Hızlı Mod SA) Teklifleri

Merhaba aşağıdaki tabloda IPSec SA (IKE hızlı mod) tekliflerini listeler. Teklifler olan listelenen hello sipariş tercihine göre bu hello teklif sunulan veya kabul edildi.

#### <a name="azure-gateway-as-initiator"></a>Başlatıcı olarak Azure Gateway

|-  |**Şifreleme**|**Kimlik doğrulaması**|**PFS Grubu**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |

#### <a name="azure-gateway-as-responder"></a>Yanıtlayıcı olarak Azure Gateway

|-  |**Şifreleme**|**Kimlik doğrulaması**|**PFS Grubu**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |
| 7 |DES           |SHA1              |None         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |None         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* RouteBased ve Yüksek Performanslı VPN ağ geçitleri ile IPsec ESP NULL şifrelemesini belirtebilirsiniz. Null tabanlı şifreleme Aktarımdaki koruma toodata sağlamaz ve yalnızca maksimum kullanılmalıdır performans ve minimum gecikme gereklidir. İstemcileri toouse bunu VNet-VNet iletişim senaryolarında veya şifreleme hello çözümde başka bir yere uygulanmakta olduğunda tercih edebilirsiniz.
* Merhaba Internet üzerinden şirket içi bağlantılar için şifreleme ve karma algoritmaları hello tabloları, kritik iletişiminizin tooensure güvenlik yukarıda listelenen hello varsayılan Azure VPN ağ geçidi ayarlarını kullanın.

## <a name="known"></a>Bilinen cihaz uyumluluk sorunları

> [!IMPORTANT]
> Bunlar olan hello üçüncü taraf VPN aygıtları ve Azure VPN ağ geçitleri arasında bilinen uyumluluk sorunları. Hello Azure ekibi, burada listelenen sorunları tooaddress hello hello satıcıları ile etkin olarak çalışıyor. Merhaba sorunları çözüldükten sonra bu sayfayı hello en güncel bilgilerle güncelleştirilir. Lütfen bu sayfayı düzenli aralıklarla kontrol edin.
>
>

### <a name="feb-16-2017"></a>16 Şubat 2017

**Sürüm önceki too7.1.4 Palo Alto Networks aygıtlarla** Azure yol tabanlı VPN için: Palo Alto ağlardan VPN aygıtları ile PAN-OS sürümü önceki too7.1.4 kullanıyorsanız ve bağlantı yaşıyor tooAzure rota tabanlı VPN ağ geçitleri sorunları Merhaba aşağıdaki adımları gerçekleştirin:

1. Palo Alto Networks Cihazınızı Hello bellenim sürümünü denetleyin. PAN-OS sürümünüzü 7.1.4 eski ise too7.1.4 yükseltin.
2. Merhaba Palo Alto Networks aygıtta hello Aşama 2 SA (veya hızlı mod SA) yaşam süresi too28 800 saniyedir (8 saat) değiştirdiğinizde toohello Azure VPN ağ geçidi bağlanma.
3. Bağlantı sorunları yaşamaya devam ediyorsanız, hello Azure portal ' bir destek isteği açın.
