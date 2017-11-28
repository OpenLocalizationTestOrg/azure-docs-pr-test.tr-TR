---
title: Ruby'den kuyruk depolama kullanma | Microsoft Docs
description: "Oluşturmak ve Kuyruklar silmek için Azure Queue hizmetini kullanmayı öğrenin ve Ekle, Al ve iletilerini silin. Ruby içinde yazılmış örneklerini içerir."
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
ms.openlocfilehash: b978b65bb3b717362697a41510c5b2b4d057cf1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="5dac4-104">Ruby’den Kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="5dac4-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="5dac4-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5dac4-105">Overview</span></span>
<span data-ttu-id="5dac4-106">Bu kılavuz Microsoft Azure kuyruk depolama hizmeti kullanılarak yaygın senaryolar gerçekleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="5dac4-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="5dac4-107">Örnekler, Ruby Azure API'sini kullanarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="5dac4-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="5dac4-108">Kapsamdaki senaryolar dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="5dac4-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="5dac4-109">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5dac4-109">Create a Ruby Application</span></span>
<span data-ttu-id="5dac4-110">Bir Ruby uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5dac4-110">Create a Ruby application.</span></span> <span data-ttu-id="5dac4-111">Yönergeler için bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="5dac4-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="5dac4-112">Uygulamanızı erişimli depolama için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5dac4-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="5dac4-113">Azure depolama kullanmak için indirme ve storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Söyleniş azure paketini kullanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dac4-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="5dac4-114">Paket elde etmek için RubyGems kullanın</span><span class="sxs-lookup"><span data-stu-id="5dac4-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="5dac4-115">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="5dac4-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="5dac4-116">Gem ve bağımlılıklarını yüklemek için komut penceresinde "gem yükleme azure" yazın.</span><span class="sxs-lookup"><span data-stu-id="5dac4-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="5dac4-117">Paket alma</span><span class="sxs-lookup"><span data-stu-id="5dac4-117">Import the package</span></span>
<span data-ttu-id="5dac4-118">Sık kullandığınız metin düzenleyiciyi kullanın, burada depolama kullanmayı düşündüğünüz Söyleniş dosyasının üstüne aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5dac4-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="5dac4-119">Bir Azure depolama bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="5dac4-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="5dac4-120">Azure modülü ortam değişkenleri okur **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_ACCESS_KEY** Azure depolama hesabınıza bağlanmak için gerekli bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="5dac4-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="5dac4-121">Bu ortam değişkenleri ayarlanmamışsa, hesap bilgilerini kullanmadan önce belirtmelisiniz **Azure::QueueService** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="5dac4-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="5dac4-122">Klasik veya Resource Manager depolama hesabı Azure portalında bu değerleri almak için:</span><span class="sxs-lookup"><span data-stu-id="5dac4-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="5dac4-123">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5dac4-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5dac4-124">Kullanmak istediğiniz depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="5dac4-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="5dac4-125">Sağ taraftaki ayarları dikey penceresinde tıklayın **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="5dac4-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="5dac4-126">Görüntülenen erişim anahtarları dikey penceresinde, erişim tuşu 1 ve 2 erişim anahtarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="5dac4-127">Bunlardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-127">You can use either of these.</span></span> 
5. <span data-ttu-id="5dac4-128">Anahtarı panoya kopyalamak için Kopyala simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dac4-128">Click the copy icon to copy the key to the clipboard.</span></span> 

<span data-ttu-id="5dac4-129">Klasik Azure portalında bir Klasik depolama hesabı bu değerleri almak için:</span><span class="sxs-lookup"><span data-stu-id="5dac4-129">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="5dac4-130">Oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5dac4-130">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5dac4-131">Kullanmak istediğiniz depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="5dac4-131">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="5dac4-132">Tıklatın **erişim ANAHTARLARINI Yönet** alt gezinti bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5dac4-132">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="5dac4-133">Açılan iletişim, depolama hesabı adı ve birincil erişim anahtarını ikincil erişim anahtarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-133">In the pop up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="5dac4-134">Erişim anahtarı için birincil veya ikincil bir kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-134">For access key, you can use either the primary one or the secondary one.</span></span> 
5. <span data-ttu-id="5dac4-135">Anahtarı panoya kopyalamak için Kopyala simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dac4-135">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="5dac4-136">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="5dac4-136">How To: Create a Queue</span></span>
<span data-ttu-id="5dac4-137">Aşağıdaki kod oluşturur bir **Azure::QueueService** kuyruklarla çalışmanıza olanak tanır nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5dac4-137">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="5dac4-138">Kullanım **create_queue()** yöntemi belirtilen ada sahip bir kuyruk oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5dac4-138">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="5dac4-139">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="5dac4-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="5dac4-140">Kuyruğa bir ileti eklemek için kullanın **create_message()** yeni bir ileti oluşturun ve sıraya eklemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="5dac4-140">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="5dac4-141">Nasıl yapılır: sonraki iletiye</span><span class="sxs-lookup"><span data-stu-id="5dac4-141">How To: Peek at the Next Message</span></span>
<span data-ttu-id="5dac4-142">Kuyruğun önündeki iletiye sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **gözlem\_messages()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5dac4-142">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="5dac4-143">Varsayılan olarak, **gözlem\_messages()** tek bir iletiye peeks.</span><span class="sxs-lookup"><span data-stu-id="5dac4-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="5dac4-144">Gözatmak istediğiniz kaç iletileri de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-144">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="5dac4-145">Nasıl yapılır: sonraki iletiyi sıradan çıkarma</span><span class="sxs-lookup"><span data-stu-id="5dac4-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="5dac4-146">Bir iletiyi bir kuyruktan iki adımda kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="5dac4-147">Çağırdığınızda **listesi\_messages()**, varsayılan olarak bir sırada sonraki iletiyi alın.</span><span class="sxs-lookup"><span data-stu-id="5dac4-147">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="5dac4-148">Kaç tane iletileri almak istediğiniz de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-148">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="5dac4-149">Döndürülen iletileri **listesi\_messages()** iletileri bu sıradan okuyan herhangi bir kod görünmez olur.</span><span class="sxs-lookup"><span data-stu-id="5dac4-149">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="5dac4-150">Görünürlük zaman aşımı saniye olarak bir parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="5dac4-150">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="5dac4-151">İletiyi kuyruktan kaldırmayı tamamlamak için de çağırmanız gerekir **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="5dac4-151">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="5dac4-152">Bir ileti kaldırmanın bu iki adımlı işlem donanım veya yazılım hatası nedeniyle bir ileti işlemek kodunuzu başarısız olduğunda, kodunuzu başka bir örneği aynı ileti alma ve yeniden deneyin sağlar.</span><span class="sxs-lookup"><span data-stu-id="5dac4-152">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="5dac4-153">Kod çağrılarınızı **silmek\_message()** ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="5dac4-153">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="5dac4-154">Nasıl yapılır: kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="5dac4-154">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="5dac4-155">Kuyrukta yer alan bir iletinin içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-155">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="5dac4-156">Aşağıdaki kod kullanır **update_message()** bir ileti güncelleştirmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="5dac4-156">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="5dac4-157">Yöntem pop alınmasını kuyruk iletisi ve ileti sırası görünür olacak zaman temsil eden bir UTC tarih saat değeri içeren bir tanımlama grubu döndürür.</span><span class="sxs-lookup"><span data-stu-id="5dac4-157">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="5dac4-158">Nasıl yapılır: kuyruktan alma için ek seçenekler iletileri</span><span class="sxs-lookup"><span data-stu-id="5dac4-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="5dac4-159">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="5dac4-160">İleti toplu elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="5dac4-161">Uzun veya daha kısa bir görünmezlik zaman aşımı kodunuzun her iletiyi tamamen işlemesi için zaman daha az veya daha fazla izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="5dac4-162">Aşağıdaki kod örneğinde **listesi\_messages()** tek çağrıda 15 iletileri almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5dac4-162">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="5dac4-163">Ardından yazdırır ve her iletiyi siler.</span><span class="sxs-lookup"><span data-stu-id="5dac4-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="5dac4-164">Ayrıca her ileti için görünmezlik zaman aşımı beş dakika olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5dac4-164">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="5dac4-165">Nasıl yapılır: kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="5dac4-165">How To: Get the Queue Length</span></span>
<span data-ttu-id="5dac4-166">Sırasındaki ileti sayısını tahmin alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac4-166">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="5dac4-167">**Almak\_sıra\_metadata()** yöntemi yaklaşık ileti sayısı ve kuyruk hakkındaki meta verileri döndürmek için sıra hizmeti sorar.</span><span class="sxs-lookup"><span data-stu-id="5dac4-167">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="5dac4-168">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="5dac4-168">How To: Delete a Queue</span></span>
<span data-ttu-id="5dac4-169">Bir kuyruk ve içerdiği tüm iletileri silmek için arama **silmek\_queue()** nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5dac4-169">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="5dac4-170">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5dac4-170">Next Steps</span></span>
<span data-ttu-id="5dac4-171">Kuyruk depolamanın temellerini öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5dac4-171">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="5dac4-172">Ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="5dac4-172">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="5dac4-173">Ziyaret [Ruby için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki</span><span class="sxs-lookup"><span data-stu-id="5dac4-173">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="5dac4-174">Bu makalede ele alınan Azure sıra hizmeti ve Azure hizmet veri yolu kuyrukları ele arasında bir karşılaştırma için [Service Bus kuyruklarını kullanma](/develop/ruby/how-to-guides/service-bus-queues/) makale için bkz: [Azure kuyruklar ve hizmet veri yolu kuyrukları karşılaştırılan ve Contrasted -](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="5dac4-174">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>