---
title: "aaaVisualizing Azure ağ güvenlik grubu akış günlükleri Power BI ile | Microsoft Docs"
description: "Bu sayfa toovisualize NSG akış Power BI ile nasıl günlüğe yazacağını açıklar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Power BI ile visualizing ağ güvenlik grubu akış günlükleri

Ağ güvenlik grubu akış günlükleri, ağ güvenlik grupları hakkında giriş ve çıkış IP trafiği tooview bilgi sağlar. Bu akış günlükleri giden Göster ve gelen akış kuralı başına temelinde hello NIC hello akış, 5-tanımlama grubu ve hakkında bilgi hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) hello trafiğine izin verilen veya reddedilen varsa uygular.

Merhaba günlük dosyalarını el ile arama yaparak veri günlüğü akış zor toogain fikir olabilir. Bu makalede, bir çözüm toovisualize en son akışınız günlüğe kaydeder ve ağınızdaki trafiği hakkında bilgi sağlar.

## <a name="scenario"></a>Senaryo

Senaryo aşağıdaki hello hello havuzu olarak bizim akış NSG günlüğü verilerini yapılandırdıktan Power BI Masaüstü toohello depolama hesabı bağlayın. Biz tooour depolama hesabı bağlandıktan sonra Power BI indirir ve hello günlükleri tooprovide görsel bir ağ güvenlik grupları tarafından günlüğe hello trafiği ayrıştırır.

Merhaba görselleri inceleyebilirsiniz hello şablonunda sağlanan kullanma:

* Üst Talkers
* Akış zaman serisi veri yönü ve kural karar tarafından
* Ağ arabirimi MAC adresiyle akışlar
* NSG ve kural tarafından akışlar
* Hedef bağlantı noktası tarafından akışlar

tooadd yeni veri, görselleri, değiştirin ya da sorgular toosuit gereksinimlerinizi Düzenle sağlanan hello düzenlenebilir şablonudur.

## <a name="setup"></a>Kurulum

Başlamadan önce ağ güvenlik grubu akış hesabınızda bir veya daha çok ağ güvenlik grupları etkin günlüğü olması gerekir. Akış günlükleri ağ güvenliği etkinleştirme yönergeleri için aşağıdaki makaleye bakın toohello bakın: [ağ güvenlik grupları için giriş tooflow günlüğü](network-watcher-nsg-flow-logging-overview.md).

Ayrıca boş alanı, depolama hesabınız var, makine toodownload ve yük hello günlüğü verilerini makinenizde ve yeterli hello Power BI Desktop istemcisinin yüklü olması gerekir.

![Visio diyagramı][1]

### <a name="steps"></a>Adımlar

1. Karşıdan yükleme ve hello Power BI Desktop uygulamasını Power BI şablonda aşağıdaki açık hello [Ağ İzleyicisi Powerbı akış günlükleri şablonu](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Gerekli hello sorgu parametrelerini girin
    1. **StorageAccountName** – belirtir toohello içeren hello NSG akış günlükleri hello depolama hesabının adını ve gibi tooload görselleştirin.
    1. **NumberOfLogFiles** – Merhaba, gibi toodownload ve Power BI'da görselleştirin, günlük dosyası sayısını belirtir. Örneğin, 50 belirtilirse, en son 50 günlük dosyalarını hello. 2 Nsg'ler sahibiz ff etkin ve toosend NSG akış günlükleri toothis hesabı yapılandırılmış sonra hello günlüklerinin son 25 saat görüntülenebilir.

    ![Power BI ana][2]

1. Merhaba, depolama hesabının erişim anahtarı girin. Geçerli erişim tuşları hello Azure portal ve seçme tooyour depolama hesabında giderek bulabileceğiniz **erişim tuşları** hello ayarları menüsünden. Tıklatın **Bağlan** değişiklikler uygulanır.

    ![Erişim tuşları][3]

    ![erişim tuşu 2][4]

4.  Günlüklerinizi indirmek durumda, ayrıştırılmış ve şimdi hello önceden oluşturulmuş görselleri kullanabilir.

## <a name="understanding-hello-visuals"></a>Merhaba görselleri anlama

Şablon Hello olması koşuluyla Yardım görselleri kümesi hello NSG akış günlük verilerini duygusu olun. Merhaba aşağıdaki görüntüleri hangi hello Pano verilerle doldurmuş zaman benzer, bir örnek göstermektedir. Daha ayrıntılı her görsel aşağıda inceleyeceğiz 

![powerbı][5]
 
Merhaba üst visual gösterir IP'leri hello başlatılan Talkers çoğu bağlantı belirtilen dönem hello hello. Merhaba kutuları Hello boyutunu toohello göreli bağlantıları sayısına karşılık gelir. 

![toptalkers][6]

Merhaba aşağıdaki zaman serisi grafikleri hello süre boyunca akışları hello sayısını gösterir. Merhaba üst grafik hello akış yönü tarafından ayrılmış ve hello alt (izin verme veya reddetme) yapılan hello karar tarafından ayrılmış. Bu görsel ile trafiği eğilimleri zaman içinde inceleyin ve herhangi bir anormal ani nokta veya trafiği veya trafiği segmentasyonunun reddedin.

![flowsoverperiod][7]

Merhaba aşağıdaki grafikleri hello akışları akış yönü tarafından kesimli hello üst ve alt hello tarafından yapılan karar bölümlenmiş sahip ağ arabirimi başına gösterir. Bu bilgiyle iletilen Vm'leriniz hangisinin çoğu göreli tooothers hello ve trafik tooa belirli VM yüklenmekte olan kazanmadan izin verilen veya reddedilen.

![flowspernic][8]

Halka tekerleği grafiği aşağıdaki hello hedef bağlantı noktası tarafından akışları dökümünü gösterir. Bu bilgi ile belirtilen hello içinde kullanılan en yaygın olarak kullanılan hello hedef bağlantı noktaları görüntüleyebilirsiniz Süresi.

![Halka][9]

Merhaba aşağıdaki çubuk grafik hello akış NSG ve kural tarafından gösterir. Bu bilgiyle, hello Nsg'ler Merhaba sorumlu çoğu trafiği ve trafik hello dökümünü üzerinde bir NSG kural tarafından görebilirsiniz.

![barchart][10]
 
Merhaba aşağıdaki bilgi grafikler hakkında bilgi görüntüler hello Nsg'ler hello günlüklerinde sunmak, hello dönemi ve yakalanan hello erken günlük hello tarihi yakalanan akışlarının sayısı hello. Bu bilgiler, hangi Nsg'ler hakkında bir fikir günlüğe kaydedilen ve akışlar tarih aralığını hello sağlar.

![infochart1][11]

![infochart2][12]

Bu şablon içerir dilimleyiciler tooallow en ilgi tooview hello veriler yalnızca hello. Kaynak grupları, Nsg'ler ve kuralları filtreleyebilirsiniz. Ayrıca, 5-tanımlama bilgileri, karar ve hello günlük yazıldığı hello zaman filtreleyebilirsiniz.

![dilimleyicileri][13]

## <a name="conclusion"></a>Sonuç

Bu senaryoda Ağ İzleyicisi'ni ve Power BI tarafından sağlanan ağ güvenlik grubu akış günlükleri'ni kullanarak, biz mümkün toovisualize ve hello trafiği anlamak olduğundan gösterdi. Sağlanan hello şablonunu kullanarak, Power BI hello günlükleri doğrudan depolama biriminden yükler ve yerel olarak işler. Geçen süre tooload hello şablon istenen dosyaları hello sayısına bağlı olarak değişir ve dosyaların toplam boyutu yüklenir.

Bu şablon, gereksinimleriniz için ücretsiz toocustomize eşitleyerek. Ağ güvenlik grubu akış günlükleri ile Power BI kullanabileceğiniz birçok pek çok yolu vardır. 

## <a name="notes"></a>Notlar

* Günlükler varsayılan olarak depolanır`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Diğer verileri başka bir dizinde olup olmadığını sorgular toopull hello ve işlem hello verileri değiştirilmesi gerekir.

* sağlanan hello şablonu 1 GB'den fazla günlükleri ile kullanım için önerilmez.

* Günlükleri, büyük bir miktarını varsa, Data Lake veya SQL server gibi başka bir veri deposunu kullanan bir çözüm araştırmanız önerilir.

## <a name="next-steps"></a>Sonraki Adımlar

Toovisualize NSG akışınız hello Elastick yığını ile ziyaret ederek nasıl oturum öğrenin [açık kaynaklı araçları kullanarak, Vm'lerden gelen ağ trafiği desenlerini tooand Görselleştirme](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
