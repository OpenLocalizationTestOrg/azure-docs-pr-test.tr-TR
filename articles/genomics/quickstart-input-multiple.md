---
title: "Hızlı Başlangıç: Çoklu giriş kullanarak iş akışı gönderme | Microsoft Docs"
titleSuffix: Azure
description: "Bu hızlı başlangıçta msgen istemcisini yüklediğiniz ve hizmette örnek verileri başarıyla çalıştırdığınız kabul edilmektedir."
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: quickstart
ms.date: 12/07/2017
ms.openlocfilehash: d410516f807b7914e15bed1fb93ee58d3e340d1e
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/13/2017
---
# <a name="submit-a-workflow-using-multiple-inputs-from-the-same-sample"></a>Aynı örnekten birden fazla giriş kullanarak iş akışı gönderme

Bu hızlı başlangıçta giriş dosyanız **aynı örnekten alınan** birden fazla FASTQ veya BAM dosyası olduğunda Microsoft Genomiks hizmetine iş akışı gönderme adımları gösterilmektedir. Ancak aynı gönderide FASTQ ve BAM dosyalarını bir arada **kullanamayacağınızı** unutmayın.

Bu konu başlığında `msgen` istemcisini yükleyip çalıştırdığınız ve Azure Depolama konusunda bilgi sahibi olduğunuz kabul edilmektedir. Sağlanan örnek verileri kullanarak başarıyla bir iş akışı gönderdiyseniz bu hızlı başlangıca devam etmeye hazırsınız demektir. 


## <a name="multiple-bam-files"></a>Birden fazla BAM dosyası

### <a name="upload-your-input-files-to-azure-storage"></a>Giriş dosyalarınızı Azure depolamaya yükleme
Giriş olarak *reads.bam*, *additional_reads.bam* ve *yet_more_reads.bam* olmak üzere birden fazla BAM dosyasına sahip olduğunuzu ve bunları *myaccount* adlı Azure depolama hesabınıza yüklediğinizi düşünelim. API URL'sine ve erişim anahtarına sahipsiniz. **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>** içinde iki çıkış olmasını istiyorsunuz.


### <a name="submit-your-job-to-the-msgen-client"></a>İşinizi `msgen` istemcisine gönderme 

Birden fazla BAM dosyasını adlarını --input-blob-name-1 komutuna bağımsız değişken olarak ileterek gönderebilirsiniz. Tüm dosyaların aynı örnekten gelmesi gerektiğini ancak sıralamanın önemli olmadığını unutmayın. Aşağıda Windows'da komut satırında ve Unix'te yapılandırma dosyası kullanılarak gerçekleştirilen örnek gönderimlere yer verilmiştir. Kodun daha anlaşılır olması için satır sonları eklenmiştir:


Windows için:

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


Unix için

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


Yapılandırma dosyası kullanmayı tercih ediyorsanız şu bileşenleri dahil etmeniz gerekir:

``` config.txt
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads.bam additional_reads.bam yet_more_reads.bam
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

`config.txt` dosyasını şu çağrıyla gönderin: `msgen submit -f config.txt`


## <a name="multiple-paired-fastq-files"></a>Birden fazla eşleştirilmiş FASTQ dosyası

### <a name="upload-your-input-files-to-azure-storage"></a>Giriş dosyalarınızı Azure depolamaya yükleme
Giriş olarak *reads_1.fq.gz* ve *reads_2.fq.gz*, *additional_reads_1.fq.gz* ve *additional_reads_2.fq.gz* ile *yet_more_reads_1.fq.gz* ve *yet_more_reads_2.fq.gz* olmak üzere birden fazla eşleştirilmiş FASTQ dosyasına sahip olduğunuzu düşünelim. Bunları *myaccount* adlı Azure depolama hesabınıza yüklediniz. API URL'sine ve erişim anahtarına sahipsiniz. **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>** içinde iki çıkış olmasını istiyorsunuz.


### <a name="submit-your-job-to-the-msgen-client"></a>İşinizi `msgen` istemcisine gönderme 

Eşleştirilmiş FASTQ dosyalarının aynı örneğe ait olması ve bir arada işlenmesi gerekir.  Dosya adlarının sırası --input-blob-name-1 ve --input-blob-name-2 komutlarına bağımsız değişken olarak ilettiğinizde önemlidir. 

Aşağıda Windows'da komut satırında ve Unix'te yapılandırma dosyası kullanılarak gerçekleştirilen örnek gönderimlere yer verilmiştir. Kodun daha anlaşılır olması için satır sonları eklenmiştir:


Windows için:

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz ^
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


Unix için:

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz \
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


Yapılandırma dosyası kullanmayı tercih ediyorsanız şu bileşenleri dahil etmeniz gerekir:

```
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads_1.fq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz
input_blob_name_2:                reads_2.fq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

`config.txt` dosyasını şu çağrıyla gönderin: `msgen submit -f config.txt`

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede birden fazla BAM dosyasını veya eşleştirilmiş FASTQ dosyalarını Azure Depolama'ya yükleyip `msgen` python istemcisi üzerinden Microsoft Genomiks hizmetine bir iş akışı gönderdiniz. İş akışının gönderilmesi ve Microsoft Genomiks hizmetiyle kullanabileceğiniz diğer komutlar hakkında daha fazla bilgi için bkz. [SSS](frequently-asked-questions-genomics.md). 