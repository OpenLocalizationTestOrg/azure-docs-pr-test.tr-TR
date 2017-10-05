---
title: "Göz atma ve Sunucu Gezgini ile depolama kaynaklarını yönetme | Microsoft Docs"
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
ms.openlocfilehash: 43ab501c69c0c1e3271dbfcf08e5342a3507ab82
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Göz atma ve Sunucu Gezgini ile depolama kaynaklarını yönetme
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Genel Bakış
Microsoft Visual Studio için Azure araçlarını yüklediyseniz, depolama hesapları blob, kuyruk ve tablo verileri için Azure görüntüleyebilirsiniz. Sunucu Gezgininde Azure Storage yerel depolama öykünücüsü hesabınızı ve diğer Azure storage hesaplarınızı verileri gösterir.

Sunucu Gezgini Visual Studio'nun menü çubuğunda, görüntülemeyi **Görünüm**, **Sunucu Gezgini**. Depolama düğümü her Azure aboneliği veya bağlı olduğunuz sertifikanın altında mevcut tüm depolama hesaplarını gösterir. Depolama hesabınız görünmüyorsa, bu yönergeleri izleyerek ekleyebileceğiniz [bu konunun devamındaki](#add-storage-accounts-by-using-server-explorer).

Azure SDK 2.7 başlayarak, yeni Cloud Explorer görüntülemek ve Azure kaynaklarınızı yönetmek için de kullanabilirsiniz. Bkz: [bulut Gezgini ile Azure kaynaklarını yönetme](vs-azure-tools-resources-managing-with-cloud-explorer.md) daha fazla bilgi için.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Visual Studio'da depolama kaynakları görüntülemek ve yönetmek
Sunucu Gezgini otomatik olarak depolama öykünücüsü hesabınızda BLOB, kuyruklar ve tablolar listesini gösterir. Depolama öykünücüsü hesabı Depolama düğümü altındaki Server Explorer'da listelenir **geliştirme** düğümü.

Depolama öykünücüsü hesabın kaynakları görmek için genişletme **geliştirme** düğümü. ' Nı depolama öykünücüsünü başlatılmış kurmadı varsa **geliştirme** düğümü, onu otomatik olarak başlatılacak. Bu işlem birkaç saniye alabilir. Depolama öykünücüsü başlatılırken diğer Visual Studio alanlarında çalışmaya devam edebilirsiniz.

Bir depolama hesabında kaynakları görüntülemek için Sunucu Gezgini depolama hesabının düğümünü genişletin. Aşağıdaki alt düğümleri görüntülenir:

* Bloblar
* Kuyruklar
* Tablolar

## <a name="work-with-blob-resources"></a>BLOB kaynakların ile çalışma
BLOB'lar düğümü kapsayıcıları seçilen depolama hesabı için bir listesini görüntüler. BLOB kapsayıcıları blob dosyaları içerir ve bu BLOB'lar klasörler ve alt klasörler halinde düzenleyebilirsiniz. Bkz: [Blob Storage kullanma konusunda](storage/blobs/storage-dotnet-how-to-use-blobs.md) daha fazla bilgi için.

### <a name="to-create-a-blob-container"></a>Bir blob kapsayıcısını oluşturmak için
1. Kısayol menüsünü açın **BLOB'lar** düğümünü ve ardından **Blob kapsayıcısı oluşturmak**.
2. İçinde **Blob kapsayıcısı oluşturmak** iletişim kutusunda, yeni kapsayıcının adını girin.  
3. Tuşuna **ENTER** klavyenizi veya, tıklayın veya dokunun blob kapsayıcısında kaydetmek için ad alanı dışında.
   
   > [!NOTE]
   > Blob kapsayıcı adı bir sayı (0-9) veya küçük harf (a-z) ile başlamalıdır.
   > 
   > 

### <a name="to-delete-a-blob-container"></a>Bir blob kapsayıcısını silmek için
* Kaldırın ve ardından istediğiniz blob kapsayıcısı için kısayol menüsünü açın **silmek**.

### <a name="to-display-a-list-of-the-items-contained-in-a-blob-container"></a>Bir blob kapsayıcısında bulunan öğeleri listesini görüntülemek için
* Listeden bir blob kapsayıcı adı için kısayol menüsünü açın ve ardından **açık**.
  
    Bir blob kapsayıcı içeriğini görüntülediğinizde, blob kapsayıcı görünüm olarak bilinen bir sekmede görüntülenir.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Blob kapsayıcı görünümü sağ üst köşesindeki düğmeleri kullanarak BLOB'ları üzerinde aşağıdaki işlemleri gerçekleştirebilirsiniz:
  
  * Bir filtre değeri girin ve uygulayın
  * BLOB'ları kapsayıcıda listesini yeniler
  * Dosyayı karşıya yükleme
  * Blob silme
    
    > [!NOTE]
    > Bir blob kapsayıcısından bir dosya silindiğinde, temel alınan dosya silinmez; Bunu yalnızca blob kapsayıcısından kaldırır.
    > 
    > 
  * Bir blob açın
  * Bir blob yerel bilgisayara kaydedin

### <a name="to-create-a-folder-or-subfolder-in-a-blob-container"></a>Bir klasörü veya alt klasör bir blob kapsayıcısında oluşturmak için
1. Blob kapsayıcısı Cloud Explorer'da seçin. Kapsayıcı penceresinde seçin **karşıya Blob** düğmesi.
   
    ![Blob klasörüne bir dosya karşıya yükleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. İçinde **yeni dosyasını karşıya yükle** iletişim kutusunda, seçin **Gözat** karşıya yüklemek istediğiniz dosyayı belirtmek için düğmesine tıklayın ve ardından bir klasör adı girin **(isteğe bağlı) klasör** kutusu.
   
    Aynı yordamı izleyerek kapsayıcı klasörlerde alt klasörler ekleyebilirsiniz. Bir klasör adı belirtmezseniz, dosyanın en üst düzeye blob kapsayıcısının yüklenecek. Belirtilen klasöre kapsayıcısında dosya görünür.
   
    ![Klasör bir blob kapsayıcıya eklendi](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Klasörü çift tıklatın veya klasörün içeriğini görmek için ENTER tuşuna basın. Kapsayıcının klasöründe olduğunuzda seçerek kapsayıcısının kök geri gidebilirsiniz **açık üst dizin** (yukarı ok) düğmesi.

### <a name="to-delete-a-container-folder"></a>Bir kapsayıcı klasörü silmek için
* Klasördeki dosyaların tümünü Sil
  
  > [!NOTE]
  > Blob kapsayıcıları klasörlerde sanal klasörler olduğundan, boş bir klasöre oluşturamaz veya dosya içeriğini silmek için bir klasör silebilirsiniz. Klasörünü silmek için bir klasörün tüm içeriğini silmeniz gerekir.
  > 
  > 

### <a name="to-filter-blobs-in-a-container"></a>BLOB'ları bir kapsayıcıda filtre uygulamak için
Ortak bir önek belirterek görüntülenen BLOB'ları filtreleyebilirsiniz.

Önek girerseniz, örneğin, `hello` filtre metin kutusuna ve ardından **yürütme** (**!**) 'hello' ile başlayan BLOB'lar düğmesi görünür.

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> Filtre alanına duyarlıdır ve joker karakterlerle filtreleme desteklemiyor. BLOB'ları yalnızca önek göre filtre uygulanabilir. Sanal bir hiyerarşideki BLOB'lar düzenlemek için bir sınırlayıcı kullanıyorsanız öneki bir sınırlayıcı içerebilir. Örneğin, HelloFabric ön ekini temel filtreleme / Bu dize ile başlayan tüm BLOB'lar döndürür.
> 
> 

### <a name="to-download-blob-data"></a>BLOB verilerini yüklemek için
* İçinde **Cloud Explorer**, bir veya daha fazla BLOB'lar için kısayol menüsünü açın ve ardından **açmak**, veya blob adı seçin ve ardından **açmak** düğmesini veya blob adına çift tıklayın.
  
    Bir blob Yükleme ilerlemesini görünür **Azure etkinlik günlüğü** penceresi.
  
    Bu dosya türü için varsayılan düzenleyicisinde blob açar. İşletim sistemi dosya türü tanısa, dosyayı yerel olarak yüklenmiş bir uygulamada açar; Aksi takdirde, blob dosya türü için uygun bir uygulama seçin istenir. Bir blob yüklediğinizde oluşturduğunuz yerel dosya salt okunur olarak işaretlendi.
  
    BLOB verilerini yerel olarak önbelleğe ve blob'un son değişiklik zamanını Blob hizmetinde karşılaştırılarak. Son yüklemenizden sonra blob güncelleştirilmişse, yeniden yüklenir; Aksi takdirde, blob yerel diskten yüklenir. Varsayılan olarak, bir blob geçici bir dizine yüklenir. Belirli bir dizine BLOB indirmek için seçilen blob adları için kısayol menüsünü açın ve seçin **Kaydet**. Bu şekilde bir blob kaydettiğinizde, blob Dosya açılmadı ve yerel dosya okuma-yazma özniteliklerle oluşturulur.

### <a name="to-upload-blobs"></a>BLOB karşıya yüklemek için
* Seçin **karşıya Blob** düğmesini kapsayıcı blob kapsayıcı görünümünde görüntülemek için açık olduğunda.
  
    Karşıya yüklemek için bir veya daha fazla seçebilir ve tüm dosya türlerini karşıya yükleyebilirsiniz. **Azure etkinlik günlüğü** karşıya yükleme ilerlemesini gösterir. Blob verilerle çalışma hakkında daha fazla bilgi için bkz: [.NET ile Azure Blob Depolama hizmetinin kullanmayı](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="to-view-logs-transferred-to-blobs"></a>BLOB'larını transfer günlükleri görüntülemek için
* Azure Tanılama verileri Azure uygulamanızı günlüğe kaydetmek için kullandığınız ve depolama hesabınıza günlükleri aktarılmış, Azure tarafından Bu günlükler için oluşturulan kapsayıcıları görürsünüz. Özellikle Azure dağıtıldıktan varsa Server Explorer'da bu günlükleri görüntüleme, uygulamanızın sorunları tanımlamak için kolay bir yoludur. Azure Tanılama hakkında daha fazla bilgi için bkz: [kullanarak Azure tanılama tarafından günlüğü verilerini toplamak](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="to-get-the-url-for-a-blob"></a>URL için bir blob almak için
* Blob'un kısayol menüsünü açın ve ardından **kopya URL**.

### <a name="to-edit-a-blob"></a>Bir blob düzenlemek için
* Blob seçin ve ardından **açık Blob** düğmesi.
  
    Dosyanın geçici bir konuma indirilir ve yerel bilgisayarda açılır. Değişiklikleri yaptıktan sonra blob yeniden yüklemeniz gerekir.

## <a name="work-with-queue-resources"></a>Queue kaynaklarına ile çalışma
Depolama Hizmetleri sorguları bir Azure depolama hesabında barındırılır ve bulut hizmeti rolleri bir ileti mekanizması geçirme tarafından birbirleriyle ve diğer hizmetleri ile iletişim kurmak izin vermek için kullanabilirsiniz. Sıranın program aracılığıyla bir bulut hizmeti aracılığıyla ve dış istemcilere web hizmeti üzerinden erişebilirsiniz. Sıranın Visual Studio'da doğrudan Sunucu Gezgini kullanarak da erişebilirsiniz.

Kuyrukları kullanan bir bulut hizmet geliştirirken sıraları oluşturmak ve bunlarla etkileşimli olarak geliştirmek ve kodunuzu test ederken çalışmak için Visual Studio kullanmak isteyebilirsiniz.

Sunucu Gezgini'nde, bir depolama hesabında sıralarını görüntüleyin, oluşturun ve sırayı silmek, kendi iletilerini görüntülemek için bir sırayı açmak ve iletileri kuyruğa Ekle. Bir kuyruk görüntüleme için açtığınızda, tek bir ileti görüntüleyebilir ve sol üst köşede düğmelerini kullanarak sıra üzerinde aşağıdaki eylemleri gerçekleştirebilirsiniz:

* Kuyruk görünümü yenileyin
* Kuyruğa bir ileti Ekle
* En üstteki ileti dequeue
* Tüm sıranın temizleyin

Aşağıdaki görüntü iki ileti içeren bir kuyruk gösterir.

![Bir kuyruğu görüntüleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Kuyruklar Hizmetleri depolama hakkında daha fazla bilgi için bkz: [nasıl yapılır: kuyruk depolama hizmeti kullanmak](http://go.microsoft.com/fwlink/?LinkID=264702). Kuyruklar depolama hizmetleri için web hizmeti hakkında bilgi için bkz [kuyruk hizmeti kavramları](http://go.microsoft.com/fwlink/?LinkId=264788). Visual Studio kullanarak bir depolama hizmetleri sıraya ileti gönderme hakkında daha fazla bilgi için bkz: [depolama hizmetleri kuyruğuna iletiler gönderme](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Depolama Hizmetleri sıraları service bus sıralarından farklıdır. Hizmet veri yolu kuyrukları, konu başlıkları ve abonelikleri service bus kuyruklarını hakkında daha fazla bilgi için bkz.
> 
> 

## <a name="work-with-table-resources"></a>Tablo kaynakları ile çalışma
Azure Table Storage hizmeti büyük miktarlarda yapısal veriyi depolar. Bu hizmet, Azure bulutunun içinden ve dışından gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL olmayan veri deposudur. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.

### <a name="to-create-a-table"></a>Bir tablo oluşturmak için
1. Cloud Explorer'da seçin **tabloları** düğümü depolama hesabı ve ardından **Create Table**.
2. İçinde **Create Table** iletişim kutusunda, tablo için bir ad girin.

### <a name="to-view-table-data"></a>Tablo verileri görüntülemek için
1. Cloud Explorer'da açın **Azure** düğümünü ve ardından açın **depolama** düğümü.
2. İlginizi çekiyor mu ve açın depolama hesabı düğümünü açın **tabloları** depolama hesabı için tabloların bir listesini görmek için düğüm.
3. Bir tablo için kısayol menüsünü açın ve ardından **görünüm tablosu**.
   
    ![Çözüm Gezgini'nde bir Azure tablosu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

Tablo, varlıkları (satırlarda gösterilen) ve (sütunlarda gösterilir) özellikleri tarafından düzenlenir. Örneğin, aşağıda listelenen varlıkları gösterilmiştir **Tablo Tasarımcısı**:

### <a name="to-edit-table-data"></a>Tablo verisi düzenlemek için
1. İçinde **Tablo Tasarımcısı**, bir varlığın (tek satır) ya da bir özellik (tek bir hücre) için kısayol menüsünü açın ve ardından **Düzenle**.
   
    ![Ekleme veya Tablo varlığı düzenleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Tek bir tabloyu varlıklarda özellikleri (sütunları) aynı kümesine sahip gerekli değildir. Tablo veri görüntüleme ve düzenleme aşağıdaki kısıtlamaları göz önünde bulundurun.
   
   * Görüntüleyemez veya ikili verileri düzenleme (tür byte[]), ancak saklayabilir, bir tablodaki.
   * Düzenleyemezsiniz **PartitionKey** veya **RowKey** Azure tablo depolaması bu işlemi desteklemediğinden, değerleri.
   * Zaman damgası adlı bir özellik oluşturulamıyor, Azure depolama hizmetleri, bu ada sahip bir özelliğini kullanın.
   * Bir tarih saat değeri girerseniz, bilgisayarınızın bölge ve dil ayarları uygun biçimde izlemeniz gereken (örneğin, GG/AA/YYYY SS: dd: [AM | PM] ABD için İngilizce).

### <a name="to-add-entities"></a>Varlıkları eklemek için
1. İçinde **Tablo Tasarımcısı**, seçin **varlık Ekle** düğmesi.
   
    ![Varlık ekleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. İçinde **varlık Ekle** iletişim kutusunda, değerlerini girin **PartitionKey** ve **RowKey** özellikleri.
   
    ![Varlık Ekle iletişim kutusu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Varlık silin ve yeniden ekleyin sürece iletişim kutusunu kapattıktan sonra bunları değiştirilemiyor çünkü dikkatle değerleri girin.

### <a name="to-filter-entities"></a>Varlıkları filtre uygulamak için
Sorgu Oluşturucusu'nu kullanırsanız, bir tabloda görünen varlıkları kümesinin özelleştirebilirsiniz.

1. Sorgu Oluşturucusu'nu açmak için bir tablo görüntülemek için açın.
2. Tablo görünümünün araç çubuğunda Sorgu Oluşturucusu düğmesini seçin.
   
    **Sorgu Oluşturucusu** iletişim kutusu görüntülenir. Aşağıdaki çizimde oluşturulmakta olan bir sorgu Sorgu Oluşturucu'da gösterir.
   
    ![Sorgu Oluşturucusu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Bitirdiğinizde, sorgu oluşturma iletişim kutusunu kapatın. Sorgu sonuç metin biçiminde bir metin kutusuna bir WCF Veri Hizmetleri filtre olarak görünür.
4. Sorguyu çalıştırmak için yeşil üçgenle simgesini seçin.
   
    Görünür varlık verilerini de filtre uygulayabilirsiniz **Tablo Tasarımcısı** , doğrudan filtre alanına bir WCF Veri Hizmetleri filtre dizesi girin. Bu tür bir dize bir SQL WHERE yan tümcesine benzer, ancak sunucuya bir HTTP isteği olarak gönderilir. Filtre dizeleri oluşturma hakkında daha fazla bilgi için bkz: [oluşturma filtre dizeleri Tablo Tasarımcısı için](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Aşağıdaki çizimde bir geçerli filtre dizesi örneği gösterilmektedir:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Depolama veri yenileme
Sunucu Gezgini bağlandığı veya bir depolama hesabından verileri alır, bu işlemin tamamlanması için bir dakika sürebilir. Bağlanamıyorsanız, işlemi zaman aşımına olabilir. Veriler alınır, ancak Visual Studio'nun diğer bölümlerinde çalışmaya devam edebilirsiniz. Çok uzun sürüyorsa işlemi iptal etmeyi seçmediğiniz **Yenilemeyi Durdur** Sunucu Gezgini araç çubuğunda.

#### <a name="to-refresh-blob-container-data"></a>BLOB kapsayıcı verileri yenilemek için
* Seçin **BLOB'lar** düğümün altında **depolama** ve **yenileme** Sunucu Gezgini araç çubuğunda.
* Görüntülenen BLOB'lar listesini yenilemek için tercih **yürütme** düğmesi.

#### <a name="to-refresh-table-data"></a>Tablo verileri yenilemek için
* Seçin **tabloları** düğümün altında **depolama** ve **yenileme** düğmesi.
* Görüntülenen varlıklar listesini yenilemek için **Tablo Tasarımcısı**, seçin **yürütme** düğmesini **Tablo Tasarımcısı**.

#### <a name="to-refresh-queue-data"></a>Sıra verileri yenilemek için
* Seçin **sıraları** düğümünü ve ardından **yenileme** düğmesi.

#### <a name="to-refresh-all-items-in-a-storage-account"></a>Bir depolama hesabındaki tüm öğeleri yenilemek için
* Hesap adı seçin ve ardından **yenileme** Sunucu Gezgini için araç çubuğunda.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Sunucu Gezgini kullanarak depolama hesapları ekleme
Sunucu Gezgini kullanarak depolama hesapları eklemek için iki yolu vardır. Azure aboneliğinizde yeni bir depolama hesabı oluşturabilir veya varolan bir depolama hesabı ekleyebilirsiniz.

#### <a name="to-create-a-new-storage-account-by-using-server-explorer"></a>Sunucu Gezgini kullanarak yeni bir depolama hesabı oluşturmak için
1. Sunucu Gezgini'nde, Depolama düğümü için kısayol menüsünü açın ve ardından depolama hesabı oluştur seçin.
   
    ![Yeni bir Azure depolama hesabı oluşturma](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Yeni depolama hesabı için aşağıdaki bilgileri girin veya seçin **depolama hesabı oluştur** iletişim kutusu.
   
   * Depolama hesabı eklemek istediğiniz Azure aboneliği.
   * Yeni depolama hesabı için kullanmak istediğiniz adı.
   * Bölge veya benzeşim grubunda (örneğin, Batı ABD veya Doğu Asya).
   * Coğrafi olarak yedekli gibi depolama hesabı için kullanmak istediğiniz çoğaltma türü.
3. **Oluştur**’u seçin.
   
    Yeni depolama hesabı görünür **depolama** Çözüm Gezgini'nde listesi.

#### <a name="to-attach-an-existing-storage-account-by-using-server-explorer"></a>Sunucu Gezgini kullanarak mevcut bir depolama hesabını eklemek için
1. Sunucu Gezgini'nde, Azure Depolama düğümü için kısayol menüsünü açın ve ardından **harici depolama ekleme**.
   
    ![Varolan bir depolama hesabı ekleme](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Yeni depolama hesabı için aşağıdaki bilgileri girin veya seçin **depolama hesabı oluştur** iletişim kutusu.
   
   * Eklemek istediğiniz varolan depolama hesabı adı. Bir ad girin veya listeden seçin.
   * Seçilen depolama hesabı anahtarı. Bir depolama hesabı seçtiğinizde bu değer genellikle sizin için sağlanır. Depolama hesap anahtarını anımsa için Visual Studio istiyorsanız anımsa hesap anahtar kutusunu seçin.
   * Depolama hesabı, örneğin HTTP, HTTPS veya özel bir uç nokta bağlanmak için kullanılacak protokolü. Bkz: [yapılandırmak bağlantı dizeleri nasıl](https://msdn.microsoft.com/library/azure/ee758697.aspx) özel uç noktaları hakkında daha fazla bilgi.

### <a name="to-view-the-secondary-endpoints"></a>İkincil uç noktaları görüntülemek için
* Kullanarak bir depolama hesabı oluşturduysanız **okuma erişimli coğrafi olarak yedekli** çoğaltma seçeneği, ikincil uç noktalarını görüntüleyebilirsiniz. Hesap adı için kısayol menüsünü açın ve ardından **özellikleri**.
  
    ![Depolama ikincil uç noktaları](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="to-remove-a-storage-account-from-server-explorer"></a>Server Explorer'dan bir depolama hesabını kaldırmak için
* Sunucu Gezgini'nde, hesap adı için kısayol menüsünü açın ve ardından **silmek**. Bir depolama hesabı silerseniz, bu hesap için kaydedilen tüm anahtar bilgileri de kaldırılır.
  
  > [!NOTE]
  > Server Explorer'dan bir depolama hesabı silerseniz, depolama hesabınız veya onu içeren herhangi bir veri etkilemez; Server Explorer'dan yalnızca başvuru kaldırır. Bir depolama hesabı kalıcı olarak silmek için kullanın [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Sonraki adımlar
Azure storage Hizmetleri kullanma hakkında daha fazla bilgi edinmek için [Azure depolama hizmetlerine erişilmesi](https://msdn.microsoft.com/library/azure/ee405490.aspx).

