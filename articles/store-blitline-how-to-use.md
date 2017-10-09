---
title: "Görüntü işleme - aaaHow toouse Blitline Azure özellik Kılavuzu"
description: "Nasıl toouse hello Blitline hizmet tooprocess görüntüleri Azure uygulamadaki öğrenin."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Nasıl toouse Blitline Azure ve Azure Storage ile
Bu kılavuz anlatılmıştır nasıl tooaccess Blitline Hizmetleri ve nasıl toosubmit tooBlitline işler.

## <a name="what-is-blitline"></a>Blitline nedir?
Blitline kurumsal düzey görüntü işleme bir kısmı toobuild mal olacağını hello fiyat sağlayan hizmet işleme bulut tabanlı bir görüntü olduğundan bunu kendiniz.

Merhaba olgu görüntü işleme tekrar tekrar, genellikle hello başından başlayarak her Web sitesi için gelen yeniden gerçekleştirildi emin olur. Biz bunları milyon kez çok oluşturuncaya çünkü Biz bu unutmayın. Bir belki de, zaman olduğunu karar gün biz yalnızca herkes için bunu. Biliyoruz nasıl toodo, hızlı ve verimli bir şekilde ve kaydetme herkesin çalışır hello sırada toodo.

Daha fazla bilgi için bkz: [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>Ne Blitline değil...
tooclarify ne Blitline ileriye doğru taşımadan önce yapmaz genellikle daha kolay tooidentify olduğu için ne Blitline yararlıdır.

* Blitline HTML pencere öğeleri tooupload görüntüleri yok. Genel olarak veya kısıtlı izinleri Blitline tooreach için kullanılabilir olan kullanılabilir olması gerekir.
* Blitline yapmaz dinamik görüntü işleme, Aviary.com gibi
* Blitline görüntüyü karşıya kabul etmez, görüntüleri tooBlitline doğrudan gönderemezsiniz. Bunları tooAzure depolama veya Blitline destekleyen diğer yerler gönderme ve toogo nereden bunları Blitline söyleyin.
* Blitline yüksek düzeyde paralel ve herhangi bir zaman uyumlu işlem yapmaz. Başka bir deyişle vermelidir bize bir postback_url ve biz, biz tamamladığınızda söyleyebilir işleniyor.

## <a name="create-a-blitline-account"></a>Blitline hesabı oluşturma
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Nasıl toocreate Blitline işi
Blitline tootake görüntüdeki istediğiniz JSON toodefine hello eylemleri kullanır. Bu JSON birkaç basit alanlarının oluşur.

Merhaba basit örneği aşağıdaki gibidir:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Burada "src" görüntü sürer JSON sahibiz "... boys.jpeg" ve bu görüntüyü too240x140 yeniden boyutlandırın.

Merhaba uygulama kimliği olan şey içinde bulabilirsiniz, **bağlantı bilgisi** veya **Yönet** Azure sekmesinde. Üzerinde Blitline toorun işleri sağlar, gizli tanımlayıcısıdır.

Merhaba "Kaydet" parametresi biz işledikten sonra tooput hello görüntü istediğiniz hakkında bilgi tanımlar. Önemsiz bu durumda, biz tanımlanan henüz. Konum tanımlanmışsa Blitline, yerel olarak (ve geçici olarak) depolar benzersiz bulut konumda. Merhaba Blitline yaptığınızda, hello JSON konumdan Blitline tarafından döndürülen mümkün tooget olacaktır. Merhaba "Görüntü" tanımlayıcısı gereklidir ve tooidentify görüntü bu belirli kaydedildiğinde tooyou döndürülür.

Merhaba hakkında daha fazla bilgi bulabilirsiniz *işlevleri* burada destekliyoruz: <http://www.blitline.com/docs/functions>

Merhaba hakkındaki belgeler işi seçenekleri burada bulabilirsiniz: <http://www.blitline.com/docs/api>

JSON olduktan sonra tek toodo ihtiyacınız olan **POST** , çok`http://api.blitline.com/job`

Şunun gibi JSON geri alırsınız:

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


Bu, Blitline isteği aldı, onu bir işleme sırasına getirdi ve onu tamamlandığında hello görüntü adresinde bildirir: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_uygulama\_kimliği /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Nasıl toosave bir görüntü tooyour Azure depolama hesabı
Bir Azure depolama hesabınız varsa, kolayca Blitline itme işlenen hello görüntüleri Azure kapsayıcıya sahip olabilir. Bir "azure_destination" ekleyerek hello konumu ve Blitline toopush izinlerini tanımlayın.

Örnek aşağıda verilmiştir:

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


Merhaba CAPITALIZED değerleri kendi değerlerinizle doldurarak, bu JSON toohttp://api.blitline.com/job gönderebilir ve hello "src" görüntü Bulanıklaştırma filtresi ile işlenir ve tooyou Azure hedef gönderilir.

### <a name="please-note"></a>Lütfen unutmayın:
Merhaba SAS hello dosya hello hedef dosya adını dahil olmak üzere hello tüm SAS URL'si, içermelidir.

Örnek:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


Ayrıca, Blitline'nın Azure Storage belgeleri en son sürümünü hello okuyabilirsiniz [burada](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Sonraki Adımlar
Bizim diğer özellikler hakkında blitline.com tooread ziyaret edin:

* Blitline API uç noktası belgeleri <http://www.blitline.com/docs/api>
* Blitline API işlevleri <http://www.blitline.com/docs/functions>
* Blitline API örnekleri <http://www.blitline.com/docs/examples>
* Üçüncü Nuget kitaplığı Kısım <http://nuget.org/packages/Blitline.Net>

