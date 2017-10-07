---
title: "Azure BizTalk Services aaaRelease notları | Microsoft Docs"
description: "Hello Azure BizTalk Services için bilinen sorunları listeler"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Azure BizTalk Services için sürüm notları

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Merhaba sürüm notları hello Microsoft Azure BizTalk Services için bilinen sorunlar bu sürümde hello içerir.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>BizTalk Hizmetleri Kasım güncelleştirmesi hello yenilikler nelerdir?
* Bekleyen şifreleme hello BizTalk Services portalı etkinleştirilebilir. Bkz: [etkinleştirmek BizTalk Services Portalı'nda bekleyen şifreleme](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Güncelleştirme geçmişini
### <a name="october-update"></a>Ekim güncelleştirme
* Kurumsal hesaplar desteklenir:  
  * **Senaryo**: bir Microsoft hesabı kullanarak bir BizTalk hizmeti dağıtımı kayıtlı (gibi user@live.com). Bu senaryoda, kullanıcılar yönetebilir yalnızca Microsoft Account hello hello BizTalk Services portalını kullanarak BizTalk hizmeti. Bir kurumsal hesap kullanılamaz.  
  * **Senaryo**: Azure Active Directory'de bir kurumsal hesap kullanarak bir BizTalk hizmeti dağıtımı kayıtlı (gibi user@fabrikam.com veya user@contoso.com). Bu senaryoda, yalnızca Azure Active Directory kullanıcıları aynı kuruluş yönetebilirsiniz hello içinde hello BizTalk Services portalını kullanarak BizTalk hizmeti hello. Bir Microsoft hesabı kullanılamaz.  
* Merhaba Klasik Azure portalında bir BizTalk hizmeti oluşturduğunuzda, hello BizTalk Services Portal otomatik olarak kaydedilir.
  * **Senaryo**: hello Klasik Azure portalı oturum BizTalk hizmeti oluşturma ve ardından **Yönet** hello çok ilk kez için. Hello BizTalk Services portalı açıldığında, hello BizTalk hizmeti otomatik olarak kaydeder ve dağıtımları için hazırdır.  
    Bkz: [kaydetme ve üzerinde bir BizTalk hizmeti dağıtımı güncelleştirme hello BizTalk Services portalı](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>14 Ağustos güncelleştirme
* Şimdi sözleşmesi ve ayırma – ticari ortak sözleşmeleri ve köprüleri köprüsü hello BizTalk Services portalı birbirinden ayrılır. Artık anlaşmalar ve köprüleri ayrı olarak oluşturun ve çalışma zamanı köprüleri hello EDI ileti hello değerlerine dayalı olarak tooan anlaşması çözümleyin. Bkz: [Azure BizTalk Services oluşturma sözleşmelerde](https://msdn.microsoft.com/library/azure/hh689908.aspx), [BizTalk Services Portalı'nı kullanarak bir EDI köprüsü oluşturma](https://msdn.microsoft.com/library/azure/dn793986.aspx), [BizTalk Services Portalı'nı kullanarak bir AS2 köprüsü oluşturma](https://msdn.microsoft.com/library/azure/dn793993.aspx), ve [nasıl köprüleri çözümlemek çalışma zamanında anlaşmaları?](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* Merhaba seçeneği toocreate şablonları sözleşmeleri için son verildi.  
* Merhaba gönderme tarafı anlaşma için farklı sınırlayıcı kümeleri her şema için artık belirtebilirsiniz. Bu yapılandırma, gönderme tarafı anlaşması Protokolü Ayarları altında belirtilir. Daha fazla bilgi için bkz: [oluşturma X12 bir Azure BizTalk Services anlaşmasında](https://msdn.microsoft.com/library/azure/hh689847.aspx) ve [Azure BizTalk Services ' bir EDIFACT sözleşmesi oluşturun](https://msdn.microsoft.com/library/azure/dn606267.aspx). İki yeni varlıklar da toohello TPM OM API hello için eklenen üstlenir. Bkz: [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) ve [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Türetilmiş türler dahil olmak üzere standart XSD yapıları artık desteklenmektedir. Bkz: [kullanım standart XSD oluşturur, maps](https://msdn.microsoft.com/library/azure/dn793987.aspx) ve [kullanım türetilmiş türlerini eşleme senaryoları ve örnekler](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 ileti imzalama için yeni MIC algoritmalarını ve yeni şifreleme algoritmaları destekler. Bkz: [AS2 sözleşmesi Azure BizTalk Services oluşturma](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Bilinen sorunlar

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>BizTalk Services Portal güncelleştirmesi sonra bağlantı sorunları
  BizTalk Hizmetleri portalını açın BizTalk Services yükseltilirken hello varsa tooroll içinde toohello hizmeti değiştirir, hello BizTalk Services portalı ile ilgili bağlantı sorunlarını yüz.  
  Geçici bir çözüm olarak hello tarayıcıyı yeniden, hello tarayıcı önbelleğine silin veya özel modda hello portal başlatın.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Bir hata veya uyarı BizTalk Services projesinde tıklatırsanız visual Studio IDE hello yapı bulunamıyor
Visual Studio 2012 güncelleştirme 3 RC 1 Hello toofix hello sorunu yükleyin.  

### <a name="custom-binding-project-reference"></a>Özel bağlama proje başvurusu
Aşağıdaki durumlarda bir BizTalk Services proje bir Visual Studio çözümü ile Merhaba göz önünde bulundurun:  

* İçinde aynı Visual Studio çözümü Merhaba, BizTalk Services projesi ve özel bağlama proje yok. Merhaba BizTalk hizmeti projesini bir başvuru toothis özel bağlama proje dosyası vardır.
* Merhaba BizTalk hizmeti projesini bir başvuru tooa özel bağlama/davranışı DLL vardır.

'Derleme' Visual Studio'da Çözüm başarıyla hello. Ardından, 'Yeniden' veya 'hello çözüm temiz'. Yeniden oluşturmanız veya temiz bir yeniden aşağıdaki hello bundan sonra hata oluşur:  
  %S toocopy dosya <Path tooDLL> too"bin\Debug\FileName.dll". başka bir işlem tarafından kullanıldığından hello işlem hello dosya 'bin\Debug\FileName.dll' erişemiyor.  

#### <a name="workaround"></a>Geçici çözüm
* Varsa [Visual Studio 2012 güncelleştirme 3'ü](https://www.microsoft.com/download/details.aspx?id=39305) olan yüklü hello aşağıdaki iki seçenek vardır:
  
  * Visual Studio'yu yeniden başlatın veya
  * Merhaba çözümü yeniden başlatın. Sonra yalnızca bir yapı hello çözüm üzerinde gerçekleştirin.  
* Varsa [Visual Studio 2012 güncelleştirme 3'ü](https://www.microsoft.com/download/details.aspx?id=39305) olan yüklü değil, Görev Yöneticisi'ni açın, hello İşlemler sekmesinde hello MSBuild.exe işlemi'ı tıklatın ve hello İşlemi Sonlandır düğmesini tıklatın.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Yazdırılamayan karakterler HTTP üst bilgileri olarak yükselttiyseniz tooBasicHttpRelay uç noktaları yönlendirme köprüleri ve BizTalk Services portalı desteklenmiyor
İletiler için yükseltilen özelliklerinin bir parçası yazdırılamayan karakterleri kullanırsanız, bu iletileri hello BasicHttpRelay bağlamayı kullanan yönlendirilmiş toorelay hedefleri olamaz. Ayrıca, hello yükseltilmiş izleme bir parçası olarak BLOB'lar için URL olarak kodlanmış ve beklemediğiniz kodlanmış hedefler için kullanılabilir olan özellikler.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>Zaman uyumsuz MDN seçeneği işaretli değil dahi Hello Gönder MDN zaman uyumsuz olarak gönderilir
Merhaba seçerseniz bu senaryoyu – göz önünde bulundurun **gönderme zaman uyumsuz MDN** onay kutusunu ve URL toosend hello async MDN belirtin ve hello kutusunun işaretini kaldırın **gönderme zaman uyumsuz MDN** onay kutusunu yeniden hello MDN olmasına rağmen Merhaba seçeneği toosend zaman uyumsuz MDNs seçilmemiş olsa da gönderilen toohello URL belirtildi.  
Geçici bir çözüm olarak temizlemeniz gerekir hello belirtilen URL hello işaretleyerek önce **gönderme zaman uyumsuz MDN** onay kutusunu ve ardından hello AS2 sözleşmesi dağıtın.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Boşluk karakterleri geçerli değişim neden bir boş ileti gönderilen toobe toohello ötesinde uç nokta askıya alma
Bir IEA kesimi ötesinde boşluklar varsa, hello ayrıştırıcı Bu geçerli değişim ucu olarak değerlendirir ve sonraki ileti olarak boşluk sonraki kümesini hello bakar. Bu, geçerli değişim olmadığından, başarılı bir ileti toohello rota hedef gönderilir ve boş bir ileti hello gönderilen görebilirsiniz uç nokta askıya alma.  

### <a name="tracking-in-biztalk-services-portal"></a>BizTalk Services Portalı'nda izleme
İzleme olaylarını toohello EDI ileti işleme ve hiçbir bağıntı yakalanır. Bir ileti Protokolü aşama hello dışında başarısız olursa izleme başarılı olarak gösterilir. Bu durumda, hello altında toohello günlük bölümüne bakın **ayrıntıları** sütununda **izleme** hata ayrıntıları.
Merhaba X12 ayarları gönderip ([oluşturma X12 bir Azure BizTalk Services anlaşmasında](https://msdn.microsoft.com/library/azure/hh689847.aspx)) protokolü aşama hello hakkında bilgi sağlar.  

### <a name="update-agreement"></a>Güncelleştirme anlaşması
bir anlaşma yapılandırıldığında hello BizTalk Services portalı toomodify hello bir kimliği niteleyicisi sağlar. Bu, tutarsız özelliklerinde neden olabilir. Örneğin, ZZ:1234567 ve ZZ:7654321 hello niteleyicisi kullanarak bir anlaşma var. Merhaba BizTalk Services portalı profili ayarlarında ZZ:1234567 toobe 01:ChangedValue değiştirin. Merhaba Sözleşmesi'ni açın ve 01:ChangedValue ZZ:1234567 yerine görüntülenir.
toomodify hello delete hello anlaşma, bir kimliği niteleyicisi güncelleştirme **kimlikleri** hello ortağı profili ve hello sözleşmesi yeniden oluşturun.  

> AZURE. Bu davranış uyarı X12 ve AS2 etkiler.  
> 
> 

### <a name="as2-attachments"></a>AS2 ekler
İletileri desteklenmez AS2 eklerini göndermek veya almak. Özellikle, ekleri sessizce yok sayılır ve hello ileti gövdesi normal AS2 ileti olarak işlenir.  

### <a name="resources-remembering-path"></a>Kaynaklar: Yolu anımsama
Eklerken **kaynakları**, hello iletişim penceresinde hello daha önce kullanılan yolu tooadd bir kaynak değil unutmayın. Merhaba BizTalk Services portalı web sitesini çok eklemeyi deneyin olan tooremember hello daha önce kullanılan yolu**Güvenilen siteler** Internet Explorer'da.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Değişiklikleri kaydetmeden hello varlık adı Köprüsü ve Kapat Merhaba projeyi yeniden adlandırırsanız, hello varlık tekrar açmayı hatayla sonuçlanır
Sırasının hello senaryoda göz önünde bulundurun:  

* Köprü (örneğin bir XML One-Way köprüsü) tooa BizTalk hizmeti projesini ekleyin  
* Merhaba köprüsü hello varlık adı özelliği için bir değer belirterek yeniden adlandırın. Bu, belirtilen hello adıyla hello ilişkili .bridgeconfig dosyayı yeniden adlandırır.  
* Merhaba .bcs dosyasını (Visual Studio hello sekmesinde kapatarak) hello değişiklikleri kaydetmeden kapatın.  
* Merhaba .bcs dosyasını Solution Explorer hello yeniden açın.  
  Merhaba ilişkili .bridgeconfig dosya belirttiğiniz hello yeni adı varken hello varlık adı hello tasarım yüzeyinde hala hello eski adı olduğunu fark edeceksiniz. Merhaba köprüsü bileşeni çift tıklatarak tooopen hello Köprü yapılandırması denerseniz aşağıdaki hata hello alın:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`Bu senaryo çalıştıran tooavoid BizTalk hizmeti projesini hello varlıklarda yeniden adlandırdıktan sonra değişiklikleri kaydetmek emin olun.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>Bir yapı bir Visual Studio Proje dışlanan olsa bile BizTalk hizmeti projesini başarıyla derlemeler
Burada bir yapı (örneğin, bir XSD dosyası) tooa BizTalk hizmeti projesini eklemek, bu yapı hello Köprü yapılandırması (örneğin, bu bir istek iletisi türü belirterek) ekleyin ve hello Visual Studio Proje hariç bir senaryo düşünün. Silinen hello yapı hello hello diskte kullanılabilir olduğu sürece böyle bir durumda hello proje derleme herhangi bir hata veremezsiniz aynı konumdaki burada hello Visual Studio projeye eklendi.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Merhaba BizTalk hizmeti projesi için şema kullanılabilirlik hello köprüleri yapılandırılırken denetlemez
Toohello proje eklenen bir şema başka bir şema alıyorsa bir BizTalk hizmeti projesini hello alınan şema toohello proje eklenip eklenmeyeceğini hello BizTalk hizmeti projesini denetlemez. Bu tür bir proje toobuild çalışırsanız, yapı hataları almamış.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>Merhaba yanıt için bir XML istek-yanıt köprüsü her zaman charset UTF-8 ' iletisidir
Bu sürüm için bir XML istek-yanıt köprüsü gelen hello yanıt iletisinin hello charset her zaman tooUTF-8 ayarlanır.
  
### <a name="user-defined-datatypes"></a>Kullanıcı tanımlı veri türleri
Merhaba BizTalk bağdaştırıcı paketi hello BizTalk bağdaştırıcı hizmeti özellik bağdaştırıcılara kullanıcı tanımlı veri türleri bağdaştırıcısı işlemleri için kullanabilir.
Kullanıcı tanımlı veri türleri kullanırken hello dosyaları (.dll) toodrive:\Program Files\Microsoft BizTalk Bağdaştırıcısı Service\BAServiceRuntime\bin\ veya hello BizTalk bağdaştırıcı hizmeti barındıran hello sunucusunda toohello Genel Derleme Önbelleği (GAC) kopyalayın. Aksi takdirde, aşağıdaki hata hello hello istemcide oluşabilir:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> Önerilen toouse GACUtil.exe tooinstall hello Genel Derleme Önbelleği dosyasına olur. GACUtil.exe belgeleri nasıl toouse bu aracı ve hello Visual Studio komut satırı seçenekleri.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Merhaba BizTalk bağdaştırıcı hizmeti Web sitesi yeniden başlatılıyor
Yükleme hello **BizTalk bağdaştırıcı hizmeti çalışma zamanı*** hello oluşturur **BizTalk bağdaştırıcı hizmeti** hello içeren IIS web sitesinde **BAService** uygulama. **BAService** uygulama dahili olarak geçiş bağlama tooextend hello şirket içi hizmet uç noktası toohello bulut ulaşabileceği kullanır. Yalnızca hello hizmeti başlatıldığında içi olduğunda bir barındırılan hizmet şirket için Service Bus hello üzerinde hello karşılık gelen geçiş endpoint kaydedilir.  

Durdur ve uygulama başlatma, bir uygulamayı otomatik olarak başlatıyor hello yapılandırması dikkate alınır değil. Böyle olduğunda **BAService** olan durduruldu, her zaman hello yeniden başlatmanız gerekir **BizTalk bağdaştırıcı hizmeti** yerine web sitesi. Olmayan başlatma veya durdurma hello **BAService** uygulama.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>Özel karakterler LOB bileşenleri adresi ve varlık adları için kullanılmamalıdır
LOB bileşenleri adresi ve varlık adları için özel karakterler kullanmamalısınız. Bunu yaparsanız, hello BizTalk hizmeti projesini dağıtma sırasında bir hata alırsınız. Belirli '%' gibi karakterler, hello BizTalk bağdaştırıcı hizmeti Web sitesi durdurulmuş bir duruma geçebilir ve bunu toomanually gerekir.

### <a name="test-map-with-get-context-property"></a>Get içerik özelliği test Haritası
Bir dönüştürme içeriyorsa bir **alma içerik özelliği** eşleme işlemi **Test eşlemesi** başarısız olur. Geçici bir çözüm olarak hello yerine **alma içerik özelliği** sahte verileri içeren dize birleştirme Map işlemi ile eşleme işlemi. Merhaba hedef şema doldurmak ve diğer dönüştürme işlevselliğini sınamak izin.

### <a name="test-map-property-does-not-display"></a>Test eşleme özelliğini görüntülenmez
Merhaba **Test eşlemesi** özellikleri Visual Studio'da görüntülemez. Bu hello oluşabilir **özellikleri** penceresini açın ve hello **Çözüm Gezgini** penceresi aynı anda yerleştirilmemişse. tooresolve Bu, yerleştirme hello **özellikleri** ve hello **Çözüm Gezgini** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>DateTime yeniden biçimlendirin açılan gri
Bir DateTime yeniden biçimlendirin eşleme işlemi eklendiğinde toohello yüzey ve yapılandırılmış, hello aşağı açılan liste gri biçimi tasarlayın. Merhaba bilgisayarı görüntü ayarlarsanız bu durum oluşabilir **Orta – %125** veya **daha büyük – % 150**. tooresolve, hello görüntü çok ayarlamak**daha küçük – % 100 (varsayılan)** hello adımları kullanarak:  

1. Açık hello **Denetim Masası** tıklatıp **Görünüm ve kişiselleştirme**.
2. Tıklatın **görüntü**.
3. Tıklatın **daha küçük – % 100 (varsayılan)** tıklatıp **Uygula**.

Merhaba **biçimi** aşağı açılan liste beklendiği gibi şimdi çalışmalıdır.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Yinelenen sözleşmelerde hello BizTalk Services portalı
Senaryo aşağıdaki hello göz önünde bulundurun:

1. Merhaba ticaret iş ortağı Yönetimi OM API kullanarak bir anlaşma oluşturun.
2. İki farklı sekmeler hello BizTalk Services Portalı'nda Hello Sözleşmesi'ni açın.
3. Her iki hello sekmelerindeki Hello sözleşmesi dağıtın.
4. Her iki hello anlaşmaları hello BizTalk Services portalı yinelenen girdiler sonuçta sonuç olarak, dağıtılan

**Geçici çözüm**. Merhaba BizTalk Services portalı hello yinelenen anlaşmaları herhangi birini açın ve dağıtımı geri.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>Bir sertifika hello yapıt deposunda bile güncelleştirildikten sonra köprüleri güncelleştirilmiş sertifika kullanmayın
Hello aşağıdaki senaryoları göz önünde bulundurun:  

**Senaryo 1: İleti aktarma köprüsü tooa hizmet uç noktasından güvenliğini sağlamak için parmak izi temel alarak sertifikaları kullanma**  
Parmak izi tabanlı sertifikalar, BizTalk hizmeti projenizde kullandığınız bir senaryo düşünün. Merhaba BizTalk Services portalı hello sertifika ile aynı farklı bir parmak izi adı ancak hello BizTalk hizmeti projesini uygun şekilde güncelleştirilmiyor hello güncelleştirin. Böyle bir senaryoda Hello eski sertifika verileri hello kanal önbelleğinde olabileceğinden hello köprüsü tooprocess Merhaba iletileri devam edebilir. Bundan sonra ileti işleme başarısız olur.  

**Geçici çözüm**: güncelleştirme hello BizTalk hizmeti projesini hello sertifikada ve Merhaba projeyi yeniden dağıtın.  

**Senaryo 2: İleti aktarma köprüsü tooa hizmet uç noktasından güvenliğini sağlamak için ad tabanlı davranışları tooidentify sertifikaları kullanarak**

Ad tabanlı davranışları tooidentify sertifikaları BizTalk hizmeti projenizde kullandığınız bir senaryo düşünün. Merhaba BizTalk Services portalı hello sertifikada güncelleştirme ancak hello BizTalk hizmeti projesini uygun şekilde güncelleştirmez. Böyle bir senaryoda Hello eski sertifika verileri hello kanal önbelleğinde olabileceğinden hello köprüsü tooprocess Merhaba iletileri devam edebilir. Bundan sonra ileti işleme başarısız olur.  

**Geçici çözüm**: güncelleştirme hello BizTalk hizmeti projesini hello sertifikada ve Merhaba projeyi yeniden dağıtın.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>Merhaba SQL veritabanı çevrimdışı olduğunda bile köprüleri tooprocess iletileri devam
Merhaba (dağıtılan yapıları ve ardışık düzen gibi bilgileri çalıştıran hello depolayan) Microsoft Azure SQL veritabanı olsa bile çevrimdışı hello BizTalk Services köprüleri tooprocess iletileri bir süre devam edin. BizTalk Services önbelleğe hello yapıları ve Köprü yapılandırması kullandığından budur.
Merhaba SQL veritabanı çevrimdışı olduğunda, hello köprüleri tooprocess herhangi bir ileti istemiyorsanız, hello BizTalk Hizmetleri PowerShell cmdlet'leri toostop veya hello BizTalk hizmeti askıya kullanabilirsiniz. Bkz: [Azure BizTalk Hizmeti Yönetimi örnek](http://go.microsoft.com/fwlink/p/?LinkID=329019) hello Windows PowerShell cmdlet'leri toomanage işlemleri için.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Okuma hello XML ileti bir köprünün özel kod bileşeni içinde ek bir ürün reçetesi karakter içerir
Bir köprünün özel kod içinde bir XML iletisi tooread istediğiniz bir senaryo düşünün. Merhaba .NET API System.Text.Encoding.UTF8.GetString(bytes) kullanıyorsanız ek bir ürün reçetesi karakter hello çıkış selamlama iletisine hello başında dahil edilir. Bunu, hello çıktı tooinclude hello istemiyorsanız ek ürün reçetesi karakter kullanmalısınız ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>WCF kullanarak tooa köprüsü iletileri gönderme ölçeklenmez
Gönderilen iletileri WCF kullanarak tooa köprüsü ölçekli değildir. Ölçeklenebilir bir istemcinin istiyorsanız bunun yerine HttpWebRequest kullanmanız gerekir.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>Yükseltme: belirteç sağlayıcı hatası BizTalk Services Önizleme tooGeneral kullanılabilirlik (GA) ' yükselttikten
Etkin toplu işleri bir EDI veya AS2 sözleşmesi yoktur. Merhaba BizTalk hizmeti Önizleme tooGA yükseltildiğinde hello aşağıdaki oluşabilir:

* Hata: hello belirteç sağlayıcısı oluşturamıyor tooprovide bir güvenlik belirteci idi. İleti döndürülen belirteç sağlayıcısı: hello uzak ad çözümlenemedi.
* Toplu görevler iptal edilir.

**Geçici çözüm**: hello BizTalk hizmeti güncelleştirilmiş tooGeneral kullanılabilirlik (GA) sonra hello sözleşmesi yeniden dağıtın.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>Yükseltme: Araç kutusu hello eski köprüsü simgeleri hello BizTalk Services SDK'sı yükselttikten sonra gösterir
Merhaba hello köprüleri temsil eden eski simgeleri vardı, BizTalk Services SDK'ın önceki bir sürümünü yükselttikten sonra hello araç tooshow hello eski simgeler hello köprüleri için devam eder. Ancak, bir köprü tooBizTalk hizmet projesi Tasarımcı yüzeyine eklerseniz, hello yüzeyini hello yeni simgeyi gösterir.  

**Geçici çözüm**. Altında hello .tbd dosyaları silerek bu sorunu çözmek çalışabilirsiniz <system drive>: \Users\<kullanıcı > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>Yükseltme: Önizleme tooGA BizTalk Portal Update'ten bu hello EDI özelliği kullanılabilir değil belirten bir hata gösterebilir.
Hello BizTalk Services Önizleme tooGA yükseltilirken BizTalk Services portalı hello oturum açtıysanız, aşağıdaki hata hello portalında hello alabilirsiniz:  

Bu özellik kullanılamıyor Microsoft Azure BizTalk Services'ın bu sürümünde bir parçası olarak. toouse tooan uygun sürümü bu yetenekleri geçin.  

**Çözümleme**: hello portal, Kapat ve açık hello tarayıcı ve ardından hello portal günlüğüne oturumu kapatın.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>Yükseltme: Yükseltilen tooGA BizTalk Services tamamlandıktan sonra yeni izleme verilerini görünmüyor
BizTalk Hizmetleri Önizleme abonelikte dağıtılmış bir XML köprüsü sahip olduğu bir senaryoyu ele alalım. Toohello köprüsü iletileri göndermek ve BizTalk Services portalı hello üzerinde hello karşılık gelen izleme verileri kullanılamıyor. Şimdi, Hello BizTalk Services portalı ve BizTalk Services çalışma zamanı BITS yükseltilmiş tooGA ve aynı köprüsü endpoint daha önce dağıttığınız bir ileti toohello gönderdiğiniz izleme verilerini hello yükseltmeden sonra gönderilen iletileri gösterilmez varsa.  

### <a name="pipelines-versus-bridges"></a>Ardışık Düzen köprüleri karşılaştırması
Bu belge boyunca hello terim 'ardışık düzen' ve 'köprüleri' birbirlerinin yerine kullanılır. Her ikisi de temelde aynı hello anlamına gelir, BizTalk Services üzerinde dağıtılan bir ileti işleme birimi olan bir şey.  

### <a name="concepts"></a>Kavramlar
[BizTalk Hizmetleri](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

