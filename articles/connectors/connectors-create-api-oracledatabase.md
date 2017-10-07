---
title: "aaaAdd hello Oracle Veritabanı Bağlayıcısı Azure Logic Apps içinde | Microsoft Docs"
description: "Bir mantıksal uygulama Hello Oracle Veritabanı Bağlayıcısı kullanma"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Merhaba Oracle Veritabanı Bağlayıcısı ile çalışmaya başlama

Merhaba Oracle Veritabanı Bağlayıcısı'nı kullanarak, varolan bir veritabanında veri kullanan kurumsal iş akışları oluşturun. Bu bağlayıcı, şirket içi Oracle veritabanına veya Oracle veritabanı içeren bir Azure sanal makinesi yüklü tooan bağlanabilir. Bu bağlayıcı ile şunları yapabilirsiniz:

* Yeni bir müşteri tooa müşteriler veritabanı ekleyerek veya bir sırada siparişler veritabanını güncelleştirmek, iş akışı oluşturma.
* Eylemler tooget bir veri satırı kullanın, yeni bir satır ekleyin ve hatta silin. Örneğin, bir kayıt Dynamics CRM Online içinde (tetikleyici) oluşturulduğunda, bir satır bir Oracle veritabanına (bir eylem) ekleyin. 

Bu konu nasıl toouse hello Oracle Veritabanı Bağlayıcısı bir mantıksal uygulama içinde gösterir.

## <a name="prerequisites"></a>Ön koşullar

* Desteklenen Oracle sürümleri: 
    * Oracle 9 ve sonraki sürümler
    * Oracle istemci yazılımı 8.1.7 ve sonraki sürümler

* Merhaba şirket içi veri ağ geçidi yükleyin. [Tooon içi veri mantığı uygulamalardan bağlanmak](../logic-apps/logic-apps-gateway-connection.md) hello adımları listeler. Merhaba, gerekli tooconnect tooan şirket içi Oracle veritabanına veya Oracle DB yüklü olan bir Azure VM geçididir. 

    > [!NOTE]
    > Merhaba şirket içi veri ağ geçidi köprü olarak davranır ve şirket içi verileri (Merhaba bulutta olmayan) ve logic apps arasında güvenli veri aktarımını sağlar. Merhaba, aynı ağ geçidi birden çok hizmet ve birden çok veri kaynağı ile kullanılabilir. Bu nedenle, yalnızca tooinstall hello ağ geçidi kez gerekebilir.

* Merhaba Oracle istemcisi hello şirket içi veri ağ geçidinin yüklü olduğu hello makineye yükleyin. Tooinstall Oracle .NET için 64-bit Oracle veri sağlayıcısı hello emin olun:  

  [Windows x64 için 64-bit ODAC 12c sürüm 4 (12.1.0.2.4)](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Merhaba Oracle istemcisi yüklü değilse, toocreate deneyin veya hello bağlantı kullandığınızda bir hata oluşur. Bu konuda Hello yaygın hatalar görebilirsiniz.


## <a name="add-hello-connector"></a>Merhaba bağlayıcısını ekleyin

> [!IMPORTANT]
> Bu bağlayıcı hiçbir tetikleyici yok. Yalnızca eylem yok. Mantıksal uygulamanızı oluşturduğunuzda, bu nedenle başka bir tetikleyici toostart mantıksal uygulamanızı gibi ekleyin **çizelgesi - yinelenme**, veya **istek / yanıt - yanıt**. 

1. Merhaba, [Azure portal](https://portal.azure.com), boş mantıksal uygulama oluşturma.

2. Mantıksal uygulamanızı Hello başlangıcında hello seçin **istek / yanıt - istek** tetikleyici: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. **Kaydet**’i seçin. Kaydettiğinizde, bir istek URL'sini otomatik olarak oluşturulur. 

4. Seçin **yeni adım**seçip **Eylem Ekle**. Yazın `oracle` toosee hello kullanılabilir eylemler: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Bu aynı zamanda hello hızlı şekilde toosee olup hello tetikleyiciler ve Eylemler herhangi bir bağlayıcı için kullanılabilir. Merhaba bağlayıcı adı, bir parçası yazın `oracle`. Merhaba Tasarımcısı hiçbir tetikleyici ve eylemleri listeler. 

5. Merhaba eylemlerden birini gibi seçin **Oracle veritabanı - Get satır**. Seçin **Connect şirket içi veri ağ geçidi üzerinden**. Merhaba Oracle sunucu adını, kimlik doğrulama yöntemi, kullanıcı adı, parola ve select hello ağ geçidi girin:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Bağlantı kurulduktan sonra hello listesinden bir tablo seçin ve hello satır kimliği tooyour tablo girin. Tooknow hello tanımlayıcı toohello tablo gerekir. Bilmiyorsanız, Oracle DB yöneticinize başvurun ve hello çıktısını almak `select * from yourTableName`. Tooproceed gereksinim olarak tanımlanabilir bilgileri hello kazandırır.

    Aşağıdaki örnek hello, İnsan Kaynakları veritabanından iş veri döndürülmüyor: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. Bu sonraki adımda hello herhangi diğer bağlayıcıları toobuild kullanabilirsiniz, iş akışı. Oracle tootest alma verileri istediğiniz sonra hello Oracle veri hello birini kullanarak kendiniz bir e-posta Gönder, e-posta bağlayıcıları, böyle bir Office 365 veya Gmail gönderin. Merhaba dinamik hello Oracle tablo toobuild hello belirteçlerinden kullanmak `Subject` ve `Body` e-postanızın:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Kaydet** mantıksal uygulama ve ardından **çalıştırmak**. Merhaba Tasarımcısını Kapat ve hello durumu için hello çalıştırır geçmişini bakın. Başarısız olursa hello başarısız ileti satırını seçin. Merhaba Tasarımcısı açılır ve hangi adım başarısız gösterir ve ayrıca gösterir hata bilgilerini hello. Başarılı olursa, eklediğiniz hello bilgi içeren bir e-posta almanız gerekir.


### <a name="workflow-ideas"></a>İş akışı fikirleri

* Toomonitor hello #oracle diyez istediğiniz ve bunlar sorgulanan ve diğer uygulamalar içinde kullanılan şekilde hello tweet'leri bir veritabanında yerleştirin. Bir mantıksal uygulama hello eklemek `Twitter - When a new tweet is posted` tetikleyebilir ve hello girin **#oracle** diyez. Ardından, hello ekleyin `Oracle Database - Insert row` eylemi ve tablonuzu seçin:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* İletileri tooa Service Bus kuyruğuna gönderilir. Bu iletiler tooget istediğiniz ve onları bir veritabanında yerleştirin. Bir mantıksal uygulama hello eklemek `Service Bus - when a message is received in a queue` tetikleyici ve select hello sırası. Ardından, hello ekleyin `Oracle Database - Insert row` eylemi ve tablonuzu seçin:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Sık karşılaşılan hataları

#### <a name="error-cannot-reach-hello-gateway"></a>**Hata**: hello ağ geçidi ulaşamıyor

**Neden**: hello şirket içi veri ağ geçidi mümkün tooconnect toohello bulut değil. 

**Azaltma**: ağ geçidiniz burada yükler ve onun toohello bağlanabilir hello şirket içi makinede çalıştığından emin olun Internet.  Merhaba ağ geçidi, bir bilgisayar kapalı olabilir veya uyku yüklenmiyor öneririz. Merhaba şirket içi veri Ağ Geçidi Hizmeti (PBIEgwService) de yeniden başlatabilirsiniz.

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Hata**: kullanılmakta olan hello sağlayıcısının kullanım dışıdır: ' System.Data.OracleClient gerektirir Oracle istemci yazılımı 8.1.7 veya daha büyük.'. Lütfen şu adresi ziyaret [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello resmi sağlayıcısı.

**Neden**: hello Oracle istemci SDK'sı yüklü değil hello makinede hello burada şirket içi veri ağ geçidi çalışıyor.  

**Çözümleme**: hello Oracle istemci SDK'sı üzerinde hello yükleyip hello şirket içi veri ağ geçidi ile aynı bilgisayara.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Hata**: '[Tablename]' tablosu tüm anahtar sütunlarını tanımlamak değil

**Neden**: hello tablo hiçbir birincil anahtar yok.  

**Çözümleme**: hello Oracle veritabanı connector, birincil anahtar sütunu içeren bir tablo kullanılmasını gerektirir.

#### <a name="currently-not-supported"></a>Şu anda desteklenmiyor

* Görünümleri ve saklı yordamlar 
* Bileşik anahtarlar ile herhangi bir tabloyu
* İç içe nesne türlerinin tablolardaki
 
## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/oracle/). 

## <a name="get-some-help"></a>Bazı Yardım alın

Merhaba [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) mükemmel tooask sorular yerleştirin, soruları ve diğer Logic Apps kullanıcıların ne yaptıklarını bakın. 

Logic Apps ve bağlayıcıları oylama ve fikirlerinizi adresindeki gönderme tarafından artırmaya yardımcı olabilir [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md)ve hello kullanılabilir bağlayıcılar Logic Apps içinde keşfetme bizim [API'leri listesi](apis-list.md).
