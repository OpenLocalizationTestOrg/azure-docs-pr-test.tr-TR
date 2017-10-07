---
title: "Merhaba C++ için depolama istemci kitaplığı ile aaaList Azure Storage kaynaklarını | Microsoft Docs"
description: "C++ tooenumerate kapsayıcıları, blobları, Microsoft Azure Storage istemci kitaplığı API'leri listeleme toouse hello nasıl kuyruklar, bilgi tabloları ve varlıkları."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>C++'ta Azure Storage kaynakları listeler
Liste, Azure Storage ile anahtar toomany geliştirme senaryolarını işlemleridir. Bu makalede nasıl toomost verimli bir şekilde listeleme C++ için Microsoft Azure Storage istemci kitaplığı hello API'lerinden listeleme hello kullanarak Azure storage'da nesneleri açıklanmaktadır.

> [!NOTE]
> Bu kılavuzda C++ sürümü için Azure Storage istemci kitaplığı hello hedefler aracılığıyla kullanıma 2.x [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Merhaba depolama istemci kitaplığı çeşitli yöntemleri toolist veya Azure Storage sorgu nesneleri sağlar. Bu makalede senaryoları aşağıdaki hello ele alır:

* Bir hesap listesi kapsayıcıları
* Liste BLOB bir kapsayıcı veya sanal blob dizini
* Bir hesap listesi kuyruklar
* Bir hesap listede tablolar
* Bir tablodaki sorgu varlıklar

Bu yöntemlerin her biri için farklı senaryolar farklı aşırı yüklemeleri kullanarak gösterilir.

## <a name="asynchronous-versus-synchronous"></a>Zaman uyumlu ve zaman uyumsuz
Merhaba C++ için depolama istemci kitaplığı hello üzerine inşa edildiğinden [C++ REST Kitaplığı](https://github.com/Microsoft/cpprestsdk), kendiliğinden zaman uyumsuz işlemleri kullanarak destekliyoruz [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Örneğin:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Zaman uyumlu işlemler hello karşılık gelen zaman uyumsuz işlemleri kaydır:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Birden çok iş parçacıklı uygulamalar veya hizmetler ile çalışıyorsanız, doğrudan bir iş parçacığı toocall hello eşitleme, performansı önemli ölçüde etkiler API ' larını oluşturmak yerine hello zaman uyumsuz API'leri kullanmanızı öneririz.

## <a name="segmented-listing"></a>Bölümlenmiş listeleme
Bulut depolama Hello ölçeğini bölümlenmiş listeleme gerektirir. Örneğin, bir Azure blob kapsayıcısındaki bir milyon BLOB veya bir Azure tablosu bir milyar varlıklarda üzerinden olabilir. Bunlar teorik numaraları, ancak gerçek müşteri kullanım durumları olup olmadığı.

Bu nedenle, tüm nesneleri tek bir yanıtta pratik toolist olur. Bunun yerine, disk belleği kullanarak nesneleri listeleyebilirsiniz. Her API listeleme hello sahip bir *kesimli* aşırı yükleme.

bölümlenmiş listeleme işlemi Hello yanıtı içerir:

* <i>_segment</i>, API listeleyen tek çağrı toohello için döndürülen sonuçları hello kümesi içerir.
* *continuation_token*, hangi geçirilir toohello sonraki çağrı sırası tooget hello sonraki sonuç sayfasını içinde. Daha fazla hiçbir sonuç tooreturn olduğunda hello devamlılık belirteci null.

Örneğin, tipik çağrısı toolist bir kapsayıcıdaki tüm blob'lara hello kod parçacığını aşağıdaki gibi görünebilir. Merhaba kodudur bulunan bizim [örnekleri](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

Bir sayfa döndürülen sonuç sayısı Hello hello parametresiyle denetlenebilir Not *max_results* örneğin her API hello yüklemesini içinde:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Merhaba belirtmezseniz *max_results* parametresi, hello varsayılan too5000 sonuçları yukarı en büyük değer olan tek bir sayfayla döndürülür.

Ayrıca, Azure Table storage bir sorgu kayıt yok veya hello hello değerinden daha az sayıda kayıt döndürebilir unutmayın *max_results* hello devamlılık belirteci boş olsa bile, belirtilen parametre. Nedenlerinden biri, o hello sorgu beş saniye içinde tamamlanamadı olabilir. Hello devamlılık belirteci boş değil sürece hello sorgu devam etmesi gerektiğini ve kodunuzu segment sonuçları hello boyutunu varsayımında bulunmamalıdır.

Çoğu senaryo için desen kodlama listeleme listeleme veya sorgulama açık ilerleme sağlayan bölümlenmiş ve hello hizmet tooeach isteği nasıl yanıt vereceğini Hello önerilir. Özellikle C++ uygulamalar veya hizmetler için alt düzey denetim ilerleme listeleme hello denetim bellek ve performans yardımcı olabilir.

## <a name="greedy-listing"></a>Doyumsuz listeleme
Merhaba C++ için depolama istemci Kitaplığı'nın önceki sürümlerini (sürümleri 0.5.0 Önizleme ve önceki sürümler) kesimli olmayan listeleme API'leri tablolar ve Kuyruklar aşağıdaki örneğine hello olduğu için dahil:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Bu yöntemleri bölümlenmiş API'leri sarmalayıcılar olarak oluşturulmuştur. Her yanıtı bölümlenmiş dökümün hello kod hello sonuçları tooa vektör eklenmiş ve tam Merhaba kapsayıcılara taranan sonra tüm sonuç döndürmedi.

Az sayıda nesne Hello depolama hesabı veya tablo içerdiğinde, bu yaklaşım çalışabilir. Ancak, tüm sonuçları bellekte kalan çünkü bir artış ile Merhaba nesnelerin sayısı, gerekli hello bellek sınırı arttırabilir. Bir listeleme işlemi sırasında hangi hello ilerleme durumunu hakkında hiçbir bilgi arayan sahip bir çok uzun zaman alabilir.

Doyumsuz bu hello SDK API'leri listeleme C# ' ta, Java, yok veya JavaScript Node.js ortamı hello. doyumsuz bu API'leri kullanarak tooavoid hello olası sorunları, biz onları kaldırmış sürüm 0.6.0 Önizleme.

Kodunuzu bu doyumsuz API çağırıyorsa:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Kodunuzu değiştirmelisiniz sonra toouse hello kesimli API'leri listeleme:

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

Merhaba belirterek *max_results* parametresi hello kesiminin, Bakiye hello sayıda isteği ve uygulamanız için bellek kullanım toomeet başarım düşünceleri arasında.

Bölümlenmiş listeleme API'leri kullanarak ancak bir "Hızlı" stili yerel bir koleksiyondaki hello verilerini depolamak olduğunuz, ayrıca, aynı zamanda dikkatle ölçekte yerel bir koleksiyondaki veri depolama, kod toohandle yeniden düzenlemeniz öneririz.

## <a name="lazy-listing"></a>Yavaş listeleme
Doyumsuz listeleme olası sorunları ortaya hello kapsayıcısında çok fazla nesne değilse bu kullanışlı olsa da.

C# veya Oracle Java SDK'ları da kullanıyorsanız, bir yavaş, gerekirse burada hello belirli uzaklığındaki veri yalnızca alınmadığı listeleme stili sunan hello numaralandırılabilir programlama modeli, tanımanız gerekir. C++'da, hello yineleyici tabanlı şablonunu de benzer bir yaklaşım sağlar.

Tipik yavaş listeleme API'sini kullanarak **list_blobs** örnek olarak, şöyle görünür:

```cpp
list_blob_item_iterator list_blobs() const;
```

Merhaba yavaş listeleme desen kullanan bir tipik kod parçacığını şuna benzeyebilir:

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

Yavaş listeleme yalnızca zaman uyumlu modda kullanılabilir olduğunu unutmayın.

Doyumsuz listesi ile karşılaştırıldığında, yavaş listeleme verileri yalnızca gerekli olduğunda getirir. Yalnızca hello sonraki yineleyici sonraki segmentin taşındığında hello perde arkasında bu verileri Azure depolama biriminden getirir. Bu nedenle, bellek kullanımı ile sınırlanmış bir boyutu denetlenir ve hello hızlı bir işlemdir.

Yavaş listeleme API'leri dahil edilir hello depolama istemci kitaplığı C++ için sürüm 2.2.0.

## <a name="conclusion"></a>Sonuç
Bu makalede, C++ için depolama istemci kitaplığı hello çeşitli nesneler için API listeleme için farklı aşırı açıklanmıştır. toosummarize:

* Zaman uyumsuz API'leri birden çok iş parçacığı senaryolarda önerilir.
* Bölümlenmiş listeleme çoğu senaryolar için önerilir.
* Yavaş listeleme kullanışlı bir sarmalayıcı zaman uyumlu senaryolarda olarak hello Kitaplığı'nda sağlanır.
* Doyumsuz listeleme tavsiye edilmez ve hello Kitaplığı'ndan kaldırıldı.

## <a name="next-steps"></a>Sonraki adımlar
C++ için Azure Storage istemci Kitaplığı hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.

* [Nasıl toouse Blob depolama alanından C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Nasıl toouse C++ tablo depolamasından](storage-c-plus-plus-how-to-use-tables.md)
* [Nasıl toouse C++ içinden kuyruk depolama](storage-c-plus-plus-how-to-use-queues.md)
* [C++ API belgeleri için Azure Storage istemci kitaplığı.](http://azure.github.io/azure-storage-cpp/)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)

