---
title: "aaaConnect tooon içi dosya Azure Logic Apps sistemlerden | Microsoft Docs"
description: "Mantıksal uygulama akışınızı hello şirket içi veri ağ geçidi ve dosya sistemi bağlayıcısı aracılığıyla tooon içi dosya sistemleri bağlayın"
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
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Logic apps hello dosya sistemi bağlayıcı ile tooon içi dosya sistemleri bağlayın

Karma bulut bağlantı merkezi toologic uygulamaların, bunu toomanage verilerini ve güvenli bir şekilde erişim şirket içi kaynakları, mantıksal uygulamalarınızı hello şirket içi veri ağ geçidi kullanabilirsiniz. Bu makalede, nasıl tooconnect tooan dosya sistemi temel senaryo ile şirket içi gösteriyoruz: Bu karşıya yüklenen tooDropbox tooa dosya paylaşımı, sonra bir e-posta Gönder dosyasını kopyalayın.

## <a name="prerequisites"></a>Ön koşullar

- Merhaba son yükleyip [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127).
- Merhaba son şirket içi veri ağ geçidi, sürüm 1.15.6150.1 yüklemek veya üstü. [Toohello şirket içi veri ağ geçidi bağlantı](http://aka.ms/logicapps-gateway) hello adımları listeler. Merhaba adımları hello kalanı ile devam etmeden önce bir şirket içi makinede hello ağ geçidi yüklenmelidir.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Tetikleyici ve tooyour dosya sistemine bağlanmak için Eylemler ekleme

1. Bir mantıksal uygulama oluşturun ve bu Dropbox tetikleyici ekleyin: **bir dosya oluşturulduğunda** 
2. Merhaba tetikleyici altında seçin **sonraki adım** > **Eylem Ekle**. 
3. Merhaba arama kutusuna `file system` hello dosya sistemi Bağlayıcısı için desteklenen tüm eylemler görmesine olanak tanır.

   ![Dosya bağlayıcı arayın](media/logic-apps-using-file-connector/search-file-connector.png)

2. Merhaba seçin **dosyası oluştur** eylemi ve bir bağlantı tooyour dosya sistemi oluşturun.

   Varolan bir bağlantıyı yoksa, istendiğinde toocreate biri demektir.

   1. Seçin **Connect şirket içi veri ağ geçidi üzerinden**. Daha fazla özellik görünür.
   2. Dosya sistemi için kök klasör seçin.
      
       > [!NOTE]
       > Tüm dosya ile ilgili eylemler için göreli yollar için kullanılan hello ana üst klasör Hello kök klasörüdür. Burada hello şirket içi veri ağ geçidi yüklü değil veya hello klasör makine hello bir ağ paylaşımına erişmek için olabilir hello makinede yerel bir klasöre belirtebilirsiniz.

   3. Merhaba ağ geçidi için Hello kullanıcı adı ve parola girin.
   4. Daha önce yüklediğiniz hello ağ geçidi seçin.

       ![Bağlantıyı yapılandırın](media/logic-apps-using-file-connector/create-file.png)

3. Tüm hello ayrıntıları verdikten sonra Seç **oluşturma**. 

   Logic Apps yapılandırır ve hello bağlantı düzgün çalıştığından emin olmayı bağlantınızı test eder. 
   Merhaba bağlantı düzgün şekilde ayarlanıp ayarlanmadığını seçenekler, daha önce seçtiğiniz hello eylemi için bkz. 
   Merhaba dosya sistemi bağlayıcı artık kullanıma hazırdır.

4. Şirket içi dosya paylaşımı için Dropbox toohello kök klasörü toocopy dosyalarından istediğinizi belirtin.

   ![Dosya eylem oluşturun](media/logic-apps-using-file-connector/create-file-filled.png)

5. Mantıksal uygulama kopyaları hello dosyanıza sonra ilgili kullanıcıların hello yeni dosya hakkında bilmesi bir e-posta gönderen bir Outlook eylem ekleyin. Merhaba alıcılar, başlık ve hello e-posta gövdesini girin. 

   Merhaba dinamik içerik Seçici'de, daha fazla ayrıntı toohello e-posta ekleyebilmek hello dosya Bağlayıcısı'ndan veri çıkışları seçebilirsiniz.

   ![E-posta eylemi Gönder](media/logic-apps-using-file-connector/send-email.png)

6. Mantıksal uygulamanızı kaydedin. Bir dosya tooDropbox karşıya yükleyerek uygulamanızı test edin. Merhaba dosya kopyalanan toohello şirket içi dosya paylaşımı almanız gerekir ve hello işlemi hakkında bir e-posta almanız gerekir.

   > [!TIP] 
   > Nasıl çok öğrenin[mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Tebrikler, artık tooyour şirket içi dosya sistemi bağlanabilmesi için bir çalışma mantıksal uygulama vardır. Bağlayıcı sunar, örneğin hello diğer işlevleri keşfetme deneyin:

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

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/fileconnector/). 

## <a name="get-help"></a>Yardım alın

tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Sonraki adımlar

- [Tooon içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan
- Hakkında bilgi edinin [Kurumsal tümleştirme](../logic-apps/logic-apps-enterprise-integration-overview.md)
