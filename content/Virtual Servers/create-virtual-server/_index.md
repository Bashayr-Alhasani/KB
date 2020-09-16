---
title: "How to Create a Virtual Server"
date: 2020-9-29T11:02:05+06:00
weight: 4
draft: false
---
Login to Bluvat Virtual Datacenter admin page, then got to:
Project --> Compute --> Instances
Click on the Launch Instance Button. Then, the Launch Instance dialog will appear with the first default ***flavor***

![](http://95.177.209.65/uploads/create-an-instance.png)
A ***Flavor*** is an available hardware configuration for an instance. bluvalt comes with a list of default flavors to be used by all users. The Launch Instance dialog provides the details of the selected flavor and how it will count against the Project Quotas.

there are three main tabs in the instance creation page:

| Tab | Description |
| -------- | -------- |
| Details  | Enter instance details, in terms of Availability Zone, Instance Name, Flavor, Instance Count, Instance Boot Sources and Image Name. This tab also lists ‘Flavor Details’ in a grid, along with the ‘Project Limits’; in order to show the resources used by the project in comparison with the project quotas.   |
| Access & Security | This tab controls connectivity to an instance via SSH key pairs, security groups, and other mechanisms.|
| Networking | It enables users to choose required network(s) for an instance. If there is only one network available for the project, then it is selected by default. To select or deselect the network, click the + or - sign button next to it. 
Upon network selection, click the Launch button and pay attention to how the Status, Task and Power State fields change for the new VM.

