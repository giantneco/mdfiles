# GCP JA NIGHT 2016/07/14
## GCP 最新動向を一通り紹介

kind of cloud
 10years ago
   .
node.js on Google Clouod Appps

 simple to use GCP API
  download credential -> json object

'''javascript
// use google clould client library
var gcloud = require('gcloud');

var storage - glcoud.storage();
var bucket = storage .bucket(process.env.UPLOAD_BUCKET);

// use google cloud vision api
var vision = gcloud.vision();
...

var datastore = gcloud.datastore();

post(path,...)  function*req, res9{
  var storagePath + ...;
   bucket.upload(req.file, ....

 vision.annotate(args, function(...) {

 }
.
'''

check trace of appcliation from google cloud platoform console

 - check differenece between 2 version
 - GCP notify if version change make performance change ?

show pull command tab, shows docker pull command

app engineautomatic
 high SLA.
 java8, python3x, node, go
 automatic HTTPS support


## compute engine (brian)
VMs are better computer
 GCE instances ae beter MVs
 。
 create new instance in 30s

 inside project,  DNS settinag automaticcally
.
bandwidth
 2GB per CPU

Ask for 10 VMs , you get 10 VM

persisten Disks
 standard or SSSD, up to 64TB

Disk performance
 bigger disk , good performance

Disk snapthos
 globla!
 any zone, any time

load balancer
 1+ million requests/sec
  SSL terminations, URL routing

Billing
 per minute
 sustained use discounts
  preemptible VMs (you can kill anytime!

ML based usage alerts

persisitent disk
 google の分散ディスク
 ブロック単位で２つの、チェックサム比較

## BIg Query

BigQuery + carto = visualization

## Google Cloud Dataflow
