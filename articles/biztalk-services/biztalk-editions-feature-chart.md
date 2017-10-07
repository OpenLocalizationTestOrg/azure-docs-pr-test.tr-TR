---
title: "BizTalk Services sürümleri özellikleri hakkında aaaLearn | Microsoft Docs"
description: "Merhaba hello BizTalk Services sürümlerinin özelliklerini karşılaştırın: ücretsiz, geliştirici, temel, standart ve Premium. MABS, WABS."
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
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>BizTalk Services: Sürümler grafiği

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services çeşitli sürümler sunar. Bu makale toodetermine hangi sürümünün senaryonuz ve iş gereksinimleriniz için doğru kullanın.

## <a name="compare-hello-editions"></a>Merhaba sürümlerini karşılaştırın
**Ücretsiz (Önizleme)**

Karma Bağlantılar oluşturabilir ve yönetebilir. Kolay bir yolu tooconnect bir Azure Web sitesi tooan sistemi, SQL Server gibi şirket içi bir karma bağlantıdır.

**Geliştirici**

Karma Bağlantılar, kolay kullanılan ticari ortak yönetim portalıyla EAI ve EDI ileti işleme, ortak EDI şemaları için destek, X12 ve AS2 üzerinde zengin EDI işlemeyi kapsar. Tüm HTTP/S, REST, FTP, WCF ve SFTP protokolleri tooread ile Merhaba bulut Hizmetleri'nde bağlayan ortak EAI senaryoları oluşturabilir ve iletileri yazma.  Bağlantı tooon içi LOB sistemlerini kullanıma hazır SAP, Oracle eBusiness, Oracle DB, Siebel ve SQL sunucusu bağdaştırıcılarıyla kullanın. Geliştirici merkezli ortamı, kolay geliştirme ve dağıtım için Visual Studio araçlarıyla birlikte kullanın. Sınırlı toodevelopment ve test amaçları yalnızca olan hiçbir hizmet düzeyi sözleşmesi (SLA).

**Temel**

Çoğu hello geliştiricinin yeteneklerini, karma bağlantılar, EAI köprüleri, EDI sözleşmeleri ve BizTalk bağdaştırıcı paketi bağlantılarındaki yükselişe ekler. Aynı zamanda yüksek kullanılabilirlik ve hello seçeneği tooscale bir hizmet düzeyi sözleşmesi (SLA) ile sağlar.

**Standart**

Tüm hello temel yetenekleri, karma bağlantılar, EAI köprüleri, EDI sözleşmeleri ve BizTalk bağdaştırıcı paketi bağlantılarındaki yükselişe ekler. Aynı zamanda yüksek kullanılabilirlik ve hello seçeneği tooscale bir hizmet düzeyi sözleşmesi (SLA) ile sağlar.

**Premium**

Tüm hello standart yetenekleri, karma bağlantılar, EAI köprüleri, EDI sözleşmeleri ve BizTalk bağdaştırıcı paketi bağlantılarındaki yükselişe ekler. Ayrıca, arşivleme, yüksek kullanılabilirlik ve hello seçeneği tooscale bir hizmet düzeyi sözleşmesi (SLA) ile içerir.

## <a name="editions-chart"></a>Sürümler grafiği
Merhaba aşağıdaki tabloda hello farklar listelenmektedir.

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
<td>Too8 birimler</td>
<td>Too8 birimler</td>
<td>Too8 birimler</td>
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
<td><strong>BizTalk bağdaştırıcı hizmeti bağlantıları tooon içi LOB sistemlerini</strong></td>
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
"Birim" Merhaba Azure BizTalk Services dağıtımının atomik düzeyi değil. Her sürüm, farklı işlem kapasitesi ve belleğe sahip bir birimle birlikte verilir. Örneğin, Temel birimde Geliştirici’ye göre daha fazla işlem varken, Standart’ta da Temel’e göre daha fazla işlem vardır vb. BizTalk Hizmetini ölçeklendirdiğinizde birimler cinsinden ölçeklendirirsiniz.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Merhaba BizTalk Services ve Azure BizTalk VM arasındaki fark nedir?
BizTalk Services tümleştirme çözümleri hello bulutta oluşturmak için doğru bir Platform olarak-hizmet (PaaS) mimarisini sağlar. Merhaba PaaS modeliyle odaklanmak tamamen hello uygulama mantığına ve tüm hello altyapı Yönetimi tooMicrosoft bırakın dahil olmak üzere:

* Gereksinim toomanage ya da düzeltme eki sanal makine yok.
* Microsoft kullanılabilirliği sağlar.
* Ölçek isteğe bağlı yalnızca daha isteyen tarafından veya daha çok kapasite hello Azure portal aracılığıyla denetler.

Azure Virtual Machines’deki BizTalk Server hizmet olarak altyapı (IaaS) mimarisi sağlar. Sanal makineler oluşturup bunları tam olarak, şirket içi ortamda olduğu gibi kod değişikliğine hello bulutta daha kolay toorun uygulamalarınız kolaylaştırarak yapılandırabilirsiniz. Iaas ile hello sanal makineleri yapılandırma, hello sanal makineleri (örneğin, yazılım yükleme ve OS düzeltme ekleri) yönetme ve yüksek kullanılabilirlik için hello uygulama mimariden hala sorumludur.

Altyapı yönetimi çabanızı en aza indiren yeni tümleştirme çözümlerini derlemeye bakarsanız, BizTalk Services'ni kullanın. Tooquickly arıyorsanız mevcut BizTalk çözümlerinizi veya bir isteğe bağlı ortam toodevelop ve test BizTalk Server arayan uygulamaları kullanın BizTalk Server bir Azure sanal makinesinde.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Merhaba BizTalk bağdaştırıcı hizmeti ve karma bağlantılar arasındaki fark nedir?
Merhaba BizTalk Bağdaştırıcısı hizmeti Azure BizTalk hizmeti tarafından kullanılır. Merhaba BizTalk bağdaştırıcı hizmeti hello BizTalk bağdaştırıcı paketi tooconnect tooan şirket içi iş kolu (LOB) sistemine kullanır. Ve Azure Mobile Services, tooan kaynak şirket içi karma bağlantı kolay ve uygun şekilde tooconnect hello Azure App Service'te Web Apps özelliği gibi Azure uygulamalarını sağlar.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>“Birim başına Karma Bağlantı Veri Aktarımı (GB)” ne anlama geliyor? Bu dakika/saat/gün/hafta/ay mı? Merhaba sınıra ulaşıldığında ne olur?
Merhaba birim başına karma bağlantı maliyeti hello BizTalk Services sürümüne bağlıdır. Basitçe, maliyetler ne kadar veri aktarımı yaptığınıza bağlıdır. Örneğin, günde 10 GB veri aktarmanın maliyeti günde 100 GB veri aktarmanın maliyetinden daha düşüktür. Kullanım hello [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/?scenario=full) BizTalk Services toodetermine belirli maliyetleri için. Genellikle, hello sınırları günlüktür. Merhaba sınırı aşarsanız, aşmalar GB başına 1 USD hello hızında doludur.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>BizTalk Services'da sözleşme oluşturduğunuzda, neden köprü sayısı hello tarafından yerine ikiye yükseliyor?
Her sözleşme iki farklı köprüden oluşur: gönderme tarafı iletişim köprüsü ve alma tarafı iletişim köprüsü.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>Merhaba köprü sayısına veya anlaşmaları göre hello kota sınırına ulaştı. ne olur?
Yeni köprüleri erişilemiyor toodeploy olan veya yeni sözleşmeler oluşturamazsınız. Daha fazla toodeploy, tooscale toomore birimleri hello BizTalk hizmeti ya da daha yüksek sürüme yükseltme tooa gerekir.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>BizTalk Services tooanother bir katmandan nasıl geçişini?
Hello ücretsiz sürüm geçirilen ya da 'ölçeklendirilmiş' tooanother katmanı olamaz ve yedeklenemiyor ve tooanother katmanı geri yüklenebilir. Başka bir katman gerekiyorsa hello yeni katmanı kullanarak yeni bir BizTalk hizmeti oluşturun. Karma bağlantılar, gerek toobe de yeniden de dahil olmak üzere hello ücretsiz sürüm kullanılarak oluşturulan yapıtların yeni BizTalk hizmeti hello. 

Merhaba kalan sürümler için hello yedekleme ve bir katmanı tooanother yapıtları geçirmek için geri yükleme. Örneğin, hello standart katmanındaki yapıtlarınızı yedekleyin ve ardından toohello Premium katmanına geri yükleyin. [BizTalk Services: Yedekleme ve geri yükleme](biztalk-backup-restore.md) hello desteklenen geçiş yolları açıklanmıştır ve hangi yapıtların yedeklendiğini listeler. Karma Bağlantıların yedeklenmediğini unutmayın. Yedekleme ve tooa yeni katmanı geri yükleme sonrasında, ardından hello karma bağlantıları yeniden oluşturun.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Merhaba BizTalk bağdaştırıcı hizmeti hello hizmetinde dahil edildi? Merhaba yazılım nasıl alıyor musunuz?
Evet, BizTalk bağdaştırıcı hizmeti ile Merhaba BizTalk bağdaştırıcı paketi hello hello Azure BizTalk Services SDK'sı ile birlikte [karşıdan](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Sonraki adımlar
toocreate Azure BizTalk Services hello Azure portal, Git çok[BizTalk Services: hello Azure portalını kullanarak hazırlama](biztalk-provision-services.md). uygulamaları, Git çok oluşturma toostart[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Ek kaynaklar
* [BizTalk Services: hello Azure portalını kullanarak hazırlama](biztalk-provision-services.md)<br/>
* [BizTalk Services: Durum Grafiğini hazırlama](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Yedekleme ve Geri Yükleme](biztalk-backup-restore.md)<br/>
* [BizTalk Services: Azaltma](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](biztalk-issuer-name-issuer-key.md)<br/>
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

