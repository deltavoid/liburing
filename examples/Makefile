CFLAGS ?= -g -O2
XCFLAGS =
override CFLAGS += -Wall -D_GNU_SOURCE -L../src/ -I../src/include/

include ../Makefile.quiet

ifneq ($(MAKECMDGOALS),clean)
include ../config-host.mak
endif

all_targets += io_uring-test io_uring-cp link-cp ucontext-cp

all: $(all_targets)

test_srcs := io_uring-test.c io_uring-cp.c link-cp.c

test_objs := $(patsubst %.c,%.ol,$(test_srcs))

%: %.c
	$(QUIET_CC)$(CC) $(CFLAGS) -o $@ $< -luring $(XCFLAGS)

clean:
	@rm -f $(all_targets) $(test_objs)


run_io_uring_test: io_uring-test
	./$< infile1.txt

run_io_uring_cp: io_uring-cp
	./$< infile1.txt outfile1.txt

run_link_cp: link-cp
	./$< infile1.txt outfile1.txt

run_ucontext_cp: ucontext-cp
	./$<  infile1.txt outfile1.txt infile2.txt outfile2.txt