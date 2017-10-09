
1. Listelenen hello adımları kullanarak Azure aboneliği tooyour oturum [tooAzure hello Azure CLI 1.0 ' bağlanma](../articles/xplat-cli-connect.md).

2. Aşağıdaki gibi hello Klasik dağıtım modunda olduğundan emin olun:

    ```azurecli
    azure config mode asm
    ```

3. Merhaba Linux görüntüyü hello kullanılabilir görüntülerden tooload gibi istediğiniz bulun:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    Bir Windows komut istemi penceresinde grep yerine **find** komutunu kullanın.
   
4. Kullanım `azure vm create` toocreate hello önceki listeden hello Linux görüntüsü olan bir VM. Bu adımda bir bulut hizmeti ve depolama hesabı oluşturulur. VM tooan mevcut bulut hizmeti ile bağlantı kurulamadı bir `-c` seçeneği. Bir SSH uç noktası toolog hello ile toohello Linux sanal makine oluşturma `-e` seçeneği. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` hello kullanarak `Ubuntu-14_04_4-LTS` hello görüntüde `West US` konumu ve bir kullanıcı adı ekler `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Bir Linux sanal makine için hello sağlamalısınız `-e` seçeneğini `vm create`. Merhaba sanal makine oluşturulduktan sonra olası tooenable SSH değil. SSH hakkında daha fazla bilgi için okuma [nasıl tooUse Linux Azure üzerinde SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Merhaba VM hello özniteliklerini hello kullanarak doğrulayabilirsiniz `azure vm show` komutu. Merhaba aşağıdaki örnek listeler bilgi hello adlı VM için `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. VM ile Merhaba Başlat `azure vm start` gibi komut:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Sonraki adımlar
Bu Azure CLI 1.0 sanal makine komutlar hakkında daha fazla bilgi için hello okuma [hello Klasik dağıtım API'si ile kullanma hello Azure CLI 1.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

