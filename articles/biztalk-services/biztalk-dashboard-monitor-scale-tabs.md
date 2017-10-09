---
title: "aaaDashboard, monitör, Ölçek, yapılandırma ve karma bağlantılar BizTalk Services | Microsoft Docs"
description: "Merhaba denetimleri hakkında bilgi edinin ve izleme hello Klasik portal sekmelerde performans için BizTalk Services: pano, İzleyici, Ölçek, yapılandırma ve karma bağlantılar. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Merhaba Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri gözden geçirin

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

BizTalk hizmeti oluşturma ve uygulamanızı dağıttıktan sonra bazı hello BizTalk hizmeti ayarlarını değiştirin ve hello uygulama performansı izleme. 

Merhaba Klasik Azure portalını açtığınızda, başlangıç sırasında otomatik olarak yerleştirilir **tüm öğeleri** sekmesini tooview BizTalk hizmetinizi seçin, BizTalk hizmetinize hello **tüm öğeleri** sekme veya select hello **BIZTALK SERVICES** sekmesinde; ve ardından, BizTalk hizmeti adını seçin.

Bu sekme aşağıdaki hello ile yeni bir pencere açılır. Bu konuda aşağıdaki sekmelerden açıklanmaktadır.

## <a name="quickstart-quickstartquickstart"></a>Hızlı Başlangıç)![Hızlı Başlangıç][Quickstart])
Merhaba BizTalk Services sürümüne bağlı olarak listelenen tüm seçenekleri kullanılamayabilir. 

<table border="1">
    <tr>
        <td><strong>Merhaba araçları edinin</strong></td>
        <td>Şirket içi geliştirme bilgisayarınızda Hello BizTalk Services SDK'sı tooinstall hello Visual Studio Proje şablonları indirin. Bu şablonlar hello oluşturma <strong>BizTalk Services</strong> (köprü) ve hello <strong>BizTalk hizmeti yapıları</strong> dağıtılan tooyour BizTalk hizmeti olan (dönüştürme) Visual Studio projeleri.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Ne ı Başlat kullanarak hello Azure BizTalk Services SDK'sı </a> ve <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">yükleme hello Azure BizTalk Services SDK'sı</a> listeleri hello adımları tooget başlatıldı.
        </td>
    </tr>
    <tr>
        <td><strong>İş ortağı anlaşmaları oluşturma</strong></td>
        <td>Açılır hello Azure BizTalk Services burada ortakları ekleme ve X12, AS2, oluşturma Azure üzerinde barındırılan portalı ve EDIFACT EDI sözleşmeleri.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> listeleri hello adımları tooget başlatıldı.
        </td>
    </tr>

<tr>
        <td><strong>BizTalk hizmetleri hakkında daha fazla bilgi edinin</strong></td>
        <td>Toohello Git <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">center öğrenme</a> toolearn Azure BizTalk Services hakkında daha fazla bilgi.</td>
</tr>
</table>


Merhaba görev çubuğunda hello altta, şunları yapabilirsiniz:

<table border="1">

<tr>
<td><strong>Yönetme</strong> , uygulama dağıtımı</td>
<td>Hello Azure BizTalk Services portalı açar. Merhaba BizTalk Services portalı olan iş ortakları ekleme ve X12, AS2, oluşturma dahil olmak üzere, hello giriş tooEDI yapılandırma ve EDIFACT sözleşmelerini.
<br/><br/>
Bu olduğu hello aynı <strong>ortak sözleşmeleri oluşturmak</strong> hello üzerinde <strong>Hızlı Başlangıç</strong> sekmesi.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> hello BizTalk Services Portal hakkında daha fazla bilgi sağlar.</td>
</tr>

<tr>
<td><strong>Bağlantı bilgilerini</strong> hello erişim denetimi Namespace,</td>
<td>Bağlantı bilgilerini seçtiğinizde, erişim denetimi Namespace, varsayılan, veren hello ve varsayılan anahtar görüntülenir. Bu değerleri kopyalayabilirsiniz.
<br/><br/>
Merhaba erişim denetimi portalı da açabilirsiniz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Erişim denetimi Namespace oluşturmak</a> hello erişim denetimi portalı üzerinde daha fazla bilgi sağlar.</td>
</tr>

<tr>
<td><strong>Eşitleme anahtarları</strong> hello depolama hesabı,</td>
<td>Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur. Bu şifreleme anahtarları erişim tooyour depolama hesabı denetler. BizTalk hizmeti otomatik olarak hello birincil anahtarı kullanır. <strong>Eşitleme anahtarları</strong> hello BizTalk hizmeti kesintiye uğratmadan hello birincil anahtar hello ikincil anahtar arasındaki kullanıcılar tooswitch etkinleştirin.
<br/><br/>
Örneğin, BizTalk hizmeti toouse hello depolama hesabı için yeni bir birincil anahtar hello istiyorsunuz. toodo bu:
<br/><br/>
<ol>
<li>BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>. Merhaba ikincil anahtarı seçin. Bunu yaptığınızda hello BizTalk hizmeti hello ikincil anahtarı kullanarak başlatır.</li>
<li>Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello birincil anahtarı yeniden oluşturma. BizTalk hizmetinizi hello ikincil anahtarı kullanarak unutmayın.</li>
<li>BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>. Şimdi, hello birincil anahtarı seçin. Bu olduğu hello yeni birincil anahtar, yeniden oluşturulacak.</li>
<li>Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello ikincil anahtarını yeniden oluşturma.</li>
</ol>
<br/>
Bu işlem, "rollover anahtarları" adı verilir. Merhaba tooenable kullanıcılar tooswitch hello birincil anahtar ve ikincil anahtar hello arasında hello BizTalk hizmeti kesintiye uğratmadan amaçtır.</td>
</tr>

<tr>
<td><strong>Silme</strong> uygulamanız</td>
<td>Seçtiğinizde silin, BizTalk hizmeti ve tüm öğeleri dağıtılan tooit kaldırılır.</td>
</tr>
</table>


## <a name="dashboard"></a>Pano
Merhaba BizTalk Services sürümüne bağlı olarak listelenen tüm seçenekleri kullanılamayabilir. 

BizTalk hizmet adınızı seçin, hello Pano sekmesi görüntülenir. Panosunda, şunları yapabilirsiniz:

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Kullanıma genel bakış: kullanılan karma bağlantılar hello sayısını gösterir
Ayrıca hello veri kullanımı GB cinsinden görüntüler. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Ölçüm grafiği: performans ölçümleri sabit bir listesini gösterir
Bu ölçümler hello durumunu hello BizTalk hizmeti ile ilgili gerçek zamanlı değerleri sağlayın. Merhaba de seçebilirsiniz **göreli** veya **mutlak** değerleri ve hello zaman aralığı **aralığı** hello grafiğinde görüntülenen hello ölçümleri. 

Bu performans ölçümleri açıklaması için çok Git[kullanılabilir ölçümler](#Metrics) bu konuda.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Hızlı Bakış: BizTalk hizmeti özelliklerinizi listeler
<table border="1">

<tr>
<td><strong>İzleme veritabanı kimlik bilgileri güncelleştir</strong></td>
<td>Kullanıcı adı değişiklikleri hello ve izleme veritabanı hello toolog kullanılan parolayı.</td>
</tr>
<tr>
<td><strong>SSL sertifikasını güncelleştir</strong></td>
<td>Merhaba BizTalk hizmeti toouse farklı bir SSL sertifikası güncelleştirebilirsiniz. Otomatik olarak imzalanan bir SSL sertifikası otomatik olarak oluşturulur, <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">hello BizTalk hizmeti oluşturma</a>.</td>
</tr>
<tr>
<td><strong>Sertifikayı indirin</strong></td>
<td>BizTalk hizmeti tooa yerel makinenize tarafından kullanılan hello SSL sertifikası yükleyebilirsiniz.</td>
</tr>
<tr>
<td><strong>Durumu</strong></td>
<td>Merhaba, BizTalk hizmetinin geçerli durumunu görüntüler. Bkz: <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Hizmet durumu grafiği</a>. </td>
</tr>
<tr>
<td><strong>Hizmet URL'si</strong></td>
<td>BizTalk hizmeti başlangıç URL'si. Bu olduğu hello aynı hello <strong>etki alanı URL'si</strong> BizTalk hizmeti oluşturulduğunda girildi.</td>
</tr>
<tr>
<td><strong>Genel sanal IP (VIP) adresi</strong></td>
<td>Başlangıç IP adresi tooyour BizTalk hizmeti atanır. Tüm giriş uç noktaları için kullanılır ve giden trafiği hello kaynak adresidir. Oluşturulan sürece bu IP adresi tooyour BizTalk hizmeti aittir. Hello BizTalk hizmeti silerseniz, başlangıç IP adresi tooanother BizTalk hizmeti atanır.</td>
</tr>
<tr>
<td><strong>ACS Namespace</strong></td>
<td>BizTalk hizmeti Hello ile kimliğini doğrular.</td>
</tr>
<tr>
<td><strong>Sürüm</strong></td>
<td>Merhaba BizTalk hizmeti oluşturulduğunda Edition girilen hello listeler.</td>
</tr>
<tr>
<td><strong>Konum</strong></td>
<td>Görüntüler, BizTalk hizmeti barındıran coğrafi bölge hello.</td>
</tr>
<tr>
<td><strong>Oluşturulan</strong></td>
<td>Tarih ve saati görüntüler hello hello BizTalk hizmeti oluşturuldu.</td>
</tr>
<tr>
<td><strong>Veritabanı izleme</strong></td>
<td>BizTalk hizmeti tarafından kullanılan tablolar izleme hello depolar hello Azure SQL veritabanı adı. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Gereksinimleri Explained</a> hello veritabanı izleme hakkında ayrıntılar sağlar.</td>
</tr>
<tr>
<td><strong>Depolama izleme/arşivleme</strong></td>
<td>BizTalk hizmetinizi çıktısını izleme hello depolayan hello Azure depolama hesabı adı.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Gereksinimleri Explained</a> hello depolama hesabı hakkında ayrıntılar sağlar.</td>
</tr>
<tr>
<td><strong>Abonelik adı</strong></td>
<td>BizTalk hizmetinizi barındıran hello abonelik listeler. Merhaba abonelik erişim toohello Klasik Azure portalı yönetir.</td>
</tr>
<tr>
<td><strong>Abonelik kimliği</strong></td>
<td>Bir abonelik kimliği, bir abonelik oluşturduğunuzda, otomatik olarak oluşturulur. REST API kullanırken, tooenter hello abonelik kimliği gerekebilir</td>
</tr>
</table>

[BizTalk Services: Klasik portalı kullanarak Azure sağlama](http://go.microsoft.com/fwlink/p/?LinkID=302280) listeleri hello adımları toocreate BizTalk hizmeti.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>, Bağlantı bilgilerini, eşitleme anahtarları, yönetin ve hello görev çubuğunda silin:
<table border="1">

<tr>
<td><strong>Yönetme</strong> , uygulama dağıtımı</td>
<td>Hello Azure BizTalk Services portalı açar. Merhaba BizTalk Services portalı olan iş ortakları ekleme ve X12, AS2, oluşturma dahil olmak üzere, hello giriş tooEDI yapılandırma ve EDIFACT sözleşmelerini.
<br/><br/>
Bu olduğu hello aynı <strong>ortak sözleşmeleri oluşturmak</strong> hello üzerinde <strong>Hızlı Başlangıç</strong> sekmesi.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> hello BizTalk Services Portal hakkında daha fazla bilgi sağlar.</td>
</tr>
<tr>
<td><strong>Bağlantı bilgilerini</strong> hello erişim denetimi Namespace,</td>
<td>Erişim denetimi Namespace, varsayılan veren ve varsayılan anahtar değerleri görüntüler hello; hangi kopyalanabilir.
<br/><br/>
Merhaba erişim denetimi portalı da açabilirsiniz. Bu erişim denetimi portalı olan hello hello Sol Gezinti Bölmesi'nde hello Active Directory seçeneğini kullanarak aynı.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Bilgisayarınızı ACS Namespace yönetme</a> hello erişim denetimi portalı üzerinde daha fazla bilgi sağlar.</td>
</tr>
<tr>
<td><strong>Eşitleme anahtarları</strong> hello depolama hesabı,</td>
<td>Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur. Bu şifreleme anahtarları erişim tooyour depolama hesabı denetler. BizTalk hizmeti otomatik olarak hello birincil anahtarı kullanır. <strong>Eşitleme anahtarları</strong> hello BizTalk hizmeti kesintiye uğratmadan hello birincil anahtar hello ikincil anahtar arasındaki kullanıcılar tooswitch etkinleştirin.
<br/><br/>
Örneğin, BizTalk hizmeti toouse hello depolama hesabı için yeni bir birincil anahtar hello istiyorsunuz. toodo bu:
<br/><br/>
<ol>
<li>BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>. Merhaba ikincil anahtarı seçin. Bunu yaptığınızda hello BizTalk hizmeti hello ikincil anahtarı kullanarak başlatır.</li>
<li>Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello birincil anahtarı yeniden oluşturma. BizTalk hizmetinizi hello ikincil anahtarı kullanarak unutmayın.</li>
<li>BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>. Şimdi, hello birincil anahtarı seçin. Bu olduğu hello yeni birincil anahtar, yeniden oluşturulacak.</li>
<li>Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello ikincil anahtarını yeniden oluşturma.</li>
</ol>
<br/>
Bu işlem, "rollover anahtarları" adı verilir. Merhaba tooenable kullanıcılar tooswitch hello birincil anahtar ve ikincil anahtar hello arasında hello BizTalk hizmeti kesintiye uğratmadan amaçtır.</td>
</tr>

<tr>
<td><strong>Silme</strong> uygulamanız</td>
<td>BizTalk hizmeti ve tüm öğeleri dağıtılan tooit kaldırılır.</td>
</tr>
</table>


## <a name="monitor"></a>İzleme
Toohello uygulanmaz ücretsiz sürüm.

BizTalk hizmet adınızı seçtiğinizde hello İzleyici sekmesi kullanılabilir ve hello şunları görüntüler:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Ölçüm grafiği: Performans ölçümleri görüntüler hello seçili
Bu ölçümler hello durumunu hello BizTalk hizmeti ile ilgili gerçek zamanlı değerleri sağlayın. Hangi performans ölçümleri görüntülenen seçin. En fazla altı performans ölçümleri eşzamanlı olarak görüntülenebilir. 

Merhaba de seçebilirsiniz **göreli** veya **mutlak** değerleri ve hello zaman aralığı **aralığı** görüntülenen hello ölçümleri. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>Merhaba grafikte tooremove veya görüntü ölçümleri:
1. Select hello **İzleyici** sekmesi.
2. Seçin **ölçüm Ekle** hello görev çubuğunda:  
   ![Select ölçüm Ekle][AddMetrics]
3. Merhaba performans ölçümleri toodisplay istediğiniz denetleyin.
4. Merhaba onay işareti tooreturn toohello seçin **İzleyici** sekmesi.
5. Merhaba daire sonraki toohello ölçüm toodisplay hello grafiğinde, ölçüm ait değer seçin.  
   
    Örneğin, hello **CPU kullanımı** çıkışı ölçüm gri; çıktısını hello grafik olarak gösterilmez:  
   ![CPU kullanım ölçüm gri][GrayedMetric]  
   
    Select hello gri daire tooenable hello **CPU kullanımı** ölçüm toodisplay çıktısını hello grafikte:  
   ![CPU kullanım ölçüm etkin][EnabledMetric]
6. tooremove hello görünen grafik ve hello listesinde, bir ölçüm seçin **silmek ölçüm** hello görev çubuğunda. tooadd hello ölçüm geri toohello listesinden, **ölçüm Ekle** hello görev çubuğunda hello ölçüm Seç hello onay işareti tooreturn toohello denetleyip **İzleyici** sekmesi. Select hello daire tooenable hello seçilemez ölçüm.

## <a name="Metrics"></a>Kullanılabilir ölçümler
performans sayaçları/ölçümleri aşağıdaki hello kullanılabilir:

<table border="1">

<tr>
<td><strong>RountdTrip gecikme süresi</strong></td>
<td>Merhaba ortalama süre (ms) tooprocess selamlama iletisine tam olarak tüm köprüleri arasında hello BizTalk hizmeti tarafından işlenen kadar hello zaman hello iletisi bir ileti alındığında milisaniye cinsinden geçen görüntüler. Başarıyla işlenen iletiler kabul edilir.<br/><br/>
Bir zaman damgası, olayları aşağıdaki hello oluştuğunda oluşturulur:
<ul>
<li>İleti hello ağ geçidi girer.</li>
<li>Yönlendirilmiş toohello hedef iletisidir</li>
<li>Hedef yanıtı aldı</li>
<li>Hedef bildirim gönderilen yanıtı toohello ağ geçidi</li>
</ul>
<br/>
Bu ölçüm, hesaplama aşağıdaki hello hello sonucunu gösterir:
<br/><br/>
[Hedef bildirim gönderilen yanıtı toohello ağ geçidi] - [ileti girer hello ağ geçidi]</td>
</tr>
<tr>
<td><strong>Kaynaktaki hataları</strong></td>
<td>Merhaba başarısız iletilerin toplam sayısını görüntüler hello hello kaynak uç noktaları iletilerden çekme BizTalk hizmet tarafından.</td>
</tr>
<tr>
<td><strong>CPU kullanımı</strong></td>
<td>Merhaba ortalama % işlemci zamanı, tüm rol örneği listeler.</td>
</tr>
<tr>
<td><strong>İşleme gecikmesi</strong></td>
<td>Bir ileti hello zaman hariç tüm köprüleri arasında hello BizTalk hizmeti tarafından varış yeri için harcanan milisaniye (ms) tooprocess alınan hello ortalama süreyi görüntüler. Başarıyla işlenen iletiler kabul edilir.<br/><br/>
Olayları aşağıdaki hello her oluştuğunda bir zaman damgası oluşturulur:

<ul>
<li>İleti hello ağ geçidi girer.</li>
<li>Yönlendirilmiş toohello hedef iletisidir</li>
<li>Hedef yanıtı aldı</li>
<li>Hedef bildirim gönderilen yanıtı toohello ağ geçidi</li>
</ul>
<br/>Bu ölçüm, hesaplama aşağıdaki hello hello sonucunu gösterir:<br/><br/>
[Hedef bildirim gönderilen yanıtı toohello ağ geçidi] - [ileti girer hello ağ geçidi] - [hedef yanıt alındığında] + [ileti yönlendirilmiş toohello hedef]</td>
</tr>
<tr>
<td><strong>İşlemdeki hataları</strong></td>
<td>Merhaba işleme sırasında tüm hello köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığında başarısız iletilerin toplam sayısını görüntüler.</td>
</tr>
<tr>
<td><strong>Gönderilen iletileri</strong></td>
<td>Tüm köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığı içinde gönderilen iletilerin toplam sayısını görüntüler hello. Bu ölçüm, ardışık düzen tarafından gönderilen bir ileti hello rota hedef ulaştığında artırılır. Bu ölçüm, bir ileti başarıyla işlendi göstermez.<br/><br/>
Merhaba rota hedef giriş bildirim geri toohello ardışık gönderdiğinde istek-yanıt senaryoda hello ölçüm artırılır.</td>
</tr>
<tr>
<td><strong>Alınan iletileri</strong></td>
<td>Tüm köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığı içinde alınan iletilerin toplam sayısını görüntüler hello. Bu ölçüm, yeni bir ileti hello ardışık düzen tarafından alındığında artırılır.</td>
</tr>
<tr>
<td><strong>İşlemindeki iletiler</strong></td>
<td>Bir zaman aralığı içinde hello BizTalk hizmeti tarafından işlenmekte olan iletilerin toplam sayısını görüntüler hello.</td>
</tr>
<tr>
<td><strong>İşlenen iletileri</strong></td>
<td>Görüntüler başarıyla tüm köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığı içinde işlenen iletilerin toplam sayısı hello. Bu ölçüm, bir ileti başarıyla hello ardışık düzen ve başarıyla yönlendirilmiş toohello hedef tarafından alındığında artırılır.</td>
</tr>
</table>


## <a name="scale"></a>Ölçek
Hello ölçek sekmesinde, ekleyin veya BizTalk hizmeti tarafından kullanılan birim sayısını hello çıkarın. Varsayılan olarak, yoktur birim yapılandırılmış bir. Ek birimler tooscale eklenebilir, BizTalk hizmeti. Merhaba ölçek artırdığınızda, üretilen iş artmaktadır. Hello kaynakları da, dağıtılan köprüleri, anlaşmalar, LOB bağlantıları dahil olmak üzere ve işlemci gücü artar. Örneğin, 1 birim too2 birimlerinden hello ölçeği artırın. Bu durumda, çift hello sayısı köprüleri, çift hello anlaşmaları, çift hello LOB bağlantıları ve çift hello işleme gücünü dağıtabilirsiniz.

Bazı BizTalk sürümleri Ölçek seçeneği sağlamaz. Bu durumda, tek bir birim izin verilir. toodetermine sürümünüz ölçeklendirilmiş, kaç tane birimleri başvurmak çok[BizTalk Services: sürümler grafiği](biztalk-editions-feature-chart.md).

Birimleri Hello sayısını artırmayı fiyatlandırmayı etkileyebilir. Merhaba birimleri artırırsanız, seçme **kaydetmek** faturalama etkilenen olmadığını bildiren bir ileti görüntüler. Ardından, toocontinue de seçin. Hello birim sayısını artırdığınızda, Active tooUpdating hello BizTalk hizmeti durumunu değiştirir. Hello güncelleştirme durumu, BizTalk hizmeti toorun devam eder.

[BizTalk Services: Sürümler grafiği](biztalk-editions-feature-chart.md) "Birim" tanımlar.

## <a name="configure"></a>Yapılandırma
TooHybrid bağlantıları için geçerli değildir.

Merhaba yedekleme durumu tooNone veya otomatik olarak ayarlar. TooNone, ayarlandığında yedekleme otomatik olarak oluşturulur. TooAutomatic, ayarlandığında hello yedekleme konumu, hello yedekleme ve ne kadar süreyle tookeep hello yedekleme dosyalarını hello sıklığını yapılandırın. 

[BizTalk Services: Yedekleme ve geri yükleme](biztalk-backup-restore.md) hello ayrıntıları sağlar. 

## <a name="HybridConnections"></a>Karma bağlantılar
Karma bağlantılar Azure uygulaması, Web uygulamaları veya Mobile Apps Azure App Service'te bir statik TCP bağlantı noktası, SQL Server, MySQL, HTTP Web API'leri ve en özel Web Hizmetleri gibi kullanan tooan şirket içi kaynağa gibi bağlanın. Karma bağlantılar BizTalk Services'da hello Klasik Azure portalı yönetilir.

Karma bağlantılar Azure App Service'te toocreate bkz [erişim şirket içi Azure App Service içinde karma bağlantılar kullanarak kaynakları](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate veya karma bağlantılar Azure BizTalk Services yönetmek için bkz: [karma bağlantılar](integration-hybrid-connection-overview.md).

## <a name="next"></a>Sonraki
Merhaba farklı sekmelerle tanıdık, hello Azure BizTalk Services özellikleri hakkında daha fazla bilgi edinebilirsiniz:

* [BizTalk Services: Azaltma](biztalk-throttling-thresholds.md)  
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](biztalk-issuer-name-issuer-key.md)  
* [BizTalk Services: Yedekleme ve Geri Yükleme](biztalk-backup-restore.md)

## <a name="see-also"></a>Ayrıca Bkz.
* [Karma Bağlantılar](integration-hybrid-connection-overview.md)  
* [BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği](biztalk-editions-feature-chart.md)  
* [BizTalk Services: Klasik portalı kullanarak Azure hazırlama](biztalk-provision-services.md)  
* [BizTalk Services: BizTalk hizmeti durumu grafiği](biztalk-service-state-chart.md)  
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

