# Elastic Block Storage

Amazon EBS is a block-level storage device that you can attach to an Amazon EC2 instance. These storage devices are called Amazon EBS volumes. They are similar to how we attach an external drive to our laptops.

There are two main categories of Amazon EBS volumes: solid-state drives (SSDs) and hard-disk drives (HDDs). SSDs provide strong performance for random input/output (I/O), while HDDs provide strong performance for sequential I/O. AWS offers two types of each.

## Scaling

Scaling is done in two ways
 * Increase volume size (max 16TB)
 * Attach multiple EC2 instances to volume

## Uses

 * **Operating systems**: Boot/root volumes to store an operating system. The root device for an instance launched from an Amazon Machine Image (AMI) is typically an Amazon EBS volume. These are commonly referred to as EBS-backed AMIs. 
 * **Databases**: A storage layer for databases running on Amazon EC2 that rely on transactional reads and writes.
 * **Enterprise applications**: Amazon EBS provides reliable block storage to run business-critical applications.
 * **Throughput-intensive applications**: Applications that perform long, continuous reads and writes.

## Benefits

 * **High availability**: When you create an EBS volume, it is automatically replicated within its Availability Zone to prevent data loss from single points of failure.
 * **Data persistence**: The storage persists even when your instance doesn’t.
 * **Data encryption**: All EBS volumes support encryption.
 * **Flexibility**: EBS volumes support on-the-fly changes. You can modify volume type, volume size, and input/output operations per second (IOPS) capacity without stopping your instance.
 * **Backups**: Amazon EBS provides you the ability to create backups of any EBS volume.

## EBS Snapshots

We can backup EBS by taking snapshots of it. This will be stored in multiple AZ within S3.