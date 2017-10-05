---
title: "Jupyter yerel olarak yüklemek ve bir Azure Hdınsight Spark kümesine bağlanma | Microsoft Docs"
description: "Jupyter not defteri bilgisayarınıza yerel olarak yüklemek ve Azure hdınsight'ta Apache Spark kümesinde bağlanmak öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="19b2d-103">Jupyter not defteri bilgisayarınıza yüklemek ve hdınsight'ta Apache Spark bağlanın</span><span class="sxs-lookup"><span data-stu-id="19b2d-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="19b2d-104">Bu makalede (Python için) özel PySpark ve Spark Sihirli ile (Scala için) Spark çekirdekler ile Jupyter Not Defteri, yükleme ve not defteri bir Hdınsight kümesine bağlanma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="19b2d-105">Bir dizi Jupyter yerel bilgisayarınıza yüklemek için neden olabilir ve bazı zorluklar de olabilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="19b2d-106">Hakkında daha fazla bilgi için bu bölüme bakın [neden yüklediğimde Jupyter bilgisayarımda](#why-should-i-install-jupyter-on-my-computer) bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="19b2d-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="19b2d-107">Jupyter ve Spark Sihirli bilgisayarınızda yükleme ilgili üç önemli adımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="19b2d-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="19b2d-108">Jupyter not defteri yükleyin</span><span class="sxs-lookup"><span data-stu-id="19b2d-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="19b2d-109">İle Spark Sihirli PySpark ve Spark tekrar yükleme</span><span class="sxs-lookup"><span data-stu-id="19b2d-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="19b2d-110">Hdınsight'ta Spark kümesinde erişmek için Spark Sihirli yapılandırın</span><span class="sxs-lookup"><span data-stu-id="19b2d-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="19b2d-111">Özel tekrar ve Hdınsight kümesi ile Jupyter not defterleri için kullanılabilir Spark Sihirli hakkında daha fazla bilgi için bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Apache Spark Linux kümeleri Hdınsight'ta](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="19b2d-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19b2d-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="19b2d-112">Prerequisites</span></span>
<span data-ttu-id="19b2d-113">Burada listelenen önkoşulları Jupyter yüklemek için değildir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="19b2d-114">Bu, Not Defteri yüklendikten sonra Jupyter not defteri bir Hdınsight kümesine bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19b2d-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="19b2d-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="19b2d-115">An Azure subscription.</span></span> <span data-ttu-id="19b2d-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="19b2d-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="19b2d-117">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="19b2d-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="19b2d-118">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="19b2d-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="19b2d-119">Jupyter not defteri bilgisayarınıza yüklemek</span><span class="sxs-lookup"><span data-stu-id="19b2d-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="19b2d-120">Jupyter not defterleri yükleyebilmek için önce Python yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="19b2d-121">Python ve Jupyter kullanılabilir olarak parçası [Anaconda dağıtım](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="19b2d-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="19b2d-122">Anaconda yüklediğinizde, Python bir dağıtımını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="19b2d-123">Anaconda yüklendikten sonra uygun komutlarını çalıştırarak Jupyter yükleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="19b2d-124">Karşıdan [Anaconda yükleyici](https://www.continuum.io/downloads) platform ve Çalıştır kurulumu için.</span><span class="sxs-lookup"><span data-stu-id="19b2d-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="19b2d-125">Kurulum Sihirbazı'nı çalıştırırken PATH değişkenine Anaconda ekleme seçeneğini seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="19b2d-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="19b2d-126">Jupyter yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="19b2d-127">Jupyter yükleme hakkında daha fazla bilgi için bkz: [Anaconda kullanarak Jupyter yükleme](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="19b2d-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="19b2d-128">Spark Sihirli ve tekrar yükleyin</span><span class="sxs-lookup"><span data-stu-id="19b2d-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="19b2d-129">Spark Sihirli yükleme hakkında yönergeler için PySpark ve Spark çekirdekleri kurulum yönergelerini izleyin [sparkmagic belgelerine](https://github.com/jupyter-incubator/sparkmagic#installation) github'da.</span><span class="sxs-lookup"><span data-stu-id="19b2d-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="19b2d-130">İlk adım Spark Sihirli belgelerinde Spark Sihirli yüklemenizi ister.</span><span class="sxs-lookup"><span data-stu-id="19b2d-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="19b2d-131">Bu ilk adım bağlantıda bağlanacağınız Hdınsight kümesi sürümüne bağlı olarak aşağıdaki komutları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="19b2d-132">Bundan sonra Spark Sihirli belgelerindeki kalan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="19b2d-133">Farklı tekrar yüklemek istiyorsanız, Spark Sihirli yükleme yönergeleri bölümünde 3. adım gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="19b2d-134">Yürüterek sparkmagic 0.2.3 kümeleri v3.4 için yükleyin`pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="19b2d-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="19b2d-135">Kümeleri v3.5 ve v3.6 için sparkmagic 0.11.2 yürüterek yükleme`pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="19b2d-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="19b2d-136">Spark Sihirli Hdınsight Spark kümeye bağlanmak için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="19b2d-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="19b2d-137">Bu bölümde daha önce Azure Hdınsight'ta oluşturmuş olmalısınız bir Apache Spark kümesi bağlanmak için yüklü Spark Sihirli yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="19b2d-138">Jupyter yapılandırma bilgileri, genellikle kullanıcıların giriş dizininde depolanır.</span><span class="sxs-lookup"><span data-stu-id="19b2d-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="19b2d-139">Giriş dizininize herhangi bir işletim sistemi platformda bulmak için aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="19b2d-140">Python Kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-140">Start the Python shell.</span></span> <span data-ttu-id="19b2d-141">Bir komut penceresinde, aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="19b2d-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="19b2d-142">Python Kabuğu giriş dizini bulmak için aşağıdaki komutu girin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="19b2d-143">Giriş dizinine gidin ve adlı bir klasör oluşturun **.sparkmagic** zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="19b2d-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="19b2d-144">Klasör içinde adlı bir dosya oluşturun **config.json** ve onun içindeki aşağıdaki JSON parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="19b2d-145">Yedek **{USERNAME}**, **{CLUSTERDNSNAME}**, ve **{BASE64ENCODEDPASSWORD}** uygun değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="19b2d-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="19b2d-146">Yardımcı programlar, sık kullanılan programlama dili veya çevrimiçi çeşitli gerçek parolanızı bir base64 ile kodlanmış parolası oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b2d-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="19b2d-147">Sağ sinyal ayarlarında yapılandırdığınız `config.json`.</span><span class="sxs-lookup"><span data-stu-id="19b2d-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="19b2d-148">Bu ayarları aynı düzeyde eklemelisiniz `kernel_python_credentials` ve `kernel_scala_credentials` parçacıkları, eklenen önceki.</span><span class="sxs-lookup"><span data-stu-id="19b2d-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="19b2d-149">Örneği nasıl ve nerede sinyal ayarları eklemek bu bkz [örnek config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="19b2d-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="19b2d-150">İçin `sparkmagic 0.2.3` (v3.4 kümeleri) içerir:</span><span class="sxs-lookup"><span data-stu-id="19b2d-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="19b2d-151">İçin `sparkmagic 0.11.2` (kümeleri v3.5 ve v3.6) içerir:</span><span class="sxs-lookup"><span data-stu-id="19b2d-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="19b2d-152">Sinyal oturumları sızdırılmaz sağlamak için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="19b2d-153">Bir bilgisayar uyku moduna geçer veya kapatılmış, sinyal gönderilmez, elde edilen oturum temizlendi.</span><span class="sxs-lookup"><span data-stu-id="19b2d-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="19b2d-154">Kümeleri v3.4 için bu davranışı devre dışı bırakmak isterseniz, Livy config ayarlayabilirsiniz `livy.server.interactive.heartbeat.timeout` için `0` Ambari UI gelen.</span><span class="sxs-lookup"><span data-stu-id="19b2d-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="19b2d-155">Yukarıdaki 3.5 yapılandırma ayarlamazsanız kümeleri v3.5 için oturum silinmez.</span><span class="sxs-lookup"><span data-stu-id="19b2d-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="19b2d-156">Jupyter başlatın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-156">Start Jupyter.</span></span> <span data-ttu-id="19b2d-157">Komut isteminde aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="19b2d-158">Jupyter Not Defteri kullanarak kümeye bağlanabilir ve ile tekrar kullanılabilir Spark Sihirli kullanabileceğiniz doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="19b2d-159">Aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-159">Perform the following steps.</span></span>

    <span data-ttu-id="19b2d-160">a.</span><span class="sxs-lookup"><span data-stu-id="19b2d-160">a.</span></span> <span data-ttu-id="19b2d-161">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19b2d-161">Create a new notebook.</span></span> <span data-ttu-id="19b2d-162">Sağ köşesinden tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="19b2d-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="19b2d-163">Varsayılan çekirdek görmelisiniz **Python2** ve yüklediğiniz, iki yeni çekirdekler **PySpark** ve **Spark**.</span><span class="sxs-lookup"><span data-stu-id="19b2d-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="19b2d-164">Tıklatın **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="19b2d-164">Click **PySpark**.</span></span>

    <span data-ttu-id="19b2d-165">![Jupyter not defterlerinde çekirdekler](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter not defterlerinde çekirdekler")</span><span class="sxs-lookup"><span data-stu-id="19b2d-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="19b2d-166">b.</span><span class="sxs-lookup"><span data-stu-id="19b2d-166">b.</span></span> <span data-ttu-id="19b2d-167">Aşağıdaki kod parçacığını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="19b2d-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="19b2d-168">Çıktı başarıyla alabilir, Hdınsight kümesi bağlantınızı test edilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="19b2d-169">Farklı bir kümeye bağlanmak için dizüstü bilgisayar yapılandırmasını güncelleştirmek istiyorsanız, config.json değerleri, yeni kümesiyle yukarıdaki adım 3'te gösterildiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="19b2d-170">Bilgisayarımda neden Jupyter yüklediğimde?</span><span class="sxs-lookup"><span data-stu-id="19b2d-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="19b2d-171">Pek çok neden Jupyter bilgisayarınıza yüklemek ve Hdınsight Spark kümesinde bağlanmaya isteyebileceğinizi olabilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="19b2d-172">Jupyter not defterleri zaten Azure Hdınsight Spark kümesinde kullanılabilir olsa bile, bilgisayarınıza Jupyter yükleme, defterlerinizi oluşturma seçeneğini yerel olarak çalışan bir küme karşı uygulamanızı test etmek ve kümeye not defterlerini karşıya yükleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="19b2d-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="19b2d-173">Dizüstü bilgisayarlar kümeye karşıya yüklemek için çalışan Jupyter Not Defteri veya küme kullanarak bunları karşıya yükleme veya bunları kümeyle ilişkili depolama hesabındaki /HdiNotebooks klasörüne kaydedin.</span><span class="sxs-lookup"><span data-stu-id="19b2d-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="19b2d-174">Dizüstü bilgisayarlar kümede nasıl depolandığını daha fazla bilgi için bkz: [Jupyter not defterleri depolandığı](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="19b2d-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="19b2d-175">Yerel olarak not defterlerini kullanılabilir uygulama gereksinimi temel alan farklı Spark kümelerine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="19b2d-176">Kaynak denetim sistemi uygulamak ve dizüstü bilgisayarlar için sürüm denetimi sağlamak için GitHub'ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b2d-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="19b2d-177">Ayrıca, birden çok kullanıcı aynı not defteri ile burada çalışabilir işbirliğine dayalı bir ortam olabilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="19b2d-178">Bir küme bile sahip olmadan dizüstü bilgisayarlar ile yerel olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="19b2d-179">Yalnızca el ile defterlerinizi veya geliştirme ortamında yönetmediğinizden defterlerinizi karşı test etmek için bir küme gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="19b2d-180">Kümede Jupyter yüklemesini yapılandırmak yerine, kendi yerel geliştirme ortamı yapılandırmak daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="19b2d-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="19b2d-181">Bir veya daha fazla uzak kümelerini yapılandırma olmadan yerel olarak yüklü tüm yazılımların avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b2d-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="19b2d-182">Yerel bilgisayarınızda yüklü Jupyter ile birden çok kullanıcı aynı dizüstü bilgisayar aynı Spark kümesi üzerinde aynı anda çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b2d-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="19b2d-183">Böyle bir durumda, birden çok Livy oturumu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="19b2d-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="19b2d-184">Bir sorunu yaşayıp çalıştırın ve, hata ayıklamak istediğiniz, hangi Livy oturumu izlemek için karmaşık bir görev hangi kullanıcıya ait olur.</span><span class="sxs-lookup"><span data-stu-id="19b2d-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="19b2d-185"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="19b2d-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="19b2d-186">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="19b2d-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="19b2d-187">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="19b2d-187">Scenarios</span></span>
* [<span data-ttu-id="19b2d-188">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="19b2d-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="19b2d-189">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="19b2d-190">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="19b2d-191">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="19b2d-192">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="19b2d-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="19b2d-193">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="19b2d-193">Create and run applications</span></span>
* [<span data-ttu-id="19b2d-194">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="19b2d-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="19b2d-195">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="19b2d-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="19b2d-196">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="19b2d-196">Tools and extensions</span></span>
* [<span data-ttu-id="19b2d-197">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisini kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="19b2d-198">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="19b2d-199">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="19b2d-200">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="19b2d-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="19b2d-201">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="19b2d-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="19b2d-202">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="19b2d-202">Manage resources</span></span>
* [<span data-ttu-id="19b2d-203">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="19b2d-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="19b2d-204">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="19b2d-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
