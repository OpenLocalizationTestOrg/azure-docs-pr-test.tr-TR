---
title: "Jenkins ile sürekli tümleştirme aaaUse Azure VM Aracısı."
description: "Jenkins alt sunucuları olarak Azure VM aracıları."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="10346-103">Jenkins ile sürekli tümleştirme için Azure VM aracılarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="10346-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="10346-104">Bu hızlı başlangıç nasıl toouse hello Jenkins Azure VM Aracısı eklentisi toocreate isteğe bağlı Linux (Ubuntu) aracıyı Azure gösterir.</span><span class="sxs-lookup"><span data-stu-id="10346-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10346-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="10346-105">Prerequisites</span></span>

<span data-ttu-id="10346-106">toocomplete Bu hızlı başlangıç:</span><span class="sxs-lookup"><span data-stu-id="10346-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="10346-107">Jenkins asıl zaten yoksa, hello ile başlayabilirsiniz [çözüm şablonu](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="10346-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="10346-108">Çok başvuran[Azure CLI 2.0 ile Azure hizmet sorumlusu oluşturma](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) bir Azure hizmet sorumlusu zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="10346-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="10346-109">Azure VM Aracıları eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="10346-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="10346-110">Hello başlatırsanız [çözüm şablonu](install-jenkins-solution-template.md), hello Azure VM Aracısı eklentisi hello Jenkins yöneticisinde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="10346-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="10346-111">Aksi takdirde, hello yükleyin **Azure VM Aracısı** gelen eklentisi hello Jenkins Pano içinde.</span><span class="sxs-lookup"><span data-stu-id="10346-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="10346-112">Merhaba eklentisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="10346-112">Configure hello plugin</span></span>

* <span data-ttu-id="10346-113">Merhaba Jenkins Pano içinde tıklatın **Jenkins Yönet -> Sistem Yapılandırma ->**.</span><span class="sxs-lookup"><span data-stu-id="10346-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="10346-114">Merhaba sayfanın toohello'e gidin ve hello açılır hello bölümle Bul **yeni bulut eklemek**.</span><span class="sxs-lookup"><span data-stu-id="10346-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="10346-115">Başlangıç menüsünden seçin **Microsoft Azure VM Aracısı**</span><span class="sxs-lookup"><span data-stu-id="10346-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="10346-116">Var olan bir hesap hello Azure kimlik bilgilerini aşağı açılır listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="10346-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="10346-117">Yeni bir tooadd **Microsoft Azure hizmet sorumlusu** hello aşağıdaki değerleri girin: abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası.</span><span class="sxs-lookup"><span data-stu-id="10346-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure Kimlik Bilgileri](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="10346-119">Tıklatın **doğrulama yapılandırma** toomake bu hello profil yapılandırmasının doğru olduğundan emin.</span><span class="sxs-lookup"><span data-stu-id="10346-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="10346-120">Merhaba yapılandırmasını kaydetmek ve toohello sonraki adıma devam edin.</span><span class="sxs-lookup"><span data-stu-id="10346-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="10346-121">Şablon yapılandırması</span><span class="sxs-lookup"><span data-stu-id="10346-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="10346-122">Genel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="10346-122">General configuration</span></span>
<span data-ttu-id="10346-123">Ardından, kullanım toodefine bir Azure VM aracısı için bir şablon yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="10346-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="10346-124">Tıklatın **Ekle** tooadd bir şablon.</span><span class="sxs-lookup"><span data-stu-id="10346-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="10346-125">Şablonunuza bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="10346-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="10346-126">"Ubuntu." Merhaba etiketini girin</span><span class="sxs-lookup"><span data-stu-id="10346-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="10346-127">Bu etiket hello iş yapılandırması sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10346-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="10346-128">Merhaba açılan kutudan Hello istediğiniz bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="10346-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="10346-129">Select hello VM boyutu istenen.</span><span class="sxs-lookup"><span data-stu-id="10346-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="10346-130">Hello Azure depolama hesabı adı belirtin veya boş toouse hello varsayılan adı "jenkinsarmst." bırakın</span><span class="sxs-lookup"><span data-stu-id="10346-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="10346-131">Merhaba bekletme süresini dakika cinsinden belirtin.</span><span class="sxs-lookup"><span data-stu-id="10346-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="10346-132">Bu ayar, hello Jenkins boşta aracıyı otomatik olarak silmeden önce bekleyebilirsiniz dakika sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="10346-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="10346-133">Otomatik olarak silinmesini boşta aracıları toobe istemiyorsanız 0 belirtin.</span><span class="sxs-lookup"><span data-stu-id="10346-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Genel yapılandırma](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="10346-135">Görüntü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="10346-135">Image configuration</span></span>

<span data-ttu-id="10346-136">toocreate Linux (Ubuntu) aracısı seçin **görüntü başvurusu** ve kullanım hello aşağıdaki örnek olarak yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="10346-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="10346-137">Çok başvuran[Azure Marketi](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello için görüntüleri en son Azure desteklenir.</span><span class="sxs-lookup"><span data-stu-id="10346-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="10346-138">Görüntü Yayımcısı: Canonical</span><span class="sxs-lookup"><span data-stu-id="10346-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="10346-139">Görüntü Teklifi: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="10346-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="10346-140">Görüntü Sku’su: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="10346-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="10346-141">Görüntü sürümü: en son</span><span class="sxs-lookup"><span data-stu-id="10346-141">Image version: latest</span></span>
* <span data-ttu-id="10346-142">İşletim Sistemi Türü: Linux</span><span class="sxs-lookup"><span data-stu-id="10346-142">OS Type: Linux</span></span>
* <span data-ttu-id="10346-143">Başlatma yöntemi: SSH</span><span class="sxs-lookup"><span data-stu-id="10346-143">Launch method: SSH</span></span>
* <span data-ttu-id="10346-144">Yönetici kimlik bilgilerini sağlama</span><span class="sxs-lookup"><span data-stu-id="10346-144">Provide an admin credentials</span></span>
* <span data-ttu-id="10346-145">VM başlatma betiği için şunu girin:</span><span class="sxs-lookup"><span data-stu-id="10346-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Görüntü yapılandırma](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="10346-147">Tıklatın **doğrulayın şablonu** tooverify hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="10346-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="10346-148">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10346-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="10346-149">Jenkins içinde iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="10346-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="10346-150">Merhaba Jenkins Pano içinde tıklatın **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="10346-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="10346-151">Bir ad girip **Serbest tarzda proje**’yi seçin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10346-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="10346-152">Merhaba, **genel** sekmesi, seçin "proje çalıştırdığı kısıtlamak" ve tür etiket ifadesi "ubuntu".</span><span class="sxs-lookup"><span data-stu-id="10346-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="10346-153">Şimdi hello açılır "ubuntu" konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="10346-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="10346-154">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10346-154">Click **Save**.</span></span>

![İşi ayarlama](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="10346-156">Yeni projenizi derleme</span><span class="sxs-lookup"><span data-stu-id="10346-156">Build your new project</span></span>

* <span data-ttu-id="10346-157">Toohello Jenkins panoya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="10346-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="10346-158">Oluşturduğunuz yeni hello işi, sağ tıklatın, ardından **şimdi yapı**.</span><span class="sxs-lookup"><span data-stu-id="10346-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="10346-159">Derleme başlatılır.</span><span class="sxs-lookup"><span data-stu-id="10346-159">A build is kicked off.</span></span> 
* <span data-ttu-id="10346-160">Merhaba yapı tamamlandıktan sonra çok Git**konsol çıkış**.</span><span class="sxs-lookup"><span data-stu-id="10346-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="10346-161">Merhaba yapı Azure üzerinde uzaktan gerçekleştirildiğini bakın.</span><span class="sxs-lookup"><span data-stu-id="10346-161">You see that hello build was performed remotely on Azure.</span></span>

![Konsol çıktısı](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="10346-163">Başvuru</span><span class="sxs-lookup"><span data-stu-id="10346-163">Reference</span></span>

* <span data-ttu-id="10346-164">Azure Cuma videosu: [Azure VM aracılarını kullanarak Jenkins ile Sürekli Tümleştirme](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="10346-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="10346-165">Destek bilgileri ve yapılandırma seçenekleri: [Azure VM Aracısı Jenkins Eklentisi Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="10346-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

