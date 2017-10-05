---
title: "Azure Logic Apps ile tümleşen bir işlev oluşturun | Microsoft Docs"
description: "Tweet düşünceleri kategorilere ayırmak ve düşünceleri düşük olduğunda bildirim göndermek için Azure Logic Apps ve Azure Bilişsel hizmetler ile tümleşen bir işlev oluşturun."
services: functions, logic-apps, cognitive-services
keywords: "iş akışı, bulut uygulamaları, bulut hizmetleri, iş süreçleri, sistem tümleştirme, kuruluş uygulaması tümleştirme, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Azure Logic Apps ile tümleşen bir işlev oluşturun

Azure işlevleri Logic Apps Tasarımcısı'nda Azure Logic Apps ile tümleşir. Bu tümleştirme işlevleri bilgi işlem gücü düzenlemelerin de diğer Azure ve üçüncü taraf hizmetleri ile kullanmanıza olanak sağlar. 

Bu öğretici işlevleri Logic Apps ile Azure Bilişsel hizmetler Twitter gönderileri gelen düşünceleri çözümlemek için nasıl kullanılacağını gösterir. Bir HTTP tetiklenen işlevi tweet'leri yeşil, sarı veya kırmızı düşünceleri puan dayalı olarak kategorilere ayırır. Zayıf düşünceleri algılandığında bir e-posta gönderilir. 

![ilk iki adım uygulamasının mantığı Uygulama Tasarımcısı'nda Görüntü](media/functions-twitter-email/designer1.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Bilişsel Hizmetler hesabı oluşturun.
> * Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.
> * Twitter hesabına bağlanan bir mantıksal uygulama oluşturun.
> * Düşünceleri algılama mantığı uygulamaya ekleyin. 
> * Mantıksal uygulama işlevine bağlayın.
> * İşlev yanıttan dayalı bir e-posta gönderin.

## <a name="prerequisites"></a>Ön koşullar

+ Etkin bir [Twitter](https://twitter.com/) hesabı. 
+ Bir [Outlook.com](https://outlook.com/) hesap (bildirim göndermek için).
+ Bu konu başlığında, başlangıç noktası olarak [Azure portalında ilk işlevinizi oluşturma](functions-create-first-azure-function.md) bölümünde oluşturulan kaynaklar kullanılmaktadır.  
Zaten yapmadıysanız, işlev uygulaması oluşturmak için şimdi aşağıdaki adımları tamamlayın.

## <a name="create-a-cognitive-services-account"></a>Bilişsel Hizmetler hesabı oluşturma

Bilişsel Hizmetler hesabı izlenmekte olan tweet'leri düşünceleri algılamak için gereklidir.

1. [Azure Portal](https://portal.azure.com/) oturum açın.

2. Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.

3. Tıklatın **veri + analiz** > **Bilişsel Hizmetler**. Ardından, tabloda belirtildiği gibi ayarları kullanmak için koşullarını kabul edin ve denetleyin **panoya Sabitle**.

    ![Bilişsel hesabı dikey penceresi oluşturma](media/functions-twitter-email/cog_svcs_account.png)

    | Ayar      |  Önerilen değer   | Açıklama                                        |
    | --- | --- | --- |
    | **Ad** | MyCognitiveServicesAccnt | Benzersiz bir hesap adı seçin. |
    | **API türü** | Metin Analizi API’si | Metin çözümlemek için kullanılan API.  |
    | **Konum** | Batı ABD | Şu anda yalnızca **Batı ABD** metin analizi için kullanılabilir. |
    | **Fiyatlandırma katmanı** | F0 | En düşük katman ile başlatın. Çağrıları dışında çalıştırırsanız, daha yüksek bir katmana ölçeklendirin.|
    | **Kaynak grubu** | myResourceGroup | Aynı kaynak grubunun tüm hizmetler için bu öğreticiyi kullanın.|

4. Tıklatın **oluşturma** hesabınızı oluşturmak için. Hesap oluşturulduktan sonra yeni Bilişsel hesabı panosuna sabitlediğiniz hizmetleriniz tıklatın. 

5. Hesabı'nda tıklatın **anahtarları**ve ardından değerini kopyalayın **anahtar 1** ve kaydedin. Bilişsel hizmetler hesabınıza mantıksal uygulama bağlanmak için bu anahtarı kullanın. 
 
    ![Anahtarlar](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a>İşlevi oluşturma

İşlevler bir iş akışındaki logic apps işleme görevlerini boşaltmak için harika bir yol sağlar. Bu öğretici, tweet düşünceleri puanları Bilişsel Hizmetleri'nden işlemek ve bir kategori değeri döndürmek için bir HTTP tetiklenen işlevi kullanır.  

1. İşlev uygulamanızı genişletin, tıklayın  **+**  düğmesine **işlevleri**, tıklatın **HTTPTrigger** şablonu. Tür `CategorizeSentiment` işlevi için **adı** tıklatıp **oluşturma**.

    ![İşlev uygulamalar dikey penceresinde, İşlevler +](media/functions-twitter-email/add_fun.png)

2. Run.csx dosyasının içeriğini aşağıdaki kodla değiştirin ve ardından **kaydetmek**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Bu işlev kodu istekte alınan düşünceleri puan bağlı bir renk kategori döndürür. 

3. İşlevi test etmek için tıklatın **Test** Test sekmesi genişletmek sağ uçta. Değerini yazın `0.2` için **istek gövdesinde**ve ardından **çalıştırmak**. Değerini **kırmızı** yanıt gövdesinde döndürülür. 

    ![Azure portalında işlevi test etme](./media/functions-twitter-email/test.png)

Artık düşünceleri puanları kategorilere ayıran bir işlev var. Ardından, işlevinizi Twitter ve Bilişsel hizmetler hesaplarınızı ile tümleşen bir mantıksal uygulama oluşturun. 

## <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma   

1. Azure portalında tıklatın **yeni** düğme Azure portalında sol üst köşesinde bulundu.

2. Tıklatın **Kurumsal tümleştirme** > **mantıksal uygulama**. Ardından, tablo, onay belirtildiği gibi ayarları kullanın **panoya Sabitle**, tıklatıp **oluşturma**.
 
4. Ardından, bir **adı** gibi `TweetSentiment`tablosunda belirtilen ayarları kullanmak, koşulları kabul edin ve denetleyin **panoya Sabitle**.

    ![Azure portalında mantıksal uygulama oluşturma](./media/functions-twitter-email/new_logicApp.png)

    | Ayar      |  Önerilen değer   | Açıklama                                        |
    | ----------------- | ------------ | ------------- |
    | **Ad** | TweetSentiment | Uygulamanız için uygun bir ad seçin. |
    | **Kaynak grubu** | myResourceGroup | Metin çözümlemek için kullanılan API.  |
    | **Konum** | Doğu ABD | Yakın bir konum seçin. |
    | **Kaynak grubu** | myResourceGroup | Var olan kaynak grubunu olarak önce seçin.|

4. Tıklatın **oluşturma** mantıksal uygulamanızı oluşturmak için. Uygulama oluşturulduktan sonra yeni mantıksal uygulamanızı panosuna sabitlediğiniz tıklayın. Ardından Logic Apps Tasarımcısı'nda aşağı kaydırın ve tıklatın **boş mantıksal uygulama** şablonu. 

    ![Boş Logic Apps şablon](media/functions-twitter-email/blank.png)

Logic Apps Tasarımcısı'nı şimdi hizmetler ve tetikleyiciler uygulamanıza eklemek için de kullanabilirsiniz.

## <a name="connect-to-twitter"></a>Twitter hesabına bağlanma

İlk olarak, Twitter hesabınız için bir bağlantı oluşturun. Mantıksal uygulama çalıştırmak için uygulamayı tetiklemek tweet'leri için yoklar.

1. Tasarımcısı'nda tıklayın **Twitter** 'ı tıklatın ve hizmeti **yeni tweet zaman nakledilir** tetikleyici. Twitter hesabınızda oturum açın ve hesabınızı kullanmak için Logic Apps yetkisi verin.

2. Tabloda belirtildiği gibi Twitter tetikleyici ayarları kullanın. 

    ![Twitter Bağlayıcısı ayarları](media/functions-twitter-email/azure_tweet.png)

    | Ayar      |  Önerilen değer   | Açıklama                                        |
    | ----------------- | ------------ | ------------- |
    | **Arama metni** | #Azure | Seçilen zaman aralığını yeni tweet'leri oluşturmak için yeterli için popülerdir diyez kullanın. Ücretsiz katmanı ve, diyez kullanarak çok popüler olduğunda, hızlı bir şekilde işlemleri Bilişsel hizmetler hesabınızı kullanabilirsiniz. |
    | **Sıklık** | Dakika | Twitter yoklama için kullanılan sıklık birim.  |
    | **Aralığı** | 15 | Twitter istekler sıklığı birimleri arasında geçen süre. |

3.  Tıklatın **kaydetmek** Twitter hesabınıza bağlanmak için. 

Artık uygulamanızı Twitter hesabına bağlıdır. Ardından, toplanan tweet'leri düşünceleri algılamak için metin analizi'ne bağlayın.

## <a name="add-sentiment-detection"></a>Düşünceleri algılama ekleme

1. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.

    ![Yeni adım ve bir eylem Ekle](media/functions-twitter-email/new_step.png)

2. İçinde **bir eylem seçin**, tıklatın **metin analizi**ve ardından **düşünceleri algılamak** eylem.

    ![Düşünceleri Algıla](media/functions-twitter-email/detect_sent.png)

3. Bir bağlantı adı gibi yazın `MyCognitiveServicesConnection`kaydedilen Bilişsel Hizmetler hesabı için anahtarını yapıştırın ve tıklatın **oluşturma**.  

4. Tıklatın **çözümlemek için metin** > **Tweet metin**ve ardından **kaydetmek**.  

    ![Düşünceleri Algıla](media/functions-twitter-email/ds_tta.png)

Düşünceleri algılama yapılandırılır, işlevinizi düşünceleri puan çıktısını kullanan bir bağlantı ekleyebilirsiniz.

## <a name="connect-sentiment-output-to-your-function"></a>Düşünceleri çıktı, işlevine bağlayın

1. Logic Apps Tasarımcısı'nda tıklayın **yeni adım** > **Eylem Ekle**ve ardından **Azure işlevleri**. 

2. Tıklatın **bir Azure işlevi seçin**seçin **CategorizeSentiment** daha önce oluşturduğunuz işlevi.  

    ![Bir Azure işlevi Seç gösteren azure işlevi kutusu](media/functions-twitter-email/choose_fun.png)

3. İçinde **iste gövde**, tıklatın **puan** ve ardından **kaydetmek**.

    ![Puan](media/functions-twitter-email/trigger_score.png)

Şimdi, düşünceleri puan mantığı uygulamadan gönderildiğinde işlevinizi tetiklenir. Bir renk kodlu kategorisi mantıksal uygulama işlevi tarafından döndürülür. Sonra düşünceleri değeri, gönderilen bir e-posta bildirimi ekleyin **kırmızı** işlevinden döndürülür. 

## <a name="add-email-notifications"></a>E-posta bildirimleri ekleme

Bir e-posta olarak düşünceleri puanlanır zaman tetiklemek için iş akışı son parçası olan _kırmızı_. Bu konuda bir Outlook.com bağlayıcısı kullanır. Gmail veya Office 365 Outlook Bağlayıcısı'nı kullanmak için benzer adımları gerçekleştirebilirsiniz.   

1. Logic Apps Tasarımcısı'nda tıklayın **yeni adım** > **bir koşul eklemek**. 

2. Tıklatın **bir değer seçin**, ardından **gövde**. Seçin **eşittir**, tıklatın **bir değer seçin** ve türü `RED`, tıklatıp **kaydetmek**. 

    ![Bir koşul mantıksal uygulama ekleyin.](media/functions-twitter-email/condition.png)

3. İçinde **Evet ise, hiçbir şey yapma**, tıklatın **Eylem Ekle**, arama `outlook.com`, tıklatın **bir e-posta Gönder**ve Outlook.com hesabınızda oturum açın.
    
    ![Koşul için bir eylem seçin.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Bir Outlook.com hesabınız yoksa, Gmail veya Office 365 Outlook gibi başka bir bağlayıcı seçebilirsiniz

4. İçinde **bir e-posta Gönder** eylem, belirtilen tabloda olarak e-posta ayarlarını kullanın. 

    ![Bir e-posta eylem göndermek için e-postayı yapılandırın.](media/functions-twitter-email/sendemail.png)

    | Ayar      |  Önerilen değer   | Açıklama  |
    | ----------------- | ------------ | ------------- |
    | **Hedef** | E-posta adresinizi yazın | Bildirim aldığı e-posta adresi. |
    | **Konu** | Negatif tweet düşünceleri algılandı  | E-posta bildirimi konu satırı.  |
    | **Gövde** | Tweet metin, konumu | Tıklatın **Tweet metin** ve **konumu** parametreleri. |

5.  **Kaydet** düğmesine tıklayın.

İş akışı tamamlandığına göre mantıksal uygulama etkinleştirin ve iş yerindeki işlevine bakın.

## <a name="test-the-workflow"></a>İş akışını sınayın.

1. Mantıksal Uygulama Tasarımcısı'nda tıklayın **çalıştırmak** uygulamayı başlatmak için.

2. Sol sütunda tıklatın **genel bakış** mantıksal uygulama durumunu görmek için. 
 
    ![Mantıksal uygulama yürütme durumu](media/functions-twitter-email/over1.png)

3. (İsteğe bağlı) Yürütme ayrıntılarını görmek için çalışır birini tıklatın.

4. Git, işlevi, günlükleri görüntülemek ve düşünceleri değerleri alınan ve işlenen olduğunu doğrulayın.
 
    ![İşlev günlüklerini görüntüle](media/functions-twitter-email/sent.png)

5. Potansiyel olarak negatif düşünceleri algılandığında, bir e-posta alırsınız. Bir e-posta almadıysanız, kırmızı döndürmek için işlev kodu değiştirebilirsiniz her zaman:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    E-posta bildirimleri doğruladıktan sonra özgün kodu değiştirin:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Bu öğreticiyi tamamladıktan sonra mantıksal uygulama devre dışı bırakmanız gerekir. Uygulama devre dışı bırakarak yürütmeleri için kartınızdan ve Bilişsel hizmetler hesabınızda işlemleri kullanarak kaçının.

Şimdi işlevleri Logic Apps iş akışı ile tümleştirmek için ne kadar kolay olduğunu gördünüz.

## <a name="disable-the-logic-app"></a>Mantıksal uygulama devre dışı bırak

Mantıksal uygulama devre dışı bırakmak için **genel bakış** ve ardından **devre dışı** ekranın üstünde. Bu mantıksal uygulama çalıştıran ve uygulamayı silmeden ücretlerinin yansıtılmasını durdurur. 

![İşlev günlükleri](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Bilişsel Hizmetler hesabı oluşturun.
> * Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.
> * Twitter hesabına bağlanan bir mantıksal uygulama oluşturun.
> * Düşünceleri algılama mantığı uygulamaya ekleyin. 
> * Mantıksal uygulama işlevine bağlayın.
> * İşlev yanıttan dayalı bir e-posta gönderin.

İşlevinizi için sunucusuz bir API oluşturma konusunda bilgi almak için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"] 
> [Azure İşlevlerini kullanarak sunucusuz bir API oluşturma](functions-create-serverless-api.md)

Logic Apps hakkında daha fazla bilgi için bkz: [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

