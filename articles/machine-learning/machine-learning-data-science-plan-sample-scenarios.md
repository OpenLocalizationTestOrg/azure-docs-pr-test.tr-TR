---
title: "Azure Machine Learning için Gelişmiş analitik senaryoları aaaIdentify | Microsoft Docs"
description: "Merhaba uygun senaryolar hello takım veri bilimi işlemi ile Tahmine dayalı analiz Gelişmiş yapmak için seçin."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Azure Machine Learning’de gelişmiş analiz senaryoları
Bu makalede hello birçok örnek veri kaynakları ve hello tarafından işlenebilir hedef senaryoları özetlenmektedir [takım veri bilimi işlem (TDSP)](data-science-process-overview.md). Merhaba TDSP akıllı uygulamaları derleme üzerinde takımlar toocollaborate sistematik bir yaklaşım sağlar. Burada sunulan hello senaryoları hello veri özellikleri, kaynak konumları ve Azure hedef depoları bağlıdır hello veri işleme iş akışında kullanılabilir seçenekler gösterilmektedir.

Merhaba **karar ağacı** hello son bölümde sunulan veri ve hedefi için uygun hello Örnek senaryo seçmek için.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Hello bölümleri aşağıdaki her bir örnek senaryo sunar. Her senaryo, olası veri bilimi veya gelişmiş analizler için akışı ve Azure kaynaklarını destekleyen listelenir.

> [!NOTE]
> **Tüm senaryoları aşağıdaki hello için şunları yapmanız gerekir:**
> <br/>
> 
> * [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Senaryo \#1: küçük toomedium tablo yerel bir dosya kümesinde
![Küçük toomedium yerel dosyaları][1]

#### <a name="additional-azure-resources-none"></a>Ek Azure kaynaklarını: yok
1. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
2. Bir veri kümesi karşıya yükleyin.
3. Karşıya yüklenen veri kümeleri ile başlayan bir Azure Machine Learning deneme akışı oluşturun.

## <a name="smalllocalprocess"></a>Senaryo \#2: küçük toomedium dataset işleme gerektiren yerel dosyaları
![Küçük toomedium yerel dosyaları işleme ile][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure sanal makinesi (IPython not defteri sunucusu)
1. IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.
2. Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.
3. Önceden işleyebilir ve verileri Azure depolama kapsayıcıdan verilere IPython not defterinde Temizle.
4. Veri toocleaned, Tablo formunda dönüştürün.
5. Dönüştürülen veriler Azure BLOB'ları kaydedin.
6. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
7. Hello kullanarak Azure bloblarından Hello veri okuma [veri içeri aktarma] [ import-data] modülü.
8. Alınan veri kümeleri ile başlayan bir Azure Machine Learning deneme akışı oluşturun.

## <a name="largelocal"></a>Senaryo \#3: büyük veri kümesi yerel dosyaların Azure BLOB'ları hedefleme
![Büyük yerel dosyaları][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure sanal makinesi (IPython not defteri sunucusu)
1. IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.
2. Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.
3. Önceden işleyebilir ve IPython Azure bloblarından verilere dizüstü bilgisayar, veri temizleme.
4. Veri toocleaned, Tablo formunda, gerekirse dönüştürün.
5. Verileri araştırmak ve Özellikler gerektiği şekilde oluşturun.
6. Küçük ve orta veri örneği ayıklayın.
7. Merhaba örneklenen verileri Azure BLOB'ları kaydedin.
8. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Hello kullanarak Azure bloblarından Hello veri okuma [veri içeri aktarma] [ import-data] modülü.
10. Alınan veri kümeleri ile başlayan Azure Machine Learning deneme akış oluşturun.

## <a name="smalllocaltodb"></a>Senaryo \#4: küçük toomedium dataset yerel dosyaları, SQL Server içinde bir Azure sanal makine hedefleme
![Azure'da küçük toomedium yerel dosyaları tooSQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)
1. SQL Server + IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.
2. Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.
3. Önceden işleyebilir ve IPython Not Defteri kullanarak Azure depolama kapsayıcısının verileri temizleyin.
4. Veri toocleaned, Tablo formunda, gerekirse dönüştürün.
5. Veri tooVM yerel dosyaları kaydetme (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere tooVM sürücüleri bakın).
6. Bir Azure VM'de çalıştırılan veri tooSQL sunucu veritabanı yükleyin.
   
   Seçenek \#1: SQL Server Management Studio'yu kullanarak.
   
   * Oturum açma tooSQL Server VM
   * SQL Server Management Studio'yu çalıştırın.
   * Veritabanı ve hedef tablolar oluşturun.
   * Merhaba toplu birini kullanın yöntemleri tooload hello veri VM yerel dosyalarından içeri aktarın.
   
   Seçenek \#2: kullanarak IPython not defteri – Orta ve büyük veri kümeleri için değil önerilir
   
   <!-- -->    
   * ODBC bağlantı dizesi tooaccess SQL Server VM üzerinde kullanın.
   * Veritabanı ve hedef tablolar oluşturun.
   * Merhaba toplu birini kullanın yöntemleri tooload hello veri VM yerel dosyalarından içeri aktarın.
7. Özellikler gerektiği şekilde oluşturun, verileri keşfedin. Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın. Yalnızca hello gerekli sorgu toocreate Not bunları.
8. Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.
9. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
10. Okuma hello verileri doğrudan gelen hello hello kullanarak SQL Server [veri içeri aktarma] [ import-data] modülü. Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.
11. Alınan veri kümeleri ile başlayan Azure Machine Learning deneme akış oluşturun.

## <a name="largelocaltodb"></a>Senaryo \#5: yerel dosyaları büyük bir veri kümesini hedef Azure VM'deki SQL Server
![Azure'da büyük yerel dosyaları tooSQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)
1. SQL Server ve IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.
2. Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.
3. (İsteğe bağlı) Önceden işleyebilir ve veri temizleme.
   
   a.  Önceden işleyebilir ve IPython Azure'dan verilere dizüstü bilgisayar, veri temizleme
   
       blobs.
   
   b.  Veri toocleaned, Tablo formunda, gerekirse dönüştürün.
   
   c.  Veri tooVM yerel dosyaları kaydetme (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere tooVM sürücüleri bakın).
4. Bir Azure VM'de çalıştırılan veri tooSQL sunucu veritabanı yükleyin.
   
   a.  Oturum açma tooSQL Server VM.
   
   b.  Veri zaten kaydedilmemişse, veri dosyalarını Azure'dan indirir.
   
       storage container toolocal-VM folder.
   
   c.  SQL Server Management Studio'yu çalıştırın.
   
   d.  Veritabanı ve hedef tablolar oluşturun.
   
   e.  Merhaba toplu birini kullanın yöntemleri tooload hello veri içeri aktarın.
   
   f.  Tablo birleştirme gerekirse, dizinleri tooexpedite birleştirmeler oluşturabilir.
   
   > [!NOTE]
   > Büyük veri boyutları hızlı yükleme için bölümlenmiş tabloları oluşturma ve içeri aktarma hello verilerini paralel toplu önerilir. Daha fazla bilgi için bkz: [paralel veri alma tooSQL bölümlenmiş tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Özellikler gerektiği şekilde oluşturun, verileri keşfedin. Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın. Yalnızca hello gerekli sorgu toocreate Not bunları.
6. Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.
7. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Okuma hello verileri doğrudan gelen hello hello kullanarak SQL Server [veri içeri aktarma] [ import-data] modülü. Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.
9. Karşıya yüklenen veri kümesi ile başlayan basit Azure Machine Learning deneme akışı

## <a name="largedbtodb"></a>Senaryo \#6: bir SQL Server veritabanı SQL Server içinde bir Azure sanal makine hedefleme şirket içi, büyük bir veri kümesini
![Azure'da büyük SQL DB şirket içi tooSQL DB][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)
1. SQL Server ve IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.
2. Merhaba veri birini kullanın, SQL Server toodump dosyalarından yöntemleri tooexport hello veri verin.
   
   > [!NOTE]
   > Merhaba şirket içi veritabanındaki bir alternatif (hızlı) yöntemi toomove hello tam veritabanı toothe SQL Server örneğinde Azure tüm verileri toomove karar verirseniz. Merhaba adımları tooexport verileri atlayabilirsiniz, veritabanı ve yük/içe aktarma veri toohello hedef veritabanı oluşturun ve hello Alternatif yöntem izleyin.
   > 
   > 
3. Döküm dosyaları tooAzure depolama kapsayıcısı karşıya yükleyin.
4. Bir Azure sanal makinede çalışan yük hello veri tooa SQL Server veritabanı.
   
   a.  Oturum açma toohello SQL Server VM.
   
   b.  Veri dosyaları bir Azure depolama kapsayıcısı toohello yerel VM klasöründen yükleyin.
   
   c.  SQL Server Management Studio'yu çalıştırın.
   
   d.  Veritabanı ve hedef tablolar oluşturun.
   
   e.  Merhaba toplu birini kullanın yöntemleri tooload hello veri içeri aktarın.
   
   f.  Tablo birleştirme gerekirse, dizinleri tooexpedite birleştirmeler oluşturabilir.
   
   > [!NOTE]
   > Büyük veri boyutları hızlı yükleme için bölümlenmiş tablolar ve toobulk alma hello verileri paralel olarak oluşturun. Daha fazla bilgi için bkz: [paralel veri alma tooSQL bölümlenmiş tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Özellikler gerektiği şekilde oluşturun, verileri keşfedin. Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın. Yalnızca hello gerekli sorgu toocreate Not bunları.
6. Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.
7. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Okuma hello verileri doğrudan gelen hello hello kullanarak SQL Server [veri içeri aktarma] [ import-data] modülü. Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.
9. Basit Azure Machine Learning ile karşıya yüklenen dataset başlangıç akışı deneyin.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Alternatif yöntem toocopy bir şirket içi SQL Server tooAzure SQL veritabanını tam bir veritabanından
![Yerel DB detach ve Azure DB tooSQL ekleme][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)
tooreplicate hello tüm SQL Server veritabanında SQL Server VM'nize hello veritabanı geçici olarak çevrimdışı duruma getirilebilen varsayarak bir veritabanı bir konum/sunucu tooanother kopyalamanız gerekir. Bu SQL Server Management Studio Object Explorer hello veya hello eşdeğer Transact-SQL komutlarını kullanarak yapın.

1. Merhaba kaynak konumda Hello veritabanı ayrılmadı. Daha fazla bilgi için bkz: [bir veritabanını ayırma](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. Windows Gezgini veya Windows komut istemi penceresinde, veritabanı dosyası veya dosya ve günlük dosyası veya dosyaları toohello hedef konumu'hello Azure'nın SQL Server VM üzerinde kopyalama hello ayrıldı.
3. Kopyalanan hello dosyaları toohello hedef SQL Server örneği ekleyin. Daha fazla bilgi için bkz: [bir veritabanını](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Kullanarak bir veritabanı ayırma ve (Transact-SQL) ekleme taşıma](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Senaryo \#7: yerel dosyalarında büyük veri hedef Azure Hdınsight Hadoop kümeleri Hive veritabanında
![Yerel hedef Hive büyük verileri][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Ek Azure kaynaklarını: Azure Hdınsight Hadoop kümesi ve Azure sanal makine (IPython not defteri sunucusu)
1. IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.
2. Bir Azure Hdınsight Hadoop kümesi oluşturun.
3. (İsteğe bağlı) Önceden işleyebilir ve veri temizleme.
   
   a.  Önceden işleyebilir ve IPython Azure'dan verilere dizüstü bilgisayar, veri temizleme
   
       blobs.
   
   b.  Veri toocleaned, Tablo formunda, gerekirse dönüştürün.
   
   c.  Veri tooVM yerel dosyaları kaydetme (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere tooVM sürücüleri bakın).
4. Veri toohello varsayılan kapsayıcı hello adım 2 seçili hello Hadoop kümesi karşıya yükleyin.
5. Azure Hdınsight Hadoop kümesindeki verileri tooHive veritabanı yükleyin.
   
   a.  Toohello baş hello Hadoop küme düğümünde oturum
   
   b.  Merhaba Hadoop komut satırı açın.
   
   c.  Komutu tarafından Hello Hive kök dizini girin `cd %hive_home%\bin` , Hadoop komut satırı.
   
   d.  Merhaba Hive sorguları toocreate veritabanı ve tablo çalıştırın ve blob depolama tooHive tablolarından veri yükleme.
   
   > [!NOTE]
   > Merhaba veri büyük ise, kullanıcıların bölümlerle hello Hive tablosu oluşturabilirsiniz. Kullanıcılar daha sonra kullanabileceğiniz bir `for` hello Hadoop komut satırı hello baş düğüm tooload verileri hello Hive tablosu tarafından bölüm bölümlenmiş bir döngüde.
   > 
   > 
6. Verileri araştırmak ve özellikleri Hadoop komut satırında gerektiği şekilde oluşturun. Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın. Yalnızca hello gerekli sorgu toocreate Not bunları.
   
   a.  Toohello baş hello Hadoop küme düğümünde oturum
   
   b.  Merhaba Hadoop komut satırı açın.
   
   c.  Komutu tarafından Hello Hive kök dizini girin `cd %hive_home%\bin` , Hadoop komut satırı.
   
   d.  Merhaba Hive sorguları Hadoop komut satırında hello baş hello Hadoop küme tooexplore hello verileri düğümde çalıştırın ve gerektiği gibi özellikleri oluşturun.
7. Gerekli ve/veya istenen, Azure Machine Learning Studio'da hello veri toofit örnek.
8. İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Doğrudan hello Hello veri okuma `Hive Queries` hello kullanarak [veri içeri aktarma] [ import-data] modülü. Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.
10. Basit Azure Machine Learning ile karşıya yüklenen dataset başlangıç akışı deneyin.

## <a name="decisiontree"></a>Senaryo seçimi için karar ağacı
- - -
Merhaba Aşağıdaki diyagramda yukarıda açıklanan hello senaryoları ve tooeach dökümü hello senaryoların atmanız yapılan hello Advanced Analytics işlemi ve teknoloji seçimler özetler. Veri işleme, keşfi, özellik Mühendisliği ve örnekleme alabileceğini unutmayın, bir veya daha fazla yöntem/ortam--kaynaktaki Merhaba, Ara, ve/veya hedef ortamları – içinde yerleştirin ve gerektiğinde tekrarlayarak devam edebilirsiniz. Merhaba diyagram yalnızca bazı olası akışlarının çizim görev yapar ve kapsamlı bir numaralandırma sağlamaz.

![DS işlemi izlenecek senaryolar][8]

### <a name="advanced-analytics-in-action-examples"></a>Gelişmiş analizler eylem örnekleri
Ortak veri kümeleri kullanarak, kullanan uçtan uca Azure Machine Learning izlenecek yollar için Gelişmiş analiz işlem ve teknoloji Merhaba, bkz:

* [Veri bilimi işlemi eylemde ekip: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).
* [Veri bilimi işlemi eylemde ekip: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
