---
title: "Hdınsight sırasında aaaAdd Hıve kitaplıkları küme oluşturma - Azure | Microsoft Docs"
description: "Nasıl tooadd Hıve kitaplıkları (jar dosyaları), tooan Hdınsight Küme Küme oluşturma sırasında öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Özel Hıve kitaplıkları, Hdınsight kümesi oluştururken ekleme

Hdınsight'ta Hive sık kullandığınız kitaplıkları varsa, bu belgede küme oluşturma sırasında bir betik eylemi toopre yük hello kitaplıklarını kullanma hakkında bilgi içerir. Bu belgede Hello adımları kullanarak eklenen kitaplıkları genel olarak kullanılabilir kovanında - gerek toouse [eklemek JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload bunları.

## <a name="how-it-works"></a>Nasıl çalışır?

Bir küme oluştururken, bunlar oluşturulurken hello küme düğümleri üzerinde bir komut dosyası çalıştırılan bir komut dosyası eylemi isteğe bağlı olarak belirtebilirsiniz. Bu belgedeki Hello betik önceden yüklenmiş hello (jar dosyaları olarak depolanır) kitaplıkları toobe içeren bir WASB konumunun tek bir parametre kabul eder.

Küme oluşturma sırasında hello betik hello dosyaları sıralar, toohello kopyalar `/usr/lib/customhivelibs/` head ve çalışan düğümleri üzerinde dizin sonra toohello bunları ekler `hive.aux.jars.path` hello özelliğinde `core-site.xml` dosya. Linux tabanlı kümelerde de hello güncelleştirir `hive-env.sh` hello hello dosyalarının konumunu dosyasıyla.

> [!NOTE]
> Bu makalede Hello betik eylemleri kullanılarak hello kitaplıkları senaryoları aşağıdaki hello yapar:
>
> * **Linux tabanlı Hdınsight** - kullanarak hello olduğunda bir Hive istemci **WebHCat**, ve **HiveServer2**.
> * **Windows tabanlı Hdınsight** - hello Hive istemci kullanırken ve **WebHCat**.

## <a name="hello-script"></a>Merhaba komut dosyası

**Komut dosyası konumu**

İçin **Linux tabanlı kümelerde**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

İçin **Windows tabanlı kümeler**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

**Gereksinimleri**

* Merhaba betikleri uygulanan tooboth hello olmalıdır **baş düğümler** ve **çalışan düğümleri**.

* Merhaba istiyor tooinstall depolanan, Azure Blob Depolama Kavanoz bir **tek kapsayıcısı**.

* Merhaba kitaplığı jar dosyalarını içeren hello depolama hesabı **gerekir** bağlantılı toohello Hdınsight kümesi oluşturma sırasında olabilir. Ya da hello varsayılan depolama hesabı olması gerekir ya da bir hesap üzerinden eklenen __isteğe bağlı yapılandırma__.

* Merhaba WASB yolu toohello kapsayıcı parametresi toohello betik eylemi belirtilmelidir. Örneğin, hello varsa Kavanoz adlı bir kapsayıcıda depolanır **kitaplıklar** bir depolama hesabında adlı **mystorage**, hello parametre olacaktır  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Bu belge sahip önceden oluşturduğunuz bir depolama hesabı, blob kapsayıcısı ve karşıya yüklenen hello dosyaları tooit varsayar.
  >
  > Bir depolama hesabı oluşturmadıysanız hello bunu yapabilirsiniz [Azure portal](https://portal.azure.com). Ardından bir programı gibi kullanabilir [Azure Storage Gezgini](http://storageexplorer.com/) toocreate hello hesabı ve karşıya yükleme kapsayıcısında tooit dosyaları.

## <a name="create-a-cluster-using-hello-script"></a>Merhaba komut dosyası kullanarak bir küme oluşturun

> [!NOTE]
> Aşağıdaki adımları hello Linux tabanlı Hdınsight kümesi oluşturun. toocreate Windows tabanlı bir küme seçin **Windows** hello küme oluştururken, işletim sistemi hello küme ve hello bash betik yerine hello Windows (PowerShell) komut dosyası kullanın.
>
> Azure PowerShell veya hello Hdınsight .NET SDK'sı toocreate bu komut dosyası kullanarak bir küme de kullanabilirsiniz. Bu yöntemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).

1. Merhaba adımları kullanarak bir küme hazırlama Başlat [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md), ancak sağlama tamamlamayın.

2. Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **betik eylemleri**ve aşağıdaki bilgilerle hello sağlayın:

   * **AD**: hello betik eylemi için kolay bir ad girin.

   * **BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**: Bu seçeneği işaretleyin.

   * **ÇALIŞAN**: Bu seçeneği işaretleyin.

   * **ZOOKEEPER**: Bu alanı boş bırakın.

   * **PARAMETRELERİ**: hello Kavanoz içeren hello WASB adresi toohello kapsayıcı ve depolama hesabını girin. Örneğin,  **wasb://libs@mystorage.blob.core.windows.net/** .

3. Merhaba hello sonundaki **betik eylemleri**, hello kullan **seçin** düğme toosave hello yapılandırması.

4. Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **bağlantılı depolama hesapları** ve select hello **depolama anahtarı eklemek** bağlantı. Hello Kavanoz içeren hello depolama hesabını seçin ve sonra hello **seçin** düğmeleri toosave ayarları ve dönüş hello **isteğe bağlı yapılandırma** dikey.

5. Kullanım hello **seçin** düğmesi hello hello sonundaki **isteğe bağlı yapılandırma** dikey toosave hello isteğe bağlı yapılandırma bilgileri.

6. Bölümünde açıklandığı gibi Hello küme hazırlama devam [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md).

Küme oluşturma tamamlandıktan sonra bu komut dosyası aracılığıyla toouse hello gerek kalmadan kovanından eklenen mümkün toouse hello Kavanoz olan `ADD JAR` deyimi.

## <a name="next-steps"></a>Sonraki adımlar

Hive ile çalışma hakkında daha fazla bilgi için bkz: [Hdınsight ile Hive kullanma](hdinsight-use-hive.md)
