---
title: "Büyük dağıtımlar dağıtma"
description: "Eclipse için Azure Araç Seti kullanarak büyük dağıtımlar dağıtmayı öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="dfa5e-103">Büyük dağıtımlar dağıtma</span><span class="sxs-lookup"><span data-stu-id="dfa5e-103">Deploying Large Deployments</span></span>
<span data-ttu-id="dfa5e-104">Dağıtımınız varsayılan approot klasöründe bulunması için çok büyük ise, JDK için yerel depolama kaynağı dağıtım kök klasör olarak kullanabilirsiniz ve uygulama sunucusu.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="dfa5e-105">Yerel depolama kaynağı büyük dağıtımlar için dağıtım kök klasör olarak kullanmak için</span><span class="sxs-lookup"><span data-stu-id="dfa5e-105">To use a local storage resource as the deployment root folder for large deployments</span></span>
1. <span data-ttu-id="dfa5e-106">Yeni bir yerel depolama kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-106">Create a new local storage resource.</span></span> <span data-ttu-id="dfa5e-107">Kaynağın adını belirttiğinizin önemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-107">The name of the resource does not matter.</span></span> <span data-ttu-id="dfa5e-108">Depolama kaynaklarını rol düzeyinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="dfa5e-109">İçinden oluşturduğunuz yeni bir yerel depolama kaynağı yerel depolama yapılandırma iletişim erişmek için en hızlı aşağıdaki adımları kullanarak yoludur: rolünde sağ **Proje Gezgini** Görünüm (Azure projenizi genişletin düğüm) rolü görmüyorsanız, tıklatın **Azure**ve ardından **yerel depolama**.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="dfa5e-110">İçinde **yerel depolama** iletişim kutusunda, tıklatın **Ekle** yeni bir yerel depolama kaynağı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

2. <span data-ttu-id="dfa5e-111">İstenen boyuta (karşılaşabileceğinizi herhangi bir şey daha az aynı dosyanın boyutu sorunları approot neden olabilir) en az 2048 MB ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

3. <span data-ttu-id="dfa5e-112">Emin **rol örneği geri dönüştürüldüğünde içeriği temiz** denetlenir; bu dağıtımın başlangıç mantığı rol örneği olduğunda çakışmaları kaynak önceden var olan dosyalarla engellenmesine yardımcı olur geri dönüştürüldü.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

4. <span data-ttu-id="dfa5e-113">Emin **kaynağın dizin yolu dağıtımdan sonra Depolama ortam değişkeni** değeri dizeye ayarlayın **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="dfa5e-114">Yerel depolama kaynak iletişim aşağıdakine benzer görünecektir.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="dfa5e-115">Alternatif olarak, kullanırsanız **DEPLOYROOT** olarak *adı* yerel kaynağınız ve, otomatik olarak oluşturulan ortam değişkeni adı değiştirmeyin (hangi şekilde ayarlanacak **DEPLOYROOT_ YOL** bu durumda), uygulamanız için çalışması.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="dfa5e-116">Yerel depolama kaynağı oluşturma hakkında daha fazla bilgi bulunabilir [yerel depolama özellikleri][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="dfa5e-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="dfa5e-117">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="dfa5e-117">See Also</span></span>
<span data-ttu-id="dfa5e-118">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dfa5e-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="dfa5e-119">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dfa5e-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="dfa5e-120">[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dfa5e-120">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="dfa5e-121">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="dfa5e-121">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
