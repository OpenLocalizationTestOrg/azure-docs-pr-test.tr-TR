---
title: "aaaAutomate Azure Application Insights Microsoft Flow işler."
description: "Microsoft Flow nasıl kullanabileceğinizi öğrenin tooquickly hello Application Insights Bağlayıcısı'nı kullanarak yinelenebilir işlemleri otomatikleştirme."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>İçin Microsoft Flow hello Bağlayıcısı ile Azure Application Insights süreçleri otomatik hale getirme

Kendiniz art arda hello hizmetinizi düzgün çalıştığından, telemetri verileri toocheck aynı sorguları çalıştırma bulurum? Görünümlü tooautomate eğilimleri ve daha fazla bilgi bulmak için bu sorgular ve ardından bunları geçici kendi iş akışları oluşturmak mı? Hello Azure Application Insights (Önizleme) için Microsoft Flow hello doğru aracı bu amaçlar için Bağlayıcıdır.

İle tümleştirme, tek satırlık bir kod yazmak zorunda kalmadan artık çok sayıda süreçlerini otomatikleştirebilirsiniz. Application Insights eylemini kullanarak bir akış oluşturduktan sonra hello akış uygulama Öngörüler Analytics sorgunuzu otomatik olarak çalıştırılır. 

Ek Eylemler ekleyebilirsiniz. Microsoft Flow Eylemler yüzlerce kullanılabilir hale getirir. Örneğin, Microsoft Flow tooautomatically Gönder bir e-posta bildirimi kullanın ya da Visual Studio Team Services içinde oluşturma. Merhaba biri birçok kullanabilirsiniz [şablonları](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) Microsoft Flow hello bağlayıcı için kullanılabilir. Bu şablonları bir akış oluşturma hello işlemi hızlandırmak. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Bir akış için Application Insights oluşturma

Bu öğreticide, nasıl bir web uygulaması için hello verilerdeki hello Analytics otomatik küme algoritması toogroup kullanan bir akış toocreate öznitelikleri öğreneceksiniz. Merhaba akış hello sonuçları e-posta ile tek bir örneği nasıl Microsoft Flow ve uygulama Öngörüler Analytics birlikte kullanabileceğiniz otomatik olarak gönderir. 

### <a name="step-1-create-a-flow"></a>1. adım: bir akışı oluşturma
1. Çok oturum[Microsoft Flow](http://flow.microsoft.com)ve ardından **My akar**.
2. Tıklatın **bir akışı boş iken oluşturmak**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>2. adım: akışınız için bir Tetikleyici oluşturma
1. Seçin **zamanlama**ve ardından **çizelgesi - yinelenme**.
2. Merhaba, **sıklığı** kutusunda **gün**ve hello **aralığı** kutusuna **1**.

    ![Microsoft Flow tetikleyici iletişim kutusu](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>3. adım: Application Insights Eylem Ekle
1. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.
2. Arama **Azure Application Insights**.
3. Tıklatın **Azure Application Insights – görselleştirmek Analytics sorgu Önizleme**.

    ![Analytics sorgu penceresi](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>4. adım: tooan Application Insights kaynağı bağlanma

toocomplete Bu adım, kaynak için bir uygulama kimliği ve bir API anahtarı gerekir. Bunları Azure portal hello hello Aşağıdaki diyagramda gösterildiği gibi alabilirsiniz:

![Hello Azure portalında uygulama kimliği](./media/app-insights-automate-with-flow/appid.png) 

- Merhaba uygulama kimliği ve API anahtarı ile birlikte bağlantınız için bir ad sağlayın.

    ![Microsoft Flow bağlantı penceresi](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>5. adım: hello Analytics sorgu ve grafik türünü belirtin
Bu örnek sorgu hello başarısız istekleri hello son gün içinde seçer ve bunları hello işleminin bir parçası oluşan özel durumları ile karşılık gelen. Analytics bunları hello operation_Id tanımlayıcısına göre hatalarla ilintilidir. Merhaba sorgu hello autocluster algoritması kullanılarak hello sonuçları sonra kesim. 

Kendi sorguları oluşturduğunuzda, tooyour akış eklemeden önce bunlar düzgün analizleri çalıştığını doğrulayın.

- Analytics sorgu aşağıdaki hello ekleyin ve ardından hello HTML tablo grafik türü seçin. 

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
    
    ![Analytics sorgu yapılandırma penceresi](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>6. adım: hello akış toosend e-posta yapılandırma

1. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.
2. Arama **Office 365 Outlook**.
3. Tıklatın **Office 365 Outlook – bir e-posta Gönder**.

    ![Office 365 Outlook seçim penceresi](./media/app-insights-automate-with-flow/flow2b.png)

4. Merhaba, **bir e-posta Gönder** penceresinde, aşağıdaki hello:

   a. Merhaba alıcı Hello e-posta adresini yazın.

   b. Merhaba e-posta için bir konu yazın.

   c. Hello herhangi bir yere tıklayın **gövde** kutusuna ve ardından hello sağdaki açan hello dinamik içerik menüsünden seçin **gövde**.

   d. Tıklatın **Gelişmiş Seçenekleri Göster**.

    ![Office 365 Outlook yapılandırma](./media/app-insights-automate-with-flow/flow5.png)

5. Merhaba dinamik içerik menüsünden aşağıdaki hello:

    a. Seçin **ek adı**.

    b. Seçin **ek içerik**.
    
    c. Merhaba, **HTML'dir** kutusunda **Evet**.

    ![Office 365 e-posta yapılandırma penceresi](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>7. adım: Kaydetmek ve akışınız test
- Merhaba, **Akış adı** kutusuna akışınız için bir ad ekleyin ve ardından **akışı oluşturmak**.

    ![Akış oluşturma penceresi](./media/app-insights-automate-with-flow/flow8.png)

Bu eylemin hello tetikleyici toorun için bekleyebilir veya hello akış hemen göre çalıştırabilirsiniz [isteğe bağlı çalışan hello tetikleyici](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Merhaba akışı çalıştığında, hello e-posta listesinde belirtilen hello alıcılar hello şuna benzeyen bir e-posta iletisi alırsınız:

![Örnek e-posta](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Sonraki adımlar

- Oluşturma hakkında daha fazla bilgi [analitik sorguları](app-insights-analytics-using.md).
- Daha fazla bilgi edinmek [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





