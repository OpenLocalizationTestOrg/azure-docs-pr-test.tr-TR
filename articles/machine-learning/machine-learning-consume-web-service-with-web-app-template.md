---
title: "bir Machine Learning web hizmeti bir web uygulaması şablonu aaaConsume | Microsoft Docs"
description: "Azure Market tooconsume Azure Machine Learning Tahmine dayalı web hizmetinde bir web uygulaması şablonu kullanın."
keywords: "Web hizmeti, operationalization, REST API makine öğrenme"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Bir Azure Machine Learning web hizmetini web uygulaması şablonu ile kullanma

Bir kez artık Tahmine dayalı modelde geliştirilen ve Machine Learning Studio kullanarak bir Azure web hizmeti dağıtılmış veya R veya Python gibi araçları kullanarak, bir REST API kullanarak hello kullanıma hazır hale getirilmiş modeli erişebilir.

Tooconsume hello REST API ve erişim hello web hizmetini birkaç yolla vardır. Örneğin, bir uygulama C# ' ta R, yazabilirsiniz veya Python hello kullanarak örnek hello web hizmetini dağıttığınızda sizin için oluşturulan kod (Merhaba bulunan [Machine Learning Web Hizmetleri portalı](https://services.azureml.net/quickstart) veya hello web hizmeti panosunda Machine Learning Studio). Veya hello örnek Microsoft Excel çalışma kitabı hello sırasında oluşturduğunuz kullanabilirsiniz aynı anda.

Ancak, web hizmetinin çalıştığı hello Web Uygulama Şablonları hello kullanılabilir aracılığıyla hızlı ve kolay bir yol tooaccess hello [Azure Web uygulaması Market](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Hello Azure Machine Learning Web Uygulama Şablonları
Merhaba web uygulama şablonları hello Azure Marketi kullanılabilir web hizmetinizin giriş verilerini ve beklenen sonuçları bildiği bir özel web uygulaması oluşturabilirsiniz. Toodo gereken tek şey hello web uygulama erişim tooyour web hizmeti ve veri verin ve hello şablon rest hello.

İki şablonlar kullanılabilir:

* [Azure ML istek-yanıt hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Her bir şablon web hizmetiniz için hello API URI ve anahtarı kullanarak bir örnek ASP.NET uygulaması oluşturur ve bir web sitesi tooAzure dağıtır. Merhaba istek-yanıt hizmeti (RRS) şablonu toosend veri toohello web hizmeti tooget tek bir sonuç tek bir satır sağlayan bir web uygulaması oluşturur. Merhaba toplu yürütme hizmeti (BES) şablonu oluşturur toosend sağlayan bir web uygulaması verileri tooget çok sayıda satırı birden çok sonuç.

Hiçbir kodlama Bu şablonlar gerekli toouse değil. Yalnızca hello API anahtarı ve URI sağlayın ve hello şablon hello uygulamayı sizin için oluşturur.

tooget hello API anahtarı ve bir web hizmeti için istek URI'si:

1. Merhaba, [Web Hizmetleri portalı](https://services.azureml.net/quickstart), yeni bir web hizmeti için tıklatın **Web Hizmetleri** hello üstünde. Veya bir Klasik web hizmeti tıklatın **Klasik Web Hizmetleri**.
2. Merhaba web hizmeti tooaccess istediğiniz'ı tıklatın.
3. Klasik web hizmeti, tooaccess istediğiniz hello uç noktası'ı tıklatın.
4. Tıklatın **Tüket** hello üstünde.
5. Kopya hello **birincil** veya **ikincil anahtar** ve kaydedin.
6. İstek-yanıt hizmeti (RRS) şablonu oluşturuyorsanız, hello kopyalama **istek-yanıt** URI ve kaydedin. Bir toplu iş yürütme hizmeti (BES) şablonu oluşturuyorsanız, hello kopyalama **toplu istekleri** URI ve kaydedin.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Nasıl toouse hello istek-yanıt hizmeti (RRS) şablonu
Bu adımları toouse hello RR web uygulaması şablonu, hello Aşağıdaki diyagramda gösterildiği gibi izleyin.

![İşlem toouse RRS web şablonu][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Toohello Git [Azure portal](https://portal.azure.com), **oturum açma**, tıklatın **yeni**, aramak ve seçmek **Azure ML istek-yanıt hizmeti Web uygulaması**,'ye tıklayın **Oluşturma**. 
   
   * Web uygulamanızı benzersiz bir ad verin. Merhaba hello web uygulamasının URL'sini ve ardından bu ad olacaktır `.azurewebsites.net.` Örneğin,`http://carprediction.azurewebsites.net.`
   * Web hizmetiniz altında çalıştığı Hello Azure aboneliği ve hizmetleri seçin.
   * **Oluştur**'a tıklayın.
     
     ![Web uygulaması oluşturma][image5]

4. Azure hello web uygulamasına dağıtmayı bitirdiğinde, hello tıklatın **URL** hello Azure web uygulaması Ayarları sayfasında, veya bir web tarayıcısında hello URL'sini girin. Örneğin, `http://carprediction.azurewebsites.net.`
5. Web uygulaması ilk çalışır, sorar Merhaba'ne zaman hello **API gönderme URL'sini** ve **API anahtarı**.
   Daha önce kaydettiğiniz hello değerleri girin (**istek URI'si** ve **API anahtarı**sırasıyla).
     
     Tıklatın **gönderme**.
     
     ![POST URI ve API anahtarını girin][image6]

6. web uygulaması görüntüler Hello kendi **Web Uygulama Yapılandırması** hello geçerli web hizmeti ayarları sayfası. Burada hello web uygulaması tarafından kullanılan toohello ayarlarını değişiklik yapabilirsiniz.
   
   > [!NOTE]
   > Burada Hello ayarlarını değiştirdiğinizde yalnızca bunları bu web uygulaması için değişir. Web hizmetinizin hello varsayılan ayarları değiştirmez. Örneğin, hello değiştirirseniz **açıklama** burada hello web hizmeti panosundaki Machine Learning Studio'da gösterilen hello açıklama değişmez.
   > 
   > 
   
    İşiniz bittiğinde tıklatın **değişiklikleri kaydetmek**ve ardından **tooHome sayfa Git**.

7. Hello toosend tooyour web hizmeti giriş sayfasına girdiğiniz değerleri. Tıklatın **gönderme** zaman işiniz bittiğinde ve hello sonuç döndürülecek.

Tooreturn toohello istiyorsanız **yapılandırma** sayfasında, Git toohello `setting.aspx` hello web uygulaması sayfasında. Örneğin: `http://carprediction.azurewebsites.net/setting.aspx.` istendiğinde tooenter hello API anahtarı yeniden olacaktır - tooaccess hello sayfa ve hello ayarları güncelleştirme gerekir.

Durdurmak, yeniden başlatın veya hello Azure portal başka bir web uygulaması gibi hello web uygulamasında silin. Çalıştığı sürece toohello ev web adresini göz atın ve yeni değerler girin.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Nasıl toouse hello toplu yürütme hizmeti (BES) şablonu
Merhaba BES kullanabilirsiniz hello aynı şekilde hello RR şablon olarak dışında oluşturulan bu hello web uygulaması web uygulaması şablonu etmenizi sağlar toosubmit verilerin birden çok satır ve birden çok sonuç alırsınız.

bir toplu iş yürütme web hizmeti için giriş değerleri Hello Azure depolama veya bir yerel dosya gelebilir; Merhaba sonuçları bir Azure depolama kapsayıcısında depolanır.
Bu nedenle, artıracaksınız bir Azure depolama kapsayıcısı toohold hello web uygulaması tarafından döndürülen sonuçları hello ve tooget giriş verilerinizi hazır olması gerekir.

![Toouse BES işlem web şablonu][image2]

1. İzleme hello aynı yordamı toocreate hello BES web uygulaması Git dışında hello RR şablonu için olduğu gibi çok[Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Azure Marketi BES şablona hello ve tıklayın **Web uygulaması oluşturma** .

2. saklı hello sonuçları istediğiniz toospecify hello web uygulama giriş sayfasında hello hedef kapsayıcı bilgileri girin. Ayrıca, başlangıç web uygulaması hello giriş değerleri, yerel bir dosya veya bir Azure depolama kapsayıcısı nereden belirtin.
   Tıklatın **gönderme**.
   
    ![Depolama birimi bilgileri][image7]

Merhaba web uygulaması iş durumunu içeren bir sayfa görüntülenir.
Hello iş tamamlandığında hello sonuçları Azure blob depolama alanındaki hello konumunu verilmesi. Merhaba sonuçları tooa yerel dosya indirilmesi hello seçeneğiniz de vardır.

## <a name="for-more-information"></a>Daha fazla bilgi için
toolearn hakkında daha fazla bilgi...

* machine learning denemeyi Machine Learning Studio ile bkz [Azure Machine Learning Studio'da ilk denemenizi oluşturma](machine-learning-create-experiment.md)
* machine learning web hizmeti olarak denemeler toodeploy nasıl görürüm [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md)
* diğer yolları tooaccess web hizmetiniz bkz [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
