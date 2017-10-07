---
title: "aaaMove veri tooan Azure SQL veritabanı için Azure Machine Learning | Microsoft Docs"
description: "SQL tablo oluşturma ve veri tooSQL tablo yükleme"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Azure Machine Learning için verileri tooan Azure SQL veritabanını taşıma
Bu konu, verileri düz dosyalardan (CSV veya TSV biçimleri) veya bir şirket içi SQL Server tooan Azure SQL veritabanında depolanan veri taşıma için hello seçenekleri özetler. Bu görevler için taşıma veri toohello bulut hello takım veri bilimi işlemi bir parçasıdır.

Taşıma veri tooan hello seçeneklerini özetlenmektedir bir konu SQL Server Machine Learning için şirket için bkz: [veri tooSQL sunucu bir Azure sanal makineyi taşımak](machine-learning-data-science-move-sql-server-virtual-machine.md).

Merhaba aşağıdaki **menü** nasıl burada hello veri depolanabilir ve sırasında işlenen hedef ortamları tooingest verisine takım veri bilimi işlem (TDSP) hello açıklamak tootopics bağlar.

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Merhaba aşağıdaki tabloda taşıma veri tooan Azure SQL veritabanı için hello seçenekleri özetler.

| <b>KAYNAK</b> | <b>Hedef: Azure SQL veritabanı</b> |
| --- | --- |
| <b>Düz dosya (CSV ya da biçimlendirilmiş TSV)</b> |<a href="#bulk-insert-sql-query">Toplu ekleme SQL sorgusu |
| <b>Şirket içi SQL Server</b> |1. <a href="#export-flat-file">TooFlat dosyası dışarı aktarma<br> 2. <a href="#insert-tables-bcp">SQL veritabanı Geçiş Sihirbazı<br> 3. <a href="#db-migration">Yukarı geri veritabanı ve geri yükleme<br> 4. <a href="#adf">Azure veri fabrikası |

## <a name="prereqs"></a>Önkoşullar
Burada gösterilen hello yordamları sahip olması gerekir:

* Bir **Azure aboneliği**. Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Bir **Azure depolama hesabı**. Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanın. Bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesi. Merhaba depolama hesabı oluşturduktan sonra anahtarı tooaccess hello depolama kullanılan tooobtain hello hesabınızın olması gerekir. Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Erişim tooan **Azure SQL veritabanı**. Bir Azure SQL veritabanı, ayarlarsanız, [Microsoft Azure SQL veritabanı ile çalışmaya başlama](../sql-database/sql-database-get-started.md) ilgili bilgiler verilmektedir tooprovision bir Azure SQL veritabanına yeni bir örneğini.
* Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak. Yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

**Veri**: hello geçiş işlemlerini gösterilen hello kullanarak [NYC ücreti dataset](http://chriswhong.com/open-data/foil_nyc_taxi/). Merhaba NYC ücreti dataset seyahat veri ve fairs hakkında bilgi içerir ve Azure blob depolama alanında kullanılabilir: [NYC ücreti verileri](http://www.andresmh.com/nyctaxitrips/). Bir örnek ve bu dosyaların açıklaması sağlanan [NYC ücreti dönüşleri veri kümesi tanımı](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Merhaba yordamlar burada açıklanan tooa kendi veri kümesini uyum veya hello NYC ücreti dataset kullanarak açıklandığı gibi hello adımları izleyin. tooupload Merhaba, şirket içi SQL Server veritabanınızın NYC ücreti kümesine özetlenen hello yordamı izleyin [toplu içeri aktarma verileri SQL Server veritabanına](machine-learning-data-science-process-sql-walkthrough.md#dbload). SQL Server üzerinde bir Azure sanal makine için bu yönergeleri bağlıdır, ancak şirket içi SQL Server toohello yüklemeyle hello yordamı hello aynı.

## <a name="file-to-azure-sql-database"></a>Düz dosya kaynak tooan Azure SQL veritabanından veri taşıma
Bir toplu ekleme SQL sorgusunu kullanarak taşınan tooan Azure SQL veritabanı (CSV veya TSV biçimlendirilmiş) düz dosyalara veri olabilir.

### <a name="bulk-insert-sql-query"></a>Toplu ekleme SQL sorgusu
Merhaba hello toplu Ekle SQL sorgusunu kullanarak hello yordamı için Azure VM temelinde bir düz dosya kaynak tooSQL sunucu verilerini taşıma için hello bölümlerde ele benzer toothose adımlardır. Ayrıntılar için bkz [toplu Ekle SQL sorgusu](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Şirket içi SQL Server tooan Azure SQL veritabanından veri taşıma
Merhaba kaynak verileri bir şirket içi SQL Server depolanıyorsa, taşıma hello veri tooan Azure SQL veritabanı için çeşitli olasılık vardır:

1. [TooFlat dosyası dışarı aktarma](#export-flat-file)
2. [SQL veritabanı Geçiş Sihirbazı](#insert-tables-bcp)
3. [Yukarı geri veritabanı ve geri yükleme](#db-migration)
4. [Azure Data Factory](#adf)

Merhaba hello ilk üç için çok benzer toothose bölümlerde adımlardır [veri tooSQL sunucu bir Azure sanal makineyi taşımak](machine-learning-data-science-move-sql-server-virtual-machine.md) aynı yordamları kapsar. Bağlantılar toohello uygun bölümleri, bu konudaki yönergeleri izleyerek hello sağlanır.

### <a name="export-flat-file"></a>TooFlat dosyası dışarı aktarma
Merhaba bu verme tooa düz dosya için adımlardır ele benzer toothose [tooFlat dosya verme](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>SQL veritabanı Geçiş Sihirbazı
Merhaba hello SQL veritabanı Geçiş Sihirbazı'nı kullanmak için benzer toothose ele adımlardır [SQL veritabanı Geçiş Sihirbazı'nı](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Yukarı geri veritabanı ve geri yükleme
Merhaba adımları kullanarak veritabanı için yedekleme ve geri yükleme olan ele benzer toothose [geri veritabanı yedeklemek ve geri yükleme](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Azure veri fabrikası
taşıma veri tooan Azure SQL veritabanı Azure veri fabrikası (ADF) ile Merhaba yordamı hello konuda sağlanan [bir şirket içi SQL server tooSQL Azure Data Factory ile Azure gelen veri taşıma](machine-learning-data-science-move-sql-azure-adf.md). Bu konu nasıl Azure Blob Storage toomove verilerden bir şirket içi SQL Server veritabanı tooan Azure SQL veritabanı ADF kullanarak gösterir.

ADF veri gereksinimlerini toobe sürekli olarak hem şirket içi erişen bir karma senaryoda geçişi zaman kullanmayı düşünmelisiniz kaynakları Bulut ve hello veri işlem yapılan işlem ya da gereken toobe değiştirilmiş veya iş mantığı tooit Geçirilmekte olan zaman eklemiş. Zamanlama ve düzenli aralıklarla veri hello hareketini yönetmek basit JSON komut dosyalarını kullanarak iş izleme hello ADF sağlar. ADF karmaşık işlemleri için destek gibi diğer özellikleri de vardır.
