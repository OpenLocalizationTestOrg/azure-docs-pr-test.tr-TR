---
title: "Hadoop kümesi - Azure üzerinde aaaUse betik eylemi tooinstall Solr | Microsoft Docs"
description: "Toocustomize Hdınsight ile betik eylemi kullanarak Solr nasıl küme öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Yükleme ve Windows tabanlı Hdınsight kümelerinde Solr kullanma

Toocustomize Windows tabanlı Hdınsight kümesi nasıl ile betik eylemi kullanarak Solr ve nasıl öğrenin toouse Solr toosearch veri.

> [!IMPORTANT]
> Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları. Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Linux tabanlı bir kümeyle Solr kullanma hakkında daha fazla bilgi için bkz: [yükleme ve kullanma Solr Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-solr-install-linux.md).


Solr Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde kullanarak yükleyebileceğiniz *betik eylemi*. Hdınsight kümesinde bir örnek komut dosyası tooinstall Solr salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

Merhaba örnek betik yalnızca Hdınsight küme sürümü ile 3.1 çalışır. Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).

Bu konuda kullanılan hello örnek betik, belirli bir yapılandırmayla Windows tabanlı Solr küme oluşturur. Farklı Koleksiyonlara, parça, şemalar, çoğaltmalar, vb. ile tooconfigure hello Solr kümesi istiyorsanız hello komut dosyası ve Solr ikili dosyaları uygun şekilde değiştirmelisiniz.

**İlgili makaleler**

* [Yükleme ve Solr Hdınsight Hadoop kümeleri (Linux) kullanma](hdinsight-hadoop-solr-install-linux.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.
* [Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.
* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>Solr nedir?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> güçlü tam metin araması verileri sağlayan bir kurumsal arama platformudur. Hadoop depolamak ve çok büyük miktarda veri yönetme olanak sağlarken, Apache Solr tooquickly hello verileri almak hello arama yetenekleri sağlar.

## <a name="install-solr-using-portal"></a>Portal kullanarak Solr yükleyin
1. Hello kullanarak bir küme oluşturmaya başlamak **özel Oluştur** konusunda açıklandığı gibi seçeneği [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-provision-clusters.md).
2. Hello üzerinde **betik eylemleri** sayfa hello Sihirbazı'nın tıklatın **betik eylemi eklemek** tooprovide aşağıda gösterildiği gibi hello betik eylemi hakkında ayrıntıları:

    ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "kullanım betik eylemi toocustomize küme")

    <table border='1'>
        <tr><th>Özellik</th><th>Değer</th></tr>
        <tr><td>Ad</td>
            <td>Merhaba betik eylemi için bir ad belirtin. Örneğin, <b>yükleme Solr</b>.</td></tr>
        <tr><td>Betik URI'si</td>
            <td>Çağrılan toocustomize hello küme hello Tekdüzen Kaynak Tanımlayıcısı (URI) toohello komut dosyasını belirtin. Örneğin, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Düğüm Türü</td>
            <td>Merhaba özelleştirme betik çalıştığı hello düğüm belirtin. Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>yalnızca çalışan düğümleri</b>.
        <tr><td>Parametreler</td>
            <td>Merhaba komut dosyası için gereken Hello parametreleri belirtin. Bunu boş bırakabilirsiniz şekilde hello betik tooinstall Solr herhangi bir parametre gerektirmez.</td></tr>
    </table>

    Birden fazla betik eylemi tooinstall hello kümede birden çok bileşen ekleyebilirsiniz. Merhaba komut dosyaları ekledikten sonra hello küme oluşturma hello onay işareti toostart tıklayın.

## <a name="use-solr"></a>Solr kullanma
Bazı veri dosyalarıyla Solr dizin ile başlamalıdır. Bu gibi durumlarda, Solr toorun arama sorguları sonra dizine hello verilerini kullanabilirsiniz. Bir Hdınsight kümesindeki adımları toouse Solr aşağıdaki hello gerçekleştirin:

1. **Uzak Masaüstü Protokolü (RDP) tooremote hello Hdınsight kümesine yüklü Solr ile kullanmak**. Azure portal Hello Uzak Masaüstü Solr yüklü ve ardından uzak içine hello kümesi ile oluşturulan hello küme için etkinleştirin. Yönergeler için bkz: [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Dizin veri dosyaları yükleyerek Solr**. Solr dizin oluşturduğunuzda üzerinde toosearch gerekebilir, belgeleri yerleştirin. tooindex Solr, kullanım RDP tooremote hello kümesine toohello Masaüstü gidin, hello Hadoop komut satırı açın ve çok gidin**C:\apps\dist\solr-4.7.2\example\exampledocs**. Merhaba aşağıdaki komutu çalıştırın:

        java -jar post.jar solr.xml monitor.xml

    Çıktı hello konsolda aşağıdaki hello görürsünüz:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Merhaba post.jar yardımcı programı, iki örnek belgelerle Solr dizinler **solr.xml** ve **monitor.xml**. Merhaba post.jar yardımcı programı ve hello örnek belgeler Solr yükleme ile kullanılabilir.
3. **Kullanım hello Solr Pano toosearch hello içinde dizine belgeleri**. Merhaba RDP oturumu toohello Hdınsight küme, Internet Explorer'ı açın ve hello Solr Panosu'nda başlatın **solr/http://headnodehost:8983 / #/**. Merhaba gelen hello sol bölmesinde **çekirdek Seçici** açılan listesinde, select **collection1**, tıklatıp, içinde **sorgu**. Bir örnek, tooselect ve return olarak Solr, içindeki tüm hello belgeleri değerleri aşağıdaki hello sağlar:

   * Merhaba, **q** metin kutusuna  **\*:**\*. Bu dizini tüm hello belgeleri Solr döndürür. Belirli bir dizeyi hello belgelerde toosearch istiyorsanız, o dizeyi buraya girebilirsiniz.
   * Merhaba, **wt** metin kutusunda, select hello çıktı biçimi. Varsayılan değer **json**. Tıklatın **sorgu yürütme**.

     ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Solr Panoda bir sorgu çalıştırın")

     Merhaba çıktı hello için dizin oluşturma Solr kullandık iki belgeleri döndürür. Merhaba çıktı hello aşağıdakine benzer:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Önerilen: Hello yedekleme Solr tooAzure hello Hdınsight kümesi ile ilişkili Blob Depolama verileri dizine**. İyi bir uygulama hello Solr küme düğümlerinden Azure Blob Depolama üzerine dizine hello verileri yedeklemelisiniz. Adımları toodo şekilde aşağıdaki hello gerçekleştirin:

   1. Merhaba RDP oturumu, Internet Explorer ve noktası URL aşağıdaki toohello açın:

           http://localhost:8983/solr/replication?command=backup

       Şuna benzer bir yanıt görmeniz gerekir:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. Merhaba uzak oturumda çok gidin {SOLR_HOME}\{koleksiyonu} \data. Merhaba örnek komut dosyası oluşturulan hello küme için bu olmalıdır **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. Bu konumda bir adla çok benzer oluşturulmuş bir anlık görüntü klasörü görmelisiniz**anlık görüntü.* zaman damgası***.
   3. Başlangıç anlık görüntü klasörü zip ve tooAzure Blob storage'ı yükleyin. Merhaba Hadoop komut satırından komutu aşağıdaki hello kullanarak toohello hello anlık görüntü klasörü konumunu gidin:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Kopya anlık görüntü çok/örnek/data hello/hello varsayılan depolama hello kapsayıcıda altında hello kümesi ile ilişkili hesap bu komutu.

## <a name="install-solr-using-aure-powershell"></a>Solr işlemleri PowerShell kullanarak yükleme
Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Merhaba örnek gösterilmektedir nasıl tooinstall Azure PowerShell kullanarak Spark. Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>.NET SDK kullanarak Solr yükleyin
Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Merhaba örnek gösterilmektedir nasıl tooinstall Spark hello .NET SDK kullanarak. Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Ayrıca bkz.
* [Yükleme ve Solr Hdınsight Hadoop kümeleri (Linux) kullanma](hdinsight-hadoop-solr-install-linux.md)
* [Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.
* [Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.
* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).
* [Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: Spark yükleme hakkında örnek betik eylemi.
* [Hdınsight kümelerinde R yüklemek][hdinsight-install-r]: betik eylemi örnek r yükleme hakkında
* [Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install.md): Giraph yükleme hakkında örnek betik eylemi.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
