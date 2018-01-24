# mask_rcnn
This is the testing based on mask_rcnn(floyd.com)
## step 1
```git clone https://github.com/matterport/Mask_RCNN.git```
## step 2
```  
cd mask_rcnn 
floyd login
floyd init mask_rcnn
//leverage the existing coco training dataset in floyd
floyd run --env tensorflow-1.3   --mode jupyter --data narenst/datasets/coco-train-2014/1:mount
```   
## step 3 下载模型在COCO数据集上预训练权重（mask_rcnn_coco.h5)
```vi download.sh```
```id=$1
	driveURL='https://drive.google.com/uc?export=download'
	filename="$(curl -sc /tmp/gcokie "${driveURL}&id=${id}" | grep -o '="uc-name.*</span>' | sed 's/.*">//;s/<.a> .*//')"  
	getcode="$(awk '/_warning_/ {print $NF}' /tmp/gcokie)"  
	curl -Lb /tmp/gcokie "${driveURL}&confirm=${getcode}&id=${id}" -o "${filename}"
```
```bash download.sh 1dNi9Ny1h9KBMj_3mocMQNapeEwgeERlz```
## step 4 如果需要在COCO数据集上训练或测试，需要安装pycocotools， clone下来，make生成对应的文件，拷贝下工程目录下即可
```mkdir coco
git clone https://github.com/waleedka/coco.git
cd coco/PythonAPI && make
```
## step 5 
如果使用COCO数据集，需要：
pycocotools (即第4条描述的)
MS COCO Dataset。2014的训练集数据(floyd已经存在）
COCO子数据集，5K的minival和35K的validation-minus-minival
```curl -o t1 https://dl.dropboxusercontent.com/s/o43o90bna78omob/instances_minival2014.json.zip?dl=0
curl -o t2 https://dl.dropboxusercontent.com/s/s3tw5zcg7395368/instances_valminusminival2014.json.zip?dl=0
unzip -n t1 -d ./annotation/
unzip -n t2 -d ./annotation/
```
