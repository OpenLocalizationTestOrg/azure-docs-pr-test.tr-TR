---
title: "Merhaba Hive ODBC sürücüsü - Azure Hdınsight ile aaaConnect Excel tooHadoop | Microsoft Docs"
description: "Excel tooquery veri Hdınsight kümelerinde Microsoft Excel için Microsoft Hive ODBC sürücüsü tooset ayarlama ve kullanma nasıl hello öğrenin."
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="ad4eb-104">Azure hdınsight'ta Excel tooHadoop hello Microsoft Hive ODBC sürücüsü ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="ad4eb-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="ad4eb-105">Microsoft'un büyük veri çözüm Microsoft Business Intelligence (BI) bileşenleri hello Azure Hdınsight tarafından dağıtılan Apache Hadoop kümeleri ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="ad4eb-106">Bu tümleştirme hello özelliği tooconnect Excel toohello Hive veri ambarının hello Microsoft Hive açık veritabanı bağlantısı (ODBC) sürücüsü kullanarak hdınsight'ta Hadoop kümesi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="ad4eb-107">Ayrıca bir Hdınsight kümesi ve diğer veri kaynakları ile ilgili olası tooconnect hello veri olduğundan, diğer (olmayan-Hdınsight) Hadoop kümeleri, hello kullanarak Excel'den Excel için Microsoft Power Query Eklentisi.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="ad4eb-108">Yükleme ve Power Query kullanma hakkında daha fazla bilgi için bkz: [Power Query ile bağlanma Excel tooHDInsight][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="ad4eb-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="ad4eb-109">Merhaba adımları sırasında bu makalede bir ya da Linux ile kullanılabilir veya Windows tabanlı Hdınsight kümesi, Windows hello istemci iş istasyonu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="ad4eb-110">**Önkoşullar**:</span><span class="sxs-lookup"><span data-stu-id="ad4eb-110">**Prerequisites**:</span></span>

<span data-ttu-id="ad4eb-111">Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad4eb-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="ad4eb-112">**Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="ad4eb-113">toocreate biri bkz [Azure Hdınsight kullanmaya başlama][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="ad4eb-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="ad4eb-114">**Bir iş istasyonu** Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 tek başına veya Office 2010 Professional Plus ile.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="ad4eb-115">Microsoft Hive ODBC sürücüsünü yükleme</span><span class="sxs-lookup"><span data-stu-id="ad4eb-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="ad4eb-116">Microsoft Hive ODBC sürücüsü hello yükleyip [Yükleme Merkezi'nden][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="ad4eb-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="ad4eb-117">Bu sürücü Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 ve Windows Server 2012, 32 bit veya 64 bit sürümlerinde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="ad4eb-118">Merhaba sürücüsü verir bağlantı tooAzure Hdınsight (sürüm 1.6 ve üstü) ve Azure Hdınsight öykünücüsünde (v.1.0.0.0 ve üzeri).</span><span class="sxs-lookup"><span data-stu-id="ad4eb-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="ad4eb-119">Merhaba uygulaması hello ODBC sürücüsü kullandığınız hello sürümüyle eşleşen hello sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="ad4eb-120">Bu öğretici için Office Excel'den hello sürücü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="ad4eb-121">Hive ODBC veri kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad4eb-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="ad4eb-122">Merhaba aşağıdaki adımlarda size yol gösterecektir toocreate Hive ODBC veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="ad4eb-123">Windows 8 veya Windows 10, hello Windows anahtar tooopen hello başlangıç ekranı tuşuna basın ve ardından yazın **veri kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="ad4eb-124">Tıklatın **ODBC veri kaynakları (32 bit) ayarlamanız** veya **ODBC veri kaynakları (64 bit) ayarlamanız** Office sürümüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="ad4eb-125">Windows 7 kullanıyorsanız seçin **ODBC veri kaynakları (32 bit)** veya **ODBC veri kaynakları (64 bit)** gelen **Yönetimsel Araçlar**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="ad4eb-126">Merhaba göreceksiniz **ODBC Veri Kaynağı Yöneticisi** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="ad4eb-127">![OBDC Veri Kaynağı Yöneticisi](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "ODBC Veri Kaynağı Yöneticisi kullanan bir DSN'ye yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="ad4eb-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="ad4eb-128">Kullanıcı DNS'den tıklatın **Ekle** tooopen hello **yeni veri kaynağı oluştur** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="ad4eb-129">Seçin **Microsoft Hive ODBC sürücüsü**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="ad4eb-130">Merhaba göreceksiniz **Microsoft Hive ODBC sürücüsü DNS Kurulumu** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="ad4eb-131">Değerleri aşağıdaki hello seçin veya yazın:</span><span class="sxs-lookup"><span data-stu-id="ad4eb-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="ad4eb-132">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad4eb-132">Property</span></span> | <span data-ttu-id="ad4eb-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad4eb-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="ad4eb-134">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="ad4eb-134">Data Source Name</span></span> |<span data-ttu-id="ad4eb-135">Bir ad tooyour veri kaynağı verin</span><span class="sxs-lookup"><span data-stu-id="ad4eb-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="ad4eb-136">Host</span><span class="sxs-lookup"><span data-stu-id="ad4eb-136">Host</span></span> |<span data-ttu-id="ad4eb-137">&lt;HDInsightKümesiAdı>.azurehdinsight.net yazın.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="ad4eb-138">Örnek: HDIKumesi.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="ad4eb-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="ad4eb-139">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="ad4eb-139">Port</span></span> |<span data-ttu-id="ad4eb-140"><strong>443</strong> yazın.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="ad4eb-141">(Bu bağlantı noktasına 563 too443 değiştirildi.)</span><span class="sxs-lookup"><span data-stu-id="ad4eb-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="ad4eb-142">Database</span><span class="sxs-lookup"><span data-stu-id="ad4eb-142">Database</span></span> |<span data-ttu-id="ad4eb-143"><strong>Default</strong>’u kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="ad4eb-144">Mechanism</span><span class="sxs-lookup"><span data-stu-id="ad4eb-144">Mechanism</span></span> |<span data-ttu-id="ad4eb-145"><strong>Azure HDInsight Service</strong>’i seçin</span><span class="sxs-lookup"><span data-stu-id="ad4eb-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="ad4eb-146">User Name</span><span class="sxs-lookup"><span data-stu-id="ad4eb-146">User Name</span></span> |<span data-ttu-id="ad4eb-147">Hdınsight küme HTTP kullanıcının kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="ad4eb-148">Merhaba varsayılan kullanıcı adı <strong>yönetici</strong>.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="ad4eb-149">Parola</span><span class="sxs-lookup"><span data-stu-id="ad4eb-149">Password</span></span> |<span data-ttu-id="ad4eb-150">Hdınsight küme kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="ad4eb-151">Bazı önemli parametreleri toobe tıkladığınızda farkında **Gelişmiş Seçenekler**:</span><span class="sxs-lookup"><span data-stu-id="ad4eb-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="ad4eb-152">Parametre</span><span class="sxs-lookup"><span data-stu-id="ad4eb-152">Parameter</span></span> | <span data-ttu-id="ad4eb-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad4eb-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="ad4eb-154">Yerel sorgu kullanma</span><span class="sxs-lookup"><span data-stu-id="ad4eb-154">Use Native Query</span></span> |<span data-ttu-id="ad4eb-155">Seçildiğinde, hello ODBC sürücüsü HiveQL tooconvert TSQL denemez.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="ad4eb-156">Yalnızca % 100 saf HiveQL ifadelerini gönderiliyor emin olduğunuzda kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="ad4eb-157">TooSQL sunucusu veya Azure SQL veritabanına bağlanırken denetlenmeyen bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="ad4eb-158">Satır blok alınarak</span><span class="sxs-lookup"><span data-stu-id="ad4eb-158">Rows fetched per block</span></span> |<span data-ttu-id="ad4eb-159">Bu parametre ayarlama, çok sayıda kayıt getirilirken gerekli tooensure en iyi performanslarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="ad4eb-160">Varsayılan dize sütun uzunluğu, ikili sütun uzunluğu, ondalık sütun ölçeği</span><span class="sxs-lookup"><span data-stu-id="ad4eb-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="ad4eb-161">Merhaba veri türü uzunlukları ve Precision bilgisayarlar, verinin nasıl döndürüldüğüne etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="ad4eb-162">Son döndürülen yanlış bilgi toobe neden duyarlık ve/veya kesme tooloss.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="ad4eb-163">![Gelişmiş Seçenekleri](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN Gelişmiş yapılandırma seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="ad4eb-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="ad4eb-164">Tıklatın **Test** tootest hello veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="ad4eb-165">Merhaba veri kaynağının doğru şekilde yapılandırıldığında, gösterir *TESTLERİ başarıyla tamamlandı!*.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="ad4eb-166">Tıklatın **Tamam** tooclose hello Test iletişim.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="ad4eb-167">Merhaba yeni veri kaynağı üzerinde hello listelenen **ODBC Veri Kaynağı Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="ad4eb-168">Tıklatın **Tamam** tooexit hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="ad4eb-169">HDInsight’tan Excel’e veri aktarma</span><span class="sxs-lookup"><span data-stu-id="ad4eb-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="ad4eb-170">Merhaba aşağıdaki adımlar bir Hive tablosu hello yolu tooimport verileri'hello önceki bölümde oluşturduğunuz hello ODBC veri kaynağını kullanan bir Excel çalışma kitabına açıklar.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="ad4eb-171">Excel’de yeni veya mevcut bir çalışma kitabını açın.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="ad4eb-172">Merhaba gelen **veri** sekmesini tıklatın, **Veri Al**, tıklatın **diğer kaynaklardan**ve ardından **gelen ODBC** toolaunch hello  **Veri Bağlantı Sihirbazı**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="ad4eb-173">![Açık Veri Bağlantı Sihirbazı'nı](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "açık Veri Bağlantı Sihirbazı")</span><span class="sxs-lookup"><span data-stu-id="ad4eb-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="ad4eb-174">Select hello veri kaynağı hello son bölümünde oluşturduğunuz adı ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="ad4eb-175">Hadoop kullanıcı adını girin (Merhaba varsayılan addır yönetici) ve parola hello ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="ad4eb-176">Gezgin üzerinde genişletin **HIVE**, genişletin **varsayılan**, tıklatın **hivesampletable**ve ardından **yük**.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="ad4eb-177">Veri içe aktarılan tooExcel büyümeden birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="ad4eb-178">![Hdınsight Hive ODBC Gezgini](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "açık Veri Bağlantı Sihirbazı")</span><span class="sxs-lookup"><span data-stu-id="ad4eb-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="ad4eb-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad4eb-179">Next steps</span></span>
<span data-ttu-id="ad4eb-180">Bu makalede, nasıl toouse hello hello Hdınsight hizmeti Microsoft Hive ODBC sürücüsü tooretrieve verileri Excel'e öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="ad4eb-181">Benzer şekilde, Hdınsight hizmeti hello SQL veritabanına veri alabilir.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="ad4eb-182">Ayrıca bir Hdınsight hizmeti olası tooupload verisine olur.</span><span class="sxs-lookup"><span data-stu-id="ad4eb-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="ad4eb-183">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="ad4eb-183">toolearn more, see:</span></span>

* <span data-ttu-id="ad4eb-184">[Hdınsight kullanma uçuş gecikme verilerini çözümleme][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="ad4eb-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="ad4eb-185">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ad4eb-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ad4eb-186">[Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="ad4eb-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


