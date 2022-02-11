ccomp?=gcc
cflags=-fopenmp -O3 -D__HIP_PLATFORM_AMD__
cexec=many-small-dgemms-amd.x
csources=many-small-dgemms-amd.c
cobjects=${patsubst %.c,%.c.obj, $(csources)}
incl=-I$(OLCF_OPENBLAS_ROOT)/include -I$(HIP_PATH)/include -I$(ROCM_PATH)/include -I$(OLCF_MAGMA_ROOT)/include
clibs=-L$(OLCF_OPENBLAS_ROOT)/lib -lopenblas
clibs+=-L$(OLCF_MAGMA_ROOT)/lib -lmagma
clibs+=-L$(ROCM_PATH)/lib -lrocblas
clibs+=-L$(HIP_PATH)/lib -lamdhip64

main: $(cexec)

$(cexec): $(cobjects)
	$(ccomp) $(cflags) -g $(clibs) -o $(cexec) $(cobjects)

%.c.obj: %.c
	$(ccomp) $(cflags) $(incl) -g -c -o $@ $<

clean:
	rm *.o *.c.obj $(cexec)

