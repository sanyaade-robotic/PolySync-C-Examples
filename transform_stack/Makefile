##########################################################
# makefile for transform_stack
##########################################################


# source PolySync environment if not already done, assumes x86_64 if set here
# usually, the environment has these set
PSYNC_HOME ?= /usr/local/polysync
OSPL_HOME ?= $(PSYNC_HOME)/utils/x86_64.linux

# target
TARGET	:= bin/polysync-transform-stack-c

# sources
SRCS    :=  src/transform_stack.c

# object files, dep files
OBJS    := $(SRCS:.c=.o)
DEPS    := $(SRCS:.c=.dep)
XDEPS   := $(wildcard $(DEPS))

# get standard PolySync build resources
include $(PSYNC_HOME)/build_res.mk

# compiler
CC = gcc

#
all: dirs $(TARGET)

#
ifneq ($(XDEPS),)
include $(XDEPS)
endif

# directories
dirs::
	mkdir -p bin

#
$(TARGET): $(OBJS)
	$(CC) $(LDFLAGS) $(INCLUDE) -o $@ $^ $(LIBS)

#
$(OBJS): %.o: %.c %.dep
	$(CC) $(CCFLAGS) $(INCLUDE) -o $@ -c $<

#
$(DEPS): %.dep: %.c Makefile
	$(CC) $(CCFLAGS) $(INCLUDE) -MM $< > $@

# install to system
install: all
	cp $(TARGET) $(PSYNC_HOME)/bin/

#
clean:
	-rm -f src/*.o
	-rm -f src/*.dep
	-rm -f $(TARGET)
	-rm -f bin/*
	-rm -rf ospl-*.log
