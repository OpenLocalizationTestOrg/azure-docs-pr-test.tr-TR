---
title: "DevTest Labs VM için özel yapılar aaaCreate | Microsoft Docs"
description: "Tooauthor kendi yapıtlar için DevTest Labs ile kullanma hakkında bilgi edinin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="a0d3e-103">DevTest Labs VM için özel yapılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0d3e-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="a0d3e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a0d3e-104">Overview</span></span>
<span data-ttu-id="a0d3e-105">**Yapıları** kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="a0d3e-106">Yapı tanımı dosyası ve bir git deposu klasöründe depolanan diğer komut dosyalarını bir yapı oluşur.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="a0d3e-107">Yapı tanımı dosyaları oluşur JSON ve istediğiniz toospecify kullanabileceğiniz ifadeler bir VM'de tooinstall.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="a0d3e-108">Örneğin, bir yapı, komut toorun ve hello komutu çalıştırdığınızda, kullanılabilir hale getirilir parametreleri hello adını tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="a0d3e-109">Ada göre tooother komut dosyaları hello yapı tanımı dosyasındaki başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="a0d3e-110">Yapı tanımı dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="a0d3e-110">Artifact definition file format</span></span>
<span data-ttu-id="a0d3e-111">Merhaba aşağıdaki örnek hello temel bir tanım dosyası yapınızı olun hello bölümleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="a0d3e-112">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="a0d3e-112">Element name</span></span> | <span data-ttu-id="a0d3e-113">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="a0d3e-113">Required?</span></span> | <span data-ttu-id="a0d3e-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a0d3e-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0d3e-115">$schema</span><span class="sxs-lookup"><span data-stu-id="a0d3e-115">$schema</span></span> |<span data-ttu-id="a0d3e-116">Hayır</span><span class="sxs-lookup"><span data-stu-id="a0d3e-116">No</span></span> |<span data-ttu-id="a0d3e-117">Merhaba tanım dosyası hello geçerliliğini sınamada yardımcı hello JSON Şeması dosyasının konumu.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="a0d3e-118">Başlık</span><span class="sxs-lookup"><span data-stu-id="a0d3e-118">title</span></span> |<span data-ttu-id="a0d3e-119">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-119">Yes</span></span> |<span data-ttu-id="a0d3e-120">Merhaba laboratuvarda görüntülenen hello yapı adı.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="a0d3e-121">açıklama</span><span class="sxs-lookup"><span data-stu-id="a0d3e-121">description</span></span> |<span data-ttu-id="a0d3e-122">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-122">Yes</span></span> |<span data-ttu-id="a0d3e-123">Merhaba laboratuvarda görüntülenen hello yapı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="a0d3e-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="a0d3e-124">iconUri</span></span> |<span data-ttu-id="a0d3e-125">Hayır</span><span class="sxs-lookup"><span data-stu-id="a0d3e-125">No</span></span> |<span data-ttu-id="a0d3e-126">Merhaba simgesi hello laboratuvarda görüntülenir URI'si.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="a0d3e-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="a0d3e-127">targetOsType</span></span> |<span data-ttu-id="a0d3e-128">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-128">Yes</span></span> |<span data-ttu-id="a0d3e-129">Merhaba VM yapıt yüklendiği işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="a0d3e-130">Desteklenen Seçenekler şunlardır: Windows ve Linux.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="a0d3e-131">parametreler</span><span class="sxs-lookup"><span data-stu-id="a0d3e-131">parameters</span></span> |<span data-ttu-id="a0d3e-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="a0d3e-132">No</span></span> |<span data-ttu-id="a0d3e-133">Bir makinede yapı yükleme komutunu çalıştırdığınızda, sağlanan değerler.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="a0d3e-134">Bu, yapı özelleştirme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="a0d3e-135">KomutÇalıştır</span><span class="sxs-lookup"><span data-stu-id="a0d3e-135">runCommand</span></span> |<span data-ttu-id="a0d3e-136">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-136">Yes</span></span> |<span data-ttu-id="a0d3e-137">Yapı bir VM üzerinde yürütülen komutu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="a0d3e-138">Yapı parametreleri</span><span class="sxs-lookup"><span data-stu-id="a0d3e-138">Artifact parameters</span></span>
<span data-ttu-id="a0d3e-139">Merhaba Parametreler bölümünde hello tanım dosyası, bir kullanıcı bir yapı yüklerken giriş hangi değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="a0d3e-140">Merhaba yapı yükleme komut toothese değerleri başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="a0d3e-141">Yapı izlenerek hello ile parametrelerini tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="a0d3e-142">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="a0d3e-142">Element name</span></span> | <span data-ttu-id="a0d3e-143">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="a0d3e-143">Required?</span></span> | <span data-ttu-id="a0d3e-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a0d3e-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0d3e-145">type</span><span class="sxs-lookup"><span data-stu-id="a0d3e-145">type</span></span> |<span data-ttu-id="a0d3e-146">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-146">Yes</span></span> |<span data-ttu-id="a0d3e-147">Parametre değeri türü.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-147">Type of parameter value.</span></span> <span data-ttu-id="a0d3e-148">Liste türleri izin hello için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="a0d3e-149">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="a0d3e-149">displayName</span></span> |<span data-ttu-id="a0d3e-150">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-150">Yes</span></span> |<span data-ttu-id="a0d3e-151">Görüntülenen tooa kullanıcı hello laboratuarda hello parametresinin adı.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="a0d3e-152">açıklama</span><span class="sxs-lookup"><span data-stu-id="a0d3e-152">description</span></span> |<span data-ttu-id="a0d3e-153">Evet</span><span class="sxs-lookup"><span data-stu-id="a0d3e-153">Yes</span></span> |<span data-ttu-id="a0d3e-154">Merhaba laboratuvarda görüntülenen hello parametre açıklaması.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="a0d3e-155">Merhaba izin verilen türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-155">hello allowed types are:</span></span>

* <span data-ttu-id="a0d3e-156">dize – geçerli bir JSON dize</span><span class="sxs-lookup"><span data-stu-id="a0d3e-156">string – any valid JSON string</span></span>
* <span data-ttu-id="a0d3e-157">int – geçerli bir JSON tamsayı</span><span class="sxs-lookup"><span data-stu-id="a0d3e-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="a0d3e-158">bool – geçerli bir JSON Boole</span><span class="sxs-lookup"><span data-stu-id="a0d3e-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="a0d3e-159">dizi – geçerli bir JSON dizisi</span><span class="sxs-lookup"><span data-stu-id="a0d3e-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="a0d3e-160">Yapı ifadeleri ve İşlevler</span><span class="sxs-lookup"><span data-stu-id="a0d3e-160">Artifact expressions and functions</span></span>
<span data-ttu-id="a0d3e-161">İşlevler tooconstruct hello yapı yükleme komutunu ve ifade kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="a0d3e-162">İfadeler ile parantez içine ([ve]) ve hello yapı yüklendiğinde değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="a0d3e-163">İfadeler bir JSON dizesi değerindeki herhangi bir yerde görünür ve her zaman başka bir JSON değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="a0d3e-164">Toouse köşeli ayraç ile başlayan bir sabit dize gerekip gerekmediğini [, iki ayraç kullanmalısınız [[.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="a0d3e-165">Genellikle, ifadeler işlevleri tooconstruct bir değer kullanın.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="a0d3e-166">JavaScript'te, gibi işlev çağrılarını functionName(arg1,arg2,arg3) biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="a0d3e-167">Merhaba aşağıdaki listede ortak işlevleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="a0d3e-168">parameters(parameterName) - hello yapı komutu çalıştırdığınızda, sağlanan bir parametre değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="a0d3e-169">concat (arg1, arg2, arg3,...) - birden çok dize değerlerini birleştirir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="a0d3e-170">Bu işlev bağımsız değişkenleri herhangi bir sayıda alabilir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="a0d3e-171">örnekte gösterildiği nasıl aşağıdaki hello toouse ifadesi ve işlevleri tooconstruct bir değer:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="a0d3e-172">Özel yapı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0d3e-172">Create a custom artifact</span></span>
<span data-ttu-id="a0d3e-173">Özel yapı, aşağıdaki adımları izleyerek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="a0d3e-174">Bir JSON Düzenleyicisi yükleme - yapı tanım dosyalarını bir JSON Düzenleyicisi toowork gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="a0d3e-175">Kullanmanızı öneririz [Visual Studio Code](https://code.visualstudio.com/), Windows, Linux ve OS X için kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="a0d3e-176">Azure DevTest Labs ekibi tarafından oluşturulan bir örnek artifactfile.json - hello yapıları kullanıma alma bizim [GitHub deposunu](https://github.com/Azure/azure-devtestlab), zengin denetim kitaplığı oluşturduk burada yardımcı yapıları kendi yapıları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="a0d3e-177">Yapı tanımı dosyasını indirin ve kendi yapıları değişiklikleri tooit toocreate olun.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="a0d3e-178">IntelliSense - kullanılan tooconstruct olabilir Dengeleme IntelliSense toosee geçerli öğeleri bir yapı tanımı dosyası yararlanır.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="a0d3e-179">Merhaba, bir öğenin değerleri için farklı seçenekler de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="a0d3e-180">Örneğin, size hello iki seçenek Windows veya Linux hello düzenlerken IntelliSense'i Göster **targetOsType** öğesi.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="a0d3e-181">Mağaza hello yapı içinde bir [git deposu](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a0d3e-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="a0d3e-182">Burada hello dizin adı olduğu hello aynı hello yapı adı olarak her bir yapı için ayrı bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="a0d3e-183">Merhaba yapı tanım dosyası (artifactfile.json), oluşturduğunuz hello dizinde depolayın.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="a0d3e-184">Hello yapıdan başvurulan deposu hello komut dosyaları yükleme komutu.</span><span class="sxs-lookup"><span data-stu-id="a0d3e-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="a0d3e-185">Yapı klasörü nasıl görünebileceği örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a0d3e-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Yapı git deposuna örnek](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="a0d3e-187">Merhaba yapıları depo toohello Laboratuvar add - toohello makalesine başvurun [yapıları ve şablonlar için Git deposu ekleme](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a0d3e-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="a0d3e-188">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="a0d3e-188">Related articles</span></span>
* [<span data-ttu-id="a0d3e-189">Nasıl DevTest Labs de toodiagnose yapı hataları</span><span class="sxs-lookup"><span data-stu-id="a0d3e-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="a0d3e-190">VM tooexisting AD Azure DevTest Labs'de resource manager şablonu kullanarak etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="a0d3e-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="a0d3e-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0d3e-191">Next steps</span></span>
* <span data-ttu-id="a0d3e-192">Nasıl çok öğrenin[Git yapıt deposu tooa Laboratuvar ekleme](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a0d3e-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

