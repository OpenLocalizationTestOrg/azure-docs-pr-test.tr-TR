---
title: "Azure mantıksal uygulamaları için aaaConnectors | Microsoft Docs"
description: "Tüm hello kullanılabilir Microsoft tarafından yönetilen bağlayıcıların toobuild seçin ve mantıksal uygulamalar oluşturma"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Bağlayıcıların listesi
> [!TIP]
> Merhaba [A-Z tam listesi](#az) (Bu konuda) Logic Apps içinde kullanabileceğiniz tüm hello kullanılabilir bağlayıcılar listeler. [Bağlayıcı ayrıntıları](/connectors/) tüm tetikleyiciler ve Eylemler hello swagger tanımlanan listeler ve her bağlayıcı için herhangi bir sınır aynı zamanda listeler.

Bağlayıcılar, mantıksal uygulama oluşturma işleminin ayrılmaz bir parçasıdır. Bu bağlayıcıların kullanarak, gerçekten şirket içi genişletin ve oluşturduğunuz veri ve zaten verilerle uygulamaları toodo farklı işlemler bulut. Merhaba bağlayıcılar kategorileri aşağıdaki hello kullanılabilir: 

* **Standart bağlayıcılar**: Mantıksal uygulamaları kullandığınızda otomatik olarak kullanılabilir durumdadır ve eklenir. Service Bus, Power BI, Oracle Database, OneDrive ve daha birçok örnek mevcuttur.

* **Tümleştirme hesabı bağlayıcıları**: Bir tümleştirme hesabı satın aldığınızda kullanılabilir. Bu bağlayıcıları kullanarak, XML dönüştürüp doğrulayabilir, AS2 / X12 / EDIFACT ile işletmeden işletmeye iletileri işleyebilir ve düz dosyaları kodlayıp kod çözebilirsiniz. BizTalk Server ile çalışır, bu bağlayıcıların iyi bir tooexpand, BizTalk iş akışlarınızı Azure sığması demektir.  

    BizTalk Server de sahip bir [Logic Apps bağdaştırıcısı](https://msdn.microsoft.com/library/mt787163.aspx) mantığı uygulamadan alma ve gönderme tooa mantıksal uygulama içerir.

* **Enterprise bağlayıcıları**: MQ ve SAP içerir. Ek bir maliyet karşılığında sunulur. 

[Logic Apps fiyatlandırma](https://azure.microsoft.com/pricing/details/logic-apps/) ve [fiyatlandırma modeli](../logic-apps/logic-apps-pricing.md) hello maliyetlerinde daha fazla ayrıntı sağlar. 

## <a name="popular-connectors"></a>Popüler bağlayıcılar
Bu bağlayıcıları kullanarak veri ve bilgileri başarılı bir şekilde işleyen binlerce uygulama ve milyonlarca yürütme vardır. Aşağıdaki tablonun hello hello en popüler ve bazı Sık Kullanılanlar kullanıcılarımızın ile listeler:

| |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][AzureBlobStorageicon]<br/>**Azure Blob<br/>Storage**][AzureBlobStoragedoc] | Depolama hesabınızı ile herhangi bir görevi tooautomate istiyorsanız, bu bağlayıcı bakmanız gerekir. CRUD (create, read, update, delete) işlemlerini destekler. | [![API Icon][Azure-Functionsicon]<br/>**Azure İşlevleri**][azure-functionsdoc] | Özel C# veya node.js kod parçacıkları çalıştıran işlevler oluşturun ve sonra bu işlevleri mantıksal uygulamalarınızda kullanın.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Merhaba bağlayıcıları için çoğu sorulan biri. Müşteri adayları ve daha fazla iş akışlarıyla otomatikleştirme tetikleyiciler ve Eylemler toohelp sahiptir. | [![API Icon][Event-Hubs-icon]<br/>**Event Hubs**][event-hubs-doc] | Bir Olay Hub’ındaki olayları tüketin ve yayımlayın. Örneğin, olay hub'ları kullanarak mantığı uygulamanızdan çıkış almak ve hello çıktı tooa gerçek zamanlı analiz sağlayıcısı gönderin. |
| [![API Icon][FTPicon]<br/>**FTP**][FTPdoc] | FTP sunucunuzun erişilebilir olması durumunda iş akışları toowork dosyalar ve klasörlerle otomatikleştirebilirsiniz sonra Internet hello. <br/><br/>SFTP hello SFTP Bağlayıcısı ile de kullanılabilir. | [![API Icon][HTTPicon]<br/>**HTTP**][httpdoc] | Logic apps toocommunicate HTTP üzerinden herhangi bir uç nokta ile kullanın. |
| [![API Icon][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Tetikleyiciler ve çok daha fazla Eylemler toouse Office 365 e-posta ve olaylar, iş akışlarınızı içinde çok sayıda. <br/><br/>Bu bağlayıcı içeren bir *onay e-posta* eylem tooapprove tatil istekleri gider raporlar ve benzeri. <br/><br/>Office 365 kullanıcıları hello Office 365 kullanıcıları Bağlayıcısı ile de kullanılabilir.| [![API Icon][HTTP-Requesticon]<br/>**İstek / Yanıt**][HTTP-Requestdoc] | Bu bağlayıcı bir HTTPS URL'si sağlar. Merhaba mantıksal uygulama isteği toothis URL aldığında, hello mantıksal uygulama başlatır. |
| [![API Icon][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Kolayca, Salesforce hesap tooget erişim tooobjects, müşteri adayları gibi ve daha fazla ile oturum açın. |  [![API Icon][Service-Busicon]<br/>**Service Bus**][Service-Busdoc] | Merhaba en popüler bağlayıcı logic apps içinde tetikleyiciler ve Eylemler toodo zaman uyumsuz ileti gönderme ve yayımlama/abonelik kuyruklar, abonelikleri ve konuları içerir. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | SharePoint ile bir işlem yapıyor ve otomasyondan yararlanabiliyorsanız, bu bağlayıcıya bakmanız önerilir. Şirket içi SharePoint ve SharePoint Online ile birlikte kullanılabilir. | [![API Icon][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Merhaba birini en sık kullanılan bağlayıcılar, tooan bağlanabilir SQL Server ve Azure SQL veritabanı şirket içi. | 
| [![API Icon][Twittericon]<br/>**Twitter**][Twitterdoc] | Bir Twitter hesabıyla kolayca oturum açın ve yeni tweet gönderildiğinde bir iş akışı başlatın. Daha sonra bu tweet'leri tooa SQL database veya SharePoint listesi kaydedin. | | | 

## <a name="integration-account-connectors"></a>Tümleştirme hesabı bağlayıcıları 

Merhaba Enterprise Integration Pack (EIP) iyi bilinen toohello BizTalk Server topluluğu olan bağlayıcıları içerir. Satın aldığınız zaman bir [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), ayrıca bağlayıcıları aşağıdaki hello elde edersiniz: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][as2icon]<br/>**AS2</br> kod çözme**][as2decode] | [![API Icon][as2icon]<br/>**AS2</br> kodlama**][as2encode] | [![API Icon][x12icon]<br/>**EDIFACT</br> kod çözme**][EDIFACTdecode] | [![API Icon][x12icon]<br/>**EDIFACT</br> kodlama**][EDIFACTencode] |
[![API Icon][flatfileicon]<br/>**Düz dosya</br> kodlama**][flatfiledoc] | [![API Icon][flatfiledecodeicon]<br/>**Düz dosya</br> kod çözme**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Tümleştirme<br/>hesabı**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**XML<br/>Dönüştürme**][xmltransformdoc] |
| [![API Icon][x12icon]<br/>**X12</br> kod çözme**][x12decode] | [![API Icon][x12icon]<br/>**X12</br> kodlama**][x12encode] | [![API Icon][xmlvalidateicon]<br/>**XML <br/>validation**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Kurumsal bağlayıcılar

Logic apps içinde tooyour kurumsal uygulamalar bağlayın.

|  |  |
| --- | --- |
|[![API Icon][MQicon]<br/>**MQ**][mqdoc]|[![API Icon][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>A’dan Z’ye tam liste

[Bağlayıcı ayrıntıları](/connectors/) tüm tetikleyiciler ve Eylemler hello swagger tanımlanan liste ve ayrıca her bağlayıcı için herhangi bir sınır listeler.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10-8 Randevu Planlama<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Azure API Management<br/>Azure Uygulama Hizmetleri<br/>Azure Uygulaması<br/>Azure Otomasyonu<br/>[Azure Blob Depolama][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Azure İşlevleri][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Azure Kuyrukları<br/>Azure Resource Manager<br/>[Azure SQL Veritabanı][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Kıyaslama E-postası<br/>Bing Arama<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>Bilişsel Hizmetler Görüntü İşleme API’si<br/>Bilişsel Hizmetler Yüz Tanıma API’si<br/>Bilişsel Hizmetler LUIS<br/>Bilişsel Hizmetler Metin Analizi<br/>Common Data Service<br/>İçerik Dönüştürme<br/>Denetleme-Sonlandırma<br/>[Özel API’ler / web uygulamaları][api/web-appdoc]<br/><br/><a name="d"></a>Veri İşlemleri<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Event Hubs][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[Dosya Sistemi][filesystemdoc]<br/>[Düz Dosya][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>Freshservice<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google Takvim<br/>Google Kişiler<br/>Google Drive<br/>Google E-Tablolar<br/>Google Görevler<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP Web Kancası][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Tümleştirme Hesabı<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Orta<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Hava Durumu<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Office 365 Kullanıcıları<br/>Office 365 Video<br/>OneDrive<br/>OneDrive İş<br/>OneNote (İş)<br/>[Oracle Veritabanı][oracle-db-doc]<br/>Outlook Customer Manager<br/>Outlook Görevleri<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[İstek / Yanıt][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP Uygulama Sunucusu][sapconnector]<br/>[SAP İleti Sunucusu][sapconnector]<br/>[Zamanlama][recurrencedoc]<br/>Kapsam<br/>SendGrid<br/>İletileri toobatch Gönder<br/>[Service Bus][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[XML Dönüştürme][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Değişkenler<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[XML Doğrulaması][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> bir Azure hesabı için kaydolmadan önce Azure Logic Apps ile başlatılan tooget Git çok[deneyin Logic Apps](https://tryappservice.azure.com/?appservice=logic). Başlangıç düzeyinde kısa süreli mantıksal uygulamayı hemen oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.

## <a name="connectors-as-triggers-and-actions"></a>Tetikleyici ve eylem olarak bağlayıcılar

**Tetikleyici**, mantıksal uygulamanızın bir örneğini başlatır veya çalıştırır. Bazı bağlayıcılar, belirli olaylar meydana geldiğinde uygulamanızı bilgilendiren tetikleyiciler sağlar. Örneğin, FTP hello hello bağlayıcının `OnUpdatedFile` mantıksal uygulamanızı bir dosya güncelleştirildiğinde başlayan tetikleyici. 

Logic apps tetikleyici türleri aşağıdaki hello şunlardır:  

* *Yoklama Tetikleyicileri*: Bu Tetikleyiciler hizmetinizin belirtilen sıklığı toocheck en yeni verileri yoklamak. 

    Yeni veriler kullanılabilir olduğunda, uygulamanızın yeni bir örneğini hello verilerle giriş olarak çalışır. 

* *Tetikleyiciler anında*: Bu Tetikleyiciler uç noktada verileri dinlemek veya bir olay için toohappen, sonra mantıksal uygulamanızı yeni bir örneğini tetikler.

* *Yineleme tetikleyicisi*: Bu tetikleyici, önceden belirlenmiş bir zamanlamaya göre mantıksal uygulamanızın bir örneğini başlatır.

Bağlayıcılar ayrıca iş akışınızda kullanabileceğiniz **eylemler** sağlar. Örneğin, mantıksal uygulamanız verileri arayabilir ve bu verileri daha sonra mantıksal uygulamanızda kullanabilir. Daha belirgin olarak bir SQL veritabanında müşteri verileri aramak ve sonra bu müşteri verileri toobuild akışınızı kullanın. 

> [!TIP]
> [Bağlayıcılara genel bakış](connectors-overview.md) bölümünde tetikleyici ve eylemler hakkında daha fazla bilgi verilmektedir. 


## <a name="message-manipulation-actions"></a>İleti işleme eylemleri

Mantıksal uygulamalar, yük verilerinizi değiştirebilen veya işleyebilen yerleşik eylemler içerir. Merhaba yerleşik **veri işlemleri** bağlayıcı eylemleri aşağıdaki hello içerir: 

| | |
|---|---|
| **Oluştur** | Derleme veya değerleri veya nesneler toouse daha sonra oluşturmak veya gibi iş akışı oluşturabilirsiniz. Örneğin, bir JSON nesnesi birden çok adımı değerlerle yazar veya sabit tooreference daha sonra çalıştırmak bir mantıksal uygulama içinde hesaplanamıyor. |
| **CSV tablosu oluşturma**<br/>**HTML tablosu oluşturma** | Dizi sonuç kümesini bir CSV veya HTML tablosuna dönüştürün. Örneğin, hello CRM "Listesi kayıtları" eylemi ekleyin ve bugün eklenen kayıtları için bir filtre ekleyin. Ardından, bir HTML tablosu bir e-posta gibi hello sonuçları gönderin. |
| **Filtre dizisi** (sorgu) | Sizi ilgilendiren bir sonuç kümesi toohello girişleri filtreleyin. Örneğin, tüm tweet'leri ile arama `#Azure`, ve ardından "filtre" Merhaba tweet'leri tooonly dönüş sonucu döndürdü `Tweeted_by_followers > 50`. |
| **Birleştir** | Bir diziyi bazı sınırlayıcılarla birleştirin. Örneğin, hello algılamak anahtar tümcecikleri işlemi anahtar tümcecikleri bir dizi döndürür. Bu tümcecikleri bir `,` veya benzer bir şey ile “birleştirebilirsiniz”. Bu nedenle, `["Some", "Phrase"]` yerine `"Some, Phrase"` elde edersiniz. |
| **JSON Ayrıştırma** | Out ayrıştırabilir ve hello Tasarımcısı'nda bir JSON nesnesinden değerlere erişebilir. Azure işlevinizi bir JSON yükü döndürürse, örneğin, daha sonra onu tooaccess hello JSON özellikleri daha sonra başka bir adımda ayrıştıramıyor. Merhaba eylem ayrıca bu hello JSON eşleşmeleri hello belirtilen şema çalışma zamanında doğrular. | 
| **Seç** | Daha fazla işleme için bir dizinin belirli özelliklerini seçin. SQL'de "Kayıtları listeleme" seçeneğini belirlerseniz ve 15 sütun döndürülürse daha fazla işleme için bu sütunların yalnızca birkaçını seçin. Merhaba çıktı yalnızca seçtiğiniz hello özellikleri içeren bir dizidir. |

## <a name="custom-connectors-and-azure-certification"></a>Özel bağlayıcılar ve Azure sertifikaları 

toocall özel kodu çalıştırmak veya bağlayıcıları olarak kullanılabilen değil API uygulamasına hello Logic Apps platformu tarafından genişletebilir [özel bağlayıcılar olarak API uygulamaları REST tabanlı oluşturma](../logic-apps/logic-apps-create-api-app.md). 

Özel API Apps ortak ve kullanılabilir toouse azure'da toomake istiyorsanız adaylar toohello gönderme [Azure Microsoft Sertifikalı program](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Yardım alın

tooask sorular, soruları ve diğer Azure mantıksal uygulamaları kullanıcıların gittiğini, bkz: Git toohello [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

Bağlayıcılarla ilgili olarak değinmediğimiz bir konu başlığı veya önemli olduğunu düşündüğünüz herhangi bir ayrıntı var mı? Yanıt Evet ise, tooour mevcut konularda ekleyerek yardımcı veya kendi yazma. Belgelerimiz açık kaynak olup GitHub'da barındırılır. Başlamak için [GitHub depomuza](https://github.com/Microsoft/azure-docs) gidin. 

## <a name="next-steps"></a>Sonraki adımlar
* [İlk mantıksal uygulamanızı oluşturma](../logic-apps/logic-apps-create-a-logic-app.md)
* [Mantıksal uygulamalar için özel API’ler oluşturma](../logic-apps/logic-apps-create-api-app.md)
* [Mantıksal uygulamalarınızı izleyin](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Mantıksal uygulamaları App Service API Apps ile tümleştirin"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Blob kapsayıcınızdaki dosyaları Azure blob depolama bağlayıcısı ile yönetin"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Mantıksal uygulamaları Azure İşlevleri ile tümleştirin"
[db2doc]: ./connectors-create-api-db2.md "Merhaba Bulut veya şirket içi DB2 tooIBM bağlayın. Bir satırı güncelleştirin, bir tabloyu alın ve diğer işlemleri yapın"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "CRM Online verileriyle çalışabilirsiniz tooDynamics CRM Online'a bağlanın"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "TooAzure olay hub'ları bağlayın. Logic Apps ile Event Hubs arasında olay gönderip alma"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Tooan şirket içi dosya sistemine bağlanma"
[ftpdoc]: ./connectors-create-api-ftp.md "Connect tooan FTP / FTPS sunucusuna karşıya yükleme gibi FTP görevler için alma, dosyaları ve daha fazla silme"
[httpdoc]: ./connectors-native-http.md "Merhaba HTTP Bağlayıcısı ile HTTP çağrıları yapma"
[http-requestdoc]: ./connectors-native-reqres.md "HTTP istekleri ve yanıtları tooyour mantıksal uygulamalar eylemleri ekleme"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "HTTP + Swagger bağlayıcısı ile HTTP çağrıları yapın"
[informixdoc]: ./connectors-create-api-informix.md "Merhaba Bulut veya şirket içi tooInformix bağlayın. Bir satır, liste hello tabloları ve daha fazlasını okuyun"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Mantıksal uygulamaları iç içe geçmiş iş akışları ile tümleştirin"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Tooyour Office 365 hesabı bağlayın. E-posta gönderip alın, takvim ve kişilerinizi yönetin ve daha fazlasını yapın"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Bağlantı tooan Oracle veritabanı tooadd, Ekle, Sil satırları ve daha fazla bilgi"
[mqdoc]: ./connectors-create-api-mq.md "TooMQ şirket içi veya Azure'a bağlanmak ve ileti gönderme ve alma"
[recurrencedoc]:  ./connectors-native-recurrence.md "Mantıksal uygulamalar için yinelenen eylemleri tetikleyin"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Tooyour Salesforce hesabı bağlayın. Hesapları, müşteri adaylarını, fırsatları ve daha fazlasını yönetin"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Tooan şirket içi SAP sistemine bağlanmak"
[service-busdoc]: ./connectors-create-api-servicebus.md "Service Bus Kuyruklarından ve Konu Başlıklarından iletiler gönderin ve Service Bus Kuyrukları ile Aboneliklerinden iletiler alın"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Çevrimiçi tooSharePoint bağlayın. Belgeleri yönetin, öğeleri listeleyin ve daha fazlasını yapın"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Şirket içi sunucuda tooSharePoint bağlayın. Belgeleri yönetin, öğeleri listeleyin ve daha fazlasını yapın"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "TooAzure SQL Database veya SQL server bağlayın. SQL veritabanı tablosunda girdiler oluşturun, güncelleştirin, alın ve silin."
[twitterdoc]: ./connectors-create-api-twitter.md "TooTwitter bağlanın. Zaman çizelgelerini alın, tweetler gönderin ve daha fazlasını yapın"
[webhookdoc]: ./connectors-native-webhook.md "Web kancası eylemleri ve Tetikleyicileri tooyour mantıksal uygulamalar ekleme"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Enterprise integration AS2 hakkında bilgi edinin."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Enterprise integration X12 hakkında bilgi edinin."
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Enterprise integration düz dosyası hakkında bilgi edinin."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Enterprise integration düz dosyası hakkında bilgi edinin."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Enterprise integration XML doğrulaması hakkında bilgi edinin."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Enterprise integration dönüştürmeleri hakkında bilgi edinin."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Enterprise integration AS2 kod çözme hakkında bilgi edinin"
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Enterprise integration AS2 kodlama hakkında bilgi edinin"
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Enterprise integration X12 kod çözme hakkında bilgi edinin"
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Enterprise integration X12 kodlama hakkında bilgi edinin"
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Enterprise integration EDIFACT kod çözme hakkında bilgi edinin"
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Enterprise integration EDIFACT kodlama hakkında bilgi edinin"
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Tümleştirme hesabınızda şemalar, haritalar, iş ortakları ve daha fazlasını arayın"


[boxDoc]: ./connectors-create-api-box.md "TooBox bağlanın. Dosyalarınızı karşıya yükleyin, silin, listeleyin ve diğer işlemleri yapın"
[delaydoc]: ./connectors-native-delay.md "Gecikmeli eylemleri gerçekleştirin"
[dropboxdoc]: ./connectors-create-api-dropbox.md "TooDropbox bağlanın. Dosyalarınızı karşıya yükleyin, silin, listeleyin ve diğer işlemleri yapın"
[facebookdoc]: ./connectors-create-api-facebook.md "TooFacebook bağlanın. Tooa zaman çizelgesi işlemleri sonrasında, sayfa akışı ve daha fazla bilgi edinin"
[githubdoc]: ./connectors-create-api-github.md "TooGitHub bağlanmak ve sorunları izlemek"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Verilerinizi ile çalışabilmek için tooGoogleDrive Bağlan"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Sayfalarınızı değiştirebilirsiniz tooGoogle sayfaları bağlanın"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Görevlerinizi yönetebilirsiniz tooGoogle görevleri bağlandığında"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "TooGoogle Takvim bağlanır ve Takvim yönetebilirsiniz."
[http-responsedoc]: ./connectors-native-reqres.md "HTTP istekleri ve yanıtları tooyour mantıksal uygulamalar eylemleri ekleme"
[instagramdoc]: ./connectors-create-api-instagram.md "TooInstagram bağlanın. Olayları tetikleyin veya üzerinde işlem yapın"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Tooyour MailChimp hesabı bağlayın. Postaları yönetin ve otomatikleştirin"
[mandrilldoc]: ./connectors-create-api-mandrill.md "İletişim için tooMandrill Bağlan"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "TooMicrosoft Çeviricisi bağlayın. Metinleri çevirin, dilleri algılayın ve daha fazlasını yapın" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Office 365 için video bilgileri, video listeleri ile kanallar ve kayıttan yürütme URL'lerini alın"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Tooyour bağlanmak kişisel Microsoft OneDrive. Dosyaları karşıya yükleyin, silin, listeleyin ve daha fazlasını yapın"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Tooyour iş Microsoft OneDrive bağlayın. Dosyalarınızı karşıya yükleyin, silin, listeleyin ve diğer işlemleri yapın"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Tooyour Outlook posta bağlayın. E-posta, takvim, kişi ve diğerlerini yönetin"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "TooMicrosoft Project Online'a bağlanır. Proje, görev, kaynaklar ve daha fazlasını yönetin"
[querydoc]: ./connectors-native-query.md "Seçin ve hello sorgu eylemi dizilerle filtre"
[rssdoc]: ./connectors-create-api-rss.md "Yayımlama ve akış öğelerini almak, yeni bir öğe yayımlanan tooan RSS olduğunda işlemleri tetiklemesini akış."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "TooSendGrid bağlanın. E-posta gönderin ve alıcı listelerini yönetin"
[sftpdoc]: ./connectors-create-api-sftp.md "Tooyour SFTP hesabı bağlayın. Dosyalarınızı karşıya yükleyin, alın, silin ve diğer işlemleri yapın"
[slackdoc]: ./connectors-create-api-slack.md "TooSlack bağlanmak ve tooSlack kanalları iletileri gönderme"
[smtpdoc]: ./connectors-create-api-smtp.md "Tooa SMTP sunucusuna bağlanmak ve ekler içeren e-posta Gönder"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "İletişim için tooSparkPost bağlanır"
[trellodoc]: ./connectors-create-api-trello.md "TooTrello bağlanın. Projelerinizi yönetin ve herhangi bir şeyi herhangi bir kimseyle düzenleyin"
[twiliodoc]: ./connectors-create-api-twilio.md "TooTwilio bağlanın. İletiler gönderip alın, mevcut numaraları alın, gelen telefon numaralarını yönetin ve daha fazlasını yapın"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "TooWunderlist bağlanın. Görevlerinizi ve yapılacaklar listenizi yönetin, tüm işlerinizi eşitleyin ve daha fazlasını yapın"
[yammerdoc]: ./connectors-create-api-yammer.md "TooYammer bağlanın. İleti gönderin, yeni iletiler alın ve daha fazlasını yapın"
[youtubedoc]: ./connectors-create-api-youtube.md "TooYouTube bağlanın. Videolarınızı ve kanallarınızı yönetin"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
