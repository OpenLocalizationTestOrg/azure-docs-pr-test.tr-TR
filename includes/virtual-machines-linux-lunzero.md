<span data-ttu-id="b4c01-101">Bir diski LUN 0 mevcut değilse veri disklerinin bir Linux VM eklerken, hatalarla karşılaşabilir.</span><span class="sxs-lookup"><span data-stu-id="b4c01-101">When adding data disks to a Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span></span> <span data-ttu-id="b4c01-102">Kullanarak el ile bir disk ekliyorsanız `azure vm disk attach-new` komutu ve belirtirseniz bir LUN (`--lun`) uygun LUN belirlemek Azure platformu izin vermek yerine dikkatli bir disk zaten var. / LUN 0 yer alır.</span><span class="sxs-lookup"><span data-stu-id="b4c01-102">If you are adding a disk manually using the `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing the Azure platform to determine the appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span></span> 

<span data-ttu-id="b4c01-103">Çıktısını parçacığıyla gösteren aşağıdaki örneği göz önünde bulundurun `lsscsi`:</span><span class="sxs-lookup"><span data-stu-id="b4c01-103">Consider the following example showing a snippet of the output from `lsscsi`:</span></span>

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

<span data-ttu-id="b4c01-104">İki veri diski LUN 0 ve LUN 1 mevcut (ilk sütunda `lsscsi` çıkış ayrıntıları `[host:channel:target:lun]`).</span><span class="sxs-lookup"><span data-stu-id="b4c01-104">The two data disks exist at LUN 0 and LUN 1 (the first column in the `lsscsi` output details `[host:channel:target:lun]`).</span></span> <span data-ttu-id="b4c01-105">Her iki diskin VM içinden gelen accessbile olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b4c01-105">Both disks should be accessbile from within the VM.</span></span> <span data-ttu-id="b4c01-106">LUN 1 eklenecek ilk disk ve LUN 2 konumundaki ikinci diski el ile belirtilen, diskleri doğru VM içinden göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4c01-106">If you had manually specified the first disk to be added at LUN 1 and the second disk at LUN 2, you may not see the disks correctly from within your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b4c01-107">Azure `host` değer 5 Bu örneklerde, ancak bu seçtiğiniz depolama türüne bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="b4c01-107">The Azure `host` value is 5 in these examples, but this may vary depending on the type of storage you select.</span></span>
> 
> 

<span data-ttu-id="b4c01-108">Bu disk davranış Azure sorun ancak Linux çekirdek SCSI belirtimleri izleyen yolu değil.</span><span class="sxs-lookup"><span data-stu-id="b4c01-108">This disk behavior is not an Azure problem, but the way in which the Linux kernel follows the SCSI specifications.</span></span> <span data-ttu-id="b4c01-109">Linux çekirdek SCSI veri yoluna bağlı aygıtları için tarama yaptığında ek cihazlar için taramaya devam etmek için LUN 0 değerine sırada sistem için bir aygıt bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4c01-109">When the Linux kernel scans the SCSI bus for attached devices, a device must be found at LUN 0 in order for the system to continue scanning for additional devices.</span></span> <span data-ttu-id="b4c01-110">Bu nedenle:</span><span class="sxs-lookup"><span data-stu-id="b4c01-110">As such:</span></span>

* <span data-ttu-id="b4c01-111">Çıkışı gözden `lsscsi` LUN 0 bir diske sahip olduğunuzu doğrulamak için bir veri diski ekledikten sonra.</span><span class="sxs-lookup"><span data-stu-id="b4c01-111">Review the output of `lsscsi` after adding a data disk to verify that you have a disk at LUN 0.</span></span>
* <span data-ttu-id="b4c01-112">Diskinizin doğru VM içinden gösterilmez, bir diski LUN 0 mevcut doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b4c01-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span></span>

