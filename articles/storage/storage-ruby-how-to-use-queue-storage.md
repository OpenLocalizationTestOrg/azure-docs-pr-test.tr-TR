---
title: aaaHow toouse ruby'den kuyruk depolama | Microsoft Docs
description: "Nasıl toouse hello Azure kuyruk hizmeti toocreate ve delete kuyruklar ve Ekle, Al ve iletileri silmek öğrenin. Ruby içinde yazılmış örneklerini içerir."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>Nasıl toouse ruby'den kuyruk depolama
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl Microsoft Azure kuyruk depolama hizmeti kullanarak tooperform genel senaryolar hello gösterir. Merhaba örnekleri hello Ruby Azure API kullanılarak yazılır.
Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Ruby uygulaması oluşturma
Bir Ruby uygulaması oluşturun. Yönergeler için bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Uygulamanızı tooAccess depolama yapılandırma
Azure depolama toouse, toodownload ve kullanım hello hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketi gerekir.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).
2. "Gem yükle azure" Merhaba komut penceresinde tooinstall hello gem ve bağımlılıkları yazın.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Sık kullandığınız metin düzenleyiciyi kullanın, hello toouse depolama burada düşündüğünüz Söyleniş dosya toohello üstündeki aşağıdaki hello ekleyin:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Bir Azure depolama bağlantı Kur
Hello azure modülü hello ortam değişkenleri okuma **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_ACCESS_KEY** için bilgi tooconnect tooyour Azure depolama hesabı gerekiyor. Bu ortam değişkenleri ayarlanmamışsa, kullanmadan önce hello hesap bilgileri belirtmelisiniz **Azure::QueueService** koddan hello ile:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain hello Azure portal bu değerleri Klasik veya Resource Manager depolama hesabı:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Toouse istediğiniz toohello depolama hesabının gidin.
3. Merhaba sağ üzerinde Hello ayarları dikey penceresinde tıklayın **erişim tuşları**.
4. Görüntülenen hello erişim anahtarları dikey penceresinde hello erişim tuşu 1 ve 2 erişim anahtarı görürsünüz. Bunlardan kullanabilirsiniz. 
5. Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın. 

tooobtain hello Klasik Azure Portalı'nda bu değerleri Klasik depolama hesabı:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Toouse istediğiniz toohello depolama hesabının gidin.
3. Tıklatın **erişim ANAHTARLARINI Yönet** hello Gezinti bölmesinin hello altındaki.
4. İletişim kutusunu pop Hello içinde hello depolama hesabı adı, birincil erişim anahtarını ve ikincil erişim anahtarını görürsünüz. Erişim anahtarı hello birincil veya ikincil bir hello kullanabilirsiniz. 
5. Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.

## <a name="how-to-create-a-queue"></a>Nasıl yapılır: bir sıra oluşturun
Merhaba aşağıdaki kod oluşturur bir **Azure::QueueService** toowork kuyruklarla sağlayan nesne.

```ruby
azure_queue_service = Azure::QueueService.new
```

Kullanım hello **create_queue()** yöntemi toocreate hello sahip bir sıra adı belirtildi.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Nasıl yapılır: bir sıraya bir ileti Ekle
tooinsert bir sıra kullanım hello iletiye **create_message()** yöntemi toocreate yeni bir ileti ve toohello sıra ekleyin.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Nasıl yapılır: sonraki iletiyi hello Gözat
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **gözlem\_messages()** yöntemi. Varsayılan olarak, **gözlem\_messages()** tek bir iletiye peeks. Kaç tane iletileri belirtebilirsiniz toopeek istiyor.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Nasıl yapılır: hello sonraki iletiyi sıradan çıkarma
Bir iletiyi bir kuyruktan iki adımda kaldırabilirsiniz.

1. Çağırdığınızda **listesi\_messages()**, varsayılan olarak bir kuyruktaki hello sonraki iletiyi alın. Kaç tane iletileri belirtebilirsiniz tooget istiyor. Merhaba döndürülen iletileri **listesi\_messages()** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. Merhaba görünürlük zaman aşımı saniye olarak bir parametre olarak geçirin.
2. toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **delete_message()**.

Aynı iletiyi ve try toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilir, kod başarısız tooprocess yeniden hello zaman bir ileti kaldırmanın bu iki adımlı işlem, sağlar. Kod çağrılarınızı **silmek\_message()** hello ileti işlendikten sonra sağ.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Nasıl yapılır: bir sıraya ileti hello içeriğini değiştirme
Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz. Aşağıdaki Hello kodu kullanan hello **update_message()** yöntemi tooupdate bir ileti. Merhaba yöntemi hello pop iletinin alınması, hello sırası içeren bir tanımlama grubu ve selamlama iletisine hello sırasına görünür olacak zaman temsil eden bir UTC tarih saat değeri döndürür.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Nasıl yapılır: kuyruktan alma için ek seçenekler iletileri
İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.

1. İleti toplu elde edebilirsiniz.
2. Kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.

Merhaba aşağıdaki kod örneği kullanır hello **listesi\_messages()** bir çağrı yöntemi tooget 15 iletileri. Ardından yazdırır ve her iletiyi siler. Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Nasıl yapılır: hello kuyruk uzunluğu alma
Merhaba kuyrukta iletileri hello sayısının bir tahmin elde edebilirsiniz. Merhaba **almak\_sıra\_metadata()** yöntemi hello sırası hakkında hello kuyruk hizmeti tooreturn hello yaklaşık ileti sayısı ve meta veri sorar.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Nasıl yapılır: bir kuyruk silme
toodelete bir sıra ve tüm karışılama iletileri bulunan, içinde arama hello **silmek\_queue()** hello nesnesinde yöntemi.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Sonraki Adımlar
Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* Merhaba ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)
* Merhaba ziyaret [Ruby için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki

Azure sıra bu makale ve Azure hizmet veri yolu kuyrukları hello ele alınan ele hizmeti arasında bir karşılaştırma için hello [nasıl toouse Service Bus kuyruklarını](/develop/ruby/how-to-guides/service-bus-queues/) makale için bkz: [Azure kuyruklar ve hizmet veri yolu kuyrukları - karşılaştırıldığında ve Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
