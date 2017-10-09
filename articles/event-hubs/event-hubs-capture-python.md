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
# <a name="event-hubs-capture-walkthrough-python"></a>Olay hub'ları yakalama izlenecek yol: Python

Olay hub'ları yakalama özelliği, tooautomatically sağlayan Event hubs olay hub'ı tooan Azure Blob Depolama hesabı tercih ettiğiniz veri akış hello teslim olur. Bu özellik, kolay tooperform toplu üzerinde gerçek zamanlı veri akışı işlemeyi kolaylaştırır. Bu makalede toouse Event Hubs ile Python yakalama nasıl. Olay hub'ları yakalama hakkında daha fazla bilgi için bkz: hello [genel bakış makalesi](event-hubs-archive-overview.md).

Bu örnek hello kullanan [Azure Python SDK'sı](https://azure.microsoft.com/develop/python/) toodemonstrate hello yakalama özelliği. Merhaba sender.py program sanal ortam telemetriyi tooEvent hub JSON biçiminde gönderir. Merhaba olay hub'ı yapılandırılmış toouse hello yakalama toowrite bu veri tooblob depolama toplu özellik. Merhaba capturereader.py uygulama bu BLOB'lar okur ve cihaz başına bir ekleme dosyası oluşturur, sonra hello verileri .csv dosyasına yazar.

## <a name="what-will-be-accomplished"></a>Ne elde edilecek

1. Bir Azure Blob Storage hesabı ve hello Azure portal kullanarak bir blob kapsayıcısına, oluşturun.
2. Hello Azure portal kullanarak bir Event Hub'ad alanı oluşturun.
3. Bir event hub'hello yakalama özelliği etkin, hello Azure portal kullanarak oluşturun.
4. Veri toohello olay hub'ı bir Python komut dosyası ile gönderin.
5. Okuma hello hello dosyalarından yakalamak ve başka bir Python komut dosyasıyla işlem.

## <a name="prerequisites"></a>Ön koşullar

- Python 2.7.x
- Bir Azure aboneliği
- Etkin bir [olay hub'ları ad alanı ve olay hub'ı.](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Azure Depolama hesabı oluşturma
1. Toohello üzerinde oturum [Azure portal][Azure portal].
2. Merhaba sol gezinti bölmesinde hello portalı tıklatın **yeni**, ardından **depolama**ve ardından **depolama hesabı**.
3. Hello depolama hesabı dikey penceresinde hello alanları tamamlayın ve ardından **oluşturma**.
   
   ![][1]
4. Merhaba gördükten sonra **dağıtımları başarılı** iletisi, hello yeni depolama hesabı ve hello hello adına tıklayın **Essentials** dikey penceresinde tıklatın **BLOB'lar**. Ne zaman hello **Blob hizmeti** dikey penceresi açıldığında, tıklatın **+ kapsayıcı** hello üstünde. Ad hello kapsayıcı **yakalama**, ardından Kapat hello **Blob hizmeti** dikey.
5. Tıklatın **erişim anahtarları** hello Sol dikey ve kopyalama hello adı hello depolama hesabı ve hello değeri **key1**. Bu değerleri tooNotepad veya başka bir geçici konuma kaydedin.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Bir Python komut dosyası toosend olayları tooyour olay hub'ı Oluştur
1. Sık kullanılan Python düzenleyici gibi açıp [Visual Studio Code][Visual Studio Code].
2. Adlı bir komut dosyası oluşturma **sender.py**. Bu komut dosyası 200 olayları tooyour olay hub'ı gönderir. JSON'da gönderilen basit ortam okumalar oldukları.
3. Kod sender.py aşağıdaki hello yapıştırın:
   
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
4. Ad alanı adı, anahtar değeri ve hello olay hub'ları ad alanı oluşturduğunuzda aldığınız olay hub'ı adı kod toouse önceki hello güncelleştirin.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Python komut dosyası tooread yakalama dosyalarınızı oluşturma

1. Merhaba dikey doldurun ve **oluşturma**.
2. Adlı bir komut dosyası oluşturma **capturereader.py**. Bu komut dosyasını okur hello dosyaları yakalanan ve yalnızca bu cihaz için cihaz toowrite hello verileri her bir dosya oluşturur.
3. Kod capturereader.py aşağıdaki hello yapıştırın:
   
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
4. Depolama hesabı adı ve anahtar çağrısı çok hello hello uygun değerleri emin toopaste olması`startProcessing`.

## <a name="run-hello-scripts"></a>Merhaba komut dosyalarını çalıştır
1. Python kendi yolunda sahip bir komut istemi açın ve ardından tooinstall Python önkoşul şu komutları çalıştırın:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Azure-storage veya azure önceki bir sürümü varsa, toouse hello gerekebilir **--yükseltme** seçeneği
   
  Merhaba toorun aşağıdaki (çoğu sistemlerde gerekli değildir) etmeniz gerekebilir:
   
  ```
  pip install cryptography
  ```
2. Sender.py ve capturereader.py kaydettiğiniz, dizin toowherever geçin ve şu komutu çalıştırın:
   
  ```
  start python sender.py
  ```
   
  Bu komut, yeni bir Python işlem toorun hello gönderen başlatır.
3. Şimdi hello yakalama toorun birkaç dakika bekleyin. Komut, özgün komut penceresine aşağıdaki hello yazın:
   
   ```
   python capturereader.py
   ```

   Bu yakalama işlemci hello yerel dizin toodownload tüm hello BLOB kapsayıcısından hello depolama hesabı/kullanır. Boş olmayan tüm işler ve hello sonuçları hello yerel dizine .csv dosyaları olarak yazar.

## <a name="next-steps"></a>Sonraki adımlar

Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs'a genel bakış yakalama][Overview of Event Hubs Capture]
* [Event Hubs kullanan bir örnek uygulamanın][sample application that uses Event Hubs] tamamı.
* Merhaba [Event Hubs ile olay işleme ölçeğini artırma] [ Scale out Event Processing with Event Hubs] örnek.
* [Event Hubs'a genel bakış][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
