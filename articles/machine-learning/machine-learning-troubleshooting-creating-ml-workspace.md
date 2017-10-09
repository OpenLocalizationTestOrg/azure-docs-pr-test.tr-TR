---
title: "Sorunlarını giderme: Oluşturun ve tooa Machine Learning çalışma alanı bağlantı | Microsoft Docs"
description: "Oluşturma ve tooan Azure Machine Learning çalışma alanına bağlanma ortak sorunlar için çözümleri"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="070ac-103">Sorun giderme kılavuzu: oluşturmak ve tooan Machine Learning çalışma alanına bağlayın</span><span class="sxs-lookup"><span data-stu-id="070ac-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="070ac-104">Bu kılavuz, Azure Machine Learning çalışma alanlarınızı ayarlarken çözümleri için bazı sık zorluklar karşılaşılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="070ac-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="070ac-105">Çalışma alanı sahibi</span><span class="sxs-lookup"><span data-stu-id="070ac-105">Workspace owner</span></span>
<span data-ttu-id="070ac-106">Machine Learning Studio'da bir çalışma alanı tooopen olmalıdır toohello Microsoft Account imzalı toocreate hello çalışma kullanılan veya tooreceive hello sahibi toojoin hello çalışma alanından bir davet gerekir.</span><span class="sxs-lookup"><span data-stu-id="070ac-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="070ac-107">Azure portal Hello hello özelliği tooconfigure erişim içerir hello çalışma yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ac-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="070ac-108">Bir çalışma alanı yönetme ile ilgili daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme].</span><span class="sxs-lookup"><span data-stu-id="070ac-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[bir Azure Machine Learning çalışma alanını yönetme]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="070ac-110">İzin verilen bölgeleri</span><span class="sxs-lookup"><span data-stu-id="070ac-110">Allowed regions</span></span>
<span data-ttu-id="070ac-111">Machine Learning bölgeler sınırlı bir süre içinde şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="070ac-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="070ac-112">Aboneliğiniz bu bölgelerinden içermiyorsa hello hata iletisi görebilirsiniz, "Hello bölgeler izin hiç aboneliğiniz yok."</span><span class="sxs-lookup"><span data-stu-id="070ac-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="070ac-113">bir bölge olması toorequest eklenen tooyour abonelik, Azure portal hello yeni bir Microsoft destek isteği oluşturmak, seçin **faturalama** hello sorun türü ve izleme hello isteğiniz toosubmit ister.</span><span class="sxs-lookup"><span data-stu-id="070ac-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="070ac-114">Depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="070ac-114">Storage account</span></span>
<span data-ttu-id="070ac-115">Merhaba Machine Learning hizmetindeki bir depolama hesabı toostore verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="070ac-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="070ac-116">Mevcut bir depolama hesabını kullanabilir veya (yeni bir depolama hesabı'de kota toocreate varsa) hello yeni Machine Learning çalışma alanı oluşturduğunuzda, yeni bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ac-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="070ac-117">Merhaba yeni Machine Learning çalışma alanı oluşturulduktan sonra toocreate hello çalışma kullanılan hello Microsoft hesabı kullanarak tooMachine Learning Studio imzalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070ac-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="070ac-118">Lütfen hello hata iletisi, "Çalışma alanı bulunamadı" (benzer toohello ekran aşağıdaki) karşılaşırsanız, aşağıdaki adımları toodelete hello tarayıcı tanımlama bilgilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="070ac-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Çalışma alanı bulunamadı][screen3]

<span data-ttu-id="070ac-120">**toodelete tarayıcı tanımlama**</span><span class="sxs-lookup"><span data-stu-id="070ac-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="070ac-121">Internet Explorer kullanıyorsanız, hello tıklatın **Araçları** hello sağ üst köşesinde düğmesine tıklayın ve ardından **Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="070ac-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Internet Seçenekleri][screen4]

2. <span data-ttu-id="070ac-123">Merhaba altında **genel** sekmesini tıklatın, **silin...**</span><span class="sxs-lookup"><span data-stu-id="070ac-123">Under hello **General** tab, click **Delete…**</span></span>

![Genel sekmesi][screen5]

3. <span data-ttu-id="070ac-125">Merhaba, **Gözatma Geçmişini Sil** iletişim kutusunda, emin olun **tanımlama bilgileri ve Web sitesi verileri** seçilir ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="070ac-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Tanımlama bilgilerini silin][screen6]

<span data-ttu-id="070ac-127">Hello tanımlama bilgilerini silindikten sonra hello tarayıcı yeniden başlatın ve sonra toohello gidin [Microsoft Azure Machine Learning](https://studio.azureml.net) sayfası.</span><span class="sxs-lookup"><span data-stu-id="070ac-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="070ac-128">Bir kullanıcı adı ve parolanızı girmeniz için sizden istendiğinde toocreate hello çalışma kullandığınız aynı Microsoft hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="070ac-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="070ac-129">Yorumlar</span><span class="sxs-lookup"><span data-stu-id="070ac-129">Comments</span></span>

<span data-ttu-id="070ac-130">Amacımız toomake hello Machine Learning deneyiminizi olarak sorunsuz ' dir.</span><span class="sxs-lookup"><span data-stu-id="070ac-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="070ac-131">Lütfen tüm yorumlar ve sorunları hello sonrası [Azure Machine Learning Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) bize hizmet, daha iyi toohelp.</span><span class="sxs-lookup"><span data-stu-id="070ac-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
