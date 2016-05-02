# CompressedModules for LibreELEC

This PR was pointless because because their was no net gain on space recovered.  Because of this, I'm archiving this for future reference.

    xz|```9.7M    /lib/modules/4.4.6```
    
    gzip|```12.6M   /lib/modules/4.4.6```
    
    none|```37.5M   /lib/modules/4.4.6```

  - Enable xz and gzip compression for kernel modules.
  - Project can apply either xz, gzip or no compression to the kernel modules.  
    - The only exception as is, are the nvidia kernel modules which jump through some wonky hoops.
  - The compression takes place after everything is installed to $INSTALL and before squashing, thus packages falling under .install_init will be uncompressed as expected and busybox can continue to handle the uncompressed init modules if they exist.
  - Tested that each compression works and that the modules.dep is generated successfully.
  - Inserted modules each time to verify the kernel does load the modules as expected.
  - Because the SYSTEM squashed file can be compressed, the resulting SYSTEM file size tends to stay the same.  If no compression is being used, the resulting SYSTEM file would be smaller, and if xz was used on the squashed system, there would be really no gain.  This whole endeavor was an attempt to shrink SYSTEM so that reading it from disk at boot would go faster.  This should work as expected in some scenarios, but not many.
