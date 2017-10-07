---
title: "aaaSet ayarlama ve kullanma hello Machine Learning önerileri API'si | Microsoft Docs"
description: "Microsoft önerileri Azure Machine Learning ile ilgili SSS ile yerleşik API"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
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
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Machine Learning Öneri API’sini ayarlama ve kullanma hakkında SSS
**ÖNERİLER nedir?**

> [!NOTE]
> Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir. Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
> Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)
> 
> 

Kuruluşlar ve öneriler toocross satış ve yukarı satış ürünleri ve Hizmetleri tootheir müşteriler kullanan işletmeler için Azure Machine Learning önerileri bir Self Servis önerileri altyapısı sağlar. Bu matris factorization kendi çekirdek algoritması kullanan işbirliği filtrelemenin bir uygulamasıdır. Uygulama geliştiricilerinin önerileri REST API'lerini kullanarak erişebilirsiniz. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**ÖNERİLERİ ne yapabilirim?**

ÖNERİLER bir öğe girişi veya öğeleri kümesi alır ve ilgili öneriler listesini döndürür. Örneğin: bir çevrimiçi satıcısı müşterinin bir ürün tıklar. Hello çevrimiçi satıcısında bu ürünü giriş tooRECOMMENDATIONS gönderir, iade ürünlerin listesini alır ve toohello müşteri bu ürünlerin gösterileceği karar verir. Çevrimiçi mağazada toouse önerileri toooptimize istediğiniz veya tooinform, iç hatta satış departmanı veya Arama Merkezi.

**Kullanım sınırlamalar var mı?**

Öneriler kullanım kısıtlamaları aşağıdaki hello içerir:

* Model abonelik başına en yüksek sayısı: 10
* En fazla bir katalog tutabilir öğe sayısı: 100.000
* Merhaba maksimum tutulur kullanım noktaları ~ 5,000,000 sayısıdır. Yeni bir tane karşıya bildirilen veya gereken hello eski silinir.
* 200 MB (örneğin, veri içeri aktar katalog kullanım verileri İçeri Aktar) e-posta ile gönderilen verilerin en büyük boyut:
* İşlemler (TP'ler) etkin değil önerileri modeli derlemesi için saniye başına ~ 2 TP'leri sayısıdır. Etkin bir önerileri modeli yapı too20 TP'leri basılı tutabilirsiniz.

## <a name="purchase-and-billing"></a>Satın Alma ve Fatura
**Nasıl önerileri hello başlatma süresi boyunca maliyeti nedir?**

Öneriler, bir abonelik tabanlı hizmetidir. Şarj aylık işlem hacmi temel alır. Merhaba denetleyebilirsiniz [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) fiyatlandırma bilgileri için Microsoft Azure Marketplace içinde.

**Öneriler sahip ile ilişkili maliyetlerin izlemek ve kullanıcı etkinliğini benim yerime depolamak var mı?**

Merhaba şu anda değil.

**Öneriler ücretsiz deneme sürümü var mı?**

Kısıtlı too10, her ay 000 hareketleri olan ücretsiz bir izleme yoktur.

**Ne zaman ı önerileri için Fatura edilecek?**

Ücretli bir abonelik var olduğu aylık bir ücret herhangi bir aboneliği ' dir. Ücretli bir abonelik satın aldığınızda, hemen Merhaba ilk ücretlendirilen ayın kullanın. Merhaba aboneliği sayfasına (artı geçerli vergileri) hello teklifini ilişkilendirilen hello tutar sizden ücret kesilir. Bu aylık ücret her ay hello aboneliği iptal kadar aynı takvim tarih orijinal satın alma olarak hello üzerinde yapılır. 

**Tooa daha yüksek katmanlı bir hizmet nasıl yükseltme?**

Satın alma veya hello aboneliğinizden güncelleştirme [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) Microsoft Azure Market sayfasında.

Bir abonelik yükseltme yaptığınızda:

* Eski aboneliğinizi kalan işlemler tooyour yeni abonelik eklenmez. 
* Olsa bile tam fiyat hello yeni abonelik için ödeme eski aboneliğinizi kullanılmayan hareketleri.

İşlem tooupgrade bir abonelik:

* Nevigate toohello [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).
* Oturum açmış değilseniz toohello Market oturum açın.
* Merhaba sağ bölmede, tüm hello taşınabileceği listelenir. İçin tooupgrade hello planı için Hello radyo düğmesine tıklayın.
* Tooupgrade istiyorsanız, **Tamam**. Tooupgrade istemiyorsanız tıklayın **iptal**.

**Önemli** faturalama ve kullanım uygulamalarını olduğundan yükseltme yapmadan önce dikkatle okuma hello iletişim kutusu.

**My abonelik tooRecommendations ne zaman sona erecek mi?**

İptal ettiğinizde, aboneliğiniz sona erer. Toocancel isterseniz aboneliklerinizi, yönergeleri izleyerek hello bakın.

**Öneriler Aboneliğimi nasıl iptal edebilirim?**

Aşağıdaki kullanım hello aboneliğinizi adımları toocancel. Geçerli aboneliğinizi Ücretli abonelik ise, aboneliğinizi yürürlükte hello faturalama dönemi geçerli hello sonuna kadar devam eder. Etkili iptal toobe hemen hello varsa, adresinden bize başvurun [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Not** bir fatura döneminde hello bitiş fatura döneminin veya kullanılmayan işlemler için önce iptal ederseniz hiçbir para iadesi verilir.

* Toohello gidin [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).
* Oturum açmış değilseniz toohello Market oturum açın.
* Tıklatın **iptal** toohello sağında hello veri kümesi adı ve durum. Merhaba faturalama dönemi veya işlem sınırınızı geçerli Hello sonuna (hangisi önce gerçekleşirse) ulaşılana kadar bu aboneliği kullanabilirsiniz.

Aboneliğiniz bu nedenle yeni bir abonelik satın alabilirsiniz hemen bir bilet adresindeki dosya toocancel isterseniz [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Öneriler ile çalışmaya başlama
**Öneriler benim için mi?** 

Machine Learning önerileri kuruluşlar ve öneriler toocross satış ve yukarı satış ürünleri veya hizmetleri tootheir müşteriler kullanan işletmeler içindir. Varsa bir müşteri kullanıma yönelik Web sitesi, satış ekibi, bir iç satış ekibi ya da bir çağrı merkezi ve birkaç düzine ürünleri veya hizmetleri kataloğunu teklifi sunuyorsanız, alt çizgi önerileri kullanarak yararlanabilir. 

Önerileri denemeler tasarlanmış toobe oldukça basit olduğunu. temel programlama becerilerinizi Hello geçerli API tabanlı sürümünü gerektirir. Yardıma gereksinim duyarsanız, kimin Web sitenizi geliştirilen hello satıcısına başvurun. Bir iç BT departmanına ya da şirket içi bir geliştirici varsa, sizin için mümkün tooget önerileri toowork olması gerekir. 

**Önerileri ayarı hello önkoşulları nelerdir?**

Öneriler tooyour katalog ilgili olarak kullanıcı seçimlerini günlüğünü olması gerekir. Bu tür bir günlük yoksa ve bir müşteri kullanıma yönelik Web sitesi varsa, Öneriler size kullanıcı etkinliği toplayabilirsiniz. 

Öneriler, ürünleri veya hizmetleri kataloğunu de gerektirir. Merhaba katalog yoksa, öneriler hello gerçek müşteri kullanım verilerini kullanır ve bir katalog biçimlendirebilir. Kapsanan bir katalog kullanıcı işlemleri bir parçası raporlandı değil öğeleri dahil edilmez.

**Nasıl önerileri hello için ilk kez ayarlarım?**

Sonra [abone](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, hello hello API belgelerine kullanması gereken [Azure Machine Learning önerileri - Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello hizmeti.

**API belgelerine nereden bulabilirim?** 

Merhaba API belgelerine olan [Azure Machine Learning önerileri-Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md).

**Seçenekler ne tooupload katalog ve kullanım verileri tooRecommendations sahip mi?**

Katalog ve kullanım verileri yüklemek için iki seçeneğiniz vardır: CRM sisteminize veya diğer günlükler hello verilerini dışarı aktarın ve tooRecommendations yükleyin ya da kullanıcı etkinliklerini izler etiketleri tooyour Web sitesi ekleyebilirsiniz. Merhaba ikinci yöntemi kullanırsanız, Azure'da hello veriler depolanır.

## <a name="maintenance-and-support"></a>Bakım ve Destek
**My veri kümesi ne kadar büyük olabilir?**

Her bir veri kümesi too100, 000 katalog öğeleri yukarı ve Kullanım verilerinin too2048 MB yukarı içerebilir.
Ayrıca, bir abonelik too10 veri kümelerini (modellerin) içerebilir.

**Öneriler için teknik destek nereden alabilirim?**

Teknik Destek hello üzerinde kullanılabilir [Microsoft Azure desteği](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.

**Kullanım koşulları hello nereden bulabilirim?**

[Microsoft Azure Machine Learning hizmet önerileri API koşullarını](https://datamarket.azure.com/dataset/amla/recommendations#terms).

