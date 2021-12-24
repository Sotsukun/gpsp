# gpSP makefile
# Gilead Kutnick - Exophase
# pandora port - notaz
# respberry pi - DPR

# Global definitions

CROSS_COMPILE=arm-linux-gnueabihf-

CC        = $(CROSS_COMPILE)gcc

OBJS      = main.o cpu.o memory.o video.o input.o sound.o gui.o \
            cheats.o zip.o arm_stub.o  warm.o cpu_threaded.o video_blend.o sha1.o imageio.o

BIN       = gpsp

# Platform specific definitions 

VPATH      += .. ../arm
CFLAGS     = -DARM_ARCH -DPC_BUILD -DBITTBOY -Wall
#CFLAGS     += -Ofast -fdata-sections -ffunction-sections -fsingle-precision-constant -fno-PIC -flto -march=armv5te -mtune=arm926ej-s -fprofile-generate=./profile
CFLAGS     += -Ofast -fdata-sections -fdata-sections -fno-common -fno-PIC -marm -mtune=cortex-a7 -mfpu=neon-vfpv4 -mfloat-abi=hard -march=armv7ve -ffast-math -fomit-frame-pointer -fno-strength-reduce
CFLAGS     += -I$(shell pwd)/../../SDK_miyoo283_demo_2048/dependency/release/include/cust_inc 
CFLAGS     += -I$(shell pwd)/../../SDK_miyoo283_demo_2048/dependency/release/include/cust_inc/SDL/


# expecting to have PATH set up to get correct sdl-config first

LIBS    = -nodefaultlibs -lc -lgcc -lSDL -lpng -lz -Wl,--as-needed -Wl,--gc-sections -flto -s
LIBS	+= -L$(shell pwd)/../../SDK_miyoo283_demo_2048/dependency/release/nvr/i2m/common/glibc/8.2.1/cust_libs/dynamic/ 
LIBS	+= -L$(shell pwd)/../../SDK_miyoo283_demo_2048/dependency/release/nvr/i2m/common/glibc/8.2.1/mi_libs/dynamic/ 
LIBS		+= -lmi_common -lmi_sys -lmi_disp -lmi_panel -lmi_gfx -lmi_divp -lmi_ao -lmad -Wl,--as-needed -Wl,--gc-sections -s 

# Compilation:

all: $(BIN)

%.o: %.S
	$(CC) $(CFLAGS) -c -o $@ $<

cpu.o cpu_threaded.o: CFLAGS += -Wno-unused-variable -Wno-unused-label

$(BIN): $(OBJS)
	$(CC) $(OBJS) $(LIBS) -o $(BIN)

clean:
	rm -f *.o $(BIN)
