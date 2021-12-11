# Training - Log Amomaly

This article explains about how to do Log Amomaly training in Watson AIOps.

The article is based on the the following

- RedHat OpenShift 4.8 on IBM Cloud (ROKS)
- Watson AI-Ops 3.2.0

## 1. Application

We use BookInfo application here. 

Refer : [20-application-installation/01-iks](../20-application-installation/01-iks) to know how the app is deployed.

![bookinfo](./images/1-app.png)

## 2. Generate Load

The below script can be used for generating load.

Run this script and Generate load.

```bash
#!/bin/bash

while (true)
do
    ab -n 100 -c 5 http://1.1.1.1:31600/productpage?u=normal
done

```

You need to keep this running for 10 minutes.

## 3. Enable Live logs for Training

While the load is ongoing in the application, do the following steps to enable the live log mode and to copy the logs into AIMgr for training. 

1. Goto the page `Data and tool connections` and select `Humio` 

!\[bookinfo\](./images/image-00002.png)

2. Click on the humio connection `humio-connect-bookinfo`

!\[bookinfo\](./images/image-00003.png)

3. Select the `Data flow` : `On`

4. Select the `Mode` : `Live Data for Initial AI Training`

5. Click on the `Save`

!\[bookinfo\](./images/image-00004.png)


Now the live data would get copied to AIMgr.

## 4. Stop Live logs

After 10 minutes, live logs can be disbled.

1. Select the `Data flow` : `Off`

2. Click on the `Save`

!\[bookinfo\](./images/image-00005.png)

## 5. Stop Load

Click on `Ctrl+C` to stop load script.

## 6. Do Training

1. Goto the page `AI Model Management`

2. Click on `Manage` tab

!\[bookinfo\](./images/image-00006.png)

3. Click on `log-anomaly-detection` link

!\[bookinfo\](./images/image-00007.png)

4. Click on `Start Training` link

!\[bookinfo\](./images/image-00008.png)

The training would start and go for `20 to 30 minutes` based on the data size.

You will have `Training Complete` status once the training is done.

5. Click on `Versions` tab

You can see the version trained and deployed.

!\[bookinfo\](./images/image-00009.png)

