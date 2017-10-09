---
title: "aaaCustomize Hadoop kümeleri Merhaba takım veri bilimi işlemi | Microsoft Docs"
description: "Popüler Python modülleri özel Azure Hdınsight Hadoop kümeleri kullanılabilir."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Azure Hdınsight Hadoop kümeleri hello takım veri bilimi işlemi için özelleştirme
Merhaba küme bir Hdınsight hizmeti olarak sağlanır, bu makalede nasıl toocustomize bir Hdınsight Hadoop küme 64-bit Anaconda (Python 2.7) yükleyerek her düğümde açıklanmaktadır. Aynı zamanda, nasıl tooaccess headnode toosubmit özel işleri toohello küme hello gösterir. Bu özelleştirme Anaconda içinde yer alan birçok popüler Python modülleri yapar, kullanıcı için uygun şekilde kullanılabilir olan tanımlı işlevler (UDF'ler) tooprocess hello kümesindeki Hive kayıtları tasarlanmış. Bu senaryoda kullanılan hello yordamları hakkında yönergeler için bkz: [nasıl toosubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit).

Merhaba aşağıdaki menü bağlantılar hello yukarı tooset çeşitli veri bilimi ortamları hello tarafından nasıl kullanılacağını açıklamaktadır tootopics [takım veri bilimi işlem (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Azure Hdınsight Hadoop kümesi özelleştirme
özelleştirilmiş bir Hdınsight Hadoop kümesi toocreate Başlat çok oturum açarak[**Klasik Azure portalı**](https://manage.windowsazure.com/), tıklatın **yeni** hello sol alt köşesindeki ve veri hizmetleri seçin HDINSİGHT -> -> **özel Oluştur** hello yukarı toobring **küme ayrıntıları** penceresi. 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Yapılandırma sayfasında 1 oluşturulan hello küme toobe Hello adını girin ve diğer alanlar hello için varsayılan değerleri kabul edin. Merhaba ok toogo toohello sonraki yapılandırma sayfasını tıklatın. 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Hello sayısı yapılandırma sayfasında 2 giriş **veri DÜĞÜMLERİNİ**seçin hello **bölge/sanal ağ**seçip hello hello boyutlarını **baş düğüm** ve hello **Veri düğümü**. Merhaba ok toogo toohello sonraki yapılandırma sayfasını tıklatın.

> [!NOTE]
> Merhaba **bölge/sanal ağ** aynı hello bölge hello Hdınsight Hadoop kümesi için kullanılan toobe geçiyor hello depolama hesabının olarak hello toobe sahiptir. Aksi takdirde hello dördüncü yapılandırma sayfasında hello depolama hesabı hello aşağı açılan listesinde görünmez **hesap adı**.
> 
> 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

Yapılandırma sayfasında 3 hello Hdınsight Hadoop kümesi için bir kullanıcı adı ve parola sağlayın. **Sağlamadığı** select hello *Enter hello Hive/Oozie meta depo*. Merhaba ok toogo toohello sonraki yapılandırma sayfası'ye tıklayın. 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

Yapılandırma sayfasında 4 hello depolama hesabı adı, hello varsayılan kapsayıcı hello Hdınsight Hadoop kümesi belirtin. Seçerseniz *oluşturma varsayılan kapsayıcı* hello içinde **varsayılan KAPSAYICI** açılır listesi, bir kapsayıcı hello ile aynı adı hello küme oluşturulacak şekilde. Merhaba ok toogo toohello son yapılandırma sayfasını tıklatın.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

Merhaba son üzerinde **betik eylemleri** yapılandırma sayfasında, tıklatın **betik eylemi eklemek** düğmesine tıklayın ve değerleri aşağıdaki hello ile Merhaba metin alanları doldurun.

* **AD** -bu komut dosyası eylemin hello adı olarak herhangi bir dize
* **DÜĞÜM türü** - seçin **tüm düğümler**
* **BETİK URI'si** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* hello depolama hesabındaki ortak bir kapsayıcı 
  * *getgoing* Azure'da tooshare PowerShell komut dosyaları toofacilitate kullanıcıların çalışmalarını kullanırız
* **PARAMETRELERİ** -(boş bırakın)

Son olarak, özelleştirilmiş hello Hdınsight Hadoop küme hello onay işareti toostart hello oluşturma'ı tıklatın. 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Erişim hello Hadoop kümesi, baş düğümü
RDP hello Hadoop küme baş düğümüne hello erişmeden önce uzaktan erişim toohello Hadoop kümesi Azure etkinleştirmeniz gerekir. 

1. İçinde toohello oturum [ **Klasik Azure portalı**](https://manage.windowsazure.com/)seçin **Hdınsight** hello sol tarafta, Hadoop kümesi hello kümeleri listesinden seçin, hello  **Yapılandırma** sekmesini ve sonra hello **etkinleştirmek uzak** hello sayfanın hello simgesine tıklayın.
   
    ![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. Merhaba, **Uzak Masaüstü'nü yapılandırmak** penceresinde hello kullanıcı adı ve parola alanlarına girin ve Uzaktan erişim hello sona erme tarihini seçin. Merhaba onay işareti tooenable hello uzaktan erişim toohello baş düğümüne hello Hadoop kümesi'ye tıklayın.
   
    ![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> Merhaba kullanıcı adı ve parola hello uzaktan erişim için hello kullanıcı adı ve hello Hadoop küme oluştururken kullandığınız parolayı olup olmadığı. Bu kimlik bilgilerini ayrı bir kümesidir. Ayrıca, hello sona erme tarihi hello uzaktan erişim 7 gün içinde hello geçerli tarih toobe sahiptir.
> 
> 

Uzaktan erişim etkinleştirildikten sonra tıklatın **BAĞLAN** hello sayfa tooremote hello baş düğüme hello sonundaki. Daha önce belirtilen hello uzaktan erişim kullanıcıdan hello kimlik bilgileri girerek toohello baş hello Hadoop küme düğümünde oturum.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Merhaba analytics işlem Gelişmiş hello sonraki adımlarda hello eşlenen [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve Hdınsight'a, veri taşıma sonra işleyen ve onu var. hello verilerden öğrenmeyi hazırlığı örnek adımlar içerebilir Azure Machine Learning ile.

Bkz: [nasıl toosubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit) nasıl tooaccess Anaconda içinde kullanılan tooprocess olan kullanıcı tanımlı işlevler (UDF'ler) içinde hello kümenin baş düğümünden hello dahil edilen Python modülleri hello hakkında yönergeler için saklanan kayıtlarını yığını Merhaba kümesinde.

