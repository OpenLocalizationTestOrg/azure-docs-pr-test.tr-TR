---
title: "Azure mantıksal uygulamaları şirket içi dosya sistemlerine bağlanmak | Microsoft Docs"
description: "Şirket içi dosya sistemleri için mantığı uygulama akışınızı şirket içi veri ağ geçidi ve dosya sistemi bağlayıcısı aracılığıyla bağlayın"
keywords: Dosya sistemleri
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a>Logic apps dosya sistemi bağlayıcı ile şirket içi dosya sistemleri bağlayın

Karma bulut bağlantı mantıksal uygulamalar için merkezi olduğundan verileri yönetmek ve güvenli bir şekilde şirket içi kaynaklara erişmek için mantıksal uygulamalarınızı şirket içi veri ağ geçidi kullanabilirsiniz. Bu makalede, temel senaryo ile şirket içi dosya sistemine bağlanmak nasıl gösteriyoruz: Dropbox'a dosya paylaşımına yüklendikten sonra bir e-posta Gönder dosyasını kopyalayın.

## <a name="prerequisites"></a>Ön koşullar

- Yükleme ve yapılandırma en son [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127).
- En son şirket içi veri ağ geçidini, sürüm 1.15.6150.1 yükleyin veya üstü. [Şirket içi veri ağ geçidine bağlanmak](http://aka.ms/logicapps-gateway) adımlar listelenmektedir. Ağ geçidi adımları geri kalanı ile devam etmeden önce bir şirket içi makineye yüklenmesi gerekir.

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a>Tetikleyici ve dosya sistemine bağlanmak için Eylemler ekleme

1. Bir mantıksal uygulama oluşturun ve bu Dropbox tetikleyici ekleyin: **bir dosya oluşturulduğunda** 
2. Tetikleyici altında seçin **sonraki adım** > **Eylem Ekle**. 
3. Arama kutusuna `file system` dosya sistemi Bağlayıcısı için desteklenen tüm eylemler görmesine olanak tanır.

   ![Dosya bağlayıcı arayın](media/logic-apps-using-file-connector/search-file-connector.png)

2. Seçin **dosyası oluştur** eylemi ve dosya sisteminizi bağlantı oluşturun.

   Varolan bir bağlantıyı sahip değilseniz, birini oluşturmanız istenir.

   1. Seçin **Connect şirket içi veri ağ geçidi üzerinden**. Daha fazla özellik görünür.
   2. Dosya sistemi için kök klasör seçin.
      
       > [!NOTE]
       > Tüm dosya ile ilgili eylemler için göreli yollar için kullanılan ana üst klasörü kök klasörüdür. Bir yerel klasör, şirket içi veri ağ geçidi yüklendi veya klasörü makinenin erişebildiği bir ağ paylaşımı olabilir makinede belirtebilirsiniz.

   3. Ağ geçidi için kullanıcı adı ve parola girin.
   4. Daha önce yüklediğiniz ağ geçidi seçin.

       ![Bağlantıyı yapılandırın](media/logic-apps-using-file-connector/create-file.png)

3. Tüm Ayrıntılar verdikten sonra Seç **oluşturma**. 

   Logic Apps yapılandırır ve bağlantı düzgün çalıştığından emin olmayı bağlantınızı test eder. 
   Bağlantısı düzgün şekilde ayarlanıp ayarlanmadığını seçenekler, daha önce seçtiğiniz eylem için bkz. 
   Dosya sistemi Bağlayıcısı'nı şimdi kullanıma hazırdır.

4. Şirket içi dosya paylaşımı için kök klasör Dropbox'tan dosyalarını kopyalamak istediğiniz belirtin.

   ![Dosya eylem oluşturun](media/logic-apps-using-file-connector/create-file-filled.png)

5. Mantıksal uygulamanızı dosyaları kopyaladıktan sonra ilgili kullanıcılar yeni dosya hakkında bilmesi bir e-posta gönderen bir Outlook eylem ekleyin. Alıcılar, başlık ve e-posta gövdesini girin. 

   Dinamik içerik Seçici içinde daha fazla ayrıntı için e-posta ekleyebilmek dosya Bağlayıcısı'ndan veri çıkışları seçebilirsiniz.

   ![E-posta eylemi Gönder](media/logic-apps-using-file-connector/send-email.png)

6. Mantıksal uygulamanızı kaydedin. Dropbox için bir dosyayı karşıya yükleyerek uygulamanızı test edin. Dosya şirket içi dosya paylaşımına kopyalanmış ve işlemi hakkında bir e-posta almanız gerekir.

   > [!TIP] 
   > Bilgi edinmek için nasıl [mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Tebrikler, artık, şirket içi dosya sistemine bağlanmak bir çalışma mantıksal uygulama vardır. Bağlayıcı sunar, örneğin diğer işlevleri keşfetme deneyin:

- Dosya Oluştur
- Klasördeki dosyaları listele
- Dosya ekleme
- Dosya Sil
- Dosya içeriğini alma
- Dosya yolunu kullanarak dosya içeriğini al
- Dosya meta verileri alma
- Dosya yolunu kullanarak dosya meta verilerini al
- Kök klasördeki dosyaları listele
- Güncelleştirme dosyası

## <a name="view-the-swagger"></a>Swagger görüntüleyin
Bkz: [ayrıntıları swagger](/connectors/fileconnector/). 

## <a name="get-help"></a>Yardım alın

Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını öğrenmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.

Azure Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Azure Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.

## <a name="next-steps"></a>Sonraki adımlar

- [Şirket içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan
- Hakkında bilgi edinin [Kurumsal tümleştirme](../logic-apps/logic-apps-enterprise-integration-overview.md)
