## 1. software install
### （1）add current user to docker group [need root authority]
```r
sudo usermod -a -G docker $(whoami)
sudo service docker restart
newgrp docker
```
### （2）software install

```r
# method 1: docker pull
docker pull crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wy_hg002_uhrr:v2.1.0.0
docker tag crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wy_hg002_uhrr:v2.1.0.0 wy_hg002_uhrr:v2.1.0.0
docker rmi crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wy_hg002_uhrr:v2.1.0.0
# method 2: docker load
docker load -i wy_hg002_uhrr_v2.1.0.0.tar
```

## 3. Usage
```r
# run HG002 sample
newgrp docker
docker run --rm \
  -v /path/to/hg002/fastq file or fastq directory:/app/input/fastq file or fastq directory \  # HG002 fastq file or directory [if fastq directory is provided, we will automatically detect all fastq.gz/fq.gz files in this directory and merge them]    
  -v /path/to/output/directory:/app/output \                                                  # output directory (make sure output directory is empty)
  wy_hg002_uhrr:v2.1.0.0 \
  --fastq_fn1=/app/input/fastq file or fastq directory \                                      # HG002 fastq file or directory (consistent with the previous fastq or folder)
  --sample_ID1="HG002" \                                                                      # HG002 sample id (default: HG002)      
  --output_dir=/app/output/ \                                                                 # output directory (no need to change it) 
  --threads=20                                                                                # number of threads (default: 20) 
# run UHRR
newgrp docker
docker run --rm \
  -v /path/to/uhrr/fastq file or fastq directory:/app/input/fastq file or fastq directory \  # UHRR fastq file or directory [if fastq directory is provided, we will automatically detect all fastq.gz/fq.gz files in this directory and merge them]     
  -v /path/to/output/directory:/app/output \                                                 # output directory (make sure output directory is empty)
  wy_hg002_uhrr:v2.1.0.0 \
  --fastq_fn2=/app/input/fastq filename or fastq directory \                                 # UHRR fastq file or directory (consistent with the previous fastq or folder)
  --sample_ID2="UHRR" \                                                                      # UHRR sample id (default: UHRR)
  --output_dir=/app/output/ \                                                                # output directory (no need to change it) 
  --threads=20                                                                               # number of threads (default: 20) 
```
