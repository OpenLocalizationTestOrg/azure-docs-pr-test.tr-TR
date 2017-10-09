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
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="301fd-104">Nasıl toouse ruby'den kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="301fd-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="301fd-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="301fd-105">Overview</span></span>
<span data-ttu-id="301fd-106">Bu kılavuz size nasıl Microsoft Azure kuyruk depolama hizmeti kullanarak tooperform genel senaryolar hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="301fd-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="301fd-107">Merhaba örnekleri hello Ruby Azure API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="301fd-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="301fd-108">Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="301fd-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="301fd-109">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="301fd-109">Create a Ruby Application</span></span>
<span data-ttu-id="301fd-110">Bir Ruby uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="301fd-110">Create a Ruby application.</span></span> <span data-ttu-id="301fd-111">Yönergeler için bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="301fd-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="301fd-112">Uygulamanızı tooAccess depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="301fd-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="301fd-113">Azure depolama toouse, toodownload ve kullanım hello hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="301fd-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="301fd-114">RubyGems tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="301fd-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="301fd-115">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="301fd-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="301fd-116">"Gem yükle azure" Merhaba komut penceresinde tooinstall hello gem ve bağımlılıkları yazın.</span><span class="sxs-lookup"><span data-stu-id="301fd-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="301fd-117">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="301fd-117">Import hello package</span></span>
<span data-ttu-id="301fd-118">Sık kullandığınız metin düzenleyiciyi kullanın, hello toouse depolama burada düşündüğünüz Söyleniş dosya toohello üstündeki aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="301fd-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="301fd-119">Bir Azure depolama bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="301fd-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="301fd-120">Hello azure modülü hello ortam değişkenleri okuma **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_ACCESS_KEY** için bilgi tooconnect tooyour Azure depolama hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="301fd-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="301fd-121">Bu ortam değişkenleri ayarlanmamışsa, kullanmadan önce hello hesap bilgileri belirtmelisiniz **Azure::QueueService** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="301fd-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="301fd-122">tooobtain hello Azure portal bu değerleri Klasik veya Resource Manager depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="301fd-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="301fd-123">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="301fd-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="301fd-124">Toouse istediğiniz toohello depolama hesabının gidin.</span><span class="sxs-lookup"><span data-stu-id="301fd-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="301fd-125">Merhaba sağ üzerinde Hello ayarları dikey penceresinde tıklayın **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="301fd-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="301fd-126">Görüntülenen hello erişim anahtarları dikey penceresinde hello erişim tuşu 1 ve 2 erişim anahtarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="301fd-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="301fd-127">Bunlardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-127">You can use either of these.</span></span> 
5. <span data-ttu-id="301fd-128">Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="301fd-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="301fd-129">tooobtain hello Klasik Azure Portalı'nda bu değerleri Klasik depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="301fd-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="301fd-130">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="301fd-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="301fd-131">Toouse istediğiniz toohello depolama hesabının gidin.</span><span class="sxs-lookup"><span data-stu-id="301fd-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="301fd-132">Tıklatın **erişim ANAHTARLARINI Yönet** hello Gezinti bölmesinin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="301fd-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="301fd-133">İletişim kutusunu pop Hello içinde hello depolama hesabı adı, birincil erişim anahtarını ve ikincil erişim anahtarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="301fd-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="301fd-134">Erişim anahtarı hello birincil veya ikincil bir hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="301fd-135">Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="301fd-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="301fd-136">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="301fd-136">How To: Create a Queue</span></span>
<span data-ttu-id="301fd-137">Merhaba aşağıdaki kod oluşturur bir **Azure::QueueService** toowork kuyruklarla sağlayan nesne.</span><span class="sxs-lookup"><span data-stu-id="301fd-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="301fd-138">Kullanım hello **create_queue()** yöntemi toocreate hello sahip bir sıra adı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="301fd-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="301fd-139">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="301fd-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="301fd-140">tooinsert bir sıra kullanım hello iletiye **create_message()** yöntemi toocreate yeni bir ileti ve toohello sıra ekleyin.</span><span class="sxs-lookup"><span data-stu-id="301fd-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="301fd-141">Nasıl yapılır: sonraki iletiyi hello Gözat</span><span class="sxs-lookup"><span data-stu-id="301fd-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="301fd-142">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **gözlem\_messages()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="301fd-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="301fd-143">Varsayılan olarak, **gözlem\_messages()** tek bir iletiye peeks.</span><span class="sxs-lookup"><span data-stu-id="301fd-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="301fd-144">Kaç tane iletileri belirtebilirsiniz toopeek istiyor.</span><span class="sxs-lookup"><span data-stu-id="301fd-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="301fd-145">Nasıl yapılır: hello sonraki iletiyi sıradan çıkarma</span><span class="sxs-lookup"><span data-stu-id="301fd-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="301fd-146">Bir iletiyi bir kuyruktan iki adımda kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="301fd-147">Çağırdığınızda **listesi\_messages()**, varsayılan olarak bir kuyruktaki hello sonraki iletiyi alın.</span><span class="sxs-lookup"><span data-stu-id="301fd-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="301fd-148">Kaç tane iletileri belirtebilirsiniz tooget istiyor.</span><span class="sxs-lookup"><span data-stu-id="301fd-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="301fd-149">Merhaba döndürülen iletileri **listesi\_messages()** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="301fd-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="301fd-150">Merhaba görünürlük zaman aşımı saniye olarak bir parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="301fd-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="301fd-151">toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="301fd-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="301fd-152">Aynı iletiyi ve try toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilir, kod başarısız tooprocess yeniden hello zaman bir ileti kaldırmanın bu iki adımlı işlem, sağlar.</span><span class="sxs-lookup"><span data-stu-id="301fd-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="301fd-153">Kod çağrılarınızı **silmek\_message()** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="301fd-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="301fd-154">Nasıl yapılır: bir sıraya ileti hello içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="301fd-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="301fd-155">Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="301fd-156">Aşağıdaki Hello kodu kullanan hello **update_message()** yöntemi tooupdate bir ileti.</span><span class="sxs-lookup"><span data-stu-id="301fd-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="301fd-157">Merhaba yöntemi hello pop iletinin alınması, hello sırası içeren bir tanımlama grubu ve selamlama iletisine hello sırasına görünür olacak zaman temsil eden bir UTC tarih saat değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="301fd-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="301fd-158">Nasıl yapılır: kuyruktan alma için ek seçenekler iletileri</span><span class="sxs-lookup"><span data-stu-id="301fd-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="301fd-159">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="301fd-160">İleti toplu elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="301fd-161">Kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="301fd-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="301fd-162">Merhaba aşağıdaki kod örneği kullanır hello **listesi\_messages()** bir çağrı yöntemi tooget 15 iletileri.</span><span class="sxs-lookup"><span data-stu-id="301fd-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="301fd-163">Ardından yazdırır ve her iletiyi siler.</span><span class="sxs-lookup"><span data-stu-id="301fd-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="301fd-164">Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="301fd-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="301fd-165">Nasıl yapılır: hello kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="301fd-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="301fd-166">Merhaba kuyrukta iletileri hello sayısının bir tahmin elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="301fd-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="301fd-167">Merhaba **almak\_sıra\_metadata()** yöntemi hello sırası hakkında hello kuyruk hizmeti tooreturn hello yaklaşık ileti sayısı ve meta veri sorar.</span><span class="sxs-lookup"><span data-stu-id="301fd-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="301fd-168">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="301fd-168">How To: Delete a Queue</span></span>
<span data-ttu-id="301fd-169">toodelete bir sıra ve tüm karışılama iletileri bulunan, içinde arama hello **silmek\_queue()** hello nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="301fd-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="301fd-170">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="301fd-170">Next Steps</span></span>
<span data-ttu-id="301fd-171">Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="301fd-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="301fd-172">Merhaba ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="301fd-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="301fd-173">Merhaba ziyaret [Ruby için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki</span><span class="sxs-lookup"><span data-stu-id="301fd-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="301fd-174">Azure sıra bu makale ve Azure hizmet veri yolu kuyrukları hello ele alınan ele hizmeti arasında bir karşılaştırma için hello [nasıl toouse Service Bus kuyruklarını](/develop/ruby/how-to-guides/service-bus-queues/) makale için bkz: [Azure kuyruklar ve hizmet veri yolu kuyrukları - karşılaştırıldığında ve Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="301fd-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
