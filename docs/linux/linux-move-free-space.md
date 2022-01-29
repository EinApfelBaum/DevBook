---
created: 22.10.2021
tags: linux gparted
parent: Linux
---

# Move free space from end of the drive to first partition with gparted

## Problem

Is is frustrating - no matter how I try, gparted won't let me assign the empty space to the first partition:

![Unallocated space at the end](/assets/images/linux/Move_free_space_problem_1.png)

The middle partition is blocking me from expanding `/dev/sda1`. I need to move partition `/dev/sda2` to the end of the drive, like so (fabricated image):

![Unallocated space at the middle](/assets/images/linux/Move_free_space_problem_2.png)

Then I will be able to expand first partition:

![Unallocated space added to partition](/assets/images/linux/Move_free_space_problem_3.png)

How to do that? I assume data from `/dev/sda2` must be physically copied to end of the drive.

## Solution

It is recommended that, before making any changes, you make backups of any data you do not want to lose in case anything goes wrong.

Before you start, both partitions will need to be unmounted– if you cannot unmount one of them (e.g. because it is your root partition), use a live CD with GParted (e.g. the GParted live CD or the Ubuntu live CD) and resize them that way.

1. Select the second (extended) partition, and click on Resize/Move

    ![Step 1](/assets/images/linux/Move_free_space_solution_1.png)

2. Use the right handle to extend the partition to the end of the free space, and then click on Resize/Move

    ![Step 2](/assets/images/linux/Move_free_space_solution_2.png)

3. Select the contained swap partition, and click on Resize/Move

    ![Step 3](/assets/images/linux/Move_free_space_solution_3.png)

4. Drag the partition to the end of the extended partition, and then click on Resize/Move

    ![Step 4](/assets/images/linux/Move_free_space_solution_4.png)

5. You can safely click OK on this warning message, as we are only moving a swap partition

    ![Step 5](/assets/images/linux/Move_free_space_solution_5.png)

6. Select the extended partition again and click on Resize/Move

    ![Step 6](/assets/images/linux/Move_free_space_solution_6.png)

7. Use the left handle to shrink the partition to the end of the free space, and then click on Resize/Move

    ![Step 7](/assets/images/linux/Move_free_space_solution_7.png)

8. Then, select the first partition, and click on Resize/Move

    ![Step 8](/assets/images/linux/Move_free_space_solution_8.png)

9. Use the right handle to extend the partition to the end of the free space, and then click on Resize/Move

    ![Step 9](/assets/images/linux/Move_free_space_solution_9.png)

10. Finally, click on Apply and your partitions should be reformatted

    ![Step 10](/assets/images/linux/Move_free_space_solution_10.png)

---

## Resources

* [https://unix.stackexchange.com/questions/271671/move-free-space-from-end-of-the-drive-to-first-partition-with-gparted](https://unix.stackexchange.com/questions/271671/move-free-space-from-end-of-the-drive-to-first-partition-with-gparted)
