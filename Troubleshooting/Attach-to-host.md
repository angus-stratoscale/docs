
# Attach to host procedure
Prerequisites: Verify you have enough free space on the host under stratonode:/mnt/mancala0 or similar, ensure you clean up any exported data immediately after it's been verified at the destination.

Tip: Use zpool list in order to find a filesystem with enough free space

NOTE : NEVER DELETE FILES FROM THE HOST

 1. In the UI power-off the VM, this is not mandatory but will ensure
    all writes are committed, resulting image may be in dirty shutdown.

 2. In the UI go to the VM boot volume and CLONE it.

 3. Note the volume ID of the cloned volume.

 4. SSH into the node and type the following command.
	 5. mancala volumes attach-to-host <volume-id > < node full internal dns name >

 5.   note : the full dns internal name can be find in UI > nodes . just add : <node-name>.node.strato
--   for example :

 5.   mancala volumes attach-to-host 81e2a68a-4f9b-410b-932a-e1fc1fddca43 stratonode0.node.strato

 6.   Now you get a mount point with a virtual block device , like : /dev/nbd63

 7. type from the shell :
 8.   dd if=/dev/<mount point> of=/mnt/mancala0/EXPORT.raw bs=4M
 9.   example:
 10.   dd if=/dev/nbd63 of=/mnt/mancala0/my_vm_exported.raw bs=4M
    

 11.   Wait until all the stream written successfully into the file .
    

 12. Once done, copy the exported file off the node (scp)

 13. Execute detach-from-host command when finished

  

9. Clean up any files resulting from the above work

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4NjE4NDA1MCw2NDA2OTA3MzAsLTgwOD
czMjA0NSwxODAxODA1NTg3XX0=
-->