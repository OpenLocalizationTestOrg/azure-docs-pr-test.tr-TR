---
title: "aaaUse durumu - müşteri profil oluşturma"
description: "Azure Data Factory kullanılan toocreate veri temelli iş akışı (ardışık düzeni) tooprofile oyun müşteriler nasıl yapıldığını öğrenin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Kullanım Örneği - Müşteri Profili Oluşturma
Azure Data Factory birçok kullanılan hizmetler tooimplement hello Cortana Intelligence Suite Çözüm Hızlandırıcıları, biridir.  Cortana Intelligence hakkında daha fazla bilgi için ziyaret [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics). Bu belgede, biz basit kullanım örneği toohelp açıklayan Azure Data Factory ortak analytics sorunları nasıl çözebilir anlama ile başlayın.

## <a name="scenario"></a>Senaryo
Contoso olan birden çok platform için oyunlar oluşturan bir oyun şirket: oyun konsolları, taşınabilir bilgisayar cihazları ve kişisel bilgisayarlar (bilgisayarlar). Bu oyun oynatıcıları gibi günlük verilerini büyük miktarda parçaları kullanım desenlerini, oyun stil ve hello kullanıcı tercihleri hello oluşturulur.  Demografik, bölge ile birleştirildiğinde ve ürün veri Contoso analytics tooguide tooenhance oyuncuların deneyimi ve yükseltmeler için hedef hakkında onları ve oyun gerçekleştirebilir satın alır. 

Contoso'nun hedef kendi oyuncunun oyun geçmiş hello temelinde tooidentify yukarı satış/çapraz satış fırsatları ve ilgi çekici özellikler toodrive iş büyümesi ekleyin ve daha iyi bir deneyim toocustomers sağlayın. Bu kullanım durumu için bir iş örnek olarak bir oyun şirket kullanırız. Merhaba şirket toooptimize oyuncuların davranışı temelinde kendi oyunlar ister. Bu ilkeler, müşterilerinin kendi mal ve hizmet çevresinde tooengage istediği tooany iş uygulayın ve müşterilerin deneyimini geliştirmek.

Bu çözümde, Contoso tooevaluate hello son başlattı bir pazarlama kampanyası verimliliğini istemektedir. Biz hello ham oyun günlükleri, işlem ile başlayın ve coğrafi konum verilerle zenginleştirmek, başvuru verileri reklam ile katılması ve son olarak bunları bir Azure SQL veritabanı tooanalyze hello kampanya etkisi kopyalayın.

## <a name="deploy-solution"></a>Çözümü dağıtma
Tüm tooaccess ihtiyacınız olduğunu ve bu basit kullanım örneği deneme olan bir [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/), bir [Azure Blob Depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account)ve bir [Azure SQL veritabanı](../sql-database/sql-database-get-started.md). Ardışık düzen tarafından hello profil hello müşteri dağıttığınız **örnek ardışık düzen** döşeme veri fabrikanızın hello giriş sayfasında.

1. Veri Fabrikası oluşturun veya varolan bir veri fabrikası açın. Bkz: [veritabanını Data Factory kullanarak Blob Storage tooSQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adımları toocreate veri fabrikası için.
2. Merhaba, **DATA FACTORY** hello veri fabrikası dikey penceresinde hello tıklatın **örnek ardışık düzen** döşeme.

    ![Örnek komut zincirleri döşeme](./media/data-factory-samples/SamplePipelinesTile.png)
3. Merhaba, **örnek ardışık düzen** dikey penceresinde hello tıklatın **profil müşteri** toodeploy istediğiniz.

    ![Örnek komut zincirleri dikey penceresi](./media/data-factory-samples/SampleTile.png)
4. Merhaba örnek için yapılandırma ayarlarını belirtin. Örneğin, Azure depolama hesabı adı ve anahtar, Azure SQL sunucu adı, veritabanı, kullanıcı kimliği ve parola.

    ![Örnek dikey penceresi](./media/data-factory-samples/SampleBlade.png)
5. Merhaba yapılandırma ayarlarını belirtme ile tamamladıktan sonra tıklatın **oluşturma** örnek ardışık düzen ve hello ardışık düzen tarafından kullanılan bağlı hizmetler/tablolar hello toocreate ve dağıtın.
6. Tıklattığınız önceki üzerinde hello hello örnek kutucuğuna dağıtım hello durumunu görmek **örnek ardışık düzen** dikey.

    ![Dağıtım durumu](./media/data-factory-samples/DeploymentStatus.png)
7. Merhaba gördüğünüzde **dağıtım başarılı** hello bölme hello örnek, Kapat hello için iletide **örnek ardışık düzen** dikey.  
8. Üzerinde **DATA FACTORY** dikey penceresinde, gördüğünüz bağlı hizmetler, veri kümeleri ve işlem hatlarını tooyour veri fabrikası eklenir.  

    ![Data Factory dikey penceresi](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Çözüme genel bakış
Bu basit kullanım örneği, nasıl Azure Data Factory tooingest, hazırlamak, dönüştürmek, analiz ve kullanabilirsiniz veri yayımlama örneği olarak kullanılabilir.

![Uçtan uca iş akışı](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Bu şekil dağıtıldıktan sonra hello veri ardışık Azure portal hello nasıl göründüğünü gösterir.

1. Merhaba **PartitionGameLogsPipeline** hello ham oyun olayları blob depolama alanından okur ve yıl, ay ve gün göre bölümler oluşturur.
2. Merhaba **EnrichGameLogsPipeline** bölümlenmiş oyun olaylar coğrafi kod başvuru verileri ile birleştirir ve IP adreslerini toohello karşılık gelen coğrafi konumda eşleyerek hello veri aşağıdakilere zenginleştirir.
3. Merhaba **AnalyzeMarketingCampaignPipeline** ardışık düzen zenginleştirilmiş hello verileri kullanır ve pazarlama kampanyası etkinliğini içeren veri toocreate hello son çıktı reklam hello ile işler.

Bu örnekte, Data Factory giriş verilerini, dönüştürme ve işlem hello verileri kopyalayın ve hello son veri tooan Azure SQL veritabanı çıkış kullanılan tooorchestrate etkinlikleri ' dir.  Veri ardışık hello ağının görselleştirmek, bunları yönetmek ve hello UI kendi durumunu izleyin.

## <a name="benefits"></a>Avantajlar
Kendi kullanıcı profili analiz en iyi duruma getirme ve iş hedeflerini ile hizalama, oyun şirket mümkün tooquickly toplama kullanım desenlerini olduğu ve pazarlama kampanyaları hello verimliliğini analiz edin.

