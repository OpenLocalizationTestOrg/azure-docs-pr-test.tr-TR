---
title: "aaaCreate Azure Logic Apps ile tümleşen bir işlev | Microsoft Docs"
description: "Azure mantıksal uygulamaları ve Azure Bilişsel hizmetler toocategorize tweet düşünceleri ile tümleşen bir işlev oluşturun ve düşünceleri düşük olduğunda bildirimleri gönderin."
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
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Azure Logic Apps ile tümleşen bir işlev oluşturun

Azure işlevleri hello Logic Apps Tasarımcısı Azure Logic Apps ile tümleşir. Bu tümleştirme işlevlerin diğer Azure ve üçüncü taraf hizmetleri düzenlemelerin içinde gücünün hello kullanmanıza olanak sağlar. 

Bu öğreticide gösterilmiştir toouse nasıl çalıştığını Twitter gönderileri gelen Logic Apps ve Azure Bilişsel hizmetler tooanalyze düşünceleri ile. Bir HTTP tetiklenen işlevi tweet'leri yeşil, sarı veya kırmızı hello düşünceleri puan üzerinde dayalı olarak kategorilere ayırır. Zayıf düşünceleri algılandığında bir e-posta gönderilir. 

![ilk iki adım uygulamasının mantığı Uygulama Tasarımcısı'nda Görüntü](media/functions-twitter-email/designer1.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Bilişsel Hizmetler hesabı oluşturun.
> * Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.
> * TooTwitter bağlayan bir mantıksal uygulama oluşturun.
> * Düşünceleri algılama toohello mantıksal uygulama ekleyin. 
> * Merhaba mantığı uygulama toohello işlevi bağlayın.
> * Merhaba işlevi hello yanıttan dayalı bir e-posta gönderin.

## <a name="prerequisites"></a>Ön koşullar

+ Etkin bir [Twitter](https://twitter.com/) hesabı. 
+ Bir [Outlook.com](https://outlook.com/) hesap (bildirim göndermek için).
+ Bu konu içinde oluşturulan başlangıç noktası hello kaynaklarını kullanan [hello Azure portal ' ilk işlevinizi oluşturma](functions-create-first-azure-function.md).  
Zaten yapmadıysanız, bu adımları şimdi toocreate işlevi uygulamanızı tamamlayın.

## <a name="create-a-cognitive-services-account"></a>Bilişsel Hizmetler hesabı oluşturma

Bilişsel hizmetler izlenmekte olan tweet'leri, gerekli toodetect hello düşünceleri hesabıdır.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).

2. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

3. Tıklatın **veri + analiz** > **Bilişsel Hizmetler**. Ardından, olarak hello ayarları kullan hello tablosunda belirtilen hello koşullarını kabul edin ve denetleyin **PIN toodashboard**.

    ![Bilişsel hesabı dikey penceresi oluşturma](media/functions-twitter-email/cog_svcs_account.png)

    | Ayar      |  Önerilen değer   | Açıklama                                        |
    | --- | --- | --- |
    | **Ad** | MyCognitiveServicesAccnt | Benzersiz bir hesap adı seçin. |
    | **API türü** | Metin Analizi API’si | API tooanalyze metin kullanılır.  |
    | **Konum** | Batı ABD | Şu anda yalnızca **Batı ABD** metin analizi için kullanılabilir. |
    | **Fiyatlandırma katmanı** | F0 | Merhaba düşük katmanı ile başlatın. Çağrıları dışında çalıştırırsanız, tooa daha yüksek katman ölçeklendirin.|
    | **Kaynak grubu** | myResourceGroup | Kullanım hello aynı kaynak grubu bu öğreticideki tüm hizmetler için.|

4. Tıklatın **oluşturma** toocreate hesabınızı. Merhaba hesabı oluşturulduktan sonra yeni Bilişsel Hizmetler hesabı sabitlenmiş toohello panonuz'ı tıklatın. 

5. Merhaba hesabında tıklatın **anahtarları**ve ardından hello değerini kopyalayın **anahtar 1** ve kaydedin. Bu anahtar tooconnect hello mantığı uygulama tooyour Bilişsel Hizmetler hesabı kullanın. 
 
    ![Anahtarlar](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Create Hello işlevi

İşlevleri işleme görevlerini bir iş akışındaki logic apps mükemmel şekilde toooffload sağlar. Bu öğretici, bir HTTP tetiklenen işlevi tooprocess tweet düşünceleri puanları Bilişsel hizmetler ve return bir kategori değeri kullanır.  

1. İşlevi uygulamanızı genişletin, hello tıklayın  **+**  sonraki çok düğmesini**işlevleri**, hello tıklatın **HTTPTrigger** şablonu. Tür `CategorizeSentiment` hello işlevi için **adı** tıklatıp **oluşturma**.

    ![İşlev uygulamalar dikey penceresinde, İşlevler +](media/functions-twitter-email/add_fun.png)

2. Merhaba hello run.csx dosyasının içeriğini koddan hello ile değiştirin ve ardından **kaydetmek**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
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
    Bu işlev kodu hello istekte alınan hello düşünceleri puan bağlı bir renk kategori döndürür. 

3. tootest hello işlevi,'ı tıklatın **Test** hello en sağdaki tooexpand hello Test sekmesinde. Değerini yazın `0.2` hello için **istek gövdesinde**ve ardından **çalıştırmak**. Değerini **kırmızı** hello hello yanıt gövdesinde döndürülür. 

    ![Merhaba işlevi hello Azure portal test etme](./media/functions-twitter-email/test.png)

Artık düşünceleri puanları kategorilere ayıran bir işlev var. Ardından, işlevinizi Twitter ve Bilişsel hizmetler hesaplarınızı ile tümleşen bir mantıksal uygulama oluşturun. 

## <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma   

1. İçinde Azure portal Merhaba, hello tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

2. Tıklatın **Kurumsal tümleştirme** > **mantıksal uygulama**. Ardından, olarak hello ayarları kullan hello tablosunda belirtilen denetleyin **PIN toodashboard**, tıklatıp **oluşturma**.
 
4. Ardından, türü bir **adı** gibi `TweetSentiment`hello tablosunda belirtilen hello ayarları kullanmak, hello koşullarını kabul edin ve denetleyin **PIN toodashboard**.

    ![Hello Azure portal mantıksal uygulama oluşturma](./media/functions-twitter-email/new_logicApp.png)

    | Ayar      |  Önerilen değer   | Açıklama                                        |
    | ----------------- | ------------ | ------------- |
    | **Ad** | TweetSentiment | Uygulamanız için uygun bir ad seçin. |
    | **Kaynak grubu** | myResourceGroup | API tooanalyze metin kullanılır.  |
    | **Konum** | Doğu ABD | Konum Kapat tooyou seçin. |
    | **Kaynak grubu** | myResourceGroup | Seçin öncekiyle aynı olan bir kaynak grubunu hello.|

4. Tıklatın **oluşturma** toocreate mantıksal uygulamanızı. Merhaba uygulama oluşturulduktan sonra yeni bir mantıksal uygulama sabitlenmiş toohello Pano'ı tıklatın. Ardından hello Logic Apps Tasarımcı'da, aşağı kaydırın ve hello tıklatın **boş mantıksal uygulama** şablonu. 

    ![Boş Logic Apps şablon](media/functions-twitter-email/blank.png)

Artık hello Logic Apps Tasarımcısı tooadd hizmetler ve tetikleyiciler tooyour uygulamasını kullanabilir.

## <a name="connect-tootwitter"></a>TooTwitter Bağlan

İlk olarak, bir bağlantı tooyour Twitter hesabı oluşturun. Merhaba mantıksal uygulama hello uygulama toorun tetiklemek tweet'leri için yoklar.

1. Merhaba Tasarımcısı'nda hello tıklayın **Twitter** hello'ı tıklatın ve hizmeti **yeni tweet zaman nakledilir** tetikleyici. Tooyour Twitter hesabıyla oturum açın ve Logic Apps toouse hesabınızı yetkisi verin.

2. Merhaba tabloda belirtildiği gibi Hello Twitter tetikleyici ayarları kullanın. 

    ![Twitter Bağlayıcısı ayarları](media/functions-twitter-email/azure_tweet.png)

    | Ayar      |  Önerilen değer   | Açıklama                                        |
    | ----------------- | ------------ | ------------- |
    | **Arama metni** | #Azure | Seçilen hello aralığa toogenerate yeni tweet'leri için yeterince popüler bir hashtag kullanın. Hello ücretsiz katmanı ve, diyez kullanarak çok popüler olduğunda, hızlı bir şekilde hello işlemleri Bilişsel hizmetler hesabınızı kullanabilirsiniz. |
    | **Sıklık** | Dakika | Merhaba sıklığı birimi twitter yoklama için kullanılır.  |
    | **Aralığı** | 15 | Merhaba sıklığı birimlerindeki Twitter istekleri arasındaki süre. |

3.  Tıklatın **kaydetmek** tooconnect tooyour Twitter hesabı. 

Uygulamanızı bağlı tooTwitter sunulmuştur. Ardından, tootext analytics toodetect hello düşünceleri toplanan tweet'leri, bağlanın.

## <a name="add-sentiment-detection"></a>Düşünceleri algılama ekleme

1. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.

    ![Yeni adım ve bir eylem Ekle](media/functions-twitter-email/new_step.png)

2. İçinde **bir eylem seçin**, tıklatın **metin analizi**ve ardından hello **düşünceleri algılamak** eylem.

    ![Düşünceleri Algıla](media/functions-twitter-email/detect_sent.png)

3. Bir bağlantı adı gibi yazın `MyCognitiveServicesConnection`kaydedilen Bilişsel Hizmetler hesabı için başlangıç anahtarını yapıştırın ve tıklatın **oluşturma**.  

4. Tıklatın **metin tooanalyze** > **Tweet metin**ve ardından **kaydetmek**.  

    ![Düşünceleri Algıla](media/functions-twitter-email/ds_tta.png)

Düşünceleri algılama yapılandırılır, hello düşünceleri puan çıktısını kullanan bir bağlantı tooyour işlevi ekleyebilirsiniz.

## <a name="connect-sentiment-output-tooyour-function"></a>Düşünceleri çıktı tooyour işlevi Bağlan

1. Hello Logic Apps Tasarımcı'da, tıklatın **yeni adım** > **Eylem Ekle**ve ardından **Azure işlevleri**. 

2. Tıklatın **bir Azure işlevi seçin**seçin hello **CategorizeSentiment** daha önce oluşturduğunuz işlevi.  

    ![Bir Azure işlevi Seç gösteren azure işlevi kutusu](media/functions-twitter-email/choose_fun.png)

3. İçinde **iste gövde**, tıklatın **puan** ve ardından **kaydetmek**.

    ![Puan](media/functions-twitter-email/trigger_score.png)

Şimdi, düşünceleri puan hello mantığı uygulamadan gönderildiğinde işlevinizi tetiklenir. Ren kodlu bir kategori toohello mantıksal uygulama hello fonksiyonu tarafından döndürülür. Sonra düşünceleri değeri, gönderilen bir e-posta bildirimi ekleyin **kırmızı** hello işlevinden döndürülür. 

## <a name="add-email-notifications"></a>E-posta bildirimleri ekleme

Merhaba son hello iş akışının bir parçası olduğunda tootrigger bir e-posta olarak hello düşünceleri puanlanır _kırmızı_. Bu konuda bir Outlook.com bağlayıcısı kullanır. Benzer adımları toouse Gmail veya Office 365 Outlook bağlayıcı gerçekleştirebilirsiniz.   

1. Hello Logic Apps Tasarımcı'da, tıklatın **yeni adım** > **bir koşul eklemek**. 

2. Tıklatın **bir değer seçin**, ardından **gövde**. Seçin **eşittir**, tıklatın **bir değer seçin** ve türü `RED`, tıklatıp **kaydetmek**. 

    ![Bir koşul toohello mantıksal uygulama ekleyin.](media/functions-twitter-email/condition.png)

3. İçinde **Evet ise, hiçbir şey yapma**, tıklatın **Eylem Ekle**, aramak `outlook.com`, tıklatın **bir e-posta Gönder**ve tooyour Outlook.com hesap oturum.
    
    ![Merhaba koşul için bir eylem seçin.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Bir Outlook.com hesabınız yoksa, Gmail veya Office 365 Outlook gibi başka bir bağlayıcı seçebilirsiniz

4. Merhaba, **bir e-posta Gönder** eylem olarak hello e-posta ayarları kullan hello tablosunda belirtilen. 

    ![Merhaba e-posta e-posta eylemin hello göndermek için yapılandırın.](media/functions-twitter-email/sendemail.png)

    | Ayar      |  Önerilen değer   | Açıklama  |
    | ----------------- | ------------ | ------------- |
    | **Hedef** | E-posta adresinizi yazın | Merhaba bildirim aldığı hello e-posta adresi. |
    | **Konu** | Negatif tweet düşünceleri algılandı  | Merhaba e-posta bildirimi Hello konu satırı.  |
    | **Gövde** | Tweet metin, konumu | Merhaba tıklatın **Tweet metin** ve **konumu** parametreleri. |

5.  **Kaydet** düğmesine tıklayın.

Merhaba iş akışı tamamlandığına göre hello mantıksal uygulama etkinleştirin ve iş yerindeki hello işlevine bakın.

## <a name="test-hello-workflow"></a>Test hello iş akışı

1. Hello mantığı Uygulama Tasarımcısı'de, tıklatın **çalıştırmak** toostart hello uygulama.

2. Merhaba sol sütunda tıklatın **genel bakış** hello mantıksal uygulama toosee hello durumu. 
 
    ![Mantıksal uygulama yürütme durumu](media/functions-twitter-email/over1.png)

3. (İsteğe bağlı) Merhaba çalışır toosee hello yürütme ayrıntılarını birini tıklatın.

4. Git tooyour işlevi, hello günlüklerini görüntülemek ve düşünceleri değerleri alınan ve işlenen olduğunu doğrulayın.
 
    ![İşlev günlüklerini görüntüle](media/functions-twitter-email/sent.png)

5. Potansiyel olarak negatif düşünceleri algılandığında, bir e-posta alırsınız. Bir e-posta almadıysanız, her zaman hello işlevi kod tooreturn kırmızı değiştirebilirsiniz:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    E-posta bildirimleri doğruladıktan sonra geri toohello özgün kodu değiştirin:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Bu öğreticiyi tamamladıktan sonra hello mantıksal uygulama devre dışı bırakmanız gerekir. Merhaba uygulama devre dışı bırakarak yürütmeleri için kartınızdan ve Bilişsel hizmetler hesabınızda hello işlemleri kullanarak kaçının.

Şimdi ne kadar kolay toointegrate işlevleri Logic Apps akışına olduğunu gördünüz.

## <a name="disable-hello-logic-app"></a>Merhaba mantıksal uygulama devre dışı bırak

toodisable hello mantıksal uygulama'ı tıklatın **genel bakış** ve ardından **devre dışı** Merhaba ekranında hello üstünde. Çalıştıran ve hello uygulama silmeden ücretlerinin yansıtılmasını hello mantıksal uygulama durdurur. 

![İşlev günlükleri](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Bilişsel Hizmetler hesabı oluşturun.
> * Tweet düşünceleri kategorilere ayıran bir işlev oluşturun.
> * TooTwitter bağlayan bir mantıksal uygulama oluşturun.
> * Düşünceleri algılama toohello mantıksal uygulama ekleyin. 
> * Merhaba mantığı uygulama toohello işlevi bağlayın.
> * Merhaba işlevi hello yanıttan dayalı bir e-posta gönderin.

Toohello sonraki öğretici toolearn nasıl ilerlemek için işlevinizi toocreate sunucusuz bir API.

> [!div class="nextstepaction"] 
> [Azure İşlevlerini kullanarak sunucusuz bir API oluşturma](functions-create-serverless-api.md)

Logic Apps hakkında daha fazla toolearn bkz [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

