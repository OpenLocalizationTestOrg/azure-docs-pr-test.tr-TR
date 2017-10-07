---
title: "aaaMigrating BizTalk Server EDI çözümleri tooBizTalk Hizmetleri Teknik Kılavuzu | Microsoft Docs"
description: "EDI tooMABS geçirmek; Microsoft Azure BizTalk Hizmetleri"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>BizTalk Server EDI çözümleri tooBizTalk Hizmetleri geçirme: teknik Kılavuzu

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Yazar: Tim Wieman ve Nitin Mehrotra

İnceleme: Karthik Bharthy

Kullanılarak yazılmış: Microsoft Azure BizTalk Services – Şubat 2014 serbest bırakın.

## <a name="introduction"></a>Giriş
Elektronik Veri Değişimi (EDI) olarak işletmeler veri elektronik olarak da işletmeler için veya B2B işlemler olarak gösterilen değişimi hello en yaygın anlamına gelir biridir. BizTalk Server hello ilk BizTalk Server sürüm bu yana bir on üzerinden EDI desteği oluşturdu. BizTalk Services ile Microsoft hello Microsoft Azure platformu üzerinde EDI çözümleri hello desteği devam eder. B2B işlemler çoğunlukla dış tooan kuruluş, ve bir bulut platformunda uygulanırsa bu nedenle, daha kolay tooimplement. Microsoft Azure BizTalk Services aracılığıyla bu yeteneği sağlar.

Yeni EDI çözümleri için "greenfield" platform olarak bazı müşteriler BizTalk Services bakın, ancak birçok müşteri toomigrate tooAzure isteyebilirsiniz geçerli BizTalk Server EDI çözümleri sahiptir. BizTalk Services EDI tasarlanmış göre hello olduğundan Services (ticaret ortakları, varlıklar, anlaşmalar) BizTalk Server EDI mimarisi, olası toomigrate BizTalk Server EDI yapıları tooBizTalk olduğu gibi aynı Varlık anahtarı.

Bu belge geçirme BizTalk Server EDI yapıları tooBizTalk ile Merhaba farklılıklarını bazıları açıklanır Hizmetleri. Bu belge, BizTalk Server EDI işlemeyi ve ticari ortak sözleşmeleri bilgili varsayar. BizTalk Server EDI hakkında daha fazla bilgi için bkz: [iş ortağı yönetimi kullanarak BizTalk Server ticaret](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>BizTalk Server EDI yapılarının hangi sürümü olabilir tooBizTalk hizmetleri geçirilen?
yeniden modellenmiş tooinclude iş ortakları, Profiller ve anlaşmaları değiştirildiği hello BizTalk Server EDI modülü BizTalk Server 2010 için önemli ölçüde geliştirilmiştir. BizTalk hizmetleri kullanan ticaret ortakları aynı modeli tooorganize hello hello ve bu ortakların içinde iş bölümler hello. Sonuç olarak, EDI geçirme BizTalk Server 2010 ve sonraki sürümleri tooBizTalk yapılardan Hizmetleri, çok daha basit bir işlemdir. sürümleri önceki tooBizTalk Server 2010 ile ilişkili toomigrate EDI yapıların tooBizTalk Server 2010 yükseltmeniz ve ardından EDI yapıtları geçirmek tooBizTalk Hizmetleri.

## <a name="scenariosmessage-flow"></a>Senaryo/ileti akışı
BizTalk Server ile olarak BizTalk Services'da işleme EDI bir ticari ortak Yönetimi (TPM) çözüm oluşturulmuştur. Merhaba TPM çözüm anahtar bileşenleri aşağıdaki hello sahiptir:

* Ticaret ortakları, hangi B2B işlem kuruluşta temsil eder.
* Profilleri, ticari ortak içinde bölümler temsil eder.
* Ticari ortak sözleşmeleri (veya anlaşmaları) iki iş ortakları/profilleri arasında hello iş anlaşmayı temsil eder.

Aşağıdaki çizimde hello hello benzerlikler yanı sıra, BizTalk Server EDI çözüm ve BizTalk Services EDI çözümü arasındaki farklar gösterilmektedir:

![][EDImessageflow]

temel farklılıklar ve BizTalk Server EDI çözüm akışında arasındaki benzerlikler hello ve BizTalk Services şunlardır:

* EDI ileti ve EDISend ardışık düzen toosend EDI ileti BizTalk Server EDIReceive ardışık düzen tooreceive yalnızca kullanır gibi BizTalk Services bir köprü tooreceive EDI almak ve EDI gönderme köprüsü toosend EDI ileti kullanır. BizTalk Server hello ardışık düzen gönderme kullanarak bir Sözleşmesi ile ilişkili olan veya geri alma bağlantı noktalarının. BizTalk Services hello anlaşma kendisini hello gönderme gösterir veya köprüsü alırsınız.
* EDI ileti Hello EDIReceive ardışık düzen işlemleri hello sonra BizTalk Server ' hello Dökümü alınan tooa SQL Server veritabanı iletisidir. Merhaba EdiSend ardışık hello ileti hello SQL Server veritabanından alır, işler ve iş ortağı ticaret toohello gönderir.
  
    Merhaba EDI aldıktan sonra köprüsü işlemleri hello EDI ileti, BizTalk Services'da hello ileti tooan dış işlem yönlendirir. Merhaba dış işlem Microsoft Azure veya şirket içi çalıştırıyor. Merhaba dış işlem EDI gönderme köprüsü hello ileti toohello rota; Merhaba gönderme köprüsü selamlama iletisine kendiliğinden çekme değil. İşleme selamlama iletisine sonra hello ileti toohello ticari ortak EDI gönderme köprüsü hello yönlendirir.

BizTalk hizmetleri sağlayan bir kullanımı kolay yapılandırma deneyimi tooquickly oluşturun ve tüm Microsoft Azure işlem yapılandırma örnekleri (Web veya çalışan rolleri) olmadan ticaret ortakları, tüm Microsoft Azure SQL veritabanları veya arasında herhangi bir B2B anlaşması dağıtın Microsoft Azure depolama hesabı. Daha karmaşık senaryolara iş akışları veya diğer hizmetini işleme bağlamadan gerektirir "geçici hello kenarlarına" başka bir deyişle, bir ticari ortak sözleşmesi önce veya sonra ticari ortak sözleşmesi EDI köprüsü işleme. Ayrıntılı olarak hello aşağıdaki olaylar dizisi bir EDI ileti BizTalk Services'da işleme sırasında oluşur.

1. İş ortağı, Fabrikam ticari bir EDI ileti alındı.  Ticaret ortaklarından EDI iletileri almak için BizTalk Services FTP, SFTP, AS2 ve HTTP/s gibi aktarım protokollerini destekler
2. iş ortağı sözleşmesi alma tarafı işleme ticaret hello hello EDI ileti tooXML biçimi ayrıştırır.  Bir Service Bus geçişi uç noktası, hizmet veri yolu konusu, hizmet veri yolu kuyruğu ya da BizTalk Services köprü gibi çözülürken hello EDI ileti (XML biçiminde) tooService veri yolu uç yönlendirebilirsiniz.
3. Merhaba artık hata ayıklayabildiğinize XML iletileri sonra daha fazla özel işleme için hello uç noktasından alınması.  Bu uç noktalar bir şirket içi bileşeni veya bir Microsoft Azure işlem örneği toofurther işlem hello iletisinde bir Windows iş akışı (WF) veya Windows Communication Foundation (WCF) hizmetini örneğin işlenemedi.
4. Hello "Merhaba ticari ortak sözleşmesi gönderme tarafı işleme" ardından EDI biçiminde hello XML ileti derler ve tootrading iş ortağı, Contoso gönderir.  BizTalk Services tootrading ortakları EDI ileti göndermek için aynı EDI iletileri almak için kullanılan protokoller hello destekler.

Bu belgede daha fazla kavramsal rehberlik sağlar hello farklı BizTalk Server EDI yapıları tooBizTalk bazıları geçirme Hizmetleri.

## <a name="sendreceive-ports-tootrading-partners"></a>Gönder/Al bağlantı noktaları tooTrading ortakları
BizTalk Server ', alma konumları ve alma bağlantı noktalarının tooreceive EDI/XML iletileri ticaret ortaklarından ayarlamanız ve gönderme bağlantı noktaları toosend EDI/XML iletileri tootrading iş ortağı ayarlayın. Ardından, ticari ortak sözleşmesi hello BizTalk Server Yönetim Konsolu kullanılarak bu bağlantı noktaları tooa de bağlayın. BizTalk Services ' hello BizTalk Services portalı ticari ortaklar ve burada iletileri tootrading ortakları hello ticari ortak sözleşmesi kendisini (parçası olarak aktarım ayarları) bir parçası olarak yapılandırılmış olan gönderdiğiniz iletilerinin almanıza konumları hello .  Bu nedenle, gerçekten "gönderme bağlantı noktaları" ve "konumları Al" Merhaba kavramı başına uzatılmasında BizTalk Services'da sahip değilsiniz. Daha fazla bilgi için bkz: [oluşturma anlaşmaları](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Ardışık Düzen (köprü)
BizTalk Server EDI içinde ardışık düzen da Merhaba uygulaması gerektirdiği gibi belirli işleme özelliklerine yönelik özel mantık içerebilir ileti işleme varlıklardır. BizTalk Services için hello eşdeğer bir EDI köprüsü olacaktır. Ancak, şimdilik BizTalk Services hello EDI köprüleri "kapalı".  Diğer bir deyişle, kendi özel etkinlikler tooan EDI köprüsü ekleyemezsiniz. Özel işlem yapmadan önce veya selamlama iletisine hello ticari ortak sözleşmesi bir parçası olarak yapılandırılmış hello köprüsü girdikten sonra hello EDI köprüsü, uygulamanızda dışında yapılmalıdır. EAI köprüleri hello seçeneği toodo özel işleme sahip. Özel işleme istiyorsanız, önce veya sonra hello EDI köprüsü tarafından işlenen hello iletisi EAI köprüleri kullanabilirsiniz. Daha fazla bilgi için bkz: [tooInclude özel kod nasıl köprülerde](https://msdn.microsoft.com/library/azure/dn232389.aspx).

Özel kod ve/veya hizmet veri yolu kuyrukları ve konularından ticari ortak sözleşmesi hello selamlama iletisine almadan önce ya da hello sözleşmesi hello iletisini işler ve tooa Service Bus uç noktası yönlendiren sonra ileti kullanarak bir Yayımla ve abone akışla ekleyebilirsiniz.

Bkz: **senaryoları/ileti akışı** hello ileti akışı deseni için bu konudaki.

## <a name="agreements"></a>Anlaşmaları
BizTalk Server 2010 ticaret ortak sözleşmeleri EDI işleme için kullanılan hello biliyorsanız, BizTalk ticari ortak sözleşmeleri Hizmetleri bilgili arayın. Ayarları olan hello aynı hello sözleşmesi ve kullanım çoğunu aynı terminolojisi hello. Bazı durumlarda, anlaşma ayarları hello kadar basit karşılaştırılan toohello BizTalk Server'ın aynı ayarlardır. AS2, EDIFACT ve Microsoft Azure BizTalk Services destekler X12 taşıma.

Microsoft Azure BizTalk Services de sağlayan bir **TPM veri geçişi** aracı toomigrate ticari ortaklar ve BizTalk Server ticari ortak modülü tooBizTalk Hizmetleri portalı içinden sözleşmelerini. Merhaba TPM veri geçiş aracı kullanılabilir Araçlar paketinin bir parçası olarak, hangi indirilebilir hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). Merhaba paketi de nasıl toouse hello aracı ve temel sorun giderme bilgileri için aracı hello hakkında yönergeler sağlayan bir benioku dosyası içerir.

## <a name="schemas"></a>Şemalar
BizTalk Services BizTalk Services çözümlerinde kullanılan EDI şemaları sağlar.  Ayrıca, BizTalk hizmetlerinin yanı sıra BizTalk Server arasında hello EDI şema Hello kök düğümü aynı olduğu için BizTalk Server EDI şemaları da BizTalk Services ile kullanılabilir. Bu nedenle, BizTalk Server EDI şemaları mümkün toodirectly Al olması ve BizTalk Services'ı kullanarak geliştirme hello EDI çözümlerinde kullanın. Merhaba şemaları hello indirebilirsiniz [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Eşlemeleri (dönüşümler)
BizTalk Server'ın eşlemeleri dönüşümler BizTalk Services'da denir. BizTalk Server tooBizTalk Hizmetleri aşağıdakilerden biri olabilir geçirme haritaları (harita karmaşıklık) bağlı olarak daha karmaşık görevleri tooachieve hello. BizTalk Hizmetleri için kullanılan hello eşleme hello BizTalk Eşleyici farklı aracıdır. Merhaba Eşleyici görünse çoğunlukla aynı Merhaba, hello temel eşleme biçimi farklıdır. Merhaba İşlevsiler (adlı **eşleme işlemleri** BizTalk Services) kullanılabilir toohello kullanıcıların farklı de.  Uygulamada bir BizTalk harita doğrudan BizTalk Services'da kullanamazsınız. Ayrıca, BizTalk Server içinde kullanılabilir tüm hello İşlevsiler BizTalk Services harita işlemlerinde olarak kullanılabilir.

### <a name="new-transform-operations"></a>Yeni dönüştürme işlemleri
Dönüştürme eşleme işlemleri Hello listesi BizTalk Server Eşleyici hello oldukça farklı görünebilir, ancak BizTalk Services dönüştürür aynı görevleri hello gerçekleştirmeye yeni yöntemler vardır. Örneğin, BizTalk Services dönüştüren sahip **listeleme işlemleri** kullanılabilir. Bu hello BizTalk eşleyicisinde kullanılabilir değildi.  Merhaba **listeleme işlemleri** toocreate etkinleştirmek ve bir "listesinde", bir liste öğesi (olarak da bilinen "satır") kümesi ve her öğesi, birden çok üye (olarak da bilinen "sütunlar") sahip olduğunda çalışır.  Başlangıç listesi, bağlı bir koşul, vb. öğeleri seçebilir sıralayabilirsiniz.

BizTalk Services dönüştüren içindeki yeni işlevsellik başka bir örneği olan hello **döngüsü işlemleri**.  BizTalk Server Eşleyici hello iç içe geçmiş zor toocreate Döngülerde olur.  Bu nedenle, hello döngü eşleme işlemleri Merhaba BizTalk Services dönüştüren eklenir.

Yine de başka bir örnek hello **If-Then-Else** ifade eşleme işlemi.  IF-then-başka bir işlem yapmakla hello BizTalk eşleyicisinde mümkün olsa da, birden çok İşlevsiler tooaccomplish görünen basit bir görev gerekli.

### <a name="migrating-biztalk-server-maps"></a>BizTalk sunucusunu taşıma eşlemeleri
Microsoft Azure BizTalk Services aracı toomigrate BizTalk Server tooBizTalk Hizmetleri dönüşümler eşlemeleri sağlar. Merhaba **BTMMigrationTool** kullanılabilir hello bir parçası olarak **Araçları** hello ile sağlanan paketini [BizTalk Services SDK'sını indirme](http://go.microsoft.com/fwlink/p/?LinkId=235057). Merhaba aracı hakkında daha fazla bilgi için bkz: [bir BizTalk harita tooa BizTalk Services dönüştürme Dönüştür](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

Ayrıca bir örnek Sandro Pereira, BizTalk MVP tarafından üzerinde nasıl çok bakabilirsiniz[BizTalk Server eşlemeleri tooBizTalk Hizmetleri dönüşümler geçirmek](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Düzenlemelerin
BizTalk Server orchestration işleme tooMicrosoft Azure toomigrate gerekiyorsa, Microsoft Azure çalışan BizTalk Server düzenlemelerin desteklemediğinden yeniden yazılmıştır toobe hello düzenlemelerin gerekir.  Windows Workflow Foundation 4.0 (WF4) hizmetinin hello orchestration işlevleri yeniden yazabilirsiniz.  BizTalk Server düzenlemelerin tooWF4 şu anda hiçbir geçişini olduğundan bu tam bir yeniden yazma olacaktır. Windows iş akışı için bazı kaynaklar aşağıda verilmiştir:

* [*Nasıl toointegrate bir WCF iş akışı hizmeti Service Bus kuyrukları ve konularından* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) Paolo Salvatori tarafından. 
* [*Windows Workflow Foundation ve Microsoft Azure ile uygulamaları oluşturmaya* oturum](http://go.microsoft.com/fwlink/p/?LinkId=237314) hello yapı 2011 konferans gelen.
* [*Windows Workflow Foundation Geliştirici Merkezi* ](http://go.microsoft.com/fwlink/p/?LinkId=237315) konusuna bakın.
* [*Windows Workflow Foundation 4 (WF4) belgeleri* ](https://msdn.microsoft.com/library/dd489441.aspx) konusuna bakın.

## <a name="other-considerations"></a>Diğer konular
BizTalk Services kullanırken yapmanız gereken birkaç dikkat edilecek noktalar aşağıda verilmiştir.

### <a name="fallback-agreements"></a>Geri dönüş sözleşmeleri
BizTalk Server EDI işlemeyi "Geri dönüş anlaşmaları" Merhaba kavramı vardır.  BizTalk Services mu **değil** bir geri dönüş sözleşmesi kavramı kadarki sahip.  BizTalk belgeleri konulara bakın [EDI işliyor anlaşmalarını rol hello](http://go.microsoft.com/fwlink/p/?LinkId=237317) ve [yapılandırma genel ya da geri dönüş sözleşmesi özelliklerini](https://msdn.microsoft.com/library/bb245981.aspx) geri dönüş anlaşmaları BizTalk nasıl kullanıldığı hakkında bilgi için Sunucu.

### <a name="routing-toomultiple-destinations"></a>Yönlendirme toomultiple hedefler
BizTalk Services köprüleri, geçerli durumunda bir yayımlama kullanarak yönlendirme iletileri toomultiple hedefler desteklemiyor-model abone olun. Bunun yerine birden çok abonelik tooreceive selamlama iletisine birden fazla uç noktada sonra sahip olabilen bir BizTalk Services köprüsü tooa Service Bus konu iletilerden yol.

## <a name="conclusion"></a>Sonuç
Microsoft Azure BizTalk Services normal kilometre taşları tooadd güncelleştirilmiş daha fazla özellik ve yetenekler. Her güncelleştirme ile BizTalk Services ve diğer Azure teknolojilerini kullanarak uçtan uca çözümler oluşturma toosupporting artırılmış işlevsellik toofacilitate umuyoruz.

## <a name="see-also"></a>Ayrıca Bkz.
[Azure ile Kurumsal uygulamaları geliştirme](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
