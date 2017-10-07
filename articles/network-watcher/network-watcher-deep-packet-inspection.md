---
title: "Azure Ağ İzleyicisi ile aaaPacket denetleme | Microsoft Docs"
description: "Bir sanal makineden toouse Ağ İzleyicisi tooperform derin paket incelemesi nasıl toplanan bu makalede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Azure Ağ İzleyicisi ile paket incelemesi

Ağ İzleyicisi Merhaba paket yakalama özelliğini kullanarak, Azure Vm'leriniz hello portalı, PowerShell CLI ve hello SDK aracılığıyla programlı olarak ve REST API yakalamaları oturumlarını yönetmesine ve başlatın. Paket yakalama, paket düzeyinde veri kullanılabilir biçiminde hello bilgileri sağlayarak gerektiren tooaddress senaryolar sağlar. Ücretsiz Araçlar tooinspect hello veri yararlanarak, Vm'leriniz iletişimler tooand inceleyin ve ağ trafiğinizi alın. Paket yakalama veri bazı örnek kullanımları şunlardır: ağ veya uygulama sorunları incelemeye, ağ kötüye ve yetkisiz erişim girişimlerini algılama veya Mevzuat uyumluluğu bakımını yapma. Bu makalede, nasıl tooopen bir paket yakalama dosyasını Ağ İzleyicisi tarafından popüler açık kaynak aracını kullanarak sağlanan gösterir. Biz de nasıl toocalculate bağlantı gecikmesi anormal trafiği tanımlamak ve ağ istatistikleri inceleyin gösteren örnekler sağlanır.

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalede önceden çalıştırılmış olan bir paket yakalama önceden yapılandırılmış bazı senaryolar üzerinden gider. Bu senaryolar, bir paket yakalama gözden geçirerek erişilebilir özellikleri gösterilmektedir. Bu senaryo kullanır [WireShark](https://www.wireshark.org/) tooinspect hello paket yakalama.

Bu senaryo, bir sanal makinede bir paket yakalama zaten başlattıysanız varsayar. nasıl toocreate paket yakalama ziyaret toolearn [Yönet paket yakalar hello portalıyla](network-watcher-packet-capture-manage-portal.md) veya REST şu adresi ziyaret ederek ile [REST API ile paket yakalar yönetme](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Senaryo

Bu senaryoda:

* Paket yakalama gözden geçirin

## <a name="calculate-network-latency"></a>Ağ gecikmesi Hesapla

Bu senaryoda, nasıl tooview hello iki uç noktaları arasında gerçekleşen İletim Denetimi Protokolü (TCP) konuşmanın ilk gidiş dönüş süresi (RTT) gösterir.

Bir TCP bağlantı kurulduğunda hello hello bağlantısında gönderilen ilk üç paketleri bir yaygın olarak ifade deseni tooas hello üç yönlü anlaşması izleyin. Bu bağlantı oluşturulduğunda bu anlaşma, bir ilk isteği hello istemciden ve hello sunucusundan yanıt gönderilen hello ilk iki paket inceleyerek, biz hello gecikme hesaplayabilirsiniz. Bu gecikme başvurulan tooas hello gidiş dönüş süresi (RTT) olur. Merhaba TCP protokolü ve hello üç yönlü el sıkışma hakkında daha fazla bilgi için kaynak aşağıdaki toohello bakın. https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-three-Way-Handshake-via-TCP-ip

### <a name="step-1"></a>1. Adım

WireShark başlatma

### <a name="step-2"></a>2. Adım

Yük hello **.cap** paket yakalama dosyasından. Bu dosya, yerel olarak üzerinde hello sanal makine içinde kaydedildi hello blob bulunabilir nasıl yapılandırdığınıza bağlı olarak.

### <a name="step-3"></a>3. Adım

tooview Merhaba'TCP konuşmalarında ilk gidiş dönüş süresi (RTT), biz Karşılama ilk iki paketleri hello TCP anlaşması söz konusu adresindeki yalnızca arayacaktır. Biz hello [Eşitlemeye] olan hello ilk iki paketlerinde hello üç yönlü el sıkışması, kullanacağınız [Eşitlemeye, ACK] paketler. Merhaba TCP üstbilgisinde ayarlanan bayraklarının adlandırılır. Merhaba son hello el sıkışması, hello [ACK] paket pakette bu senaryoda kullanılmaz. Merhaba [Eşitlemeye] paket hello istemci tarafından gönderilir. Alındıktan sonra hello sunucu hello [ACK] paket hello Eşitlemeye hello istemciden alma, bir bildirim olarak gönderir. Merhaba sunucu yanıtı çok az ek yük gerektirir hello olgu yararlanarak, biz hello [Eşitlemeye, ACK] paket hello zaman [Eşitlemeye] paket hello istemci tarafından alındı hello zaman çıkarılmasıyla tarafından RTT hello istemci tarafından gönderilen hello hesaplayın.

WireShark kullanarak bu değeri bize hesaplanır.

WireShark tarafından sağlanan yetenek filtreleme hello yararlanacak olan, toomore hello TCP üç yönlü anlaşması kolayca Karşılama ilk iki paketleri görüntüleyin.

tooapply hello WireShark, filtrede Merhaba, yakalama [Eşitlemeye] pakette "İletim Denetimi Protokolü" bölümünü genişletin ve hello TCP üstbilgisinde ayarlanan hello bayrakları inceleyin.

Tüm [Eşitlemeye] üzerinde toofilter arıyoruz beri ve [Eşitlemeye, ACK] bayrakları altında paketleri cofirm hello eşitlemeye bit too1 ayarlayın, sonra sağ tıklayarak hello eşitlemeye bit Filtre -> olarak seçili Uygula ->.

![Şekil 7][7]

### <a name="step-4"></a>4. Adım

Karşılama penceresi tooonly bakın paketleri ile filtrelenmiş göre hello [Eşitlemeye] biti ayarlanmamış, kolayca tooview ilginizi görüşmeleri hello ilk RTT. Basit bir yol tooview hello WireShark RTT tıklamanız yeterlidir "SEQ/ACK" analiz işaretlenmiş hello açılır. Ardından RTT görüntülenen hello görürsünüz. Bu durumda, hello RTT 0.0022114 saniye ya da 2.211 ms idi.

![Şekil 8][8]

## <a name="unwanted-protocols"></a>İstenmeyen protokolleri

Azure üzerinde dağıtılan sanal makine örneği üzerinde çalışan birçok uygulamalar olabilir. Bu uygulamaları birçoğu, belki de açık izniniz olmadan hello ağ üzerinden iletişim kurar. Paket yakalama toostore ağ iletişimi kullanarak, biz nasıl uygulama hello ağda varsayılır ve herhangi bir sorun için Ara araştırabilirsiniz.

Bu örnekte, sizi bir önceki gözden makinenizde çalışan bir uygulama yetkisiz iletişimi gösterebilir istenmeyen protokoller için paket yakalama çalıştı.

### <a name="step-1"></a>1. Adım

Merhaba hello önceki senaryo tıklatın aynı yakalama kullanarak **istatistikleri** > **Protokolü hiyerarşisi**

![protokol hiyerarşi menüsü][2]

Merhaba Protokolü hiyerarşisi penceresi görüntülenir. Bu görünüm hello yakalama oturumu ve aktarılan ve hello protokolleri kullanılarak alınan paket sayısı hello sırasında kullanımda olan tüm hello protokollerin bir listesini sağlar. Bu görünüm, sanal makine ya da ağ üzerindeki istenmeyen ağ trafiğini bulmak için yararlı olabilir.

![açılan iletişim kuralı hiyerarşisini][3]

Ekran yakalama aşağıdaki hello gördüğünüz eş toopeer dosya paylaşımı için kullanılan hello BitTorrent protokolünü kullanarak trafiği vardı. Yönetici olarak toosee BitTorrent trafik bu belirli sanal makinelere beklediğiniz değil. Şimdi, bu trafiğin kullanan, bu sanal makine ya da blok hello üzerinde yüklü hello eş toopeer yazılım kaldırabilirsiniz ağ güvenlik grupları veya bir Güvenlik Duvarı'nı kullanarak trafiği. Ayrıca, hello protokolü kullanmak, sanal makinelere düzenli olarak gözden geçirebilirsiniz şekilde toorun paket yakalamaları bir zamanlamaya göre tercih edebilirsiniz. Bir örneğin nasıl tooautomate ağ azure ziyaret edin görevler üzerinde [izlemek azure automation ile ağ kaynakları](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>En çok kullanılan hedefler ve bağlantı noktalarını bulma

Merhaba trafik türlerini anlama, uç noktaları hello ve hello bağlantı noktaları üzerinden iletişim önemlidir bir izleme veya uygulamaları ve ağınızdaki kaynaklara sorun giderme. Paket yakalama dosyası üstten yararlanarak, biz bizim VM ile iletişim kurduğu ve kullanılan bağlantı noktaları hello hello üst hedefleri hızlı bir şekilde öğrenebilirsiniz.

### <a name="step-1"></a>1. Adım

Merhaba hello önceki senaryo tıklatın aynı yakalama kullanarak **istatistikleri** > **IPv4 istatistikleri** > **hedefleri ve bağlantı noktaları**

![Paket yakalama penceresi][4]

### <a name="step-2"></a>2. Adım

Biz hello sonuçlar görünür olarak bir satır öne çıkması, birden çok bağlantı noktası bağlantı 111 vardı. Uzak Masaüstü olduğu hello en sık kullanılan bağlantı noktası 3389, oluştu ve hello kalan RPC dinamik bağlantı noktalarının.

Bu trafik bir şey olabilir, ancak birçok bağlantıları için kullanılan ve bilinmeyen toohello yönetici haklarına sahip bir bağlantı noktasıdır.

![Şekil 5][5]

### <a name="step-3"></a>3. Adım

Göre Yerleştir bağlantı noktası başlangıç bağlantı noktasını temel alarak bizim yakalama filtre uygulayabilirsiniz yetersiz belirledik.

Bu senaryoda Hello filtresi şöyle olacaktır:

```
tcp.port == 111
```

Biz hello filtre metni üstten hello filtre metin kutusuna girin ve ENTER tuşuna basın.

![Şekil 6][6]

Merhaba sonuçlarından tüm hello trafiği üzerinde hello yerel bir sanal makineden gelen görebiliriz aynı alt ağ. Biz bu trafiği neden oluştuğunu hala anlamadığınız, size daha fazla neden bu bağlantı noktası 111 çağrıları yapma hello paketleri toodetermine inceleyebilirsiniz. Bu bilgiyle biz hello uygun eylemde bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bilgi ziyaret ederek hello Ağ İzleyicisi'nin diğer tanılama özelliklerini hakkında [Azure ağ izlemeye genel bakış](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













