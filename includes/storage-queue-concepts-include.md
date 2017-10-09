## <a name="what-is-queue-storage"></a>Kuyruk Depolama nedir?
Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir. Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.

Kuyruk depolamanın yaygın kullanımları şunlardır:

* Zaman uyumsuz olarak biriktirme çalışma tooprocess listesi oluşturma
* İletileri Azure web rolü tooan Azure çalışan rolüne geçirme

## <a name="queue-service-concepts"></a>Kuyruk Hizmeti Kavramları
Merhaba sıra hizmeti hello aşağıdaki bileşenleri içerir:

![Kuyruk1](./media/storage-queue-concepts-include/queue1.png)

* **URL biçimi:** sıraları hello şu URL biçimi kullanılarak adreslenebilir:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    URL aşağıdaki hello hello diyagramı kuyrukta ele alır:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Depolama hesabı:** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. Depolama hesabı kapasitesi hakkında ayrıntılı bilgi için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](../articles/storage/common/storage-scalability-targets.md).
* **Kuyruk:** Kuyrukta bir dizi ileti vardır. Tüm iletiler bir kuyrukta olmalıdır. Bu hello sıra adı tüm küçük harfli olması gerektiğini unutmayın. Kuyrukların adlandırılması hakkında daha fazla bilgi için bkz. [Kuyrukları ve Meta Verileri Adlandırma](https://msdn.microsoft.com/library/azure/dd179349.aspx).
* **İleti:** bir ileti görüntülenirse, herhangi bir biçimde too64 KB. Merhaba bir ileti hello kuyrukta kalabileceği en uzun süre 7 gündür.

