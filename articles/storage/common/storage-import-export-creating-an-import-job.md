---
title: "aaaCreate içe aktarma işi için Azure içeri/dışarı aktarma | Microsoft Docs"
description: "Bilgi nasıl toocreate hello Microsoft Azure içeri/dışarı aktarma hizmeti için bir alma."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Hello Azure içeri/dışarı aktarma hizmeti için bir içeri aktarma işi oluşturma

İçe aktarma işi hello REST API kullanarak hello Microsoft Azure içeri/dışarı aktarma hizmeti oluşturma hello aşağıdaki adımları içerir:

-   Hello Azure içeri/dışarı aktarma aracı olan sürücüleri hazırlanıyor.

-   Başlangıç konumu toowhich tooship hello sürücü alma.

-   Merhaba alma işi oluşturuluyor.

-   Merhaba sevkiyat tooMicrosoft desteklenen taşıyıcı hizmeti sürücüleri.

-   Merhaba içe aktarma işi ile Sevkiyat ayrıntıları hello güncelleştiriliyor.

 Bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanarak](storage-import-export-service.md) genel bir bakış hello içeri/dışarı aktarma hizmeti ve gösteren bir öğretici için nasıl toouse hello [Azure portal](https://portal.azure.com/) toocreate alma yönetmek ve işleri dışarı aktarma.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Hello Azure içeri/dışarı aktarma aracı olan sürücüleri hazırlama

Merhaba adımları tooprepare sürücüler içeri aktarma işi için olan hello aynı olup olmadığını oluşturduğunuz jobvia hello portal hello veya REST API aracılığıyla hello.

Sürücü hazırlama kısa bir genel bakış aşağıdadır. Toohello başvuran [Azure alma ExportTool başvurusu](storage-import-export-tool-how-to-v1.md) tam yönergeler için. Hello Azure içeri/dışarı aktarma aracı indirebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkID=301900).

Sürücünüz hazırlanıyor içerir:

-   Merhaba veri toobe alınan tanımlayıcı.

-   Windows Azure depolama alanında Hello hedef BLOB'ları tanımlama.

-   Hello Azure içeri/dışarı aktarma aracı toocopy veri tooone ya da daha fazla sabit disk sürücüler kullanıyor.

 hazırlandığını gibi hello Azure içeri/dışarı aktarma aracı ayrıca her hello sürücüleri için bir bildirim dosyası oluşturur. Bildirim dosyası içerir:

-   Karşıya yükleme ve bu dosyaları tooblobs hello eşlemelerini yönelik tüm hello dosyaları numaralandırması.

-   Her bir dosyanın parçalarını hello sağlama.

-   Her bir blob ile Merhaba meta verileri ve özellikleri tooassociate hakkında bilgi sağlar.

-   Karşıya yüklenen bir blob hello varsa bir hello eylem tootake listeleme aynı hello kapsayıcısındaki bir blob olarak adlandırın. Olası seçenekler: a) hello blob ile Merhaba dosyanın üzerine, (b) hello mevcut blob ve hello dosyayı karşıya yüklemeyi atlayın tutmak, c) toohello sonek başka dosyalarla çakışmadığından emin Ekle.

## <a name="obtaining-your-shipping-location"></a>Sevkiyat Konumunuz alma

İçe aktarma işi oluşturmadan önce tooobtain sevkiyat konum adı ve adres tarafından arama hello ihtiyacınız [listesi konumları](/rest/api/storageimportexport/listlocations) işlemi. `List Locations`konumlar ve posta adresleri listesi döndürür. Liste döndürülen hello bir konum seçin ve sabit sürücüler toothat adresinizi sevk. Merhaba de kullanabilirsiniz `Get Location` belirli bir konuma adresini doğrudan aktarma işlemi tooobtain hello.

 Tooobtain hello sevkiyat konumu Hello adımları izleyin:

-   Merhaba hello konumun depolama hesabınızın adını belirleyin. Bu değer hello altında bulunabilir **konumu** hello depolama hesabının alanını **Pano** hello Azure portal veya hello Hizmet Yönetimi API işlemi kullanarak için sorgulanan içinde [depolama Al Hesap özellikleri](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Kullanılabilir tooprocess hello konuma göre arama hello bu depolama hesabı almak `Get Location` işlemi.

-   Merhaba, `AlternateLocations` özelliği hello konumunun hello konumu kendisini içeren sonra kesebilirsiniz toouse olduğu bu konumu. Aksi takdirde hello çağrı `Get Location` hello alternatif konumlar biriyle yeniden işlemi. Merhaba özgün konumuna bakım için geçici olarak kapalı.

## <a name="creating-hello-import-job"></a>Merhaba alma işi oluşturma
toocreate hello alma işi, çağrı hello [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi. Aşağıdaki bilgilerle tooprovide hello gerekir:

-   Merhaba işi için bir ad.

-   Merhaba depolama hesabı adı.

-   Merhaba sevkiyat Hello önceki adımda elde edilen konum adı.

-   İş türü (içe aktarma).

-   Merhaba dönüş adresi Hello alma işi tamamlandıktan sonra hello sürücüleri burada gönderilmelidir.

-   Merhaba işteki sürücülerin listesini Hello. Her bir sürücü için hello sürücü hazırlık adımı sırasında edinilen bilgisinden hello şunları içermelidir:

    -   Merhaba sürücü kimliği

    -   Merhaba BitLocker anahtarı

    -   Merhaba bildirim dosyası göreli yolda hello sabit sürücü

    -   bildirim dosyası MD5 karma değeri Hello Base16 kodlanmış

## <a name="shipping-your-drives"></a>Sürücülerinizin aktarma
Merhaba önceki adımda elde ettiğiniz sürücüleri toohello adresinizi hazırlamalısınız ve hello içeri/dışarı aktarma hizmeti ile Merhaba paket sayısı izleme hello sağlamanız gerekir.

> [!NOTE]
>  Sürücülerinizin paketiniz için bir izleme numarası sağlayacak bir desteklenen taşıyıcı hizmeti aracılığıyla hazırlamalısınız.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Merhaba içe aktarma işi ile sevkiyat bilgilerinizi güncelleştirme
İzleme numaranızın aldıktan sonra hello çağrısı [güncelleştirme işi özellikleri](/api/storageimportexport/jobs#Jobs_Update) taşıyıcı adı, hello izleme numarası hello işi için ve hello taşıyıcı hesap numarası dönüş sevkiyat aktarma işlemi tooupdate hello. İsteğe bağlı olarak, sürücüler ve tarihi de sevkiyat hello hello sayısını belirtebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma](storage-import-export-using-the-rest-api.md)
