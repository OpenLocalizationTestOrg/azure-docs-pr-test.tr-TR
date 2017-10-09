---
title: "aaaAutomate Logic Apps kullanarak Azure Application Insights işler."
description: "Nasıl hızlı bir şekilde yinelenebilir işlemler hello Application Insights Bağlayıcısı tooyour mantıksal uygulama ekleyerek otomatikleştirebilirsiniz öğrenin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Logic Apps kullanarak Application Insights işlemlerini otomatik hale

Kendiniz hizmetinizi düzgün çalışıp çalışmadığını Merhaba, telemetri verileri toocheck aynı sorgu tekrar tekrar çalıştırmayı bulurum? Görünümlü tooautomate eğilimleri ve daha fazla bilgi bulmak için bu sorgular ve ardından bunları geçici kendi iş akışları oluşturmak mı? Logic Apps için Hello Azure Application Insights Bağlayıcısı (Önizleme) hello sağ bu amaçla aracıdır.

İle tümleştirme, tek satırlık bir kod yazmak zorunda kalmadan çeşitli işlemleri otomatik hale getirebilirsiniz. Mantıksal uygulama oluşturma hello Application Insights ile bağlayıcı tooquickly otomatikleştirmek herhangi bir Application Insights işlem. 

Ek Eylemler ekleyebilirsiniz. Azure App Service Logic Apps özelliğini Hello Eylemler yüzlerce kullanılabilir hale getirir. Örneğin, bir mantıksal uygulama kullanarak, yapabilir otomatik olarak bir e-posta bildirim göndermek veya bir hata Visual Studio Team Services içinde oluşturabilirsiniz. Merhaba birini kullanılabilir birçok kullanabilirsiniz [şablonları](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp mantıksal uygulamanızı oluşturma hello işlemini hızlandırabilir. 

## <a name="create-a-logic-app-for-application-insights"></a>Application Insights için bir mantıksal uygulama oluşturma

Bu öğreticide, nasıl toocreate hello Analytics autocluster algoritması toogroup kullanan bir mantıksal uygulama bir web uygulaması için hello veri öznitelikleri öğrenin. Merhaba akış hello sonuçları e-posta ile tek bir örneği nasıl uygulama Öngörüler analizi ve Logic Apps birlikte kullanabileceğiniz otomatik olarak gönderir. 

### <a name="step-1-create-a-logic-app"></a>1. adım: bir mantıksal uygulama oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba, **yeni** bölmesinde, **Web + mobil**ve ardından **mantıksal uygulama**.

    ![Yeni mantıksal uygulama penceresi](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>2. adım: mantıksal uygulamanız için bir Tetikleyici oluşturma
1. Merhaba, **mantığı Uygulama Tasarımcısı** penceresi altında **Başlat sahip ortak bir tetikleyici**seçin **yineleme**.

    ![Mantıksal Uygulama Tasarımcısı penceresi](./media/automate-with-logic-apps/logicapp2.png)

2. Merhaba, **sıklığı** kutusunda **gün** ve ardından hello **aralığı** kutusuna **1**.

    ![Mantıksal Uygulama Tasarımcısı "Recurrence" penceresi](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>3. adım: Application Insights Eylem Ekle
1. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.

2. Merhaba, **bir eylem seçin** arama kutusuna **Azure Application Insights**.

3. Altında **Eylemler**, tıklatın **Azure Application Insights – görselleştirmek Analytics sorgu Önizleme**.

    ![Mantıksal Uygulama Tasarımcısı penceresinin "bir eylem seçin"](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>4. adım: tooan Application Insights kaynağı bağlanma

toocomplete Bu adım, kaynak için bir uygulama kimliği ve bir API anahtarı gerekir. Bunları Azure portal hello hello Aşağıdaki diyagramda gösterildiği gibi alabilirsiniz:

![Hello Azure portalında uygulama kimliği](./media/automate-with-logic-apps/appid.png) 

Bağlantı, hello uygulama kimliği ve hello API anahtarı için bir ad sağlayın.

![Mantıksal Uygulama Tasarımcısı akış bağlantısı penceresi](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>5. adım: hello Analytics sorgu ve grafik türünü belirtin
Aşağıdaki örneğine hello hello sorgu hello başarısız istekleri hello son gün içinde seçer ve hello işleminin bir parçası oluşan özel durumları ile bunlara karşılık gelen. Analytics hello operation_Id tanımlayıcısına göre hello başarısız istekleri hatalarla ilintilidir. Merhaba sorgu hello autocluster algoritması kullanılarak hello sonuçları sonra kesim. 

Kendi sorguları oluşturduğunuzda, tooyour akış eklemeden önce bunlar düzgün analizleri çalıştığını doğrulayın.

1. Merhaba, **sorgu** kutusunda, Analytics sorgu aşağıdaki hello ekleyin: 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. Merhaba, **grafik türü** kutusunda **Html tablosu**.

    ![Analytics sorgu yapılandırma penceresi](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>6. adım: hello mantığı uygulama toosend e-postayı yapılandırın

1. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.

2. Merhaba arama kutusuna yazın **Office 365 Outlook**.

3. Tıklatın **Office 365 Outlook – bir e-posta Gönder**.

    ![Office 365 Outlook seçimi](./media/automate-with-logic-apps/flow2b.png)

4. Merhaba, **bir e-posta Gönder** penceresinde, aşağıdaki hello:

   a. Merhaba alıcı Hello e-posta adresini yazın.

   b. Merhaba e-posta için bir konu yazın.

   c. Hello herhangi bir yere tıklayın **gövde** kutusuna ve ardından hello sağdaki açan hello dinamik içerik menüsünden seçin **gövde**.

   d. Tıklatın **Gelişmiş Seçenekleri Göster**.

      ![Office 365 Outlook yapılandırma](./media/automate-with-logic-apps/flow5.png)

5. Merhaba dinamik içerik menüsünden aşağıdaki hello:

    a. Seçin **ek adı**.

    b. Seçin **ek içerik**.
    
    c. Merhaba, **HTML'dir** kutusunda **Evet**.

      ![Office 365 e-posta yapılandırma ekranında](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>7. adım: Kaydedin ve mantıksal uygulamanızı test etme
* Tıklatın **kaydetmek** toosave değişikliklerinizi.

Merhaba tetikleyici toorun hello mantıksal uygulama için bekleyebilir veya seçerek hello mantıksal uygulamayı hemen çalıştırabilirsiniz **çalıştırmak**.

![Logic app oluşturma ekran](./media/automate-with-logic-apps/step7.png)

Mantıksal uygulamanızı çalıştığında hello e-posta listesinde belirtilen hello alıcılar hello şuna benzeyen bir e-posta alırsınız:

![Mantıksal uygulama e-posta iletisi](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Sonraki adımlar

- Oluşturma hakkında daha fazla bilgi [analitik sorguları](app-insights-analytics-using.md).
- Daha fazla bilgi edinmek [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





