ifeq ($(COMP),)
COMP=gnu
endif

COMMONDIR=../../common

ifeq ($(COMP),gnu)
CXX=g++
CC=gcc
CCFLAGS=-g -O3 -march=native -Wall -I$(COMMONDIR) -DNDEBUG -fopenmp
LDFLAGS=
LIBS=-lpng
endif

ifeq ($(COMP),intel)
CXX=icpc
CC=icc
CCFLAGS=-g -O3 -xHost -I$(COMMONDIR) -DNDEBUG -fopenmp
LDFLAGS=
LIBS=-lpng
endif

EXE=heat_omp
OBJS=main.o heat.o core.o setup.o io.o utilities.o
OBJS_PNG=$(COMMONDIR)/pngwriter.o


all: $(EXE)


utilities.o: utilities.cpp heat.hpp
heat.o: heat.cpp heat.hpp matrix.hpp
core.o: core.cpp heat.hpp
setup.o: setup.cpp heat.hpp
io.o: io.cpp heat.hpp matrix.hpp
main.o: main.cpp heat.hpp

$(OBJS_PNG): C_COMPILER := $(CC)
$(OBJS): C_COMPILER := $(CXX)

$(EXE): $(OBJS) $(OBJS_PNG)
	$(CXX) $(CCFLAGS) $(OBJS) $(OBJS_PNG) -o $@ $(LDFLAGS) $(LIBS)

%.o: %.cpp
	$(CXX) $(CCFLAGS) -c $< -o $@

%.o: %.c
	$(CC) $(CCFLAGS) -c $< -o $@

.PHONY: clean
clean:
	-/bin/rm -f $(EXE) a.out *.o *.png *~
