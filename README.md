# Sharanya-5-AWS-Cloud-Cost-Optimization

## Identifying Stale EBS Snapshots

Implemented a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

### Description:
Cost optimization is a key responsibility for engineers and it is the main advantage in cloud.This project implements a  cost optimization project using the Lambda function where it fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.To explain more breifly:

### 1.Fetch All EBS Snapshots:

The function initiates by fetching a list of all EBS snapshots owned by the AWS account using the describe_snapshots API call with the parameter 'OwnerIds': ['self']. This ensures that only snapshots owned by the same AWS account are retrieved.

### 2.Retrieve Active EC2 Instances:

The function then fetches a list of all active EC2 instances (both running and stopped) using the describe_instances API call. This provides information about the currently active EC2 instances and their attached volumes.

### 3.Check Each Snapshot:

For each EBS snapshot retrieved, the function checks if the snapshot's associated volume ID (if it exists) is attached to any of the active EC2 instances.
This is done by comparing the volume ID of the snapshot with the volume IDs attached to the active instances.

### 4.Identify Stale Snapshots:

A snapshot is considered stale if its associated volume is not attached to any active EC2 instance.
If the volume associated with a snapshot is not found in the list of active volumes, it means the snapshot is no longer needed and can be deleted.

### 5.Delete Stale Snapshots:

The function deletes the identified stale snapshots using the delete_snapshot API call.
This action helps to free up storage space and reduce storage costs by removing unnecessary snapshots.

The Lambda function automates the process of identifying and deleting stale EBS snapshots that are not associated with any active EC2 instances. By doing so, it helps optimize AWS storage costs by ensuring that only necessary snapshots are retained, thereby preventing unnecessary storage expenses.
