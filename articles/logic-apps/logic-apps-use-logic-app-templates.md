---
title: "Şablonları - Azure Logic Apps aaaCreate akışlarından | Microsoft Docs"
description: "Kullanmaya başlama - Azure mantıksal uygulama şablonları tooconnect uygulamaları kullanarak hızlı bir şekilde iş akışları oluşturmak ve veri tümleştirebilirsiniz."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>Önceden derlenmiş şablon veya hızlı şekilde kullanmaya düzeni tooget kullanarak bir iş akışı yapılandırma

## <a name="what-are-logic-app-templates"></a>Mantıksal uygulama şablonları nelerdir
Bir mantıksal uygulama tooquickly kullanabileceğiniz önceden oluşturulmuş mantıksal uygulama kendi iş akışı oluşturma Başlarken şablonudur. 

Bu şablonlar logic apps kullanarak yerleşik çeşitli desenleri en iyi yolu toodiscover alır. Bu şablon olarak da kullanabilirsiniz-toofit değiştirin ya da senaryonuz.

## <a name="overview-of-available-templates"></a>Kullanılabilir şablonlarına genel bakış
Şu anda hello mantığı uygulama platformu yayımlanan birçok kullanılabilir şablonlar vardır. Bazı örnek kategorileri yanı sıra bunların içinde kullanılan bağlayıcılar hello türü aşağıda listelenmiştir.

### <a name="enterprise-cloud-templates"></a>Kurumsal bulut şablonlar
Dynamics CRM, Salesforce, kutusu, Azure Blob ve kurumsal bulut gereksinimleriniz için diğer bağlayıcıları tümleştirmek şablonları. Bazı örnekler ne bunlarla yapılabilir şablonları, müşteri adayları düzenleme ve kurumsal dosya verilerinizi yedeklemeye içerir.

### <a name="enterprise-integration-pack-templates"></a>Kurumsal tümleştirme paketi şablonları
VETER yapılandırmalarını (doğrulamak, ayıklama, dönüştürme, zenginleştirmek ve rota) ardışık EDI belge AS2 üzerinde ve tooXML, dönüştürme olarak yanı sıra X12 ve AS2 iletisi olarak işleme bir X12 alma.

### <a name="protocol-pattern-templates"></a>Protokol düzeni şablonları
İstek-yanıt gibi Protokolü düzenleri tümleştirmeler yanı sıra HTTP FTP ve SFTP arasında içeren mantıksal uygulamalar, bu şablonları oluşur. Bunlar oldukları gibi veya temel olarak daha karmaşık Protokolü desenleri oluşturmak için kullanın.  

### <a name="personal-productivity-templates"></a>Kişisel üretkenlik şablonları
Desenler toohelp kişisel üretkenliği artırmak günlük anımsatıcı ayarı, yapılacaklar listelerinde önemli iş öğelerini açın ve tooa tek kullanıcı onayı adım uzun görevleri otomatikleştirmek şablonları içerir.

### <a name="consumer-cloud-templates"></a>Tüketici bulut şablonları
Twitter, boşluk ve e-posta, sosyal medya girişimleri pazarlama güçlendirme sonuçta özellikli gibi sosyal medya Hizmetleri ile tümleştirme basit şablonları. Bu da üretkenliklerini geleneksel yinelenen görevler üzerinde harcanan süre kaydederek yardımcı olabilecek cloudy kopyalama gibi şablonları içerir. 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>Nasıl toocreate bir şablonu kullanarak bir mantıksal uygulama
bir mantıksal uygulama şablonu kullanmaya tooget hello mantığı Uygulama Tasarımcısı'na gidin. Varolan bir mantıksal uygulama açarak hello Tasarımcısı girdiğinizden yoksa, hello mantıksal Uygulama Tasarımcısı görünümünüzde otomatik olarak yükler. Ancak, yeni bir mantıksal uygulama oluşturuyorsanız, aşağıdaki hello ekrana bakın.  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

Bu ekranda toostart boş mantıksal uygulama ya da önceden derlenmiş şablon ile ya da seçebilirsiniz. Merhaba şablonlarından birini seçerseniz, ek bilgiler sağlanır. Bu örnekte, kullandığımız hello *yeni bir dosya Dropbox'oluşturulduğunda, tooOneDrive kopyalama* şablonu.  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

Merhaba toouse hello şablonu seçerseniz, yalnızca seçin *bu şablonu kullanmak* düğmesi. Hangi bağlayıcılar hello şablonu kullanan temel tooyour hesaplarındaki toosign istenir. Ya da daha önce bu bağlayıcıların bağlantıyla belirlediğinize göre seçebileceğiniz aşağıda görüldüğü gibi devam eder.  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

Merhaba bağlantı kurma ve seçtikten sonra *devam*, hello mantıksal Uygulama Tasarımcısı görünümünde açılır.  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

Birçok şablonlarıyla Hello olduğu gibi hello yukarıdaki örnekte, bazı hello zorunlu özellik alanlarını hello bağlayıcılar içinde doldurulması; Ancak, bazı hala bir değer bölümlemeye önce gerektirebilir tooproperly hello mantıksal uygulama dağıtın. Bazı alanlar eksik hello girmeden toodeploy çalışırsanız, bir hata iletisi ile bildirilir.

Merhaba tooreturn toohello şablonu Görüntüleyicisi istiyorsanız seçin *şablonları* hello üst gezinti çubuğu düğmesini. Geri toohello şablonu Görüntüleyicisi geçerek, kaydedilmemiş ilerleme kaybedersiniz. Önceki tooswitching şablonu Görüntüleyicisi uygulamasına geri bu bildiren bir uyarı iletisi görürsünüz.  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>Nasıl bir mantıksal uygulama toodeploy şablondan oluşturulan
Şablonunuzu yüklü ve istediğiniz değişiklikleri yapılan sonra Kaydet düğmesine hello hello sol üst köşedeki seçin. Bu kaydeder ve mantıksal uygulamanızı yayımlar.  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

İster nasıl tooadd var olan bir mantıksal uygulama şablonu daha adımları hakkında daha fazla bilgi veya genel düzenlemeler, hakkında daha fazla okuma [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

