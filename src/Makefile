
UNAME := $(shell uname)
ifeq ($(UNAME),Darwin)
	SHAREDEXT := .dylib
	EXTRAFLAGS :=
	SHAREDFLAGS := -dynamiclib
else
	SHAREDEXT := .so
	EXTRAFLAGS := -fPIC
	SHAREDFLAGS := -shared
endif

CFLAGS = $(EXTRAFLAGS) -std=c99 -Wall -Werror -O3 -g

CUTEST_OBJS = cutest.o cutest_assert.o
CUTEST_HEADERS = cutest.h cutest_assert.h


all:
	@echo "Use"
	@echo "    make test"
	@echo "or"
	@echo "    make clean"
	@echo "or"
	@echo "    make sharedlib"
	@echo "or"
	@echo "    make install"
	@echo

sharedlib: libcutest$(SHAREDEXT)

libcutest$(SHAREDEXT): $(CUTEST_OBJS)
	gcc $(SHAREDFLAGS) $(CUTEST_OBJS) -o libcutest$(SHAREDEXT)

install: libcutest$(SHAREDEXT) $(CUTEST_HEADERS)
	cp libcutest$(SHAREDEXT) /usr/local/lib
	cp cutest.h cutest_assert.h /usr/local/include/

cutest_assert.h cutest_assert.c: generate_cutest_assert.py
	python generate_cutest_assert.py

test:
	@echo Sorry, no tests yet.  How ironical.

clean:
	rm -rf $(CUTEST_OBJS)
	rm -rf cutest_assert.c cutest_assert.h

$(CUTEST_OBJS): $(CUTEST_HEADERS) cutest_assert.c
