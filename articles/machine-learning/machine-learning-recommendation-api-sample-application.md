---
title: "Merhaba Machine Learning önerileri API'si aaaCommon işlemlerinde | Microsoft Docs"
description: "Azure ML öneri örnek uygulama"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Öneri API’si Örnek Uygulama Kılavuzu
> [!NOTE]
> Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir. Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
> Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Amaç
Bu belge hello hello kullanımı aracılığıyla Azure Machine Learning önerileri API gösterir. bir [örnek uygulama](https://code.msdn.microsoft.com/Recommendations-144df403).

Bu uygulamanın hedeflenen tooinclude tam işlevsel değildir ve tüm hello API'leri kullanmaz. Merhaba Machine Learning önerisi hizmeti ile tooplay ilk istediğinizde bazı ortak işlemleri tooperform gösterir. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Giriş tooMachine öğrenme önerisi hizmeti
Veri aşağıdaki hello üzerinde temel alan bir öneri modeli derlerken önerileri hello Machine Learning önerisi hizmeti aracılığıyla etkinleştirilir:

* Bir katalog olarak da bilinen toorecommend istediğiniz hello öğelerinin bir depo
* Kullanıcı veya (Bu hello örnek uygulaması parçası olarak değil, veri alım aracılığıyla zaman içinde elde edilebilecek) oturum başına öğe Hello kullanımını temsil eden veri

Bir öneri model oluşturulduktan sonra bir kullanıcı, ilginizi çekiyor toopredict öğeleri kullanabilirsiniz tooa göre öğeleri (veya tek bir öğe) kümesini hello kullanıcı seçer.

tooenable Merhaba önceki senaryoda, hello aşağıdakileri Machine Learning önerisi hizmeti hello yapın:

* Bir model oluşturmak: Bu hello verileri (katalog ve kullanım) ve hello tahmin modellerini tutan, mantıksal bir kapsayıcısıdır. Her model kapsayıcı oluşturulduğunda, ayrılmış benzersiz bir kimlik tanımlanır. Bu kimliği hello model kimliği olarak adlandırılır ve hello API'leri çoğu tarafından kullanılır. 
* Toocatalog karşıya: model kapsayıcı oluşturulduğunda, tooit bir katalog ilişkilendirebilirsiniz.

**Not**: model oluşturma ve tooa katalog karşıya yükleme genellikle gerçekleştirilir kez hello modeli yaşam döngüsü için.

* Kullanım karşıya yükleme: Bu kullanım verileri toohello model kapsayıcı ekler.
* Bir öneri model oluşturma: yeterli veri aldıktan sonra hello öneri modeli oluşturabilirsiniz. Bu işlem hello üst Machine Learning algoritmaları toocreate bir öneri modeli kullanır. Her benzersiz bir kimlik ile ilişkili bir yapıdır Bazı API'leri hello işlevselliği için gerekli olduğundan tookeep bu kimliği kaydını gerekir.
* Oluşturma işlemi İzleyicisi Merhaba: zaman uyumsuz bir işlem öneri modeli yapıdır ve bu verileri (katalog ve kullanım) hello miktarını bağlı olarak birkaç dakika tooseveral saat alabilir ve yapı parametreleri hello. Bu nedenle, toomonitor hello yapı gerekir. Yalnızca ilişkili derleme başarıyla tamamlarsa bir öneri modeli oluşturulur.
* (İsteğe bağlı) Bir active öneri modeli oluşturma seçin: Bu adım yalnızca, model kapsayıcısında yerleşik birden fazla öneri model varsa gereklidir. Merhaba etkin öneri modeli gösteren olmadan herhangi bir istek tooget önerimiz hello sistem toohello varsayılan etkin yapı tarafından otomatik olarak yönlendirildiği. 

**Not**: üretim hazır bir etkin öneri modeldir ve üretim iş yükü için oluşturulmuştur. Bu, (hazırlama de denir) bir test benzeri ortamda kalır bir etkin olmayan öneri modelinden farklıdır.

* Öneriler alın: bir öneri modeli aldıktan sonra tek bir öğe veya seçtiğiniz öğeler listesi için öneriler tetikleyebilir. 

Belirli bir süre alma öneri genellikle çağırır. Bu süre boyunca kullanım verilerini toohello bu veri toohello belirtilen model kapsayıcısı ekler Machine Learning öneri sistem yeniden yönlendirebilirsiniz. Yeterli kullanım verilerini sahip olduğunuzda, hello ek kullanım verilerini içeren yeni bir öneri modeli oluşturabilirsiniz. 

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2013 veya üzeri
* İnternet erişimi 
* Abonelik toohello önerileri API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning örnek uygulama çözümü
Bu çözüm hello kaynak kodu, örnek kullanım, katalog dosyası ve derleme için gerekli olan yönergeleri toodownload hello paketleri içerir.

## <a name="hello-apis-used"></a>Merhaba kullanılan API'leri
Merhaba uygulaması bir alt kümesini kullanılabilir API'ler aracılığıyla Machine Learning öneri işlevi kullanır. Merhaba hello uygulamada aşağıdaki API gösterilmiştir:

* Model oluşturma: mantıksal kapsayıcısı toohold veri ve öneri modelleri oluşturun. Model bir ada göre tanımlanır ve hello ile birden fazla model oluşturulamıyor aynı adı.
* Katalog dosyasını karşıya yükleyin: tooupload katalog verilerini kullanın.
* Kullanım dosyasını karşıya: tooupload kullanım verileri kullanın.
* Yapı tetiklemek: toocreate bir öneri modeli kullanın.
* İzleme yapı yürütme: toomonitor hello bir öneri modeli yapı durumunu kullanın.
* Öneri için yerleşik bir modeli seçin: tooindicate hangi öneri modeli toouse varsayılan olarak belirli bir model kapsayıcı için kullanın. Bu adım, yalnızca birden fazla öneri modeline sahiptir ve etkin olmayan yapı hello etkin öneri model olarak tooactivate istiyorsanız gereklidir.
* Öneri alın: öğeleri tek öğe veya öğeleri kümesi verilen tooa göre önerilen tooretrieve kullanın. 

Merhaba API'leri tam bir açıklaması için lütfen hello Microsoft Azure Market belgelerine bakın. 

**Not**: bir model çeşitli yapılar Zamanla (aynı anda değil) olabilir. Her yapı hello ile aynı ya da güncelleştirilmiş oluşturulan katalog ve ek kullanım verileri.

## <a name="common-pitfalls"></a>Ortak Tuzaklar
* Tooprovide kullanıcı adınızı ve Microsoft Azure Market birincil hesap anahtar toorun hello örnek uygulamanız gerekir.
* Çalışan hello örnek uygulaması art arda başarısız olur. Merhaba uygulama akışını oluşturma, karşıya yükleme, hello İzleyicisi oluşturma ve önceden tanımlanmış bir modelden öneriler alınırken içerir; Bu nedenle, hello model adı çağrılarını arasında değişiklik yapmazsanız, ardışık yürütme sırasında başarısız olur.
* Öneriler olmadan veri döndürebilir. Merhaba örnek uygulaması çok küçük bir katalog ve kullanım dosyasını kullanır. Bu nedenle, bazı öğeler hello Kataloğu'ndan önerilen öğe olacaktır.

## <a name="disclaimer"></a>Bildirim
Merhaba örnek uygulaması, bir üretim ortamında çalıştırmak hedeflenen toobe değil. Başlangıç Kataloğu'nda sağlanan hello verileri çok küçük ve anlamlı öneri modeli sağlamaz. Merhaba veri bir örnek sağlanır. 

