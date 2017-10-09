---
title: "aaaAzure olay hub'ları yakalama izlenecek | Microsoft Docs"
description: "Merhaba olay hub'ları yakalama özelliği kullanılarak hello Azure Python SDK'sı toodemonstrate kullanan bir örnektir."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="05884-103">Olay hub'ları yakalama izlenecek yol: Python</span><span class="sxs-lookup"><span data-stu-id="05884-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="05884-104">Olay hub'ları yakalama özelliği, tooautomatically sağlayan Event hubs olay hub'ı tooan Azure Blob Depolama hesabı tercih ettiğiniz veri akış hello teslim olur.</span><span class="sxs-lookup"><span data-stu-id="05884-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="05884-105">Bu özellik, kolay tooperform toplu üzerinde gerçek zamanlı veri akışı işlemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="05884-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="05884-106">Bu makalede toouse Event Hubs ile Python yakalama nasıl.</span><span class="sxs-lookup"><span data-stu-id="05884-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="05884-107">Olay hub'ları yakalama hakkında daha fazla bilgi için bkz: hello [genel bakış makalesi](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05884-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="05884-108">Bu örnek hello kullanan [Azure Python SDK'sı](https://azure.microsoft.com/develop/python/) toodemonstrate hello yakalama özelliği.</span><span class="sxs-lookup"><span data-stu-id="05884-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="05884-109">Merhaba sender.py program sanal ortam telemetriyi tooEvent hub JSON biçiminde gönderir.</span><span class="sxs-lookup"><span data-stu-id="05884-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="05884-110">Merhaba olay hub'ı yapılandırılmış toouse hello yakalama toowrite bu veri tooblob depolama toplu özellik.</span><span class="sxs-lookup"><span data-stu-id="05884-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="05884-111">Merhaba capturereader.py uygulama bu BLOB'lar okur ve cihaz başına bir ekleme dosyası oluşturur, sonra hello verileri .csv dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="05884-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="05884-112">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="05884-112">What will be accomplished</span></span>

1. <span data-ttu-id="05884-113">Bir Azure Blob Storage hesabı ve hello Azure portal kullanarak bir blob kapsayıcısına, oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05884-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="05884-114">Hello Azure portal kullanarak bir Event Hub'ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05884-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="05884-115">Bir event hub'hello yakalama özelliği etkin, hello Azure portal kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05884-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="05884-116">Veri toohello olay hub'ı bir Python komut dosyası ile gönderin.</span><span class="sxs-lookup"><span data-stu-id="05884-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="05884-117">Okuma hello hello dosyalarından yakalamak ve başka bir Python komut dosyasıyla işlem.</span><span class="sxs-lookup"><span data-stu-id="05884-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05884-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="05884-118">Prerequisites</span></span>

- <span data-ttu-id="05884-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="05884-119">Python 2.7.x</span></span>
- <span data-ttu-id="05884-120">Bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="05884-120">An Azure subscription</span></span>
- <span data-ttu-id="05884-121">Etkin bir [olay hub'ları ad alanı ve olay hub'ı.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="05884-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="05884-122">Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="05884-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="05884-123">Toohello üzerinde oturum [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="05884-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="05884-124">Merhaba sol gezinti bölmesinde hello portalı tıklatın **yeni**, ardından **depolama**ve ardından **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="05884-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="05884-125">Hello depolama hesabı dikey penceresinde hello alanları tamamlayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="05884-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="05884-126">Merhaba gördükten sonra **dağıtımları başarılı** iletisi, hello yeni depolama hesabı ve hello hello adına tıklayın **Essentials** dikey penceresinde tıklatın **BLOB'lar**.</span><span class="sxs-lookup"><span data-stu-id="05884-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="05884-127">Ne zaman hello **Blob hizmeti** dikey penceresi açıldığında, tıklatın **+ kapsayıcı** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="05884-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="05884-128">Ad hello kapsayıcı **yakalama**, ardından Kapat hello **Blob hizmeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="05884-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="05884-129">Tıklatın **erişim anahtarları** hello Sol dikey ve kopyalama hello adı hello depolama hesabı ve hello değeri **key1**.</span><span class="sxs-lookup"><span data-stu-id="05884-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="05884-130">Bu değerleri tooNotepad veya başka bir geçici konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="05884-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="05884-131">Bir Python komut dosyası toosend olayları tooyour olay hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="05884-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="05884-132">Sık kullanılan Python düzenleyici gibi açıp [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="05884-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="05884-133">Adlı bir komut dosyası oluşturma **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="05884-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="05884-134">Bu komut dosyası 200 olayları tooyour olay hub'ı gönderir.</span><span class="sxs-lookup"><span data-stu-id="05884-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="05884-135">JSON'da gönderilen basit ortam okumalar oldukları.</span><span class="sxs-lookup"><span data-stu-id="05884-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="05884-136">Kod sender.py aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="05884-136">Paste hello following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="05884-137">Ad alanı adı, anahtar değeri ve hello olay hub'ları ad alanı oluşturduğunuzda aldığınız olay hub'ı adı kod toouse önceki hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="05884-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="05884-138">Python komut dosyası tooread yakalama dosyalarınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="05884-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="05884-139">Merhaba dikey doldurun ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="05884-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="05884-140">Adlı bir komut dosyası oluşturma **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="05884-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="05884-141">Bu komut dosyasını okur hello dosyaları yakalanan ve yalnızca bu cihaz için cihaz toowrite hello verileri her bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="05884-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="05884-142">Kod capturereader.py aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="05884-142">Paste hello following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="05884-143">Depolama hesabı adı ve anahtar çağrısı çok hello hello uygun değerleri emin toopaste olması`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="05884-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="05884-144">Merhaba komut dosyalarını çalıştır</span><span class="sxs-lookup"><span data-stu-id="05884-144">Run hello scripts</span></span>
1. <span data-ttu-id="05884-145">Python kendi yolunda sahip bir komut istemi açın ve ardından tooinstall Python önkoşul şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="05884-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="05884-146">Azure-storage veya azure önceki bir sürümü varsa, toouse hello gerekebilir **--yükseltme** seçeneği</span><span class="sxs-lookup"><span data-stu-id="05884-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="05884-147">Merhaba toorun aşağıdaki (çoğu sistemlerde gerekli değildir) etmeniz gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="05884-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="05884-148">Sender.py ve capturereader.py kaydettiğiniz, dizin toowherever geçin ve şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="05884-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="05884-149">Bu komut, yeni bir Python işlem toorun hello gönderen başlatır.</span><span class="sxs-lookup"><span data-stu-id="05884-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="05884-150">Şimdi hello yakalama toorun birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="05884-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="05884-151">Komut, özgün komut penceresine aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="05884-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="05884-152">Bu yakalama işlemci hello yerel dizin toodownload tüm hello BLOB kapsayıcısından hello depolama hesabı/kullanır.</span><span class="sxs-lookup"><span data-stu-id="05884-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="05884-153">Boş olmayan tüm işler ve hello sonuçları hello yerel dizine .csv dosyaları olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="05884-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05884-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05884-154">Next steps</span></span>

<span data-ttu-id="05884-155">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05884-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="05884-156">[Event Hubs'a genel bakış yakalama][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="05884-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="05884-157">[Event Hubs kullanan bir örnek uygulamanın][sample application that uses Event Hubs] tamamı.</span><span class="sxs-lookup"><span data-stu-id="05884-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="05884-158">Merhaba [Event Hubs ile olay işleme ölçeğini artırma] [ Scale out Event Processing with Event Hubs] örnek.</span><span class="sxs-lookup"><span data-stu-id="05884-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="05884-159">[Event Hubs'a genel bakış][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="05884-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
