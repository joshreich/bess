ifneq ($(wildcard $(RTE_SDK)/$(RTE_TARGET)*),)
	DPDK_INC_DIR = $(RTE_SDK)/$(RTE_TARGET)/include
	DPDK_LIB_DIR = $(RTE_SDK)/$(RTE_TARGET)/lib
else
	DPDK_INC_DIR = $(RTE_SDK)/build/include
	DPDK_LIB_DIR = $(RTE_SDK)/build/lib
endif

DPDK_LIBS = -L$(DPDK_LIB_DIR)
DPDK_LIBS += -lintel_dpdk

LIBS = -ldl -lpthread -lm

SN_LIBS = -L../ -lsn

CC = gcc
CFLAGS = -std=gnu99 -Wall -Werror -march=native -Wno-unused-function -Wno-unused-but-set-variable -I../sndrv -I../ -fPIC -g3 -O3 

all: sample sink source fastforward sourcesink alloc_test iso_test 
clean:
	rm -f *.o *.a *.so sample sink source fastforward sourcesink iso_test alloc_test

sample.o: sample.c
	$(CC) $(CFLAGS) -c $< -o $@ $(CFLAGS) -I$(DPDK_INC_DIR) 

sample: sample.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)

sourcesink.o: sourcesink.c
	$(CC) $(CFLAGS) -c $< -o $@ $(CFLAGS) -I$(DPDK_INC_DIR)

sourcesink: sourcesink.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)

sink.o: sink.c 
	$(CC) $(CFLAGS) -c $< -o $@ -I$(DPDK_INC_DIR)

sink: sink.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)

source.o: source.c 
	$(CC) $(CFLAGS) -c $< -o $@ -I$(DPDK_INC_DIR)

source: source.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)

fastforward.o: fastforward.c 
	$(CC) $(CFLAGS) -c $< -o $@ -I$(DPDK_INC_DIR)

fastforward: fastforward.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)

alloc_test.o: alloc_test.c 
	$(CC) $(CFLAGS) -c $< -o $@ -I$(DPDK_INC_DIR)

alloc_test: alloc_test.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)

iso_test.o: iso_test.c 
	$(CC) $(CFLAGS) -c $< -o $@ -I$(DPDK_INC_DIR)

iso_test: iso_test.o 
	$(CC) $< -o $@ -L. -Wl,--whole-archive $(SN_LIBS) $(DPDK_LIBS) -Wl,--no-whole-archive $(LIBS)
