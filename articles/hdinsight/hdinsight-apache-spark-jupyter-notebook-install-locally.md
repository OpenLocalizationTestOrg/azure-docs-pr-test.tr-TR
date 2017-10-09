---
title: "yerel olarak Jupyter aaaInstall & tooan Azure Hdınsight Spark küme bağlanma | Microsoft Docs"
description: "Bilgi nasıl tooinstall Jupyter Not Defteri, bilgisayarınıza yerel olarak ve Azure hdınsight'ta Apache Spark kümesinde tooan bağlanın."
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
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="d9efe-103">Jupyter not defteri bilgisayarınıza yüklemek ve tooApache hdınsight'ta Spark bağlanın</span><span class="sxs-lookup"><span data-stu-id="d9efe-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="d9efe-104">Bu makalede, bilgi nasıl tooinstall Jupyter Not Defteri, ile Merhaba (Python için) özel PySpark ve Spark Sihirli ve hello not defteri tooan Hdınsight kümesine bağlanın (Scala için) Spark çekirdekler ile.</span><span class="sxs-lookup"><span data-stu-id="d9efe-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="d9efe-105">Yerel bilgisayarınızda nedeniyle tooinstall Jupyter sayısı olabilir ve bazı zorluklar de olabilir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="d9efe-106">Bunun hakkında daha fazla bilgi için hello bölümüne bakın [neden yüklediğimde Jupyter bilgisayarımda](#why-should-i-install-jupyter-on-my-computer) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="d9efe-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="d9efe-107">Jupyter ve hello Spark Sihirli bilgisayarınızda yükleme ilgili üç önemli adımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="d9efe-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="d9efe-108">Jupyter not defteri yükleyin</span><span class="sxs-lookup"><span data-stu-id="d9efe-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="d9efe-109">Merhaba PySpark ve Spark çekirdekler Spark Sihirli hello ile yükleme</span><span class="sxs-lookup"><span data-stu-id="d9efe-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="d9efe-110">Hdınsight'ta Spark Sihirli tooaccess Spark kümesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d9efe-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="d9efe-111">Merhaba özel tekrar ve hello Spark Sihirli Hdınsight kümesi ile Jupyter not defterleri için kullanılabilir hakkında daha fazla bilgi için bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Apache Spark Linux kümeleri Hdınsight'ta](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="d9efe-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9efe-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d9efe-112">Prerequisites</span></span>
<span data-ttu-id="d9efe-113">Burada listelenen hello Önkoşullar Jupyter yüklemek için değildir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="d9efe-114">Merhaba dizüstü yüklendikten sonra bağlanan hello Jupyter not defteri tooan Hdınsight kümesi için bunlar.</span><span class="sxs-lookup"><span data-stu-id="d9efe-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="d9efe-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d9efe-115">An Azure subscription.</span></span> <span data-ttu-id="d9efe-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d9efe-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d9efe-117">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="d9efe-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="d9efe-118">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d9efe-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="d9efe-119">Jupyter not defteri bilgisayarınıza yüklemek</span><span class="sxs-lookup"><span data-stu-id="d9efe-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="d9efe-120">Jupyter not defterleri yükleyebilmek için önce Python yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="d9efe-121">Python ve Jupyter kullanılabilir hello bir parçası olarak [Anaconda dağıtım](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="d9efe-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="d9efe-122">Anaconda yüklediğinizde, Python bir dağıtımını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="d9efe-123">Anaconda yüklendikten sonra uygun komutlarını çalıştırarak hello Jupyter yükleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="d9efe-124">Merhaba karşıdan [Anaconda yükleyici](https://www.continuum.io/downloads) platform ve çalışma hello kurulumu için.</span><span class="sxs-lookup"><span data-stu-id="d9efe-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="d9efe-125">Çalışan hello Kurulum Sihirbazı sırasında hello seçeneği tooadd Anaconda tooyour PATH değişkeni seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9efe-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="d9efe-126">Çalışma hello aşağıdaki tooinstall Jupyter komutu.</span><span class="sxs-lookup"><span data-stu-id="d9efe-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="d9efe-127">Jupyter yükleme hakkında daha fazla bilgi için bkz: [Anaconda kullanarak Jupyter yükleme](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="d9efe-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="d9efe-128">Merhaba tekrar ve Spark Sihirli yükleyin</span><span class="sxs-lookup"><span data-stu-id="d9efe-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="d9efe-129">Yönergeler için nasıl tooinstall hello Spark Sihirli, hello PySpark ve Spark çekirdekler hello Yükleme'ndaki yönergeleri izlediğinizden hello [sparkmagic belgelerine](https://github.com/jupyter-incubator/sparkmagic#installation) github'da.</span><span class="sxs-lookup"><span data-stu-id="d9efe-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="d9efe-130">Merhaba hello Spark Sihirli belgelerinde ilk adım, tooinstall Spark Sihirli ister.</span><span class="sxs-lookup"><span data-stu-id="d9efe-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="d9efe-131">Bu ilk adım hello bağlantısında komutları, bağlanacağınız hello Hdınsight kümesi hello sürümüne bağlı olarak aşağıdaki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="d9efe-132">Bundan sonra hello Spark Sihirli belgelerindeki adımları kalan hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="d9efe-133">Tooinstall hello farklı tekrar istiyorsanız hello Spark Sihirli yükleme yönergeleri bölüm 3. adım gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="d9efe-134">Yürüterek sparkmagic 0.2.3 kümeleri v3.4 için yükleyin`pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="d9efe-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="d9efe-135">Kümeleri v3.5 ve v3.6 için sparkmagic 0.11.2 yürüterek yükleme`pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="d9efe-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="d9efe-136">Spark Sihirli tooconnect tooHDInsight Spark kümesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d9efe-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="d9efe-137">Bu bölümde, Azure Hdınsight'ta oluşturmuş olmalısınız önceki tooconnect tooan Apache Spark kümesi yüklü hello Spark Sihirli yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d9efe-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="d9efe-138">Merhaba Jupyter yapılandırma bilgileri genellikle hello kullanıcıların giriş dizininde depolanır.</span><span class="sxs-lookup"><span data-stu-id="d9efe-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="d9efe-139">toolocate giriş dizininize herhangi bir platformda işletim sistemi, türü hello aşağıdaki komutları.</span><span class="sxs-lookup"><span data-stu-id="d9efe-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="d9efe-140">Merhaba Python Kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="d9efe-140">Start hello Python shell.</span></span> <span data-ttu-id="d9efe-141">Bir komut penceresinde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d9efe-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="d9efe-142">Hello Python kabuğu, komut toofind hello giriş dizini çıkışı aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="d9efe-143">Toohello giriş dizinine gidin ve adlı bir klasör oluşturun **.sparkmagic** zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="d9efe-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="d9efe-144">Merhaba klasör içinde adlı bir dosya oluşturun **config.json** ve JSON parçacığı içindeki aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="d9efe-145">Yedek **{USERNAME}**, **{CLUSTERDNSNAME}**, ve **{BASE64ENCODEDPASSWORD}** uygun değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="d9efe-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="d9efe-146">Sık kullanılan programlama dili veya çevrimiçi toogenerate bir Base64 ile kodlanmış parolayı yardımcı programları sayısı için gerçek parolanızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9efe-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="d9efe-147">Hello sağ sinyal ayarlarında yapılandırdığınız `config.json`.</span><span class="sxs-lookup"><span data-stu-id="d9efe-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="d9efe-148">Aynı düzeydeki hello hello sırasında bu ayarları eklemelisiniz `kernel_python_credentials` ve `kernel_scala_credentials` parçacıkları, eklenen önceki.</span><span class="sxs-lookup"><span data-stu-id="d9efe-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="d9efe-149">Bunu nasıl ve nerede tooadd hello sinyal ayarları, bir örnek için bkz [örnek config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="d9efe-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="d9efe-150">İçin `sparkmagic 0.2.3` (v3.4 kümeleri) içerir:</span><span class="sxs-lookup"><span data-stu-id="d9efe-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="d9efe-151">İçin `sparkmagic 0.11.2` (kümeleri v3.5 ve v3.6) içerir:</span><span class="sxs-lookup"><span data-stu-id="d9efe-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="d9efe-152">Sinyal oturumları sızdırılmaz tooensure gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="d9efe-153">Bir bilgisayar toosleep geçip geçmeyeceğini veya kapatılmış açtığınızda hello sinyal gönderilmez, oturum hello olan içinde kaynaklanan temizlendi.</span><span class="sxs-lookup"><span data-stu-id="d9efe-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="d9efe-154">Kümeleri v3.4 için bu davranış toodisable istiyorsanız hello Livy config ayarlayabilirsiniz `livy.server.interactive.heartbeat.timeout` çok`0` hello Ambari UI gelen.</span><span class="sxs-lookup"><span data-stu-id="d9efe-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="d9efe-155">Yukarıdaki hello 3.5 yapılandırma ayarlamazsanız kümeleri v3.5 için hello oturum silinmez.</span><span class="sxs-lookup"><span data-stu-id="d9efe-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="d9efe-156">Jupyter başlatın.</span><span class="sxs-lookup"><span data-stu-id="d9efe-156">Start Jupyter.</span></span> <span data-ttu-id="d9efe-157">Komut hello komut isteminden aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9efe-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="d9efe-158">Merhaba Jupyter not defteri ve hello tekrar ile Merhaba Spark Sihirli kullanabileceğiniz kullanarak toohello küme bağlanabildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d9efe-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="d9efe-159">Merhaba aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-159">Perform hello following steps.</span></span>

    <span data-ttu-id="d9efe-160">a.</span><span class="sxs-lookup"><span data-stu-id="d9efe-160">a.</span></span> <span data-ttu-id="d9efe-161">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9efe-161">Create a new notebook.</span></span> <span data-ttu-id="d9efe-162">Merhaba sağ köşesinden tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="d9efe-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="d9efe-163">Merhaba varsayılan çekirdek görmelisiniz **Python2** ve yüklediğiniz, iki yeni çekirdek hello **PySpark** ve **Spark**.</span><span class="sxs-lookup"><span data-stu-id="d9efe-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="d9efe-164">Tıklatın **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="d9efe-164">Click **PySpark**.</span></span>

    <span data-ttu-id="d9efe-165">![Jupyter not defterlerinde çekirdekler](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter not defterlerinde çekirdekler")</span><span class="sxs-lookup"><span data-stu-id="d9efe-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="d9efe-166">b.</span><span class="sxs-lookup"><span data-stu-id="d9efe-166">b.</span></span> <span data-ttu-id="d9efe-167">Aşağıdaki kod parçacığını hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d9efe-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="d9efe-168">Başarılı bir şekilde hello çıkış alabilir, bağlantı toohello Hdınsight kümenize test edilir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="d9efe-169">Tooupdate hello dizüstü bilgisayar yapılandırmasını tooconnect tooa farklı küme istiyorsanız hello config.json hello yeni değerleri kümesiyle yukarıdaki adım 3'te gösterildiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9efe-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="d9efe-170">Bilgisayarımda neden Jupyter yüklediğimde?</span><span class="sxs-lookup"><span data-stu-id="d9efe-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="d9efe-171">Bir sayı olabilir, neden tooinstall Jupyter bilgisayarınızda istediğiniz, ardından bağlanmak nedeniyle tooa Spark küme Hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="d9efe-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="d9efe-172">Jupyter not defterleri zaten hello Azure hdınsight'ta Spark kümesi üzerinde kullanılabilir olsa bile, bilgisayarınıza Jupyter yükleme seçeneği toocreate defterlerinizi yerel olarak Merhaba, uygulamanızı çalıştıran bir kümeye karşı test etmek ve hello karşıya sağlar not defterlerini toohello küme.</span><span class="sxs-lookup"><span data-stu-id="d9efe-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="d9efe-173">tooupload hello not defterlerini toohello küme ya da karşıya yüklediğiniz bunları çalıştıran hello Jupyter Not Defteri veya hello kullanarak küme veya hello kümesi ile ilişkili hello depolama hesabındaki toohello /HdiNotebooks klasörü kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="d9efe-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="d9efe-174">Not defterlerini hello kümede nasıl depolandığını daha fazla bilgi için bkz: [Jupyter not defterleri depolandığı](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="d9efe-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="d9efe-175">Kullanılabilir Hello dizüstü bilgisayarlarla yerel olarak uygulama gereksinimi temel alan toodifferent Spark kümeleri bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="d9efe-176">GitHub tooimplement kaynak denetim sistemi kullanabilir ve sürüm denetimi hello dizüstü bilgisayarlar için sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="d9efe-177">Ayrıca, birden çok kullanıcı çalışabilir hello ile aynı işbirliğine dayalı bir ortam olabilir dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="d9efe-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="d9efe-178">Bir küme bile sahip olmadan dizüstü bilgisayarlar ile yerel olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="d9efe-179">Bir küme tootest defterlerinizi karşı yeterlidir, değil toomanually defterlerinizi veya geliştirme ortamında yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9efe-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="d9efe-180">Bu tooconfigure hello Jupyter yükleme hello kümede olandan daha kolay tooconfigure kendi yerel geliştirme ortamı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d9efe-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="d9efe-181">Bir veya daha fazla uzak kümelerini yapılandırma olmadan yerel olarak yüklü tüm hello yazılım avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9efe-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="d9efe-182">Yerel bilgisayarınızda yüklü Jupyter ile birden çok kullanıcı hello çalıştırabilirsiniz aynı Spark küme hello hello aynı Not aynı anda.</span><span class="sxs-lookup"><span data-stu-id="d9efe-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="d9efe-183">Böyle bir durumda, birden çok Livy oturumu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d9efe-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="d9efe-184">Bir sorunu yaşayıp çalıştırmak ve hangi Livy oturumu toowhich kullanıcının ait olduğu bir karmaşık görev tootrack olacaktır, toodebug istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d9efe-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="d9efe-185"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d9efe-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d9efe-186">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="d9efe-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d9efe-187">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="d9efe-187">Scenarios</span></span>
* [<span data-ttu-id="d9efe-188">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="d9efe-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d9efe-189">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="d9efe-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d9efe-190">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="d9efe-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d9efe-191">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="d9efe-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d9efe-192">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="d9efe-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d9efe-193">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d9efe-193">Create and run applications</span></span>
* [<span data-ttu-id="d9efe-194">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9efe-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d9efe-195">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d9efe-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d9efe-196">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="d9efe-196">Tools and extensions</span></span>
* [<span data-ttu-id="d9efe-197">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="d9efe-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d9efe-198">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="d9efe-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d9efe-199">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="d9efe-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d9efe-200">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="d9efe-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d9efe-201">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="d9efe-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="d9efe-202">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="d9efe-202">Manage resources</span></span>
* [<span data-ttu-id="d9efe-203">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="d9efe-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d9efe-204">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="d9efe-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
