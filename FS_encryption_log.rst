File System Encryption Test
===========================
Test executed on our cloud controller:

::

  # rbd map volume-3bedc7bc-eaed-466f-9d55-f2c29b44a7b2 --pool volumes
  /dev/rbd0
  
  # lsb        
  lsblk        lsb_release  

  # lsblk -f
  NAME          FSTYPE      LABEL UUID                                   MOUNTPOINT
  sda                                                                    
  |-sda1        ext4              db06fc46-7231-4189-ba2b-0b0117049680   /boot
  |-sda2                                                                 
  |-sda5        swap              e5b98538-8337-4e25-8f82-f97f04258716   [SWAP]
  `-sda6        LVM2_member       n4SAgY-GRNy-4Fl2-ROoQ-rRIf-bdBP-QC1B6s
    `-vg00-root ext4              1e3f1ff1-8677-4236-8cb4-07d5cad32441   /
  rbd0          crypto_LUKS       c4bee3b9-e0dc-438e-87ae-2a3e491081c0   
  
  # mount /dev/rbd0 /mnt/
  mount: unknown filesystem type ‘crypto_LUKS’
