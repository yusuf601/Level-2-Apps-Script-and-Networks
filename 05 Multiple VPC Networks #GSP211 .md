# GSP211
>🚨 [PLEASE SUBSCRIBE OUR CHANNEL CLOUDHUSTLER](https://www.youtube.com/@cloudhustlers) **&** [JOIN OUR COMMUNITY](https://chat.whatsapp.com/KBfUcSleGGEFf2Xvvm8FW3)
## Run in cloudshell (SOLUTION UPDATED 24/08/2023)
### (ZONE1 from Task 2, Step 3)
```cmd
export ZONE1=
```
### (REGION2 from Task 3, Step 4 `only the text inside yellow box`)
```cmd
export REGION2=
```
```cmd
export REGION1=${ZONE1%-*}
gcloud compute networks create managementnet --subnet-mode=custom
gcloud compute networks subnets create managementsubnet-$REGION1 --network=managementnet --region=$REGION1 --range=10.130.0.0/20
gcloud compute networks create privatenet --subnet-mode=custom
gcloud compute networks subnets create privatesubnet-$REGION1 --network=privatenet --region=$REGION1 --range=172.16.0.0/24
gcloud compute networks subnets create privatesubnet-$REGION2 --network=privatenet --region=$REGION2 --range=172.20.0.0/20
gcloud compute firewall-rules create managementnet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=managementnet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0
gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0
gcloud compute instances create managementnet-$REGION1-vm --zone=$ZONE1 --machine-type=e2-micro --subnet=managementsubnet-$REGION1
gcloud compute instances create privatenet-$REGION1-vm --zone=$ZONE1 --machine-type=e2-micro --subnet=privatesubnet-$REGION1
gcloud compute instances create vm-appliance \
    --zone=$ZONE1 \
    --machine-type=e2-standard-4 \
    --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=privatesubnet-$REGION1 \
    --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=managementsubnet-$REGION1 \
    --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=mynetwork
```
