---
title: "aaaDeploying büyük dağıtımlar"
description: "Eclipse için Azure Araç Seti kullanarak toodeploy büyük dağıtımları nasıl hello öğrenin."
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
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="f0102-103">Büyük dağıtımlar dağıtma</span><span class="sxs-lookup"><span data-stu-id="f0102-103">Deploying Large Deployments</span></span>
<span data-ttu-id="f0102-104">Dağıtımınızı hello varsayılan approot klasöründe yer alan çok büyük toobe ise, JDK için yerel depolama kaynağı hello dağıtım kök klasör olarak kullanabilirsiniz ve uygulama sunucusu.</span><span class="sxs-lookup"><span data-stu-id="f0102-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="f0102-105">toouse büyük dağıtımlar için hello dağıtım kök klasör olarak yerel depolama kaynağı</span><span class="sxs-lookup"><span data-stu-id="f0102-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="f0102-106">Yeni bir yerel depolama kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f0102-106">Create a new local storage resource.</span></span> <span data-ttu-id="f0102-107">Merhaba hello kaynağın adını belirttiğinizin önemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="f0102-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="f0102-108">Depolama kaynaklarını hello rol düzeyinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f0102-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="f0102-109">Merhaba içinden oluşturduğunuz yeni bir yerel depolama kaynağı hızlı şekilde tooaccess hello yerel depolama yapılandırması iletişim kutusunda, aşağıdaki adımları hello kullanmaktır: hello sağ hello rolünde **Proje Gezgini** Görünüm (genişletin, Azure projesi düğümü) hello rolü görmüyorsanız, tıklatın **Azure**ve ardından **yerel depolama**.</span><span class="sxs-lookup"><span data-stu-id="f0102-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="f0102-110">Merhaba içinde **yerel depolama** iletişim kutusunda, tıklatın **Ekle** toocreate yeni bir yerel depolama kaynağı.</span><span class="sxs-lookup"><span data-stu-id="f0102-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="f0102-111">Set hello istenen boyutu tooat (hiçbir şey daha az hello aynı dosya boyutu sorunlara neden karşılaşabileceğinizi hello approot) en az 2048 MB.</span><span class="sxs-lookup"><span data-stu-id="f0102-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="f0102-112">Emin **hello rol örneği geri dönüştürüldüğünde hello içeriği temiz** denetlenir; bu hello dağıtımın başlangıç mantığı çakışmaları hello kaynak önceden var olan dosyaları ile engellenmesine yardımcı olur rolü'ne zaman hello geri dönüştürüldüğünde örneğidir.</span><span class="sxs-lookup"><span data-stu-id="f0102-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="f0102-113">Bu hello olun **dağıtımdan sonra hello kaynağın dizin yolu ortam değişkeni depolamak** değeri toohello dize ayarlanır **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="f0102-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="f0102-114">Yerel depolama kaynak iletişim benzer toohello aşağıdaki arar.</span><span class="sxs-lookup"><span data-stu-id="f0102-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="f0102-115">Alternatif olarak, kullanırsanız **DEPLOYROOT** hello olarak *adı* yerel kaynağınız ve, hello otomatik olarak oluşturulan ortam değişkeni adı değiştirmeyin (hangi ayarlanacak çok **DEPLOYROOT_PATH** bu durumda), uygulamanız için çalışması.</span><span class="sxs-lookup"><span data-stu-id="f0102-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="f0102-116">Yerel depolama kaynağı oluşturma hakkında daha fazla bilgi bulunabilir [yerel depolama özellikleri][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="f0102-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="f0102-117">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f0102-117">See Also</span></span>
<span data-ttu-id="f0102-118">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0102-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="f0102-119">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0102-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="f0102-120">[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0102-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="f0102-121">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f0102-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
