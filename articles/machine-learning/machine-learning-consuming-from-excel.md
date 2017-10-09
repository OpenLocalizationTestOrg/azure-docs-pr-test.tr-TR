---
title: bir Machine Learning Web hizmeti Excel'den aaaConsume | Microsoft Docs
description: Bir Azure Machine Learning Web hizmeti Excel'den kullanma
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Bir Azure Machine Learning Web Hizmetini Excel’den kullanma
 Azure Machine Learning Studio'da herhangi bir kod toowrite Hello gerek olmadan kolayca toocall web hizmetleri doğrudan Excel'den kolaylaştırır.

Excel 2013 (veya üstü) veya Excel Online'da kullandığınız sonra hello Excel kullanmanızı öneririz [Excel eklentisi](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Adımlar
Bir web hizmeti yayımlayın. [Bu sayfayı](machine-learning-walkthrough-5-publish-web-service.md) açıklar nasıl toodo onu. Şu anda hello Excel çalışma kitabı özelliği yalnızca tek bir çıktı (diğer bir deyişle, tek bir Puanlama etiketi) sahip istek/yanıt Hizmetleri için desteklenir. 

Bir web hizmeti olduktan sonra üzerinde hello tıklatın **WEB Hizmetleri** bölümünde hello studio hello sol tarafta ve ardından hello web hizmeti tooconsume Excel'den seçin.

**Klasik Web hizmeti**

1. Merhaba üzerinde **PANO** hello web hizmetidir hello için bir satır sekmesi **istek/yanıt** hizmet. Bu hizmet tek bir çıktı olsaydı hello görmelisiniz **karşıdan Excel çalışma kitabı** o satırdaki bağlantı.
   
    ![][1]
2. Tıklayın **karşıdan Excel çalışma kitabı**.

**Yeni Web hizmeti**

1. Hello Azure Machine Learning Web hizmeti Portalı'nda seçin **Tüket**.
2. Merhaba Tüket sayfasında, hello **Web hizmeti tüketim seçenekleri** bölümünde, hello Excel simgesine tıklayın.

**Merhaba çalışma kitabı kullanma**

1. Açık hello çalışma kitabı.
2. Bir güvenlik uyarısı görüntülenmez; Merhaba üzerinde tıklatın **düzenlemeyi etkinleştir** düğmesi.
   
    ![][2]
3. Bir güvenlik uyarısı görüntülenmez. Tıklatın hello üzerinde **içeriği etkinleştir** düğmesini toorun makroları, elektronik tablo.
   
    ![][3]
4. Makrolar etkinleştirildikten sonra bir tablo oluşturulur. Mavi olan sütunlarda gerekli hello giriş olarak RRS web hizmeti veya **parametreleri**. Not hello RR hizmet hello çıktısını **ÖNGÖRÜLEN değerleri** yeşil. Belirli bir satır için tüm sütunları dolduğunda, hello çalışma kitabı otomatik olarak API Puanlama hello çağıran ve sonuçları skoru hello görüntüler.
   
    ![][4]
5. tooscore birden fazla bir satır, veriler ve hello ile dolgu hello ikinci satır değerleri üretilen tahmin. Aynı anda birden çok satır bile yapıştırabilirsiniz.

Hello Excel özelliklerinden (grafikleri, güç harita, koşullu biçimlendirme, vs.) herhangi birini tahmin hello ile kullanabileceğiniz değerleri toohelp hello verileri görselleştirin.    

## <a name="sharing-your-workbook"></a>Çalışma kitabınız paylaşımı
Merhaba makroları toowork için API anahtarınıza hello elektronik tablonun parçası olması gerekir. Yalnızca varlıklar/güvenilir kişiler ile Merhaba çalışma kitabı paylaşmalıdır anlamına gelir.

## <a name="automatic-updates"></a>Otomatik güncelleştirmeler
Bir RRS çağrı bu iki durumlarda yapılmıştır:

1. Merhaba ilk kez bir satır var içerik tümünde kendi **parametreleri**
2. Hello hiçbirini kurduğunda **parametreleri** tümüne sahip olan bir satır değişiklikleri kendi **parametreleri** girildi.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
