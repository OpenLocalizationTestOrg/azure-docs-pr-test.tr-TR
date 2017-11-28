---
title: "Hive tabloları Hive sorguları ile keşfedin | Microsoft Docs"
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
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="406fe-103">Hive sorguları ile Hive tablosundaki verileri keşfedin</span><span class="sxs-lookup"><span data-stu-id="406fe-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="406fe-104">Bu belgede bir Hdınsight Hadoop kümesindeki Hive tablolarındaki verileri keşfetmek için kullanılan örnek Hive komut dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="406fe-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="406fe-105">Aşağıdaki **menü** araçları çeşitli depolama ortamlarından verileri araştırmak için nasıl kullanılacağını açıklayan konulara bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="406fe-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="406fe-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="406fe-106">Prerequisites</span></span>
<span data-ttu-id="406fe-107">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="406fe-107">This article assumes that you have:</span></span>

* <span data-ttu-id="406fe-108">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="406fe-108">Created an Azure storage account.</span></span> <span data-ttu-id="406fe-109">Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="406fe-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="406fe-110">Özelleştirilmiş bir Hadoop kümesine Hdınsight hizmetiyle sağlandı.</span><span class="sxs-lookup"><span data-stu-id="406fe-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="406fe-111">Yönergeler gerekiyorsa bkz [Advanced Analytics için Azure Hdınsight Hadoop kümeleri özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="406fe-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="406fe-112">Azure Hdınsight Hadoop kümeleri Hive tabloları için verileri karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="406fe-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="406fe-113">Sahip değil,'ndaki yönergeleri izleyin. [Hive tabloları oluşturma ve yük verileri](machine-learning-data-science-move-hive-tables.md) verileri ilk Hive tablolara yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="406fe-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="406fe-114">Küme uzak erişim etkin.</span><span class="sxs-lookup"><span data-stu-id="406fe-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="406fe-115">Yönergeler gerekiyorsa bkz [Hadoop küme baş düğümü erişim](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="406fe-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="406fe-116">Hive sorguları göndermek yönergeler gerekiyorsa bkz [nasıl Hive sorguları göndermek için](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="406fe-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="406fe-117">Veri keşfi için örnek Hive sorgusu komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="406fe-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="406fe-118">Bölüm başına gözlemleri sayısını alın`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="406fe-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="406fe-119">Gün başına gözlemleri sayısını alın`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="406fe-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="406fe-120">Kategorik bir sütunda düzeylerini Al</span><span class="sxs-lookup"><span data-stu-id="406fe-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="406fe-121">İki kategorik sütun arada düzey sayısını Al`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="406fe-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="406fe-122">Sayısal sütunlar için dağıtım Al</span><span class="sxs-lookup"><span data-stu-id="406fe-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="406fe-123">İki tablo birleştirme kayıtları Ayıkla</span><span class="sxs-lookup"><span data-stu-id="406fe-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="406fe-124">Ücreti seyahat veri senaryoları için ek sorgu komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="406fe-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="406fe-125">Özel sorgular örnekleri [NYC ücreti seyahat veri](http://chriswhong.com/open-data/foil_nyc_taxi/) senaryoları burada da sunulmaktadır [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="406fe-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="406fe-126">Bu sorgular zaten belirtilen veri şeması varsa ve çalıştırmak için gönderilmesi hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="406fe-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

