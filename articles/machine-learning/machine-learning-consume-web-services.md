---
title: Bir Azure Machine Learning Web hizmetini kullanma | Microsoft Docs
description: "Machine learning hizmeti dağıtıldıktan sonra gerçek zamanlı istek-yanıt hizmeti veya toplu yürütme hizmeti olarak kullanılabilir hale getirileceğini RESTFul Web hizmeti tüketilebilir."
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
ms.openlocfilehash: eec9f637b4b2306ab4a888dbd5ef5b9a021bcac5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a>Bir Azure Machine Learning Web hizmetini kullanma

Bir Azure Machine Learning Tahmine dayalı modeli bir Web hizmeti olarak dağıttığınızda, veri göndermek ve Öngörüler elde etmek için bir REST API'si kullanabilirsiniz. Gerçek zamanlı veya toplu iş modunda veriler gönderebilir.

Oluştur ve buraya Machine Learning Studio kullanarak bir Machine Learning Web hizmetini dağıtma hakkında daha fazla bilgi bulabilirsiniz:

* Machine Learning Studio'da bir deneme oluşturma konusunda bir öğretici için bkz: [ilk denemenizi oluşturma](machine-learning-create-experiment.md).
* Web hizmetinin nasıl dağıtılacağı hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).
* Machine Learning hakkında daha fazla bilgi için genel olarak, ziyaret [Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Genel Bakış
Azure Machine Learning Web hizmeti ile bir dış uygulama Machine Learning bir iş akışı Puanlama modeli ile gerçek zamanlı iletişim kurar. Bir Machine Learning Web hizmeti çağrısı bir dış uygulamaya tahmin sonuçlarını döndürür. Bir Machine Learning Web hizmeti çağrısı yapmak için bir tahmini dağıttığınızda oluşturduğunuz bir API anahtarı geçirirsiniz. Machine Learning Web hizmeti web programlama projeleri için popüler bir mimari seçimi olan REST'i temel alır.

Azure Machine Learning iki tür hizmet içerir:

* İstek-yanıt hizmeti (RRS) – düşük gecikme, Machine Learning Studio'dan oluşturulan ve dağıtılan durum bilgisi olmayan modellere bir arabirim sağlayan yüksek düzeyde ölçeklenebilir hizmet.
* Toplu yürütme hizmeti (BES) – zaman uyumsuz bir hizmet veri kayıtları için toplu iş yapan.

Machine Learning Web Hizmetleri hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Bir Azure Machine Learning yetkilendirme anahtarı alma
API anahtarları denemenizi dağıttığınızda, Web hizmeti için oluşturulur. Anahtarları çeşitli konumlardan alabilirsiniz.

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a>Microsoft Azure Machine Learning Web Hizmetleri Portalı'ndan
Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.

Yeni Machine Learning Web hizmeti için API anahtarı almak için:

1. Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Web Hizmetleri** üst menü.
2. Anahtar almak istediğiniz Web hizmeti tıklatın.
3. Üst menüsünde **Tüket**.
4. Kopyalayıp kaydedin **birincil anahtar**.

Klasik Machine Learning Web hizmeti için API anahtarı almak için:

1. Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Klasik Web Hizmetleri** üst menü.
2. Çalıştığınız Web hizmeti tıklatın.
3. Anahtar almak istediğiniz uç noktasına tıklayın.
4. Üst menüsünde **Tüket**.
5. Kopyalayıp kaydedin **birincil anahtar**.

### <a name="classic-web-service"></a>Klasik Web hizmeti
 Klasik Web hizmeti için bir anahtar, Machine Learning Studio veya Azure Klasik portalından da alabilirsiniz.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. Machine Learning Studio'da tıklatın **WEB Hizmetleri** soldaki.
2. Bir Web hizmeti tıklatın. **API anahtarı** açık **PANO** sekmesi.

#### <a name="azure-classic-portal"></a>Klasik Azure portalı
1. Tıklatın **MACHINE LEARNING** soldaki.
2. Web hizmetiniz bulunduğu çalışma alanına tıklayın.
3. Tıklatın **WEB Hizmetleri**.
4. Bir Web hizmeti tıklatın.
5. Bir uç nokta'ı tıklatın. Sağ alt köşesindeki "API anahtarı" çalışmıyor.

## <a id="connect"></a>Bir Machine Learning Web hizmetine bağlanma
HTTP istek ve yanıt destekleyen herhangi bir programlama dili kullanılarak bir Machine Learning Web hizmetine bağlanabilir. C#, Python ve R örnekler bir Machine Learning Web hizmeti Yardım sayfasından görüntüleyebilirsiniz.

**Machine Learning API Yardım** Machine Learning API'si Yardım Web hizmetini dağıttığınızda oluşturulur. Bkz: [Azure Machine Learning izlenecek dağıtımı Web hizmeti](machine-learning-walkthrough-5-publish-web-service.md).
Machine Learning API'si Yardım tahmin Web hizmeti hakkındaki ayrıntıları içerir.

1. Çalıştığınız Web hizmeti tıklatın.
2. API Yardım sayfasında görüntülemek istediğiniz uç noktasına tıklayın.
3. Üst menüsünde **Tüket**.
4. Tıklatın **API Yardım sayfası** istek-yanıt ya da toplu iş yürütme bitiş noktaları altında.

**Machine Learning API görünümüne yeni Web hizmeti için Yardım**

Web Hizmetleri portalı Azure Machine Learning içinde:

1. Tıklatın **WEB Hizmetleri** üst menüsünde.
2. Anahtar almak istediğiniz Web hizmeti tıklatın.

Tıklatın **Tüket** URI'ler isteği Reposonse ve toplu yürütme Hizmetleri ve örnek kod için C#, R ve Python almak için.

Tıklatın **Swagger API'si** Swagger almak için sağlanan URI'ler API çağrısı için belgelerine bağlı.

### <a name="c-sample"></a>C# örnek
Bir Machine Learning Web hizmetine bağlanmak için bir **HttpClient** ScoreData geçirme. ScoreData bir FeatureVector ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir. Machine Learning hizmetine bir API anahtarı ile kimlik doğrulaması.

Machine Learning Web hizmetine bağlanmak için **Microsoft.AspNet.WebApi.Client** NuGet paketi yüklü olmalıdır.

**Microsoft.AspNet.WebApi.Client NuGet Visual Studio yükleme**

1. UCI indirme kümesinden yayımlama: yetişkin 2 sınıfı dataset Web hizmeti.
2. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.
3. Seçin **Install-Package Microsoft.AspNet.WebApi.Client**.

**Kod örneği çalıştırmak için**

1. Yayımla "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, Machine Learning örnek koleksiyonunun bir parçası.
2. Apikey ile yapılan bir Web hizmetinden anahtarla atayın. Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** üstünde.
3. İstek URI'si ile serviceUri atayın.

### <a name="python-sample"></a>Python örneği
Bir Machine Learning Web hizmetine bağlanmak için **urllib2** ScoreData geçirme kitaplığı. ScoreData bir FeatureVector ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir. Machine Learning hizmetine bir API anahtarı ile kimlik doğrulaması.

**Kod örneği çalıştırmak için**

1. Dağıtma "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, Machine Learning örnek koleksiyonunun bir parçası.
2. Apikey ile yapılan bir Web hizmetinden anahtarla atayın. Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** başına bir kısmına bu makalenin.
3. İstek URI'si ile serviceUri atayın.

