---
title: "hdınsight'ta - Azure HBase örnek aaaGet Başlarken | Microsoft Docs"
description: "Hdınsight'ta hadoop kullanarak bu Apache HBase örnek toostart izleyin. Hello HBase Kabuğu ' tablolar oluşturmak ve bunları sorgulayabilirsiniz Hive kullanma."
keywords: "hbase komutu,hbase örneği"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>HDInsight'ta Apache HBase örneğiyle çalışmaya başlama

Toocreate bir HBase kümesi, hdınsight'ta HBase tabloları oluşturma ve tabloları Hive kullanarak sorgulama öğrenin. Genel HBase bilgileri için bkz. [HDInsight HBase’e genel bakış][hdinsight-hbase-overview].

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu HBase örnek çalışırken başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>HBase kümesi oluşturma
Merhaba aşağıdaki yordam bir Azure Resource Manager şablonu toocreate sürüm 3.4 Linux tabanlı HBase kümesi ve hello bağımlı varsayılan bir Azure depolama hesabı kullanır. Merhaba yordam ve diğer küme oluşturma yöntemlerinde kullanılan toounderstand hello parametreler bkz [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).

1. Görüntü tooopen hello hello Azure portal şablonda aşağıdaki hello'ı tıklatın. Merhaba şablonu bir ortak blob kapsayıcısında bulunur. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Merhaba gelen **özel dağıtım** dikey penceresinde hello aşağıdaki değerleri girin:
   
   * **Abonelik**: kullanılan toocreate hello küme Azure aboneliğinizi seçin.
   * **Kaynak grubu**: Bir Azure Resource Management grubu oluşturun veya var olan gruplardan birini kullanın.
   * **Konum**: hello hello kaynak grubu konumunu belirtin. 
   * **ClusterName**: Merhaba HBase kümesi için bir ad girin.
   * **Küme oturum açma adı ve parola**: hello varsayılan oturum açma adı **yönetici**.
   * **SSH kullanıcı adı ve parola**: hello varsayılan kullanıcı adı **sshuser**.  Bunu yeniden adlandırabilirsiniz.
     
     Diğer parametreler isteğe bağlıdır.  
     
     Her kümenin bir Azure Depolama hesabı bağımlılığı vardır. Bir küme silindikten sonra hello veri hello depolama hesabında saklanır. Merhaba kümenin varsayılan depolama hesabı adı hello küme depo"ifadesi eklenmiş" adıdır. Bu, sabit kodlanmış hello şablon değişkenler bölümünde olur.
3. Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul**ve ardından **satın alma**. Bir küme toocreate yaklaşık 20 dakika sürer.

> [!NOTE]
> Bir HBase kümesi silindikten sonra hello kullanarak başka bir HBase kümesi oluşturabilirsiniz aynı varsayılan blob kapsayıcısı. Merhaba yeni küme hello özgün kümede oluşturduğunuz hello HBase tablolarını seçer. tooavoid tutarsızlıklar hello küme silmeden önce hello HBase tablolarını devre dışı bırakmanızı öneririz.
> 
> 

## <a name="create-tables-and-insert-data"></a>Tablo oluşturma ve veri ekleme
SSH tooconnect tooHBase kümeleri kullanan ve HBase Kabuğu toocreate HBase tablolarını kullanın, veri ve sorgu veri ekleyin. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

Çoğu kişi için veriler hello tablo biçiminde görünür:

![HDInsight HBase tablo verileri][img-hbase-sample-data-tabular]

HBase (BigTable uygulaması), hello aynı veri gibi görünüyor:

![HDInsight HBase BigTable verileri][img-hbase-sample-data-bigtable]


**toouse hello HBase Kabuğu**

1. SSH, HBase komutu aşağıdaki hello çalıştırın:
   
    ```bash
    hbase shell
    ```

2. İki sütun ailesi ile bir HBase oluşturun:

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Bazı verileri ekleyin:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase kabuğu][img-hbase-shell]
4. Tek bir satır alın
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    Yalnızca bir satır olduğundan hello tarama komutunu kullanmanızla aynı sonuçları hello göreceksiniz.
   
    Merhaba HBase tablo şeması hakkında daha fazla bilgi için bkz: [şema tasarımına giriş tooHBase][hbase-schema]. HBase komutları hakkında daha fazla bilgi için bkz. [Apache HBase başvuru kılavuzu][hbase-quick-start].
5. Merhaba kabuktan çıkış yapma
   
    ```hbaseshell
    exit
    ```

**toobulk hello kişiler HBase tablosuna veri yükleme**

HBase’de verileri tablolara yüklemek için bazı yöntemler vardır.  Daha fazla bilgi için bkz. [Toplu yükleme](http://hbase.apache.org/book.html#arch.bulk.load).

Örnek veri dosyası, ortak blob kapsayıcısı *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt* içinde bulunabilir.  Merhaba veri dosyası Merhaba içeriğine şöyledir:

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

İsteğe bağlı olarak, bir metin dosyası oluşturun ve hello dosya tooyour kendi depolama hesabı yükleyin. Merhaba yönergeler için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme][hdinsight-upload-data].

> [!NOTE]
> Bu yordam hello son yordamda oluşturduğunuz hello kişiler HBase tablosunu kullanır.
> 

1. SSH, verileri tooStoreFiles dosya ve Dimporttsv.bulk.output tarafından belirtilen göreli bir yola depolamak komutu tootransform hello aşağıdaki hello çalıştırın.  HBase Kabuğu'nda varsa, hello çıkış komut tooexit kullanın.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Komut tooupload hello veri /example/data/storeDataFileOutput toohello HBase tablosundan aşağıdaki hello çalıştırın:
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. Merhaba HBase Kabuğu'nu açın ve hello tarama komutunu toolist hello tablo içeriğini kullanın.

## <a name="use-hive-tooquery-hbase"></a>Hive tooquery HBase kullanın

Hive kullanarak HBase tablolarındaki verileri sorgulayabilirsiniz. Bu bölümde, bir Hive tablosu, oluşturduğunuz toohello HBase tablo eşler ve HBase tablosunda tooquery hello verileri kullanır.

1. Açık **PuTTY**ve toohello kümesine bağlanın.  Merhaba önceki yordamda bulunan Hello yönergelere bakın.
2. Merhaba SSH oturumunda, aşağıdaki komut toostart Beeline hello kullanın:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Beeline hakkında daha fazla bilgi için bkz. [Beeline ile HDInsight’ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md).
       
3. Aşağıdaki HiveQL betiğini toocreate hello toohello HBase tablosuyla eşlenen bir Hive tablosu çalıştırın. Bu öğreticide daha önce bu deyimi çalıştırmadan önce hello HBase Kabuğu'nu kullanarak tarafından başvurulan hello örnek tablosunu oluşturduğunuzdan emin olun.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Aşağıdaki HiveQL betiğini tooquery hello veri hello HBase tablosundaki hello çalıştırın:

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Curl kullanarak HBase REST API’lerini kullanma

Merhaba REST API aracılığıyla güvenli [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication). Her zaman güvenli HTTP (toohelp olun kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir HTTPS) kullanarak isteğini hale.

2. Komut toolist hello var olan HBase tablolarını aşağıdaki hello kullan:

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Komut toocreate iki sütun ailesi ile yeni bir HBase tablosu aşağıdaki hello kullan:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    Merhaba şema hello JSon biçiminde sağlanır.
4. Komut tooinsert aşağıdaki hello bazı veriler kullanın:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    Base64 gerekir hello -d anahtarda belirtilen hello değerleri kodlayın. Merhaba örnekte:
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [false satır anahtarını](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert sağlar (toplu) birden çok değer.
5. Komut tooget bir satır aşağıdaki hello kullan:
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

HBase Rest hakkında daha fazla bilgi için bkz. [Apache HBase Başvuru Kılavuzu](https://hbase.apache.org/book.html#_rest).

> [!NOTE]
> Thrift, HDInsight’ta HBase tarafından desteklenmez.
>
> Curl'ü veya başka bir REST iletişimini WebHCat ile kullanırken, hello kullanıcı adı ve parola hello Hdınsight küme yöneticisinin sağlayarak hello istekleri kimliğini doğrulaması gerekir. Merhaba Tekdüzen Kaynak Tanımlayıcısı (URI) bir parçası toosend hello istekleri toohello sunucu kullanılan gibi hello küme adını kullanmanız gerekir:
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    Yanıt aşağıdaki yanıt benzer toohello almanız gerekir:
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>Küme durumunu denetleme
HDInsight içinde HBase, kümelerin izlenmesi için bir Web Kullanıcı Arabirimi ile birlikte gönderilir. Merhaba Web kullanıcı arabirimini kullanarak istatistikler veya bölgeler hakkında bilgi isteyebilir.

**tooaccess hello HBase ana kullanıcı Arabirimi**

1. Merhaba içine oturum hello Ambari Web kullanıcı Arabirimi https://&lt;Clustername >. azurehdinsight.net.
2. Tıklatın **HBase** hello sol menüden.
3. Tıklatın **hızlı bağlantılar** hello noktası toohello etkin Zookeeper düğüm bağlantı hello Sayfanın üstü ve ardından **HBase ana UI**.  başka bir tarayıcı sekmesinde Hello kullanıcı Arabirimi açılır:

  ![HDInsight HBase HMaster Kullanıcı Arabirimi](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Merhaba HBase ana UI hello aşağıdaki bölümleri içerir:

  - Bölge sunucuları
  - Yedekleme yöneticileri
  - Tablolar
  - Görevler
  - Yazılım öznitelikleri

## <a name="delete-hello-cluster"></a>Merhaba küme silme
tooavoid tutarsızlıklar hello küme silmeden önce hello HBase tablolarını devre dışı bırakmanızı öneririz.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl toocreate bir HBase kümesi ve toocreate tablo ve görünüm bu tablolardaki verileri nasıl hello HBase kabuğunu hello öğrendiniz. Ayrıca nasıl toouse bir Hive HBase tabloları ve nasıl toouse hello HBase C# REST API'lerini toocreate veriler üzerinde bir HBase tablosu sorgulama ve hello tablosundan verileri öğrendiniz.

toolearn daha bakın:

* [HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
