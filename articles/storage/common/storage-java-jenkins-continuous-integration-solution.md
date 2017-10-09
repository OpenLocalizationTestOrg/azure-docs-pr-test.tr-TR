---
title: "aaaUsing Jenkins sürekli tümleştirme çözümü olan Azure Storage | Microsoft Docs"
description: "Bu öğretici Göster nasıl toouse hello Azure blob hizmeti için bir havuz oluşturmak gibi bir Jenkins sürekli tümleştirme çözümü tarafından oluşturulan yapıları."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 853c0c6c028596b3057bdc1dbbc59a9415c0fb77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Jenkins Sürekli Tümleştirme çözümüyle Azure Depolama'yı kullanma
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki bilgileri nasıl toouse Blob Depolama Jenkins sürekli tümleştirme (CI) çözümü tarafından oluşturulan yapı yapılarının deposu olarak ya da indirilebilir dosyaları toobe kaynağı olarak bir yapı işleminde kullanılan gösterir. Olabilir, bu yararlı bulabileceğiniz hello senaryolardan biri, (Java veya diğer dilleri kullanarak) Çevik Geliştirme ortamında kodlama, üzerinde sürekli tümleştirme derlemeleri çalıştırıyorsanız ve derleme yapıtları için bir depo gerekir, böylelikle , örneğin, müşterilerinizin diğer kuruluş üyeleriyle paylaşmak ya da bir arşiv tutmak. Yapı hello bir parçası olarak giriş, yapı işinizi diğer dosyaları, örneğin, bağımlılıkları toodownload gerektirdiğinde, başka bir senaryodur.

Bu öğreticide, Azure depolama eklentisi hello Jenkins Microsoft tarafından kullanılabilir hale CI için kullanır.

## <a name="overview-of-jenkins"></a>Jenkins genel bakış
Jenkins etkinleştirir sürekli tümleştirme tooeasily kod değişikliklerini tümleştirmek ve sahip geliştiriciler sağlayarak yazılım projenin üretilen otomatik olarak ve sık, böylece hello verimliliğini hello geliştiricilerin oluşturur. Derlemeleri sürümlü ve derleme yapıları karşıya yüklenen toovarious depoları olabilir. Bu konu, nasıl toouse Azure blob depolama hello derleme yapıları hello deposu olarak gösterilir. Ayrıca, nasıl toodownload bağımlılıklar Azure blob depolama gösterir.

Jenkins hakkında daha fazla bilgi bulunabilir [karşılamak Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-hello-blob-service"></a>Merhaba Blob hizmeti kullanmanın yararları
Çevik Geliştirme derleme yapıtları hello Blob hizmeti toohost kullanmanın avantajları şunlardır:

* Yüksek kullanılabilirlik derleme yapıları ve/veya indirilebilir bağımlılıkları.
* Jenkins CI çözümünüzü derleme yapıtları yüklediğinde performans.
* Müşterileri ve ortakları derleme yapıtları yüklediğinizde performans.
* Kullanıcı erişim ilkeleri, anonim erişim, sona erme tabanlı paylaşılan erişim imzası erişim, özel arasında bir seçim ile üzerinden erişim, vb. denetler.

## <a name="prerequisites"></a>Ön koşullar
Toouse hello Blob hizmeti Jenkins CI çözümünüzle birlikte hello:

* Jenkins sürekli tümleştirme çözümü.
  
    Jenkins CI çözüm yoksa, yöntem aşağıdaki hello kullanarak bir Jenkins CI çözüm çalıştırabilirsiniz:
  
  1. Java etkin bir makinede jenkins.war gelen indirme <http://jenkins-ci.org>.
  2. Bir komut jenkins.war içeren açılan toohello klasörü olan isteminde çalıştırın:
     
      `java -jar jenkins.war`

  3. Tarayıcınızda açın `http://localhost:8080/`. Bu şunları yapacaksınız hello Jenkins Pano açar tooinstall kullanın ve hello Azure depolama eklentisi yapılandırın.
     
      Tipik bir Jenkins CI çözüm yukarı toorun bir hizmet olarak ayarlanır, ancak hello Jenkins war hello komut satırında çalıştıran Bu öğretici için yeterli olacaktır.
* Bir Azure hesabı. Azure hesabı için kaydolabilirsiniz <http://www.azure.com>.
* Bir Azure depolama hesabı. Bir depolama hesabı zaten sahip değilseniz, birini oluşturabilirsiniz hello adımları kullanarak [depolama hesabı oluşturma](../common/storage-create-storage-account.md#create-a-storage-account).
* Merhaba Jenkins CI çözüm aşina önerilir ancak gerekli değildir, hello aşağıdaki içeriği kullanacak şekilde hello Blob hizmeti Jenkins CI için depo olarak kullanırken gerekli adımları hello temel örnek tooshow yapı yapıları.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>Nasıl toouse hello Jenkins CI Blob hizmetiyle
toouse hello Blob hizmeti Jenkins ile tooinstall gerekir Azure depolama eklentisi Merhaba, depolama hesabınız hello eklentisi toouse yapılandırmak ve derleme yapıları tooyour depolama hesabınız yükleyen oluşturma sonrası eylem oluşturun. Aşağıdaki bölümlerde hello adımları açıklanmaktadır.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Nasıl tooinstall hello Azure depolama eklentisi
1. Merhaba Jenkins Pano içinde tıklatın **yönetmek Jenkins**.
2. Merhaba, **yönetmek Jenkins** sayfasında, **eklentileri yönetme**.
3. Merhaba tıklatın **kullanılabilir** sekmesi.
4. Merhaba, **yapı Uploaders** bölümünde, onay **Microsoft Azure depolama eklentisi**.
5. Ya da tıklatın **yeniden yükleme** veya **şimdi yükleyip yeniden başlatma sonrasında**.
6. Jenkins yeniden başlatın.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Nasıl tooconfigure hello Azure depolama eklentisi toouse depolama hesabınız
1. Merhaba Jenkins Pano içinde tıklatın **yönetmek Jenkins**.
2. Merhaba, **yönetmek Jenkins** sayfasında, **yapılandırma sistem**.
3. Merhaba, **Microsoft Azure depolama hesabı Yapılandırması** bölümü:
   1. Merhaba elde edebilirsiniz, depolama hesabı adı girin [Azure Portal](https://portal.azure.com).
   2. Depolama hesabı anahtarınızı, hello da elde edilebilir girin [Azure Portal](https://portal.azure.com).
   3. Merhaba varsayılan değeri kullanın **Blob Hizmeti uç noktası URL'si** hello genel Azure bulut kullanıyorsanız. Farklı bir Azure bulut kullanıyorsanız, hello uç noktası belirtilen hello kullan [Azure Portal](https://portal.azure.com) depolama hesabınız için. 
   4. Tıklatın **depolama kimlik bilgilerini doğrulama** toovalidate depolama hesabınız. 
   5. [İsteğe bağlı] Yapılan kullanılabilir tooyour Jenkins CI istediğiniz ek depolama hesapları varsa, tıklatın **daha fazla depolama hesapları ekleme**.
   6. Tıklatın **kaydetmek** toosave ayarlarınızı.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Nasıl toocreate derleme yapıları tooyour depolama hesabınız yükleyen oluşturma sonrası eylem
Yönerge amaçlar için önce kimliğinizi toocreate birkaç dosyalarını oluşturmak ve hello oluşturma sonrası eylem tooupload hello dosyaları tooyour depolama hesabı ekleme bir iş gerekir.

1. Merhaba Jenkins Pano içinde tıklatın **yeni öğe**.
2. Ad hello iş **MyJob**, tıklatın **serbest stili yazılım olan bir projeyi derleme**ve ardından **Tamam**.
3. Merhaba, **yapı** bölüm hello iş yapılandırmasına, tıklatın **Ekle derleme adımı** ve seçin **yürütme Windows toplu iş komutu**.
4. İçinde **komutu**, hello aşağıdaki komutları kullanın:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. Merhaba, **oluşturma sonrası eylemleri** bölüm hello iş yapılandırmasına, tıklatın **oluşturma sonrası eylem eklemek** ve seçin **yapıları tooAzure Blob Depolama yükleme**.
6. İçin **depolama hesabı adı**, depolama hesabı toouse hello seçin.
7. İçin **kapsayıcı adı**, hello kapsayıcı adı belirtin. (Merhaba derleme yapıları yüklenirken zaten yoksa, hello kapsayıcı oluşturulacak.) Ortam değişkenlerini kullanma, bu nedenle bu örnek için girin **${JOB_NAME}** hello kapsayıcı adı olarak.
   
    **İpucu**
   
    Merhaba aşağıda **komutu** bölüm için bir komut dosyası girmiş **yürütme Windows toplu iş komutu** toohello ortam değişkenleri Jenkins tarafından tanınan bir bağlantıdır. Toolearn hello ortam değişkeni adları ve açıklamaları bağlantısını tıklatın. Bu ortam Not hello gibi özel karakterleri içeren değişkenler **BUILD_URL** ortam değişkeni, bir kapsayıcı adı veya ortak sanal yol olarak izin verilmez.
8. Tıklatın **olun yeni kapsayıcı Ortak varsayılan olarak** Bu örnek için. (Toouse özel bir kapsayıcı istiyorsanız, toocreate bir paylaşılan erişim imzası tooallow erişimi gerekir. Bu konuda hello kapsamı dışındadır olmasıdır. Paylaşılan erişim imzaları hakkında daha fazla bilgiyi [kullanarak paylaşılan erişim imzaları (SAS)](../storage-dotnet-shared-access-signature-part-1.md).)
9. [İsteğe bağlı] Tıklatın **karşıya yüklemeden önce temiz kapsayıcı** hello kapsayıcı toobe temizlenmiş içeriğini derleme yapıları karşıya önce istiyorsanız (Merhaba kapsayıcı tooclean Merhaba içeriğine istemiyorsanız bu işaretli bırakın).
10. İçin **listesi, yapıları tooupload**, girin  **metin /*.txt**.
11. İçin **karşıya yüklenen yapıları için ortak sanal yol**, bu öğreticinin amaçları girmek için **${yapı\_kimliği} / ${yapı\_numarası}**.
12. Tıklatın **kaydetmek** toosave ayarlarınızı.
13. Merhaba Jenkins panosunda tıklatın **şimdi yapı** toorun **MyJob**. Durum için Hello konsol çıktıyı inceleyin. Merhaba oluşturma sonrası eylem tooupload derleme yapıları başladığında Azure depolama için bildirilen durum iletileri hello konsol çıkışı dahil edilir.
14. Merhaba iş başarılı tamamlandığında hello ortak blob açarak hello derleme yapıları inceleyebilirsiniz.
    1. Oturum açma toohello [Azure Portal](https://portal.azure.com).
    2. Tıklatın **depolama**.
    3. Jenkins için kullanılan hello depolama hesabının adına tıklayın.
    4. Tıklatın **kapsayıcıları**.
    5. Adlı hello kapsayıcısını tıklatın **myjob**, hello Jenkins proje oluşturduğunuzda, size atanan hello iş adı küçük harfli sürümünü hello olduğu. Kapsayıcı adları ve blob adları küçük harf (ve büyük küçük harfe duyarlı) Azure depolama alanında. Adlı hello kapsayıcısı için BLOB hello listesindeki **myjob** görmeniz gerekir **hello.txt** ve **date.txt**. Merhaba URL bu öğelerden birini kopyalayın ve tarayıcınızda açın. Karşıya yüklenen hello metin dosyası yapı yapı görürsünüz.

Yapıları tooAzure blob depolama karşıya yükleme yalnızca bir oluşturma sonrası eylem iş başına oluşturulabilir. Merhaba tek oluşturma sonrası eylem tooupload yapıları tooAzure blob depolama (joker karakterleri dahil olmak üzere) farklı dosyaları ve yolları toofiles içinde belirtebilirsiniz Not **listesi, yapıları tooupload** ayırıcı olarak noktalı virgül kullanıyor. Örneğin, sizin Jenkins yapı JAR dosyaları ve TXT dosyaları alanınızdaki 's üretir **yapı** klasörü ve her iki tooAzure blob depolama tooupload istediğiniz, hello aşağıdaki Merhaba kullanın **listesi, yapıları tooupload** değeri: **yapı /\*.jar; derleme /\*.txt**. Çift iki nokta üst üste sözdizimi toospecify yolu toouse hello blob adı içinde de kullanabilirsiniz. Merhaba Kavanoz tooget kullanarak karşıya isterseniz, örneğin, **ikili dosyaları** hello blob yolu ve hello TXT dosyaları tooget karşıya kullanarak **bildirimler** hello blob yolunda hello aşağıdaki Merhaba kullanın  **Yapıları tooupload listesi** değeri: **yapı /\*. jar::binaries; derleme /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Nasıl Azure blob depolama alanından indirmeleri toocreate bir derleme adımı
Aşağıdaki adımları hello nasıl tooconfigure bir derleme adımı toodownload öğeleri Azure blob depolama alanından gösterir. Bu yapı içinde tooinclude öğe istiyorsanız, örneğin, Azure'da korumak Kavanoz blob depolama yararlı olacaktır.

1. Merhaba, **yapı** bölüm hello iş yapılandırmasına, tıklatın **Ekle derleme adımı** ve seçin **Azure Blob depolama alanından karşıdan**.
2. İçin **depolama hesabı adı**, depolama hesabı toouse hello seçin.
3. İçin **kapsayıcı adı**, toodownload istediğiniz hello BLOB'ları sahip hello kapsayıcı hello adını belirtin. Ortam değişkenleri kullanabilirsiniz.
4. İçin **Blob adı**, hello blob adı belirtin. Ortam değişkenleri kullanabilirsiniz. Ayrıca, hello ilk letter(s) hello blob adını belirttikten sonra bir joker karakter olarak bir yıldız işareti kullanabilirsiniz. Örneğin, **proje\***  adları ile başlayan tüm BLOB'lar belirtirsiniz **proje**.
5. [İsteğe bağlı] İçin **indirme yolunu**, Azure blob depolama biriminden toodownload dosyaları istediğiniz hello Jenkins makine hello yolu belirtin. Ortam değişkenleri de kullanılabilir. (İçin bir değer belirtmezseniz, **indirme yolunu**, Azure blob depolama biriminden hello dosyaları indirilen toohello işin çalışma olacaktır.)

Azure blob depolama biriminden toodownload istediğiniz başka öğeler varsa, ek yapılandırma adımları oluşturabilirsiniz.

Bir yapı çalıştırdıktan sonra hello yapı geçmiş konsol çıktısı ya da yükleme konumunuzu toosee bakma olup hello başarıyla indirildi beklenen BLOB'ları kontrol edebilirsiniz.  

## <a name="components-used-by-hello-blob-service"></a>Merhaba Blob hizmeti tarafından kullanılan bileşenler
Merhaba aşağıdaki hello Blob hizmeti bileşenlerini genel bir bakış sağlar.

* **Depolama hesabı**: üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. BLOB'ları erişmek için hello ad alanı en yüksek düzeyde hello budur. Altında 100 TB toplam kendi boyuttur sürece bir hesapta sınırsız sayıda kapsayıcı, olabilir.
* **Kapsayıcı**: BLOB'lar kümesinin bir gruplandırma bir kapsayıcı sağlar. Tüm bloblar bir kapsayıcıda olmalıdır. Bir hesapta sınırsız sayıda kapsayıcı olabilir. Kapsayıcıda sınırsız sayıda blob depolanabilir.
* **BLOB**: bir dosya türü ve boyutu. Azure Storage'da depolanan BLOB'ları iki tür vardır: blok ve sayfa blobları. Blok blobları çoğu dosyalarıdır. Tek blok blob boyutu too200GB yukarı olabilir. Bu öğretici blok blobları kullanır. Bir dosyada bayt aralıkları sık değiştirildiğinde sayfa blobları, başka bir blob türü, boyut ve daha verimli olan too1TB yukarı olabilir. BLOB'ları hakkında daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **URL biçimi**: BLOB'lar hello şu URL biçimi kullanılarak adreslenebilir:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (yukarıdaki hello biçimini toohello genel Azure bulut uygular. Farklı bir Azure bulut kullanıyorsanız, hello içinde hello uç noktası kullan [Azure Portal](https://portal.azure.com) toodetermine URL uç noktanızı.)
  
    Yukarıdaki hello biçiminde `storageaccount` temsil hello depolama hesabınızın adını `container_name` Merhaba, kapsayıcının adını temsil eder ve `blob_name` Merhaba, blob adı sırasıyla temsil eder. Merhaba kapsayıcı adı içinde birden fazla yol eğik tarafından ayrılmış, olabilir  **/** . Bu öğreticide Hello örnek kapsayıcı adı **MyJob**, ve **${yapı\_kimliği} / ${yapı\_numarası}** hello blob elde etmeyle kaynaklanan hello ortak sanal yolu için kullanılan bir Form aşağıdaki hello URL'si:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Sonraki adımlar
* [Jenkins karşılayan](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Azure depolama için Java SDK'sı](https://github.com/azure/azure-storage-java)
* [Azure Storage istemci SDK'sı başvurusu](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)

Daha fazla bilgi için bkz. [Java geliştiricileri için Azure](/java/azure).