---
title: "aaaCreate bir dışa aktarma işi için Azure içeri/dışarı aktarma | Microsoft Docs"
description: "Nasıl toocreate bir dışa aktarma işi Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti hakkında bilgi edinin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Hello Azure içeri/dışarı aktarma hizmeti için bir dışa aktarma işi oluşturma
Bir dışarı aktarma işinin hello REST API kullanarak hello Microsoft Azure içeri/dışarı aktarma hizmeti oluşturma hello aşağıdaki adımları içerir:

-   Merhaba seçerek tooexport BLOB '.

-   Bir sevkiyat konum alma.

-   Merhaba dışarı aktarma işini oluşturuluyor.

-   Boş sürücüleri tooMicrosoft desteklenen taşıyıcı hizmeti üzerinden aktarma.

-   Merhaba dışarı aktarma işini hello paket bilgilerle güncelleştiriliyor.

-   Microsoft'tan geri alma hello sürücüler.

 Bkz: [hello Windows Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanarak](storage-import-export-service.md) genel bir bakış hello içeri/dışarı aktarma hizmeti ve gösteren bir öğretici için nasıl toouse hello [Azure portal](https://portal.azure.com/) toocreate alma yönetmek ve işleri dışarı aktarma.

## <a name="selecting-blobs-tooexport"></a>BLOB'ları tooexport seçme
 bir dışarı aktarma işinin toocreate, tooprovide BLOB storage hesabınızdan tooexport istediğiniz listesini gerekir. Birkaç yolu vardır tooselect BLOB'ların verilen toobe:

-   Tek bir blob ve tüm alt anlık görüntü göreli blob yolu tooselect kullanabilirsiniz.

-   Kendi anlık görüntüleri hariç olmak üzere tek bir blob göreli blob yolu tooselect kullanabilirsiniz.

-   Göreli blob yolu ve bir anlık görüntü saati tooselect bir anlık görüntüsü kullanabilirsiniz.

-   Bir blob öneki tooselect öneki verilen hello ile tüm BLOB'ları ve anlık görüntüleri kullanabilirsiniz.

-   Tüm BLOB'ları ve anlık görüntüleri hello depolama hesabındaki dışarı aktarabilirsiniz.

 Merhaba BLOB'ların tooexport belirtme hakkında daha fazla bilgi için bkz: [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi.

## <a name="obtaining-your-shipping-location"></a>Sevkiyat Konumunuz alma
Bir dışarı aktarma işinin oluşturmadan önce tooobtain sevkiyat konum adı ve adres tarafından arama hello ihtiyacınız [alma konumu](https://portal.azure.com) veya [listesi konumları](/rest/api/storageimportexport/listlocations) işlemi. `List Locations`konumlar ve posta adresleri listesi döndürür. Liste döndürülen hello bir konum seçin ve sabit sürücüler toothat adresinizi sevk. Merhaba de kullanabilirsiniz `Get Location` belirli bir konuma adresini doğrudan aktarma işlemi tooobtain hello.

Tooobtain hello sevkiyat konumu Hello adımları izleyin:

-   Merhaba hello konumun depolama hesabınızın adını belirleyin. Bu değer hello altında bulunabilir **konumu** hello depolama hesabının alanını **Pano** hello Klasik portal ya da hello Hizmet Yönetimi API işlemi kullanarak için sorgulanan içinde [Al Depolama hesabı özellikleri](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Kullanılabilir tooprocess olan hello konum bu depolama hesabı tarafından arama hello almak `Get Location` işlemi.

-   Merhaba, `AlternateLocations` özelliği hello konumunun hello konumu kendisini içeren sonra kesebilirsiniz toouse olduğu bu konumu. Aksi takdirde hello çağrı `Get Location` hello alternatif konumlar biriyle yeniden işlemi. Merhaba özgün konumuna bakım için geçici olarak kapalı.

## <a name="creating-hello-export-job"></a>Merhaba dışa aktarma işi oluşturma
 toocreate hello dışarı aktarma işini, çağrı hello [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi. Aşağıdaki bilgilerle tooprovide hello gerekir:

-   Merhaba işi için bir ad.

-   Merhaba depolama hesabı adı.

-   Merhaba sevkiyat Hello önceki adımda elde konum adı.

-   İş türü (verme).

-   Merhaba dönüş adresi Hello dışa aktarma işi tamamlandıktan sonra hello sürücüleri burada gönderilmelidir.

-   Merhaba BLOB'lar (veya blob önekler) listesini toobe verildi.

## <a name="shipping-your-drives"></a>Sürücülerinizin aktarma
 Ardından, hello Azure içeri/dışarı aktarma aracı toodetermine hello dışarı toobe seçtiğiniz hello BLOB'ları üzerinde temel toosend, gereksinim duyduğunuz sürücü sayısı kullanın ve disk boyutu hello. Merhaba bkz [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md) Ayrıntılar için.

 Tek bir paket hello sürücü paketini ve toohello sevk hello elde edilen adresi önceki adım. Merhaba sonraki adımınız, paket sayısı izleme hello unutmayın.

> [!NOTE]
>  Sürücülerinizin paketiniz için bir izleme numarası sağlayacak bir desteklenen taşıyıcı hizmeti aracılığıyla hazırlamalısınız.

## <a name="updating-hello-export-job-with-your-package-information"></a>Paket bilgilerinizle Hello dışarı aktarma işini güncelleştiriliyor
 İzleme numaranızın aldıktan sonra hello çağrısı [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlem tooupdated hello taşıyıcı adı ve izleme hello proje numarası. İsteğe bağlı olarak, sürücüler, hello dönüş adresi ve hello sevkiyat tarihi de hello sayısını belirtebilirsiniz.

## <a name="receiving-hello-package"></a>Merhaba paket alma
 Dışarı aktarma işini işlendikten sonra sürücülerinizin tooyou şifrelenmiş verilerinizi ile döndürülür. Her çağırma hello hello sürücüleriyle hello BitLocker anahtarını alabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi. Ardından hello sürücü hello anahtarını kullanarak kilidini açabilirsiniz. Merhaba sürücü bildirim dosyası her sürücüde hello özgün blob adresi yanı sıra hello sürücü dosyalarını her dosya için hello listesini içerir.

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma](storage-import-export-using-the-rest-api.md)
