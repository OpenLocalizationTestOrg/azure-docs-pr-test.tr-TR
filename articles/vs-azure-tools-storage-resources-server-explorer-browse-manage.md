---
title: "aaaBrowsing ve Sunucu Gezgini ile depolama kaynaklarını yönetme | Microsoft Docs"
description: "Göz atma ve Sunucu Gezgini ile depolama kaynaklarını yönetme"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Göz atma ve Sunucu Gezgini ile depolama kaynaklarını yönetme
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Genel Bakış
Hello Azure Araçları için Microsoft Visual Studio yüklediyseniz, depolama hesapları blob, kuyruk ve tablo verileri için Azure görüntüleyebilirsiniz. Sunucu Gezgininde Hello Azure Depolama düğümü yerel depolama öykünücüsü hesabınızı ve diğer Azure storage hesaplarınızı verileri gösterir.

Merhaba menü çubuğunda, Visual Studio'da Sunucu Gezgini tooview seçin **Görünüm**, **Sunucu Gezgini**. Merhaba depolama düğüm tüm her Azure aboneliği veya bağlı olduğunuz sertifikanın altında mevcut hello depolama hesaplarını gösterir. Depolama hesabınız görünmüyorsa, bunu hello yönergeleri izleyerek ekleyebilirsiniz [bu konunun devamındaki](#add-storage-accounts-by-using-server-explorer).

Azure SDK 2.7 başlayarak, ayrıca hello yeni Cloud Explorer tooview kullanın ve Azure kaynaklarınızı yönetmek. Bkz: [bulut Gezgini ile Azure kaynaklarını yönetme](vs-azure-tools-resources-managing-with-cloud-explorer.md) daha fazla bilgi için.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Visual Studio'da depolama kaynakları görüntülemek ve yönetmek
Sunucu Gezgini otomatik olarak depolama öykünücüsü hesabınızda BLOB, kuyruklar ve tablolar listesini gösterir. Merhaba depolama öykünücüsü hesabı hello olarak hello Depolama düğümü altındaki Server Explorer'da listelendiğini **geliştirme** düğümü.

toosee hello depolama öykünücüsü hesabın kaynaklarını genişletmek hello **geliştirme** düğümü. Merhaba genişlettiğinizde hello depolama öykünücüsü başlatılmış kurmadı varsa **geliştirme** düğümü, onu otomatik olarak başlatılacak. Bu işlem birkaç saniye alabilir. Merhaba depolama öykünücüsü başlatılırken, diğer Visual Studio alanlarında toowork devam edebilirsiniz.

bir depolama hesabı tooview kaynaklarında Sunucu Gezgininde hello depolama hesabının düğümünü genişletin. Aşağıdaki alt düğümleri hello görüntülenir:

* Bloblar
* Kuyruklar
* Tablolar

## <a name="work-with-blob-resources"></a>BLOB kaynakların ile çalışma
Hello BLOB'lar düğümü kapsayıcıları seçili hello depolama hesabı için bir listesini görüntüler. BLOB kapsayıcıları blob dosyaları içerir ve bu BLOB'lar klasörler ve alt klasörler halinde düzenleyebilirsiniz. Bkz: [nasıl toouse Blob depolama alanından .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) daha fazla bilgi için.

### <a name="toocreate-a-blob-container"></a>toocreate blob kapsayıcısı
1. Hello için açık hello kısayol menüsü **BLOB'lar** düğümünü ve ardından **Blob kapsayıcısı oluşturmak**.
2. Merhaba, **Blob kapsayıcısı oluşturmak** iletişim kutusunda, hello yeni kapsayıcı hello adını girin.  
3. Tuşuna **ENTER** klavyenizi veya, tıklayın veya dokunun hello ad alanı toosave hello blob kapsayıcısı dışında.
   
   > [!NOTE]
   > Merhaba blob kapsayıcı adı bir sayı (0-9) veya küçük harf (a-z) ile başlamalıdır.
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete blob kapsayıcısı
* Tooremove istediğiniz ve ardından hello blob kapsayıcısı için açık hello kısayol menüsü **silmek**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>bir blob kapsayıcısında bulunan hello öğeleri listesini toodisplay
* Merhaba listesinde bir blob kapsayıcı adı için hello kısayol menüsünü açın ve ardından **açık**.
  
    Bir blob kapsayıcısını Merhaba içeriğine görüntülediğinizde hello blob kapsayıcı görünüm olarak bilinen bir sekmede görüntülenir.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    BLOB'ları üzerinde işlemler hello sağ üst köşesinde hello blob kapsayıcı görünümü hello düğmelerini kullanarak aşağıdaki hello gerçekleştirebilirsiniz:
  
  * Bir filtre değeri girin ve uygulayın
  * Merhaba kapsayıcıdaki blobları Hello listesini yeniler
  * Dosyayı karşıya yükleme
  * Blob silme
    
    > [!NOTE]
    > Bir blob kapsayıcısından bir dosya silindiğinde hello temel alınan dosya silinmez; Bunu yalnızca hello blob kapsayıcısından kaldırır.
    > 
    > 
  * Bir blob açın
  * Bir blob toohello yerel bilgisayara kaydedin

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate bir klasörü veya alt klasör bir blob kapsayıcısında
1. Cloud Explorer'da Hello blob kapsayıcısı seçin. Merhaba kapsayıcı penceresinde hello seçin **karşıya Blob** düğmesi.
   
    ![Blob klasörüne bir dosya karşıya yükleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. Merhaba, **yeni dosyasını karşıya yükle** iletişim kutusunda, hello seçin **Gözat** tooupload istediğiniz ve bir klasör adı hello enter toospecify hello dosya düğmesi **(isteğe bağlı) klasör** kutusu .
   
    Alt klasörleri izleyerek kapsayıcı klasörlerde hello aynı ekleyebilirsiniz yordamı. Bir klasör adı belirtmezseniz, hello dosyası olacaktır toohello üst düzey hello blob kapsayıcısının karşıya yüklendi. Merhaba dosya hello belirtilen hello kapsayıcı klasöründe görünür.
   
    ![Klasör tooa blob kapsayıcısı eklendi](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Merhaba klasörünü çift tıklatın veya ENTER toosee hello hello klasörünün içeriğini tuşuna basın. Merhaba kapsayıcının klasöründe olduğunuzda hello seçerek geri toohello kök hello kapsayıcısının gidebilirsiniz **açık üst dizin** (yukarı ok) düğmesi.

### <a name="toodelete-a-container-folder"></a>toodelete kapsayıcı klasörü
* Tüm hello klasöründeki hello dosyaları sil
  
  > [!NOTE]
  > Blob kapsayıcıları klasörlerde sanal klasörler olduğundan, boş bir klasöre oluşturamaz veya klasör toodelete dosya içeriğini silin. Toodelete hello klasörün tüm içeriğini bir klasör toodelete hello var.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>toofilter BLOB'ları bir kapsayıcıda
Ortak bir önek belirterek görüntülenen hello BLOB'ları filtreleyebilirsiniz.

Merhaba ön eki girin, örneğin, `hello` hello filtre metni kutusuna ve ardından hello seçin **yürütme** (**!**) 'hello' ile başlayan BLOB'lar düğmesi görünür.

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> Merhaba Filtre alanını duyarlıdır ve joker karakterlerle filtreleme desteklemiyor. BLOB'ları yalnızca önek göre filtre uygulanabilir. sanal bir hiyerarşide bir sınırlayıcı tooorganize BLOB'ları kullanıyorsanız hello önek bir sınırlayıcı içerebilir. Örneğin, filtre önek HelloFabric hello / Bu dize ile başlayan tüm BLOB'lar döndürür.
> 
> 

### <a name="toodownload-blob-data"></a>toodownload blob verileri
* İçinde **Cloud Explorer**, bir veya daha fazla BLOB hello kısayol menüsünü açın ve ardından **açmak**, veya hello blob adı seçin ve ardından hello **açmak** düğmesini tıklatın veya çift Merhaba blob adı.
  
    bir blob Yükleme ilerlemesini Hello görünür hello **Azure etkinlik günlüğü** penceresi.
  
    Bu dosya türü için hello varsayılan Düzenleyicisi'nde Hello blob açar. Merhaba işletim sistemi hello dosya türü tanısa hello dosyayı yerel olarak yüklenmiş bir uygulamada açar; Aksi takdirde istenir toochoose hello BLOB hello dosya türü için uygun bir uygulama. bir blob yüklediğinizde oluşturduğunuz hello yerel dosya salt okunur olarak işaretlendi.
  
    BLOB verilerini yerel olarak önbelleğe ve hello karşı blob'un son değişiklik zamanını hello Blob hizmeti olarak işaretli. Son yüklemenizden sonra hello blob güncelleştirilmişse, yeniden yüklenir; Aksi takdirde hello blob hello yerel diskten yüklenir. Varsayılan olarak, bir blob indirilen tooa geçici dizin ' dir. toodownload BLOB'lar tooa belirli dizin, seçili hello için açık hello kısayol menüsü blob adları ve seçin **Kaydet**. Bu şekilde bir blob kaydettiğinizde, hello blob Dosya açılmadı ve hello yerel dosya okuma-yazma özniteliklerle oluşturulur.

### <a name="tooupload-blobs"></a>tooupload BLOB'ları
* Merhaba seçin **karşıya Blob** düğmesini hello kapsayıcı hello blob kapsayıcı görünümünde görüntülemek için açık olduğunda.
  
    Daha fazla dosya tooupload ve herhangi bir türde dosyaları karşıya yükleyebilir ya da birini seçebilirsiniz. Merhaba **Azure etkinlik günlüğü** hello hello karşıya yükleme ilerlemesini gösterir. Hakkında daha fazla bilgi için blob verileriyle toowork bkz [nasıl toouse hello Azure Blob Depolama hizmetinin .NET içinde](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>tooblobs tooview günlükleri aktarılan
* Azure uygulamanızı Azure tanılama toolog veri kullanıyorsanız ve günlükleri tooyour depolama hesabı aktarılan Bu günlükler için Azure tarafından oluşturulan kapsayıcıları görürsünüz. Özellikle dağıtılan tooAzure yüklediyse Server Explorer'da bu günlükleri görüntüleme, uygulamanızın bir kolay bir yolu tooidentify sorunları var. Azure Tanılama hakkında daha fazla bilgi için bkz: [kullanarak Azure tanılama tarafından günlüğü verilerini toplamak](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>bir blob tooget hello URL'si
* Merhaba blob'un kısayol menüsünü açın ve ardından **kopya URL**.

### <a name="tooedit-a-blob"></a>tooedit blob
* Merhaba blob seçin ve ardından hello **açık Blob** düğmesi.
  
    Merhaba dosyası indirilen tooa geçici konuma ve hello yerel bilgisayarda açılır. Değişiklikleri yaptıktan sonra hello blob yeniden yüklemeniz gerekir.

## <a name="work-with-queue-resources"></a>Queue kaynaklarına ile çalışma
Depolama Hizmetleri kuyruklar, bir Azure depolama hesabında barındırılır ve tooallow kullanabilirsiniz, bulut hizmeti rolleri toocommunicate birbirleriyle ve diğer hizmetlerle bir ileti mekanizması geçirme tarafından. Merhaba sıra program aracılığıyla bir bulut hizmeti aracılığıyla ve dış istemcilere web hizmeti üzerinden erişebilirsiniz. Hello sıra Visual Studio'da doğrudan Sunucu Gezgini kullanarak da erişebilirsiniz.

Kuyrukları kullanan bir bulut hizmet geliştirirken, toouse Visual Studio toocreate sıraları istediğiniz ve bunlarla etkileşimli olarak geliştirmek ve kodunuzu test ederken çalışmak.

Sunucu Gezgini'nde, bir depolama hesabında hello sıralarını görüntüleyin, oluşturun ve sırayı silmek, sıra tooview iletileri açın ve iletileri tooa sırası ekleyin. Görüntülemek için bir sıra açtığınızda hello tek bir ileti görüntüleyebilir ve hello sol üst köşede hello düğmelerini kullanarak hello sırası eylemleri aşağıdaki hello gerçekleştirebilirsiniz:

* Merhaba sırasının Hello görünümü yenileyin
* Bir ileti toohello sırası Ekle
* Merhaba en üstteki ileti dequeue
* Clear hello tüm sırası

Görüntü aşağıdaki hello iki ileti içeren bir kuyruk gösterir.

![Bir kuyruğu görüntüleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Kuyruklar Hizmetleri depolama hakkında daha fazla bilgi için bkz: [nasıl yapılır: kullanım hello kuyruk depolama hizmeti](http://go.microsoft.com/fwlink/?LinkID=264702). Kuyruklar depolama hizmetleri için hello web hizmeti hakkında bilgi için bkz [kuyruk hizmeti kavramları](http://go.microsoft.com/fwlink/?LinkId=264788). Visual Studio kullanarak toosend iletileri tooa depolama kuyruğu nasıl hizmetleri hakkında daha fazla bilgi için bkz: [iletiler gönderme tooa depolama hizmetleri kuyruğu](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Depolama Hizmetleri sıraları service bus sıralarından farklıdır. Hizmet veri yolu kuyrukları, konu başlıkları ve abonelikleri service bus kuyruklarını hakkında daha fazla bilgi için bkz.
> 
> 

## <a name="work-with-table-resources"></a>Tablo kaynakları ile çalışma
Hello Azure Table depolama hizmeti büyük miktarlarda yapılandırılmış veri depolar. Merhaba içinden ve dışından hello Azure bulut gelen çağrıları kabul eden bir NoSQL veri deposu kimlik doğrulaması hizmetidir. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.

### <a name="toocreate-a-table"></a>toocreate bir tablo
1. Cloud Explorer'da hello seçin **tabloları** düğümü hello depolama hesabı ve ardından **Create Table**.
2. Merhaba, **Create Table** iletişim kutusunda, hello tablo için bir ad girin.

### <a name="tooview-table-data"></a>tooview tablo verileri
1. Cloud Explorer'da hello açmak **Azure** düğümünü ve ardından açık hello **depolama** düğümü.
2. İlgilendiğiniz ve hello açmak açık hello depolama hesabı düğümünü **tabloları** düğümü toosee tabloların hello depolama hesabı için bir listesi.
3. Bir tablo için hello kısayol menüsünü açın ve ardından **görünüm tablosu**.
   
    ![Çözüm Gezgini'nde bir Azure tablosu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

Merhaba tablo, varlıkları (satırlarda gösterilen) ve (sütunlarda gösterilir) özellikleri tarafından düzenlenir. Örneğin, aşağıdaki çizimde hello hello listelenen varlıkları gösterir **Tablo Tasarımcısı**:

### <a name="tooedit-table-data"></a>tooedit tablo verileri
1. Merhaba, **Tablo Tasarımcısı**, bir varlığın (tek satır) ya da bir özellik (tek bir hücre) hello kısayol menüsünü açın ve ardından **Düzenle**.
   
    ![Ekleme veya Tablo varlığı düzenleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Varlıkları tek bir tablodaki gerekli toohave hello aynı özellikleri (sütunları) kümesi değil. Görüntüleme ve tablo verileri düzenleme kısıtlamaları aşağıdaki göz hello unutmayın.
   
   * Görüntüleyemez veya ikili verileri düzenleme (tür byte[]), ancak saklayabilir, bir tablodaki.
   * Merhaba düzenleyemezsiniz **PartitionKey** veya **RowKey** Azure tablo depolaması bu işlemi desteklemediğinden, değerleri.
   * Zaman damgası adlı bir özellik oluşturulamıyor, Azure depolama hizmetleri, bu ada sahip bir özelliğini kullanın.
   * Bir tarih saat değeri girerseniz, uygun toohello bölge ve dil ayarları bilgisayarınızın biçimde izlemeniz gereken (örneğin, GG/AA/YYYY SS: dd: [AM | PM] ABD için İngilizce).

### <a name="tooadd-entities"></a>tooadd varlıklar
1. Merhaba, **Tablo Tasarımcısı**, hello seçin **varlık Ekle** düğmesi.
   
    ![Varlık ekleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. Merhaba, **varlık Ekle** iletişim kutusunda, hello hello değerlerini girin **PartitionKey** ve **RowKey** özellikleri.
   
    ![Varlık Ekle iletişim kutusu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Merhaba varlık silin ve yeniden ekleyin sürece hello iletişim kutusunu kapattıktan sonra bunları değiştirilemiyor çünkü dikkatle hello değerleri girin.

### <a name="toofilter-entities"></a>toofilter varlıklar
Merhaba Sorgu Oluşturucusu kullanıyorsanız, bir tabloda görünen varlıkları hello kümesinin özelleştirebilirsiniz.

1. tooopen hello Sorgu Oluşturucusu, görüntülemek için bir tablo açın.
2. Merhaba Tablo görünümünün araç çubuğunda Hello Sorgu Oluşturucusu düğmesini seçin.
   
    Merhaba **Sorgu Oluşturucusu** iletişim kutusu görüntülenir. Merhaba aşağıdaki şekilde oluşturulmakta olan bir sorgu hello Sorgu Oluşturucusu'nda gösterilmektedir.
   
    ![Sorgu Oluşturucusu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Bitirdiğinizde hello sorgu oluşturma, hello iletişim kutusunu kapatın. hello sorgu Hello elde edilen metin biçiminde bir metin kutusunda WCF Veri Hizmetleri filtre olarak görünür.
4. toorun hello sorgu, hello yeşil üçgenle simgesini seçin.
   
    Hello görünür varlık verilerini de filtre uygulayabilirsiniz **Tablo Tasarımcısı** , doğrudan hello filtre alanına bir WCF Veri Hizmetleri filtre dizesi girin. Bu tür bir dize benzer tooa SQL WHERE yan tümcesi ancak toohello sunucu bir HTTP isteği gönderilir. Nasıl tooconstruct filtre dizeleri hakkında daha fazla bilgi için bkz: [oluşturma filtre dizeleri hello Tablo Tasarımcısı için](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Merhaba aşağıdaki resimde bir geçerli filtre dizesi örneği gösterilmektedir:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Depolama veri yenileme
Sunucu Gezgini bir depolama hesabından tooor verileri bağlandığında, işlem hello işlemi toocomplete tooa dakika sürebilir. Bağlanamıyorsanız, hello işlemi zaman aşımına olabilir. Veriler alınır, ancak Visual Studio'nun diğer bölümlerinde toowork devam edebilirsiniz. çok uzun sürüyorsa toocancel hello işlemi seçin hello **Yenilemeyi Durdur** hello Sunucu Gezgini araç çubuğunda.

#### <a name="toorefresh-blob-container-data"></a>toorefresh blob kapsayıcı verileri
* Select hello **BLOB'lar** düğümün altında **depolama** ve hello seçin **yenileme** hello Sunucu Gezgini araç çubuğunda.
* toorefresh hello görüntülenir, BLOB'ları listesi seçin hello **yürütme** düğmesi.

#### <a name="toorefresh-table-data"></a>toorefresh tablo verileri
* Select hello **tabloları** düğümün altında **depolama** ve hello seçin **yenileme** düğmesi.
* toorefresh hello hello görüntülenen varlıkların listesi **Tablo Tasarımcısı**, hello seçin **yürütme** hello düğmesinde **Tablo Tasarımcısı**.

#### <a name="toorefresh-queue-data"></a>toorefresh sırası verileri
* Select hello **sıraları** düğümü ve hello seçin **yenileme** düğmesi.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>bir depolama hesabında toorefresh tüm öğeler
* Merhaba hesap adı seçin ve ardından hello **yenileme** için Sunucu Gezgini hello araç çubuğundan düğme.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Sunucu Gezgini kullanarak depolama hesapları ekleme
İki yolu vardır tooadd depolama hesapları Sunucu Gezgini kullanarak. Azure aboneliğinizde yeni bir depolama hesabı oluşturabilir veya varolan bir depolama hesabı ekleyebilirsiniz.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate Sunucu Gezgini kullanarak yeni bir depolama hesabı
1. Sunucu Gezgininde hello Depolama düğümü için hello kısayol menüsünü açın ve ardından depolama hesabı oluştur seçin.
   
    ![Yeni bir Azure depolama hesabı oluşturma](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Bilgi hello hello yeni depolama hesabı için aşağıdaki hello girin veya seçin **depolama hesabı oluştur** iletişim kutusu.
   
   * hello Azure aboneliği toowhich tooadd hello depolama hesabı istiyor.
   * Merhaba yeni depolama hesabı için toouse istediğiniz hello adı.
   * Merhaba bölge veya benzeşim grubunda (örneğin, Batı ABD veya Doğu Asya).
   * Merhaba türü çoğaltmasını coğrafi olarak yedekli gibi hello depolama hesabı için toouse istiyor.
3. **Oluştur**’u seçin.
   
    Merhaba yeni depolama hesabı görünür hello **depolama** Çözüm Gezgini'nde listesi.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach Sunucu Gezgini kullanarak var olan bir depolama hesabı
1. Sunucu Gezgininde hello Azure Depolama düğümü için hello kısayol menüsünü açın ve ardından **harici depolama ekleme**.
   
    ![Varolan bir depolama hesabı ekleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Bilgi hello hello yeni depolama hesabı için aşağıdaki hello girin veya seçin **depolama hesabı oluştur** iletişim kutusu.
   
   * Merhaba hello tooattach istediğiniz var olan depolama hesabının adıdır. Bir ad girin veya hello listeden seçin.
   * başlangıç anahtarı hello için depolama hesabı seçili. Bir depolama hesabı seçtiğinizde bu değer genellikle sizin için sağlanır. Visual Studio tooremember hello depolama hesabı anahtarı istiyorsanız hello anımsa hesap anahtar kutusunu seçin.
   * Merhaba Protokolü toouse tooconnect toohello depolama hesabı, örneğin HTTP, HTTPS veya özel bir uç noktası. Bkz: [tooConfigure bağlantı dizeleri nasıl](https://msdn.microsoft.com/library/azure/ee758697.aspx) özel uç noktaları hakkında daha fazla bilgi.

### <a name="tooview-hello-secondary-endpoints"></a>tooview hello ikincil uç noktaları
* Hello kullanarak bir depolama hesabı oluşturduysanız **okuma erişimli coğrafi olarak yedekli** çoğaltma seçeneği, ikincil uç noktalarını görüntüleyebilirsiniz. Merhaba hesap adı hello kısayol menüsünü açın ve ardından **özellikleri**.
  
    ![Depolama ikincil uç noktaları](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove Sunucu Gezgini'nden bir depolama hesabı
* Sunucu Gezgininde hello hesap adı hello kısayol menüsünü açın ve ardından **silmek**. Bir depolama hesabı silerseniz, bu hesap için kaydedilen tüm anahtar bilgileri de kaldırılır.
  
  > [!NOTE]
  > Server Explorer'dan bir depolama hesabı silerseniz, depolama hesabınız veya onu içeren herhangi bir veri etkilemez; Server Explorer'dan hello başvuru yalnızca kaldırır. toopermanently bir depolama hesabını silmek, hello kullan [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Sonraki adımlar
toolearn hakkında daha fazla Azure storage hizmetleri kullanmak için bkz: [hello Azure depolama hizmetlerine erişilmesi](https://msdn.microsoft.com/library/azure/ee405490.aspx).

