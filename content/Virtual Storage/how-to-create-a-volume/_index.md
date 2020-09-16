---
title: "How to Create a Volume"
date: 2020-9-29T11:02:05+06:00
weight: 4
draft: false
---

1.Log in to the dashboard.

2.Select the appropriate project from the drop down menu at the top left.

3.On the `Project` tab, open the `Compute` tab and click `Volumes` category.

4.Click Create `Volume`.

In the dialog box that opens, enter or select the following values.

`Volume Name:` Specify a name for the volume.

`Description:` Optionally, provide a brief description for the volume.

`Volume Source:` Select one of the following options:

- No source, empty volume: Creates an empty volume. An empty volume does not contain a file system or a partition table.
  Snapshot: If you choose this option, a new field for `Use snapshot as a source` displays. You can select the snapshot from the list.
- Image: If you choose this option, a new field for `Use image as a source` displays. You can select the image from the list.
- Volume: If you choose this option, a new field for `Use volume as a source` displays. You can select the volume from the list. Options to use a snapshot or a volume as the source for a volume are displayed only if there are existing snapshots or volumes.
  `Type:` Leave this field blank.

`Size (GB):` The size of the volume in gibibytes (GiB).

`Availability Zone:` Select the Availability Zone from the list. By default, this value is set to the availability zone given by the cloud provider (for example, us-west or apac-south). For some cases, it could be nova.

5.Click Create `Volume`.

The dashboard shows the volume on the Volumes tab.
