# Compiler und Flags
CC = /usr/bin/g++
CFLAGS = -Wall -std=c++11 -g

# Architektur-Flags für Universal Binary
ARCHS = -arch x86_64 -arch arm64

# Programme & Quellcode
BINARY1 = cputhrottle
SRCS1 = cputhrottle.cc manip.cc
OBJS1 = $(SRCS1:.cc=.o)

BINARY2 = test
SRCS2 = test.cc
OBJS2 = $(SRCS2:.cc=.o)

# Default-Ziel
all: $(BINARY1) $(BINARY2)

# Regel für .o-Dateien als FAT-Objekte (Universal Binary)
%.o: %.cc
	@echo "Compiling $< as universal binary..."
	@$(CC) $(CFLAGS) -c -arch x86_64 $< -o $*.x86_64.o
	@$(CC) $(CFLAGS) -c -arch arm64 $< -o $*.arm64.o
	@lipo -create -output $@ $*.x86_64.o $*.arm64.o
	@rm -f $*.x86_64.o $*.arm64.o

# Linken
$(BINARY1): $(OBJS1)
	$(CC) $(CFLAGS) $(ARCHS) -o $@ $(OBJS1)

$(BINARY2): $(OBJS2)
	$(CC) $(CFLAGS) $(ARCHS) -o $@ $(OBJS2)

# Aufräumen
clean:
	rm -f *.o *.x86_64.o *.arm64.o $(BINARY1) $(BINARY2)
