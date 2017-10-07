---
title: "aaaCreate bulut uygulamalarını & Bulut Hizmetleri - Azure mantıksal uygulamaları arasındaki ilk iş akışınızın | Microsoft Docs"
description: "Azure Logic Apps’te iş akışları oluşturup çalıştırarak, sistem tümleştirmeden kuruluş uygulaması tümleştirmeye (EAI) kadar tüm senaryolar için iş süreçlerini otomatik hale getirin"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "iş akışı, bulut uygulamaları, bulut hizmetleri, iş süreçleri, sistem tümleştirme, kuruluş uygulaması tümleştirme, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>İş akışı tooautomate işlemleri bulut uygulamaları ve bulut hizmetleri arasında ilk mantıksal uygulamanızı oluşturma

[Azure Logic Apps](logic-apps-what-are-logic-apps.md) ile iş akışları oluşturup çalıştırdığınızda, herhangi bir kod yazmadan iş süreçlerini daha kolay ve hızlı bir şekilde otomatik hale getirebilirsiniz. Bu ilk örnek nasıl toocreate bir Web sitesinde yeni içerik için bir RSS denetler bir temel mantığı uygulama iş akışı gösterilmektedir. Yeni öğeler hello Web sitesinin akışta görüntülendiğinde, hello mantıksal uygulama bir Outlook veya Gmail hesaptan e-posta gönderir.

toocreate ve Çalıştır bir mantıksal uygulama, bu öğeler gerekir:

* Azure aboneliği. Bir aboneliğiniz yoksa [ücretsiz bir Azure hesabı ile başlayabilirsiniz](https://azure.microsoft.com/free/). Ya da [Kullandıkça Öde aboneliğine kaydolabilirsiniz](https://azure.microsoft.com/pricing/purchase-options/).

  Azure aboneliğiniz, mantıksal uygulama kullanımını faturalamak için kullanılır. [Kullanım ölçümü](../logic-apps/logic-apps-pricing.md) ve [fiyatlandırma](https://azure.microsoft.com/pricing/details/logic-apps) işlemlerinin Azure Logic Apps’te nasıl işlediğini öğrenin.

Ayrıca, bu örnek şu öğeleri gerektirir:

* Bir Outlook.com, Office 365 Outlook veya Gmail hesabı

    > [!TIP]
    > Kişisel bir [Microsoft hesabınız](https://account.microsoft.com/account) varsa Outlook.com hesabınız vardır. Aksi takdirde, bir Azure iş veya okul hesabınız varsa **Office 365 Outlook** hesabınız vardır.

* Bir bağlantı tooa Web sitesinin RSS akışı. Bu örnek hello kullanır [RSS hello CNN.com Web sitesinden için üst hikayeleri akışı](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>İş akışınızı başlatan bir tetikleyici ekleme

A [ *tetikleyici* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) , logic app iş akışınızı başlatır bir olaydır ve mantıksal uygulamanızı gerektiren hello ilk öğedir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").

2. Merhaba sol menüden seçin **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama** aşağıda gösterildiği gibi:

     ![Azure portalı, Yeni, Kurumsal Tümleştirme, Mantıksal Uygulama](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > Ayrıca seçebilirsiniz **yeni**, hello arama kutusuna yazın `logic app`, ve Enter tuşuna basın. Ardından **Mantıksal Uygulama** > **Oluştur**’u seçin.

3. Mantıksal uygulamanızı adlandırın ve Azure aboneliğinizi seçin. Şimdi, ilgili Azure kaynaklarını düzenleyip yönetmenize yardımcı olan bir Azure kaynak grubu oluşturun veya seçin. Son olarak, mantıksal uygulamanızı barındırmak için hello datacenter konumu seçin. Hazır olduğunuzda, seçin **PIN toodashboard** ve ardından **oluşturma**.

     ![Mantıksal uygulama ayrıntıları](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Seçtiğinizde, **PIN toodashboard**, mantıksal uygulamanızı Azure Pano hello üzerinde dağıtımdan sonra görünür ve otomatik olarak açılır. Mantıksal uygulamanızı hello Panoda hello görünmüyor varsa **tüm kaynakları** döşeme, seçin **daha görmek**, mantıksal uygulamanızı seçin. Veya hello sol menüsünde, **daha fazla hizmet**. **Kurumsal Tümleştirme** altında **Logic Apps**’ı belirleyip mantıksal uygulamanızı seçin.

4. Mantıksal uygulamanızı hello için ilk kez açtığınızda, hello mantığı Uygulama Tasarımcısı şablonları başlatılan tooget kullanacağınızı gösterir. Mantıksal uygulamanızı sıfırdan oluşturabilmek için şimdilik **Boş Mantıksal Uygulama**’yı seçin.

    Merhaba mantığı Uygulama Tasarımcısı açılır ve kullanılabilir hizmetler gösterir ve *Tetikleyicileri* , mantıksal uygulamanızı kullanabilirsiniz.

5. Merhaba arama kutusuna yazın `RSS`, bu Tetikleyici seçin: **bir akış öğesi yayımlandığında RSS -** 

    ![RSS tetikleyicisi](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Merhaba bağlantısı için hello Web sitesinin RSS akışı tootrack istediğiniz girin. 

     Ayrıca **Sıklık** ve **Aralık** değerlerini değiştirebilirsiniz. 
     Bu ayarlar mantıksal uygulamanızın yeni öğeleri ne sıklıkla denetleyeceğini belirler ve bu süre boyunca bulunan tüm öğeleri döndürür.

     Bu örnekte, şimdi popüler konular için her gün toohello CNN Web sitesine gönderilen denetleyin.

     ![Tetikleyicinin RSS akışı, sıklık ve aralık ayarını yapma](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Çalışmanızı şimdilik kaydedin. (Merhaba Tasarımcı komut çubuğunda seçin **kaydetmek**.)

   ![Mantıksal uygulamanızı kaydetme](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Kaydettiğiniz, mantıksal uygulamanızı Canlı gider, ancak şu anda, mantıksal uygulamanızı yalnızca yeni öğe denetler hello RSS akışı belirtildi. 
   Bu örnek, tetikleyici sonra mantıksal uygulamanızı gerçekleştiren eylem eklediğimiz daha kullanışlı toomake ateşlenir.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Tooyour tetikleyici yanıtlayan Eylem Ekle

[*Eylem*](./logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınız tarafından gerçekleştirilen bir görevdir. Bir tetikleyici tooyour mantıksal uygulama ekledikten sonra Bu tetikleyici tarafından oluşturulan verilerle bir eylem tooperform işlemleri ekleyebilirsiniz. Bizim örneğimizde, biz şimdi yeni öğeler görüntülendiğinde hello Web sitesinin RSS akışı e-posta gönderen bir eylem ekleyin.

1. Tetikleyici altında hello Tasarımcısı'nda seçin **yeni adım** > **Eylem Ekle** aşağıda gösterildiği gibi:

   ![Eylem ekleme](media/logic-apps-create-a-logic-app/add-new-action.png)

   Merhaba Tasarımcı gösterir [kullanılabilir Bağlayıcılar](../connectors/apis-list.md) , tetikleyici başlatıldığında bir eylem tooperform seçebilirsiniz.

2. E-posta hesabınıza bağlı olarak, Outlook veya Gmail hello adımları izleyin.

   * Merhaba arama kutusuna, Outlook hesabınızdan toosend e-posta girin `outlook`. **Hizmetler** altında kişisel Microsoft hesaplarınız için **Outlook.com** veya Azure iş ya da okul hesapları için **Office 365 Outlook**’u seçin. 
   **Eylemler** altında **E-posta gönder**’i seçin.

       ![Outlook "E-posta gönder" eylemini seçin](media/logic-apps-create-a-logic-app/actions.png)

   * Merhaba arama kutusuna, Gmail hesabınızdan toosend e-posta girin `gmail`. 
   **Eylemler** altında **E-posta gönder**’i seçin.

       !["Gmail - E-posta gönder" öğesini seçin](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Kimlik bilgileri istendiğinde, e-posta hesabınız için hello kullanıcı adı ve parolayla oturum. 

4. Merhaba hedef e-posta adresi gibi bu eylemin Hello ayrıntıları sağlayın ve hello veri tooinclude hello parametrelerini hello e-postada, örneğin seçin:

   ![E-posta ile veri tooinclude seçin](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Outlook’u seçerseniz mantıksal uygulamanız bu örnektekine benzer şekilde görünür:

    ![Tamamlanan mantıksal uygulama](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Yaptığınız değişiklikleri kaydedin. (Merhaba Tasarımcı komut çubuğunda seçin **kaydetmek**.)

6. Mantıksal uygulamanızı test için el ile çalıştırabilirsiniz. Merhaba Tasarımcı komut çubuğunda seçin **çalıştırmak**. Aksi takdirde, ayarladığınız hello zamanlamaya göre RSS akışı hello belirtilen denetleyin mantıksal uygulamanızı izin verebilirsiniz.

   Mantıksal uygulamanızı yeni öğeler bulursa, hello mantıksal uygulama, seçilen verileri içeren e-posta gönderir. 
   Yeni öğe bulunursa, mantıksal uygulamanızı e-posta gönderir hello eylem atlar.

7. toomonitor seçip mantıksal uygulamanızı çalıştıran ve tetikleyecek mantığı uygulama menünüzde geçmişi onay **genel bakış**.

   ![Mantıksal uygulamanın çalışma ve tetikleyici geçmişini izleme ve görüntüleme](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Merhaba komut çubuğunda, beklediğiniz hello veri bulamazsanız seçmeyi deneyin **yenileme**.

   toolearn mantığı uygulamanızın durumu hakkında daha fazla veya çalıştırın ve geçmiş veya toodiagnose mantıksal uygulamanızı tetiklemek, bkz: [mantıksal uygulamanızı sorun giderme](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > Mantıksal uygulamanız siz kapatana kadar çalışmaya devam eder. Uygulamanız için mantığı uygulama menünüzde şimdi kapatmak tooturn seçin **genel bakış**. Merhaba komut çubuğunda seçin **devre dışı**.

Tebrikler, ilk temel mantıksal uygulamanızı oluşturup çalıştırdınız. Ayrıca, herhangi bir kod kullanmadan, süreçleri otomatik hale getiren iş akışlarını ne kadar kolay oluşturabileceğinizi ve bulut uygulamaları ile bulut hizmetlerini tümleştirmeyi öğrendiniz.

## <a name="manage-your-logic-app"></a>Mantıksal uygulamanızı yönetme

toomanage, uygulamanızın hello durumunu denetlemek, düzenleme, görüntüleme geçmişi, kapatmak veya mantıksal uygulamanızı silme gibi görevleri gerçekleştirebilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").

2. Merhaba sol menüsünde, **daha fazla hizmet**. **Kurumsal Tümleştirme** altında **Logic Apps**’ı seçin. Mantıksal uygulamanızı seçin. 

   Merhaba mantığı uygulama menüsünde, bu mantığı uygulama yönetim görevlerini bulabilirsiniz:

   |Görev|Adımlar| 
   |:---|:---| 
   | Uygulamanızın durumunu, yürütme geçmişini ve genel bilgilerini görüntüleme| **Genel Bakış**’ı seçin.| 
   | Uygulamanızı düzenleme | **Mantıksal Uygulama Tasarımcısı**’nı seçin. | 
   | Uygulamanızın iş akışı JSON tanımını görüntüleme | **Mantıksal Uygulama Kod Görünümü**’nü seçin. | 
   | Mantıksal uygulamanız üzerinde gerçekleştirilen işlemleri görüntüleme | **Ekinlik günlüğü**’nü seçin. | 
   | Mantıksal uygulamanızın geçmiş sürümlerini görüntüleme | **Sürümler**’i seçin. | 
   | Uygulamanızı geçici olarak kapatma | Seçin **genel bakış**, hello komut çubuğunda seçin **devre dışı**. | 
   | Uygulamanızı silme | Seçin **genel bakış**, hello komut çubuğunda seçin **silmek**. Mantıksal uygulamanızın adını girip **Sil**’i seçin. | 

## <a name="get-help"></a>Yardım alın

tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Sonraki adımlar

*  [Koşul ekleme ve iş akışları çalıştırma](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Mantıksal uygulama şablonları](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Azure Resource Manager şablonlarından mantıksal uygulama oluşturma](../logic-apps/logic-apps-arm-provision.md)
