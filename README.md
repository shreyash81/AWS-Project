# AWS-Project-Cost-Optimization

Identifying Stale EBS Snapshots
In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.
In the case of if it is associated with volume and that volume is not attached to any running instance then delete the volume as well them to save on storage costs.
OR In the case of if ebs snapshot is associated with volume and that volume is attached to any active instance then firstly delete the running instance after that delete the volume and snapshots.

Description:
The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.
