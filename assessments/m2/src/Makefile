#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#
#------------------------------------------------------------------------------
#include sources.mk

include sources.mk 

# Platform Overrides
CFLAGS = -g -Wall -Werror -std=c99
CPPFLAGS = 
PLATFORM ?= HOST

ifeq ($(PLATFORM), HOST)
    # Compiler Flags and Defines 
    CC = gcc
    CPPFLAGS += -DHOST
else ifeq ($(PLATFORM), msp432)
    CC = arm-none-eabi-gcc
    LINKER_FILE = path/to/linker_script.ld
    CPU = cortex-m4
    ARCH = armv7e-m
    SPECS = nosys.specs
    CFLAGS += -mcpu=$(CPU) -march=$(ARCH) --specs=$(SPECS)
    LDFLAGS = -T $(LINKER_FILE)
endif

# Target rules
.PHONY: all program clean compile-all
all: program

program: $(OBJECTS)
	$(CC) $(CFLAGS) $(CPPFLAGS) -o program $(OBJECTS) $(LDFLAGS)

%.o: %.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c $< -o $@

%.i: %c
	$(CC) $(CFLAGS) $(CPPFLAGS) -E $< -o $@
%asm: %c 
	$(CC) $(CFLAGS) $(CPPFLAGS) -S $< -o $@

clean:
# del /Q *.o program
ifeq ($(OS),Windows_NT)
# -del /Q *.o program.exe
	-del /Q $(OBJECTS)
else
	-rm -f $(OBJECTS)
endif
