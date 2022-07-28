---
title: "File Servers Overview"
weight: 20
pre: "4. "
---

{{< youtube BCYgjyywcFU >}}

#### Resources

* **[Slides]({{< relref "/6-application-servers/04-file-servers-overview-slides.md" >}})**
* [Standard RAID Levels](https://en.wikipedia.org/wiki/Standard_RAID_levels) on Wikipedia
* [Nested RAID Levels](https://en.wikipedia.org/wiki/Nested_RAID_levels)on Wikipedia
* [Parity](http://crystalclearmaths.com/videos-learning-resources/fun-stuff/parity/) from Crystal Clear Mathematics
* [What are the Different Types of Storage: Block, Object and File?](https://blog.ubuntu.com/2015/05/18/what-are-the-different-types-of-storage-block-object-and-file) on Ubuntu Blog
* [NAS vs. SAN vs. DAS: Which is Right for You?](https://blog.seagate.com/business/nas-vs-san-vs-das-which-is-right-for-you/) from Seagate Blog
* [Getting Started with Storage: Understanding SAN vs NAS vs DAS](https://vanillavideo.com/blog/2014/started-storage-understanding-san-nas-das) from Vanilla Video
* [Storage Education and Learning Resources for VMware Admins](http://www.virtualizationsoftware.com/storage-education-learning-resources-vmware-admins/) from VirtualizationSoftware.com

#### Video Transcript

The first type of application server we will cover in this module is the file server. In essence, a file server is simply a system on the network that is responsible for sharing files and storage resources to users in our organization. While that may seem simple on the surface, there is quite a bit going on behind the scenes.

Of course, the major component of any storage server is the actual storage medium itself. Typically most servers today use either the traditional, rotational hard disk drive, or HDD, or the newer solid state drives, or SSD. Each one has significant tradeoffs in terms of storage size, price, and performance, so you should look at each option closely to determine which one is best for your organization.

Once you have your storage, you'll also need to understand how it is viewed by your computer or operating system. Typically storage devices can be accessed in one of three ways. Most computers use a file storage system, where data is stored and represented as files in a hierarchical file system. This is what we have been dealing with so far in this course. However, you can also use storage devices as block storage, which stores binary data in identically sized blocks. In fact, the file systems you are familiar with are actually just abstractions on top of a block-based storage device. However, block storage might be preferred for some uses, such as databases or large files. Finally, you can also treat a storage device as an object store, where data is stored as independent objects on the disk, regardless of any underlying block structure. This is very uncommon right now, but it may become more common going forward. Amazon's Simple Cloud Storage Service, or S3, is a great example of object storage.

Another major concept in file servers is the use of RAID. RAID originally stood for "Redundant Array of Inexpensive Disks,", but more recently it has been referred to as "Redundant Array of Independent Disks" as well. In a RAID, multiple disks are combined in unique ways to either increase the overall performance of the system, or to provide for better data protection in case of a failure. In some cases, RAID can even be used to achieve both goals. While you may not deal with RAID in a cloud environment, it is still very common on certain storage devices, so it is helpful to understand what it is.

RAID uses a variety of "levels" to determine how the disks are combined. There are several commonly used RAID levels, so I'll cover just a few of them. First is RAID 0, commonly known as "striping." In this setup, each data file is split, or "striped" across two drives. In this way, any attempts to read or write the file are much faster than on a single drive, since they can work in tandem. However, if either drive experiences a failure, the data on both drives will be unusable. So, you gain performance, but it increases the risk of data loss.

RAID 1 is known as "mirroring," and is effectively the opposite of RAID 0. In RAID 1, each data file is written in its entirety to each disk. So, the disks are perfect copies of each other. If one disk fails, the system can continue to run using the other disk, often without the user even noticing the difference. With RAID 1, you gain increased resistance to data loss, but it doesn't add any performance. Thankfully, RAID 1 can generally perform just about as well as a single drive, so there isn't much of a performance loss, either.

The next most commonly used RAID is RAID 5. Yes, RAID 2 through RAID 4 exist, but they aren't used very much in practice today. They are somewhat like B batteries in that regard. In RAID 5, typically four disks are used. When data is stored to the drive, it is written across three of them, with the fourth drive containing a "parity" section that can be used to verify the data. That parity sections are spread across each of the four drives, making read and write performance higher than if it was stored on a single drive. With this setup, if any one drive experiences a failure, the data on it can be reconstructed using the information present on the other three drives. With this setup, you can gain some performance over using a single drive, while still getting better data protection as well. Unfortunately, you have to give up one quarter of your storage space for this to work, but I'd say it is probably worth it.

So, what is parity? At its core, parity is just a checksum value that is based on the other values in the data. For binary, typically we use either Even Parity or Odd Parity. In Even Parity, we would make sure that the data plus the parity bit has an even number of 1s, while in Odd Parity we would make sure there are an odd number of 1s. So, in this example, looking at the second line, we see that the data includes five 1s. To make it an even number of 1s, we would set the Even Parity bit to 1. If we are using Odd Parity instead, we would set it to 0. Then, if we lost any single bit in the original data, we could determine what it was just by looking at the remaining data and the parity bit. With RAID levels such as RAID 5, we can use that same trick to reconstruct data on a drive that failed, just by looking at the remaining drives. Pretty neat, right?

Back to RAID levels, RAID 6 is very similar to RAID 5, but with two different parity sections spread across typically 5 or more drives. RAID 6 is designed in such a way that any two drives can fail and the data will still be secure. As with RAID 5, RAID 6 also includes some performance boosts as well.

Lastly, RAID levels can sometimes be combined in unique ways. For example, RAID 1+0 is a RAID 0 made up of two RAID 1 setups. In this way, you can gain the performance boost of striping with the enhanced data protection of mirroring, all in a single RAID. There are many other ways that this can be done, depending on the number of disks you have available and the characteristics you'd like your RAID to have.

Ok, so once you've determined how to configure your disks, the next step is to create partitions. A partition is a division of a physical disk into multiple parts. Each partition can be used for different things, such as block storage, different file systems or operating systems, or even as swap space. Years ago, it was very common to partition disks several ways in order to store multiple operating systems on the same disk, or to separate the operating system from the data. However, as hard drives have grown in size and dropped in price, coupled with the rise of virtualization, it is very uncommon to have multiple data partitions on the same disk today. Your operating system may automatically manage a few small partitions for system recovery and boot information, but in general, you probably won't be dealing with partitions much in the future.

As you set up your file server, you may also have to deal with the various protocols that can be used to access the files. Most servers today typically use the Windows-based protocol Server Message Block or SMB, which is sometimes also referred to as the Common Internet File System or CIFS. Windows servers and clients natively use these protocols to share files, and Linux-based systems can use Samba to do the same. If files are being shared between multiple Linux systems, they could also use the Network File System or NFS protocol. In the lab assignment, you'll learn how to set up servers using the SMB protocol using Windows Server and Samba.

In addition, there are protocols for sharing files over the internet. The most commonly used are the File Transfer Protocol, or FTP, and the SSH File Transfer Protocol, or SFTP, which transfers files via an SSH-secured tunnel. Finally, some storage devices maybe accessed using lesser-known protocols such as the Internet Small Computer Systems Interface, or iSCSI, and the Fibre Channel Protocol, or FCP. These are typically used in storage area networks to access data stored on block devices, as well see a bit later in this video.

Another concern that comes with storage is the location of the storage itself. There are typically three ways to think about where to locate your storage. First, you can use DAS, or direct-attached storage. This would be large storage devices connected directly to your system, such as a large external hard drive. In some cases, this might be the best option since it is generally the simplest and cheapest. However, it isn't very flexible if you need to share that information with multiple systems.

The other two options are NAS, or network attached storage, and SAN, or a storage area network. As you can probably tell, these two terms are often confusing, so I'll try to explain them in detail.

This graphic shows the major difference between a NAS and a SAN. Network attached storage simply refers to storage that is available via a network. Typically, NAS is accessed at the file level, using protocols such as SMB or NFS. In essence, you can think of any dedicated file server as a NAS device. A SAN, on the other hand, is a collection of storage devices that are typically accessed at the block level by a file server, using protocols such as iSCSI or FCP. If a file server needs access to a large amount of storage, you might set up a SAN inside your datacenter, with several large-scale block storage devices that actually handle the storage of the data. Hopefully this helps you make sense of these two similar terms.

Lastly, I'd like to introduce one major trend in storage, which is the concept of storage virtualization. Just like with hardware virtualization, it is possible to add a virtual layer between the physical storage devices and the systems using those devices. In that way, you could seamlessly migrate storage across multiple physical systems without interrupting access to the data. This diagram does a great job of showing how you could use different disks across a variety of hardware setups to create virtual datastores for your data. However, storage virtualization does come with a downside, being that the virtualization layer could represent a single point of failure in your infrastructure. So, you may have to carefully analyze the risks that such as setup would bring compared to the added flexibility it provides.

That should give you a pretty good overview of some common terms and concepts you'll come across when dealing with file servers. The next two videos will discuss some of the implementation steps for setting up your own file server in both Windows and Samba on Ubuntu.