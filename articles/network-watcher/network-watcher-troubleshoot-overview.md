---
title: "Azure Ağ İzleyicisi sorun giderme aaaIntroduction tooresource | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi kaynak sorun giderme özelliklerine genel bakış sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Giriş tooresource Azure Ağ İzleyicisi sorunlarını giderme

Sanal ağ geçitleri, şirket içi kaynakları ile Azure içindeki diğer sanal ağlar arasında bağlantı sağlar. Bu ağ geçitleri ve kendi bağlantılarını izleme kritik tooensuring iletişim bozuk değil. Ağ İzleyicisi Merhaba yetenek tootroubleshoot sağlayan sanal ağ geçitleri ve ağ bağlantıları. Bu hello portal, PowerShell'i, CLI veya REST API çağrılabilir. Çağrıldığında, Ağ İzleyicisi Merhaba durumunu hello sanal ağ geçidi veya bağlantı ve dönüş hello uygun sonuçları tanılar. Merhaba tanılama tamamlandıktan sonra bu istek uzun süren bir işlemdir, hello sonuçlar döndürülür.

![portal][2]

## <a name="results"></a>Sonuçlar

döndürülen hello ön sonuçları hello kaynak hello durumunu genel bir bakış sağlar. Daha ayrıntılı bilgi için kaynaklar hello bölümü aşağıdaki gösterildiği gibi sağlanabilir:

Merhaba aşağıdaki hello ile döndürülen hello değerleri API sorun giderme listesidir:

* **startTime** -bu değer hello sorun giderme, çalışmaya API çağrısı hello saattir.
* **endTime** -bu değer hello sorun giderme ne zaman sona hello saattir.
* **kod** -tek tanılama hatası varsa bu sağlıksız, değerdir.
* **Sonuçları** -sonuçları hello bağlantısı veya hello sanal ağ geçidinde döndürülen sonuçları koleksiyonudur.
    * **Kimliği** -bu değeri hello hataya türüdür.
    * **Özet** -bu değer hello hataya bir özetidir.
    * **ayrıntılı** -bu değer hello hatası için ayrıntılı bir açıklama sağlar.
    * **recommendedActions** -bu özellik önerilen eylemleri tootake koleksiyonudur.
      * **actionText** -bu değer hangi eylemini tootake açıklayan hello metni içerir.
      * **actionUri** -bu değer hello URI toodocumentation hakkında yönergeler sağlar. tooact.
      * **actionUriText** -bu değer hello eylem metni kısa açıklamasıdır.

kullanılabilir olan tabloları göster hello farklı hata türleri (ID listesi önceki hello sonuçlarından altında) aşağıdaki hello ve hello hata günlükleri oluşturur.

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
| ConnectionsNotConnected | Bağlantıları bağlı değil. Bu yalnızca bir uyarıdır.| Evet|
| GatewayCPUUsageExceeded | Merhaba geçerli ağ geçidi CPU kullanımı % > 95 ' dir. | Evet |

### <a name="connection"></a>Bağlantı

| Hata türü | Neden | Günlük|
|---|---|---|
| NoFault | Herhangi bir hata algılandığında. |Evet|
| GatewayNotFound | Ağ geçidi veya ağ geçidi sağlanmamış bulunamıyor. |Hayır|
| PlannedMaintenance | Ağ geçidi örneği bakım yapılıyor.  |Hayır|
| UserDrivenUpdate | Ne zaman bir kullanıcı güncelleştirme devam ediyor. Bu, yeniden boyutlandırma işlemi olabilir.  | Hayır |
| VipUnResponsive | Merhaba birincil hello ağ geçidi örneğini ulaşamıyor. Merhaba durumu araştırması başarısız olduğunda gerçekleşir. | Hayır |
| ConnectionEntityNotFound | Bağlantı yapılandırması eksik. | Hayır |
| ConnectionIsMarkedDisconnected | Merhaba bağlantı "bağlantısız" olarak işaretlenmiş. |Hayır|
| ConnectionNotConfiguredOnGateway | Merhaba temel alınan hizmet bağlantı yapılandırılmış hello yok. | Evet |
| ConnectionMarkedStandy | arka plandaki hizmet hello yedek olarak işaretlenir.| Evet|
| Kimlik Doğrulaması | Önceden paylaşılmış anahtar uyuşmuyor. | Evet|
| PeerReachability | Merhaba eş ağ geçidi ulaşılabilir değil. | Evet|
| IkePolicyMismatch | Merhaba eş ağ geçidi, Azure tarafından desteklenmez IKE ilkeleri vardır. | Evet|
| WfpParse hata | Ayrıştırma hello WFP günlük bir hata oluştu. |Evet|

## <a name="supported-gateway-types"></a>Desteklenen ağ geçidi türleri

Merhaba aşağıdaki listede hello destek hangi ağ geçitleri ve bağlantıları desteklenen gösterir Ağ İzleyicisi sorun giderme.
|  |  |
|---------|---------|
|**Ağ geçidi türleri**   |         |
|VPN      | Destekleniyor        |
|ExpressRoute | Desteklenmiyor |
|Hypernet | Desteklenmiyor|
|**VPN türleri** | |
|Rota tabanlı | Destekleniyor|
|İlke tabanlı | Desteklenmiyor|
|**Bağlantı türleri**||
|IPSec| Destekleniyor|
|VNet2Vnet| Destekleniyor|
|ExpressRoute| Desteklenmiyor|
|Hypernet| Desteklenmiyor|
|VPNClient| Desteklenmiyor|

## <a name="log-files"></a>Günlük dosyaları

Kaynak sorun giderme tamamlandıktan sonra hello kaynak sorun giderme günlük dosyalarının bir depolama hesabında depolanır. Merhaba aşağıdaki görüntüde hello örnek hatayla sonuçlandı bir çağrı içeriğini gösterir.

![zip dosyası][1]

> [!NOTE]
> Bazı durumlarda, yalnızca bir alt kümesini hello günlük dosyalarını toostorage yazılır.

Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kullanılabilir başka bir Depolama Gezgini aracıdır. Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Merhaba **ConnectionStats.txt** dosyası hello bağlantı, giriş ve çıkış baytlarını, bağlantı durumu ve bağlantının oluşturulduğu hello zaman hello dahil olmak üzere, genel istatistikleri içerir.

> [!NOTE]
> API sorun giderme hello çağrısı toohello sağlıklı döndürürse, hello tek şey hello zip dosyasında döndürdü bir **ConnectionStats.txt** dosya.

Bu dosyanın içeriğini Hello aşağıdaki örneğine benzer toohello şunlardır:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Merhaba **CPUStats.txt** dosyasını içeren CPU kullanımı ve bellek sınama hello aynı anda kullanılabilir.  Bu dosyanın içeriğini Hello benzer toohello örneği aşağıdaki verilmiştir:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Merhaba **IKEErrors.txt** dosyasını içeren IKE hataları izleme sırasında bulunamadı.

Merhaba aşağıdaki örnek bir IKEErrors.txt dosyasının hello içeriğini gösterir. Hatalarınızı hello sorunu bağlı olarak farklı olabilir.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>İptal etti wfpdiag.txt

Merhaba **Scrubbed wfpdiag.txt** günlük dosyası hello wfp günlük içerir. Bu günlük paket bırakma ve IKE/AuthIP hataları günlüğe kaydedilmesini içerir.

Merhaba aşağıdaki örnek hello hello Scrubbed wfpdiag.txt dosyasının içeriğini gösterir. Bu örnekte, bir bağlantısı paylaşılan anahtarı hello satırından hello 3 hello alt görüldüğü gibi doğru değildi. Aşağıdaki örneğine hello yalnızca hello tüm günlük parçacığıyla aynıdır Hello günlük hello sorunu bağlı olarak uzun olabilir.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.Sum

Merhaba **wfpdiag.txt.sum** hello arabellek ve işlenen olayların gösteren bir günlük dosyasıdır.

Merhaba aşağıdaki wfpdiag.txt.sum dosyasının Merhaba içeriğine örnektir.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toodiagnose VPN ağ geçitleri ve bağlantıları üzerinden ziyaret ederek portal hello öğrenin [ağ geçidi sorun giderme - Azure portalında](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
