---
title: "dönüşümler - Azure Logic Apps ile aaaConvert XML veri | Microsoft Docs"
description: "Dönüşümler veya mapps hello Kurumsal tümleştirme SDK kullanarak logic apps biçimlerde arasında tooconvert XML verileri oluşturma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>XML dönüşümler ile Kurumsal tümleştirme
## <a name="overview"></a>Genel Bakış
Merhaba Kurumsal tümleştirme dönüştürme Bağlayıcısı verileri bir biçim tooanother biçimden diğerine dönüştürür. Örneğin, hello hello YearMonthDay biçiminde geçerli tarihi içeren gelen ileti olabilir. Merhaba MonthDayYear biçiminde bir dönüştürme tooreformat hello tarih toobe kullanabilirsiniz.

## <a name="what-does-a-transform-do"></a>Bir dönüştürme ne yapar?
Kaynak XML Şeması (giriş hello) ve hedef XML Şeması (Merhaba çıktı) olarak da bilinen bir eşleme olduğundan, bir dönüşüm oluşur. Toohelp yönetmek veya hello veri denetimi farklı yerleşik işlevler dahil dize işlemeleri, koşullu atamaları, aritmetik ifadeler, tarih saat biçimlendiricileri ve hatta döngü yapıları kullanabilirsiniz.

## <a name="how-toocreate-a-transform"></a>Nasıl toocreate bir dönüşüm?
Merhaba Visual Studio kullanarak bir dönüşüm/eşlemesi oluşturabilirsiniz [Kurumsal tümleştirme SDK](https://aka.ms/vsmapsandschemas). Tamamlanmış oluşturma ve hello dönüştürme sınama olduğunda tümleştirme hesabınızda hello dönüştürme karşıya yükleyin. 

## <a name="how-toouse-a-transform"></a>Nasıl toouse bir dönüştürme
Tümleştirme hesabınızda hello dönüştürme/map yükledikten sonra bir mantıksal uygulama toocreate kullanabilirsiniz. Merhaba mantıksal uygulama, dönüştürmeleri hello mantıksal uygulama tetiklenir (ve dönüştürülen toobe gereken Giriş bir içerik olduğunda) çalışır.

**Bir dönüştürme hello adımları toouse işte**:

### <a name="prerequisites"></a>Ön koşullar

* Bir tümleştirme hesabı oluşturun ve bir harita tooit ekleyin  

Merhaba önkoşulların yapılan verdiğiniz göre zaman toocreate olduğu mantıksal uygulamanızı:  

1. Mantıksal uygulama oluşturma ve [tooyour tümleştirme hesap bağlantı](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink bir tümleştirme hesap tooa mantıksal uygulama öğrenin") hello eşlemesi içerir.
2. Ekleme bir **isteği** tetikleyici tooyour mantıksal uygulama  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Ekle hello **dönüştürme XML** ilk seçerek eylemi **Eylem Ekle**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Merhaba sözcüğü girin *dönüştürme* hello arama kutusu toofilter tüm toouse istediğiniz eylemleri toohello bir hello  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Select hello **XML dönüştürme** eylem   
6. Merhaba XML eklemek **içerik** , dönüştüren. Merhaba HTTP isteği hello olarak aldığınız herhangi bir XML veri kullanabilirsiniz **içerik**. Bu örnekte, hello hello mantıksal uygulama tetiklenen hello HTTP istek gövdesi seçin.
7. Merhaba SELECT hello adını **harita** toouse tooperform hello dönüştürme istiyor. Merhaba eşlemesi zaten tümleştirme hesabınız olması gerekir. Bir önceki adımda, eşleme içeren mantıksal uygulama erişim tooyour tümleştirme hesabınız zaten verdi.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Çalışmanızı kaydedin  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

Bu noktada, map ayarlama tamamlandı. Gerçek dünya uygulamada bir LOB uygulaması SalesForce gibi toostore hello dönüştürülmüş verileri isteyebilirsiniz. TooSalesforce hello eylem toosend hello çıktısı olarak kolayca dönüştürebilirsiniz. 

Ayrıca, bir istek toohello HTTP uç noktası yaparak, dönüştürme artık test edebilirsiniz.  

## <a name="features-and-use-cases"></a>Özellikleri ve kullanım örnekleri
* Merhaba dönüştürme bir eşleminde oluşturulan bir ad ve adres bir belge tooanother kopyalama gibi basit olabilir. Veya daha karmaşık dönüşümleri hello Giden kutusu eşleme işlemleri kullanarak oluşturabilirsiniz.  
* Birden çok eşleme işlemleri veya İşlevler dizeler, tarih saat işlevleri vb. dahil olmak üzere kullanıma hazır.  
* Merhaba Şemalar arasında doğrudan veri kopyalama yapabilirsiniz. Merhaba SDK Eşleyici dahil hello bu dekiler hello hedef şemasında ile Merhaba kaynak şemadaki hello öğelerin bağlayan bir çizgi çizme olarak kadar basittir.  
* Bir harita oluştururken, tüm hello ilişkiler gösterilmektedir hello harita ve oluşturduğunuz bağlantıları grafik gösterimi görüntüleyin.
* Merhaba Test eşleme özelliğini tooadd bir örnek XML ileti kullanın. Bir basit tıklamayla oluşturulur ve oluşturulan hello çıktı görmeniz hello eşlemesi test edebilirsiniz.  
* Var olan eşlemeleri karşıya yükle  
* Merhaba XML biçimi için destek içerir.

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  
* [Eşlemeleri hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-maps.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")  

