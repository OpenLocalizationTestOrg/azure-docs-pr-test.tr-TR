---
title: "Hive tabloları Hive sorguları ile aaaExplore verileri | Microsoft Docs"
description: "Hive sorgularını kullanarak Hive tablolarındaki verileri keşfedin."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="cc8de-103">Hive sorguları ile Hive tablosundaki verileri keşfedin</span><span class="sxs-lookup"><span data-stu-id="cc8de-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="cc8de-104">Bu belgede kullanılan tooexplore verileri bir Hdınsight Hadoop kümesindeki Hive tablolardaki örnek Hive komut dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc8de-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="cc8de-105">Merhaba aşağıdaki **menü** nasıl toouse tooexplore veri çeşitli depolama ortamlarından araçları açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="cc8de-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="cc8de-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc8de-106">Prerequisites</span></span>
<span data-ttu-id="cc8de-107">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="cc8de-107">This article assumes that you have:</span></span>

* <span data-ttu-id="cc8de-108">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cc8de-108">Created an Azure storage account.</span></span> <span data-ttu-id="cc8de-109">Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="cc8de-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="cc8de-110">Özelleştirilmiş bir Hadoop kümesine hello Hdınsight hizmeti ile sağlandı.</span><span class="sxs-lookup"><span data-stu-id="cc8de-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="cc8de-111">Yönergeler gerekiyorsa bkz [Advanced Analytics için Azure Hdınsight Hadoop kümeleri özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cc8de-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="cc8de-112">Merhaba veri Azure Hdınsight Hadoop kümeleri karşıya yüklenen tooHive tablolarda olmuştur.</span><span class="sxs-lookup"><span data-stu-id="cc8de-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="cc8de-113">Sahip değil, hello yönergeleri izleyin. [oluşturma ve yük veri tooHive tabloları](machine-learning-data-science-move-hive-tables.md) tooupload veri tooHive tabloları ilk.</span><span class="sxs-lookup"><span data-stu-id="cc8de-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="cc8de-114">Uzaktan erişim toohello küme etkin.</span><span class="sxs-lookup"><span data-stu-id="cc8de-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="cc8de-115">Yönergeler gerekiyorsa bkz [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="cc8de-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="cc8de-116">Yönergeler gerekiyorsa bkz: toosubmit Hive sorguları [nasıl tooSubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="cc8de-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="cc8de-117">Veri keşfi için örnek Hive sorgusu komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="cc8de-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="cc8de-118">Bölüm başına gözlemleri Hello sayısını alın`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="cc8de-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="cc8de-119">Gün başına gözlemleri Hello sayısını alın`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="cc8de-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="cc8de-120">Merhaba düzeylerini kategorik sütunda Al</span><span class="sxs-lookup"><span data-stu-id="cc8de-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="cc8de-121">İki kategorik sütun arada Hello düzey sayısını Al`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="cc8de-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="cc8de-122">Merhaba dağıtım sayısal sütunlar için alma</span><span class="sxs-lookup"><span data-stu-id="cc8de-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="cc8de-123">İki tablo birleştirme kayıtları Ayıkla</span><span class="sxs-lookup"><span data-stu-id="cc8de-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="cc8de-124">Ücreti seyahat veri senaryoları için ek sorgu komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="cc8de-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="cc8de-125">Çok belirli sorguları örnekleri[NYC ücreti seyahat veri](http://chriswhong.com/open-data/foil_nyc_taxi/) senaryoları burada da sunulmaktadır [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="cc8de-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="cc8de-126">Bu sorgular zaten belirtilen veri şeması varsa ve gönderilen hazır toobe toorun.</span><span class="sxs-lookup"><span data-stu-id="cc8de-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

