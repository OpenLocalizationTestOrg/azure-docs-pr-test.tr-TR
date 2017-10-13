---
title: "BizTalk Services sürümleri özellikleri hakkında bilgi edinme| Microsoft Belgeleri"
description: "BizTalk Services sürümlerinin özelliklerini karşılaştırın: Ücretsiz, Geliştirici, Temel, Standart ve Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 718b57a801a9ba62a0154ae42da2ac0c0741f203
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="biztalk-services-editions-chart"></a>BizTalk Services: Sürümler grafiği

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services çeşitli sürümler sunar. Bu makaleyi senaryonuz ve iş gereksinimleriniz için hangi sürümün doğru olduğunu saptamak için kullanın.

## <a name="compare-the-editions"></a>Sürümleri karşılaştırma
**Ücretsiz (Önizleme)**

Karma Bağlantılar oluşturabilir ve yönetebilir. Karma Bağlantı, Azure web sitesini SQL Sunucusu gibi şirket içi bir sisteme bağlamanın kolay yoludur.

**Geliştirici**

Karma Bağlantılar, kolay kullanılan ticari ortak yönetim portalıyla EAI ve EDI ileti işleme, ortak EDI şemaları için destek, X12 ve AS2 üzerinde zengin EDI işlemeyi kapsar. İleti okumak ve yazmak için. buluttaki hizmetleri HTTP/S, REST, FTP, WCF ve SFTP protokolleriyle bağlayan ortak EAI senaryoları oluşturabilir.  Şirket içi LOB sistemlerini kullanıma hazır SAP, Oracle eBusiness, Oracle DB, Siebel, ve SQL Sunucusu bağdaştırıcılarıyla bağlantıyı kullanır. Geliştirici merkezli ortamı, kolay geliştirme ve dağıtım için Visual Studio araçlarıyla birlikte kullanın. Geliştirme ve test amaçları Hizmet Düzeyi Sözleşmesi (SLA) olmadıkça sınırlıdır

**Temel**

Çoğu Geliştiricinin yeteneklerini, Karma Bağlantılar, EAI köprüleri, EDI Sözleşmeleri ve BizTalk Bağdaştırıcı Paketi bağlantılarındaki yükselişe ekler. Ayrıca, yüksek kullanılabilirlik ve Hizmet Düzeyi Sözleşmesi (SLA) ile ölçeklendirme seçeneği sunar.

**Standart**

Tüm Temel yetenekleri, Karma Bağlantılar, EAI köprüleri, EDI Sözleşmeleri ve BizTalk Bağdaştırıcı Paketi bağlantılarındaki yükselişe ekler. Ayrıca, yüksek kullanılabilirlik ve Hizmet Düzeyi Sözleşmesi (SLA) ile ölçeklendirme seçeneği sunar.

**Premium**

Tüm Standart yetenekleri, Karma Bağlantılar, EAI köprüleri, EDI Sözleşmeleri ve BizTalk Bağdaştırıcı Paketi bağlantılarındaki yükselişe ekler. Ayrıca, arşivleme, yüksek kullanılabilirlik ve Hizmet Düzeyi Sözleşmesi (SLA) ile ölçeklendirme seçeneği içerir.

## <a name="editions-chart"></a>Sürümler grafiği
Aşağıdaki tabloda farklar listelenmektedir:

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Ücretsiz (Önizleme)</th>
        <th>Geliştirici</th>
        <th>Temel</th>
        <th>Standart</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Başlangıç fiyatı</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Azure BizTalk Services Fiyatlandırması</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full"> Azure Fiyatlandırma Hesaplayıcısı</a></td>
</tr>
<tr>
<td><strong>Varsayılan en düşük yapılandırma</strong></td>
<td>1 Ücretsiz Birim</td>
<td>1 Geliştirici Birimi</td>
<td>1 Temel Birim</td>
<td>1 Standart Birim</td>
<td>1 Premium Birim</td>
</tr>
<tr>
<td><strong>Ölçeklendirme</strong></td>
<td>Ölçek yok</td>
<td>Ölçek yok</td>
<td>Evet, 1 Temel birim artışlarıyla</td>
<td>Evet, 1 Standart birim artışlarıyla</td>
<td>Evet, 1 Premium birim artışlarıyla</td>
</tr>
<tr>
<td><strong>İzin verilen ölçek genişletme üst sınırı</strong></td>
<td>Ölçek yok</td>
<td>Ölçek yok</td>
<td>8 Birime Kadar</td>
<td>8 Birime Kadar</td>
<td>8 Birime Kadar</td>
</tr>
<tr>
<td><strong>Birim başına EAI Köprü sayısı</strong></td>
<td>Dahil değil</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
TPM sözleşmeleri dahil</td>
<td>Dahil değil</td>
<td>Dahil. Birim başına 10 sözleşme.</td>
<td>Dahil. Birim başına 50 sözleşme.</td>
<td>Dahil. Birim başına 250 sözleşme.</td>
<td>Dahil. Birim başına 1000 sözleşme.</td>
</tr>
<tr>
<td><strong>Birim başına Karma Bağlantılar</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Birim başına Karma Bağlantı Veri Aktarımı (GB)</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Şirket içi LOB sistemlerine yönelik BizTalk Bağdaştırıcı Hizmeti bağlantıları</strong></td>
<td>Dahil değil</td>
<td>1 bağlantı</td>
<td>2 bağlantı</td>
<td>5 bağlantı</td>
<td>25 bağlantı</td>
</tr>
<tr>
<td align="left"><strong>Desteklenen protokoller/Sistemler:</strong>
<ul>
<li>HTTP</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Service Bus (SB)</li>
<li>Azure Blob</li>
<li>REST API'leri</li>
</ul>
</td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
</tr>
<tr>
<td><strong>Yüksek düzey kullanılabilirlik</strong>
<br/><br/>
Hizmet Düzeyi Sözleşmesi (SLA) için bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Azure BizTalk Services Fiyatlandırması</a>.
</td>
<td>Dahil değil</td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
</tr>
<tr>
<td><strong>Yedekleme ve geri yükleme</strong></td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
</tr>
<tr>
<td><strong>İzleme</strong></td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
</tr>
<tr>
<td><strong>Arşivleme</strong><br/><br/>
İnkar Edilemez Makbuz (NRR) ve izlenen iletilerin indirilmesi dahildir</td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil Değil</td>
<td>Dahil Değil</td>
<td>Dahil</td>
</tr>
<tr>
<td><strong>Özel kod kullanımı</strong></td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
</tr>
<tr>
<td><strong>Özel XSLT de dahil olmak üzere dönüşüm kullanımı</strong></td>
<td>Dahil değil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
<td>Dahil</td>
</tr>
</table>

> [!NOTE]
> Donanım arızalarına karşı dayanıklılık için, Yüksek Kullanılabilirlik tek bir BizTalk Biriminde birden çok VM olduğu anlamına gelir.
> 
> 

## <a name="faqs"></a>SSS
#### <a name="what-is-a-biztalk-unit"></a>BizTalk birimi nedir?
"Birim", Azure BizTalk Services dağıtımının atomik düzeyidir. Her sürüm, farklı işlem kapasitesi ve belleğe sahip bir birimle birlikte verilir. Örneğin, Temel birimde Geliştirici’ye göre daha fazla işlem varken, Standart’ta da Temel’e göre daha fazla işlem vardır vb. BizTalk Hizmetini ölçeklendirdiğinizde birimler cinsinden ölçeklendirirsiniz.

#### <a name="what-is-the-difference-between-biztalk-services-and-azure-biztalk-vm"></a>BizTalk Services ve Azure BizTalk VM arasındaki fark nedir?
BizTalk Services, bulutta yapı tümleştirme çözümleri için doğru hizmet olarak platform (PaaS) mimarisini sağlar. PaaS modeliyle, tamamen uygulama mantığına odaklanır ve tüm altyapı yönetimini Microsoft'a bırakırsınız; buna şunlar dahildir:

* Sanal makineleri yönetme ve düzeltme eki gerekmez.
* Microsoft kullanılabilirliği sağlar.
* Azure Portalı aracılığıyla yalnızca daha az veya daha çok kapasite isteyerek İsteğe bağlı ölçeği denetlersiniz.

Azure Virtual Machines’deki BizTalk Server hizmet olarak altyapı (IaaS) mimarisi sağlar. Kod değişikliğine gerek kalmadan bulutta mevcut uygulamaların çalışmasını kolaylaştırarak sanal makineler oluşturup bunları tam da şirket içi ortamda olduğu gibi yapılandırırsınız. IaaS ile, sanal makinelerin yapılandırılmasından, sanal makinelerin yönetilmesinden (örneğin, yazılım yükleme ve OS düzeltme ekleri), yüksek kullanılabilirlik için uygulama mimarisinden sorumlu olmayı sürdürürsünüz.

Altyapı yönetimi çabanızı en aza indiren yeni tümleştirme çözümlerini derlemeye bakarsanız, BizTalk Services'ni kullanın. Mevcut BizTalk çözümlerinizi hızlı geçirmeye bakıyorsanız ya da BizTalk Server uygulamalarını geliştirmek ve test etmek için isteğe bağlı ortam arıyorsanız, Azure Sanal Makinede BizTalk Server’ı kullanın.

#### <a name="what-is-the-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>BizTalk Bağdaştırıcı Hizmeti ve Karma Bağlantılar arasındaki fark nedir?
BizTalk Bağdaştırıcı Hizmeti bir Azure BizTalk Hizmeti tarafından kullanılır. BizTalk Bağdaştırıcı Hizmeti, BizTalk Bağdaştırıcı Paketini şirket içi iş kolu (LOB) sistemine bağlamak için kullanır. Karma Bağlantı, Azure App Service’de ve Azure Mobile Services’da Web Uygulamaları özelliği gibi Azure uygulamalarını şirket içi kaynağa bağlamak için kolay ve uyumlu bir yol sağlar.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-the-limit-is-reached"></a>“Birim başına Karma Bağlantı Veri Aktarımı (GB)” ne anlama geliyor? Bu dakika/saat/gün/hafta/ay mı? Sınıra ulaşıldığında ne olur?
Birim başına Karma Bağlantı maliyeti BizTalk Services sürümüne bağlıdır. Basitçe, maliyetler ne kadar veri aktarımı yaptığınıza bağlıdır. Örneğin, günde 10 GB veri aktarmanın maliyeti günde 100 GB veri aktarmanın maliyetinden daha düşüktür. Belirli maliyetleri saptamak için BizTalk Services’da [Fiyatlandırma Hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/?scenario=full) kullanın. Sınırlar genellikle günlüktür. Sınırı aşarsanız, aşmalar GB başına 1 USD oranında ücretlendirilir.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-the-number-of-bridges-go-up-by-two-instead-of-just-one"></a>BizTalk Services’da sözleşme oluşturduğumda neden köprü sayısı bir yerine ikiye yükseliyor?
Her sözleşme iki farklı köprüden oluşur: gönderme tarafı iletişim köprüsü ve alma tarafı iletişim köprüsü.

#### <a name="what-happens-when-i-hit-the-quota-limit-on-the-number-of-bridges-or-agreements"></a>Köprü sayısına veya sözleşmeye göre kota sınırına ulaştığımda ne olur?
Yeni köprüleri dağıtamaz veya yeni sözleşmeler oluşturamazsınız. Daha fazla dağıtmak için, BizTalk hizmetinin ölçeğini daha fazla birime yükseltmelisiniz ya da daha yüksek bir sürüme geçmelisiniz.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-to-another"></a>BizTalk Services’ın bir katmanından diğerine nasıl geçerim?
Ücretsiz sürüm başka bir katmana geçemez veya 'yukarı ölçeklendirilemez' ve başka bir katmana yedeklenemez ve geri yüklenemez. Başka bir katman gerekiyorsa, yeni katmanı kullanarak yeni bir BizTalk Hizmeti oluşturun. Karma bağlantılar da dahil, Ücretsiz sürüm kullanılarak oluşturulan yapıtların yeni BizTalk Hizmetinde yeniden oluşturulması gerekir. 

Diğer sürümler için, bir katmandan diğerine yapıtları geçirmek için geçiş için yedeklemeyi ve geri yüklemeyi kullanın. Örneğin, standart katmanındaki yapıtlarınızı yedekleyin, sonra da bunları Premium katmanına geri yükleyin. [BizTalk Services: Yedekleme ve Geri Yükleme](biztalk-backup-restore.md) desteklenen geçiş yollarını açıklar ve hangi yapıtların yedeklendiğini listeler. Karma Bağlantıların yedeklenmediğini unutmayın. Yeni katmana yedekleyip geri yükledikten sonra karma bağlantıları yeniden oluşturun.  

#### <a name="is-the-biztalk-adapter-service-included-in-the-service-how-do-i-receive-the-software"></a>BizTalk Bağdaştırıcı Hizmeti hizmette mi? Yazılım nasıl alırım?
Evet, BizTalk Bağdaştırıcı Paketi bulunan BizTalk Bağdaştırıcısı Hizmeti Azure BizTalk Services SDK [indirmede](http://www.microsoft.com/download/details.aspx?id=39087) bulunur.

## <a name="next-steps"></a>Sonraki adımlar
Azure portalında Azure BizTalk hizmetleri oluşturmak için [BizTalk Services: Azure portalını kullanarak hazırlama](biztalk-provision-services.md)’ya gidin. Uygulamalar oluşturmaya başlamak için [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197)’a gidin.

## <a name="additional-resources"></a>Ek kaynaklar
* [BizTalk Services: Azure portalını kullanarak hazırlama](biztalk-provision-services.md)<br/>
* [BizTalk Services: Durum Grafiğini hazırlama](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Yedekleme ve Geri Yükleme](biztalk-backup-restore.md)<br/>
* [BizTalk Services: Azaltma](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](biztalk-issuer-name-issuer-key.md)<br/>
* [Azure BizTalk Services SDK'sını Kullanmaya Nasıl Başlarım](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

