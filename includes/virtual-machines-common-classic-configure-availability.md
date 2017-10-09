


Yardımcı bir kullanılabilirlik kümesi sanal makinelerinizin kapalı kalma süresi sırasında kullanılabilir gibi tutmak bakımı sırasında. Bir kullanılabilirlik kümesinde iki veya daha fazla benzer şekilde yapılandırılmış sanal makine yerleştirme hello gerekli artıklık toomaintain kullanılabilirliğini sanal makineniz çalıştıran hello uygulamalar veya hizmetler oluşturur. Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz [hello sanal makinelerin kullanılabilirliğini yönetme][Manage hello availability of virtual machines].

En iyi yöntem toouse olan kullanılabilirlik kümeleri ve Yük Dengeleme uç noktaları toohelp uygulamanızın her zaman verimli bir şekilde kullanılabilir ve çalışıyor olduğundan emin olun. Yük dengeli uç noktalar hakkında daha fazla ayrıntı için bkz: [Yük Dengeleme için Azure altyapı hizmetleri][Load balancing for Azure infrastructure services].

Kullanılabilirlik kümesi iki seçenekten birini kullanarak içine Klasik sanal makineleri ekleyin:

* [Seçenek 1: bir sanal makine oluşturun ve aynı hello kullanılabilirlik kümesi zaman][Option 1: Create a virtual machine and an availability set at hello same time]. Ardından, bu sanal makineleri oluşturduğunuzda yeni sanal makineler toohello ekleyin.
* [Seçenek 2: varolan bir sanal makine tooan kullanılabilirlik kümesini ekleme][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> Merhaba Klasik modelde tooput istediğiniz sanal makineleri hello aynı kullanılabilirlik kümesi toohello ait olmalıdır aynı bulut hizmeti.
> 
> 

## <a id="createset"></a>Seçenek 1: bir sanal makine oluşturun ve aynı hello kullanılabilirlik kümesi süresi
Azure PowerShell toodo bu komutları veya ya da hello Azure portalını kullanabilirsiniz.

toouse hello Azure portalı:

1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba hub menüsünde **+ yeni**ve ardından **sanal makine**.
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Toouse istediğiniz hello Market sanal makine görüntüsü seçin. Bir Linux veya Windows sanal makine toocreate seçebilirsiniz.
4. Sanal makine Hello seçilen için o hello dağıtım modeli olarak ayarlanmış çok doğrulayın**Klasik** ve ardından **oluştur**
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Bir sanal makine adı, kullanıcı adı ve parolası (Windows makineler) veya SSH ortak anahtarı (Linux makinelerde) girin. 
6. Merhaba VM boyutunu seçin ve ardından **seçin** toocontinue.
7. Seçin **isteğe bağlı yapılandırma > kullanılabilirlik kümesi**ve tooadd hello sanal makineye istediğiniz hello kullanılabilirlik kümesi seçin.
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Yapılandırma ayarlarınızı gözden geçirin. İşiniz bittiğinde tıklatın **oluşturma**.
9. Azure sanal makine oluştururken altında hello ilerleme durumunu izleyebilirsiniz **sanal makineleri** hello hub menüsünde.

toouse Azure PowerShell toocreate bir Azure sanal makinesi komutları ve tooa yeni veya var olan kullanılabilirlik kümesi ekleme, bkz: [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden yapılandırın](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Seçenek 2: varolan bir sanal makine tooan kullanılabilirlik kümesini ekleyin
Hello Azure portal, kullanılabilirlik kümesi varolan varolan Klasik sanal makineleri tooan ekleyin veya onları için yeni bir tane oluşturun. (Merhaba sanal makineler aynı kullanılabilirlik kümesinde hello unutmayın toohello ait olmalıdır aynı bulut hizmetine.) Merhaba adımları olan neredeyse hello aynı. Azure PowerShell ile Merhaba sanal makine tooan varolan kullanılabilirlik kümesi ekleyebilirsiniz.

1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **sanal makineleri (Klasik)**.
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Sanal makineler Hello listeden hello tooadd toohello kümesi istediğiniz hello sanal makinenin adını seçin.
4. Seçin **kullanılabilirlik kümesi** hello sanal makineden **ayarları**.
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Tooadd hello sanal makineye istediğiniz hello kullanılabilirlik kümesi seçin. Merhaba sanal makine toohello ait olmalıdır hello kullanılabilirlik kümesi aynı bulut hizmeti.
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. **Kaydet** düğmesine tıklayın.

toouse Azure PowerShell komutları, bir yönetici düzeyi Azure PowerShell oturumu açın ve hello aşağıdaki komutu çalıştırın. Merhaba yer tutucuları için (gibi &lt;VmCloudServiceName&gt;), merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi değiştirin, adları ile Merhaba düzeltin.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> Merhaba sanal makine yeniden toobe toofinish toohello kullanılabilirlik kümesi ekleme sahip olabilir.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

