#
# Makefile:

ifneq ($V,1)
Q ?= @
endif

#DEBUG	= -g -O0
DEBUG	= -O3
# INCLUDE	= -I/usr/local/include
# INCLUDE	= -I/usr/include
CFLAGS	= $(DEBUG) -Wall $(INCLUDE) -Winline -pipe
# CFLAGS	= $(DEBUG) -Wall  -Winline -pipe

# change to use local vs system
LDFLAGS	= -L/usr/local/lib
# LDFLAGS	= -L/usr/lib
LDLIBS    = -lpi-spi -lpthread -lm -lcrypt -lrt

###############################################################################

SRC	=	spidev_test.c \
		awrite.c \
		aread.c \
		ADXL345.c

OBJ	=	$(SRC:.c=.o)

BINS	=	$(SRC:.c=)

all:	$(BINS)

.c.o:
	$Q echo [CC] $<
	$Q $(CC) -c $(CFLAGS) $< -o $@

.cc.o:
	$Q echo [Compile] $<
	$Q $(CC) -c $(CFLAGS) $< -o $@

clean:
	$Q echo "[Clean]"
	$Q rm -f $(OBJ) *~ core tags $(BINS)

