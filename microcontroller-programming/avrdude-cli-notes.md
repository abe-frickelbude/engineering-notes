

# The #$!@ing script that wraps `avrdude` on Linux (at least as provided by PlatformIO) makes use of 
  hardcoded paths (PFUI..), and also insists on specifying the path to _its very own_ configuration
  file when running, even though such a default location should ideally have been known by the tool...
  Keep these factors in mind if you get confusing error messages from `avrdude` 
