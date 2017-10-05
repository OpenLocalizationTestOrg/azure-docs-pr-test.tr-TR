---
title: "Jupyter/IPython not defteri oluşturma | Microsoft Docs"
description: "Azure resource manager dağıtım modelinde oluşturulan Linux sanal makinede Jupyter/IPython dizüstü dağıtmayı öğrenin."
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
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="5f44d-103">Bir Azure Jupyter yükleme ve Jupyter not defteri Azure üzerinde çalışan VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f44d-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="5f44d-104">[Jupyter proje](http://jupyter.org), eskiden [IPython proje](http://ipython.org), bir koleksiyon için araçlar sağlar kod yürütmeyi canlı bir oluşturulmasını ile birleştirin güçlü etkileşimli Kabukları kullanarak bilimsel hesaplama Hesaplama belgesi.</span><span class="sxs-lookup"><span data-stu-id="5f44d-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="5f44d-105">Bu not defteri dosyaları rastgele metin, matematiksel formüller, giriş kod, sonuçları, grafik, videolar ve modern bir web tarayıcısı görüntüleyebilen ortamının başka herhangi bir tür içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="5f44d-106">Python için kesinlikle yeni ve eğlenceli, etkileşimli bir ortamda öğrenin veya paralel/teknik ciddi bazı bilgi işlem yapmak istediğiniz olup olmadığını Jupyter not defteri harika bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="5f44d-107">![Ekran](./media/jupyter-notebook/ipy-notebook-spectral.png) ses kaydını yapısını çözümlemek için kullanarak SciPy ve Matplotlib paketleri.</span><span class="sxs-lookup"><span data-stu-id="5f44d-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="5f44d-108">Jupyter iki yolu: Azure dizüstü bilgisayarlar veya özel dağıtım</span><span class="sxs-lookup"><span data-stu-id="5f44d-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="5f44d-109">Azure için kullanabileceğiniz bir hizmet sunar [Jupyter kullanarak hızlı bir şekilde başlatmak ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f44d-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="5f44d-110">Azure Not Defteri hizmetini kullanarak, kolayca Jupyter'ın web üzerinden erişilebilen arabirimi Python tüm gücünü ile ölçeklenebilir hesaplama kaynaklarına ve onun birçok kitaplıklarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f44d-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="5f44d-111">Yükleme hizmeti tarafından işlenen olduğundan, kullanıcılar Yönetim ve yapılandırma kullanıcı tarafından gerek kalmadan bu kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="5f44d-112">Senaryonuz için Not Defteri hizmeti çalışmıyorsa Lütfen size Microsoft Azure üzerinde Jupyter not defteri dağıtma Linux sanal makineleri (VM'ler) kullanarak gösterir bu makalenin okumaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="5f44d-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="5f44d-113">Oluşturma ve Azure üzerinde bir VM yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5f44d-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="5f44d-114">Azure üzerinde çalışan sanal makine (VM) oluşturmak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="5f44d-115">Bu VM bulutta eksiksiz bir işletim sistemi ve Jupyter not defteri çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="5f44d-116">Azure Linux ve Windows sanal makineleri çalıştırabilen ve her iki tür sanal makineler üzerinde Jupyter Kurulum ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="5f44d-117">Bir Linux VM oluşturun ve Jupyter için bir bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="5f44d-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="5f44d-118">Verilen yönergeleri izleyin [burada] [ portal-vm-linux] , bir sanal makine oluşturmak için *Ubuntu* dağıtım.</span><span class="sxs-lookup"><span data-stu-id="5f44d-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="5f44d-119">Bu öğretici, Ubuntu Server 14.04 LTS kullanır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="5f44d-120">Kullanıcı adı varsayıyoruz *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="5f44d-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="5f44d-121">Sanal makine dağıtıldıktan sonra bir ağ güvenlik grubu güvenlik kuralı açmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="5f44d-122">Azure Portal'dan Git **ağ güvenlik grupları** ve VM'nize karşılık gelen güvenlik grubu için sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="5f44d-123">Aşağıdaki ayarlarla bir gelen güvenlik kuralı eklemeniz gerekir: **TCP** protokolü için  **\***  kaynak (Genel) bağlantı noktası için ve **9999** için (özel) hedef bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="5f44d-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![ekran görüntüsü](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="5f44d-125">Ağ güvenlik grubundaki karşın, tıklayın **ağ arabirimleri** ve not edin **genel IP adresi** sonraki adımda VM'nize bağlanmak için gerekli şekilde.</span><span class="sxs-lookup"><span data-stu-id="5f44d-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="5f44d-126">Gerekli yazılımı'nı VM'e yükleyin</span><span class="sxs-lookup"><span data-stu-id="5f44d-126">Install required software on the VM</span></span>
<span data-ttu-id="5f44d-127">Jupyter not defteri bizim VM üzerinde çalıştırmak için biz öncelikle Jupyter ve bağımlılıklarını yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="5f44d-128">Linux vm ssh kullanarak bağlanma ve kullanıcı adı/parola eşleştirin vm oluştururken seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="5f44d-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="5f44d-129">Bu öğreticide biz PuTTY kullanın ve Windows'dan bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="5f44d-130">Ubuntu üzerinde Jupyter yükleme</span><span class="sxs-lookup"><span data-stu-id="5f44d-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="5f44d-131">Tablodan sağlanan bağlantılardan birini kullanarak Anaconda, popüler veri bilimi python dağıtımı yüklemek [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="5f44d-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="5f44d-132">İtibariyle, bu belgenin bağlantılardır en tarih sürümleri kadar.</span><span class="sxs-lookup"><span data-stu-id="5f44d-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="5f44d-133">Linux için anaconda yükler</span><span class="sxs-lookup"><span data-stu-id="5f44d-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="5f44d-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="5f44d-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="5f44d-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="5f44d-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="5f44d-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="5f44d-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="5f44d-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="5f44d-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5f44d-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="5f44d-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="5f44d-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="5f44d-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="5f44d-140">Anaconda3 yükleme 2.3.0 Ubuntu üzerinde 64-bit</span><span class="sxs-lookup"><span data-stu-id="5f44d-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="5f44d-141">Örnek olarak, bu, Ubuntu üzerinde Anaconda nasıl yükleyebileceğinizi değil.</span><span class="sxs-lookup"><span data-stu-id="5f44d-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![ekran görüntüsü](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="5f44d-143">Jupyter yapılandırma ve SSL kullanma</span><span class="sxs-lookup"><span data-stu-id="5f44d-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="5f44d-144">Yükledikten sonra bir kez Jupyter için kurulum yapılandırma dosyaları için bir dakikanızı ayırın gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="5f44d-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="5f44d-145">Jupyter yapılandırma ile sorunlarına karşılaşırsanız bakmak yararlı olabilir [Jupyter not defteri Server çalıştıran belgelerine](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="5f44d-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="5f44d-146">Sonraki biz `cd` profili dizine bizim SSL sertifikası oluşturun ve profilleri yapılandırma dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="5f44d-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="5f44d-147">Linux üzerinde aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="5f44d-148">SSL sertifikası (Linux ve Windows) oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="5f44d-149">Dizüstü tarayıcınız bağlamak için bir güvenlik uyarısı verecektir olduğunda otomatik olarak imzalanan bir SSL sertifikası oluşturmakta olduğunuz bu yana unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="5f44d-150">Uzun vadeli üretim kullanımı için kuruluşunuz ile ilişkilendirilen düzgün olarak imzalanan bir sertifika kullanmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="5f44d-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="5f44d-151">Sertifika yönetiminin bu demo kapsamında olduğundan, biz kendinden imzalı bir sertifika için şu an için bağlı kalın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="5f44d-152">Bir sertifika kullanarak ek olarak, dizüstü bilgisayarınızı yetkisiz kullanıma karşı korumak için bir parola sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="5f44d-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="5f44d-153">Parolanızı ilk şifrelemek gerekir böylece güvenlik nedenleriyle, yapılandırma dosyasında şifrelenmiş parolalar Jupyter kullanır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="5f44d-154">Bunu yapmak için bir yardımcı program IPython sağlar; bir komut isteminde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="5f44d-155">Bu bir parola ve onay ister ve ardından parolayı yazdırır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="5f44d-156">İçin aşağıdaki adımı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="5f44d-157">Ardından, biz profilinin yapılandırma dosyasını düzenlersiniz `jupyter_notebook_config.py` bulunduğunuz dizindeki dosyayı.</span><span class="sxs-lookup"><span data-stu-id="5f44d-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="5f44d-158">Bu dosya, olmayabilir--Not Böyle değilse yalnızca oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f44d-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="5f44d-159">Bu dosya alan sayısını vardır ve varsayılan olarak tüm dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="5f44d-160">Bu dosyayı, istediğiniz herhangi bir metin düzenleyicisi ile açmak ve onu en az aşağıdaki içeriğe sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="5f44d-161">**Önceki adımdan sha1 yapılandırmada c.NotebookApp.password değiştirdiğinizden emin olun**.</span><span class="sxs-lookup"><span data-stu-id="5f44d-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="5f44d-162">Jupyter not defteri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5f44d-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="5f44d-163">Bu noktada biz Jupyter not defteri başlatmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="5f44d-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="5f44d-164">Bunu yapmak için not defterlerinde depolamak ve Jupyter not defteri sunucusu aşağıdaki komutla başlatmak istediğiniz dizine gidin.</span><span class="sxs-lookup"><span data-stu-id="5f44d-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="5f44d-165">Şimdi, Jupyter not defteri adresinde erişebilir olmalıdır `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="5f44d-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="5f44d-166">Dizüstü bilgisayarınızı ilk eriştiğinizde, oturum açma sayfasına parolanızı ister.</span><span class="sxs-lookup"><span data-stu-id="5f44d-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="5f44d-167">Ve oturum açtığında Tim merkezi tüm dizüstü bilgisayar işlemleri için olan "Jupyter not defteri panoyu" görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5f44d-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="5f44d-168">Bu sayfadan yeni not defterlerini oluşturun ve varolanları açın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-168">From this page you can create new notebooks and open existing ones.</span></span>

![ekran görüntüsü](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="5f44d-170">Jupyter Not Defteri kullanarak</span><span class="sxs-lookup"><span data-stu-id="5f44d-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="5f44d-171">Tıklatırsanız **yeni** düğme, aşağıdaki açma sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5f44d-171">If you click the **New** button, you will see the following opening page.</span></span>

![ekran görüntüsü](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="5f44d-173">Alan işaretlenmiş bir `In []:` istemi giriş alanını ve geçerli bir Python kodu buraya yazın ve, isabet olduğunda yürütecek `Shift-Enter` veya (sağı gösteren üçgen araç çubuğunda) "Çalıştır" simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="5f44d-174">Güçlü bir standardı: zengin medya hesaplama belgelerle Canlı</span><span class="sxs-lookup"><span data-stu-id="5f44d-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="5f44d-175">Bazı yönlerden her ikisinin bir karışımı olduğundan dizüstü Python ve bir sözcük işlemci kullandı herkes çok doğal geliyor olmalıdır: Python kod bloklarını yürütebilir, ancak bir "Markdo"Code"hücreden stilini değiştirerek notları ve diğer metin da tutabilirsiniz aşağı"araç çubuğundaki aşağı açılan menüyü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5f44d-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="5f44d-176">Jupyter hesaplama ve zengin ortam (metin, grafik, video ve hemen modern bir web tarayıcısı görüntüleyebilirsiniz her şeyi) karıştırma verdiğinden sözcük işlemci çok daha fazladır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="5f44d-177">Karışımı, metin, kod, videolar ve daha fazlası!</span><span class="sxs-lookup"><span data-stu-id="5f44d-177">You can mix, text, code, videos and more!</span></span>

![ekran görüntüsü](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="5f44d-179">Ve bilimsel ve teknik için birçok mükemmel kitaplıkları Python'un gücü, aşağıdaki ekran görüntüsünde, basit bir hesaplama bir karmaşık ağ analizi, tüm bir ortamda olarak aynı kolaylığı ile gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="5f44d-180">Modern web gücünü Canlı hesaplama ile karıştırma, bu kip pek çok sayıda olasılık sunar ve bulut için ideal uygundur; Not Defteri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="5f44d-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="5f44d-181">Keşif kaydetmek için hesaplama bir karalama alanı bir sorun üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5f44d-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="5f44d-182">'Canlı' hesaplama form veya basılı kopya biçimleri (HTML, PDF) iş arkadaşlarınızı sonuçları paylaşmak için.</span><span class="sxs-lookup"><span data-stu-id="5f44d-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="5f44d-183">Dağıtma ve dinamik öğretme sunmak için hesaplama, Öğrenciler hemen gerçek koduyla deneyebilirsiniz şekilde gerektiren malzemeleri değiştirin ve etkileşimli olarak yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5f44d-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="5f44d-184">"Araştırma sonuçlarını hemen çoğaltılamaz, doğrulandı ve başkaları tarafından genişletilmiş bir şekilde sunmak yürütülebilir yazıları" sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="5f44d-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="5f44d-185">Ortak bilgi işlem için bir platform olarak: birden çok kullanıcı Canlı hesaplama oturumu paylaşmak için aynı not defteri sunucuya oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f44d-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="5f44d-186">IPython kaynak koduna giderseniz [deposu][repository], indirin ve ardından kendi Azure Jupyter VM deneme dizüstü bilgisayar örnekleri ile tüm bir dizin bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5f44d-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="5f44d-187">Yalnızca karşıdan `.ipynb` sitesinden dosyaları ve dizüstü bilgisayarınızı Azure VM Pano yükleyin (veya doğrudan VM'de oturum indirin).</span><span class="sxs-lookup"><span data-stu-id="5f44d-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="5f44d-188">Sonuç</span><span class="sxs-lookup"><span data-stu-id="5f44d-188">Conclusion</span></span>
<span data-ttu-id="5f44d-189">Jupyter Not Defteri, etkileşimli olarak Azure üzerinde Python ekosistemi gücünü erişmek için güçlü bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f44d-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="5f44d-190">Çok çeşitli Python, veri çözümleme ve görselleştirme, benzetimi ve paralel bilgi işlem öğrenme ve basit araştırması dahil olmak üzere kullanım durumları kapsar.</span><span class="sxs-lookup"><span data-stu-id="5f44d-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="5f44d-191">Sonuçta elde edilen not defteri belgeler gerçekleştirilir ve diğer Jupyter kullanıcılarla paylaşılabilir hesaplamayı eksiksiz bir kaydı içerir.</span><span class="sxs-lookup"><span data-stu-id="5f44d-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="5f44d-192">Jupyter not defteri yerel bir uygulama kullanılabilir, ancak azure'da bulut dağıtımları için ideal olarak uygun</span><span class="sxs-lookup"><span data-stu-id="5f44d-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="5f44d-193">Jupyter çekirdek özelliklerini de Visual Studio içinde kullanılabilir [Visual Studio için Python Araçları] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="5f44d-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="5f44d-194">PTVS olan ücretsiz ve açık kaynaklı Visual Studio hata ayıklama, IntelliSense, Gelişmiş bir düzenleyiciyle içeren Gelişmiş bir Python geliştirme ortamında profil oluşturma ve paralel dönüştürür Microsoft'tan eklenti computing tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="5f44d-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f44d-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5f44d-195">Next steps</span></span>
<span data-ttu-id="5f44d-196">Daha fazla bilgi için bkz. [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="5f44d-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
