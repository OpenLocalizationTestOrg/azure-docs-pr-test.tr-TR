---
title: aaaCreate Jupyter/IPython not defteri | Microsoft Docs
description: "Bir Linux sanal makinede toodeploy hello Jupyter/IPython dizüstü hello resource manager dağıtım modeline Azure ile nasıl oluşturulacağını öğrenin."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="6a395-103">Bir Azure Jupyter yükleme ve Jupyter not defteri Azure üzerinde çalışan VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a395-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="6a395-104">Merhaba [Jupyter proje](http://jupyter.org), eskiden hello [IPython proje](http://ipython.org), bir koleksiyon için araçlar sağlar kod yürütmeyi hello oluşturulmasını ile birleştirin güçlü etkileşimli Kabukları kullanarak bilimsel hesaplama Canlı bir hesaplama belge.</span><span class="sxs-lookup"><span data-stu-id="6a395-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="6a395-105">Bu not defteri dosyaları rastgele metin, matematiksel formüller, giriş kod, sonuçları, grafik, videolar ve modern bir web tarayıcısı görüntüleyebilen ortamının başka herhangi bir tür içerebilir.</span><span class="sxs-lookup"><span data-stu-id="6a395-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="6a395-106">Olup kesinlikle yeni tooPython olduğunuz ve toolearn istiyorsanız bunu eğlenceli, etkileşimli ortam veya bazı önemli paralel/bilgi işlem teknik hello Jupyter not defteri olduğu harika bir seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="6a395-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="6a395-107">![Ekran](./media/jupyter-notebook/ipy-notebook-spectral.png) ses kaydını kullanarak SciPy ve Matplotlib paketleri tooanalyze hello yapısı.</span><span class="sxs-lookup"><span data-stu-id="6a395-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="6a395-108">Jupyter iki yolu: Azure dizüstü bilgisayarlar veya özel dağıtım</span><span class="sxs-lookup"><span data-stu-id="6a395-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="6a395-109">Azure çok kullanabileceğiniz bir hizmet sunar[Jupyter kullanarak hızlı bir şekilde başlatmak ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a395-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="6a395-110">Hello Azure Not Defteri hizmeti kullanarak erişim tooJupyter'ın web üzerinden erişilebilen arabirimi kolayca kazanmadan Python tüm hello gücünü ve birçok kitaplıkları ile ölçeklenebilir hesaplama kaynaklarına.</span><span class="sxs-lookup"><span data-stu-id="6a395-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="6a395-111">Merhaba yükleme hello hizmeti tarafından işlenen olduğundan, kullanıcılar Yönetim ve yapılandırma hello kullanıcı tarafından hello gerek kalmadan bu kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="6a395-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="6a395-112">Lütfen Hello Not Defteri hizmeti senaryonuz için işe yaramazsa tooread size nasıl toodeploy hello Jupyter not defteri Microsoft Azure üzerinde Linux sanal makineleri (VM'ler) kullanarak gösterir bu makalenin devam edin.</span><span class="sxs-lookup"><span data-stu-id="6a395-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="6a395-113">Oluşturma ve Azure üzerinde bir VM yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6a395-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="6a395-114">Merhaba ilk adım bir Azure üzerinde çalıştıran sanal makine (VM) toocreate değil.</span><span class="sxs-lookup"><span data-stu-id="6a395-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="6a395-115">Bu VM hello bulutta eksiksiz bir işletim sistemi ve hello Jupyter not defteri çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6a395-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="6a395-116">Azure Linux ve Windows sanal makineleri çalıştırabilen ve her iki tür sanal makineler üzerinde Jupyter hello Kurulumu ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="6a395-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="6a395-117">Bir Linux VM oluşturun ve Jupyter için bir bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="6a395-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="6a395-118">Verilen hello yönergeleri [burada] [ portal-vm-linux] toocreate hello bir sanal makineye *Ubuntu* dağıtım.</span><span class="sxs-lookup"><span data-stu-id="6a395-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="6a395-119">Bu öğretici, Ubuntu Server 14.04 LTS kullanır.</span><span class="sxs-lookup"><span data-stu-id="6a395-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="6a395-120">Merhaba kullanıcı adı varsayıyoruz *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="6a395-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="6a395-121">Merhaba sanal makine dağıtıldıktan sonra tooopen hello ağ güvenlik grubundaki güvenlik kuralı ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="6a395-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="6a395-122">Azure portal Hello çok Git**ağ güvenlik grupları** ve hello güvenlik grubuna karşılık gelen tooyour VM için açık hello sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6a395-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="6a395-123">Ayarları aşağıdaki hello ile tooadd gelen güvenlik kuralı gerekir: **TCP** hello protokolü için  **\***  hello kaynak (Genel) bağlantı noktası için ve **9999** için Merhaba (özel) hedef bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="6a395-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![ekran görüntüsü](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="6a395-125">Ağ güvenlik grubundaki karşın, tıklayın **ağ arabirimleri** ve Not hello **genel IP adresi** hello sonraki adımda gerekli tooconnect tooyour VM olacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="6a395-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="6a395-126">Merhaba VM üzerinde gerekli yazılımı yükleyin</span><span class="sxs-lookup"><span data-stu-id="6a395-126">Install required software on hello VM</span></span>
<span data-ttu-id="6a395-127">toorun Merhaba bizim VM'de Jupyter Not Defteri, biz Jupyter ve bağımlılıklarını önce yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a395-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="6a395-128">SSH kullanarak tooyour linux vm bağlanın ve vm oluştururken seçtiğiniz hello kullanıcı adı/parola çifti hello.</span><span class="sxs-lookup"><span data-stu-id="6a395-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="6a395-129">Bu öğreticide biz PuTTY kullanın ve Windows'dan bağlanın.</span><span class="sxs-lookup"><span data-stu-id="6a395-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="6a395-130">Ubuntu üzerinde Jupyter yükleme</span><span class="sxs-lookup"><span data-stu-id="6a395-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="6a395-131">Tablodan sağlanan hello bağlantılardan birini kullanarak Anaconda, popüler veri bilimi python dağıtımı yüklemek [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="6a395-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="6a395-132">Bu belgenin Hello makalenin yazıldığı sırada hello aşağıdaki bağlantıları var. hello en toodate sürümleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="6a395-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="6a395-133">Linux için anaconda yükler</span><span class="sxs-lookup"><span data-stu-id="6a395-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="6a395-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="6a395-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="6a395-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="6a395-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="6a395-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="6a395-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="6a395-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="6a395-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="6a395-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="6a395-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="6a395-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="6a395-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="6a395-140">Anaconda3 yükleme 2.3.0 Ubuntu üzerinde 64-bit</span><span class="sxs-lookup"><span data-stu-id="6a395-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="6a395-141">Örnek olarak, bu, Ubuntu üzerinde Anaconda nasıl yükleyebileceğinizi değil.</span><span class="sxs-lookup"><span data-stu-id="6a395-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![ekran görüntüsü](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="6a395-143">Jupyter yapılandırma ve SSL kullanma</span><span class="sxs-lookup"><span data-stu-id="6a395-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="6a395-144">Yükledikten sonra tootake şu anda toosetup hello yapılandırma dosyaları için Jupyter ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="6a395-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="6a395-145">Jupyter yapılandırma ile sorunlarına karşılaşırsanız hello en yararlı toolook olabilir [Jupyter not defteri Server çalıştıran belgelerine](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="6a395-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="6a395-146">Sonraki biz `cd` toohello directory toocreate bizim SSL sertifikası profili ve hello profilleri yapılandırma dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="6a395-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="6a395-147">Linux'ta hello aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a395-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="6a395-148">Komut toocreate hello SSL sertifikası (Linux ve Windows) aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a395-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="6a395-149">Toohello dizüstü bağlanırken otomatik olarak imzalanan bir SSL sertifikası oluşturuyoruz olduğundan tarayıcınız bir güvenlik uyarısı erişmenizi sağlayan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6a395-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="6a395-150">Uzun vadeli üretim kullanımı için toouse kuruluşunuz ile ilişkilendirilen düzgün olarak imzalanan bir sertifika isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6a395-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="6a395-151">Sertifika yönetimi bu demo hello kapsamı dışında olduğundan, biz tooa otomatik olarak imzalanan sertifika şu an için bağlı kalın.</span><span class="sxs-lookup"><span data-stu-id="6a395-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="6a395-152">Ayrıca bir sertifika toousing, de parola tooprotect defterinizde yetkisiz kullanıma karşı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a395-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="6a395-153">Tooencrypt gerekir böylece güvenlik nedenleriyle Jupyter şifrelenmiş parola, yapılandırma dosyasında parolanızı ilk kullanır.</span><span class="sxs-lookup"><span data-stu-id="6a395-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="6a395-154">IPython yardımcı programı toodo bunu sağlar; bir komut isteminde hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6a395-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="6a395-155">Bu bir parola ve onay ister ve ardından hello parola yazdırır.</span><span class="sxs-lookup"><span data-stu-id="6a395-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="6a395-156">Bu adım aşağıdaki Merhaba unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6a395-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="6a395-157">Ardından, biz hello profilinin yapılandırma dosyasını düzenlersiniz `jupyter_notebook_config.py` bulunduğunuz hello dizindeki dosyayı.</span><span class="sxs-lookup"><span data-stu-id="6a395-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="6a395-158">Bu dosya, olmayabilir--not yalnızca, hello durumda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6a395-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="6a395-159">Bu dosya alan sayısını vardır ve varsayılan olarak tüm dışı bırakılır.  Bu dosyayı, istediğiniz herhangi bir metin düzenleyicisi ile açmak ve onu sahip en az Merhaba, içerik emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="6a395-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="6a395-160">**Merhaba sha1 hello önceki adımdaki ile Merhaba yapılandırmada emin tooreplace hello c.NotebookApp.password olması**.</span><span class="sxs-lookup"><span data-stu-id="6a395-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="6a395-161">Merhaba Jupyter not defteri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="6a395-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="6a395-162">Bu noktada hazır toostart hello Jupyter not defteri duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="6a395-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="6a395-163">toodo bunu toostore not defterlerini istediğiniz ve komut aşağıdaki hello ile Merhaba Jupyter not defteri sunucu başlangıç toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="6a395-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="6a395-164">Şimdi gerekir, Jupyter not defteri hello adresindeki mümkün tooaccess olması `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="6a395-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="6a395-165">Dizüstü bilgisayarınızı ilk eriştiğinizde hello oturum açma sayfası için parolanızı ister.</span><span class="sxs-lookup"><span data-stu-id="6a395-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="6a395-166">Ve oturum açtığında Tim merkezi tüm dizüstü bilgisayar işlemleri için olduğu hello "Jupyter not defteri Pano" görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6a395-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="6a395-167">Bu sayfadan yeni not defterlerini oluşturun ve varolanları açın.</span><span class="sxs-lookup"><span data-stu-id="6a395-167">From this page you can create new notebooks and open existing ones.</span></span>

![ekran görüntüsü](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="6a395-169">Merhaba Jupyter Not Defteri kullanarak</span><span class="sxs-lookup"><span data-stu-id="6a395-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="6a395-170">Merhaba tıklatırsanız **yeni** düğmesi, giriş sayfası aşağıdaki hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6a395-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![ekran görüntüsü](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="6a395-172">Merhaba alanı ile işaretlenmiş bir `In []:` istemi hello giriş alanını ve geçerli bir Python kodu buraya yazın ve, isabet olduğunda yürütecek `Shift-Enter` veya hello "Yürüt" simgesini (Merhaba sağı üçgen hello araç çubuğunda) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a395-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="6a395-173">Güçlü bir standardı: zengin medya hesaplama belgelerle Canlı</span><span class="sxs-lookup"><span data-stu-id="6a395-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="6a395-174">Bazı yönlerden her ikisinin bir karışımı olduğundan, Hello dizüstü kendisini Python ve bir sözcük işlemci kullanan çok doğal tooanyone eşitleyerek: Python kod bloklarını yürütebilir, ancak çok "Code" hücreden hello stilini değiştirerek notları ve diğer metin da tutabilirsiniz "Ma rkdown"Merhaba açılır menü araç çubuğundaki kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6a395-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="6a395-175">Jupyter hesaplama ve zengin ortam (metin, grafik, video ve hemen modern bir web tarayıcısı görüntüleyebilirsiniz her şeyi) karıştırma verdiğinden sözcük işlemci çok daha fazladır.</span><span class="sxs-lookup"><span data-stu-id="6a395-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="6a395-176">Karışımı, metin, kod, videolar ve daha fazlası!</span><span class="sxs-lookup"><span data-stu-id="6a395-176">You can mix, text, code, videos and more!</span></span>

![ekran görüntüsü](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="6a395-178">Ve kitaplıkların bilimsel ve teknik, ekran, aşağıdaki hello bilgi işlem için Python'un birçok mükemmel hello gücüne sahip basit bir hesaplama ile aynı tüm bir ortamda bir karmaşık ağ analizi olarak kolaylaştırır hello gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6a395-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="6a395-179">Bu kip hello modern web hello gücünü Canlı hesaplama ile karıştırma, çok sayıda olasılık sunar ve hello bulut için ideal olarak uygundur; Merhaba not defteri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="6a395-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="6a395-180">Hesaplama karalama alanı toorecord keşif bir sorun üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="6a395-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="6a395-181">arkadaşlarınızla 'Canlı' hesaplama formunda veya basılı kopya biçimleri (HTML, PDF) tooshare sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="6a395-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="6a395-182">toodistribute ve hesaplama, Öğrenciler hemen hello gerçek koduyla deneyebilirsiniz şekilde gerektiren mevcut Canlı öğretme malzemeleri değiştirin ve etkileşimli olarak yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6a395-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="6a395-183">"hello sonuçlarını araştırma hemen çoğaltılamaz bir biçimde sunmak yürütülebilir yazıları" tooprovide doğrulandı ve başkaları tarafından Genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="6a395-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="6a395-184">Ortak bilgi işlem için bir platform olarak: birden çok kullanıcı aynı toothe içinde oturum not defteri sunucu tooshare Canlı hesaplama oturumu.</span><span class="sxs-lookup"><span data-stu-id="6a395-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="6a395-185">Toohello IPython kaynak kodu giderseniz [deposu][repository], indirin ve ardından kendi Azure Jupyter VM deneme dizüstü bilgisayar örnekleri ile tüm bir dizin bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6a395-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="6a395-186">Yalnızca hello karşıdan `.ipynb` hello dosyalarından site ve dizüstü bilgisayarınızı Azure VM hello Pano yükleyin (veya hello doğrudan VM indirin).</span><span class="sxs-lookup"><span data-stu-id="6a395-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="6a395-187">Sonuç</span><span class="sxs-lookup"><span data-stu-id="6a395-187">Conclusion</span></span>
<span data-ttu-id="6a395-188">Merhaba Jupyter Not Defteri, azure'da hello Python ekosistemi hello gücü etkileşimli olarak erişmek için güçlü bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a395-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="6a395-189">Çok çeşitli Python, veri çözümleme ve görselleştirme, benzetimi ve paralel bilgi işlem öğrenme ve basit araştırması dahil olmak üzere kullanım durumları kapsar.</span><span class="sxs-lookup"><span data-stu-id="6a395-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="6a395-190">Merhaba elde edilen not defteri belgeler gerçekleştirilir ve diğer Jupyter kullanıcılarla paylaşılabilir hello hesaplamalar eksiksiz bir kaydı içerir.</span><span class="sxs-lookup"><span data-stu-id="6a395-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="6a395-191">Merhaba Jupyter not defteri yerel bir uygulama kullanılabilir, ancak azure'da bulut dağıtımları için ideal olarak uygun</span><span class="sxs-lookup"><span data-stu-id="6a395-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="6a395-192">Merhaba çekirdek Jupyter özelliklerini Visual Studio içinde kullanılabilir de [Visual Studio için Python Araçları] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="6a395-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="6a395-193">PTVS olan ücretsiz ve açık kaynaklı Visual Studio hata ayıklama, IntelliSense, Gelişmiş bir düzenleyiciyle içeren Gelişmiş bir Python geliştirme ortamında profil oluşturma ve paralel dönüştürür Microsoft'tan eklenti computing tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="6a395-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a395-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a395-194">Next steps</span></span>
<span data-ttu-id="6a395-195">Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="6a395-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
