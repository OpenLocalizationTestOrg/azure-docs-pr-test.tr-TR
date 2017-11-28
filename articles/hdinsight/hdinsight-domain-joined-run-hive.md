---
title: "Etki alanına katılmış Hdınsight - Azure aaaConfigure Hive ilkelerinde | Microsoft Docs"
description: "Öğrenin ...."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="68210-103">Etki alanına katılmış HDInsight’ta (Önizleme) Hive ilkelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="68210-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="68210-104">Bilgi nasıl Hive için tooconfigure Apache bırakabilmenizi ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="68210-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="68210-105">Bu makalede, iki bırakabilmenizi ilkeleri toorestrict erişim toohello hivesampletable oluşturun.</span><span class="sxs-lookup"><span data-stu-id="68210-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="68210-106">Merhaba hivesampletable Hdınsight kümeleri ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="68210-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="68210-107">Merhaba ilkeleri yapılandırdıktan sonra Excel ve ODBC sürücüsü tooconnect tooHive tablolarını Hdınsight'ta kullanın.</span><span class="sxs-lookup"><span data-stu-id="68210-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68210-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="68210-108">Prerequisites</span></span>
* <span data-ttu-id="68210-109">Etki alanına katılmış HDInsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="68210-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="68210-110">Bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="68210-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="68210-111">Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013’ün tek başına sürümü veya Office 2010 Professional Plus yüklü iş istasyonu.</span><span class="sxs-lookup"><span data-stu-id="68210-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="68210-112">TooApache bırakabilmenizi yönetici UI Bağlan</span><span class="sxs-lookup"><span data-stu-id="68210-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="68210-113">**tooconnect tooRanger yönetim kullanıcı Arabirimi**</span><span class="sxs-lookup"><span data-stu-id="68210-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="68210-114">Tarayıcıdan tooRanger yönetici UI bağlayın.</span><span class="sxs-lookup"><span data-stu-id="68210-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="68210-115">Merhaba URL'dir https://&lt;ClusterName >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="68210-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="68210-116">Ranger’ın kimlik bilgileri Hadoop kümesinin kimlik bilgilerinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="68210-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="68210-117">önbelleğe alınan Hadoop kimlik bilgilerini kullanarak tooprevent tarayıcılar yeni InPrivate tarayıcı penceresini tooconnect toohello bırakabilmenizi yönetici kullanıcı arabirimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="68210-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="68210-118">Merhaba Küme Yöneticisi etki alanı kullanıcı adı ve parola kullanarak oturum açın:</span><span class="sxs-lookup"><span data-stu-id="68210-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![HDInsight etki alanına katılmış Ranger ana sayfası](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="68210-120">Ranger şu an için yalnızca Yarn ve Hive ile birlikte çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="68210-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="68210-121">Etki alanı kullanıcılarını oluşturma</span><span class="sxs-lookup"><span data-stu-id="68210-121">Create Domain users</span></span>
<span data-ttu-id="68210-122">[Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) bölümünde hiveruser1 ve hiveuser2 kullanıcılarını oluşturmuştunuz.</span><span class="sxs-lookup"><span data-stu-id="68210-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="68210-123">Bu öğreticide hello iki kullanıcı hesabını kullanır.</span><span class="sxs-lookup"><span data-stu-id="68210-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="68210-124">Ranger ilkelerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="68210-124">Create Ranger policies</span></span>
<span data-ttu-id="68210-125">Bu bölümde hivesampletable erişimi için iki Ranger ilkesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="68210-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="68210-126">Farklı sütun kümelerine select izni vereceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68210-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="68210-127">İki kullanıcı da [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) bölümünde oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="68210-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="68210-128">Merhaba sonraki bölümde hello iki ilke Excel'de test edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="68210-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="68210-129">**toocreate bırakabilmenizi ilkeleri**</span><span class="sxs-lookup"><span data-stu-id="68210-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="68210-130">Ranger Yönetici Arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="68210-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="68210-131">Bkz: [tooApache bırakabilmenizi yönetici UI bağlanmak](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="68210-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="68210-132">****Hive**’ın altındaki &lt;KümeAdı>_hive** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="68210-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="68210-133">Önceden yapılandırılmış iki ilke göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68210-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="68210-134">Tıklatın **yeni ilke Ekle**ve değerlerini aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="68210-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="68210-135">Policy name: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="68210-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="68210-136">Hive Database: default</span><span class="sxs-lookup"><span data-stu-id="68210-136">Hive Database: default</span></span>
   * <span data-ttu-id="68210-137">table: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="68210-137">table: hivesampletable</span></span>
   * <span data-ttu-id="68210-138">Hive column: *</span><span class="sxs-lookup"><span data-stu-id="68210-138">Hive column: *</span></span>
   * <span data-ttu-id="68210-139">Select User: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="68210-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="68210-140">Permissions: select</span><span class="sxs-lookup"><span data-stu-id="68210-140">Permissions: select</span></span>

     ![HDInsight etki alanına katılmış Ranger Hive ilkesi yapılandırma](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="68210-142">.</span><span class="sxs-lookup"><span data-stu-id="68210-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="68210-143">Bir etki alanı kullanıcısı Kullanıcı Seç doldurulmazsa bırakabilmenizi toosync aad'ye için birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="68210-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="68210-144">Tıklatın **Ekle** toosave hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="68210-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="68210-145">Merhaba son iki adımı toocreate hello aşağıdaki özelliklere başka bir ilke Yinele:</span><span class="sxs-lookup"><span data-stu-id="68210-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="68210-146">Policy name: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="68210-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="68210-147">Hive Database: default</span><span class="sxs-lookup"><span data-stu-id="68210-147">Hive Database: default</span></span>
   * <span data-ttu-id="68210-148">table: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="68210-148">table: hivesampletable</span></span>
   * <span data-ttu-id="68210-149">Hive column: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="68210-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="68210-150">Select User: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="68210-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="68210-151">Permissions: select</span><span class="sxs-lookup"><span data-stu-id="68210-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="68210-152">Hive ODBC veri kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="68210-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="68210-153">Merhaba yönergeleri bulunabilir [oluşturma Hive ODBC veri kaynağını](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="68210-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="68210-154">Özellik</span><span class="sxs-lookup"><span data-stu-id="68210-154">Property</span></span>|<span data-ttu-id="68210-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="68210-155">Description</span></span>
    ---|---
    <span data-ttu-id="68210-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="68210-156">Data Source Name</span></span>|<span data-ttu-id="68210-157">Bir ad tooyour veri kaynağı verin</span><span class="sxs-lookup"><span data-stu-id="68210-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="68210-158">Host</span><span class="sxs-lookup"><span data-stu-id="68210-158">Host</span></span>|<span data-ttu-id="68210-159">&lt;HDInsightKümesiAdı>.azurehdinsight.net yazın.</span><span class="sxs-lookup"><span data-stu-id="68210-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="68210-160">Örnek: HDIKumesi.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="68210-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="68210-161">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="68210-161">Port</span></span>|<span data-ttu-id="68210-162"><strong>443</strong> yazın.</span><span class="sxs-lookup"><span data-stu-id="68210-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="68210-163">(Bu bağlantı noktasına 563 too443 değiştirildi.)</span><span class="sxs-lookup"><span data-stu-id="68210-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="68210-164">Database</span><span class="sxs-lookup"><span data-stu-id="68210-164">Database</span></span>|<span data-ttu-id="68210-165"><strong>Default</strong>’u kullanın.</span><span class="sxs-lookup"><span data-stu-id="68210-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="68210-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="68210-166">Hive Server Type</span></span>|<span data-ttu-id="68210-167"><strong>Hive Server 2</strong>’yi seçin</span><span class="sxs-lookup"><span data-stu-id="68210-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="68210-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="68210-168">Mechanism</span></span>|<span data-ttu-id="68210-169"><strong>Azure HDInsight Service</strong>’i seçin</span><span class="sxs-lookup"><span data-stu-id="68210-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="68210-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="68210-170">HTTP Path</span></span>|<span data-ttu-id="68210-171">Boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="68210-171">Leave it blank.</span></span>
    <span data-ttu-id="68210-172">User Name</span><span class="sxs-lookup"><span data-stu-id="68210-172">User Name</span></span>|<span data-ttu-id="68210-173">Girin hiveuser1@contoso158.onmicrosoft.com. Farklı ise hello etki alanı adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="68210-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="68210-174">Parola</span><span class="sxs-lookup"><span data-stu-id="68210-174">Password</span></span>|<span data-ttu-id="68210-175">Merhaba parola için hiveuser1 girin.</span><span class="sxs-lookup"><span data-stu-id="68210-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="68210-176">Emin tooclick olun **Test** hello veri kaynağı kaydetmeden önce.</span><span class="sxs-lookup"><span data-stu-id="68210-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="68210-177">HDInsight’tan Excel’e veri aktarma</span><span class="sxs-lookup"><span data-stu-id="68210-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="68210-178">Merhaba son bölümünde iki ilke yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="68210-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="68210-179">hiveuser1 hello tüm hello sütunlarda izni seçin, ve iki sütun izninin seçin hello hiveuser2 sahiptir.</span><span class="sxs-lookup"><span data-stu-id="68210-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="68210-180">Bu bölümde, hello iki kullanıcı tooimport verileri Excel'e taklit.</span><span class="sxs-lookup"><span data-stu-id="68210-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="68210-181">Excel’de yeni veya mevcut bir çalışma kitabını açın.</span><span class="sxs-lookup"><span data-stu-id="68210-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="68210-182">Merhaba gelen **veri** sekmesini tıklatın, **diğer veri kaynaklardan**ve ardından **Veri Bağlantı Sihirbazı'ndan** toolaunch hello **Veri Bağlantı Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="68210-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="68210-183">![Veri bağlantı sihirbazını açın][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="68210-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="68210-184">Seçin **ODBC DSN** hello veri kaynağı ve ardından olarak **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="68210-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="68210-185">ODBC veri kaynaklarından select hello veri kaynağı hello önceki adımda oluşturduğunuz adı ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="68210-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="68210-186">Başlangıç Sihirbazı'nda hello küme Hello parolayı yeniden girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="68210-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="68210-187">Merhaba bekleyin **veritabanı ve Tablo Seç** iletişim tooopen.</span><span class="sxs-lookup"><span data-stu-id="68210-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="68210-188">Bu işlem birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="68210-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="68210-189">**hivesampletable**’ı seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="68210-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="68210-190">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="68210-190">Click **Finish**.</span></span>
8. <span data-ttu-id="68210-191">Merhaba, **Veri Al** iletişim kutusunda, değiştirmek veya hello sorgusunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="68210-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="68210-192">Bu nedenle, toodo'ı tıklatın **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="68210-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="68210-193">Bu işlem birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="68210-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="68210-194">Merhaba tıklatın **tanımı** sekmesini hello komut metni:</span><span class="sxs-lookup"><span data-stu-id="68210-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="68210-195">Tanımladığınız hello bırakabilmenizi ilkeleri tarafından hiveuser1 tüm hello sütunlarda select izni vardır.</span><span class="sxs-lookup"><span data-stu-id="68210-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="68210-196">Bu nedenle bu sorgu hiveuser1 kullanıcısının kimlik bilgileriyle çalışır ancak hiveuser2 kullanıcısının kimlik bilgileriyle çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="68210-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="68210-197">![Bağlantı Özellikleri][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="68210-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="68210-198">Tıklatın **Tamam** tooclose hello bağlantı özellikleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="68210-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="68210-199">Tıklatın **Tamam** tooclose hello **Veri Al** iletişim.</span><span class="sxs-lookup"><span data-stu-id="68210-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="68210-200">Hiveuser1 Hello parolasını yeniden girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="68210-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="68210-201">Veri içe aktarılan tooExcel büyümeden birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="68210-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="68210-202">İşlem tamamlandığında 11 veri sütunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68210-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="68210-203">Merhaba son bölümünde oluşturduğunuz tootest hello ikinci ilke (okuma hivesampletable devicemake)</span><span class="sxs-lookup"><span data-stu-id="68210-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="68210-204">Excel'de yeni bir sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="68210-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="68210-205">Merhaba son yordamı tooimport hello verileri izleyin.</span><span class="sxs-lookup"><span data-stu-id="68210-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="68210-206">vereceğiniz hello yalnızca hiveuser1'ın yerine toouse hiveuser2'in kimlik bilgilerini değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="68210-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="68210-207">Bu hiveuser2 yalnızca izni toosee iki sütun olduğu için başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="68210-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="68210-208">Aşağıdaki hata hello alın:</span><span class="sxs-lookup"><span data-stu-id="68210-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="68210-209">İzleme hello aynı yordamı tooimport veri.</span><span class="sxs-lookup"><span data-stu-id="68210-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="68210-210">Bu süre, hiveuser2'in kimlik bilgilerini kullanın ve ayrıca hello select deyiminden değiştirin:</span><span class="sxs-lookup"><span data-stu-id="68210-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="68210-211">yerine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="68210-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="68210-212">İşlem tamamlandığında iki veri sütununun içe aktarıldığını göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68210-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68210-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="68210-213">Next steps</span></span>
* <span data-ttu-id="68210-214">Etki alanına katılmış HDInsight kümesini yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="68210-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="68210-215">Etki alanına katılmış HDInsight kümesini yönetmek için bkz. [Etki alanına katılmış HDInsight kümelerini yönetme](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="68210-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="68210-216">Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="68210-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="68210-217">Bağlanma JDBC Hive kullanarak Hive için bkz: [tooHive hello Hive JDBC sürücüsü kullanarak Azure hdınsight'ta Bağlan](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="68210-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="68210-218">Hive ODBC kullanarak bağlanan Excel tooHadoop için bkz: [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="68210-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="68210-219">Power Query kullanarak bağlanan Excel tooHadoop için bkz: [Power Query kullanarak bağlanmak Excel tooHadoop](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="68210-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
