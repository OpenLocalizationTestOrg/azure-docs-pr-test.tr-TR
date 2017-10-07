---
title: "Öğretici: Azure BizTalk Services kullanarak EDIFACT faturaları işlem | Microsoft Docs"
description: "Nasıl toocreate hello kutusunu Bağlayıcısı veya API uygulamasını yapılandırma ve Azure App Service'te bir mantıksal uygulama kullanın"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Öğretici: Azure BizTalk Services kullanarak işlem EDIFACT faturalar

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Merhaba BizTalk Services portalı tooconfigure kullanabilir ve X12 ve EDIFACT sözleşmelerini dağıtabilirsiniz. Bu öğreticide, nasıl toocreate değiştirmek için bir EDIFACT sözleşmesi ticaret iş ortakları arasında faturalar adresindeki arayın. Bu öğretici EDIFACT ileti değiş tokuşu Northwind ve Contoso olmak üzere iki ticari ortaklar içeren bir uçtan uca iş çözüm yazılır.  

## <a name="sample-based-on-this-tutorial"></a>Bu öğretici temel örnek
Bu öğretici bir örnek yazılır **EDIFACT faturaları kullanarak BizTalk Services gönderme**, kullanılabilir toodownload hello gelen olduğu [MSDN kod Galerisi'nden](http://go.microsoft.com/fwlink/?LinkId=401005). Merhaba örneği kullanmak ve Bu öğretici toounderstand hello örnek nasıl oluşturulmuş gidin. Veya Bu öğretici toocreate kullanabilir başından başlayarak kendi çözümü. Bu çözümün nasıl oluşturulmuş anlamanız Bu öğretici hello İkinci yaklaşımı yöneliktir. Ayrıca, mümkün olduğunca hello öğretici hello örneği ile tutarlıdır ve hello örnek kullanılan yapılar (örneğin, şemalar, Dönüşümlerin) için aynı adı kullanan hello.  

> [!NOTE]
> Bu çözüm EAI köprü tooan EDI köprüsü ileti gönderme içerdiğinden hello yeniden kullanır [BizTalk Services örnek zincirleme köprüsü](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) örnek.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Merhaba çözüm ne yapar?
Bu çözümde, Northwind EDIFACT faturalar Contoso alır. Bu faturalar standart EDI biçimde değil. Bu nedenle, hello fatura tooNorthwind göndermeden önce bu dönüştürülmüş tooan EDIFACT (INVOIC olarak da bilinir) fatura belge olmalıdır. Alındığında, Northwind hello EDIFACT fatura işlemek ve denetim (CONTRL olarak da bilinir) ileti tooContoso dönüş gerekir.

![][1]  

tooachieve bu iş senaryosu, Contoso Microsoft Azure BizTalk Services ile sağlanan hello özelliklerini kullanır.

* Contoso EAI köprüleri tootransform hello özgün fatura tooEDIFACT INVOIC kullanır.
* Merhaba EAI köprü sonra EDI hello BizTalk Services portalı yapılandırılmış anlaşmanın bir parçası olarak dağıtılan köprüsü Gönder hello ileti tooan gönderir.
* Merhaba EDI gönderme köprüsü hello EDIFACT INVOIC işler ve tooNorthwind yönlendirir.
* Merhaba fatura aldıktan sonra Northwind EDI alma hello anlaşmanın bir parçası dağıtılan köprüsü CONTRL ileti toohello döndürür.  

> [!NOTE]
> İsteğe bağlı olarak, bu çözüm ayrıca nasıl yığınlardaki ayrı ayrı her bir fatura göndermek yerine toosend hello toplu işleme toouse faturalar gösterir.  
> 
> 

toocomplete hello senaryosu, toosend Contoso tooNorthwind fatura veya Northwind onay almak Service Bus kuyruklarını kullanın. Bu kuyruklar, bir yükleme olarak kullanılabilir ve kullanılabilir hello örnek paketinde bulunan bir istemci uygulaması kullanılarak oluşturulabilir. Bu öğreticinin bir parçası olarak.  

## <a name="prerequisites"></a>Ön koşullar
* Hizmet veri yolu ad alanı olması gerekir. Bir ad alanı oluşturma ile ilgili yönergeler için bkz: [nasıl yapılır: oluşturmak veya bir hizmet veri yolu hizmet Namespace değiştirmek](https://msdn.microsoft.com/library/azure/hh674478.aspx). Bize sağlanan, bir hizmet veri yolu ad alanı zaten sahip olduğunuzu varsaymaktadır adlı **edifactbts**.
* BizTalk Services aboneliğinizin olması gerekir. Yönergeler için bkz: [Klasik Azure portalını kullanarak BizTalk hizmeti oluşturma](http://go.microsoft.com/fwlink/?LinkID=302280). Bu öğretici için bize adlı bir BizTalk Services abonelik olduğunu varsayın **contosowabs**.
* BizTalk Services aboneliğinize hello BizTalk Services portalı kaydedin. Yönergeler için bkz: [hello BizTalk Services portalı üzerinde bir BizTalk hizmeti dağıtımı kaydetme](https://msdn.microsoft.com/library/hh689837.aspx)
* Visual Studio yüklü olmalıdır.
* BizTalk Services SDK'sı olması gerekir. İndirebilirsiniz SDK'dan hello [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>1. adım: hello hizmet veri yolu Kuyrukları Oluşturma
Bu çözüm, ticari ortaklar arasında Service Bus kuyrukları tooexchange iletileri kullanır. Contoso ve Northwind iletileri hello EAI ve/veya EDI köprüleri bunları burada tüketen gelen toohello sıraları gönderin. Bu çözüm için üç hizmet veri yolu kuyrukları gerekir:

* **northwindreceive** – Northwind Contoso hello fatura bu sırayı alır.
* **contosoreceive** – Contoso Bu kuyruk Northwind hello bildirim alır.
* **askıya** – yönlendirilmiş toothis sıra tüm askıya alınan iletileri şunlardır. İşleme sırasında başarısız olursa iletileri askıya alınır.

Bu hizmet veri yolu kuyrukları hello örnek paketinde bulunan bir istemci uygulaması kullanarak oluşturabilirsiniz.  

1. Merhaba örnek indirdiğiniz hello konumdan açmak **öğretici gönderme faturaları kullanarak BizTalk Services EDI Bridges.sln**.
2. Tuşuna **F5** toobuild ve başlangıç hello **öğretici istemci** uygulama.
3. Merhaba ekranında hello Service Bus ACS ad alanı, verenin adı ve verenin anahtarı girin.
   
   ![][2]  
4. Bir ileti kutusu üç sıraları hizmet veri yolu ad alanınız içinde oluşturulacak ister. **Tamam** düğmesine tıklayın.
5. Başlangıç Öğreticisi istemci çalışan bırakın. Merhaba açın, **Service Bus** > ***hizmet veri yolu ad alanınız*** > **sıraları**ve hello üç sıraları oluşturulduğunu doğrulayın.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>2. adım: Oluşturma ve ticari ortak sözleşmesi dağıtma
Contoso Northwind arasındaki ticari ortak sözleşmesi oluşturun. Ticari ortak sözleşmesi hangi ileti şema toouse gibi hello iki iş ortakları arasında bir ticari sözleşmesini tanımlayan Protokolü toouse, vb. Mesajlaşma. Bir toosend iletileri tootrading iş ortakları, ticari ortak sözleşmesi iki EDI köprüleri içerir (Merhaba adlı **EDI gönderme köprüsü**) ve iş ortakları ticari bir tooreceive iletilerinin (hello adlı **köprüsüEDIalma**).

Merhaba bağlamında bu çözümün hello EDI gönderme köprüsü toohello gönderme tarafı hello Sözleşmesi'nin karşılık gelir ve kullanılan toosend hello EDIFACT fatura Contoso tooNorthwind olur. Benzer şekilde, hello EDI alma köprüsü toohello alma tarafı hello Sözleşmesi'nin karşılık gelir ve kullanılan tooreceive onayları Northwind gelen olduğu.  

### <a name="create-hello-trading-partners"></a>Merhaba ticaret ortakları oluşturun
toostart, Contoso ve Northwind için ticari ortaklar oluşturun.  

1. Hello üzerinde hello BizTalk Services Portalı'nda **ortakları** sekmesini tıklatın, **Ekle**.
2. Merhaba yeni iş ortağı sayfasında girin **Contoso** bir ortak adı ve ardından olarak **kaydetmek**.
3. Yineleme hello adım toocreate hello ikinci iş ortağı, **Northwind**.  

### <a name="create-hello-agreement"></a>Merhaba sözleşmesi oluşturma
Ticari ortak sözleşmeleri ortakları ticari iş profilleri arasında oluşturulur. Bu çözüm hello ortakları oluşturduğumuz olduğunda otomatik olarak oluşturulan hello varsayılan iş ortağı profilleri kullanır.  

1. Hello BizTalk Services Portalı'da, tıklatın **anlaşmaları** > **Ekle**.
2. Merhaba yeni anlaşmanın içinde **genel ayarları** sayfasında, aşağıdaki hello görüntüde gösterildiği gibi hello değerlerini belirtin ve ardından **devam**.
   
   ![][3]  
   
   Tıklattıktan sonra **devam**, iki sekme **alma ayarı** ve **gönderme ayarları** kullanılabilir hale gelir.
3. Contoso Northwind arasındaki Hello gönderme sözleşmesi oluşturun. Bu anlaşma, Contoso hello EDIFACT fatura tooNorthwind nasıl göndereceğini yönetir.
   
   1. Tıklatın **gönderme ayarları**.
   2. Merhaba Hello varsayılan değerlerine korumak **gelen URL**, **dönüştürme**, ve **Batching** sekmeleri.
   3. Merhaba üzerinde **Protokolü** sekmesinde hello **şemaları** bölümünde, hello karşıya **EFACT_D93A_INVOIC.xsd** şema. Bu şemayı hello örnek paketi ile birlikte kullanılabilir.
      
      ![][4]  
   4. Merhaba üzerinde **aktarım** sekmesinde, hello Service Bus kuyruklarını hello ayrıntılarını belirtin. Merhaba gönderme tarafı anlaşması için kullandığımız hello **northwindreceive** toosend hello EDIFACT fatura tooNorthwind sıraya ve hello **askıya** tooroute işleme ve misiniz sırasında başarısız iletileri kuyruğa askıya alındı. Bu kuyruklar oluşturulan **1. adım: hello hizmet veri yolu Kuyrukları Oluşturma** (Bu konudaki).
      
      ![][5]  
      
      Altında **Aktarım Ayarları > taşıma türü** ve **ileti askıya Ayarları > taşıma türü**, Azure hizmet veri yolu seçin ve hello görüntüde gösterildiği gibi hello değerler sağlayın.
4. Merhaba oluşturmak Contoso ve Northwind arasında sözleşmesi alırsınız. Bu anlaşma nasıl Contoso hello Northwind alındısı yönetir.
   
   1. Tıklatın **alma ayarlarını**.
   2. Merhaba Hello varsayılan değerlerine korumak **aktarım** ve **dönüştürme** sekmeleri.
   3. Merhaba üzerinde **Protokolü** sekmesinde hello **şemaları** bölümünde, hello karşıya **EFACT_4.1_CONTRL.xsd** şema. Bu şemayı hello örnek paketi ile birlikte kullanılabilir.
   4. Merhaba üzerinde **rota** sekmesinde, Northwind gelen onayları yönlendirilmiş tooContoso yalnızca bir filtre tooensure oluşturun. Altında **yönlendirme ayarlarını**, tıklatın **Ekle** toocreate hello yönlendirme filtre.
      
      ![][6]  
      
      1. İçin değerler sağlayın **kural adı**, **yol kuralı**, ve **rota hedef** hello görüntüde gösterildiği gibi.
      2. **Kaydet** düğmesine tıklayın.
   5. Merhaba üzerinde **rota** yeniden sekmesinde, askıya alınmış onayları (işleme sırasında başarısız onayları) burada yönlendirilir belirtin. Merhaba aktarım türü tooAzure Service Bus ayarlayın, hedef türü çok rota**sıra**, kimlik doğrulama türü çok**paylaşılan erişim imzası** (SAS), Service Bus hello için hello SAS bağlantı dizesi sağlayın ad alanı ve ardından hello kuyruk adı olarak **askıya**.
5. Son olarak, tıklatın **dağıtma** toodeploy hello anlaşma. Burada hello gönderip anlaşmaları Not hello uç noktaları dağıtılan.
   
   * Merhaba üzerinde **gönderme ayarları** sekmesinde, altında **gelen URL**, hello endpoint unutmayın. toosend EDI gönderme köprüsü hello kullanarak Contoso tooNorthwind gelen iletiyi, ileti toothis endpoint göndermeniz gerekir.
   * Merhaba üzerinde **alma ayarı** sekmesinde, altında **aktarım**, hello endpoint unutmayın. toosend hello EDI kullanarak Northwind tooContoso iletiden köprüsü almak, bir ileti toothis uç noktası göndermeniz gerekir.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>3. adım: Oluşturma ve hello BizTalk Services projesi dağıtma
Merhaba önceki adımda, EDI sözleşmeleri tooprocess EDIFACT faturaları ve gönderip onayları almaya hello dağıtıldı. Bu sözleşmeler toohello standart EDIFACT ileti şeması uygun işlem iletileri görüntüleyebilirsiniz. Ancak, bu çözüm için hello senaryo şirket içi bir özel şemada bir fatura tooNorthwind Contoso gönderir. Merhaba iletisi EDI gönderme köprüsü toohello gönderilmeden önce bu nedenle, onu hello şirket içi şema toohello standart EDIFACT fatura şemadan dönüştürülmesi gerekir. Merhaba BizTalk Services EAI proje gerçekleştirir.

Merhaba BizTalk Services projesi **InvoiceProcessingBridge**, dönüşümler ileti hello de parçası olarak indirdiğiniz hello örneği bulunmaktadır. başlangıç projesi yapıları aşağıdaki hello içerir:

* **INHOUSEINVOICE. XSD** – tooNorthwind gönderilen hello şirket içi faturayı şeması.
* **EFACT_D93A_INVOIC. XSD** – hello standart EDIFACT fatura şeması.
* **EFACT_4.1_CONTRL. XSD** – şeması hello EDIFACT bildirim Northwind tooContoso gönderir.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** – hello şirket içi faturayı şema toohello standart EDIFACT fatura şema eşlemeleri dönüştürme hello.  

### <a name="create-hello-biztalk-services-project"></a>Merhaba BizTalk Services projesi oluşturma
1. Hello Visual Studio çözümü, hello InvoiceProcessingBridge projenizi genişletin ve ardından hello açın **MessageFlowItinerary.bcs** dosya.
2. Merhaba tuvalde herhangi bir yere tıklayın ve ayarlayın hello **BizTalk hizmeti URL'si** içindeki BizTalk Services abonelik adınızı özelliği kutusunu toospecify hello. Örneğin, `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Merhaba Araç Kutusu'ndan sürükleyin bir **Xml One-Way köprüsü** toohello tuvale. Set hello **varlık adı** ve **göreli adres** hello özelliklerini köprüsü çok**ProcessInvoiceBridge**. Çift **ProcessInvoiceBridge** tooopen hello köprüsü yapılandırması yüzeyini.
4. Merhaba içinde **ileti türleri** kutusunda, hello artı (**+**) düğmesini toospecify hello şeması hello gelen ileti. Merhaba gelen ileti hello EAI köprü için her zaman hello şirket içi faturayı olduğundan, bu çok ayarlamak**INHOUSEINVOICE**.
   
   ![][8]  
5. Hello tıklatın **Xml dönüştürme** şekli ve hello özelliği kutusunda, hello **eşlemeleri** özelliği, hello üç nokta düğmesine (**...** ) düğmesi. Merhaba, **eşlemeleri seçimi** iletişim kutusu, select hello **INHOUSEINVOICE_to_D93AINVOIC** dönüşüm dosyasında ve ardından **Tamam**.
   
   ![][9]  
6. Çok dön**MessageFlowItinerary.bcs**ve hello Araç Kutusu'ndan sürükleyin bir **iki yönlü dış hizmet uç noktası** hello sağında toohello **ProcessInvoiceBridge**. Ayarlama, **varlık adı** özelliği çok**EDIBridge**.
7. Merhaba Hello Çözüm Gezgini, genişletin **MessageFlowItinerary.bcs** hello çift tıklayın ve **EDIBridge.config** dosya. Merhaba Hello içeriğinin yerine geçecek **EDIBridge.config** hello aşağıdaki ile.
   
   > [!NOTE]
   > Tooedit hello .config dosyası neden gerekiyor mu? Merhaba dış hizmet uç noktası toohello köprüsü Tasarımcı tuvaline eklediğimiz daha önce dağıtılan hello EDI köprüleri temsil eder. EDI köprüleri gönderme ile iki yönlü köprüleri olan ve alma tarafı. Ancak, hello toohello köprüsü Tasarımcısı eklediğimiz EAI köprü tek yönlü bir köprü olur. Bu nedenle, toohandle hello farklı ileti exchange desenlerini hello iki köprüleri, özel köprüsü davranışı hello .config dosyasına yapılandırmasına dahil olmak üzere kullanırız. Ayrıca, hello özel davranış hello kimlik doğrulama toohello EDI gönderme köprüsü endpoint işler. Bu özel davranış ayrı bir örnek olarak kullanılabilir [BizTalk Services örnek - EAI tooEDI zincirleme köprüsü](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Bu çözüm hello örnek yeniden kullanır.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Merhaba EDIBridge.config dosya tooinclude yapılandırma ayrıntılarını güncelleştir
   
   * Altında  *<behaviors>* hello ACS ad alanı sağlar ve anahtar BizTalk Services abonelik hello ile ilişkili.
   * Altında  *<client>* , EDI Gönderme Sözleşmesi hello dağıtıldığı hello uç noktası sağlar.
   
   Değişiklikleri kaydetmek ve hello yapılandırma dosyasını kapatın.
9. Merhaba Hello ifadesini araç tıklatın **bağlayıcı** ve birleştirme hello **ProcessInvoiceBridge** ve **EDIBridge** bileşenleri. Merhaba bağlayıcıyı seçin ve Özellikler kutusunda ayarlanan **filtre koşulu** çok**eşleşen tüm**. Bu EAI köprü hello tarafından işlenen tüm iletileri yönlendirilir sağlar toohello EDI köprüsü.
   
   ![][10]  
10. Değişiklikleri toohello çözüm kaydedin.  

### <a name="deploy-hello-project"></a>Merhaba projesini dağıtma
1. Merhaba BizTalk Services projesi oluşturulduğu hello bilgisayarda indirin ve BizTalk Services aboneliğinize hello SSL sertifikası yükleyin. BizTalk Services'ın altında tıklatın **Pano**ve ardından **SSL sertifikası indir**. Merhaba sertifikayı çift tıklatın ve hello komut istemi toocomplete hello yükleme izleyin. Altına hello sertifikayı yüklediğinizden emin olun **güvenilen kök sertifika yetkilileri** sertifika deposu.
2. Visual Studio Çözüm Gezgini'nde hello sağ **InvoiceProcessingBridge** proje ve ardından **dağıtma**.
3. Merhaba görüntüde gösterildiği gibi Hello değerler sağlayın ve ardından **dağıtma**. Tıklayarak için BizTalk Services hello ACS kimlik bilgilerini alabilirsiniz **bağlantı bilgilerini** hello BizTalk Services panosundan.
   
   ![][11]  
   
   Merhaba çıkış bölmesinden hello EAI köprü dağıtıldığı, örneğin, hello uç noktasını kopyalayın `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. Bu uç nokta URL'si daha sonra ihtiyacınız olacak.  

## <a name="step-4-test-hello-solution"></a>4. adım: Test hello çözümü
Bu konuda, nasıl tootest hello çözüm hello kullanarak ele **öğretici istemci** hello örnek bir parçası olarak sağlanan uygulama.  

1. Visual Studio'da F5 toostart hello basın **öğretici istemci**.
2. Merhaba ekranında hello Service Bus kuyruklarını burada oluşturduğumuz hello adımından önceden doldurulmaz hello değerlere sahip olmalıdır. **İleri**’ye tıklayın.
3. Merhaba sonraki penceresinde BizTalk Services abonelik için ACS kimlik bilgilerini sağlayın ve hello uç noktalar burada EAI ve EDI (Al) köprüleri dağıtılır.
   
   Merhaba EAI köprü endpoint hello önceki adımda kopyaladığınız. Merhaba BizTalk Services portalı köprüsü endpoint EDI almak için toohello sözleşmesi Git > alma ayarı > aktarım > uç nokta.
   
   ![][12]  
4. Merhaba sonraki Contoso altında hello penceresinde **şirket içi faturayı gönderin** düğmesi. Merhaba Dosya Aç iletişim kutusu, hello INHOUSEINVOICE.txt dosyasını açın. Merhaba dosyanın Merhaba içeriğine inceleyin ve ardından **Tamam** toosend hello fatura.
   
   ![][13]  
5. Birkaç saniye hello fatura Northwind alınır. Merhaba tıklatın **iletiyi görüntüle** Northwind tarafından alınan bağlantı toosee hello fatura. Nasıl hello bir Contoso tarafından gönderilen sırasında standart EDIFACT şemadaki Northwind tarafından alınan hello fatura olduğuna dikkat edin, bir şirket içi şema oluştu.
   
   ![][14]  
6. Merhaba Fatura'yı seçin ve ardından **gönderin alındısı**. Açılır hello iletişim kutusunda, o hello değişim kimliği gönderilen hello alınan fatura ve hello bildirim içinde aynı dikkat edin. Hello Tamam'ı tıklatın **gönderin alındısı** iletişim kutusu.
   
   ![][15]  
7. Birkaç saniye içinde hello bildirim başarıyla Contoso alındı.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>(İsteğe bağlı) 5. adım: gönderme EDIFACT fatura gruplar halinde
BizTalk Services EDI köprüleri de destekler giden iletiler toplu işleme. Bu özellik, tooreceive toplu iletiler (belirli ölçütlerine uyan) tek bir ileti yerine tercih ortakları almak için kullanışlıdır.

toplu işlemler ile çalışırken en önemli boy hello hello gerçek hello sürüm ölçütlerini olarak da bilinir hello toplu sürümüdür. Merhaba sürüm ölçütlerini hello alıcı ortağın tooreceive iletileri nasıl istediği bağlı olabilir. Toplu işleme etkinleştirilirse hello EDI köprüsü hello sürüm ölçütlerini verildikten kadar iş ortağı alma hello giden ileti toohello göndermez. Örneğin, bir toplu işleme ölçütlerini toplu ileti boyutu gönderileri üzerinde temel yalnızca 'n' iletileri toplu. Sağlayacak şekilde her gün sabit bir saatte bir toplu gönderilen bir toplu iş ölçütlerini de zamana dayalı olabilir. Bu çözümde hello ileti boyutu tabanlı ölçütleri deneyin.

1. Hello BizTalk Services Portalı'da, daha önce oluşturduğunuz hello Sözleşmesi'ı tıklatın. Gönderme Ayarları > Toplu işleme > Toplu ekleyin.
2. Batch, adı **InvoiceBatch**, bir açıklama girin ve ardından **sonraki**.
3. Hangi iletilerin toplu tanımlayan bir toplu ölçütü belirtin. Bu çözümde, tüm iletileri toplu. Bu nedenle, hello tanımları seçeneği Gelişmiş kullanım seçip girin **1 = 1**. Bu her zaman true olacak bir durumdur ve bu nedenle tüm iletileri toplu. **İleri**’ye tıklayın.
   
   ![][17]  
4. Toplu sürüm ölçütlerini belirtin. Merhaba açılan-kutusundan seçin **MessageCountBased**ve **sayısı**, belirtin **3**. Bu, toplu üç iletiler tooNorthwind gönderilecek anlamına gelir. **İleri**’ye tıklayın.
   
   ![][18]  
5. Merhaba özeti gözden geçirin ve ardından **kaydetmek**. Tıklatın **dağıtma** tooredeploy hello anlaşma.
6. Toohello dönün **öğretici istemci**, tıklatın **şirket içi faturayı gönderin**ve hello istemleri toosend hello fatura izleyin. Merhaba toplu iş boyutu karşılanmadı çünkü hiçbir fatura Northwind aldığınızı fark edeceksiniz. Böylece tooNorthwind gönderilen üç fatura iletileri sahip iki kez daha, bu adımı yineleyin. Bu, toplu sürüm ölçütlerini 3 iletilerinin hello ve northwind'de faturayı görmelisiniz karşılar.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

