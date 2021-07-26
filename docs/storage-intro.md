# Storage

AWS storage services are grouped into three different categories: block storage, file storage, and object storage. 

## File Storage

Each file has metadata such as file name, file size, and the date the file was created. The file also has a path, for example, computer/Application_files/Cat_photos/cats-03.png. When you need to retrieve a file, your system can use the path to find it in the file hierarchy.

## Block Storage

While file storage treats files as a singular unit, block storage splits files into fixed-size chunks of data called blocks that have their own addresses. Since each block is addressable, blocks can be retrieved efficiently. 

Since block storage is optimized for low-latency operations, it is a typical storage choice for high-performance enterprise workloads, such as databases or enterprise resource planning (ERP) systems, that require low-latency storage. 

## Object Storage

Objects, much like files, are also treated as a single unit of data when stored. However, unlike file storage, these objects are stored in a flat structure instead of a hierarchy. 

Each object is a file with a unique identifier. This identifier, along with any additional metadata, is bundled with the data and stored.

With object storage, you can store almost any type of data, and there is no limit to the number of objects stored, making it easy to scale. Object storage is generally useful when storing large data sets, unstructured files like media assets, and static assets, such as photos.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/storage-intro1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>