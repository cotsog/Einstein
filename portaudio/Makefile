#
# PortAudio V19 Makefile.in
#
# Dominic Mazzoni
#

PREFIX = /usr/local
CC = gcc
CFLAGS = -g -O2 -Wall -pedantic -pipe -fPIC -DPA_BIG_ENDIAN  -Ipa_common -DPACKAGE_NAME=\"\" -DPACKAGE_TARNAME=\"\" -DPACKAGE_VERSION=\"\" -DPACKAGE_STRING=\"\" -DPACKAGE_BUGREPORT=\"\" -DWORDS_BIGENDIAN=1 -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DSIZEOF_SHORT=2 -DSIZEOF_INT=4 -DSIZEOF_LONG=4 -DPA_USE_COREAUDIO=1 
LIBS = -framework CoreAudio -framework AudioToolbox -framework AudioUnit -framework Carbon
AR = /usr/bin/ar
RANLIB = ranlib
INSTALL = /opt/local/bin/ginstall -c
SHARED_FLAGS = -framework CoreAudio -framework AudioToolbox -framework AudioUnit -framework Carbon -dynamiclib
DLL_LIBS = 
CXXFLAGS = 
NASM = 
NASMOPT = 

OTHER_OBJS = pa_mac/pa_mac_hostapis.o pa_unix/pa_unix_util.o pa_mac_core/pa_mac_core.o

PALIB = libportaudio.a
PADLL = libportaudio.dylib
PADLLV_MIN = 19
PADLLV = 0.0.19
PADLLEXT = 
PASHLIBNAME = $(PADLL).$(PADLLV)$(PADLLEXT)
PAINC = pa_common/portaudio.h

COMMON_OBJS = \
	pa_common/pa_allocation.o \
	pa_common/pa_converters.o \
	pa_common/pa_cpuload.o \
	pa_common/pa_dither.o \
	pa_common/pa_front.o \
	pa_common/pa_process.o \
	pa_common/pa_skeleton.o \
	pa_common/pa_stream.o \
	pa_common/pa_trace.o

TESTS = \
	bin/paqa_devs \
	bin/paqa_errs \
	bin/patest1 \
	bin/patest_buffer \
	bin/patest_callbackstop \
	bin/patest_clip \
	bin/patest_dither \
	bin/patest_hang \
	bin/patest_in_overflow \
	bin/patest_latency \
	bin/patest_leftright \
	bin/patest_longsine \
	bin/patest_many \
	bin/patest_maxsines \
	bin/patest_multi_sine \
	bin/patest_out_underflow \
	bin/patest_pink \
	bin/patest_prime \
	bin/patest_read_record \
	bin/patest_record \
	bin/patest_ringmix \
	bin/patest_saw \
	bin/patest_sine8 \
	bin/patest_sine \
	bin/patest_sine_formats \
	bin/patest_sine_time \
	bin/patest_start_stop \
	bin/patest_stop \
	bin/patest_sync \
	bin/patest_toomanysines \
	bin/patest_underflow \
	bin/patest_wire \
	bin/patest_write_sine \
	bin/pa_devs \
	bin/pa_fuzz \
	bin/pa_minlat

# Most of these don't compile yet.  Put them in TESTS, above, if
# you want to try to compile them...
ALL_TESTS = \
	bin/debug_convert \
	bin/debug_dither_calc \
	bin/debug_dual \
	bin/debug_multi_in \
	bin/debug_multi_out \
	bin/debug_record \
	bin/debug_record_reuse \
	bin/debug_sine_amp \
	bin/debug_sine \
	bin/debug_sine_formats \
	bin/debug_srate \
	bin/debug_test1 \
	bin/pa_devs \
	bin/pa_fuzz \
	bin/pa_minlat \
	bin/paqa_devs \
	bin/paqa_errs \
	bin/patest1 \
	bin/patest_buffer \
	bin/patest_clip \
	bin/patest_dither \
	bin/patest_hang \
	bin/patest_in_overflow \
	bin/patest_latency \
	bin/patest_leftright \
	bin/patest_longsine \
	bin/patest_many \
	bin/patest_maxsines \
	bin/patest_multi_sine \
	bin/patest_out_underflow \
	bin/patest_pink \
	bin/patest_read_record \
	bin/patest_record \
	bin/patest_ringmix \
	bin/patest_saw \
	bin/patest_sine8 \
	bin/patest_sine \
	bin/patest_sine_formats \
	bin/patest_sine_time \
	bin/patest_start_stop \
	bin/patest_stop \
	bin/patest_sync \
	bin/patest_toomanysines \
	bin/patest_underflow \
	bin/patest_wire \
	bin/patest_write_sine

OBJS = $(COMMON_OBJS) $(OTHER_OBJS)

all: lib/$(PALIB) lib/$(PASHLIBNAME) tests

tests: bin/ $(TESTS)

lib/$(PALIB): lib/ $(OBJS) Makefile $(PAINC)
	$(AR) ruv lib/$(PALIB) $(OBJS)
	$(RANLIB) lib/$(PALIB)

lib/$(PASHLIBNAME): lib/ $(OBJS) Makefile $(PAINC)
	$(CC) $(SHARED_FLAGS) -o lib/$(PASHLIBNAME) $(OBJS) $(DLL_LIBS) -install_name $(PREFIX)/lib/$(PASHLIBNAME) -compatibility_version $(PADLLV) -current_version $(PADLLV)

$(TESTS): bin/%: lib/$(PALIB) Makefile $(PAINC) pa_tests/%.c
	$(CC) -o $@ $(CFLAGS) pa_tests/$*.c lib/$(PALIB) $(LIBS)

install: lib/$(PALIB) lib/$(PASHLIBNAME) portaudio-2.0.pc
	$(INSTALL) -d $(PREFIX)/lib
	$(INSTALL) -m 644 lib/$(PASHLIBNAME) $(PREFIX)/lib/$(PASHLIBNAME)
	$(INSTALL) -m 644 lib/$(PALIB) $(PREFIX)/lib/$(PALIB)
	cd $(PREFIX)/lib && rm -f $(PADLL)$(PADLLEXT) && ln -s $(PASHLIBNAME) $(PADLL)$(PADLLEXT)
	$(INSTALL) -d $(PREFIX)/include
	$(INSTALL) -m 644 pa_common/portaudio.h $(PREFIX)/include/portaudio.h
	$(INSTALL) -d $(PREFIX)/lib/pkgconfig
	$(INSTALL) -m 644 portaudio-2.0.pc $(PREFIX)/lib/pkgconfig/portaudio-2.0.pc
	@echo ""
	@echo "------------------------------------------------------------"
	@echo "PortAudio was successfully installed."
	@echo ""
	@echo "On some systems (e.g. Linux) you should run 'ldconfig' now"
	@echo "to make the shared object available.  You may also need to"
	@echo "modify your LD_LIBRARY_PATH environment variable to include"
	@echo "the directory $(PREFIX)/lib"
	@echo "------------------------------------------------------------"
	@echo ""

uninstall:
	rm -f $(PREFIX)/lib/$(PASHLIBNAME)
	rm -f $(PREFIX)/lib/$(PALIB)
	rm -f $(PREFIX)/lib/$(PADLL)$(PADLLEXT)
	rm -f $(PREFIX)/include/portaudio.h

clean:
	rm -f $(OBJS) $(TESTS) lib/$(PALIB) lib/$(PASHLIBNAME)

%.o: %.c Makefile $(PAINC)
	$(CC) -c $(CFLAGS) $< -o $@

%.o: %.cpp Makefile $(PAINC)
	$(CXX) -c $(CXXFLAGS) $< -o $@

%.o: %.asm
	$(NASM) $(NASMOPT) -o $@ $<

bin:
	mkdir bin

lib:
	mkdir lib



