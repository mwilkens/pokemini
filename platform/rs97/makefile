# PokeMini Makefile for SDL

CC = /opt/rs97-toolchain/bin/mipsel-linux-gcc
LD = /opt/rs97-toolchain/bin/mipsel-linux-gcc
STRIP = /opt/rs97-toolchain/bin/mipsel-linux-strip
POKEROOT = ../../
BUILD = Build
TARGET = PokeMini

CFLAGS = -Ofast -fdata-sections -ffunction-sections -mno-fp-exceptions -mno-check-zero-division -mframe-header-opt -fno-common -flto -Wall $(INCLUDE) -DPERFORMANCE
SLFLAGS = -Ofast -lSDL -lm -lz -flto -no-pie -Wl,--as-needed -Wl,--gc-sections -lz

INCDIRS = source sourcex resource freebios dependencies/minizip

OBJS = \
 PokeMini_SDL.o	\
 sourcex/KeybMapSDL.o	\
 freebios/freebios.o	\
 source/PMCommon.o	\
 source/PokeMini.o	\
 source/Multicart.o	\
 source/Hardware.o	\
 source/Video.o	\
 source/Video_x3.o	\
 source/CommandLine.o	\
 source/MinxCPU.o	\
 source/MinxCPU_XX.o	\
 source/MinxCPU_CE.o	\
 source/MinxCPU_CF.o	\
 source/MinxCPU_SP.o \
 source/MinxTimers.o	\
 source/MinxIO.o	\
 source/MinxIRQ.o	\
 source/MinxPRC.o	\
 source/MinxColorPRC.o	\
 source/MinxLCD.o	\
 source/MinxAudio.o	\
 source/UI.o	\
 source/Joystick.o	\
 source/Keyboard.o	\
 resource/PokeMini_ColorPal.o	\
 resource/PokeMini_Font12.o	\
 resource/PokeMini_Icons12.o	\
 dependencies/unzip.o	\
 dependencies/ioapi.o	\
 resource/PokeMini_BG3.o

DEPENDS = \
 sourcex/KeybMapSDL.h	\
 freebios/freebios.h	\
 source/IOMap.h	\
 source/PMCommon.h	\
 source/PokeMini.h	\
 source/PokeMini_Version.h	\
 source/Multicart.h	\
 source/Hardware.h	\
 source/Video.h	\
 source/Video_x3.h	\
 source/CommandLine.h	\
 source/MinxCPU.h	\
 source/MinxTimers.h	\
 source/MinxIO.h	\
 source/MinxIRQ.h	\
 source/MinxPRC.h	\
 source/MinxColorPRC.h	\
 source/MinxLCD.h	\
 source/MinxAudio.h	\
 source/UI.h	\
 source/Joystick.h	\
 source/Keyboard.h	\
 resource/PokeMini_ColorPal.h	\
 resource/PokeMini_Font12.h	\
 resource/PokeMini_Icons12.h	\
 resource/PokeMini_BG3.h	\
 dependencies/minizip/unzip.h	\
 dependencies/minizip/ioapi.h	
 
 
BUILDOBJS = $(addprefix $(BUILD)/, $(notdir $(OBJS)))
DEPENDSHDR = $(addprefix $(POKEROOT), $(DEPENDS))
INCLUDE = $(foreach inc, $(INCDIRS), -I$(POKEROOT)$(inc))
VPATH = $(addprefix $(POKEROOT),$(INCDIRS))

.PHONY: all clean

all: $(BUILD) $(TARGET)

$(BUILD):
	@[ -d @ ] || mkdir -p $@

$(BUILD)/%.o: %.c $(DEPENDSHDR)
	$(CC) $(CFLAGS) -o $@ -c $<

$(TARGET): $(BUILDOBJS)
	$(LD) -o $(TARGET) $(BUILDOBJS) $(SLFLAGS)

clean:
	-rm -f $(BUILDOBJS) $(TARGET) $(WINTARGET) $(WINRES_TRG)
	-rmdir --ignore-fail-on-non-empty $(BUILD)
