---
title: "bir Azure Machine Learning Klasik yeniden eğitme aaaTroubleshoot web hizmetini | Microsoft Docs"
description: "Tanımlamak ve bir Azure Machine Learning Web hizmeti için hello modeli yeniden eğitme, ortak sorunları aygıtındaki düzeltin."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Bir Azure Machine Learning Klasik Web hizmeti Hello yeniden eğitme sorunlarını giderme
## <a name="retraining-overview"></a>Yeniden eğitme genel bakış
Tahmine dayalı denemeye Puanlama web hizmeti olarak dağıttığınızda statik bir modelidir. Yeni veriler kullanılabilir olduğunda ya da kendi veri hello API hello tüketicisi varsa, hello modeli retrained toobe gerekir. 

Klasik Web hizmeti işlemi yeniden eğitme hello tam kılavuzu için bkz [yeniden eğitme Machine Learning modellerini program aracılığıyla](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>İşlemi yeniden eğitme
Web hizmeti tooretrain hello gerektiğinde, bazı ek parçalar eklemeniz gerekir:

* Eğitim denemenizi Hello dağıtılan bir Web hizmetidir. Merhaba deneme olmalıdır bir **Web hizmeti çıkış** modülü bağlı hello toohello çıktısını **Train Model** modülü.  
  
    ![Merhaba web hizmeti çıkış toohello train model ekleyin.][image1]
* Yeni bir uç noktası, Web hizmeti Puanlama tooyour eklendi.  Program aracılığıyla hello uç nokta ekleme hello başvurulan hello örnek kodu kullanarak yeniden eğitme Machine Learning program aracılığıyla konu modellerini veya hello Klasik Azure Portalı aracılığıyla.

Merhaba örnek C# kod hello eğitim Web Service'in API Yardım sayfası tooretrain modelinden daha sonra kullanabilirsiniz. Merhaba sonuçları değerlendirilen ve bunlarla memnun sonra hello eğitilen modeli Puanlama eklediğiniz hello yeni uç nokta kullanarak web hizmeti güncelleştirin.

Yerinde tüm hello parça ile tooretrain hello modeli gerçekleştirmeniz gereken hello önemli adımlar aşağıdaki gibidir:

1. Merhaba eğitim Web hizmeti çağrısı: hello çağrıdır toohello toplu yürütme hizmeti (BES), istek yanıtı hizmeti (RRS) hello değil. Merhaba API Yardım sayfası toomake hello çağrıda hello örnek C# kodu kullanabilirsiniz. 
2. Merhaba Hello değerleri bulma *BaseLocation*, *RelativeLocation*, ve *SasBlobToken*: Bu değerleri hello çıktısında çağrısı toohello eğitim Web döndürülür Hizmet. 
   ![örnek ve hello BaseLocation, RelativeLocation ve SasBlobToken değerleri yeniden eğitme hello Hello çıktısını gösteriliyor.][image6]
3. Güncelleştirme hello eklenen uç noktasından yeni web hizmeti ile Merhaba Puanlama hello eğitilmiş model: hello Machine Learning yeniden eğitme modelleri programlı olarak hello yeni uç noktasını güncelleyin. sağlanan hello örnek kodu kullanarak hello modeliyle yeni Puanlama toohello eklendi Merhaba eğitim Web hizmeti eğitilen modeli.

## <a name="common-obstacles"></a>Ortak engellerini
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Düzeltme eki URL'yi düzeltin hello varsa toosee denetleyin
Merhaba kullanmakta olduğunuz URL düzeltme eki hello bir hello ile ilişkili olmalıdır Web hizmeti Puanlama toohello eklediğiniz yeni Puanlama uç noktası. Yolları tooobtain hello düzeltme eki URL vardır:

**Seçenek 1: programlı şekilde**

tooget hello düzeltme eki URL düzeltin:

1. Merhaba çalıştırmak [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) örnek kodu.
2. Merhaba AddEndpoint Hello çıktısını Bul *HelpLocation* değer ve hello URL'yi kopyalayın.
   
   ![HelpLocation hello addEndpoint örneğinin hello çıkışı.][image2]
3. Yardım bağlantıları hello Web hizmeti için bir tarayıcı toonavigate tooa sayfası Hello URL yapıştırın.
4. Merhaba tıklatın **güncelleştirme kaynağı** bağlantı tooopen hello düzeltme eki Yardım sayfası.

**Seçenek 2: hello Klasik Azure portalını kullanın**

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Açık hello Machine Learning sekmesini tıklatın. ![Makine leaning sekmesini tıklatın.][image4]
3. Çalışma alanı adınız ardından **Web Hizmetleri**.
4. Web hizmeti birlikte çalıştığınız Puanlama hello'ı tıklatın. (Merhaba varsayılan hello web hizmeti adını değiştirmezseniz bu [Puanlama Exp içinde.] sona erer.)
5. Tıklatın **uç nokta ekleme**.
6. Merhaba endpoint eklendikten sonra hello uç nokta adına tıklayın. Ardından **güncelleştirme kaynağı** tooopen hello düzeltme eki uygulama Yardım sayfası.

> [!NOTE]
> Merhaba Tahmine dayalı Web hizmeti yerine hello uç nokta toohello eğitim Web hizmeti eklediyseniz, hello tıklattığınızda aşağıdaki hata hello alacak **güncelleştirme kaynağı** bağlantı: özür dileriz, ancak bu özellik desteklenmiyor veya Bu bağlamda kullanılabilir. Bu Web Hizmeti'nin güncelleştirilebilir kaynağı olmayan. Biz hello rahatsızlıktan ötürü özür dileriz ve bu iş akışı geliştirmeye çalışıyoruz.
> 
> 

![Yeni bir uç nokta Pano.][image3]

Hello düzeltme eki Yardım sayfası hello kullanmalısınız URL düzeltme eki içerir ve örnek kodu kullanabilirsiniz sağlar toocall onu.

![Düzeltme eki URL'si.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Onay toosee hello doğru Puanlama uç noktası güncelleştiriliyor
* Merhaba eğitim Web hizmeti düzeltme eki değil: hello düzeltme eki işlemi üzerinde Web hizmeti Puanlama hello gerçekleştirilmesi gerekir.
* Web hizmeti üzerinde Hello varsayılan uç nokta düzeltme eki değil: hello düzeltme eki işlemi üzerinde yeni eklediğiniz Web Hizmeti uç noktası Puanlama hello gerçekleştirilmesi gerekir.

Hangi Web hizmeti hello uç noktası tarafından ziyaret hello Klasik Azure portalı açıktır doğrulayabilirsiniz. 

> [!NOTE]
> Merhaba uç nokta toohello Tahmine dayalı Web hizmeti, hello eğitim Web hizmeti ekleme emin olun. Eğitim ve Tahmine dayalı bir Web hizmeti doğru olarak dağıttıysanız, listelenen iki ayrı Web Hizmetleri görmeniz gerekir. Merhaba Tahmine dayalı Web hizmeti, "[Tahmine dayalı exp.]" bitmelidir.
> 
> 

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Açık hello Machine Learning sekmesini tıklatın. ![Machine learning çalışma alanı UI.][image4]
3. Çalışma alanınızı seçin.
4. Tıklatın **Web Hizmetleri**.
5. Tahmine dayalı Web hizmetinizi seçin.
6. Yeni uç noktanızı toohello Web hizmeti eklendiğini doğrulayın.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Merhaba doğru bölgede olması tooensure, web hizmetidir hello çalışma denetleyin
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Machine Learning hello menüsünden seçin.
   ![Machine learning bölge UI.][image4]
3. Çalışma alanınızı Hello konumunu doğrulayın.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
