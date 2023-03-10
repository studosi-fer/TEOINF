CC=			g++
CFLAGS=		-c -Wall -O3
LINKFLAGS=

SRC_DIR=src

SOURCE_SRC_DIR=		${SRC_DIR}/gen/source
SOURCE_MAIN=		izvor.cpp
SOURCE_BIN=			izvor.exe
SOURCE_OBJ=			source.o

SOURCE_CODER_SRC_DIR=	${SRC_DIR}/huffman/coder
SOURCE_CODER_MAIN=	ent_kod.cpp
SOURCE_CODER_BIN=	ent_kod.exe
SOURCE_CODER_OBJ=	source-coder.o

CHANNEL_CODER_SRC_DIR=	${SRC_DIR}/hamming/coder
CHANNEL_CODER_MAIN=	z_kod.cpp
CHANNEL_CODER_BIN=	z_kod.exe
CHANNEL_CODER_OBJ=	channel-coder.o

CHANNEL_SCRAMBLER_SRC_DIR=	${SRC_DIR}/gen/channel-scrambler
CHANNEL_SCRAMBLER_MAIN=		gen_pogreske.cpp
CHANNEL_SCRAMBLER_BIN=		gen_pogreske.exe
CHANNEL_SCRAMBLER_OBJ=		channel-scrambler.o

CHANNEL_SRC_DIR=	${SRC_DIR}/channel
CHANNEL_MAIN=		kanal.cpp
CHANNEL_BIN=		kanal.exe
CHANNEL_OBJ=	channel.o

CHANNEL_DECODER_SRC_DIR=${SRC_DIR}/hamming/decoder
CHANNEL_DECODER_MAIN=	z_dekod.cpp
CHANNEL_DECODER_BIN=	z_dekod.exe
CHANNEL_DECODER_OBJ=	channel-decoder.o

DEST_DECODER_SRC_DIR=	${SRC_DIR}/huffman/decoder
DEST_DECODER_MAIN=	ent_dekod.cpp
DEST_DECODER_BIN=	ent_dekod.exe
DEST_DECODER_OBJ=	destination-decoder.o

ANALYSIS_SRC_DIR=	$(SRC_DIR)/analysis
ANALYSIS_MAIN=		analiza.cpp
ANALYSIS_BIN=		analiza.exe
ANALYSIS_OBJ=		analysis.o

RUN_ALL_BIN=		runall.bat
DELETE_TXT=			delete-txt.bat

# All
all: $(RUN_ALL_BIN)

# All
$(RUN_ALL_BIN): $(SOURCE_BIN) $(SOURCE_CODER_BIN) $(CHANNEL_SCRAMBLER_BIN) $(CHANNEL_BIN) $(CHANNEL_CODER_BIN) $(CHANNEL_DECODER_BIN) $(DEST_DECODER_BIN) $(ANALYSIS_BIN)
	echo '#!/bin/sh' > $(RUN_ALL_BIN)
	echo './${SOURCE_BIN}' >> $(RUN_ALL_BIN)
	echo './${SOURCE_CODER_BIN} 12.txt' >> $(RUN_ALL_BIN)
	echo './${CHANNEL_CODER_BIN} 23.txt' >> $(RUN_ALL_BIN)
	echo './${CHANNEL_SCRAMBLER_BIN} 34.txt' >> $(RUN_ALL_BIN)
	echo './${CHANNEL_BIN} 34.txt err_vec.txt' >> $(RUN_ALL_BIN)
	echo './${CHANNEL_DECODER_BIN} 45.txt' >> $(RUN_ALL_BIN)
	echo './${DEST_DECODER_BIN} 56.txt' >> $(RUN_ALL_BIN)
	echo './${ANALYSIS_BIN} 12.txt 67.txt' >> $(RUN_ALL_BIN)
	chmod +x $(RUN_ALL_BIN)
	
	echo '#!/bin/sh' > $(DELETE_TXT)
	echo 'rm -f 12.txt 23.txt 34.txt 45.txt 56.txt 67.txt err_vec.txt' > $(DELETE_TXT)
	chmod +x $(DELETE_TXT)
	
# Svojstva izvora
source_properties.o: $(SRC_DIR)/source_properties.cpp $(SRC_DIR)/source_properties.h
	$(CC) $(CFLAGS) -o source_properties.o ${SRC_DIR}/source_properties.cpp

# Izvor
$(SOURCE_BIN): $(SOURCE_OBJ) source_properties.o
	$(CC) $(LINKFLAGS) -o $(SOURCE_BIN) $(SOURCE_OBJ) source_properties.o
$(SOURCE_OBJ): ${SOURCE_SRC_DIR}/$(SOURCE_MAIN) ${SOURCE_SRC_DIR}/*.h ${SOURCE_SRC_DIR}/../*.h ${SOURCE_SRC_DIR}/../../*.h
	$(CC) $(CFLAGS) -o $(SOURCE_OBJ) ${SOURCE_SRC_DIR}/$(SOURCE_MAIN)

# Entropijski koder
$(SOURCE_CODER_BIN): $(SOURCE_CODER_OBJ) source_properties.o
	$(CC) $(LINKFLAGS) -o $(SOURCE_CODER_BIN) $(SOURCE_CODER_OBJ) source_properties.o
$(SOURCE_CODER_OBJ): $(SOURCE_CODER_SRC_DIR)/$(SOURCE_CODER_MAIN) $(SOURCE_CODER_SRC_DIR)/*.h $(SOURCE_CODER_SRC_DIR)/../*.h $(SOURCE_CODER_SRC_DIR)/../../*.h
	$(CC) $(CFLAGS) -o $(SOURCE_CODER_OBJ) $(SOURCE_CODER_SRC_DIR)/$(SOURCE_CODER_MAIN)
	
# Zastitni koder
$(CHANNEL_CODER_BIN): $(CHANNEL_CODER_OBJ)
	$(CC) $(LINKFLAGS) -o $(CHANNEL_CODER_BIN) $(CHANNEL_CODER_OBJ)
$(CHANNEL_CODER_OBJ): $(CHANNEL_CODER_SRC_DIR)/$(CHANNEL_CODER_MAIN) $(CHANNEL_CODER_SRC_DIR)/../*.h $(CHANNEL_CODER_SRC_DIR)/../../*.h
	$(CC) $(CFLAGS) -o $(CHANNEL_CODER_OBJ) $(CHANNEL_CODER_SRC_DIR)/$(CHANNEL_CODER_MAIN)

# Kanal
$(CHANNEL_SCRAMBLER_BIN): $(CHANNEL_SCRAMBLER_OBJ)
	$(CC) $(LINKFLAGS) -o $(CHANNEL_SCRAMBLER_BIN) $(CHANNEL_SCRAMBLER_OBJ)
$(CHANNEL_SCRAMBLER_OBJ): $(CHANNEL_SCRAMBLER_SRC_DIR)/$(CHANNEL_SCRAMBLER_MAIN) $(CHANNEL_SCRAMBLER_SRC_DIR)/../*.h $(CHANNEL_SCRAMBLER_SRC_DIR)/../../*.h
	$(CC) $(CFLAGS) -o $(CHANNEL_SCRAMBLER_OBJ) $(CHANNEL_SCRAMBLER_SRC_DIR)/$(CHANNEL_SCRAMBLER_MAIN)

# Kanal
$(CHANNEL_BIN): $(CHANNEL_OBJ)
	$(CC) $(LINKFLAGS) -o $(CHANNEL_BIN) $(CHANNEL_OBJ)
$(CHANNEL_OBJ): $(CHANNEL_SRC_DIR)/$(CHANNEL_MAIN) $(CHANNEL_SRC_DIR)/../*.h
	$(CC) $(CFLAGS) -o $(CHANNEL_OBJ) $(CHANNEL_SRC_DIR)/$(CHANNEL_MAIN)

# Zastitno dekodiranje
$(CHANNEL_DECODER_BIN): $(CHANNEL_DECODER_OBJ)
	$(CC) $(LINKFLAGS) -o $(CHANNEL_DECODER_BIN) $(CHANNEL_DECODER_OBJ)
$(CHANNEL_DECODER_OBJ): $(CHANNEL_DECODER_SRC_DIR)/$(CHANNEL_DECODER_MAIN) $(CHANNEL_DECODER_SRC_DIR)/../*.h $(CHANNEL_DECODER_SRC_DIR)/../../*.h
	$(CC) $(CFLAGS) -o $(CHANNEL_DECODER_OBJ) $(CHANNEL_DECODER_SRC_DIR)/$(CHANNEL_DECODER_MAIN)
	
# Entropijsko dekodiranje
$(DEST_DECODER_BIN): $(DEST_DECODER_OBJ) source_properties.o
	$(CC) $(LINKFLAGS) -o $(DEST_DECODER_BIN) $(DEST_DECODER_OBJ) source_properties.o
$(DEST_DECODER_OBJ): $(DEST_DECODER_SRC_DIR)/$(DEST_DECODER_MAIN) $(DEST_DECODER_SRC_DIR)/*.h $(DEST_DECODER_SRC_DIR)/../*.h $(DEST_DECODER_SRC_DIR)/../../*.h
	$(CC) $(CFLAGS) -o $(DEST_DECODER_OBJ) $(DEST_DECODER_SRC_DIR)/$(DEST_DECODER_MAIN)

# Analiza
$(ANALYSIS_BIN): $(ANALYSIS_OBJ) source_properties.o
	$(CC) $(LINKFLAGS) -o $(ANALYSIS_BIN) $(ANALYSIS_OBJ) source_properties.o
$(ANALYSIS_OBJ): $(ANALYSIS_SRC_DIR)/$(ANALYSIS_MAIN) $(ANALYSIS_SRC_DIR)/../*.h
	$(CC) $(CFLAGS) -o $(ANALYSIS_OBJ) $(ANALYSIS_SRC_DIR)/$(ANALYSIS_MAIN)

clean:
	rm -f *.o ${SOURCE_BIN} $(SOURCE_CODER_BIN) $(CHANNEL_CODER_BIN) $(CHANNEL_SCRAMBLER_BIN) $(CHANNEL_BIN) $(CHANNEL_DECODER_BIN) $(DEST_DECODER_BIN) $(ANALYSIS_BIN) $(RUN_ALL_BIN) $(DELETE_TXT) 
	
