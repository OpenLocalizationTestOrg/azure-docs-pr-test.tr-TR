---
title: "Ayarlama ve Machine Learning önerileri API'si kullanma | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Machine Learning Öneri API’sini ayarlama ve kullanma hakkında SSS
**ÖNERİLER nedir?**

> [!NOTE]
> Öneriler API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir. Öneriler Bilişsel hizmet bu hizmeti koyacağınız ve tüm yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
> Daha fazla bilgi edinmek [yeni Bilişsel Service'e geçirme](http://aka.ms/recomigrate)
> 
> 

Kuruluşlar ve çapraz satış için öneriler ve yukarı satış ürünleri ve Hizmetleri müşterilerine kullanan işletmeler için Azure Machine Learning önerileri bir Self Servis önerileri altyapısı sağlar. Bu matris factorization kendi çekirdek algoritması kullanan işbirliği filtrelemenin bir uygulamasıdır. Uygulama geliştiricilerinin önerileri REST API'lerini kullanarak erişebilirsiniz. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**ÖNERİLERİ ne yapabilirim?**

ÖNERİLER bir öğe girişi veya öğeleri kümesi alır ve ilgili öneriler listesini döndürür. Örneğin: bir çevrimiçi satıcısı müşterinin bir ürün tıklar. Çevrimiçi satıcısında önerileri girdi olarak bu ürünü gönderir, ürünlerin listesini iade alır ve bu ürünlerin müşteriye gösterileceği karar verir. Çevrimiçi mağazada en iyi duruma getirme veya bile, iç bildirmek için öneriler kullanmak isteyebilirsiniz satış departmanı veya Arama Merkezi.

**Kullanım sınırlamalar var mı?**

Önerileri şu kullanım sınırlamalara sahiptir:

* Model abonelik başına en yüksek sayısı: 10
* En fazla bir katalog tutabilir öğe sayısı: 100.000
* En fazla tutulur kullanım noktaları ~ 5,000,000 sayısıdır. Yeni bir tane karşıya bildirilen veya gereken eski silinir.
* 200 MB (örneğin, veri içeri aktar katalog kullanım verileri İçeri Aktar) e-posta ile gönderilen verilerin en büyük boyut:
* İşlemler (TP'ler) etkin değil önerileri modeli derlemesi için saniye başına ~ 2 TP'leri sayısıdır. Etkin bir önerileri modeli yapı en fazla 20 TP'leri basılı tutabilirsiniz.

## <a name="purchase-and-billing"></a>Satın Alma ve Fatura
**Ne kadar önerileri maliyet başlatma süresi boyunca mu?**

Öneriler, bir abonelik tabanlı hizmetidir. Şarj aylık işlem hacmi temel alır. Kontrol edebilirsiniz [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) fiyatlandırma bilgileri için Microsoft Azure Marketplace içinde.

**Öneriler sahip ile ilişkili maliyetlerin izlemek ve kullanıcı etkinliğini benim yerime depolamak var mı?**

Değil şu anda.

**Öneriler ücretsiz deneme sürümü var mı?**

Aylık 10.000 işlemleri için kısıtlı olan ücretsiz bir izleme yoktur.

**Ne zaman ı önerileri için Fatura edilecek?**

Ücretli bir abonelik var olduğu aylık bir ücret herhangi bir aboneliği ' dir. Ücretli bir abonelik satın aldığınızda, ilk ayın kullanımı için hemen sizden ücret kesilir. Abonelik sayfası (artı geçerli vergileri) teklifini ilişkilendirilen tutar sizden ücret kesilir. Aboneliğini iptal kadar her ay orijinal satın alma aynı takvim tarihte bu aylık ücret yapılır. 

**Daha yüksek bir katman hizmet nasıl yükseltme?**

Satın alma veya aboneliğinizden güncelleştirme [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations) Microsoft Azure Market sayfasında.

Bir abonelik yükseltme yaptığınızda:

* Eski aboneliğinizi kalan işlemler yeni aboneliğinizi eklenmez. 
* Olsa bile yeni abonelik için tam fiyat ödeme eski aboneliğinizi kullanılmayan hareketleri.

Bir abonelik yükseltme işlemi:

* İçin Nevigate [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).
* Oturum açmış değilseniz Market'te oturum açın.
* Sağ bölmede, kullanılabilen tüm planlarla listelenir. Yükseltmek istediğiniz planı için radyo düğmesine tıklayın.
* Yükseltmek istiyorsanız, tıklatın **Tamam**. Yükseltmeye istemiyorsanız tıklayın **iptal**.

**Önemli** iletişim kutusu faturalama ve kullanım uygulamalarını olduğundan yükseltme yapmadan önce dikkatle okuyun.

**Ne zaman Aboneliğimi önerileri sona erecek mi?**

İptal ettiğinizde, aboneliğiniz sona erer. Aboneliklerinizi iptal etmek istiyorsanız, aşağıdaki yönergelere bakın.

**Öneriler Aboneliğimi nasıl iptal edebilirim?**

Aboneliğinizi iptal etmek için aşağıdaki adımları kullanın. Geçerli aboneliğinizi Ücretli abonelik ise, aboneliğinizi yürürlükte geçerli fatura dönemi sonuna kadar devam eder. İptal hemen etkin olması gerekiyorsa, adresinden bize başvurun [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Not** bir fatura döneminde fatura döneminin veya kullanılmayan işlemler için bitmeden önce iptal ederseniz hiçbir para iadesi verilir.

* Gidin [sayfa teklif](https://datamarket.azure.com/dataset/amla/recommendations).
* Oturum açmış değilseniz Market'te oturum açın.
* Tıklatın **iptal** veri kümesi adı ve durum sağındaki. Bu abonelik geçerli fatura dönemi sonuna kadar kullanabilir veya (hangisi önce gerçekleşirse), işlem sınırına ulaştı.

Bu nedenle yeni bir abonelik satın alabilirsiniz hemen aboneliğinizi iptal etmek istiyorsanız, bir bilet adresindeki dosya [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Öneriler ile çalışmaya başlama
**Öneriler benim için mi?** 

Machine Learning önerileri organizasyonlar ve işletmeler arası satış önerileri ve yukarı satış ürünleri veya hizmetleri müşterilerine Bel içindir. Varsa bir müşteri kullanıma yönelik Web sitesi, satış ekibi, bir iç satış ekibi ya da bir çağrı merkezi ve birkaç düzine ürünleri veya hizmetleri kataloğunu teklifi sunuyorsanız, alt çizgi önerileri kullanarak yararlanabilir. 

Önerileri denemeler oldukça basit olacak şekilde tasarlanmıştır. Geçerli API tabanlı sürümünü temel programlama becerileri gerektirir. Yardıma gereksinim duyarsanız, kimin Web sitenizi geliştirilen satıcısına başvurun. Bir iç BT departmanına ya da şirket içi bir geliştirici varsa, bunlar işinize önerileri almak mümkün olması gerekir. 

**Önerileri ayarı önkoşulları nelerdir?**

Öneriler kataloğunuza ilgili olarak kullanıcı seçimlerini günlüğünü olması gerekir. Bu tür bir günlük yoksa ve bir müşteri kullanıma yönelik Web sitesi varsa, Öneriler size kullanıcı etkinliği toplayabilirsiniz. 

Öneriler, ürünleri veya hizmetleri kataloğunu de gerektirir. Katalog yoksa, öneriler gerçek müşteri kullanım verilerini kullanır ve bir katalog biçimlendirebilir. Kapsanan bir katalog kullanıcı işlemleri bir parçası raporlandı değil öğeleri dahil edilmez.

**İlk kez önerileri nasıl ayarlarım?**

Sonra [abone](https://datamarket.azure.com/dataset/amla/recommendations) önerileri için API belgelerine kullanmalısınız [Azure Machine Learning önerileri - Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md) hizmeti kurmak için.

**API belgelerine nereden bulabilirim?** 

API belgeleri [Azure Machine Learning önerileri-Hızlı Başlangıç Kılavuzu](machine-learning-recommendation-api-quick-start-guide.md).

**Öneriler için katalog ve kullanım verileri yüklemek hangi seçenekleri var mı?**

Katalog ve kullanım verileri yüklemek için iki seçeneğiniz vardır: verileri, CRM sisteminize veya diğer günlükler verin ve öneriler için yükleyin ya da kullanıcı etkinliklerini izler, Web sitenizin etiket ekleyebilirsiniz. İkinci yöntemi kullanırsanız, verileri Azure içinde depolanır.

## <a name="maintenance-and-support"></a>Bakım ve Destek
**My veri kümesi ne kadar büyük olabilir?**

Her bir veri kümesi en fazla 100.000 katalog öğelerini içeren ve en çok kullanım verilerinin 2048 MB.
Ayrıca, bir abonelik en fazla 10 veri kümeleri (modellerin) içerebilir.

**Öneriler için teknik destek nereden alabilirim?**

Teknik Destek edinilebilir [Microsoft Azure desteği](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.

**Kullanım koşulları nereden bulabilirim?**

[Microsoft Azure Machine Learning hizmet önerileri API koşullarını](https://datamarket.azure.com/dataset/amla/recommendations#terms).

