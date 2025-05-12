# pi-spi
pi-spi is a SPI C library for Raspberry Pi using the SPI kernel driver.

Overlays
========
Includes python overlay.
This is available with `include pi_spi`.

Documentation
=============
To read documentation:-  
	C:	`man pi-spi`
	Python:	`python3 -m pydoc pi_spi`  

*I initially developed this as part of a larger project, but realised it could form a stand alone library.  
This should work on any Linux system which includes the SPI kernel driver.*

Implementation 
==========
`pi-spi` accesses the SPI kernel driver using the `ioctl()` system call.
`pi_spi` is a python wrapper using the `ctypes` library.
