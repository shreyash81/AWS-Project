# AWS-Project-Cost-Optimization

#Identifying Stale EBS Snapshots
In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

EXPLANATIONS:

1:Fetching Snapshots: The function retrieves all EBS snapshots owned by the account using describe_snapshots.

2:Fetching Active Instances: The function retrieves all active (running and stopped) EC2 instances using describe_instances with a filter for instance-state-name.

3:Checking Volumes: For each snapshot, the function checks if the associated volume exists and if it is attached to any active EC2 instance.

4:Deleting Stale Snapshots: If the volume is not attached to any active instance or if the volume does not exist, the function deletes the snapsho


#Identifying Stale EBS Snapshots and Volumes

In the case of if EBS snapshots is associated with volume and that volume is not attached to any running instance then delete the volume as well them to save on storage costs.

EXPLANATIOS:

1:Volume Check and Deletion: After verifying that the snapshot's volume is not attached to any running instance, the function attempts to delete the volume. This is done by calling ec2.delete_volume(VolumeId=volume_id).

2:Handling Attachments: If the volume has attachments, the code checks if any of the attached instances are running. If none of them are running, the snapshot and volume are deleted.

3:Exception Handling: If the volume is not found (it might have been deleted already), the snapshot is deleted.

#Identifying Stale EBS Snapshots and Volumes and Running Instances

OR In the case of if ebs snapshot is associated with volume and that volume is attached to any active instance then firstly delete the running instance after that delete the volume and snapshots.

EXPLANATIOS:

1:Termination of Instances: If the volume is attached to any running instance, the function terminates the instance using ec2.terminate_instances(InstanceIds=[attachment['InstanceId']]).

2:Deleting Snapshots and Volumes: After terminating the instance, the function deletes the snapshot and the volume.

3:Handling Attachments: If the volume is not attached to any running instance, it proceeds to delete the snapshot and the volume as before.

4:Exception Handling: If the volume is not found, the snapshot is deleted as it might be associated with a non-existent volume.






