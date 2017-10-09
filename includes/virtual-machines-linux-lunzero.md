<span data-ttu-id="04a85-101">Bir diski LUN 0 mevcut değilse veri diskleri tooa Linux VM eklerken hatalarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04a85-101">When adding data disks tooa Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span></span> <span data-ttu-id="04a85-102">Hello kullanarak el ile bir disk ekliyorsanız `azure vm disk attach-new` komutu ve belirtirseniz bir LUN (`--lun`) hello izin vermek yerine, Azure platformu toodetermine uygun LUN Merhaba, dikkatli olun bir disk zaten var. / LUN 0 yer alır.</span><span class="sxs-lookup"><span data-stu-id="04a85-102">If you are adding a disk manually using hello `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing hello Azure platform toodetermine hello appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span></span> 

<span data-ttu-id="04a85-103">Merhaba çıktısını parçacığıyla gösteren örnek aşağıdaki hello göz önünde bulundurun `lsscsi`:</span><span class="sxs-lookup"><span data-stu-id="04a85-103">Consider hello following example showing a snippet of hello output from `lsscsi`:</span></span>

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

<span data-ttu-id="04a85-104">Merhaba iki veri diski LUN 0 ve LUN 1 mevcut (Merhaba ilk sütunda hello `lsscsi` çıkış ayrıntıları `[host:channel:target:lun]`).</span><span class="sxs-lookup"><span data-stu-id="04a85-104">hello two data disks exist at LUN 0 and LUN 1 (hello first column in hello `lsscsi` output details `[host:channel:target:lun]`).</span></span> <span data-ttu-id="04a85-105">Her iki diskin hello VM içinden gelen accessbile olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04a85-105">Both disks should be accessbile from within hello VM.</span></span> <span data-ttu-id="04a85-106">El ile Merhaba LUN 1 ve ikinci bir disk hello LUN 2 konumundaki eklenen ilk disk toobe belirttiyseniz, hello disklerden doğru VM içinden göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04a85-106">If you had manually specified hello first disk toobe added at LUN 1 and hello second disk at LUN 2, you may not see hello disks correctly from within your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="04a85-107">Hello Azure `host` değer 5 Bu örneklerde, ancak bu seçtiğiniz depolama hello türüne bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="04a85-107">hello Azure `host` value is 5 in these examples, but this may vary depending on hello type of storage you select.</span></span>
> 
> 

<span data-ttu-id="04a85-108">Bu disk davranış Azure sorun ancak hello Linux çekirdek hello SCSI belirtimleri izleyen hello yolu değil.</span><span class="sxs-lookup"><span data-stu-id="04a85-108">This disk behavior is not an Azure problem, but hello way in which hello Linux kernel follows hello SCSI specifications.</span></span> <span data-ttu-id="04a85-109">Merhaba Linux çekirdek hello SCSI veri yoluna bağlı aygıtları için tarama yaptığında bir aygıtı LUN değerine 0 ek cihazlar için tarama hello sistem toocontinue sırada bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04a85-109">When hello Linux kernel scans hello SCSI bus for attached devices, a device must be found at LUN 0 in order for hello system toocontinue scanning for additional devices.</span></span> <span data-ttu-id="04a85-110">Bu nedenle:</span><span class="sxs-lookup"><span data-stu-id="04a85-110">As such:</span></span>

* <span data-ttu-id="04a85-111">Merhaba çıkışını gözden `lsscsi` bir diski LUN 0 olması bir veri diski tooverify ekledikten sonra.</span><span class="sxs-lookup"><span data-stu-id="04a85-111">Review hello output of `lsscsi` after adding a data disk tooverify that you have a disk at LUN 0.</span></span>
* <span data-ttu-id="04a85-112">Diskinizin doğru VM içinden gösterilmez, bir diski LUN 0 mevcut doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="04a85-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span></span>

