---
title: "Veri bilimi üzerinde Linux veri bilimi sanal makine | Microsoft Docs"
description: "Linux veri bilimi VM ile birkaç genel veri bilimi görevleri gerçekleştirme."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="9d0f9-103">Linux Veri Bilimi Sanal Makinesinde veri bilimi</span><span class="sxs-lookup"><span data-stu-id="9d0f9-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="9d0f9-104">Bu kılavuzda, Linux veri bilimi VM ile birçok ortak veri bilimi görevlerinin nasıl gerçekleştirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="9d0f9-105">Linux veri bilimi sanal makine (DSVM) veri analizi ve makine öğrenme için yaygın olarak kullanılan bir araç koleksiyonu ile önceden yüklenmiş olan Azure üzerinde kullanılabilir bir sanal makine görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="9d0f9-106">Anahtar yazılım bileşenleri içinde listelenen [Linux veri bilimi sanal makine sağlama](machine-learning-data-science-linux-dsvm-intro.md) konu.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="9d0f9-107">VM görüntüsü yüklemek ve araçların her biri ayrı ayrı yapılandırmak zorunda kalmadan dakika cinsinden veri bilimi yapılması başlamak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="9d0f9-108">Kolayca VM gerekirse ölçeklendirmek ve kullanılmadığında durdurun.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="9d0f9-109">Bu nedenle bu kaynak, esnek ve ekonomik içindir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="9d0f9-110">Bu kılavuzda gösterilen veri bilimi görevleri konusunda özetlenen adımları [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="9d0f9-111">Bu işlem için etkili bir şekilde akıllı uygulamaları oluşturma yaşam döngüsü üzerinde işbirliği yapmak için veri bilimcilerine ekiplerin sağlayan veri bilimi sistematik bir yaklaşım sunar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="9d0f9-112">Veri bilimi işlemi da bir kişi tarafından izlenebilir veri bilimi için yinelemeli bir çerçeve sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="9d0f9-113">Biz analiz [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) bu kılavuzda veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="9d0f9-114">Bu e-postaların istenmeyen posta ya da (olmadıkları istenmeyen posta anlamına gelir) ham, olarak işaretlenmiş kümesidir ve ayrıca e-posta içeriğini bazı istatistiklerle içerir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="9d0f9-115">Dahil edilen istatistikleri sonraki ancak bir bölüm içinde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d0f9-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d0f9-116">Prerequisites</span></span>
<span data-ttu-id="9d0f9-117">Linux veri bilimi sanal makine kullanmadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="9d0f9-118">Bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-118">An **Azure subscription**.</span></span> <span data-ttu-id="9d0f9-119">Zaten bir yoksa, bkz: [ücretsiz Azure hesabınızı bugün oluşturmak](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9d0f9-120">A [ **Linux veri bilimi VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="9d0f9-121">Bu VM sağlama hakkında daha fazla bilgi için bkz: [Linux veri bilimi sanal makine sağlama](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="9d0f9-122">[X2Go](http://wiki.x2go.org/doku.php) bilgisayarınızda yüklü ve bir XFCE oturumu açılır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="9d0f9-123">Yükleme ve yapılandırma hakkında bilgi için bir **X2Go istemci**, bkz: [yükleme ve yapılandırma X2Go istemci](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="9d0f9-124">Bir **AzureML hesap**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-124">An **AzureML account**.</span></span> <span data-ttu-id="9d0f9-125">Zaten, yeni bir kayıt yoksa, [AzureML giriş sayfası](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="9d0f9-126">Başlamanıza yardımcı olmak için ücretsiz kullanım katmanı yoktur.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="9d0f9-127">Spambase dataset indirin</span><span class="sxs-lookup"><span data-stu-id="9d0f9-127">Download the spambase dataset</span></span>
<span data-ttu-id="9d0f9-128">[Spambase](https://archive.ics.uci.edu/ml/datasets/spambase) veri kümesi yalnızca 4601 örnekleri içeren veri görece küçük kümesidir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="9d0f9-129">Bu, veri bilimi VM şekliyle anahtar özelliklerinden bazıları tutmasını kaynak gereksinimlerini uygun gösteren sırasında kullanmak için uygun bir boyutudur.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0f9-130">Bu kılavuz bir D2 v2 ölçekli Linux veri bilimi sanal makinede oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="9d0f9-131">Bu boyut DSVM yordamları bu kılavuzda işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="9d0f9-132">Daha fazla depolama alanı gerekiyorsa, ek diskleri oluşturun ve sizin VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="9d0f9-133">Bu diskleri kalıcı Azure depolama kullandığından, sunucu yeniden boyutlandırma nedeniyle sağlama veya kapatılmış olsa bile verilerini korunur.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="9d0f9-134">Bir disk ekleyin ve VM'nize eklemek için'ndaki yönergeleri izleyin [bir Linux VM için bir disk eklemek](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9d0f9-135">Azure komut satırı DSVM üzerinde önceden yüklenmiş arabirimi (Azure CLI), aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="9d0f9-136">Bu nedenle bu yordamları tamamen sanal makineden kendisini yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="9d0f9-137">Depolama artırmak için başka bir seçenek kullanmaktır [Azure dosyaları](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="9d0f9-138">Veri yüklemek için bir terminal penceresi açın ve şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="9d0f9-139">İndirilen Dosya sağlandığından üstbilgi sahip başka bir dosya oluşturmak bir başlık satırı yok.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="9d0f9-140">Uygun üst bilgilerle bir dosya oluşturmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="9d0f9-141">Ardından komutu ile birlikte iki dosyaları birleştirme:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="9d0f9-142">Veri kümesi istatistikleri çeşitli türlerde her e-postaya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="9d0f9-143">Sütunları ister ***word\_freq\_WORD*** eşleşen sözcükleri e-postadaki yüzdesini belirtmek *WORD*.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="9d0f9-144">Örneğin, varsa *word\_freq\_olun* %1 e-posta içindeki tüm sözcükleri bundan sonra 1 ' dir *olun*.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="9d0f9-145">Sütunları ister ***char\_freq\_CHAR*** olan tüm e-posta karakter yüzdesini belirtmek *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="9d0f9-146">***büyük\_çalıştırmak\_uzunluğu\_uzun*** büyük harf bir dizi uzun uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="9d0f9-147">***büyük\_çalıştırmak\_uzunluğu\_ortalama*** büyük harf ve tüm dizilerini ortalama uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="9d0f9-148">***büyük\_çalıştırmak\_uzunluğu\_toplam*** büyük harf ve tüm dizilerini toplam uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="9d0f9-149">***istenmeyen posta*** veya e-posta istenmeyen posta kabul olup olmadığını gösterir (1 istenmeyen posta, 0 = değil istenmeyen posta =).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="9d0f9-150">Microsoft R açık ile dataset keşfedin</span><span class="sxs-lookup"><span data-stu-id="9d0f9-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="9d0f9-151">Şimdi verileri incelemek ve bazı temel makine r ile öğrenme yapın Veri bilimi VM ile birlikte gelen [Microsoft R açık](https://mran.revolutionanalytics.com/open/) önceden yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="9d0f9-152">Birden çok iş parçacıklı matematik kitaplıkları R bu sürümündeki çeşitli tek iş parçacıklı sürümleri daha iyi performans sunar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="9d0f9-153">Microsoft R açık de yeniden Üretilebilirlik CRAN Paket Deposu görüntüsünü kullanarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="9d0f9-154">Bu kılavuzda kullanılan kod örnekleri kopyalarını almak için kopyalama **Azure-Machine-Learning-Data-Bilim** git, VM önceden yüklenmiş olduğu kullanarak deposu.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="9d0f9-155">Git komut satırından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="9d0f9-156">Bir terminal penceresi açın ve yeni bir R oturumu R etkileşimli konsol ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0f9-157">Bu gibi durumlarda, Rstudio'dan da için aşağıdaki yordamları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="9d0f9-158">Rstudio'dan yüklemek için bu bir terminal komutunu yürütün:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="9d0f9-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="9d0f9-159">Veri içeri aktarın ve ortamını ayarlamak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="9d0f9-160">Her sütunun hakkındaki özet istatistikleri görmek için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="9d0f9-161">Verileri farklı bir görünüm için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="9d0f9-162">Bu, her bir değişken ve ilk birkaç değerleri türü veri kümesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="9d0f9-163">*İstenmeyen posta* sütun bir tamsayı olarak okundu, ancak gerçekte kategorik olan değişkeni (veya faktörü).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="9d0f9-164">Türünü ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="9d0f9-165">Keşif biraz analiz yapma kullanmak [ggplot2](http://ggplot2.org/) paketini, VM üzerinde zaten yüklü R için popüler bir grafik kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="9d0f9-166">, Daha önce görüntülenen özet verileri biz Özet istatistikleri ünlem işareti karakteri sıklığını sahip olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="9d0f9-167">Şimdi bu sıklıklarını burada aşağıdaki komutlarla çizimi:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="9d0f9-168">Şimdi sıfır çubuğu çizim eğriltme olduğundan, bunu kurtulun:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="9d0f9-169">Önemsiz olmayan yoğunluğu ilginç görünüyor 1 yukarıda yoktur.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="9d0f9-170">Bu verileri yalnızca bakalım:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="9d0f9-171">Ardından istenmeyen posta vs ham tarafından böl:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="9d0f9-172">Bu örnekler, içerdikleri verileri araştırmak için benzer çizimleri diğer sütunların yapmak etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="9d0f9-173">Eğitme ve test ML modeli</span><span class="sxs-lookup"><span data-stu-id="9d0f9-173">Train and test an ML model</span></span>
<span data-ttu-id="9d0f9-174">Şimdi şimdi birkaç span veya ham içeren olarak dataset postalarda sınıflandırmak için makine öğrenimi modellerini eğitmek.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="9d0f9-175">Biz karar ağacı modeli ve bu bölümdeki rastgele orman modeli eğitmek ve kendi tahminleri kendi doğruluğunu test edin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0f9-176">Aşağıdaki kod içinde kullanılan rpart (özyinelemeli bölümlendirme ve regresyon ağaçlarında) paketi veri bilimi VM üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="9d0f9-177">Öncelikle, şimdi dataset eğitim ve test ayarlar böl:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="9d0f9-178">Ve e-postaları sınıflandırmak için karar ağacı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="9d0f9-179">Sonuç şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="9d0f9-181">Ne kadar iyi eğitim kümesinde gerçekleştirip belirlemek için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="9d0f9-182">Ne kadar iyi belirlemek için test kümesinde gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="9d0f9-183">Ayrıca bir rastgele orman modeli deneyelim.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-183">Let's also try a random forest model.</span></span> <span data-ttu-id="9d0f9-184">Rastgele ormanları karar ağaçları çok sayıda eğitmek ve tüm ayrı ayrı karar ağaçları sınıflandırmaları modunun bir sınıf çıkış.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="9d0f9-185">Bir eğitim veri kümesi overfit işlemciler karar ağacı modeli için düzeltirken yaklaşım öğrenme daha güçlü bir makine sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="9d0f9-186">Azure ML model dağıtma</span><span class="sxs-lookup"><span data-stu-id="9d0f9-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="9d0f9-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML), derleme ve Tahmine dayalı analiz modelleriniz dağıtma daha kolay hale getirir bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="9d0f9-188">AzureML iyi özelliklerini bir web hizmeti olarak herhangi bir R işlev yayımlama yeteneğini biridir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="9d0f9-189">AzureML R paketi dağıtım sağ DSVM bizim R oturum yapmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="9d0f9-190">Önceki bölümde karar ağacı koddan dağıtmak için Azure Machine Learning Studio'da oturum açmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="9d0f9-191">Çalışma alanı Kimliğinizi ve bir yetki belirteci oturum açmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="9d0f9-192">Bu değerleri bulmak ve onlarla AzureML değişkenlerini başlatmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="9d0f9-193">Seçin **ayarları** sol menüdeki.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="9d0f9-194">Not, **çalışma alanı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="9d0f9-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="9d0f9-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="9d0f9-196">Seçin **yetkilendirme belirteçleri** Not ve genel gider menüden, **birincil yetkilendirme belirteci**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="9d0f9-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="9d0f9-197">Yük **AzureML** paketini ve belirteç ve çalışma alanı Kimliğiniz ile değişkenlerin değerleri üzerinde DSVM R oturumunuzda ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="9d0f9-198">Şimdi uygulamak bu tanıtımı kolaylaştırmak için model basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="9d0f9-199">Kök yakın karar ağacında üç değişkenleri seçin ve yalnızca bu üç değişkenin kullanarak yeni bir ağaç yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="9d0f9-200">Özellikleri bir girdi olarak alır ve tahmin edilen değerler döndüren bir tahmin işlevinde ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="9d0f9-201">AzureML kullanmaya predictSpam işlevi yayımlama **publishWebService** işlevi:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="9d0f9-202">Bu işlev alır **predictSpam** işlev, adlı bir web hizmeti oluşturur **spamWebService** girişleri ve çıkışları ile tanımlanan ve yeni uç noktası hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="9d0f9-203">Yayımlanan web hizmetinde, kendi API uç noktası gibi ayrıntılarını görüntülemek ve erişim anahtarları komutuyla:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="9d0f9-204">İlk denemenin testinin 10 satır ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="9d0f9-205">Kullanılabilir diğer araçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="9d0f9-205">Use other tools available</span></span>
<span data-ttu-id="9d0f9-206">Kalan bölümleri bazı Linux veri bilimi VM'de yüklü Araçları'nın nasıl kullanıldığını gösterir. Açıklanan araçları listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="9d0f9-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="9d0f9-207">XGBoost</span></span>
* <span data-ttu-id="9d0f9-208">Python</span><span class="sxs-lookup"><span data-stu-id="9d0f9-208">Python</span></span>
* <span data-ttu-id="9d0f9-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="9d0f9-209">Jupyterhub</span></span>
* <span data-ttu-id="9d0f9-210">Çıngırağı</span><span class="sxs-lookup"><span data-stu-id="9d0f9-210">Rattle</span></span>
* <span data-ttu-id="9d0f9-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="9d0f9-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="9d0f9-212">SQL Server veri ambarı</span><span class="sxs-lookup"><span data-stu-id="9d0f9-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="9d0f9-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="9d0f9-213">XGBoost</span></span>
<span data-ttu-id="9d0f9-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) hızlı ve doğru boosted ağaç uygulaması sağlayan bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="9d0f9-215">XGBoost, python veya bir komut satırından da çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="9d0f9-216">Python</span><span class="sxs-lookup"><span data-stu-id="9d0f9-216">Python</span></span>
<span data-ttu-id="9d0f9-217">Python kullanarak geliştirme için Anaconda Python dağıtımları 2.7 ve 3.5 DSVM yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0f9-218">Anaconda dağıtım içeren [Condas](http://conda.pydata.org/docs/index.html), farklı sürümlerini ve/veya bunları yüklü olan paketleri sahip Python için özel ortamlar oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="9d0f9-219">Şimdi spambase dataset bazıları okuyun ve Destek vektör scikit makinelerinizde ile e-postaları sınıflandırmak-öğrenin:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="9d0f9-220">Tahminleri yapmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="9d0f9-221">Biz R modeli önceden yayımlandığında yaptığımız gibi bir AzureML uç nokta yayımlama göstermek için daha basit bir model üç değişkenleri olalım.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="9d0f9-222">Model için AzureML yayımlamak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="9d0f9-223">Bu, yalnızca python 2.7 için kullanılabilir ve 3.5 henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="9d0f9-224">Çalıştırma **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="9d0f9-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="9d0f9-225">Jupyterhub</span></span>
<span data-ttu-id="9d0f9-226">DSVM Anaconda dağıtımlarında Jupyter not defteri ile Python, R veya Jale kodunu ve analiz paylaşmak için platformlar arası ortamda gelir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="9d0f9-227">Jupyter not defteri JupyterHub erişilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="9d0f9-228">Yerel Linux kullanıcı adı ve parola kullanarak oturum ***https://\<VM DNS adı veya IP adresi\>: 8000 /***.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="9d0f9-229">Tüm yapılandırma dosyalarını JupyterHub için dizinde bulunan **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="9d0f9-230">Birkaç örnek not defterlerini VM üzerinde zaten yüklenir:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="9d0f9-231">Bkz: [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) bir örnek Python not defteri için.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="9d0f9-232">Bkz: [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) bir örnek için **R** dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="9d0f9-233">Bkz: [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) başka bir örnek için **Python** dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0f9-234">Jale dil, Linux veri bilimi VM üzerinde komut satırından da mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="9d0f9-235">Çıngırağı</span><span class="sxs-lookup"><span data-stu-id="9d0f9-235">Rattle</span></span>
<span data-ttu-id="9d0f9-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R analitik aracı için bilgi kolayca) grafiksel bir R veri araştırma için aracıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="9d0f9-237">Yük, keşfetme, veri dönüştürme ve yapı ve modelleri değerlendirmek daha kolay hale getirir sezgisel bir arabirim vardır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="9d0f9-238">Makaleyi [Rattle: bir veri madenciliği GUI r](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) özelliklerini gösteren bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="9d0f9-239">Yükleyin ve aşağıdaki komutlarla Çıngırağı başlatın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="9d0f9-240">Yükleme DSVM üzerinde gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="9d0f9-241">Ancak, yüklediğinde, ek paketleri yüklemek için Çıngırağı isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="9d0f9-242">Çıngırağı sekmesini tabanlı bir arabirim kullanır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="9d0f9-243">Sekmeleri çoğunu karşılık adımlarda [veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)veri yükleme veya araştırma gibi.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="9d0f9-244">Veri bilimi işlemi soldan sağa sekmeler arasında akar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="9d0f9-245">Ancak son sekmesi tarafından Çıngırağı çalıştırmak R komutların günlüğünü de içerir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="9d0f9-246">Yük ve veri kümesi yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="9d0f9-247">Dosyayı yüklemek için seçin **veri** sekmesinde, ardından</span><span class="sxs-lookup"><span data-stu-id="9d0f9-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="9d0f9-248">Seçici seçin **Filename** ve **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="9d0f9-249">Dosya yüklenemedi.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-249">To load the file.</span></span> <span data-ttu-id="9d0f9-250">seçin **yürütme** düğmelerinin üst satırda.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="9d0f9-251">Bir giriş, bir hedef veya başka bir değişken türü ve benzersiz değerlerin sayısını olup olmadığını, belirtilen veri türü de dahil olmak üzere her bir sütunun özetini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="9d0f9-252">Çıngırağı doğru tanımlanan **istenmeyen posta** sütunu hedef olarak.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="9d0f9-253">İstenmeyen posta sütunu seçin, ardından ayarlamak **hedef veri türü** için **Categoric**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="9d0f9-254">Verileri araştırmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-254">To explore the data:</span></span>

* <span data-ttu-id="9d0f9-255">Seçin **Araştır** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="9d0f9-256">Tıklatın **Özet**, ardından **yürütme**, değişken türleri hakkında bazı bilgiler ve bazı Özet istatistikleri görmek için.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="9d0f9-257">Her bir değişken hakkındaki istatistiklerdir diğer türlerini görüntülemek için diğer seçenekleri gibi seçin **açıklayın** veya **Temelleri**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="9d0f9-258">**Araştır** sekmesi ayrıca birçok ayrıntılı çizimleri oluşturmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="9d0f9-259">Verilerin bir histogram çizmek için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="9d0f9-260">Seçin **dağıtımları**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-260">Select **Distributions**.</span></span>
* <span data-ttu-id="9d0f9-261">Denetleme **Histogram** için **word_freq_remove** ve **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="9d0f9-262">Seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-262">Select **Execute**.</span></span> <span data-ttu-id="9d0f9-263">Word "," çok daha sık Kaldır"den" postalarda göründüğünü Temizle olduğu bir tek grafik penceresinde, her iki yoğunluğu çizimleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="9d0f9-264">Bağıntı çizimler, ayrıca ilginç.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="9d0f9-265">Oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-265">To create one:</span></span>

* <span data-ttu-id="9d0f9-266">Seçin **bağıntı** olarak **türü**, ardından</span><span class="sxs-lookup"><span data-stu-id="9d0f9-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="9d0f9-267">Seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-267">Select **Execute**.</span></span>
* <span data-ttu-id="9d0f9-268">Çıngırağı, en çok 40 değişkenleri önerir sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="9d0f9-269">Seçin **Evet** çizim görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="9d0f9-270">Gündeme bazı ilginç bağıntıları vardır: "teknolojisinin" kesinlikle bağıntılı "HP" ve "labs" Örneğin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="9d0f9-271">Veri kümesi bağışta alan kodu 650 olduğundan "650" de kesinlikle ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="9d0f9-272">Sözcükler arasındaki bağıntıları sayısal değerleri Araştır penceresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="9d0f9-273">Örneğin, "teknolojisinin" olumsuz "sizin" bağıntılı olduğunu unutmayın ve "para" ilginç olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="9d0f9-274">Çıngırağı bazı yaygın sorunlar işlemek için veri kümesi dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="9d0f9-275">Örneğin, bu özellikleri yeniden Ölçeklendir, eksik değerleri impute, aykırı değerlerini işlemek ve değişkenlerin ya da eksik verilerle gözlemleri kaldırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="9d0f9-276">Çıngırağı gözlemleri ve/veya değişkenleri arasındaki ilişkilendirme kuralları da tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="9d0f9-277">Bu sekme, bu tanıtıcı kılavuz için kapsam dışına:.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="9d0f9-278">Çıngırağı küme analiz de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="9d0f9-279">Şimdi çıktının okunmasını kolaylaştırmak için bazı özellikler çıkar.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="9d0f9-280">Üzerinde **veri** sekmesinde, seçin **Yoksay** her bir değişken on bu öğeler dışında yanındaki:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="9d0f9-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="9d0f9-281">word_freq_hp</span></span>
* <span data-ttu-id="9d0f9-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="9d0f9-282">word_freq_technology</span></span>
* <span data-ttu-id="9d0f9-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="9d0f9-283">word_freq_george</span></span>
* <span data-ttu-id="9d0f9-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="9d0f9-284">word_freq_remove</span></span>
* <span data-ttu-id="9d0f9-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="9d0f9-285">word_freq_your</span></span>
* <span data-ttu-id="9d0f9-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="9d0f9-286">word_freq_dollar</span></span>
* <span data-ttu-id="9d0f9-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="9d0f9-287">word_freq_money</span></span>
* <span data-ttu-id="9d0f9-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="9d0f9-288">capital_run_length_longest</span></span>
* <span data-ttu-id="9d0f9-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="9d0f9-289">word_freq_business</span></span>
* <span data-ttu-id="9d0f9-290">istenmeyen posta</span><span class="sxs-lookup"><span data-stu-id="9d0f9-290">spam</span></span>

<span data-ttu-id="9d0f9-291">Daha sonra geri dönerek **küme** sekmesinde, seçin **KMeans**ve *küme sayısı* 4.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="9d0f9-292">Ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-292">Then **Execute**.</span></span> <span data-ttu-id="9d0f9-293">Sonuçlar çıktı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-293">The results are displayed in the output window.</span></span> <span data-ttu-id="9d0f9-294">Bir küme yüksek sıklığı "Hasan" ve "hp" vardır ve büyük olasılıkla yasal iş e-posta olur.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="9d0f9-295">Basit karar ağacı makine öğrenimi modeli oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="9d0f9-296">Seçin **modeli** sekmesi</span><span class="sxs-lookup"><span data-stu-id="9d0f9-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="9d0f9-297">Seçin **ağaç** olarak **türü**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="9d0f9-298">Seçin **yürütme** ağaç çıktı penceresinde metin biçiminde görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="9d0f9-299">Seçin **çizin** grafik sürümünü görüntülemek için düğmeye.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="9d0f9-300">Bunu elde daha önce kullanarak ağacına oldukça benzer *rpart*.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="9d0f9-301">İyi özelliklerinden Çıngırağı biri birkaç makine öğrenme yöntemlerini çalıştırma ve bunları hızlı bir şekilde değerlendirmek yeteneğidir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="9d0f9-302">Yordam aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-302">Here is the procedure:</span></span>

* <span data-ttu-id="9d0f9-303">Seçin **tüm** için **türü**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="9d0f9-304">Seçin **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-304">Select **Execute**.</span></span>
* <span data-ttu-id="9d0f9-305">Sona erdikten sonra tüm tek tıklatabilirsiniz **türü**gibi **SVM**ve sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="9d0f9-306">Kullanılarak ayarlanan doğrulama modellerinde performansını de karşılaştırabilirsiniz **değerlendir** sekmesi. Örneğin, **hata matris** seçimi gösterir, karışıklığı matrisi, genel hata ve ortalama sınıfı hata her model için doğrulama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="9d0f9-307">Ayrıca ROC eğriler çizme, duyarlılık çözümlemesi ve diğer türleri modeli değerlendirmeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="9d0f9-308">Model oluşturmaya yaptıktan sonra seçeneğini **günlük** Çıngırağı tarafından oturumunuz sırasında çalışma R kodu görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="9d0f9-309">Seçebileceğiniz **verme** kaydetmeyi düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0f9-310">Çıngırağı geçerli sürümde bir hata var.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="9d0f9-311">Komut dosyasını değiştirin veya daha sonra buluncaya için kullanmak için bir # karakteri önüne yerleştirin *... Bu günlüğünü Dışarı Aktar * günlük metin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="9d0f9-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="9d0f9-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="9d0f9-313">DSVM yüklü PostgreSQL ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="9d0f9-314">PostgreSQL Gelişmiş, açık kaynak ilişkisel veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="9d0f9-315">Bu bölümde, istenmeyen posta kümemize PostgreSQL yüklemek ve ardından sorgu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="9d0f9-316">Verileri yüklemeden önce localhost parola kimlik doğrulamasını izin vermeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="9d0f9-317">Bir komut isteminde:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="9d0f9-318">Yapılandırma dosyası altına izin verilen bağlantılar ayrıntı birden çok satıra şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="9d0f9-319">Biz bir kullanıcı adı ve parola kullanarak oturum için md5 plainname yerine kullanmak için "IPv4 yerel bağlantılar" satırı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="9d0f9-320">Ve postgres hizmetini yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="9d0f9-321">Etkileşimli terminal yerleşik postgres kullanıcı olarak, PostgreSQL için psql başlatmak için bir isteminden aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="9d0f9-322">Şu anda olarak oturum açtınız ve parola verin Linux hesabıyla aynı kullanıcı adı kullanarak yeni bir kullanıcı hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="9d0f9-323">Psql için kullanıcı olarak sonra oturum açın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="9d0f9-324">Ve yeni bir veritabanına veri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="9d0f9-325">Şimdi, şimdi verileri araştırırken kullanarak bazı sorgular çalıştırmak **Squirrel SQL**, JDBC sürücüsü aracılığıyla veritabanlarıyla etkileşim olanak sağlayan bir grafik aracıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="9d0f9-326">Başlamak için uygulamaları menüsünden Squirrel SQL başlatın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="9d0f9-327">Sürücüsünü kurmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-327">To set up the driver:</span></span>

* <span data-ttu-id="9d0f9-328">Seçin **Windows**, ardından **görüntülemek sürücüleri**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="9d0f9-329">Sağ **PostgreSQL** seçip **değiştirmek sürücü**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="9d0f9-330">Seçin **yolu'fazladan sınıf**, ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="9d0f9-331">Girin ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** için **dosya adı** ve</span><span class="sxs-lookup"><span data-stu-id="9d0f9-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="9d0f9-332">Seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-332">Select **Open**.</span></span>
* <span data-ttu-id="9d0f9-333">Liste sürücüleri seçin ve ardından **org.postgresql.Driver** içinde **sınıf adı**seçip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="9d0f9-334">Yerel sunucu bağlantısını ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="9d0f9-335">Seçin **Windows**, ardından **diğer adlar görüntüleyin.**</span><span class="sxs-lookup"><span data-stu-id="9d0f9-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="9d0f9-336">Seçin  **+**  düğmesi yeni bir diğer ad yapın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="9d0f9-337">Bu ad *istenmeyen posta veritabanı*, seçin **PostgreSQL** içinde **sürücü** açılır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="9d0f9-338">URL'sini ayarlamak *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="9d0f9-339">Girin, *kullanıcıadı* ve *parola*.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="9d0f9-340">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-340">Click **OK**.</span></span>
* <span data-ttu-id="9d0f9-341">Açmak için **bağlantı** penceresinde çift ***istenmeyen posta veritabanı*** diğer adı.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="9d0f9-342">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-342">Select **Connect**.</span></span>

<span data-ttu-id="9d0f9-343">Bazı sorgular çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-343">To run some queries:</span></span>

* <span data-ttu-id="9d0f9-344">Seçin **SQL** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="9d0f9-345">Basit bir sorgu girin `SELECT * from data;` sorgu metin kutusuna SQL sekmenin üstünde.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="9d0f9-346">Tuşuna **Ctrl-Enter** çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="9d0f9-347">Varsayılan olarak Squirrel SQL sorgunuzdan ilk 100 satırı döndürür.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="9d0f9-348">Bu verileri araştırmak için çalıştırabilir pek çok daha fazla sorguları vardır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="9d0f9-349">Örneğin, word sıklığını nasıl mu *olun* istenmeyen ve ham arasında farklı?</span><span class="sxs-lookup"><span data-stu-id="9d0f9-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="9d0f9-350">Veya sık içeren e-posta özelliklerini nelerdir *3B*?</span><span class="sxs-lookup"><span data-stu-id="9d0f9-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="9d0f9-351">Yüksek bir oluşumunu sahip çoğu e-postaları *3B* olan görünüşe göre istenmeyen posta göndermek, e-postaları sınıflandırmak için Tahmine dayalı bir model oluşturmak için yararlı bir özellik olması.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="9d0f9-352">Bir PostgreSQL veritabanında depolanan verilerle machine learning gerçekleştirmek istiyorsanız, kullanmayı [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="9d0f9-353">SQL Server veri ambarı</span><span class="sxs-lookup"><span data-stu-id="9d0f9-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="9d0f9-354">Azure SQL Veri Ambarı, hem ilişkisel hem de ilişkisel olmayan çok geniş hacimlerdeki verileri işleyebilen, bulut tabanlı bir genişletme veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="9d0f9-355">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse nedir?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="9d0f9-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="9d0f9-356">Veri ambarına bağlanmak ve tablo oluşturmak için bir komut isteminden aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="9d0f9-357">Ardından sqlcmd isteminde:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="9d0f9-358">Bcp ile veri kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="9d0f9-359">İndirilen Dosya, satır sonları Windows stili olsa da - r bayrağıyla söyleyin bcp ihtiyacımız şekilde bcp UNIX stilinde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="9d0f9-360">Ve sorgu sqlcmd ile:</span><span class="sxs-lookup"><span data-stu-id="9d0f9-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="9d0f9-361">Ayrıca Squirrel SQL ile sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="9d0f9-362">İçinde bulunan Microsoft MSSQL Server JDBC sürücüsü kullanarak PostgreSQL için benzer adımları ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d0f9-363">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d0f9-363">Next steps</span></span>
<span data-ttu-id="9d0f9-364">Azure veri bilimi işlemi oluşturan görevler size yol konuları genel bakış için bkz: [takım veri bilimi işlemi](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="9d0f9-365">Belirli senaryolar için takım veri bilimi işlemdeki adımlar gösteren diğer uçtan uca talimatlara açıklaması için bkz: [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="9d0f9-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="9d0f9-366">İzlenecek yollar da Bulut ve şirket içi araçları ve Hizmetleri bir iş akışı veya akıllı bir uygulama oluşturmak için ardışık düzen birleştirmek nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9d0f9-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
