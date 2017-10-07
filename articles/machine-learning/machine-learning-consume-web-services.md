---
title: bir Azure Machine Learning Web hizmeti aaaHow tooconsume | Microsoft Docs
description: "Machine learning hizmetine dağıtıldığında, gerçek zamanlı istek-yanıt hizmeti veya toplu yürütme hizmeti olarak hello sunulacağını RESTFul Web hizmeti tüketilebilir."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a>Nasıl tooconsume bir Azure Machine Learning Web hizmeti

Bir Azure Machine Learning Tahmine dayalı modeli bir Web hizmeti olarak dağıttığınızda, REST API toosend kullanabilirsiniz, veri ve get tahminleri. Gerçek zamanlı veya toplu iş modunda hello veriler gönderebilir.

Hakkında daha fazla bilgi bulabilirsiniz toocreate ve Machine Learning Studio burada kullanarak bir Machine Learning Web hizmetini dağıtma:

* Toocreate Machine Learning Studio'da bir denemeyi nasıl görürüm üzerinde bir öğretici için [ilk denemenizi oluşturma](machine-learning-create-experiment.md).
* Ayrıntılar için toodeploy bir Web hizmeti bkz [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).
* Genel olarak, hello Machine Learning hakkında daha fazla bilgi için ziyaret [Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Genel Bakış
Hello Azure Machine Learning Web hizmeti ile bir dış uygulama Machine Learning bir iş akışı Puanlama modeli ile gerçek zamanlı iletişim kurar. Bir Machine Learning Web hizmeti çağrısı tooan dış uygulama tahmin sonuçlarını döndürür. toomake bir Machine Learning Web hizmeti çağrısı, tahmin dağıttığınızda oluşturduğunuz bir API anahtarı geçirirsiniz. Merhaba Machine Learning Web hizmeti web programlama projeleri için popüler bir mimari seçimi olan REST'i temel alır.

Azure Machine Learning iki tür hizmet içerir:

* İstek-yanıt hizmeti (RRS) – düşük gecikme süresi, oluşturulan ve dağıtılan hello Machine Learning Studio toohello durum bilgisi olmayan modellere bir arabirim sağlayan yüksek düzeyde ölçeklenebilir hizmet.
* Toplu yürütme hizmeti (BES) – zaman uyumsuz bir hizmet veri kayıtları için toplu iş yapan.

Machine Learning Web Hizmetleri hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Bir Azure Machine Learning yetkilendirme anahtarı alma
Denemenizi dağıttığınızda, API anahtarları hello Web hizmeti için oluşturulur. Merhaba anahtarları çeşitli konumlardan alabilirsiniz.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>Merhaba Microsoft Azure Machine Learning Web Hizmetleri Portalı'ndan
İçinde toohello oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.

Yeni Machine Learning Web hizmeti için tooretrieve hello API anahtarı:

1. Hello Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Web Hizmetleri** hello üst menü.
2. Merhaba Web hizmeti tooretrieve hello anahtar istediğiniz'ı tıklatın.
3. Merhaba üst menüsünde **Tüket**.
4. Kopyalayın ve hello kaydedin **birincil anahtar**.

tooretrieve hello API anahtarı Klasik Machine Learning Web hizmeti için:

1. Hello Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Klasik Web Hizmetleri** hello üst menü.
2. Merhaba Web hizmeti ile çalıştığınız'ı tıklatın.
3. Tooretrieve hello anahtar istediğiniz hello uç noktasına tıklayın.
4. Merhaba üst menüsünde **Tüket**.
5. Kopyalayın ve hello kaydedin **birincil anahtar**.

### <a name="classic-web-service"></a>Klasik Web hizmeti
 Klasik Web hizmeti için bir anahtar, Machine Learning Studio veya hello Klasik Azure portalı de alabilirsiniz.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. Machine Learning Studio'da tıklatın **WEB Hizmetleri** hello soldaki.
2. Bir Web hizmeti tıklatın. Merhaba **API anahtarı** hello üzerinde olduğu **PANO** sekmesi.

#### <a name="azure-classic-portal"></a>Klasik Azure portalı
1. Tıklatın **MACHINE LEARNING** hello soldaki.
2. Web hizmetiniz bulunduğu hello çalışma alanını tıklatın.
3. Tıklatın **WEB Hizmetleri**.
4. Bir Web hizmeti tıklatın.
5. Bir uç nokta'ı tıklatın. sağ alt hello Hello "API anahtarı" çalışmıyor.

## <a id="connect"></a>Tooa Machine Learning Web hizmetine bağlanın
Tooa Machine Learning Web hizmeti, HTTP istek ve yanıt destekleyen herhangi bir programlama dili kullanarak bağlanabilir. C#, Python ve R örnekler bir Machine Learning Web hizmeti Yardım sayfasından görüntüleyebilirsiniz.

**Machine Learning API Yardım** Machine Learning API'si Yardım Web hizmetini dağıttığınızda oluşturulur. Bkz: [Azure Machine Learning izlenecek dağıtımı Web hizmeti](machine-learning-walkthrough-5-publish-web-service.md).
Merhaba Machine Learning API'si Yardım tahmin Web hizmeti hakkındaki ayrıntıları içerir.

1. Merhaba Web hizmeti ile çalıştığınız'ı tıklatın.
2. Tooview hello API Yardım sayfasında istediğiniz hello uç noktasına tıklayın.
3. Merhaba üst menüsünde **Tüket**.
4. Tıklatın **API Yardım sayfası** hello istek-yanıt ya da toplu iş yürütme bitiş noktaları altında.

**tooview Machine Learning API'si yardımcı olmak için yeni Web hizmeti**

Hello Azure Machine Learning Web Hizmetleri portalı:

1. Tıklatın **WEB Hizmetleri** hello üst menüsünde.
2. Merhaba Web hizmeti tooretrieve hello anahtar istediğiniz'ı tıklatın.

Tıklatın **Tüket** tooget hello isteği Reposonse ve toplu yürütme Hizmetleri ve örnek kodda C#, R ve Python için URI hello.

Tıklatın **Swagger API'si** tooget hello API'leri için temel belgelere adlı hello Swagger sağlanan URI.

### <a name="c-sample"></a>C# örnek
tooconnect tooa Machine Learning Web hizmeti kullanan bir **HttpClient** ScoreData geçirme. ScoreData bir FeatureVector hello ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir. Bir API anahtarı ile toohello Machine Learning hizmetinin kimlik doğrulaması.

tooconnect tooa Machine Learning Web hizmeti hello **Microsoft.AspNet.WebApi.Client** NuGet paketi yüklü olmalıdır.

**Microsoft.AspNet.WebApi.Client NuGet Visual Studio yükleme**

1. Yayımlama Hello indirme UCI kümesinden: yetişkin 2 sınıfı dataset Web hizmeti.
2. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.
3. Seçin **Install-Package Microsoft.AspNet.WebApi.Client**.

**toorun hello kod örneği**

1. Yayımla "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, hello Machine Learning örnek koleksiyonunun bir parçası.
2. Apikey ile yapılan bir Web hizmetinden hello anahtarla atayın. Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** üstünde.
3. Merhaba istek URI'si ile serviceUri atayın.

### <a name="python-sample"></a>Python örneği
tooconnect tooa Machine Learning Web hizmeti kullanmak hello **urllib2** ScoreData geçirme kitaplığı. ScoreData bir FeatureVector hello ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir. Bir API anahtarı ile toohello Machine Learning hizmetinin kimlik doğrulaması.

**toorun hello kod örneği**

1. Dağıtma "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, hello Machine Learning örnek koleksiyonunun bir parçası.
2. Apikey ile yapılan bir Web hizmetinden hello anahtarla atayın. Merhaba bkz **bir Azure Machine Learning yetkilendirme anahtarı alma** hello başına bir kısmına bu makalenin.
3. Merhaba istek URI'si ile serviceUri atayın.

