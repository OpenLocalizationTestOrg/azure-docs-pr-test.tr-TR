## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="6ef42-101">Nasıl toocreate bir ağ yapılandırması kullanılarak sanal bir ağ dosya Powershell'den</span><span class="sxs-lookup"><span data-stu-id="6ef42-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="6ef42-102">Azure bir xml dosyası toodefine tüm sanal ağların kullanılabilir tooa abonelik kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ef42-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="6ef42-103">Bu dosya indirme, toomodify düzenleyin veya varolan sanal ağları silin ve yeni sanal ağlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ef42-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="6ef42-104">Bu öğreticide, bu dosyayı nasıl toodownload başvurulan öğrenin tooas ağ yapılandırması (veya netcfg) dosyası ve toocreate yeni bir sanal ağ düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="6ef42-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="6ef42-105">toolearn hello ağ yapılandırma dosyası hakkında daha fazla bilgi görmek hello [Azure virtual network yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ef42-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="6ef42-106">toocreate PowerShell, tam hello aşağıdaki adımları kullanarak bir netcfg dosyasını sahip bir sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="6ef42-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="6ef42-107">Azure PowerShell'i hiç kullanmadıysanız, tam hello hello adımları [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azureps-cmdlets-docs) makalesi, ardından tooAzure oturum açın ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="6ef42-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="6ef42-108">Merhaba Hello Azure PowerShell konsolundan kullanmak **Get-AzureVnetConfig** cmdlet toodownload hello ağ yapılandırma dosyası tooa dizini hello aşağıdaki komutu çalıştırarak, bilgisayarınızdaki:</span><span class="sxs-lookup"><span data-stu-id="6ef42-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="6ef42-109">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="6ef42-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="6ef42-110">Herhangi bir XML veya metin düzenleyicisi uygulama kullanarak 2. adımda kaydettiğiniz hello dosyasını açın ve Merhaba arayın  **<VirtualNetworkSites>**  öğesi.</span><span class="sxs-lookup"><span data-stu-id="6ef42-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="6ef42-111">Önceden oluşturulmuş tüm ağlarınız varsa, her ağ kendi olarak görüntülenen  **<VirtualNetworkSite>**  öğesi.</span><span class="sxs-lookup"><span data-stu-id="6ef42-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="6ef42-112">Bu senaryoda açıklanan toocreate hello sanal ağ ekleme XML yalnızca hello altında aşağıdaki hello  **<VirtualNetworkSites>**  öğe:</span><span class="sxs-lookup"><span data-stu-id="6ef42-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="6ef42-113">Merhaba ağ yapılandırma dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6ef42-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="6ef42-114">Merhaba Hello Azure PowerShell konsolundan kullanmak **kümesi AzureVnetConfig** hello aşağıdaki komutu çalıştırarak cmdlet tooupload hello ağ yapılandırma dosyası:</span><span class="sxs-lookup"><span data-stu-id="6ef42-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="6ef42-115">Çıkış döndürdü:</span><span class="sxs-lookup"><span data-stu-id="6ef42-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="6ef42-116">Varsa **OperationStatus** değil *başarılı* hello çıkış döndürülen hatalar ve tam adım 6 için hello xml dosyasını yeniden denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6ef42-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="6ef42-117">Merhaba Hello Azure PowerShell konsolundan kullanmak **Get-AzureVnetSite** yeni ağ hello cmdlet tooverify hello aşağıdaki komutu çalıştırarak eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="6ef42-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="6ef42-118">Merhaba (kısaltılmış) çıkış metnini izleyen hello döndürüldü:</span><span class="sxs-lookup"><span data-stu-id="6ef42-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
