CC ?= gcc

CFLAGS	= -std=c11 -Wall -Wextra -Wpedantic -Werror -g
LDFLAGS = -Wl,--as-needed -Wl,--no-undefined

OUTPUT_DIR ?= .

SRCS		= main.c
OBJS		= $(SRCS:.c=.o)
TARGET		= $(OUTPUT_DIR)/exercise-05

LIB_NAME	= libfunctions.so
LIB_TARGET	= $(OUTPUT_DIR)/$(LIB_NAME)
LIB_SRC		= functions.c
LIB_OBJ		= $(LIB_SRC:.c=.o)
RPATH		=  -Wl,-rpath,'$$ORIGIN'

TEST_SRCS	= test.c functions.c
TEST_OBJS	= $(TEST_SRCS:.c=.o)
TEST_TARGET = $(OUTPUT_DIR)/exercise-05_test

all: $(TARGET) test

$(OUTPUT_DIR):
	mkdir -p $(OUTPUT_DIR)

$(LIB_OBJ): $(LIB_SRC)
	$(CC) -fPIC $(CFLAGS) -c -o $@ $<

$(LIB_TARGET): $(LIB_OBJ)
	$(CC) -shared -o $@ $<

$(TARGET): $(OBJS) $(LIB_TARGET)
	$(CC) $(LDFLAGS) -o $@ $(OBJS) -L$(OUTPUT_DIR) -lfunctions $(RPATH)

$(TEST_TARGET): $(TEST_OBJS) $(LIB_TARGET)
	$(CC) $(LDFLAGS) -o $@ $(TEST_OBJS) -L$(OUTPUT_DIR) -lfunctions $(RPATH)

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

test: $(TEST_TARGET)
	$(TEST_TARGET)

clean:
	rm -f $(LIB_TARGET) $(TARGET) $(TEST_TARGET) $(OBJS) $(LIB_OBJ) $(TEST_OBJS)
