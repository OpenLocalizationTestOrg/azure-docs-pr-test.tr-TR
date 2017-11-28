---
title: "Sorunlarını giderme: Oluşturma ve Machine Learning çalışma alanına bağlayın | Microsoft Docs"
description: "Oluşturma ve bir Azure Machine Learning çalışma alanına bağlanma ortak sorunlar için çözümleri"
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
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="17007-103">Sorun giderme kılavuzu: Machine Learning çalışma alanı oluşturun ve bağlanın</span><span class="sxs-lookup"><span data-stu-id="17007-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="17007-104">Bu kılavuz, Azure Machine Learning çalışma alanlarınızı ayarlarken çözümleri için bazı sık zorluklar karşılaşılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="17007-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="17007-105">Çalışma alanı sahibi</span><span class="sxs-lookup"><span data-stu-id="17007-105">Workspace owner</span></span>
<span data-ttu-id="17007-106">Bir çalışma alanı Machine Learning Studio'da açmak için çalışma alanı oluşturmak için kullanılan Microsoft Account oturum açmanız gerekir veya çalışma alanına katılmaya sahibinden davet almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="17007-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="17007-107">Azure portalından erişim yapılandırma yeteneğini içerir çalışma yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17007-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="17007-108">Bir çalışma alanı yönetme ile ilgili daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme].</span><span class="sxs-lookup"><span data-stu-id="17007-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="17007-109">[bir Azure Machine Learning çalışma alanını yönetme]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="17007-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="17007-110">İzin verilen bölgeleri</span><span class="sxs-lookup"><span data-stu-id="17007-110">Allowed regions</span></span>
<span data-ttu-id="17007-111">Machine Learning bölgeler sınırlı bir süre içinde şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="17007-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="17007-112">Aboneliğiniz bu bölgelerinden içermiyorsa, hata iletisi görebilirsiniz, "İzin verilen bölgelerde hiç aboneliğiniz yok."</span><span class="sxs-lookup"><span data-stu-id="17007-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="17007-113">Bir bölge aboneliğinize eklenmesi isteği için Azure portalından yeni bir Microsoft destek isteği oluşturun, **faturalama** sorun türü olarak ve isteğinizi göndermek için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="17007-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="17007-114">Depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="17007-114">Storage account</span></span>
<span data-ttu-id="17007-115">Machine Learning hizmetinin verileri depolamak için bir depolama hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="17007-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="17007-116">Mevcut bir depolama hesabını kullanabilir veya (yeni bir depolama hesabı oluşturmak için kota varsa) yeni Machine Learning çalışma alanı oluşturduğunuzda, yeni bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17007-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="17007-117">Yeni Machine Learning çalışma alanı oluşturulduktan sonra Machine Learning Studio çalışma alanı oluşturmak için kullanılan Microsoft hesabı kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17007-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="17007-118">Hata iletisi "Çalışma alanı bulunamadı" (aşağıdaki ekran görüntüsüne benzer) karşılaşırsanız, tarayıcı tanımlama bilgilerini silmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="17007-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Çalışma alanı bulunamadı][screen3]

<span data-ttu-id="17007-120">**Tarayıcı tanımlama bilgilerini silmek için**</span><span class="sxs-lookup"><span data-stu-id="17007-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="17007-121">Internet Explorer kullanıyorsanız, tıklatın **Araçları** sağ üst köşesinde düğmesine tıklayın ve ardından **Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="17007-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Internet Seçenekleri][screen4]

2. <span data-ttu-id="17007-123">Altında **genel** sekmesini tıklatın, **silin...**</span><span class="sxs-lookup"><span data-stu-id="17007-123">Under the **General** tab, click **Delete…**</span></span>

![Genel sekmesi][screen5]

3. <span data-ttu-id="17007-125">İçinde **Gözatma Geçmişini Sil** iletişim kutusunda, emin olun **tanımlama bilgileri ve Web sitesi verileri** seçilir ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="17007-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Tanımlama bilgilerini silin][screen6]

<span data-ttu-id="17007-127">Tanımlama bilgilerini silindikten sonra tarayıcıyı yeniden ve gidin [Microsoft Azure Machine Learning](https://studio.azureml.net) sayfası.</span><span class="sxs-lookup"><span data-stu-id="17007-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="17007-128">Bir kullanıcı adı ve parola istendiğinde, çalışma alanı oluşturmak için kullanılan aynı Microsoft hesabını girin.</span><span class="sxs-lookup"><span data-stu-id="17007-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="17007-129">Yorumlar</span><span class="sxs-lookup"><span data-stu-id="17007-129">Comments</span></span>

<span data-ttu-id="17007-130">Amacımız, Machine Learning deneyiminizi mümkün olduğunca sorunsuz olmasını sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="17007-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="17007-131">Lütfen tüm yorumlar ve sorunu sonrası [Azure Machine Learning Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) daha iyi hizmet yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="17007-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
