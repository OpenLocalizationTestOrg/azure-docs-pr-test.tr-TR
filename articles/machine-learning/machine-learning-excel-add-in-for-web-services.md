---
title: "Machine Learning Web Hizmetleri için aaaExcel eklenti | Microsoft Docs"
description: "Nasıl herhangi bir kod yazmak zorunda kalmadan doğrudan Excel'de toouse Azure Machine Learning Web Hizmetleri."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Azure Machine Learning web hizmetleri için Excel Eklentisi
Herhangi bir kod toowrite Hello gerek olmadan Excel kolay toocall web hizmetleri doğrudan kolaylaştırır.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Adımları tooUse hello çalışma kitabı varolan web hizmetinde

1. Açık hello [örnek Excel dosyası](http://aka.ms/amlexcel-sample-2)içeren hello Excel eklentisi ve yolcu hakkındaki verileri hello Titanic.
2. Tıklayarak Hello web hizmeti seçin-"Titanic hayatta bir göstergesi olduğu (Excel Eklentisi örneği) [Sonuç]" Bu örnekte.
   
    ![Web hizmetini seçin][01]
3. Bu toohello sürer **Predıct** bölümü.  Bu çalışma kitabı zaten örnek veri içeriyor, ancak için boş bir çalışma kitabını Excel'de bir hücre seçin ve'ı tıklatın **örnek verileri kullanın**.
4. Üst bilgileri ile Merhaba verileri seçin ve hello giriş verisi aralığı simgesini tıklatın.  Merhaba "Verilerimin üstbilgileri var" onay kutusunun seçili olduğundan emin olun.
5. Altında **çıkış**, burada çıkış toobe, örneğin "H1" Merhaba istediğiniz hello hücre numarasını girin.
6. Tıklatın **tahmin**.
   
    ![Bölüm tahmin etme][02]

Bir web hizmetini dağıtma veya var olan bir Web hizmetini kullanın. Bir web hizmeti dağıtma hakkında daha fazla bilgi için bkz: [gözden geçirme adım 5: hello Azure Machine Learning Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md).

Web hizmetiniz için Hello API anahtarı edinin. Gerçekleştirdiğiniz burada yeni Machine Learning web hizmeti bir Klasik Machine Learning web hizmeti olup yayımlanan Bu eylem bağlıdır.

**Klasik web hizmetini kullanın** 

1. Machine Learning Studio'da hello tıklatın **WEB Hizmetleri** bölümünde hello sol bölmede ve hello web hizmetini seçin.
   
    ![Bir Web hizmeti Studio seçin][04]
2. Merhaba web hizmeti Hello API anahtarını kopyalayın.
   
    ![Studio API anahtarı][05]
3. Merhaba üzerinde **PANO** hello web hizmeti için sekmesini ve ardından hello **istek/yanıt** bağlantı.
4. Merhaba Ara **istek URI'si** bölümü.  Kopyalayın ve hello URL kaydedin.

> [!NOTE]
> Merhaba içine olası toosign sunulmuştur [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) Klasik Machine Learning web hizmeti için portal tooobtain hello API anahtarı.
> 
> 

**Yeni bir web hizmetini kullanın**

1. Merhaba, [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal tıklatın **Web Hizmetleri**, web hizmetinizi seçin. 
2. Tıklatın **tüketen**.
3. Merhaba Ara **temel tüketim bilgileri** bölümü. Kopyalayın ve hello kaydedin **birincil anahtar** ve hello **istek-yanıt** URL.

## <a name="steps-tooadd-a-new-web-service"></a>Adımları tooAdd yeni bir web hizmeti

1. Bir web hizmetini dağıtma veya var olan bir Web hizmetini kullanın. Bir web hizmeti dağıtma hakkında daha fazla bilgi için bkz: [gözden geçirme adım 5: hello Azure Machine Learning Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md).
2. Tıklatın **tüketen**.
3. Merhaba Ara **temel tüketim bilgileri** bölümü. Kopyalayın ve hello kaydedin **birincil anahtar** ve hello **istek-yanıt** URL.
4. Excel'de toohello Git **Web Hizmetleri** bölümüne (hello varsa **Predıct** bölümünde, web hizmetleri hello geri ok toogo toohello listeye tıklayın).
   
    ![TooWeb hizmet seçimi gidin][03]
5. Tıklatın **Web hizmeti Ekle**.
6. Excel eklentisi metin kutusu etiketli hello hello URL yapıştırın **URL**.
7. Yapıştır hello API/birincil anahtarı olarak etiketlenmiş hello metin kutusuna **API anahtarı**.
8. **Ekle**'ye tıklayın.
   
    ![Klasik Web hizmeti URL'sini ve API anahtarı.][06]
9. toouse hello web hizmeti, hello önceki yönergeleri izleyin, "tooUse varolan web hizmeti adımları."

## <a name="sharing-your-workbook"></a>Çalışma kitabınız paylaşımı
Çalışma kitabınız kaydederseniz, eklediğiniz hello web hizmetleri için hello API/birincil anahtar da kaydedilir. Merhaba çalışma kitabını yalnızca güvendiğiniz kişilerle paylaşması gerekir anlamına gelir.

Merhaba Açıklama bölümüne aşağıdaki veya üzerinde herhangi bir sorunuz isteyin bizim [Forumu](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
