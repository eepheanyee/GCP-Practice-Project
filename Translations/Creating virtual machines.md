#In this lab, you explore the available options for VMs and see the differences between locations.

##In this lab, you learn how to perform the following tasks:

##Create several standard VMs
##Create advanced VMs


#Create a utility virtual machine:

1. Create a VM instance with name = "my-vm" in the us-central1-c zone with machine type n1-standard-1 with 1 cpu,3.75gb memory and assign it an external ip

        gcloud beta compute --project=qwiklabs-gcp-02-1527b5eaf70f instances create my-vm --zone=us-central1-c --machine-type=n1-standard-1 --subnet=default --no-address --maintenance-policy=MIGRATE --service-account=106254238149-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-10-buster-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=my-vm --no-shielded-secure-boot --no-shielded-vtpm --no-shielded-integrity-monitoring --reservation-affinity=any

2. Explore the vm details:

        gcloud compute instances describe my-vm --zone=us-central1-c

3. Explore the vm logs:
 
        gcloud logging logs list

#Create a windows virtual machine:

4. Create a VM instance with name = "my-vm2" in the europe-west2-a zone with machine type n1-standard-2 with 2 cpus,7.5gb memory, windows server OS version 2016 datacore and 100gb SSD persistent disk

        gcloud beta compute --project=qwiklabs-gcp-02-1527b5eaf70f instances create my-vm2 --zone=europe-west2-a --machine-type=n1-standard-2 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=106254238149-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --tags=http-server,https-server --image=windows-server-2016-dc-core-v20200813 --image-project=windows-cloud --boot-disk-size=100GB --boot-disk-type=pd-ssd --boot-disk-device-name=my-vm2 --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

5. Create firewall rules to allow http and https traffic:

        gcloud compute --project=qwiklabs-gcp-02-1527b5eaf70f firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server
        gcloud compute --project=qwiklabs-gcp-02-1527b5eaf70f firewall-rules create default-allow-https --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server

6. Set Password for the VM:

        gcloud compute reset-windows-password my-vm2 --zone=europe-west2-a

#Create a custom VM:

7. Create a VM instance with name = "my-vm" in the us-west1-b zone with machine type custom with 6 cpus,32gb memory

        gcloud beta compute --project=qwiklabs-gcp-02-1527b5eaf70f instances create my-vm3 --zone=us-west1-b --machine-type=custom-6-32768 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=106254238149-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-10-buster-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=my-vm3 --no-shielded-secure-boot --no-shielded-vtpm --no-shielded-integrity-monitoring --reservation-affinity=any

8. SSH into VM:

        gcloud compute ssh --project=qwiklabs-gcp-02-1527b5eaf70f --zone=us-west1-b vm_name=my-vm3
