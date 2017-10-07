---
title: "Azure Ağ İzleyicisi ile VPN ağ geçidi aracılığıyla aaaDiagnose şirket içi bağlantı | Microsoft Docs"
description: "Bu makalede nasıl toodiagnose bağlantı Azure Ağ İzleyicisi kaynak sorun giderme VPN ağ geçidi aracılığıyla şirket içi açıklanmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>VPN ağ geçitleri aracılığıyla şirket içi bağlantı tanılama

Azure VPN ağ geçidi, şirket içi ağınız ve Azure sanal ağınız arasında güvenli bir bağlantı hello gereksinimini adres toocreate karma çözümü sağlar. Gereksinimlerinizi benzersiz olduğundan, bu nedenle hello şirket içi VPN aygıtının seçimdir. Azure şu anda destekler [birkaç VPN aygıtları](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) , sürekli doğrulanma hello cihaz satıcılarıyla yöneticileriyle. Şirket içi VPN Cihazınızı yapılandırmadan önce Hello aygıta özgü yapılandırma ayarlarını gözden geçirin. Azure VPN ağ geçidi ile bir dizi benzer şekilde, yapılandırılmış [IPSec parametreleri desteklenen](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) bağlantıları kurmak için kullanılır. Şu anda seçin hello Azure VPN ağ geçidi IPSec parametrelerinden belirli bir bileşimini veya toospecify bir yolu yoktur. Şirket içi ve Azure arasında başarılı bir bağlantı kurmak için hello VPN cihaz ayarları Azure VPN ağ geçidi tarafından belirlenen hello IPSec parametreleri uygun olmalıdır şirket içi. Merhaba, ayarlarının doğru içinde bağlantı kaybı yoktur ve şimdiye kadar bu sorunları gidermek Önemsiz değildi ve genellikle saatleri tooidentify ve düzeltme hello sorunu sürdü.

Özellik Hello Azure Ağ İzleyicisi ile ilgili sorunları giderme, ağ geçidiniz ve bağlantıları ile ilgili tüm sorunları mümkün toodiagnose olan ve dakika içinde yeterli bilgi toomake bir bilinçli karar toorectify hello sorununuz.

## <a name="scenario"></a>Senaryo

Azure ile şirket içi arasında tooconfigure bir site siteye bağlantısı istediğiniz FortiGate hello içi VPN ağ geçidi olarak kullanma. tooachieve bu senaryo, kurulumdan sonraki hello gerekir:

1. Sanal ağ geçidi - hello Azure VPN ağ geçidi
1. Yerel ağ geçidi - hello [(FortiGate) VPN ağ geçidi şirket içi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) Azure bulutta gösterimi
1. Siteden siteye bağlantı (ilke tabanlı) - [hello hello VPN ağ geçidi arasındaki bağlantı şirket içi yönlendirici](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [FortiGate yapılandırma](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Bir siteden siteye yapılandırma hakkında ayrıntılı adım adım kılavuz ziyaret ederek bulunabilir: [hello Azure portalını kullanarak siteden siteye bağlantısı olan bir VNet oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Merhaba önemli yapılandırma adımları birini hello IPSec iletişimi parametrelerini yapılandırma, tüm yetersizliğini hello şirket içi ağınız ve Azure arasında bağlantı tooloss müşteri adayları. Şu anda Azure VPN ağ geçitleri için Aşama 1 IPSec parametreleri aşağıdaki yapılandırılmış toosupport hello içindedir. , Bu ayarlar değiştirilemez daha önce belirtildiği gibi unutmayın.  Merhaba aşağıdaki tabloda görüldüğü gibi Azure VPN ağ geçidi tarafından desteklenen hello şifreleme algoritmaları AES256, AES128 ve 3DES ' dir.

### <a name="ike-phase-1-setup"></a>IKE Aşama 1 Kurulumu

| **Özellik** | **PolicyBased** | **RouteBased ve standart veya yüksek performanslı VPN ağ geçidi** |
| --- | --- | --- |
| IKE Sürümü |IKEv1 |IKEv2 |
| Diffie-Hellman Grubu |Grup 2 (1024 bit) |Grup 2 (1024 bit) |
| Kimlik Doğrulama Yöntemi |Önceden Paylaşılan Anahtar |Önceden Paylaşılan Anahtar |
| Şifreleme Algoritmaları |AES256 AES128 3DES |AES256 3DES |
| Karma Algoritma |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Aşama 1 Güvenlik İlişkisi (SA) Yaşam Süresi (Zaman) |28.800 saniye |10.800 saniye |

Bir kullanıcı olarak gerekli tooconfigure olacaktır, FortiGate örnek bir yapılandırma bulunabilir [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Bilmeden, FortiGate toouse SHA-512 karma algoritması hello yapılandırılmış. Bu algoritma ilke tabanlı bağlantılar için desteklenen bir algoritma olmadığından, VPN bağlantınızı çalışır.

Bu sorunları sabit tootroubleshoot ve nedenlerini genellikle sezgisel olmayan. Bu durumda, bir destek bileti tooget Yardımı'hello sorun giderme açabilirsiniz. Ancak API Azure Ağ İzleyicisi ile ilgili sorunları giderme, bu sorunları kendi tanımlayabilirsiniz.

## <a name="troubleshooting-using-azure-network-watcher"></a>Azure Ağ İzleyicisi'ni kullanarak sorun giderme

toodiagnose, bağlantınızı tooAzure PowerShell bağlanmak ve başlatma hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet'i. Bu cmdlet adresindeki kullanma hello ayrıntılarını bulabilirsiniz [sorun giderme sanal ağ geçidi ve bağlantıları - PowerShell](network-watcher-troubleshoot-manage-powershell.md). Bu cmdlet toofew dakika toocomplete sürebilir.

Merhaba cmdlet tamamlandıktan sonra hello cmdlet'ini belirtilen toohello depolama konumuna gidebilirsiniz tooget ayrıntılı bilgileri üzerinde hello sorun ve Günlükler hakkında. Azure Ağ İzleyicisi Merhaba aşağıdaki günlük dosyaları içeren bir ZIP klasörü oluşturur:

![1][1]

IKEErrors.txt ve adlı açık hello dosya görüntüler hello aşağıdaki hata ile ilgili bir sorunu belirten, şirket içi IKE ayarı yanlış yapılandırma.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Bu durumda, olduğunu ilgili olarak gelen hello Scrubbed wfpdiag.txt hello hata hakkında ayrıntılı bilgi edinebilirsiniz `ERROR_IPSEC_IKE_POLICY_MATCH` bu sağlama tooconnection düzgün çalışmıyor.

Başka bir ortak yetersizliğini yanlış paylaşılan anahtarlar belirtme hello ' dir. Belirtilen, farklı paylaşılan anahtarlar örnek önceki hello varsa, hello IKEErrors.txt aşağıdaki hata hello gösterir: `Error: Authentication failed. Check shared key`.

Azure Ağ İzleyicisi sorun giderme özelliğini toodiagnose sağlar ve VPN ağ geçidi ve bağlantı hello basit bir PowerShell cmdlet kolaylığını sorun giderme. Şu anda biz koşullar aşağıdaki tanılama hello destekler ve birden çok koşul eklemeden doğrultusunda çalışıyoruz.

### <a name="gateway"></a>Ağ geçidi

| Hata türü | Neden | Günlük|
|---|---|---|
| NoFault | Herhangi bir hata algılandığında. |Evet|
| GatewayNotFound | Ağ geçidi veya ağ geçidi sağlanmamış bulunamıyor. |Hayır|
| PlannedMaintenance |  Ağ geçidi örneği bakım yapılıyor.  |Hayır|
| UserDrivenUpdate | Ne zaman bir kullanıcı güncelleştirme devam ediyor. Bu, yeniden boyutlandırma işlemi olabilir. | Hayır |
| VipUnResponsive | Merhaba birincil hello ağ geçidi örneğini ulaşamıyor. Merhaba durumu araştırması başarısız olduğunda meydana gelir. | Hayır |
| PlatformInActive | Merhaba platform ile ilgili bir sorun yoktur. | Hayır|
| ServiceNotRunning | Merhaba temel alınan hizmet çalışmıyor. | Hayır|
| NoConnectionsFoundForGateway | Hiçbir bağlantı hello ağ geçidinde bulunmaktadır. Bu yalnızca bir uyarıdır.| Hayır|
| ConnectionsNotConnected | Merhaba bağlantıları hiçbiri bağlanır. Bu yalnızca bir uyarıdır.| Evet|
| GatewayCPUUsageExceeded | Merhaba geçerli ağ geçidi CPU kullanımı % > 95 kullanımdır. | Evet |

### <a name="connection"></a>Bağlantı

| Hata türü | Neden | Günlük|
|---|---|---|
| NoFault | Herhangi bir hata algılandığında. |Evet|
| GatewayNotFound | Ağ geçidi veya ağ geçidi sağlanmamış bulunamıyor. |Hayır|
| PlannedMaintenance | Ağ geçidi örneği bakım yapılıyor.  |Hayır|
| UserDrivenUpdate | Ne zaman bir kullanıcı güncelleştirme devam ediyor. Bu, yeniden boyutlandırma işlemi olabilir.  | Hayır |
| VipUnResponsive | Merhaba birincil hello ağ geçidi örneğini ulaşamıyor. Merhaba durumu araştırması başarısız olduğunda gerçekleşir. | Hayır |
| ConnectionEntityNotFound | Bağlantı yapılandırması eksik. | Hayır |
| ConnectionIsMarkedDisconnected | Merhaba bağlantı "bağlantısı kesildi." olarak işaretlenmiş |Hayır|
| ConnectionNotConfiguredOnGateway | Merhaba temel alınan hizmet bağlantı yapılandırılmış hello yok. | Evet |
| ConnectionMarkedStandy | arka plandaki hizmet hello yedek olarak işaretlenir.| Evet|
| Kimlik Doğrulaması | Önceden paylaşılmış anahtar uyuşmuyor. | Evet|
| PeerReachability | Merhaba eş ağ geçidi ulaşılabilir değil. | Evet|
| IkePolicyMismatch | Merhaba eş ağ geçidi, Azure tarafından desteklenmez IKE ilkeleri vardır. | Evet|
| WfpParse hata | Ayrıştırma hello WFP günlük bir hata oluştu. |Evet|

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret ederek toocheck VPN ağ geçidi bağlantısı, PowerShell ve Azure Otomasyonu öğrenin [Azure Ağ İzleyicisi sorun giderme İzleyici VPN ağ geçitleri](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
